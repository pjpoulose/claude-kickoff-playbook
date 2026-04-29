# INSTRUCTIONS — How Claude Operates in This Project

## The Five Rules

**Rule 1 — Read before acting.**
Every session: START-HERE.md → CONTEXT/Current_Status.md → then work.

**Rule 2 — Ask one question for ambiguous tasks.**
If a brief could mean two things, ask one clarifying question. Never assume silently.

**Rule 3 — State the plan for complex tasks.**
More than three steps → state what you plan to do → wait for go-ahead.

**Rule 4 — Save all outputs with date prefix.**
Format: `OUTPUTS/YYYY-MM-DD-descriptive-name.ext`
Never save outputs anywhere else. Never overwrite an existing output file.

**Rule 5 — Update CHANGELOG.md and Current_Status.md at session end.**
These two files are the project's memory. Without them, every session starts from zero.

---

## Communication Style
[Replace with how the human prefers to communicate — direct/detailed, prefers options/recommendations, short answers/long analysis, etc.]

---

## Writing Voice (for any content this project produces)
[Replace with the tone, vocabulary, and style guidelines for this specific project's content.]

---

## Safety Rules

| Never do this | Because |
|---|---|
| [project-specific constraint] | [reason] |
| Add improvements to the playbook without human approval | Improvement system requires human gate |
| End a session without updating CHANGELOG.md | That session's decisions are untracked |
| Delete files in STRATEGY/, TECHNICAL/, OPERATIONS/ | These are source-of-truth documents |

---

## Document Priority (when things conflict)
1. Human's explicit instruction in current session
2. `STRATEGY/Decisions_Log.md` — locked decisions
3. `CONTEXT/Project_Brief.md` — core vision
4. These instructions

---

## Process Rules Reference
| Protocol | Document | When |
|---|---|---|
| Session start/end | `OPERATIONS/Session_Audit.md` | Every session |
| Pre-change verification | `OPERATIONS/Pre_Change_Verification.md` | Before every modification |
| CHANGELOG format | `OPERATIONS/Checkpoint_Format.md` | Before every save/commit |

---
*Last updated: [YYYY-MM-DD]*
