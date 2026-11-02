# Visa’s Zero Secrets Initiative: No Hardcoded Secrets, No Exceptions

## Private Notes
- `#Visa Harness in GitHub to help with security`
- `#Using CMDB with Custom Properties for App data`
- `#Using Chatbot to help respond to developers`
- `#Flow - GHAS > Combine Custom Properties with CMDB > Creates ticket in SNOW?`
- `#Fix Finding before archival of repo`
- `#Verification model we don’t do direct dismissal there is a check that ensures it’s actually fixed. Maybe an AI review of the file to ensure remediation is done to remove from source code?`
- `#Attestation stage and credibility of the fix when dismissing using in house LLM`
- `#Need a bot to validate dismissal that checks files and removal of secret`
- `#For bit the developer needs to state in the attention comment that it’s been rotated or revoked and removed from source`

## Summary
### Visa Harness in GitHub to Help with Security
- Visa uses GitHub Advanced Security (GHAS) across multiple GitHub instances: Enterprise Server (on-prem), SaaS, and open source enterprise
- Repository rule sets enforce checks on every PR before merge: secret scan, port security, dependency, license, and cybersecurity workflow checks
- Push protection enabled from day one; AI-detected secrets also integrated into the push protection module
- Bypass requires a push protection bypass request, which follows the same automated verification flow
- Exception process defined for edge cases: unit tests, non-sensitive apps, POCs

### Using CMDB with Custom Properties for App Data
- Custom property field added to every GitHub repository, set as mandatory at enterprise level
- Repos cannot be created without setting CMDB properties, which pull application metadata (criticality, ownership, etc.)
- Severity of a secret finding is calculated using this app data, then passed downstream to the ticketing system automatically

### Using Chatbot to Help Respond to Developers
- Scalability problem: developers would ping the finding owner directly on Teams asking what to do
- Built a Teams chatbot that reads the developer’s question, checks it against defined policy, and responds automatically
- Developers can still escalate to a human, but the bot handles the majority of queries at scale

### Flow: GHAS > Combine Custom Properties with CMDB > Creates Ticket in ServiceNow
- Intermediate system polls all GitHub accounts continuously; alerts are ingested within a couple of hours
- System enriches each alert with CMDB/custom property data, calculates severity, and creates a finding in the internal ticketing system (ServiceNow)
- Two levels of ownership:
  - GitHub alert owner: person most related to the code (committer, branch contributor, repo admin)
  - Application owner: responsible for ensuring remediation within the SLA date
- Alert assignment logic runs through six phases, stopping as soon as an owner is found:
  1. Secret committer
  2. Committer to the same file
  3. Contributor on the same branch
  4. Repository admin
  5. Organization admin
- Triage stage filters alerts before they reach developers:
  - Offline checks (structure, pattern, no network required)
  - Liveness check (validates token against the issuing system)
  - ML classifier (handles org-specific test/placeholder patterns that rules can’t cover)
- Gray-area findings (e.g., unreachable vendor systems) are passed through as real findings rather than suppressed

### Fix Finding Before Archival of Repo
- Developers previously archived repositories to make alerts disappear without remediating
- Archival process now gated: open findings must be resolved before a repo can be archived
- Developers also cannot directly dismiss alerts; all dismissals go through the verification module

### Verification Model: No Direct Dismissal, Checks That Fix Is Actually Done
- Developers submit an alert dismissal request rather than closing directly
- Fixed verification module runs four stages; all must pass for the alert to close:
  1. Secret removed from the primary branch (file location pinpointed if multiple locations exist)
  2. Liveness check: token/credential confirmed revoked or inactive
  3. GenAI attestation review: developer’s comment checked against policy rules
  4. Developer credibility/track record check
- If any stage fails, the alert is denied with a specific reason and returned to open state (closed-loop mechanism)
- Finding description in the ticket includes: alert link, alert tag, remediation steps, and training links; secrets themselves are never stored in the portal

### Attestation Stage and Credibility of the Fix When Dismissing Using In-House LLM
- In-house LLM (GenAI) evaluates the developer’s dismissal comment against defined policy
- Comment must confirm: secret removed from source, and token rotated or revoked
- Example failure: developer says “I removed the file” but does not attest to rotation/revocation; GenAI denies even if stages 1 and 2 passed
- This is an attestation stage only; the LLM is not the sole gate but adds a human-language policy check

### Need a Bot to Validate Dismissal That Checks Files and Removal of Secret
- Automated verification module handles this end-to-end: no manual review by the security team
- System checks file locations, confirms secret is absent from all flagged locations, and only then proceeds to subsequent stages
- For internal systems (e.g., Artifactory on-prem), Visa built custom liveness checks since GitHub cannot validate those tokens natively

### For the Developer: Attestation Comment Must Confirm Rotation, Revocation, and Removal from Source
- Developer must explicitly state in the dismissal comment that the secret has been:
  - Rotated or revoked at the issuing system
  - Removed from the source code
- Vague comments (e.g., “this is an encrypted password, should be fine”) are automatically denied
- Marking a finding as false positive while the secret still exists in the codebase is a stage-one failure

## Enhanced Notes

### Enterprise Conversation: Automate Verification With Defensible Evidence
- Adapt the workflow to the organization’s identity, source-control topology, CMDB quality, and incident-response process; validate each integration and ownership rule before applying it enterprise-wide.
- Keep secret values out of tickets, chat, logs, model prompts, and dashboards. Pass stable alert references and minimum necessary metadata between systems, with access controls and retention limits.
- Treat developer attestations and LLM assessments as supporting evidence, not proof that a credential is safe. Require verifiable removal and revocation evidence from authoritative systems where available, with human escalation for uncertain cases.
- Define how the process handles multi-location exposure, history, forks, generated artifacts, replicas, and systems without a reliable liveness check. Alert closure should not imply that historical exposure or incident-response obligations have ended.
- Make automated ownership and severity explainable, auditable, and correctable. Provide a dispute path and monitor misassignment, delayed tickets, false dismissals, and false-positive rates.
- Pilot with a narrow set of repositories and credential types. Use failure injection and audit review to verify that failed checks keep findings open and that bypasses, archive requests, and exceptions receive equivalent scrutiny.
