# Why Each Rule Exists — The Evidence Behind the Playbook

Every rule in the playbook exists because of a specific failure that happened in a real project. This document explains the origin of each rule so future contributors understand not just what the rule is, but why removing it would be dangerous.

---

## Rule 1 — Read Before Acting

**The failure that created this rule:**
In the Manus website project, a developer (AI-assisted) edited a file based on what it believed the file contained — a paraphrase from memory — rather than reading the actual current file. The edit applied correctly, but to the wrong version of the text, leaving a stale occurrence in another section.

**The specific cost:**
The stale occurrence appeared in a section the developer did not know existed. It was only caught during a manual grep sweep after the checkpoint was saved.

**Why the rule works:**
Reading the current state before acting eliminates the possibility of acting on a false premise. It cannot be shortcut. A 30-second read prevents a 30-minute correction cycle.

---

## Rule 2 — Verify Before and After Every Change

**The failure that created this rule:**
Verification was inconsistent. TypeScript compilation checks caught type errors but not content errors. A copy change that applied to one occurrence missed a duplicate in another section — both TypeScript and the visual check passed.

**The specific cost:**
The stale string appeared in the live site. A user noticed. The issue required a new session to locate and fix.

**Why the rule works:**
"Old string must return zero results. New string must return at least one result." This is not auditable by TypeScript. It requires explicit string verification. Making it mandatory, not optional, closes the gap.

---

## Rule 3 — Scope Multi-Step Changes Explicitly

**The failure that created this rule:**
A 24-change brief was applied in a single session. Changes 1–18 were applied and verified. The session context compacted. The next session's summary described the work as "partially complete" but did not specify which 6 changes remained. The next session reapplied changes 1–6 (creating duplicates) instead of continuing from change 19.

**The specific cost:**
6 changes had to be reverted and re-applied. The session was spent on correction rather than progress.

**Why the rule works:**
A numbered phase plan with tracked completion status makes it unambiguous which changes are done and which remain. Context compaction cannot hide the progress state if it is written in the CHANGELOG.

---

## Rule 4 — CHANGELOG.md Is Mandatory

**The failure that created this rule:**
Session context was compacted after a significant architectural decision. The summary captured what was decided but not why — specifically, what alternatives were rejected and what edge cases were noted. The next session re-opened the decision and re-debated alternatives that had already been considered and rejected.

**The specific cost:**
30 minutes re-debating a settled question. The decision ultimately converged on the same answer — but time was lost and the human was frustrated.

**Why the rule works:**
The CHANGELOG entry for a decision includes "Decisions and Reasoning" — specifically what was rejected and why. This section is what session context summaries cannot preserve. The file survives everything; context summaries do not.

---

## Rule 5 — TODO.md Is the Single Source of Truth

**The failure that created this rule:**
A task was mentioned at the end of a session — "we should also check the credential expiry" — but not written down. The next session had no record of this observation. The credential expired in production. The failure was not caught until a workflow execution failed.

**The specific cost:**
A live workflow failed. Users affected. Emergency session to diagnose and fix.

**Why the rule works:**
If it is not in TODO.md, it does not exist as a tracked commitment. The overhead of writing one line in TODO.md is vastly less than the cost of a production failure caused by a forgotten task.

---

## Rule 6 — All Outputs Are Named and Dated

**The failure that created this rule:**
Multiple versions of the same document were saved with similar names — "marketing_plan.md", "marketing_plan_v2.md", "marketing_plan_final.md". The human opened the wrong version for a presentation. Incorrect figures were presented.

**The specific cost:**
Reputational damage. The human had to correct themselves in a meeting.

**Why the rule works:**
Date-prefixed names create an unambiguous chronological sequence. "2026-04-28-marketing-plan.md" is always the April 28 version. No "final" or "v2" required — the date is the version.

---

## The Human Approval Gate for Improvements

**Why this is non-negotiable:**
Without a human gate, AI systems that can propose their own rules will accumulate rules that optimise for AI convenience rather than human outcomes. A rule that reduces Claude's verification work may increase human rework. The human is the ultimate judge of whether a rule is net positive.

**The evidence:**
This is a design principle, not an observed failure. The failure it prevents is speculative but the mechanism is clear: unbounded self-modification without human oversight is a known risk pattern in AI systems.
