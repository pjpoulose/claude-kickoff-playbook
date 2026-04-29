# Process Improvements — Playbook Learning Log
**This file tracks all improvement proposals to the Claude Kickoff Playbook.**
**Proposals come from real projects. Approved proposals become playbook rules.**

---

## How This Works

1. During any project, Claude or the human identifies a better way to do something
2. Claude adds an entry below (status: `proposed`)
3. The human reviews it — at session end or asynchronously
4. Human marks it `approved`, `rejected`, or `needs-modification`
5. Approved entries are submitted to the canonical playbook repository
6. Once merged into the playbook, status changes to `merged`
7. The playbook version increments

**The human approval gate is non-negotiable.** No improvement reaches the canonical playbook without explicit human review and approval. Claude proposes — the human decides.

---

## Improvement Template

Copy this for each new proposal:

```
---

## IMPROVEMENT-[NNNN] — [Short title]

**Date identified:** YYYY-MM-DD
**Project:** [project name]
**Identified by:** Claude | [human name]
**Status:** proposed | approved | rejected | needs-modification | merged
**Playbook section affected:** Part [N] — [section name]

### The Problem
<What specific failure or friction was observed? Give a concrete example from this session.>

### The Proposed Rule
<Exactly as it would appear in the playbook. Be specific enough to apply consistently.>

### Evidence
<What happened in this project that demonstrates the need? One specific example minimum.>

### Tradeoffs
<What friction does this add? When might this rule be wrong?>

### Human Review Notes
<Space for approval comments, modifications, or rejection reasoning>
**Decision:** [approved / rejected / needs-modification on YYYY-MM-DD]
```

---

## Active Proposals

*(None yet — this file is pre-populated from the playbook template)*

---

## Approved (Pending Playbook Merge)

*(None yet)*

---

## Merged into Playbook

*(None yet — version 1.0 is the starting point)*

---

## Rejected

*(None yet)*

---

## Notes for Claude

When you identify a potential improvement during a session:
1. Create a new entry in the Active Proposals section above
2. Use IMPROVEMENT-0001, IMPROVEMENT-0002, etc. (sequential numbering)
3. Fill in all fields — especially Evidence and Tradeoffs
4. Set status to `proposed`
5. Mention it in your session-end summary so Paul is aware
6. Do NOT add the improvement to any operational document until Paul approves it

When Paul approves an improvement:
1. Change status to `approved`
2. Move the entry to "Approved (Pending Playbook Merge)" section
3. Note the approval date and any modifications Paul requested
4. Add a TODO item: "Submit IMPROVEMENT-[NNNN] to playbook repository"

When an improvement is merged into the canonical playbook:
1. Change status to `merged`
2. Note the playbook version it was merged into
3. Move the entry to "Merged into Playbook" section
