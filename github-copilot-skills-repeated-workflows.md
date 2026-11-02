# How to turn your teams repeated workflows into GitHub Copilot Skills

### GitHub Copilot CLI: Core Concepts
- Nine concepts organized into four buckets: guide, connect, enforce, share
- Guiding tools:
  - Instructions: always-on rules loaded every CLI session (keep short, they consume context memory)
  - Skills: reusable, repeatable workflows triggered by relevance or /skillname
  - Agents: specialist roles (e.g. read-only reviewer, docs writer) defined in .env files
  - Prompts: one-off typed requests, not reusable
- Connecting tools: MCP servers (API access to external/local services) and LSP (language server for strongly typed libraries)
- Enforcement: hooks, event-driven triggers that fire deterministically (e.g. user_prompt_submitted), unlike instructions which can conflict
- Sharing: plugins (folder bundling skills, agents, hooks) and marketplaces (essentially a zip of zips)

### Who Uses What
- Developers: skills for repeated workflows
- Tech leads: instructions to enforce team standards
- Teams: shared skills (e.g. Issue Lifecycle tracker for quality/security)
- Hooks: catch secrets before they reach the model, enforce code review gates
- Platform teams: custom MCP servers, LSP setup
- Ecosystem: plugins and marketplace

### Hands-On Lab: Building the Issue Lifecycle Skill
- Scenario: automate GitHub issue creation and updates as developers build features
- Setup steps:
  1. Log into github.com/enterprises/gh-universe with lab credentials
  2. Navigate to the org, find repo prefixed with your username (sandbox starter)
  3. Clone via Copilot CLI or download as zip if permissions block cloning
  4. Run copilot --yolo from the repo directory in terminal
- Skill creation: paste the lab guide prompt into CLI, it generates the .skill.md and .env files automatically
- Reload skill after creation: skills reload, then validate with skills info issue-lifecycle
- Demo result: as a developer vibe-codes features, issues are auto-created and updated in the repo in real time

### Next Steps
- **Complete remaining lab feature requests**
  Lab accounts stay active until Friday with no token limits. Optional tasks C, D, E can be skipped; focus on Molly and Bea's feature requests in the sandbox repo.

## Enhanced Notes

### Enterprise Conversation: Governed Workflow Reuse
- Publish shared skills and plugins through a reviewed, versioned source with named maintainers, release notes, compatibility expectations, and a retirement process.
- Keep instructions concise and scoped to the files or tasks they govern. Test that overlapping instructions, agent roles, and hooks produce the intended behavior rather than assuming precedence.
- Review every connected tool and MCP server for authentication method, data access, outbound destinations, permission scope, and logging. Prefer managed identities and least privilege over personal credentials.
- Use hooks for deterministic checks, not as a substitute for authorization or server-side policy. Ensure bypasses and failures are visible and follow existing development controls.
- Validate reusable workflows against representative tasks, including negative cases. Track completion quality, unintended edits, developer overrides, maintenance burden, and context/cost impact.
- Introduce templates with an opt-in pilot, collect developer feedback, and promote only workflows that demonstrate measurable benefit without weakening code review or security controls.
