# Getting Started — New Project Setup
**Time required: 20 minutes**
**What you get: A fully structured CoWork project that works correctly from minute one**

---

## Step 1 — Create Your Project Folder (2 min)

Create a folder on your computer for your project. Give it a clear name.

```
~/Documents/[project-name]/
```

Do not put it in Downloads or Desktop. It needs a stable path that will not move.

---

## Step 2 — Copy the Templates (2 min)

Copy the entire `templates/` folder from this playbook into your project folder. Rename the copied folder contents to match your project.

Your project folder should now contain:
```
[project-name]/
├── START-HERE.md
├── INSTRUCTIONS.md
├── MEMORY.md
├── CHANGELOG.md
├── TODO.md
├── PROCESS_IMPROVEMENTS.md
├── COWORK_INSTRUCTIONS.md
├── CONTEXT/
│   ├── Project_Brief.md
│   ├── Owner_Profile.md
│   └── Current_Status.md
├── STRATEGY/
│   └── Decisions_Log.md
├── OPERATIONS/
│   ├── Process_Playbook.md
│   ├── Session_Audit.md
│   ├── Checkpoint_Format.md
│   └── Pre_Change_Verification.md
├── TEMPLATES/
│   ├── Task_Brief.md
│   └── Developer_Brief.md
└── OUTPUTS/
```

---

## Step 3 — Fill In the Context Files (10 min)

Open each file in `CONTEXT/` and fill in your project-specific information. These are the files Claude reads at the start of every session — keep them under 400 words each.

**CONTEXT/Project_Brief.md** — Answer these:
- What is this project? (one paragraph)
- What does it do for users? (one sentence)
- What is the current phase?
- What are the three most important things to know about it?

**CONTEXT/Owner_Profile.md** — Answer these:
- Your name and background
- Your communication style (direct? detailed? prefers options or recommendations?)
- What you are trying to achieve with this project
- How many hours per week you are working on it
- What you cannot or will not do (technical limitations, constraints)

**CONTEXT/Current_Status.md** — Answer these:
- What exists right now?
- What is being built next?
- What are the immediate next actions this week?
- What decisions have been made that cannot be undone?

---

## Step 4 — Update START-HERE.md (3 min)

Open `START-HERE.md` and replace all `[PLACEHOLDER]` text with your project-specific values. This is the first file Claude reads every session — it must be accurate.

---

## Step 5 — Set Up CoWork Project in Claude Desktop (3 min)

1. Open Claude Desktop → click **Cowork** tab
2. Click **Projects** in the left sidebar → click **+**
3. Select **"Use an existing folder"**
4. Navigate to your project folder and select it
5. Name the project
6. In the **Instructions** field, copy and paste the entire contents of `COWORK_INSTRUCTIONS.md`
7. Click **Create**

---

## Step 6 — First Session Verification

Open your new CoWork project. Type exactly:

```
Read START-HERE.md, INSTRUCTIONS.md, and CONTEXT/Current_Status.md.
Tell me: do these files accurately describe this project and what needs 
to be done next? Point out anything that seems incomplete or unclear.
```

Claude will read the context and surface any gaps. Fix those gaps now, before the project begins.

---

## Step 7 — Add This Playbook as a Reference (Optional but Recommended)

Add a line to your project's `START-HERE.md`:

```
This project follows the Claude Kickoff Playbook v1.0
Reference: [your playbook GitHub URL]
```

This ensures that anyone opening the project — including future Claude sessions — knows there is a canonical process document to reference.

---

## You Are Ready

Your project is set up correctly. The first real work session can begin.

The most important habit to build from session one: **update CHANGELOG.md and CONTEXT/Current_Status.md before you close every session.** These two files are your project's memory. Without them, every session starts from zero.

---

## Troubleshooting Common Setup Issues

**CoWork cannot find my folder**
Ensure the folder path has no special characters or spaces. Move it to a simple path like `~/Documents/ProjectName/` if needed.

**Claude doesn't seem to read START-HERE.md automatically**
CoWork projects read their connected folder, but Claude must be told to read specific files. Begin every session with: "Read START-HERE.md before doing anything." Add this to your CoWork project instructions.

**The Instructions field in CoWork has a character limit**
Keep COWORK_INSTRUCTIONS.md under 2,000 characters. The full process documents live in OPERATIONS/ — they do not need to be in the instructions field.

**I'm not sure what to put in the Decisions_Log**
Start with: what technology choices have been made? What positioning or product decisions are locked? What constraints cannot change? Every decision that you have made and would not want Claude to second-guess goes here.
