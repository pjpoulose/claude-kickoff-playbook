# Claude Project Kick-off Playbook — Complete Reference
**Version:** 1.1 | **April 2026**
**Source of truth for all projects using this framework**

---

## Part 1 — Philosophy

### Why This Playbook Exists

Every AI-assisted project fails in one of three ways:
1. **The context window closes** and the reasoning behind past decisions is lost forever
2. **A change is made to the wrong state** because the current state was assumed, not verified
3. **There is no record of what was done or why** — so the same mistakes repeat

This playbook eliminates all three failure modes with mandatory protocols that make verification automatic, memory permanent, and learning continuous.

### The Governing Principle

> **Read the current state before changing it. Verify after every change. Record the reasoning before the session ends.**

This principle, applied consistently across every session, is the difference between a project that compounds positively and one that accumulates invisible debt.

### The Four Levels of Memory

AI has no persistent memory. Projects need four layers to compensate:

| Layer | Mechanism | What it preserves | Survives |
|---|---|---|---|
| Session | CONTEXT/Current_Status.md | What is happening right now | Session restart |
| Project | CHANGELOG.md | Every decision and its reasoning | Context compaction |
| Decisions | STRATEGY/Decisions_Log.md | Locked choices that cannot be undone | Project lifetime |
| Playbook | This document | Lessons from all projects | Forever |

The playbook layer is the one that crosses project boundaries. It is the institutional memory that no single project can own.

---

## Part 2 — Project Structure

### The Universal Folder Layout

Every project using this playbook starts with this structure. The names are standardised so Claude can navigate any project using this playbook without needing to learn the layout.

```
[project-name]/
├── START-HERE.md          ← Claude reads this first, every session
├── INSTRUCTIONS.md        ← Operating rules for Claude
├── MEMORY.md              ← Session log (updated each session)
├── CHANGELOG.md           ← Permanent record of every change
├── TODO.md                ← Living task tracker
├── PROCESS_IMPROVEMENTS.md ← Improvement proposals for this project
│
├── CONTEXT/               ← Short files (<400 words each)
│   ├── Project_Brief.md   ← What the project is
│   ├── Owner_Profile.md   ← Who the human is and how they communicate
│   └── Current_Status.md  ← What is happening right now
│
├── STRATEGY/              ← Long-form reference documents
│   └── Decisions_Log.md
│
├── TECHNICAL/             ← Technical architecture and stack
│   └── Stack.md
│
├── OPERATIONS/            ← Process documents and setup guides
│   ├── Process_Playbook.md
│   ├── Session_Audit.md
│   ├── Checkpoint_Format.md
│   └── Pre_Change_Verification.md
│
├── OUTPUTS/               ← Everything Claude produces (date-prefixed)
└── TEMPLATES/             ← Reusable briefs and prompts
```

### The Context Window Budget

CoWork has a context window. Files loaded into it take up space. The rule:

**CONTEXT/ files must be under 400 words each.** They are loaded every session.
**All other files** are loaded on demand, only when a task requires them.

The CONTEXT/ folder is the working memory. Every other folder is long-term storage.

---

## Part 3 — The Six Core Rules

These are the non-negotiable operating rules for every Claude session on every project.

### Rule 1 — Read Before Acting

Before modifying anything, read the current state. Never act on assumed context.

**What this prevents:** Editing a workflow that has already been changed. Deleting a credential that no longer exists. Applying a copy change to text that was already updated.

**How to apply it:** Before any modification, ask: "What does the current state actually look like?" Read the file, open the dashboard, inspect the workflow. Then act.

### Rule 2 — Verify Before and After Every Change

Every change has two verification moments: before (confirm the target exists as expected) and after (confirm the change applied correctly).

**The verification table:**

| Context | Before | After |
|---|---|---|
| n8n workflow | Read workflow JSON via MCP | Trigger test → inspect execution log |
| Supabase schema | Read table structure in dashboard | Run test query → confirm result |
| Environment variable | Read Variables tab in Railway | Run dependent workflow → confirm it resolves |
| Website copy | Confirm exact current string in file | Confirm old string absent + new string present |
| Credential | Check credential name exactly | Run test operation → confirm success |
| File content | Read file → confirm exact target string | Confirm old string gone + new string present |

### Rule 3 — Scope Multi-Step Changes Explicitly

For any task with more than three changes, create a numbered phase plan before starting. Track completion against the list. Do not start Phase N+1 before Phase N is verified complete.

