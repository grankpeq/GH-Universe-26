# People, Process, GitHub: Eliminating 90% of Enterprise AppSec Risk

### The Core Problem
- Enterprise AppSec reality: fragmented tools, growing backlogs, unclear ownership, delivery pressure
- Push to remediate faster with AI/frontier models, but no clear starting point
- Goal: move from alert overload to frictionless security and accelerated innovation

### Step 1: Inventory via Repo Metadata File
- YAML metadata file stored in each GitHub repo (not a GitHub-native feature)
  - Contains: repo type, owner, application mapping, compliance notes, security scan config
  - Linked back to CMDB via unique identifier
- Developers own and maintain the file
  - Many-to-many relationship between repos and applications
- Enables consistent governance, audit readiness, and automation targeting

### Step 2: Security Tooling in the Developer Workflow
- All security tools (Snyk, Prisma, GitHub Advanced Security, etc.) integrated into GitHub
  - Results returned to GitHub Code Scanning dashboard via SARIF format
  - Developers see findings directly in the repo, line by line, no external portals
- Scanning runs via GitHub Actions through CLI integrations
- Consolidated view built for every level: developers, scrum leads, VPs, CIOs

### Step 3: Real-Time Reporting and Automated Remediation
- Automated refresh pulls repo metadata, app context, and scan results into a shared reporting pipeline
  - Power BI dashboard for leadership: risk concentration, apps needing attention
  - GitHub Code Scanning dashboard for developers: findings per repo, per line
- Hard gates on UAT/production branches: medium or higher severity findings block merges
  - Developers can do anything in dev environments; gates only apply at push to production
- AI-assisted remediation:
  - Autofix generates generic suggestions per finding
  - GitHub Copilot agent generates full PRs with repo-specific context
  - Developers still review and approve before committing

### Step 4: Feedback Loops and False Positive Management
- Developers can run scans themselves after fixing, getting instant feedback
- False positive handling built in:
  - Developers select a dismissal reason and submit for security team review
  - Decisions are logged as auditable records
  - Common false positive categories: sanitization controls missed by SAST, placeholder secrets, unreachable OSS vectors, misclassified pen test findings
- AI used to analyze trends: which vulnerability types recur, which teams struggle with what
  - Insights fed to training teams and security architects for systemic fixes
- Result: 90%+ reduction in AppSec vulnerabilities across ~2,000 repos

### Enhanced Notes

#### Enterprise Conversation: Make Risk Ownership and Exceptions Explicit
- Treat repository metadata as a governed interface to the CMDB: define required fields, authoritative sources, ownership, validation, update cadence, and what happens when values are missing or stale.
- Map repositories to applications and accountable owners, then use application criticality and exposure to prioritize remediation. Keep the risk decision and the person authorized to accept it explicit.
- Tune branch protections by severity, exploitability, and deployment context. Document time-bound exceptions, compensating controls, approval authority, and escalation rather than relying on a severity label alone.
- Ensure SARIF normalization preserves source, rule, severity, and remediation details so developers can act without losing the provenance needed for audit and tool-quality investigations.
- Use AI remediation to propose changes, not to attest that risk is gone. Require the organization’s normal tests, scans, and human approval for security-sensitive changes.
- Validate the reported “90%+” result with a defined baseline, time window, denominator, and recurrence/false-positive measures. Track time-to-remediate, overdue critical findings, exception age, and repeat findings alongside raw alert counts.
