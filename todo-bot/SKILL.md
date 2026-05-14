---
name: todo-bot
description: >
  Manage a persistent TODO.md and implement planned projects.
  Use when user says "/todo-bot", "/todo-bot add", "/todo-bot impl",
  or wants to track or build projects from their TODO list.
---

# todo-bot

Two commands: `/todo-bot add` and `/todo-bot impl`.

---

## `/todo-bot add` — Add a TODO entry

Add a new project entry to the user's TODO.md based on their description.

### TODO.md search strategy

1. Check the current working directory for `TODO.md`
2. If not found, check the user's home directory (`~/TODO.md`)
3. If still not found, create `~/TODO.md` with a `# TODO` heading and add the entry there

### Entry format

Each project is a `##` heading with an optional short description on the next line. Sub-tasks go under `###` headings.

```markdown
# TODO

## project-name — Short description
A one-line summary of what the project does.

### Sub-task A
Details about this sub-task.

### Sub-task B
Details about this sub-task.
```

### Adding a new entry

When the user says `/todo-bot add <description>`:

1. Extract the project name and description from what the user said
2. If the user's description is very terse (a few words), expand it into a clear one-line summary
3. If the user described sub-tasks, add them as `###` entries
4. If the project already exists in TODO.md, append or update sub-tasks instead of duplicating
5. After writing, show the user the updated TODO.md so they can confirm

---

## `/todo-bot impl` — Implement a TODO entry

Pick a project from TODO.md, plan it with the user, scaffold a project directory, and write the plan to `instructions.md`.

### Step 1: Select the project

If the user said `/todo-bot impl <project-name>`, use that name to find the matching `##` entry in TODO.md.

If the user just said `/todo-bot impl` with no name:
1. Read TODO.md and list all `##` entries as a numbered list
2. Ask the user which one to implement
3. Wait for their choice before proceeding

### Step 2: Confirm and scaffold

1. Confirm the project name with the user
2. Convert the project name to kebab-case (lowercase, hyphens instead of spaces)
3. Create a directory with that kebab-case name: `<project-name>/`
4. Do NOT start coding yet — enter planning mode

### Step 3: Planning discussion

Discuss with the user what to implement. Guide the conversation to cover:

- **Goal**: What exactly should the project do?
- **Tech stack**: Language, libraries, frameworks
- **Structure**: Directory layout, key files, entry points
- **Milestones**: What to build first, second, etc.
- **API / data sources**: What external data or services are needed
- **Edge cases**: What could go wrong, error handling

Treat this as a collaborative design conversation. Ask questions, offer suggestions, but let the user make the final calls. Do not start building until the user says the plan is ready.

### Step 4: Write instructions.md

Once the plan is solid, write it into `<project-name>/instructions.md`. Use this structure:

```markdown
# <Project Name>

## Goal
What the project does in one paragraph.

## Tech stack
- Language: ...
- Key libraries: ...
- Tools: ...

## Structure
\```
project/
  main.file
  module/
    ...
\```

## Milestones
1. Scaffold and setup
2. Core feature A
3. Core feature B
4. Polish and edge cases
5. Tests and release

## API / Data sources
- Endpoint A: description
- Endpoint B: description

## Notes
Any constraints, gotchas, or design decisions.
```

### Step 5: Ready to build

After writing `instructions.md`, tell the user the plan is saved and ask if they're ready to start implementing. Do not begin implementation until the user gives the go-ahead.

---

## Additional notes

- Always use the Edit tool to modify TODO.md (never overwrite blindly)
- If a project directory already exists, warn the user and ask whether to proceed, use a different name, or overwrite
- The skill handles one project at a time — do not batch multiple adds or impls