**What this prevents:** Partial application of a 24-change brief where changes 1–12 are applied but 13–24 are forgotten when the session ends.

### Rule 4 — CHANGELOG.md Is Mandatory

Every session that changes anything updates CHANGELOG.md before the session ends. The entry is written before the final save, not after.

The CHANGELOG is the memory that survives context compaction. Without it, every session starts from zero.

### Rule 5 — TODO.md Is the Single Source of Truth

Every incomplete, deferred, or flagged item creates a TODO.md entry before the session ends. Nothing lives "in my head" or "in the session context." If it is not in TODO.md, it does not exist as a tracked commitment.

### Rule 6 — All Outputs Are Named and Dated

Every file Claude produces goes into `OUTPUTS/YYYY-MM-DD-descriptive-name.ext`. Never save to the root. Never overwrite an existing output without a new dated name.

---

## Part 4 — The Session Ritual

### Session-Start (Before Any Work)

Run in this order. Do not skip.

1. Read `CONTEXT/Current_Status.md` — what is the state right now?
2. Read the most recent two entries in `CHANGELOG.md` — what was just done?
3. Read `TODO.md` — what is in progress or blocked?
4. Run a baseline health check appropriate to the project type
5. State the plan for this session before beginning any work

### Session-End (Before Closing)

Answer each question. Any "no" creates a TODO.md debt item.

| Question | Expected |
|---|---|
| Was pre-change verification run before every modification? | Yes |
| Was post-change verification run after every modification? | Yes |
| Was CHANGELOG.md updated with structured entries for this session? | Yes |
| Was TODO.md updated — items completed, new items added? | Yes |
| Was PROCESS_IMPROVEMENTS.md updated if any improvement was identified? | Yes |
| Is the project in a working state? | Yes |

---

## Part 5 — The CHANGELOG Entry Format

### The Template

```
---

## [YYYY-MM-DD HH:MM] — <Short title>

**Scope:** <category>
**Files/Services:** <what was changed>

### Request
<What the human asked for>

### Changes Made
| File / Service | Nature of Change |
|---|---|
| `file.md` | Description of change |

### Decisions and Reasoning
<Why this approach? What was rejected? What edge cases were noted?>

### Verification Steps
- [ ] Pre-change: confirmed current state
- [ ] Post-change: confirmed change applied
- [ ] [context-specific check]

### Follow-up Items
<Anything deferred or requiring future action>
```

### Scope Vocabulary (Universal)

| Scope | When to Use |
|---|---|
| `Copy` | User-visible text changes |
| `Config` | Environment variables, settings, credentials |
| `Feature` | New user-facing functionality |
| `Bug Fix` | Correcting broken behaviour |
| `Infra` | Deployment, hosting, DNS |
| `Schema` | Database changes |
| `Workflow` | Automation workflow changes |
| `Integration` | New API or service connections |
| `Docs` | Documentation updates |
| `Strategy` | Product direction decisions |
| `Process` | Improvement to the working process |
| `Multi` | Two or more categories in one session |

### Anti-Patterns (Never Write These)

| Never write | Write instead |
|---|---|
| "Updated the workflow" | Name the workflow + describe every node change |
| "Fixed an issue" | Name the symptom, the cause, and the fix |
| "Various improvements" | List every change individually |
| Empty Decisions section | At minimum: why this approach over the obvious alternative |

---

## Part 6 — The Pre-Change Verification Protocol

### The Six Steps

**Step 1 — Know the exact target.**
Write down the exact current value you intend to change. Not a paraphrase. The literal string, key, or configuration value.

**Step 2 — Confirm it exists.**
Verify the target exists in its expected form before touching it. If it is not where expected, stop and investigate.

**Step 3 — Check for duplicates.**
If the same value exists in multiple places, decide explicitly whether all instances are being changed. Document the scope.

**Step 4 — Confirm the replacement is not already there.**
If the new value already exists, the change may already have been applied. Verify before re-applying.

**Step 5 — Apply the change.**
Only after Steps 1–4 pass.

**Step 6 — Post-change verification.**
Confirm: old value is gone. Confirm: new value is present. Confirm: the system behaves correctly.

### Common Failure Modes

| Failure Mode | What Happens | Prevention |
|---|---|---|
| Assumed state | Edit applied to text/config that was already changed | Step 2 — always verify before acting |
| Duplicate occurrence | One instance changed, another left stale | Step 3 — check count before editing |
| Already applied | Same change applied twice, creating duplication | Step 4 — confirm replacement not already present |
| Wrong service/file | Variable set in wrong Railway service | State the exact target name and location in every action |
| Whitespace mismatch | Grep finds no match due to invisible characters | Read the file with a raw reader, copy string character-by-character |

