# Case Study: Sathia — April 2026
**Project type:** Consumer AI platform, pre-launch MVP
**Founder:** Paul Poulose (employed full-time at Centene during build)
**Duration:** Ongoing from April 2026
**Playbook version used:** 1.0

---

## Project Context

Sathia is an intelligent orchestration platform built as a side project while Paul is employed full-time. The product positions itself as "not AI — the layer that makes any AI yours." Key constraints: generic consumer positioning only (no healthcare marketing during Centene employment), no developer hired for Phase 0, ~25 hours/week available.

## What Worked Well

### The distilled CONTEXT/ file structure
Keeping CONTEXT files under 400 words each was the single most impactful structural decision. Sessions that started by reading three short, accurate context files were immediately productive. Sessions that tried to load longer documents spent the first exchanges correcting context rather than doing work.

**Lesson:** Context files are for orientation, not documentation. Keep them short.

### The Decisions_Log.md pattern
Maintaining a single file of locked decisions (with the exact table format) prevented Claude from re-debating settled questions. Once "n8n self-hosted from Phase 0" was in the Decisions_Log, no session re-opened that question.

**Lesson:** Decisions that are made should be written down in a dedicated file. If it's not in the Decisions_Log, Claude will sometimes suggest alternatives.

### The 48-hour MVP concept before any infrastructure
Building the morning brief using Make.com before setting up n8n was recommended as a way to validate the core loop cheaply. The insight: the smallest thing that can tell you whether you'll use the product daily is worth building before spending thousands on infrastructure.

**Lesson:** Define a "behavior change test" before building. If the founder doesn't use the MVP daily after 30 days, do not invest further.

## What Generated Improvements

### The Make.com → n8n migration avoided
The original plan included Make.com for Phase 0 and migrating to n8n at Phase 1. The discovery of Claude + MCP eliminating the n8n learning curve made this migration unnecessary. Starting with n8n self-hosted from day one saved an estimated 20-40 hours of migration work.

**Improvement identified:** The session-start audit should include a check for newly available tools that might change the recommended stack before the Phase 0 build begins. (Proposed as IMPROVEMENT-0001)

### The context file length problem
Early context files in this project were too long — the MEMORY.md was 554 words. Loading it consumed context window before any work began.

**Improvement identified:** The playbook should specify a maximum word count for each CONTEXT/ file type and enforce it during project setup. (Proposed as IMPROVEMENT-0002)

## Metrics from This Project

| Metric | Observed | Target |
|---|---|---|
| CHANGELOG coverage | 100% (setup session documented) | 100% |
| Improvements identified | 2 (both proposed, pending review) | ≥ 1 per 90 days |
| Context files over 400 words | 1 (MEMORY.md at 554 words) | 0 |
| Decisions re-opened after Decisions_Log entry | 0 | 0 |

---

*This case study is submitted as a reference for the canonical playbook.*
*Improvements IMPROVEMENT-0001 and IMPROVEMENT-0002 are submitted for review.*
