# The Improvement System — Complete Specification
**Playbook section:** Part 8
**Version:** 1.0

---

## The Core Problem This System Solves

A process defined once and never revisited decays. The conditions change — the project grows, the tooling evolves, new failure modes emerge, expectations shift. Without a deliberate mechanism for improvement, a playbook becomes outdated the moment it is written.

The Improvement System treats the playbook as a product: it is built, measured, iterated, and improved on a defined cadence, using real evidence from real projects.

---

## The Three Participants

**Claude** — observes sessions, identifies friction points and failure modes, drafts improvement proposals.

**The Human** — reviews proposals, approves or rejects, controls what enters the canonical playbook. The final authority.

**The Playbook Repository** — the canonical source of truth that receives approved improvements and distributes them to all future projects.

---

## The Improvement Lifecycle

```
OBSERVE
Claude notices a failure mode, a repeated friction, or a gap in the rules.
Happens organically during any session.
    ↓
DOCUMENT
Claude adds an entry to the project's PROCESS_IMPROVEMENTS.md.
Status: proposed.
All fields filled in — especially Evidence (required) and Tradeoffs (required).
    ↓
REVIEW
Human reads the proposal at session end or async.
Asks the five approval questions (below).
Marks: approved / rejected / needs-modification.
    ↓
PROMOTE (if approved)
Approved entry is submitted to the canonical playbook repository.
Either as a GitHub PR or by the maintainer directly.
    ↓
MERGE
Maintainer reviews, merges, increments playbook version.
CHANGELOG.md of the playbook is updated.
    ↓
DISTRIBUTE
All projects that pull the latest playbook receive the improvement.
The improvement is now part of the permanent record.
```

---

## The Five Approval Questions

The human asks these before approving any improvement:

1. **Does this rule prevent a real, observed failure mode?**
   Hypotheticals are not sufficient. There must be a specific example from a real project session.

2. **Is the rule specific enough to apply consistently?**
   A rule like "be careful" is not a rule. A rule like "run a pre-change verification before modifying any n8n workflow node" is a rule.

3. **Is the cost (friction) proportional to the benefit (errors prevented)?**
   Every rule adds overhead. If the overhead exceeds the errors prevented, the rule is net negative.

4. **Does this rule conflict with any existing rule?**
   Read the existing rules before approving. Conflicts must be resolved — either by updating the existing rule or modifying the proposal.

5. **Would this rule work on a different type of project?**
   If the improvement is specific to one tool or one project type, it may not belong in the universal playbook. It may instead belong in a project-specific extension of the playbook.

---

## Types of Improvements

### Rule Addition
A new rule that addresses a failure mode not currently covered.
Example: "Add a credential health check to the session-start audit."

### Rule Modification
An existing rule that is too vague, too broad, or creates unnecessary friction.
Example: "The pre-change verification in Step 2 should specifically require reading the current n8n workflow JSON, not just any form of inspection."

### Rule Removal
A rule that consistently creates friction without preventing errors.
Example: Removing a step that was added for one specific project type and does not apply to others.

### Template Update
A change to the template files — START-HERE.md, INSTRUCTIONS.md, CHANGELOG format, etc.
Example: Adding a new field to the CHANGELOG entry format that was found to be useful.

### New Template
A new file that should be part of every project using the playbook.
Example: Adding a RISK_REGISTER.md template for projects with regulatory constraints.

---

## The Improvement ID System

All improvements use sequential numbering across the lifetime of the playbook:

- Project A improvement: IMPROVEMENT-0001, IMPROVEMENT-0002
- Project B improvement: IMPROVEMENT-0003
- Project A improvement: IMPROVEMENT-0004
- etc.

The ID is assigned when the improvement is first documented in any project. The canonical playbook maintains a global counter.

When submitting an improvement from a project to the playbook, include the project-level ID in the PR description. The maintainer assigns the global ID at merge time.

---

## What Makes a Good Improvement Proposal

**Strong proposals have all of these:**
- A specific failure mode that was observed in a real session
- A clear rule written as it would appear in the playbook (not as a vague suggestion)
- An honest tradeoff analysis
- A narrow scope (one thing, done well)

**Weak proposals that will be rejected:**
- "Claude should be more careful about X" (too vague)
- "We should always do Y" without evidence that not doing Y caused a problem
- Rules that only apply to one specific project or tool
- Rules that add significant friction to prevent a failure that has never actually occurred

---

## The Deprecation Process

Rules can be removed if they are consistently violated (suggesting they create more friction than value) or if they are superseded by a better rule.

Deprecation proposal format:
```
DEPRECATION-[NNNN] — [Rule to remove]
**Current rule text:** [exact text from playbook]
**Reason for removal:** [specific evidence that this rule is net negative]
**Replacement rule (if any):** [exact text of replacement, or "none"]
```

Deprecation proposals go through the same review and approval process as improvement proposals.

---

## The Playbook's Own CHANGELOG

The canonical playbook maintains its own CHANGELOG.md that records:
- Every improvement merged and its source project
- Every rule modified or removed and the reason
- Every version increment and what changed

This makes the playbook's own history traceable — just as it requires all projects to make their changes traceable.

---

## Self-Improvement as a Metric

The playbook is healthy when:
- At least one improvement is submitted per 90 days of active use
- The rejection rate is below 30% (if too many are rejected, the submission quality is low)
- No approved improvement is found to create more problems than it solves (requires the milestone audit to catch)
- The playbook's own CHANGELOG shows continuous, measured evolution

A playbook that has not improved in 180 days is either perfect (impossible) or being used by people who are not engaging with the improvement system (likely).