---

## Part 7 — The TODO System

### The Three States

Every item in TODO.md is in exactly one state:
- **🔴 IN PROGRESS** — being worked on in the current session
- **🟡 NEXT UP** — ready to be worked on, not yet started
- **✅ COMPLETED** — done and verified

There is also:
- **🔴 DEBT** — a process step that was missed and needs addressing next session

### The Rules

1. If a task is not in TODO.md, it is not a tracked commitment
2. Nothing moves to COMPLETED until it is verified complete, not just applied
3. Every session ends with TODO.md updated — new items added, completed items marked, in-progress items updated
4. DEBT items are never silently dropped — they are resolved or explicitly cancelled with a reason

---

## Part 8 — The Improvement System

### How the Playbook Learns

This is the mechanism that makes the playbook self-improving. It operates at two levels:

**Level 1 — Project-level improvements (PROCESS_IMPROVEMENTS.md in each project)**
During any session, when Claude or the human identifies a better way to do something, it is documented in the project's `PROCESS_IMPROVEMENTS.md`. The human reviews it. If approved, it is marked as approved and flagged for promotion to the canonical playbook.

**Level 2 — Playbook-level improvements (this repository)**
Approved project-level improvements are submitted to the canonical playbook repository as PRs (or by the maintainer directly). Once merged, all future projects benefit.

### The Improvement Entry Format

```
---

## IMPROVEMENT-[NNNN] — [Short title]

**Date identified:** YYYY-MM-DD
**Project:** [project name]
**Identified by:** [Claude / human name]
**Status:** proposed | approved | rejected | merged

### The Problem
<What failure mode or friction point was observed? Be specific.>

### The Proposed Rule
<The exact rule change, addition, or removal being proposed.
Write it as it would appear in the playbook.>

### Evidence
<What happened in this project that demonstrates the need for this rule?
Specific example required — no hypotheticals.>

### Tradeoffs
<What does this rule cost? Does it add friction? Does it slow anything down?
Is there a scenario where this rule would be wrong?>

### Review Notes
<Space for the human to add approval notes, modifications, or rejection reasoning>
```

### The Review and Promotion Process

```
Claude identifies improvement during session
    ↓
Claude adds entry to PROCESS_IMPROVEMENTS.md (status: proposed)
    ↓
Human reviews at session end (or flags for async review)
    ↓
Human marks: approved / rejected / needs-modification
    ↓
If approved: entry promoted to canonical playbook via PR
    ↓
Playbook version incremented, CHANGELOG updated
    ↓
All projects on next pull receive the improvement
```

### The Human Approval Gate

No improvement is added to the canonical playbook without human review. This is not optional. Claude proposes — the human decides. This prevents runaway rule accumulation where every session adds friction without adding value.

The human's approval checklist:
- [ ] Does this rule prevent a real, observed failure mode?
- [ ] Is the rule specific enough to apply consistently?
- [ ] Is the cost (friction) proportional to the benefit (errors prevented)?
- [ ] Does this rule conflict with any existing rule?
- [ ] Would this rule work on a different type of project, not just this one?

---

## Part 9 — Making the Playbook Independent

### The Architecture

The playbook lives in its own GitHub repository, completely separate from any project. Projects reference the playbook but do not own it.

```
GitHub Repository: [your-username]/claude-kickoff-playbook
    ↓
Any project uses the playbook by:
1. Cloning the playbook repo
2. Copying the templates/ folder into their project
3. Running their project independently
4. Contributing improvements back via PR
```

### Why GitHub

- **Version controlled** — every change to the playbook is tracked with a commit message
- **Forkable** — anyone can fork the playbook and customise it
- **Collaborative** — multiple projects contribute improvements via pull requests
- **Portable** — the playbook URL can be shared as a simple link
- **Durable** — survives any local machine failure, cloud service shutdown, or tool migration

### How Multiple Projects Feed One Playbook

```
Project A  ─────────────────────────────────┐
  └─ identifies improvement in PROCESS_IMPROVEMENTS.md │
                                                       ↓
Project B (another project) ─────────────────────────→ PR to
  └─ identifies different improvement                   canonical
                                                       playbook repo
Project C (colleague's project) ─────────────────────┘
  └─ identifies third improvement                      │
                                                       ↓
                                              Maintainer reviews
                                              Merges approved PRs
                                                       │
                                                       ↓
                                              Playbook v1.1, v1.2...
                                                       │
                                              All projects pull
                                              latest improvements
```

