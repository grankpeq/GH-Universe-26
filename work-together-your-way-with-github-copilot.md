# Work Together, Your Way, With GitHub Copilot

### GitHub Copilot: One Connected Platform
- Single shared platform across VS Code, CLI, Copilot app, and GitHub.com/mobile
- Same harness, models, integrations, skills, instructions, and MCP servers everywhere
- Core pitch: start a session anywhere, continue it anywhere, finish it anywhere
- Demo built around TinyClips, a real screenshot/recording app for macOS and Windows

### Copilot App (Burke’s Demo)
- Two primary work modes:
  - Chat: ad hoc tasks outside a project (e.g., installing/configuring software via agent)
  - Sessions: work tied to a folder or GitHub repo, no cloning required
- Copilot Projects: new announcement, spans multiple repos, agents run in background
  - Progress visible via sidebar overview; library tracks artifacts as they’re built
  - Automation runs daily to find and open issues before users do
- Computer use: agent can control the desktop to functionally test native apps
  - Fills the gap Playwright covers for web but not native
  - Agent spins up the debug build, takes a screenshot, tests the tool, returns result
- Custom canvases: team-built UI inside the app (e.g., SQLite editor, team task board)
- Local model support on Surface Pro Ultra running Qualcomm

### VS Code (Julia’s Demo)
- Copilot Fusion: new smart model orchestration, picks and combines models per task automatically
- Image generation built into VS Code chat; just describe the image in the prompt
- Agents window: agent orchestration view across multiple repos and parallel sessions
  - Toggle between editor view and orchestration view without leaving VS Code
- Model Compare: run the same session across 2+ models simultaneously
  - LLM-as-a-judge config reviews attempts and picks a winner
  - Synthesize mode combines the best parts of each attempt
- Customization tab: single place for all VS Code customizations (plugins, canvases, MCP servers)
- Blobby: optional animated companion, customizable color, unlockable achievements

### CLI, Mobile, and Slack Integrations
- **CLI (Katie’s Demo)**
  - Full Copilot feature parity in the terminal: sessions, worktrees, canvases, model switching
  - Modes: Interactive, Plan (feature planning without implementing), Autopilot (fully autonomous)
  - /ask: one-off question that doesn’t enter session history
  - /diff: visual file-diff review with inline commenting and VS Code handoff
  - /pr with Auto-PR: creates PR, iterates to green, holds for team review before merge
  - Voice input via spacebar hold to create issues and assign them hands-free
- **Mobile (James’s Demo)**
  - GitHub mobile app: assign issues to agents, spin up cloud sessions from phone
  - New agent session from any repo: select branch, model, autopilot, then speak the task
  - Full terminal access to cloud file system from mobile
  - Generated a promo video entirely in cloud from screenshots taken autonomously
  - Sessions resume seamlessly on GitHub.com or desktop apps
- **Slack Integration (Pierce’s Demo)**
  - Tag @GitHub in Slack to spin up a cloud coding session from a message or feedback thread
  - Creates a collaborative channel where teammates can co-build without copy-pasting context
  - Before/after screenshots surfaced directly in Slack; full preview available inline

### Enhanced Notes

#### Enterprise Conversation: Consistent Experience, Consistent Controls
- A shared harness can reduce policy gaps across clients, but confirm which controls are actually enforced on each surface and how exceptions, offline use, and local models are handled.
- Approve connectors and custom canvases through an inventory and review process. Check authentication, data scope, destination, maintainer, retention, and the impact of a compromised integration.
- For computer use and mobile/cloud sessions, define device requirements, permitted data, session access, audit coverage, and the boundary between test and production environments.
- Apply least privilege to issue assignment, branch writes, PR creation, and merging. Treat autopilot as an execution mode requiring explicit boundaries, budgets, stop conditions, and review.
- Standardize secure defaults while allowing documented team-level configuration. Publish support guidance and a clear escalation path for cross-device session, connector, or permission failures.
- Pilot with a few workflows and measure task completion, policy consistency, adoption, support load, and cost across surfaces before presenting the platform as equivalent everywhere.
