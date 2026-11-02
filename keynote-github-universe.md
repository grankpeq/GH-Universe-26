# Keynote - GitHub Universe

## Private Notes
- `#Explain teh CoPilot Fusion add more context here this is important.`
- `#Copilot app highlight this`
- `#Copilot Projects we need more info on this`
- `#Copilot Fusion create more context in notes`

## Summary
### GitHub Universe: Scale and the Agentic Era
- 225 million developers on GitHub, spanning every country
  - New developer joined every second for the second straight year
- 2026 Octoverse numbers:
  - 17.9 billion code pushes
  - 34.3 billion commits
  - 1.3 billion PRs
- 566 million open source and public repos, up 30% year over year
- Growth driven by the shift to agentic software development
  - Delta between 2024 and 2026 described as “remarkable”
- SDLC is collapsing: no longer linear, agents handle bulk of implementation and verification
- Three pillars of the agentic software delivery system: velocity, intelligence, quality

### Copilot App: Highlight This
- New agent-native desktop app: single location for agents, projects, external tool integrations, and automations
- Connectors: managed services that authenticate once and connect across Slack, WorkIQ, Vercel, Netlify, Sentry, and more
  - Verified badge indicates GitHub-managed connectors (no repeated logins across devices)
- Canvas: agents interact with browser, terminal, or custom canvases inside the app
  - Not a real browser: a canvas that agents can control directly
  - Browser canvases, terminal canvases, and custom canvases available
- Copilot Dreaming: automatically updates custom instructions and memories as the codebase evolves
  - Prevents stale instructions from hurting agent output over time
  - Opens a PR with cleaned-up instructions for review, just like any other code change
  - Memories capture personal preferences and team practices for more tailored outputs

### Copilot Fusion: Need More Context Here, This Is Important
- Coordinates between multiple models to deliver frontier-level results at lower cost
- Automatically selects the optimal execution pattern per task:
  - Three modes: single, cascade, or critique
- Performance benchmark: Copilot Fusion Max scored 60 on the Artificial Analysis Coding Agent Index
  - Within 2 points of Opus 5.5 Max
  - Achieved at half the cost per task and 40% less time per task
- Promotion: 30% off Fusion usage through end of November 2026
- Need to understand more about how Fusion decides which execution pattern to use and when cascade vs. critique is triggered

### Copilot Projects: Need More Info on This
- Set a goal across one or many repos; Copilot spins up as many agents as needed
  - Agents assigned per repo based on where the task lives
- Additional context (Slack threads, design mocks, Teams call recordings) can be sent mid-session
  - Copilot orchestrator handles it; no need to wait for agents to finish
- Marketing artifact generation: Copilot can produce pixel-perfect demo videos of new features before code ships
  - Automations can trigger these video builds daily on new feature releases
- Agents run locally or in the cloud (laptop can be closed)
- PRs surface automatically in the project overview as agents complete work
- Announced as generally available today
- Need more detail on: pricing model, agent limits per project, and how the orchestrator handles conflicting context

### Quality, Security, and Continuity
- Session continuity across phone, app, VS Code, CLI, and .com via the same Copilot harness
  - Harness now rolled out across all of Microsoft
  - Can also build custom agents on Microsoft Foundry using this harness
- Copilot Automations: AI-powered workflows triggered by event, schedule, or manual trigger
  - Run in the cloud; no need to keep laptop open
  - Configurable tool permissions (e.g., can create PRs but not merge them)
  - Spend limits prevent runaway AI credit usage
  - Can chain specialist automations: signal detection, triage, reproduction, fix, verification
- Code Scanning: scans entire codebase for vulnerabilities in new and existing code
  - Expanded language support via AI
  - Findings can be assigned directly to agentic autofix, producing a suggested-fix PR
- AI Push Protection: detects secrets before they reach the repository, no pattern required
- Copilot Code Review: reviews every PR (from agent or human) before any human reviewer
  - 200 million findings surfaced to date
  - New tier: Code Review Max, highest F1 score on ReviewBench for high-severity issues
  - Available without a Copilot subscription; pay per review with AI credits
- Stacked pull requests: group related but distinct pieces of work, merge together or individually
- Agent Merge: automatically resolves conflicts, fixes CI failures, and merges once all checks pass

### Infrastructure: New Git Architecture
- Added capacity this year: 4 million CPU cores, 160 petabytes of high-speed storage, 50 terabits/second network
- Multi-region Azure migration underway; expected complete early next year
- New Git architecture principles: simplify the primitive, decouple storage from compute, minimize coordination
  - Code stored durably in Azure Blob Storage; compute servers are ephemeral and scalable
  - Reference transactions handled by a specialized replicated log service
  - Branch-level locking replaces repo-level locking: parallel agent writes on different branches
- Results: 7,200 writes per second sustained on a single repo (180x current throughput)
  - Tested with 5,000 concurrent coding agents against one monorepo
  - Read performance: internal load testing hit its own limits before the new architecture did
- Validated with OpenClaw (one of the busiest open source projects on GitHub)
- All repositories migrated to new architecture by early next year
- AI Gateway: processes trillions of requests; optimized for prompt caching, latency, and harness performance
- Actions: billions of minutes per month; hardening coordination and simplifying scheduling
- Network: more edge sites added, TLS optimizations, legacy data center traffic pulled back to Azure

### Enterprise Availability
- GitHub Enterprise customers can now use all Copilot features without a separate Copilot subscription
  - Includes: Copilot app, Code Review, Automations, and more
  - Pay only for AI credits used

## Enhanced Notes

### Enterprise Conversation: Validate Fit Before Broad Adoption
- Verify current availability, licensing, credit consumption, data handling, and administrative controls for each announced capability. Treat keynote statements and benchmark comparisons as claims to validate, not procurement assumptions.
- For Copilot Fusion, compare the organization’s representative tasks across quality, latency, cost, and failure modes. Establish when orchestration is appropriate and how teams can inspect or override the selected execution path.
- For Copilot Projects and Automations, define project boundaries, repository permissions, approval requirements, concurrency limits, spend ceilings, and stop conditions before enabling multi-repository work.
- Assess session continuity and connectors against enterprise identity, device management, data residency, retention, and audit requirements. Limit connected services to approved use cases and least-privilege scopes.
- Evaluate Code Review and Agent Merge using a risk-tiered rollout: measure missed high-severity issues, false positives, reviewer workload, CI reliability, and the proportion of changes still receiving accountable human approval.
- Treat new Git infrastructure capacity claims as platform context, not a substitute for testing the organization’s own workload, availability requirements, and recovery expectations.
