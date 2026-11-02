# The Low Orbit Agentic Cannon: Scaling Copilot through Internal Tooling

### The Two Problems
- Problem 1: change one file across 300 repos, each written differently
  - Manual approach: 300 PRs, coordinating 300 developers on merge timing
- Problem 2: get developers to try agentic AI without environment setup, tool purchases, or training

### Air Traffic Controller (Problem 2 Solution)
- Lives between Jira and GitHub
- On ticket creation, checks security guardrails, custom ticket types, labels, and story points
- Auto-creates GitHub issue, signs up for Code Fiverr, raises PR from normal dev workflow
- Removed friction from the dev’s existing Jira-to-refinement process

### Low Orbit Agentic Cannon (Problem 1 Solution)
- Accepts a list of repos (up to 300+), tied to a single ticket
- Pulls context from the ticket, visits each repo, creates an issue and PR, notifies the dev
- First run: CSV migration across 300+ repos completed in ~3 hours vs. 3-6 month estimate
- Second run: AI documentation generation across 216 repos, 97%+ success rate

### Failure Handling and Scaling Lessons
- “Iterative failure” cycle: start small, test before scale, repeatable execution, easy recovery
- Fixes were deliberately boring:
  - Agent stalled: retry
  - Wrong branch name: detect common variants (dev, develop, development)
  - Issues disabled: prompt dev to enable
  - Bad Jira ticket format: reparse, refix, notify dev to rewrite prompt
- Core insight: fundamentals matter more than tooling
  - Developers with 10-20 years experience still need to be shown how to describe work clearly
  - AI can help describe the work, but the requirement to describe it doesn’t go away

### GitHub Native Jira Integration and Takeaways
- GitHub shipped a native Jira integration; Air Traffic Controller is now redundant
  - Reaction: frustration at the time spent, but acknowledged the tools solved real problems at the time
- Broader lesson: don’t wait for the next model or tool to solve the problem
  - Build now, scale with internal tooling, form the habits
  - Good engineering fundamentals (SDLC basics, clear problem description) are what enable scale regardless of which tool or model is used

### Enhanced Notes

#### Enterprise Conversation: Bulk Changes Need Staged Execution
- Inventory and classify target repositories before acting: ownership, criticality, archived/fork status, default branch, language/build system, and whether the requested change applies.
- Start with a canary set that covers meaningful variations, review the resulting diffs, then expand in bounded waves with a pause/rollback decision after each wave.
- Make the coordinator idempotent and resumable. Persist per-repository state, distinguish retryable from terminal failures, respect API limits, and avoid duplicate issues or pull requests on retries.
- Use a dedicated automation identity with narrowly scoped permissions. Record the initiating request, target selection, agent/workflow version, changes proposed, checks, and human decisions.
- Keep pull requests reviewable and independently revertible; never make successful execution synonymous with approval or merge.
- Measure coverage, success and retry rates, time to accepted change, maintenance effort, and regressions by repository cohort. Compare those outcomes with the native integrations and platform capabilities available at the time of rollout.
