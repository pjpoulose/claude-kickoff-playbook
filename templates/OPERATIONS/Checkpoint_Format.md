# CHECKPOINT FORMAT — Structured Save/Commit Standard
**Adapted from:** Structured Checkpoint Format (Manus)
**Scope:** Every CHANGELOG.md entry in Sathia

---

## Purpose

A CHANGELOG entry is the only metadata that persists across context compaction, session restarts, and environment rebuilds. If it is written in vague prose, the history is unreadable. If it follows a fixed schema, the history becomes a queryable audit trail.

Every CHANGELOG.md entry in Sathia follows this format.

---

## The Template

```
---

## [YYYY-MM-DD HH:MM] — <Short title of the change>

**Scope:** <category from controlled vocabulary below>
**Files/Services:** <comma-separated list of what was changed>

### Request
<Verbatim or close paraphrase of what Paul asked for>

### Changes Made
| File / Service | Nature of Change |
|---|---|
| `OPERATIONS/n8n_Setup_Guide.md` | Updated Railway env vars section with Supabase SSL flag |
| n8n workflow: Morning Brief | Added Google Calendar node between Gmail read and Claude API |

### Decisions and Reasoning
<Why was this approach chosen over alternatives? What was explicitly rejected? What edge cases were noted?>

### Verification Steps
- [ ] Pre-change: confirmed current state before modifying
- [ ] Post-change: confirmed change applied correctly
- [ ] n8n test: workflow executed successfully (if applicable)
- [ ] Visual check: site/app verified in browser (if applicable)
- [ ] Other: <any additional verification>

### Known Limitations or Follow-up Items
<Anything deferred, incomplete, or requiring a future action>
```

---

## Scope Vocabulary (Use Exactly One)

| Value | When to Use |
|---|---|
| `Workflow` | n8n workflow creation, modification, or deletion |
| `Credential` | Adding, rotating, or removing API keys, OAuth tokens, or secrets |
| `Schema` | Supabase table creation, column addition, or RLS rule changes |
| `Config` | Environment variables, Railway settings, Cloudflare rules, Vercel settings |
| `Copy` | User-visible text on sathia.ai or the app — headlines, body, labels |
| `SEO` | Meta tags, OG tags, structured data, sitemaps, robots.txt |
| `Brand` | Design system changes, visual identity updates, tagline changes |
| `Feature` | New user-facing functionality in the web app or automations |
| `Integration` | New OAuth connection, MCP connector, or external API connection |
| `Infra` | Railway deployment, Vercel deployment, Cloudflare zone changes |
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
| `n8n-test` | Workflow was triggered manually and execution log showed expected output |
| `supabase-query` | Test query confirmed schema change applied correctly |
| `browser-check` | sathia.ai or app loaded in browser and change was visually confirmed |
| `credential-test` | n8n test operation confirmed credential is active and working |
| `env-check` | Railway Variables tab confirmed environment variable is set correctly |
| `mcp-confirm` | Claude Desktop MCP confirmed n8n workflow state matches expectation |

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

### Example 1: n8n Workflow Change

```
## [2026-05-02 07:15] — Morning Brief: Added Google Calendar node

**Scope:** Workflow
**Files/Services:** n8n workflow: Sathia Morning Brief

### Request
Add Google Calendar to the morning brief so it includes today's meetings alongside the email summary.

### Changes Made
| Service | Nature of Change |
|---|---|
| n8n workflow: Morning Brief | Added Google Calendar node between Gmail read and Claude summarise node |
| n8n workflow: Morning Brief | Updated Claude system prompt to include calendar events in brief structure |

### Decisions and Reasoning
Added the Calendar node before the Claude call (not after) so that Claude receives both email and calendar data in a single prompt and can produce a unified brief rather than two separate sections. Considered running them in parallel but the sequential approach is simpler to debug if the Calendar API call fails.

### Verification Steps
- [x] Pre-change: read current workflow via MCP, confirmed Gmail node was the last data source
- [x] Post-change: workflow executed manually — calendar events appeared in the brief output
- [x] n8n-test: execution log showed all nodes ran successfully, output contained today's meetings
- [x] browser-check: email received at paul@gmail.com — calendar section present and formatted correctly

### Known Limitations or Follow-up Items
The Calendar node only reads Paul's primary Google Calendar. Multiple calendars need a Phase 1 enhancement.
```

---

### Example 2: Credential Addition

```
## [2026-05-03 20:30] — Added Telegram Bot credential to n8n

**Scope:** Credential
**Files/Services:** n8n credentials store

### Request
Connect the Telegram bot to n8n so it can route incoming messages to Claude Haiku.

### Changes Made
| Service | Nature of Change |
|---|---|
| n8n credentials | Added "Telegram Bot — SathiaAI_bot" with token from @BotFather |
| n8n workflow: Telegram Router | Created new workflow using Telegram Bot credential |

### Decisions and Reasoning
Used n8n's native Telegram Bot module rather than the HTTP Request module. Native module handles long polling setup automatically and provides structured message objects. HTTP approach was considered but adds unnecessary complexity for a standard Telegram integration.

### Verification Steps
- [x] pre-read: confirmed no existing Telegram credential in n8n before adding
- [x] credential-test: sent "hello" to @SathiaAI_bot — n8n execution log showed message received
- [x] post-check: routing workflow correctly classified message as "answer" category
- [x] n8n-test: Claude Haiku responded via Telegram within 3 seconds

### Known Limitations or Follow-up Items
Telegram polling runs every 1 minute on the free n8n trigger. Upgrade to n8n Pro for webhook-based real-time response if latency becomes an issue.
```

---
*Version 1.0 — Sathia | April 2026*
