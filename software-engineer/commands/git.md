---
description: Manage git branches and commits aligned with task workflow
argument-hint: <action> [task-number]
---

# Git Integration Command

You are managing git workflow in alignment with the task-based development process.

## Input
- **Action**: {{1}}
  - `branch` - Create a branch for a task
  - `commit` - Commit changes for current task
  - `finish` - Complete task branch (commit, optionally merge)
  - `status` - Show git status relative to tasks
  - `sync` - Sync task branches with main/develop

- **Task Number**: {{2}} (optional, defaults to current in-progress task)

## Prerequisites

Verify git is initialized:
```bash
git rev-parse --is-inside-work-tree
```

If not a git repository, ask if user wants to initialize one.

## Actions

### `branch` - Create Task Branch

Create a new branch for working on a specific task.

**Process:**
1. Identify the task (from argument or first `progress` task)
2. Read task file to get title
3. Generate branch name: `task/XX-task-slug`
   - Example: `task/05-lexer-tokenizer`
4. Check if branch already exists
5. Create and checkout the branch:
   ```bash
   git checkout -b task/XX-task-slug
   ```
6. Confirm to user:
   > "Created and switched to branch `task/05-lexer-tokenizer`
   > Ready to work on Task 05: Lexer/Tokenizer"

**Branch Naming Convention:**
- Prefix: `task/`
- Task number: Zero-padded (01, 02, etc.)
- Slug: Lowercase, hyphenated task title
- Example: `task/07-stream-reader-base`

### `commit` - Commit Task Progress

Create a commit for the current task work.

**Process:**
1. Check for uncommitted changes
2. Identify current task (from branch name or in-progress task)
3. Stage all changes (or ask user what to stage)
4. Generate commit message:
   ```
   [Task XX] Brief description of changes
   
   - Detailed change 1
   - Detailed change 2
   
   Progress: X/Y acceptance criteria met
   ```
5. Create the commit
6. Confirm to user

**Commit Message Format:**
```
[Task XX] <type>: <short description>

<detailed description of changes>

Acceptance Criteria Progress:
- [x] Criterion 1
- [x] Criterion 2  
- [ ] Criterion 3 (pending)
```

Types: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`

### `finish` - Complete Task Branch

Finalize work on a task branch.

**Process:**
1. Verify all acceptance criteria are met
2. Ensure all changes are committed
3. Update task status to `done` if not already
4. Ask user about merge strategy:
   - Merge to develop/main
   - Create pull request (provide PR description)
   - Keep branch for manual merge
5. If merging:
   ```bash
   git checkout main  # or develop
   git merge --no-ff task/XX-task-slug
   ```
6. Optionally delete the task branch
7. Summarize:
   > "✅ Task 05 branch completed and merged to main
   > Branch `task/05-lexer-tokenizer` has been deleted
   > 
   > Commits merged: 5
   > Files changed: 12"

### `status` - Git Status for Tasks

Show git status in context of task workflow.

**Output:**
```
📊 Git Status - Task Workflow
═══════════════════════════════════════════════════════

Current Branch: task/05-lexer-tokenizer
Related Task: 05 - Lexer/Tokenizer (progress)

───────────────────────────────────────────────────────

Working Directory:
  Modified:  src/Internal/Lexer.php
  Modified:  tests/Unit/LexerTest.php
  Untracked: src/Internal/Token.php

Staged:
  (none)

───────────────────────────────────────────────────────

Task Branches:
  ✅ task/01-project-setup (merged)
  ✅ task/02-config-constants (merged)
  ✅ task/03-exception-classes (merged)
  ✅ task/04-buffer-manager (merged)
  🔄 task/05-lexer-tokenizer (current) - 3 commits ahead
  📋 task/06-streaming-parser (not created)

───────────────────────────────────────────────────────

Suggestions:
  → Stage and commit your current changes
  → Run: /software-engineer:git commit
```

### `sync` - Sync with Main Branch

Keep task branches up to date with main/develop.

**Process:**
1. Fetch latest from remote
2. Identify current task branch
3. Rebase or merge from main/develop:
   ```bash
   git fetch origin
   git rebase origin/main  # or merge
   ```
4. Handle conflicts if any (notify user)
5. Push updates if remote tracking exists

## Git Best Practices

### Branch Strategy
- Keep `main` or `develop` as the integration branch
- One branch per task
- Merge completed task branches promptly
- Delete merged branches to keep repo clean

### Commit Practices
- Commit frequently within a task
- Write meaningful commit messages
- Reference task number in every commit
- Keep commits focused and atomic

### Conflict Resolution
- When conflicts occur, explain the conflict clearly
- Show both versions of conflicting code
- Ask user for resolution preference
- Never auto-resolve without user confirmation

## Error Handling

If git operations fail:
1. Show the exact error message
2. Explain what went wrong
3. Suggest remediation steps
4. Offer to help fix the issue

Common issues:
- Uncommitted changes blocking checkout
- Merge conflicts
- Branch already exists
- Remote push rejected
