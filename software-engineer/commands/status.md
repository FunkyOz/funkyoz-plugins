---
description: Display the current status and progress of all development tasks
argument-hint: [detailed]
model: claude-haiku-4-5
---

# Status Command

You are reporting on the current progress of the development tasks.

## Input
- **Argument**: {{1}}
  - (empty) - Show summary status
  - `detailed` - Show detailed status with task descriptions

## Process

### Step 1: Load Task Data
1. Read the `tasks/00-index.md` file
2. Read all individual task files (`tasks/XX-*.md`)
3. Parse the YAML frontmatter from each task to get current status

If no `tasks/` directory exists:
> "No task breakdown found. Run `/software-engineer:plan <feature description>` to create a development plan."

### Step 2: Calculate Progress

Compute the following metrics:
- **Total tasks**: Count of all task files (excluding 00-index.md)
- **Completed**: Tasks with `status: done`
- **In Progress**: Tasks with `status: progress`
- **Todo**: Tasks with `status: todo`
- **Progress percentage**: (Completed / Total) × 100

### Step 3: Display Status

#### Summary View (default)

```
📊 Development Progress
═══════════════════════════════════════════════════════

Progress: [████████████░░░░░░░░] 60% (12/20 tasks)

✅ Completed:    12 tasks
🔄 In Progress:   2 tasks
📋 Todo:          6 tasks

───────────────────────────────────────────────────────

Current Focus:
  → Task 13: [Task Title] (progress)
  → Task 14: [Task Title] (progress)

Next Up:
  → Task 15: [Task Title] (Priority: High)
  → Task 16: [Task Title] (Priority: Medium)

───────────────────────────────────────────────────────

Phase Progress:
  Phase 1: Foundation       ████████████████████ 100% ✓
  Phase 2: Core             ████████████████░░░░  80%
  Phase 3: Advanced         ░░░░░░░░░░░░░░░░░░░░   0%
  Phase 4: Testing          ████████░░░░░░░░░░░░  40%

═══════════════════════════════════════════════════════
```

#### Detailed View (with `detailed` argument)

Include all the above, plus:

```
───────────────────────────────────────────────────────
📋 All Tasks
───────────────────────────────────────────────────────

Phase 1: Foundation
  ✅ 01. Project Setup (done) - Low complexity
  ✅ 02. Config Constants (done) - Low complexity
  ✅ 03. Exception Classes (done) - Low complexity

Phase 2: Core Implementation
  ✅ 04. Buffer Manager (done) - Medium complexity
  🔄 05. Lexer/Tokenizer (progress) - High complexity
       ↳ Dependencies: Tasks 03, 04 ✓
       ↳ Acceptance: 3/5 criteria met
  📋 06. Streaming Parser (todo) - High complexity
       ↳ Dependencies: Tasks 02, 03, 05 (waiting on 05)

[... continue for all tasks ...]

───────────────────────────────────────────────────────
🚧 Blockers & Issues
───────────────────────────────────────────────────────

• Task 05 is blocking tasks 06, 07, 08
• No critical issues reported

───────────────────────────────────────────────────────
```

### Step 4: Recommendations

Based on the current state, provide actionable recommendations:

1. **If tasks are blocked**: Identify which tasks need to be completed first
2. **If no tasks in progress**: Suggest which task to start next
3. **If close to completion**: Highlight remaining work
4. **If stuck on a task**: Suggest breaking it down further or seeking help

## Output Format

Use visual elements to make status clear:
- ✅ for completed tasks
- 🔄 for in-progress tasks
- 📋 for todo tasks
- ⚠️ for blocked tasks
- Progress bars for visual percentage representation

Keep the output clean, scannable, and actionable.
