# Treat your AI Context as Infrastructure

### The Context Problem in Enterprise AI
- Consumer AI benefits from implicit context: one word like “Winamp” carries enormous shared knowledge
- Enterprise dev has no equivalent shorthand: agents must infer architecture, conventions, and intent from scratch
- Common mistake: giving Copilot access to the entire codebase
  - Copilot can’t distinguish good code from legacy code, and mirrors both
  - Internal case study: Copilot Code Review given broad CLI and cert file access
    - Result: slower, more expensive, worse output
  - Fix: scope context tightly, guide the traversal path (start here, follow the call tree)

### The Five Context Primitives
- **Instructions files**: low-level coding standards (formatting, style, conventions)
  - Two formats: copilot-instructions.md (global) and .instructions.md files with path globs
  - Copilot also reads agents.md, claude.md, gemini.md if already in use
  - Folder-scoped: root applies globally, subdirectory files apply locally
- **Skills**: reusable task definitions (run tests, generate forecasts)
  - Name becomes a slash command; description lets Copilot invoke dynamically
  - Loaded only when relevant, keeping context lean
- **Custom agents**: orchestrators for specific workflows
  - Can override instructions when working in a different mode or context
- **Hooks**: lifecycle triggers (on start, post-plan, on complete)
  - Good for formatters, linters, and build steps that must run at exact moments
- **MCP servers**: external resource connectors
  - Credentials scoped to the server, not the developer’s personal token
  - Connectors tie auth to the account once, available across all surfaces
  - Can build custom MCP servers via Copilot itself (essentially just a web endpoint)

### Shipping and Governing Context at Scale
- **Plugins**: bundle instructions, skills, agents, and MCP configs into a distributable unit
- **Marketplace**: a repository/folder of approved plugins developers can pull from
- Governance controls at three levels:
  - Repository: default scope for instructions and skills
  - Organization: shared agents, org-level instructions
  - Enterprise: shared agents, managed settings (permitted MCP servers, default model)
- Default model setting: prevents developers from accidentally running expensive models on trivial tasks
- Enable plugin setting: push a plugin to the entire org without requiring manual setup

### Keeping Context Accurate Over Time
- Treat context like code: review PRs to instruction files as carefully as production code
- Eval loop: write a realistic test, define expected output, review Copilot’s result, update, repeat
- **Copilot Drift** (tool): monitors instruction files and code, raises PRs when updates are needed
  - Learns from accepted PR comments and patterns
  - Also updates memories; memories have an internal upvote mechanism to surface what’s working
- **VALVE**: executor that runs the agent and generates insight reports on what Copilot is doing and why
  - Useful for validating whether instructions files and custom agents are actually helping
- Developer upskilling is non-negotiable: Copilot is optional to use well, so training must be pervasive and ongoing
- Lightweight adoption metric: ask developers what their barriers are, implement fixes, then re-evaluate

### Enhanced Notes

#### Enterprise Conversation: Context Has an Owner and a Lifecycle
- Treat instructions, skills, agents, and connector configurations as governed artifacts: assign owners, review changes, version releases, document intended scope, and retire stale material.
- Classify what context may be shared with models or tools. Exclude secrets and unnecessary sensitive data; set access and retention expectations for retrieved documents, transcripts, and external connectors.
- Validate path scoping and precedence with realistic repositories so guidance is neither accidentally global nor silently ignored. Keep instructions focused and link to authoritative policy where possible.
- Build evaluation tasks around real engineering work, including known failure cases. Track whether context improves correctness, security, consistency, and task completion without increasing latency or cost unacceptably.
- Review automatically suggested memories or instruction updates before distribution. Require a diff, rationale, test evidence, and rollback path just as for other shared engineering configuration.
- Make ownership cross-functional: platform engineering maintains delivery mechanisms, security and legal review relevant policy, and application teams validate domain-specific guidance.
