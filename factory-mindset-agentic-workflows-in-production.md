# The Factory Mindset: Agentic Workflows in Production

## Private Notes
- `#How to get control plane for approve workflows?`

## Summary
### The Factory Mindset: Agentic Workflows in Production
Three speakers presented: a GitHub/Agentix team member (Speaker A), Tim Mason (Principal Engineer at Martin Spencer), and Paul Snoyder (CTO at Probation/Children’s Hospital).
Core thesis: shift from writing code to engineering the *processes* that let agents build safely and at scale. The “factory mindset” means viewing every workflow through the lens of a repeatable, improvable process.

### Agentix Framework (Speaker A)
- Genki/Agentix repo is a self-building, self-maintaining software factory
  - 700+ issues submitted by users; thousands of PRs per month
  - Over half of PRs initiated by GitHub Copilot workflows running in Actions
- Agentix is a markdown-based framework for declaring agent intent, guardrails, and security
  - Compiles markdown into GitHub Actions; runs in GitHub Cloud or self-hosted
  - Sandbox provides: zero secrets, egress filtering, scoped read/write, gating on agent writes
- PR workflow example:
  1. Issue assigned to agent, iterative loop begins
  2. Specialist reviewers check testing, docs, maintenance, code quality
  3. “Sous Chef” (Sushant) consolidates feedback and commits fixes
  4. Developer makes final merge/continue/close decision
- Daily improvement process for technical debt (“slop”)
  - Agents wake daily, find duplicate code, fix it, add tests, open a small PR for human merge
- Factory mindset reframe: if every PR requires forensic human intervention, the *process* is broken, not the code

### Tim Mason: Scaling Across 5,000 Repositories
- Problem: engineers spending significant time on toil (vulnerability updates, docs, policy changes)
  - Toil delivers no business value and engineers dislike it
- Built workflows: Vulcan plan, security audit, unit test engineer, BDD test engineer
  - Proof of concept on one large codebase: 123 issues found in one day, 77 fixed same day, test coverage rose to 90%+
- Scaling challenges addressed by the Agentic Control Plane:
  - Curated catalog of approved workflows; one-click deploy via pull request
  - Single source of truth (no stale copies across thousands of repos)
  - Per-repo configuration for different test environments
  - Token exchange endpoint: scoped tokens issued on demand, no personal access tokens needed
  - OpenTelemetry routing for visibility; failing workflows trigger investigator agents
- CI Doctor workflow: triggered on CI pipeline failure, reads logs, diagnoses, leaves comment; Sous Chef/Finisher loop prioritizes the diagnosis and gets CI back to green
  - Key decision: don’t build/run tests inside workflows; rely on existing CI pipelines to fail
- Current results (~10 days ago):
  - 200+ repos onboarded, 1,000+ control plane deployments
  - ~4,000 issues raised, 2,000+ addressed
  - 2,000+ PRs opened; 1,087 reviewer comments, 705 blocking comments fixed

### How to Get the Control Plane for Approved Workflows?
- Control plane is the application Tim’s team built at Martin Spencer
- Demo showed: connect a repo, run preflight checks, browse approved workflow catalog, one-click deploy
- Inspired heavily by Agentix/Agenti Workloads repo: “when I say inspired, I mean copy”
- Recommendation: start with the Agentix and Agenti Workloads repositories and take what you can

### Paul Snoyder: Factory in a Regulated Healthcare Environment
- Probation supports 3,300 hospital systems, 50,000 healthcare professionals, 75% of GI hospitals in the US
- Started with an existing agent harness (skills, MCPs, agents, org context) alongside developers
  - GitHub Actions lifted that same harness into automation without building a parallel AI stack
- Full SDLC automation pipeline:
  1. Ticket enters (manual or autonomous: bug hunter, test/security optimization, meeting transcripts, SRE investigations)
  2. Triage agent investigates and documents
  3. Product/requirements agent documents requirements
  4. Design agent handles architecture decisions
  5. Planning and implementation agent
  6. Test agent identifies test cases
  7. Human sign-off on SDLC evidence before a single line of code is written
  8. Copilot picks up issue, creates PR, runs review/fix loop with CI Doctor
- Grew to 71 agents, 32 trigger workflows, 6 entry points on one governed process
- Cost/value crisis: shift from seat-based to usage-based licensing in June forced them to turn it off temporarily
  - Couldn’t answer “what does this cost and what’s the value?”
  - Solution: OpenTelemetry instrumentation workflow by workflow, agent by agent
  - Reduced pipeline costs by 90% through model selection, context size, and frequency optimization
- Outcome: 2.5x more customer value delivered; new global regions, markets, applications, AI modalities
- Four takeaways:
  1. Start with trust: build on tools and vendors you already use
  2. Automate your process: understand your current SDLC, find the toil, eliminate it
  3. Lift your harness: automate the developer tools you already have
  4. Instrument before you scale: use OpenTelemetry to understand cost, quality, and value
- Memorable line: “Everyone likes to cook, no one likes doing the dishes. Let AI do the dishes.”

## Enhanced Notes

### Enterprise Conversation: The Workflow Control Plane
- Specify the control plane’s minimum capabilities before adopting or building one: approved workflow catalog, versioned templates, repository eligibility, staged rollout, policy checks, deployment status, audit history, and rollback.
- Use centrally maintained workflow definitions with explicit compatibility and ownership. Allow repository-specific configuration only through validated inputs so local variation does not silently weaken shared controls.
- Issue short-lived, narrowly scoped identities at runtime. Separate read, branch-write, issue/PR, and merge permissions; keep production credentials outside agent-accessible contexts unless a reviewed workflow requires them.
- Set deterministic boundaries for tool access, network egress, spend, execution time, retries, and human approvals. Record the workflow version, model/tool configuration, inputs, outputs, and approvals for each run.
- Define an evaluation gate for catalog admission: representative test repositories, security review, failure-mode testing, cost measurement, and a named service owner.
- Scale by cohort and measure successful completion, review effort, defect escape rate, failure recovery time, and cost per accepted change. In regulated healthcare contexts, also review data minimization, retention, access logging, and required human sign-offs.
