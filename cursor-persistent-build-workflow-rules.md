

## 🔧 FEATURE PROMPT RULE

Each feature must begin with the `@feature` tag, followed by feature title
The prompt must include the following fields in this order:

### 🧩 Required Format

```markdown
@feature <feature-title>

@description  
<Brief description of the feature, objective, or user problem it solves>

Example prompt
@feature user-auth-session-timeout

@description  
Implement automatic logout for users after 15 minutes of inactivity. This helps enhance account security, especially for sensitive areas like payments or admin dashboards.

@owner Nithesh M S

@owner <Owner Name> (optional)

## 🚀 WORKFLOW

### Step 1: Context Setup

- Read relevant module READMEs, and `/docs`.
- Ask clarifying questions to understand where this feature belongs.
- Document any relevant user-provided context, assumptions, or clarifications in:
  - `/codeAssistant/<feature-title>/context.md`
- DO NOT make any changes at this stage.
- Confirm understanding before proceeding.
- ✅ Update `progress.md` in codeAssistant/<feature-title> with:
  - Step 1 status: Completed
  - Timestamp
  - Path to saved context file


---

### Step 2: Generate Implementation Plan
Create a **very elaborate and detailed implementation plan** that includes:

- 🔧 Exact files and functions/classes to be created or modified
- 🧩 Input/output definitions for each function/component
- 🧠 Precise control/data flow with design diagrams if needed
- 🧪 Testing strategy (unit, integration, mocks, etc.)
- 📚 Rationale behind every design decision
- 💥 Impact on other modules or parts of the system
- 🧭 Any potential risks, constraints, or trade-offs

Once complete, ask:
> "📋 Implementation plan ready. Can I proceed?"

🛠️ **If any changes are requested by the user**, update:
- The implementation plan **and**
- The `/codeAssistant/<feature-title>/prd.md` file
accordingly before proceeding further.

✅ **Also update `progress.md`**:
- Mark Step 2 as completed
- Summarize the plan and list files to be created/modified

---

### Step 3: Break into Tasks

After plan is approved:
- Break the feature into **atomic tasks**
- Use format:

```markdown
@Task 1 Title of the first task
@Task 2 Title of the second task
```

- 💾 **Generate a `tasks.md` file** in `/codeAssistant/<feature-title>/` as a **checklist** of all the tasks. Each task should be marked as:
  - `[ ]` Pending
  - `[x]` Completed

Example:

```markdown
# Tasks for <feature-title>

- [ ] Task 1: Title of the first task
- [ ] Task 2: Title of the second task

> "🧩 Task breakdown complete and saved to `/codeAssistant/<feature-title>/tasks.md`. Shall I proceed?"
- ✅ Also update `progress.md` with:
  - Task list summary
  - Status of each task

⚠️ **At any point**, if the user requests:
- Addition of a new task
- Removal of a task
- Modification of a task title or description
- ✅ Also update `progress.md` with:
  - Task list summary
  - Status of each task

👉 **Then update** the `tasks.md` file to reflect the changes immediately.

Then ask:
> "🧩 Task breakdown complete. Shall I proceed?"

---

### Step 4: Task-by-Task Execution

For each task:
1. Say:
   > `Starting Task #<n>: <title>`
2. Explain the intended code changes.
3. Ask:
   > "🔍 Does this look good?"
4. Only if approved:
   - Apply the changes.
5. After changes are applied:
   - ✅ Update the task status in `/codeAssistant/<feature-title>/tasks.md` by marking the task as `[x]`
   - ✅ Update `progress.md` with:
     - Task completion summary
     - Files changed/created
   - Say:
     > "✅ Task #<n> completed and checklist updated."

Repeat for all tasks.

---

### Step 5: High-Level Design (HLD)

Once all tasks are complete:
- Generate a document (`/hld/<feature-title>/hld.md`)
- Include:
  - Overview
  - File/function changes
  - Design decisions
  - Edge cases
- ✅ Update `progress.md`:
  - Mark HLD as completed
  - Add summary of design insights
  - List HLD file path


Ask:
> "📄 HLD generated. Do you want to make any edits?"

---

### Step 6: Task Updates

To add a new task:
```
@Task Add XYZ functionality
```

To modify an existing task:
```
@Task 2 Update task to handle edge case ABC
```

---

## 🪠 MEMORY REFRESH PROTOCOL

If user enters:
```
Refresh memory bank <feature-title>
```
Then AI must:
1. Read `/codeAssistant/<feature-title>/progress.md`
2. Re-load completed steps, summaries, and file references
3. Read referenced files (`tasks.md`, `prd.md`, `hld.md`, etc.)
4. Resume from last incomplete step

> "🧠 Memory refreshed for `<feature-title>`. Resuming from Step <n>: `<step-name>`."
If progress.md is missing or malformed:
> "⚠️ Could not locate or parse `/codeAssistant/<feature-title>/progress.md`. Please confirm if you want to start fresh or manually re-initialize the memory."

### ⚠️ Ground Rules for Cursor
- ❌ Never apply changes without asking:
  > `"Can I apply these changes?"`
- ✅ Proceed only on explicit approval.
- 🔁 Modify plan if user requests changes.
