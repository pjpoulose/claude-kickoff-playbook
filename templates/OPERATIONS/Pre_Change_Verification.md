# PRE-CHANGE VERIFICATION PROTOCOL
**Adapted from:** Mandatory Pre-Edit Grep Audit (Manus)
**Scope:** Every change to n8n workflows, Supabase schema, configuration values, or files

---

## Purpose

The most common error in AI-assisted development is modifying something based on what you think it contains rather than what it actually contains. This protocol eliminates that error class by requiring confirmation of the current state before any change is applied.

---

## When This Protocol Is Required

Required before **every** change involving:
- Modifying an existing n8n workflow node or connection
- Changing a Supabase table column, RLS rule, or migration
- Updating an environment variable value
- Editing a file (code, content, config)
- Removing or replacing a credential

**Not required for:**
- Creating a new workflow from scratch (no prior state to verify)
- Creating a new Supabase table that does not yet exist
- Appending to the end of a file where the append point is unambiguous
- Running commands that do not modify state (health checks, status reads)

---

## The Five-Step Protocol

### Step 1 — Read the Current State

Before describing any change, read what currently exists.

**For n8n workflows:**
```
Claude Desktop: "Show me the full configuration of the [workflow name] workflow"
→ MCP returns current JSON
→ Identify the exact node you intend to modify
→ Note the current configuration values
```

**For Supabase schema:**
```
Supabase Dashboard → Table Editor → click the target table
→ Read every column name and type
→ Read any RLS rules on the table
→ Confirm the column you intend to modify exists and has the type you expect
```

**For environment variables:**
```
Railway Dashboard → your service → Variables tab
→ Confirm the variable name exactly as it appears
→ Note the current value (or confirm it is set vs. absent)
```

**For files:**
```
Read the file via Claude Desktop or bash
→ Identify the exact current string you intend to replace
→ Do not paraphrase — note the literal text
```

---

### Step 2 — Confirm the Target Exists

Before changing anything, confirm the thing you intend to change actually exists in its expected form.

**For n8n workflow nodes:** Confirm the node name and position in the workflow JSON.
**For Supabase:** Confirm the column name matches exactly (case-sensitive).
**For environment variables:** Confirm the variable key name matches exactly.
**For file content:** Confirm the exact string exists in the file.

If the target does not exist as expected: stop. Re-read the current state. Find out what is actually there before proceeding.

---

### Step 3 — Check for Duplicates

If the same string or configuration exists in multiple places, changing one occurrence and missing another creates inconsistency.

**For files:** Check if the same string appears more than once. If it does, decide explicitly: are you changing all occurrences or specific ones? Record this decision in the CHANGELOG entry.

**For n8n workflows:** Check if the same node type or configuration appears in multiple workflows. If so, determine whether all need to be updated.

**For environment variables:** Check if the same variable name exists in multiple Railway services (production vs. staging). Update all relevant environments.

---

### Step 4 — Confirm the Replacement Does Not Already Exist

Before applying the change, confirm the new value is not already present. If it is, the change may have already been applied in a previous session.

If the new value already exists where you expect to set it, do not re-apply. Record in CHANGELOG that the change was verified as already present.

---

### Step 5 — Apply the Change

Only after Steps 1–4 have passed may the change be applied. Describe the change with the exact current values confirmed in Step 1–2 as reference.

---

### Step 6 — Post-Change Verification

Immediately after the change is applied, verify it took effect correctly.

**For n8n workflows:**
```
Trigger the workflow manually
→ Inspect the execution log
→ Confirm: did the modified node produce the expected output?
→ Confirm: did any downstream nodes that depend on it still behave correctly?
```

**For Supabase schema:**
```
Run a test query against the modified table
→ SELECT the new column / use the new RLS rule
→ Confirm: does the query return the expected result?
```

**For environment variables:**
```
Run a workflow or operation that uses the variable
→ Confirm: did it resolve correctly (no "undefined" errors)?
```

**For file content:**
```
Read the file after the edit
→ Confirm: old string is absent
→ Confirm: new string is present at the expected location
```

**For website copy:**
```
Load the relevant page in the browser
→ Confirm: old text is not visible
→ Confirm: new text appears correctly formatted
```

---

## Common Failure Modes for Sathia

### Failure Mode 1: Credential name mismatch
An n8n workflow references "Google OAuth2 — Paul" but the credential in n8n was saved as "Google OAuth2 (Paul)". The workflow fails silently.

**Resolution:** Before building any workflow that uses a credential, read the exact credential name from n8n → Credentials list. Use that exact name in the workflow description.

---

### Failure Mode 2: n8n workflow JSON structure assumed incorrectly
A previous session created a workflow. A new session tries to modify it, but the MCP description of the change references a node name or position that has changed.

**Resolution:** Always call "Show me the [workflow name] workflow" via MCP before describing any modifications. Read the response before specifying changes.

---

### Failure Mode 3: Environment variable set in wrong Railway service
Sathia has multiple Railway services (n8n, LiteLLM). A variable added to the n8n service is assumed to be in LiteLLM.

**Resolution:** Check the Railway service name explicitly before adding or modifying variables. State the service name in every CHANGELOG entry.

---

### Failure Mode 4: Supabase column assumed to exist
A workflow writes to a column that was planned but not yet created in the database.

**Resolution:** Always check the Supabase table structure before building any workflow that writes to it. Add the column creation step to TODO.md if it does not yet exist.

---

### Failure Mode 5: OAuth token assumed to be valid
An n8n workflow fails because a Google OAuth token expired between sessions.

**Resolution:** Add "credential health check" to the session-start audit. After any session gap longer than one week, test each OAuth credential with a simple read operation before building workflows that depend on it.

---

## Quick Reference Card

| Step | Action | Pass Condition | Fail Action |
|---|---|---|---|
| 1 | Read current state of target | Current state is known precisely | Re-read more carefully |
| 2 | Confirm target exists as expected | Target found at expected location | Investigate actual state |
| 3 | Check for duplicates | Scope of change is explicitly decided | Decide and document scope |
| 4 | Confirm replacement not already present | New value not yet applied | Verify if already done |
| 5 | Apply the change | Change applied | Check description specificity |
| 6 | Verify post-change | System behaves as expected | Re-read and re-apply |

---
*Version 1.0 — Sathia | April 2026*
