# Agentic Engineering Past the Pilot: An Enterprise Playbook

## Summary
### Context and the Productivity Gap
- GitHub saw 236M commits/week at Universe 2025
- Last week: 1.25B commits, a ~6x increase (over 400% growth)
- But the room does not feel 400% more productive: activity growth ≠ outcome growth
- Root cause: the bottleneck has shifted from code generation to verification
  - Pharos AI study: 400%+ increase in median PR review time
  - More PRs going unreviewed entirely
- The real gap: planning, spec, ADR authoring, and review are still slow
- Goal reframe: not “agentic coding,” but **agentic engineering** across the full SDLC

### Integrate ADR Info Into Notes for Structure of Workflows
- The old way: meeting → Slack → issues (often empty) → ADR → review → sign-off → days lost before a line of code is written
- The new way: same stakeholders, different tooling
  - Transcription on during the meeting (in-person or remote)
  - PM opens Copilot session post-meeting, pulls transcript, validates assumptions against BI (Fabric, observability tools)
  - Copilot opens and fills tracking issues automatically (GitHub Issues, Jira, Azure DevOps all supported)
  - GitHub Agentic Workflows (GA today) triages each issue: maps to affected app areas, applies t-shirt size complexity estimate
  - Small/XS issues auto-assigned to Copilot for implementation; team focuses on complex work
  - WorkIQ + Fabric integration into Slack/Teams launching today: pulls meeting notes and validates them automatically
- ADR pattern preserved: planning, alternatives analysis, and sign-off still happen, just faster and with agent support
- Key principle: agentic engineering does not skip planning; writing software is still a team sport

### Implementation: Parallel Agents and Cross-Device Sessions
- Old model: single-threaded agent in VS Code, risk of agents tripping over each other in the same repo
- New model: Copilot app isolates a copy of the repo per session, all sessions run fully in parallel
- Sessions are continuous across surfaces: start on desktop, continue on phone, CLI, VS Code, or cloud agent
  - Highlighted as a favorite Universe release: inspiration strikes anywhere (2am, middle seat on a plane)
- Three new capabilities powering every agent session, all GA today:
  - **Memory**: agent memories tied to the repository, shared instantly across every developer on the project (not locked to one machine)
  - **Dreaming**: continuous learning loop; analyzes sessions, PRs, issues, and conversations to create new memories, prune stale ones, and suggest improvements to skills and code review standards
  - **Fusion**: automatic model selection (pricing + quality); developers stop choosing models manually and stop burning credits on the wrong one; ~half the price with quality maintained
- Cloud Sandboxes (microVMs): agent sessions run in the cloud, spin up near-instantly, shareable across teammates, isolated from local sensitive data
  - Prediction on record: 2027 will finally be the year of the cloud developer environment

### Unified Harness Across All Surfaces
- CLI, VS Code, JetBrains, Xcode now all run on the same underlying harness
- Benefit for developers: same Copilot experience and capabilities regardless of tool
- Benefit for admins: single policy configuration applies everywhere via enterprise-managed settings
  - No more per-surface policy gaps (e.g., JetBrains previously missing some controls)
- Memory, Dreaming, and Cloud Sandboxes automatically available across all products via the unified harness

### Verification and Code Review
- Monster PRs are the new bottleneck: 8,000-line diffs, reviewers assigned to one schema buried inside
- Stacked PRs (GA now): agents stack changes logically (data layer → API → map service → docs); unblocks dependent teams immediately
- GitHub Code Quality (GA today): enforces good practices and org-configured standards on every PR
- Copilot Code Review: tunable analysis depth
  - Light: fast, high-churn PRs
  - Balanced: standard
  - Max: deep analysis for large/complex PRs (as seen in keynote)
  - Auto mode shipping soon: Copilot automatically selects the right tier per PR

### AI Secret Detection and Supply-Chain Controls
- Secret scanning shipping as GA, surfaced directly in pull requests
- Package firewall also shipping as GA: protects against dependency/supply chain risks
- Goal: agents and humans held to the same code quality and security standards
- Delegating PR management to Copilot highlighted as one of the highest-value use cases seen internally at GitHub

### Next Steps
- **Review Fusion blog post for pricing and quality benchmarks**
  Published this morning alongside Universe; contains stats on cost reduction and model quality tradeoffs.
- **Explore WorkIQ and Fabric integration in Slack/Teams**
  Launched today; automates meeting note pull and assumption validation against BI data.
- **Evaluate GitHub Agentic Workflows and Code Quality for current pipeline**
  Both GA today; assess fit for issue triage, auto-assignment, and PR quality enforcement.

## Enhanced Notes

### Enterprise Conversation: Move From Pilot to Governed Delivery
- Map the current delivery workflow before introducing agents: identify where planning, review, testing, security approval, or environment access creates measurable delays.
- Use agents to prepare, not replace, architecture decision records. Require a concise problem statement, constraints, alternatives considered, impact analysis, decision owner, and unresolved risks; keep the accountable human approval before implementation begins.
- Pilot parallel agents in isolated workspaces and establish repository-level boundaries for write access, network egress, data access, and credential issuance. Treat isolation as a control to validate, not an assurance by itself.
- Define a verification policy by change risk: expected tests and scans, reviewer responsibility, escalation rules, and explicit conditions that prevent automated merge.
- Evaluate Memory, Dreaming, and model routing for data retention, access scope, change review, quality, latency, and cost. Review suggested context changes as code and provide a way to reject or roll them back.
- Baseline the bottleneck before scaling: track PR review time, unreviewed PRs, change failure rate, rework, lead time, and spend per successfully delivered change. Validate conference-reported results in the organization’s own environment.
- Treat AI-assisted secret detection as one layer in defense in depth. Validate supported credential types, detection coverage, false-positive handling, alert latency, and the remediation path; retain push protection, secret scanning, credential rotation, and incident response controls.
- Apply equivalent security gates to agent-authored and human-authored changes. Require dependency and secret checks on proposed changes, and ensure any automated remediation still receives normal test and review evidence.
