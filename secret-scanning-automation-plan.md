# Secret scanning automation plan

### Problem: Secret Scanning Pattern Causing Gate Blocks
- Published a custom regex pattern (built with Copilot) to detect internal auth tokens
  - Dry run showed ~1,000 results; after publishing, ballooned to ~13,000
  - Tokens expire after 21 hours, so low actual risk (most are old, pre-SaaS migration)
- Issue: all historical matches surface in the security/quality tab
  - Gates block promotion to production if any secrets are detected
  - Need a way to triage old/expired secrets without triggering blocks

### Recommended Approach: Automated Dismissal via API
- Rewriting git history to remove old secrets is not recommended
- Instead: use the GitHub API to bulk-dismiss known expired/historical alerts
  - List all secret scanning alerts for the entire org
  - Filter for alerts matching the pattern that are expired or known historical
  - Call the update secret alert endpoint, setting state to resolved
- Existing CodeQL dismissal automation (for risk exceptions) can serve as a template

### GitHub Actions Workflow for Automation
- Wrap the API calls in a GitHub Actions workflow to run automatically
  - Trigger on new vulnerability alerts: check if the secret is already expired or known
  - Avoids manual click-through of 13,000+ alerts (campaigns of 1,000 at a time ruled out as too noisy)
- Copilot can help generate the workflow logic

### Next Steps
- **Build a GitHub Actions workflow to auto-dismiss expired secret alerts** (Joe)
  Use the org-level secret alert list API and update endpoint; model it on existing CodeQL dismissal automation.

### Enhanced Notes

#### Enterprise Conversation: Close the Exposure, Not Just the Alert
- An expired credential may still be exposed in source history or indicate a wider incident. Do not dismiss an alert solely because a token is believed to be old or expired; confirm revocation/rotation and follow the organization’s incident-response policy.
- Separate alert classification from closure. Use an approved, documented reason, retain evidence and approver identity, and make exceptions time-bound and reviewable.
- Before automation, run a dry-run inventory and validate matching logic against known true positives, false positives, and edge cases. Keep a sampled human review and a safe stop condition during rollout.
- Use a dedicated, least-privilege workflow identity; protect workflow changes; avoid logging secret values; and record alert identifiers, decisions, timestamps, and workflow versions for audit.
- Design the process to be idempotent and recoverable, with bounded batches, API rate-limit handling, retry visibility, and a reconciliation report for alerts left unresolved.
- Measure time to revoke, time to remove from active source, alert aging, recurrence, exception volume, and confirmed exposure—not just the number of alerts dismissed.
