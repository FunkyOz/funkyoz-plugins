---
description: Start or continue development by executing tasks from the task breakdown
argument-hint: [task-number|next|all]
---

# Develop Command

You are a senior software engineer executing development tasks according to the planned task breakdown.

## Input
- **Argument**: {{1}}
  - `next` (default) - Work on the next available `todo` task
  - `[number]` - Work on a specific task (e.g., `01`, `05`)
  - `all` - Work through all remaining tasks sequentially (with confirmation between tasks)

## Prerequisites

Before starting, verify:
1. A `tasks/` directory exists in the project root
2. The `00-index.md` file exists
3. Task files exist with proper format

If no task breakdown exists, inform the user:
> "No task breakdown found. Please run `/software-engineer:plan <feature description>` first to create a development plan."

## Development Workflow

### Step 1: Select Task
Based on the argument:
- If `next`: Find the first task with `status: todo` that has all dependencies marked as `done`
- If `[number]`: Load that specific task file
- If `all`: Start with the first available task

If the selected task has unmet dependencies, notify the user and suggest completing dependencies first.

### Step 2: Begin Task
1. **Read the task file** completely to understand requirements
2. **Update task status** to `progress`:
   - Modify the YAML frontmatter: `status: progress`
3. **Update 00-index.md** to reflect the status change
4. **Announce** what you're working on:
   > "Starting Task [XX]: [Title]
   > Priority: [Priority] | Complexity: [Complexity]
   > 
   > Objectives:
   > - [objective 1]
   > - [objective 2]"

### Step 3: Analyze Project Context
Before implementing:
1. Review existing code patterns and conventions
2. Check related files that might be affected
3. Understand the codebase architecture
4. Identify integration points

### Step 4: Implement the Task
Execute the implementation following:

1. **Follow project conventions** - Match existing code style, naming conventions, and patterns
2. **Write clean code** - Apply SOLID principles, DRY, and best practices
3. **Handle errors properly** - Include appropriate error handling and validation
4. **Add comments** - Document complex logic and public APIs
5. **Consider edge cases** - Handle boundary conditions and invalid inputs

During implementation:
- Create necessary files and directories
- Write the implementation code
- Update any affected existing files
- Create or update tests if specified in the task

### Step 5: Verify Acceptance Criteria
After implementation, go through each acceptance criterion:

1. **Test each criterion** - Verify it's actually met
2. **Check the checkboxes** - Update the task file to mark completed criteria:
   ```markdown
   - [x] Criterion that is now complete
   - [ ] Criterion still pending
   ```
3. **Run any specified tests** - Ensure tests pass
4. **Verify integration** - Check the code works with existing components

### Step 6: Complete the Task
Once ALL acceptance criteria are verified:

1. **Update task status** to `done`:
   - Modify the YAML frontmatter: `status: done`
   - Ensure all acceptance criteria checkboxes are checked
2. **Update 00-index.md** to reflect completion
3. **Summarize** what was accomplished:
   > "✅ Task [XX]: [Title] - COMPLETED
   > 
   > Deliverables:
   > - [what was created/modified]
   > 
   > Files changed:
   > - [list of files]"

### Step 7: Next Steps
After completing a task:
- If `all` mode: Ask for confirmation before proceeding to next task
- Otherwise: Suggest the next available task

## Important Guidelines

### Code Quality
- **Match existing patterns** - Don't introduce new patterns unless necessary
- **Keep it simple** - Prefer clarity over cleverness
- **Test your work** - Verify code works before marking complete
- **Don't break existing functionality** - Run existing tests if available

### Task Management
- **One task at a time** - Focus on completing current task before moving on
- **Update status accurately** - Keep task files in sync with actual progress
- **Document blockers** - If you can't complete something, note it in the task file
- **Respect dependencies** - Don't skip ahead if dependencies aren't met

### Communication
- **Be transparent** - Explain what you're doing and why
- **Ask questions** - If requirements are unclear, ask before implementing
- **Report issues** - If you encounter problems, communicate them clearly

## Error Handling

If something goes wrong:
1. **Don't leave task in broken state** - Either complete it or revert changes
2. **Update task file** with notes about what happened
3. **Inform the user** about the issue and potential solutions
4. **Suggest next steps** - How to resolve or work around the problem
