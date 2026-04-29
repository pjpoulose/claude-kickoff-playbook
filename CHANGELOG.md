# Playbook Changelog
*Version history of the Claude Kickoff Playbook itself.*
*Every rule change, improvement merge, and version increment is recorded here.*

---

## Version 1.0 — April 2026

**What is new:** Initial release. All content.

**Sources:**
- Manus AI-Assisted Development Process Playbook (website project learnings)
- Initial CoWork project deployment (April 2026)
- Continuous Process Audit and Self-Improvement Framework (Manus)
- Structured Checkpoint Format (Manus)
- Mandatory Pre-Edit Grep Audit (Manus)
- CHANGELOG.md Implementation Plan (Manus)

**Key decisions in v1.0:**
- Manus-specific tooling (webdev_save_checkpoint, TypeScript compiler) replaced with universal equivalents
- Improvement system designed with human approval gate as non-negotiable
- Context file 400-word limit established based on CoWork context window behavior
- Sequential improvement numbering (IMPROVEMENT-NNNN) established for cross-project tracking

**Known gaps identified at v1.0:**
- No template for multi-person projects (pair programming with Claude, multiple human contributors)
- No guidance for projects with regulatory requirements (HIPAA, GDPR)
- No template for API/developer-facing projects vs. consumer product projects

---

*Next version will incorporate improvements from active projects.*
*Submit improvements via PR or by contacting the maintainer.*

---

## Version 1.0.1 — April 2026 (Security layer added)

**What changed:** Security architecture added to the playbook.

**New files:**
- `security/CORE_PRINCIPLES.md` — Seven immutable principles with integrity check mechanism
- `security/NEGATIVE_SCENARIOS.md` — Append-only failure registry with 5 initial entries (NS-0001 through NS-SEC-0001)
- `security/SECURITY.md` — Complete security model: threat model, prompt injection mitigation, contribution security, session guardrails, user protection guardrails
- `skills/SKILL.md` — The installable Claude skill with security integration

**Security decisions made:**
- Integrity phrase mechanism chosen over cryptographic hashing (accessible without tooling, adequate for the threat model at launch)
- Content-only file list established (PROCESS_IMPROVEMENTS.md, NEGATIVE_SCENARIOS.md, case-studies/, CHANGELOG.md)
- Three-gate rule for improvements: evidence + human approval + maintainer review
- Core Principles amendment process requires 14-day discussion period + 3 independent approvals

**Known gaps at v1.0.1:**
- No automated integrity verification (manual canary phrase check only)
- No cryptographic signature on CORE_PRINCIPLES.md (planned for v1.1)
- No rate limiting on improvement submissions (relies on GitHub PR review process)
- Skill update is manual — no automated notification when a new version is available
