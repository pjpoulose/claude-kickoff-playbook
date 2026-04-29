---
> **TEMPLATE NOTE:** This file contains placeholders in `[SQUARE BRACKETS]`.
> Replace every placeholder with your project-specific values before use.
> Search for `[` to find all placeholders that need filling in.
---

# [PROJECT NAME] — AI-Assisted Development Process Playbook
**Version:** 1.0 | **Adapted from:** Manus AI-Assisted Development Process Playbook
**Scope:** All AI-assisted development, configuration, and content work on [PROJECT NAME]

---

## Why This Playbook Exists

Every error in AI-assisted development comes from one of three sources:
1. Acting on an assumed state instead of a verified state
2. Failing to record why decisions were made before the context window closes
3. Having no structured way to roll back when something breaks

This playbook eliminates all three by making verification mandatory, memory persistent, and rollback systematic.

---

## The Six Process Rules

### Rule 1 — Read Before Acting (No Assumptions)

Before modifying anything — a workflow, a database table, a file, a config value — read the current state first. Never act on what you think it contains.

**For [ORCHESTRATION TOOL] workflows:**
```
Claude Desktop: "Show me the current state of the [workflow name] workflow"
→ [ORCHESTRATION TOOL]-workflow-builder MCP returns the full workflow JSON
→ Confirm the structure before describing any changes
```

**For [DATABASE TOOL] tables/schema:**
```
[DATABASE TOOL] Dashboard → Table Editor → read current columns and row-level security rules
→ Never assume a column exists — verify it
```

**For website/app files:**
```
Read the file → identify exact current string → confirm it exists → then describe the change
Never edit based on a paraphrase or approximation of what the file contains
```

**For environment variables:**
```
[HOSTING PLATFORM] Dashboard → Variables → read current values
Never assume a variable is set — confirm it in the dashboard before building a workflow that depends on it
```

---

### Rule 2 — Verify Before and After Every Change

Every change has two verification moments: before (confirm the target state exists) and after (confirm the change landed correctly).

**The Pre-Change Verification Protocol:**

| Context | Before the change | After the change |
|---|---|---|
| [ORCHESTRATION TOOL] workflow node | Read current node config via MCP | Execute test run → verify output matches expected |
| [ORCHESTRATION TOOL] workflow addition | Confirm the workflow runs cleanly without the new node | Activate → trigger manually → inspect execution log |
| [DATABASE TOOL] schema change | Read current table structure | Run a test query → confirm column/row returns correctly |
| Website copy change | Confirm old string exists in the file | Confirm old string is absent + new string is present |
| Environment variable | Read current value in [HOSTING PLATFORM] | Run a workflow that uses it → confirm it resolves |
| Credential addition | Confirm credential type is correct in [ORCHESTRATION TOOL] | Run a test operation using the credential |

**The post-change question to ask every time:**
"Does the system behave exactly as expected with this change in place? If something went wrong right now, what is the rollback?"

---

### Rule 3 — Scope Changes Explicitly Before Starting

For any task involving more than three changes, create an explicit phase plan before starting. List every change, assign each a number, and track completion against the list.

**Example phase plan (website copy brief):**
```
Phase 1: Changes 1–4 (hero section)
Phase 2: Changes 5–12 (sections 01–04)
Phase 3: Changes 13–20 (sections 05–08)
Phase 4: Changes 21–24 (footer, meta, SEO)
```

Never start Phase 2 before Phase 1 is verified complete. Progress is only real when it is verified, not just applied.

---

### Rule 4 — CHANGELOG.md Is Mandatory, Not Optional

Every session that changes anything must update CHANGELOG.md before the session ends. The CHANGELOG is the persistent memory that survives context window limits, CoWork session restarts, and even a complete rebuild of the environment.

The entry must be written BEFORE the final save/commit, not after.

If the CHANGELOG entry is skipped, that session's changes are untracked. Untracked changes create debt that compounds.

See `OPERATIONS/Checkpoint_Format.md` for the exact entry structure.

---

### Rule 5 — TODO.md Is the Single Source of Truth for What Is Left

Every action that produces something incomplete, deferred, or flagged must create a TODO.md entry before the session ends. TODO.md is updated at every session end — not monthly, not when you remember.

Three states exist in TODO.md: in progress, next up, and completed. Nothing is "in my head."

---

### Rule 6 — All Outputs Are Named and Dated

Every file Claude produces goes to `OUTPUTS/YYYY-MM-DD-descriptive-name.ext`. Never save to the root, never overwrite without a new dated name.

This creates a history of every deliverable that is searchable by date and topic. Six months from now you will thank yourself for this.

---

## The Context Loss Problem (and How This Playbook Solves It)

The core problem in AI-assisted development: session context compacts. When a conversation exceeds the context window, reasoning history is replaced with a summary. The summary captures *what* was done but loses *why*, *what was rejected*, and *what edge cases were noted*.

**[PROJECT NAME]'s three-layer protection:**

| Layer | Mechanism | Survives |
|---|---|---|
| Short-term | CONTEXT/Current_Status.md — updated each session | Session restart |
| Medium-term | CHANGELOG.md — every decision and verification recorded | Context compaction |
| Long-term | STRATEGY/Decisions_Log.md — locked decisions | Project lifetime |

**The session-start ritual** (in OPERATIONS/Session_Audit.md) is the mechanism that re-establishes context at the start of each new session by reading these three files before doing any work.

---

## What This Playbook Does Not Cover (Honest Limitations)

| Gap | Reality |
|---|---|
| Visual regression | Claude cannot compare screenshots automatically. The human ([OWNER]) must visually verify website changes in the browser |
| Cross-browser testing | [ORCHESTRATION TOOL] and web app testing happens in one environment. Safari and iOS rendering must be checked manually |
| Concurrent sessions | If [OWNER] and Claude are both making changes simultaneously, the CHANGELOG may conflict. Resolution: prepend entries, preserve both |
| Real-time monitoring | Claude cannot watch production metrics in real time. [UPTIME MONITOR] handles this — Claude responds when [OWNER] shares alert details |

---

## Adapted Rules — What Was Left Behind

The following rules from the original Manus playbook are Manus-specific and do not apply to [PROJECT NAME]:

| Original rule | Why not applicable | [PROJECT NAME] equivalent |
|---|---|---|
| `npx tsc --noEmit` | TypeScript compiler check | [ORCHESTRATION TOOL] test execution + [DATABASE TOOL] query test |
| `webdev_save_checkpoint` | Manus-specific tool | Git commit with structured message |
| `webdev_rollback_checkpoint` | Manus-specific tool | Git revert + [ORCHESTRATION TOOL] workflow rollback |
| Screenshot review before checkpoint | Manus Management UI | Browser preview of site + [ORCHESTRATION TOOL] execution log |
| Manus version history | Manus-specific | Git log + CHANGELOG.md |

---
*Version 1.0 — [PROJECT NAME] | April 2026*
