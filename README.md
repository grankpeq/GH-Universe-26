# GitHub Universe '26 Meeting Notes & Session Repository

Welcome to the GitHub Universe '26 session notes repository. This repository contains detailed meeting notes, session breakdowns, security strategies, and technical insights captured across keynotes and breakout sessions at GitHub Universe '26.

---

## 📂 Repository Structure & Session Index

| File Name | Topic / Session Title | Key Themes & Coverage |
| :--- | :--- | :--- |
| `keynote-github-universe.md` | **Keynote: GitHub Universe** | Platform scale (225M developers, 34.3B commits), Copilot App, Copilot Fusion, Copilot Projects, and new Git cloud infrastructure (7,200 writes/sec). |
| `agentic-engineering-past-the-pilot.md` | **Agentic Engineering Past the Pilot** | Shifting focus from AI coding to full SDLC engineering, overcoming PR review bottlenecks, parallel cloud sandboxes, Memory, Dreaming, and Fusion. |
| `factory-mindset-agentic-workflows-in-production.md` | **The Factory Mindset: Agentic Workflows** | Transitioning from manual coding to repeatable autonomous workflows, technical debt remediation, governance, and human-in-the-loop oversight. |
| `visas-zero-secrets-initiative.md` | **Visa’s Zero Secrets Initiative** | Eliminating hardcoded credentials, metadata-driven alert assignment via CMDB/ServiceNow, AI verification checks, and strict dismissal criteria. |
| `treat-your-ai-context-as-infrastructure.md` | **Treat Your AI Context as Infrastructure** | Scoping context for enterprise AI, instruction primitives (`.instructions.md`), skills, agents, governance plugins, and continuous evaluation. |
| `work-together-your-way-with-github-copilot.md` | **Work Together, Your Way, with Copilot** | Unified Copilot platform across VS Code, CLI, Copilot App, Mobile, and Slack; computer use testing; custom canvases; and collaborative channels. |
| `github-copilot-skills-repeated-workflows.md` | **Turning Workflows into Copilot Skills** | CLI tools framework (instructions, skills, agents, prompts, hooks, plugins), issue lifecycle tracking, and standardizing repeatable team workflows. |
| `four-days-zero-lines-ai-force-multiplier.md` | **Four Days, Zero Lines: AI Force Multiplier** | Resolving policy compliance failures across 436 repositories using policy-as-code automation, GraphQL API scripts, and Copilot orchestration. |
| `low-orbit-agentic-cannon-scaling-copilot.md` | **The Low Orbit Agentic Cannon** | Mass repository modification across 300+ repos via Low Orbit Cannon, Jira-to-GitHub integration via Air Traffic Controller, and dev friction reduction. |
| `eliminating-90-percent-appsec-risk.md` | **Eliminating 90% of Enterprise AppSec Risk** | Repository metadata files for asset ownership, inline developer security tools, automated branch quality gates, and AI-assisted remediation. |
| `pre-keynote-github-universe.md` | **Pre-Keynote: GitHub Universe** | Expert panel on the evolution of developer roles, shift to high-level system orchestration, open-source collaboration, and multi-agent systems. |
| `secret-scanning-automation-plan.md` | **Secret Scanning Automation Plan** | Bulk handling of 13,000 legacy token alerts via GitHub API and custom Actions workflows, avoiding destructive git history rewrites. |


---


## Enhanced Notes

### Enterprise Discussion Guide
- Treat the session notes as hypotheses and discussion starters, not verified product documentation. Before sharing externally, confirm product names, availability, pricing, benchmark methodology, and reported results against current primary sources.
- Prioritize opportunities by business outcome and risk: select a workflow with measurable toil, a clear owner, and reversible changes before scaling to more teams or repositories.
- Establish enterprise guardrails before broad rollout: approved identity and permissions, data handling rules, auditability, human approval points, usage budgets, and an exception path.
- Measure outcomes with a baseline and a defined period. Useful measures include cycle time, review queue age, escaped defects, remediation time, workflow failure rate, cost per completed outcome, and developer experience.
- Assign accountable owners for workflow policy, shared agent context, security exceptions, and ongoing evaluation; include maintenance and rollback plans in each pilot.
