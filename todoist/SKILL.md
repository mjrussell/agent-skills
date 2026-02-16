---
name: todoist
description: Manage tasks, projects, sections, labels, and collaborators in Todoist. Use when user asks about tasks, to-dos, reminders, deadlines, assignment, or productivity workflows.
homepage: https://todoist.com
metadata:
  clawdbot:
    emoji: "✅"
    requires:
      bins: ["todoist"]
      env: ["TODOIST_API_TOKEN"]
---

# Todoist CLI

CLI for Todoist task management, built on the official TypeScript SDK.

## Installation

```bash
# Requires todoist-ts-cli >= 0.3.0 (deadlines, assignees, sections/collaborators)
npm install -g todoist-ts-cli@^0.3.0
```

## Setup

1. Get API token from https://todoist.com/app/settings/integrations/developer
2. Either:
   ```bash
   todoist auth <your-token>
   # or
   export TODOIST_API_TOKEN="your-token"
   ```

## Commands

### Tasks

```bash
todoist                    # Show today's tasks (default)
todoist today              # Same as above
todoist tasks              # List tasks (today + overdue)
todoist tasks --all        # All tasks
todoist tasks -p "Work"    # Tasks in project
todoist tasks -f "p1"      # Filter query (priority 1)
todoist tasks --json
```

### Add Tasks

```bash
todoist add "Buy groceries"
todoist add "Meeting" --due "tomorrow 10am"
todoist add "Review PR" --due "today" --deadline "2026-03-05" --priority 1 --project "Work"
todoist add "Prep slides" --project "Work" --order 3  # add at a specific position (1-based)
todoist add "Triage inbox" --project "Work" --order top  # add to top (alternative to --top)
todoist add "Call mom" -d "sunday" -l "family"  # with label
todoist add "Review PR" -p "Work" -a "123456789"  # assign to collaborator user ID
```

### Manage Tasks

```bash
todoist view <id>          # View task details
todoist done <id>          # Complete task
todoist reopen <id>        # Reopen completed task
todoist update <id> --due "next week"
todoist update <id> --deadline "2026-03-05"
todoist update <id> --deadline none  # clear deadline
todoist update <id> --labels "next,waiting"  # replace labels
todoist update <id> --add-label next --remove-label waiting
todoist update <id> -a "123456789"  # assign
todoist update <id> -a "null"       # unassign
todoist move <id> -p "Personal"                 # move to project
todoist move <id> -p "Work" -s "Section A"      # move to section
todoist move <id> --parent <task-id>            # make sub-task
todoist delete <id>
```

### Search

```bash
todoist search "meeting"
```

### Projects, Sections, Labels

```bash
todoist projects           # List projects
todoist project-add "New Project"
todoist project-add "Roadmap" --color blue
todoist sections
todoist sections -p "Work"
todoist section-add "Q1" -p "Work"
todoist labels             # List labels
todoist label-add "urgent"
todoist label-add "focus" --color red
```

### Collaborators

```bash
todoist collaborators <project-id>  # list collaborator IDs for assignment
```

### Comments

```bash
todoist comments <task-id>
todoist comment <task-id> "Note about this task"
```

## Usage Examples

**User: "What do I have to do today?"**
```bash
todoist today
```

**User: "Add 'buy milk' to my tasks"**
```bash
todoist add "Buy milk" --due "today"
```

**User: "Remind me to call the dentist tomorrow"**
```bash
todoist add "Call the dentist" --due "tomorrow"
```

**User: "Mark the grocery task as done"**
```bash
todoist search "grocery"   # Find task ID
todoist done <id>
```

**User: "What's on my work project?"**
```bash
todoist tasks -p "Work"
```

**User: "Show my high priority tasks"**
```bash
todoist tasks -f "p1"
```

**User: "Assign this task to Alex"**
```bash
todoist collaborators <project-id>   # find Alex's collaborator ID
todoist update <id> -a "<collaborator-id>"
```

**User: "Add a hard deadline for this task"**
```bash
todoist update <id> --deadline "2026-03-05"
```

**User: "Move this into the Q1 section"**
```bash
todoist move <id> -p "Work" -s "Q1"
```

## Filter Syntax

Todoist supports powerful filter queries:
- `p1`, `p2`, `p3`, `p4` - Priority levels
- `today`, `tomorrow`, `overdue`
- `@label` - Tasks with label
- `#project` - Tasks in project
- `search: keyword` - Search

## Notes

- Task IDs are shown in task listings
- Due dates support natural language ("tomorrow", "next monday", "jan 15")
- Deadlines use explicit dates (`YYYY-MM-DD`) and can be cleared with `--deadline none`
- Priority 1 is highest, 4 is lowest
- Use `--order <n>` (1-based) or `--order top` to insert a task at a specific position within a project/section
- Assignment needs a collaborator user ID from `todoist collaborators <project-id>`
- Use `--json` for script-friendly output on supported commands