### How to Share the Playbook

Option A — Share the GitHub URL: `github.com/[username]/claude-kickoff-playbook`
Recipient forks it, uses it for their project, optionally contributes improvements back.

Option B — Download the zip from this session and share the file directly.
Recipient uses it as a starting point without GitHub access.

Option C — Reference the playbook in your project README:
```
This project uses the Claude Kickoff Playbook v1.0
github.com/[username]/claude-kickoff-playbook
```
Recipients can then find, use, and contribute to the canonical playbook.

### What "Learning from All Projects" Means in Practice

The playbook does not automatically learn. No AI reads every project and synthesises improvements. Instead, the humans using the playbook are the learning mechanism:

1. Each project generates improvements in its own `PROCESS_IMPROVEMENTS.md`
2. The humans who maintain those projects submit improvements to the canonical repo
3. The maintainer reviews and merges
4. The playbook version increments
5. Every project that pulls the latest version gets the improvements

This is deliberate. Automatic learning without human review would let bad rules accumulate. The human gate is what makes the playbook trustworthy.

---

## Part 10 — The Audit System

### Three Levels

**Session-level (every session):** The session-start and session-end checklists in Part 4.

**Milestone-level (every phase completion):** At the end of each major project phase, answer:
- Can every change be traced to a CHANGELOG.md entry?
- Were there any changes applied without pre-change verification?
- Were there user-reported bugs or regressions?
- Were there any improvements identified that were not documented?

Output: `docs/process-health-YYYY-MM.md` in the project folder.

**Retrospective-level (every 90 days):** Four questions:
1. What is working and must be protected?
2. What is not working and must change?
3. What new failure modes have emerged?
4. What would a new Claude session need to know to operate at the same quality level?

Output: Updated process documents + `docs/retrospective-YYYY-MM.md`.

### Health Metrics

| Metric | Definition | Target |
|---|---|---|
| CHANGELOG coverage | % of sessions with a CHANGELOG entry | 100% |
| Verification completeness | % of changes with pre + post verification | ≥ 95% |
| Regression rate | User-reported regressions per 10 sessions | 0 |
| Debt backlog | Open debt items in TODO.md | 0 |
| Improvement rate | Approved improvements per 90 days | ≥ 1 |
| Stale value rate | Old strings/values found in production after a change | 0 |

---

## Part 11 — The Honest Limitations

Every playbook should acknowledge what it cannot do. These are the gaps.

| Limitation | Reality |
|---|---|
| Visual regression | Claude cannot compare screenshots. Humans must visually verify UI changes. |
| Cross-browser testing | Testing in one browser does not cover all. Humans must check critical browsers. |
| Real-time monitoring | Claude cannot watch production in real time. Monitoring tools (Betterstack, Sentry) do this. |
| Concurrent sessions | If two sessions run simultaneously, CHANGELOG may conflict. Resolution: prepend entries. |
| Automatic improvement | The playbook does not self-update. Humans must submit and approve improvements. |
| Cross-project context | Claude working in Project A does not know about Project B, even if both use this playbook. |

---

## Part 12 — Quick Reference Card

Cut this out and keep it visible during sessions.

```
BEFORE EVERY SESSION:
  1. Read Current_Status.md
  2. Read last 2 CHANGELOG entries
  3. Read TODO.md in-progress items
  4. Baseline health check

BEFORE EVERY CHANGE:
  1. Read current state (don't assume)
  2. Confirm target exists as expected
  3. Check for duplicate occurrences
  4. Confirm replacement not already present
  5. Apply change
  6. Verify: old gone + new present + system works

BEFORE ENDING EVERY SESSION:
  1. Update CHANGELOG.md
  2. Update TODO.md
  3. Update Current_Status.md
  4. Add to PROCESS_IMPROVEMENTS.md if anything was learned
  5. Check session-end audit checklist

THE THREE THINGS THAT MUST NEVER HAPPEN:
  ✗ Acting on assumed state instead of verified state
  ✗ Ending a session without updating CHANGELOG.md
  ✗ Adding an improvement to the playbook without human approval
```

---

*This playbook is version 1.1. The best version is always the next one.*
*Submit improvements to: [your GitHub repo URL]*
