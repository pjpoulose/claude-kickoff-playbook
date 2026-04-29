---
> **TEMPLATE NOTE:** This file contains placeholders in [SQUARE BRACKETS].
> Replace every placeholder with your project-specific values before use.
> Search for [ to find all placeholders that need filling in.
---

# SESSION AUDIT — Start and End Checklists
**Adapted from:** Continuous Process Audit and Self-Improvement Framework
**Scope:** Every CoWork session that touches [PROJECT NAME]

---

## Session-Start Audit (Before Any Work)

Run in this order. Do not skip steps.

**1. Read CONTEXT/Current_Status.md**
What is the current state of the project? What was decided last session? What is in progress?

**2. Read the CHANGELOG.md entries from the last two sessions**
What changed? What was the reasoning? Were there any unresolved items?

**3. Check TODO.md for in-progress and blocked items**
Are there any items that were in-progress from a previous session that need to be continued before starting new work?

**4. Run a baseline health check (pick the relevant check):**

| If working on | Run this check |
|---|---|
| [ORCHESTRATION TOOL] workflows | Claude Desktop: "List my active [ORCHESTRATION TOOL] workflows and confirm the instance is reachable" |
| [DATABASE TOOL] | [DATABASE TOOL] Dashboard → check for any failed migrations or schema errors |
| Website ([project-domain.com]) | Load [project-domain.com] in browser → confirm no broken sections visible |
| [HOSTING PLATFORM] services | [HOSTING PLATFORM] Dashboard → confirm all services show green status |
| [PAYMENT PROCESSOR] billing | [PAYMENT PROCESSOR] Dashboard → confirm no failed payment webhooks pending |

**5. Record the session baseline**
Before starting work, note in CONTEXT/Current_Status.md or CHANGELOG.md:
- What is the current state (from steps 1–4)
- What this session will focus on
- Any anomalies found in the baseline check

---

## Session-End Audit (Before Closing)

Answer each question. Any "no" creates a TODO.md debt item.

| Question | Expected Answer |
|---|---|
| Was a pre-change verification run before every modification? | Yes |
| Was a post-change verification run after every modification? | Yes |
| Was CHANGELOG.md updated with this session's entries? | Yes |
| Did every CHANGELOG entry use the structured format from Checkpoint_Format.md? | Yes |
| Were all TODO.md items addressed or updated? | Yes |
| Are there new items that should be added to TODO.md? | Addressed |
| Is the project in a working state (no broken workflows, no stale credentials, no broken pages)? | Yes |
| Was anything deferred that needs a debt entry in TODO.md? | Addressed |

If any answer is "no": add a debt entry to TODO.md with a description of what was missed and why, so it can be addressed next session.

---

## Milestone-Level Audit (At Each Phase Completion)

Run at the end of Phase 0, Phase 1, Phase 2, and Phase 3.

**On completeness of the record:**
- Can every change since project inception be traced to a CHANGELOG.md entry?
- Are there any workflows, schema changes, or code changes with no CHANGELOG entry?

**On verification quality:**
- What percentage of changes had both pre-change and post-change verification?
- Were there any sessions where a change was applied to the wrong context?

**On process adherence:**
- Were there any CHANGELOG entries marked incomplete in TODO.md?
- Were there any changes applied without first reading the current state?

**On output quality:**
- Were there any user-reported bugs or regressions since the last milestone?
- Were there any broken integrations discovered after deployment?
- Were there any stale values, placeholder text, or incorrect credentials found in production?

**Output:** A short Process Health Report (one page) committed to `OPERATIONS/Process_Health/process-health-YYYY-MM.md`.

---

## Retrospective Audit (Every 90 Days)

Four questions. Honest answers.

**1. What is working well and must be protected?**
Which process rules have consistently caught errors? Give specific examples.

**2. What is not working and must be changed?**
Which rules are consistently violated, too vague, or create friction without preventing errors?

**3. What new failure modes have emerged?**
Are there errors recurring more than once that no current rule prevents?

**4. What would a new session need to know to operate at the same quality level from day one?**
If the answer requires more than reading the process documents, the documents need updating.

**Output:** Updated process documents + `OPERATIONS/Retrospective/retrospective-YYYY-MM.md`

---

## [PROJECT NAME]-Specific Health Metrics

| Metric | Definition | Target |
|---|---|---|
| CHANGELOG coverage | % of sessions with a corresponding CHANGELOG.md entry | 100% |
| Verification completeness | % of changes with both pre and post verification | ≥ 95% |
| [ORCHESTRATION TOOL] workflow stability | Number of workflow execution failures per 10 sessions | 0 |
| Credential expiry rate | Number of expired OAuth tokens discovered unexpectedly | 0 |
| Stale value rate | Number of old strings/values found in production after a change | 0 |
| Debt backlog | Number of TODO.md items marked as debt items | 0 |
| Regression rate | Number of user-reported regressions per release | 0 |

---
*Version 1.0 — [PROJECT NAME] | April 2026*
