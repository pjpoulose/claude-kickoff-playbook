---
> **TEMPLATE NOTE:** This file contains placeholders in [SQUARE BRACKETS].
> Replace every placeholder with your project-specific values before use.
> Search for [ to find all placeholders that need filling in.
---

# CHECKPOINT FORMAT — Structured Save/Commit Standard
**Adapted from:** Structured Checkpoint Format (Manus)
**Scope:** Every CHANGELOG.md entry in [PROJECT NAME]

---

## Purpose

A CHANGELOG entry is the only metadata that persists across context compaction, session restarts, and environment rebuilds. If it is written in vague prose, the history is unreadable. If it follows a fixed schema, the history becomes a queryable audit trail.

Every CHANGELOG.md entry in [PROJECT NAME] follows this format.

---

## The Template

```
---

## [YYYY-MM-DD HH:MM] — <Short title of the change>

**Scope:** <category from controlled vocabulary below>
**Files/Services:** <comma-separated list of what was changed>

### Request
<Verbatim or close paraphrase of what [OWNER] asked for>

### Changes Made
| File / Service | Nature of Change |
|---|---|
| `OPERATIONS/[ORCHESTRATION TOOL]_Setup_Guide.md` | Updated [HOSTING PLATFORM] env vars section with [DATABASE TOOL] SSL flag |
| [ORCHESTRATION TOOL] workflow: Morning Brief | Added [CALENDAR SERVICE] node between [EMAIL SERVICE] read and Claude API |

### Decisions and Reasoning
<Why was this approach chosen over alternatives? What was explicitly rejected? What edge cases were noted?>

### Verification Steps
- [ ] Pre-change: confirmed current state before modifying
- [ ] Post-change: confirmed change applied correctly
- [ ] [ORCHESTRATION TOOL] test: workflow executed successfully (if applicable)
- [ ] Visual check: site/app verified in browser (if applicable)
- [ ] Other: <any additional verification>

### Known Limitations or Follow-up Items
<Anything deferred, incomplete, or requiring a future action>
```

---

## Scope Vocabulary (Use Exactly One)

| Value | When to Use |
|---|---|
| `Workflow` | [ORCHESTRATION TOOL] workflow creation, modification, or deletion |
| `Credential` | Adding, rotating, or removing API keys, OAuth tokens, or secrets |
| `Schema` | [DATABASE TOOL] table creation, column addition, or RLS rule changes |
| `Config` | Environment variables, [HOSTING PLATFORM] settings, [DNS/CDN PROVIDER] rules, [FRONTEND HOST] settings |
| `Copy` | User-visible text on [project-domain.com] or the app — headlines, body, labels |
| `SEO` | Meta tags, OG tags, structured data, sitemaps, robots.txt |
| `Brand` | Design system changes, visual identity updates, tagline changes |
| `Feature` | New user-facing functionality in the web app or automations |
| `Integration` | New OAuth connection, MCP connector, or external API connection |
| `Infra` | [HOSTING PLATFORM] deployment, [FRONTEND HOST] deployment, [DNS/CDN PROVIDER] zone changes |
| `Bug Fix` | Correcting broken or incorrect behaviour |
| `Docs` | Changes to process documents, READMEs, or this CoWork folder |
| `Strategy` | Decisions about product direction, positioning, or technology choices |
| `Multi` | When a single session spans two or more categories |

---

## Verification Vocabulary (VERIFIED Field)

| Value | Meaning |
|---|---|
| `pre-read` | Current state of the target was read before the change was made |
| `post-check` | Change was verified as applied correctly after execution |
| `[ORCHESTRATION TOOL]-test` | Workflow was triggered manually and execution log showed expected output |
| `[DATABASE TOOL]-query` | Test query confirmed schema change applied correctly |
| `browser-check` | [project-domain.com] or app loaded in browser and change was visually confirmed |
| `credential-test` | [ORCHESTRATION TOOL] test operation confirmed credential is active and working |
| `env-check` | [HOSTING PLATFORM] Variables tab confirmed environment variable is set correctly |
| `mcp-confirm` | Claude Desktop MCP confirmed [ORCHESTRATION TOOL] workflow state matches expectation |

---

## Anti-Patterns (Never Do These)

| Anti-Pattern | Why It Fails | Correct Approach |
|---|---|---|
| "Updated the workflow" | Does not say which workflow or what changed | Name the workflow, describe every node change |
| "Fixed credential issue" | Does not identify the credential or the issue | Name the service, describe the symptom and the fix |
| "Various improvements" | Meaningless for audit or rollback | List every change individually |
| Empty Decisions section | Loses the reasoning the moment context compacts | Write at least two sentences — why this approach, why not another |
| Skipping verification | Implies no checks were run | Always list at minimum pre-read + post-check |

---

## Using the Format for Rollback Decisions

When something breaks:
1. Read CHANGELOG.md newest-first
2. Find the entry where the Scope and Changes fields match the broken area
3. The Files/Services field tells you exactly what to look at
4. The Decisions and Reasoning field tells you why it was done this way — critical for knowing whether to roll back or fix forward

A well-maintained CHANGELOG means "which version broke this?" is answerable in under two minutes.

---

## Complete Examples

### Example 1: [ORCHESTRATION TOOL] Workflow Change

```
## [2026-05-02 07:15] — Morning Brief: Added [CALENDAR SERVICE] node

**Scope:** Workflow
**Files/Services:** [ORCHESTRATION TOOL] workflow: [PROJECT NAME] Morning Brief

### Request
Add [CALENDAR SERVICE] to the morning brief so it includes today's meetings alongside the email summary.

### Changes Made
| Service | Nature of Change |
|---|---|
| [ORCHESTRATION TOOL] workflow: Morning Brief | Added [CALENDAR SERVICE] node between [EMAIL SERVICE] read and Claude summarise node |
| [ORCHESTRATION TOOL] workflow: Morning Brief | Updated Claude system prompt to include calendar events in brief structure |

### Decisions and Reasoning
Added the [CALENDAR SERVICE] node before the Claude call (not after) so that Claude receives both email and calendar data in a single prompt and can produce a unified brief rather than two separate sections. Considered running them in parallel but the sequential approach is simpler to debug if the [CALENDAR SERVICE] API call fails.

### Verification Steps
- [x] Pre-change: read current workflow via MCP, confirmed [EMAIL SERVICE] node was the last data source
- [x] Post-change: workflow executed manually — calendar events appeared in the brief output
- [x] [ORCHESTRATION TOOL]-test: execution log showed all nodes ran successfully, output contained today's meetings
- [x] browser-check: email received at [owner]@[email-service.com] — calendar section present and formatted correctly

### Known Limitations or Follow-up Items
The [CALENDAR SERVICE] node only reads [OWNER]'s primary [CALENDAR SERVICE]. Multiple calendars need a Phase 1 enhancement.
```

---

### Example 2: Credential Addition

```
## [2026-05-03 20:30] — Added [CHAT PLATFORM] Bot credential to [ORCHESTRATION TOOL]

**Scope:** Credential
**Files/Services:** [ORCHESTRATION TOOL] credentials store

### Request
Connect the [CHAT PLATFORM] bot to [ORCHESTRATION TOOL] so it can route incoming messages to Claude Haiku.

### Changes Made
| Service | Nature of Change |
|---|---|
| [ORCHESTRATION TOOL] credentials | Added "[CHAT PLATFORM] Bot — [PROJECT NAME]AI_bot" with token from @BotFather |
| [ORCHESTRATION TOOL] workflow: [CHAT PLATFORM] Router | Created new workflow using [CHAT PLATFORM] Bot credential |

### Decisions and Reasoning
Used [ORCHESTRATION TOOL]'s native [CHAT PLATFORM] Bot module rather than the HTTP Request module. Native module handles long polling setup automatically and provides structured message objects. HTTP approach was considered but adds unnecessary complexity for a standard [CHAT PLATFORM] integration.

### Verification Steps
- [x] pre-read: confirmed no existing [CHAT PLATFORM] credential in [ORCHESTRATION TOOL] before adding
- [x] credential-test: sent "hello" to @[PROJECT NAME]AI_bot — [ORCHESTRATION TOOL] execution log showed message received
- [x] post-check: routing workflow correctly classified message as "answer" category
- [x] [ORCHESTRATION TOOL]-test: Claude Haiku responded via [CHAT PLATFORM] within 3 seconds

### Known Limitations or Follow-up Items
[CHAT PLATFORM] polling runs every 1 minute on the free [ORCHESTRATION TOOL] trigger. Upgrade to [ORCHESTRATION TOOL] Pro for webhook-based real-time response if latency becomes an issue.
```

---
*Version 1.0 — [PROJECT NAME] | April 2026*
