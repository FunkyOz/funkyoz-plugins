# Software Engineer Plugin for Claude Code

A comprehensive plugin that transforms feature requests into structured development tasks, manages the development workflow, and follows software engineering best practices.

## Features

- **Task Planning**: Break down feature requests into well-structured, actionable tasks
- **Task Development**: Execute tasks with automatic status tracking
- **Progress Monitoring**: View development progress with detailed status reports
- **Comprehensive Git Integration**:
  - Smart branch management aligned with task workflow
  - AI-powered commit message generation from code analysis
  - Automatic git diff analysis for descriptive commits
  - Professional commit standards following conventional commits
- **Project Analysis**: Understand existing project patterns and conventions

## Installation

```bash
/plugin marketplace add funkyoz@claude-code-plugin

/plugin install ./software-engineer
```

## Commands

### `/software-engineer:plan <feature description>`

Transform a feature request into a structured task breakdown.

**Example:**
```
/software-engineer:plan Create a user authentication system with login, registration, and password reset
```

This will:
1. Analyze your project's technology stack and patterns
2. Create a `tasks/` directory with:
   - `00-index.md` - Main implementation plan
   - `01-task-name.md`, `02-task-name.md`, etc. - Individual tasks
3. Ask for your approval before proceeding

### `/software-engineer:develop [task-number|next|all]`

Start or continue development by executing tasks.

**Examples:**
```
/software-engineer:develop           # Work on next available task
/software-engineer:develop 05        # Work on task 05 specifically
/software-engineer:develop all       # Work through all tasks (with confirmation)
```

This will:
1. Set task status to `progress`
2. Implement the task following project conventions
3. Verify acceptance criteria
4. Set task status to `done` when complete

### `/software-engineer:status [detailed]`

Display current progress of all development tasks.

**Examples:**
```
/software-engineer:status            # Show summary status
/software-engineer:status detailed   # Show detailed status with descriptions
```

### `/software-engineer:git <action> [task-number]`

Manage git workflow aligned with tasks, featuring comprehensive commit message generation.

**Actions:**
```
/software-engineer:git branch        # Create branch for current task
/software-engineer:git commit        # Generate and commit with comprehensive message
/software-engineer:git finish        # Complete task branch (merge)
/software-engineer:git status        # Show git status relative to tasks
/software-engineer:git sync          # Sync task branch with main
```

**Comprehensive Commit Feature:**

When you run `/software-engineer:git commit`, the plugin will:
1. Analyze your git diff and changed files
2. Auto-generate a comprehensive commit message with:
   - Descriptive title (max 50 characters)
   - Detailed description (3-4 lines) based on actual code changes
   - Proper conventional commit type (feat, fix, refactor, etc.)
3. Show you the generated message for approval
4. Commit after your confirmation

**Example Generated Commit:**
```
[Task 05] feat: Add token validation to lexer

Implemented token validation logic in the lexer component to ensure
proper syntax checking. Added TokenValidator class with validation rules
for identifiers, keywords, and operators. Updated Lexer.php to integrate
validation during tokenization process.
```

**What's NOT included:**
- ❌ Acceptance criteria lists
- ❌ Author information in message body
- ❌ Generic descriptions like "Updated code"

## Task File Format

Each task file follows this structure:

```markdown
---
title: Task Title
status: todo
priority: High
description: Brief description of the task
---

## Objectives
- Clear objective 1
- Clear objective 2

## Deliverables
1. Specific deliverable
2. Another deliverable

## Technical Details
[Implementation guidance]

## Dependencies
- Task 01 - Previous Task

## Estimated Complexity
**Medium** - Justification for estimate

## Acceptance Criteria
- [ ] Testable criterion 1
- [ ] Testable criterion 2
```

## Workflow

1. **Plan**: Run `/software-engineer:plan` with your feature description
2. **Review**: Check the generated task breakdown in `tasks/`
3. **Approve**: Confirm the plan is acceptable
4. **Develop**: Run `/software-engineer:develop` to start implementation
5. **Track**: Use `/software-engineer:status` to monitor progress
6. **Commit**: Use `/software-engineer:git commit` for version control with comprehensive messages

## Git Integration Best Practices

The plugin follows professional git workflow practices:

### Branch Strategy
- One branch per task: `task/XX-task-slug`
- Keep `main` as the integration branch
- Merge completed task branches promptly
- Delete merged branches to keep repo clean

### Commit Message Standards
All commits follow this structure:
```
[Task XX] <type>: <concise description>

<detailed description of changes (3-4 lines max)>
```

**Commit Types:**
- `feat` - New features
- `fix` - Bug fixes
- `refactor` - Code restructuring without functionality changes
- `test` - Test additions or changes
- `docs` - Documentation updates
- `chore` - Maintenance tasks
- `perf` - Performance improvements
- `style` - Code style/formatting changes

### Commit Generation Process
1. **Analysis**: Automatically reviews `git diff` and changed files
2. **Generation**: Creates descriptive commit message based on actual changes
3. **Approval**: Shows you the message and asks for confirmation
4. **Commit**: Proceeds only after your approval

### What Makes Commits "Comprehensive"
- **Descriptive titles**: Clear, concise (max 50 chars), imperative mood
- **Detailed descriptions**: 3-4 lines explaining WHAT changed and WHY
- **Code-aware**: Generated from actual file changes, not generic templates
- **Clean**: No acceptance criteria, author info, or progress percentages
- **Consistent**: Follows conventional commits specification

## Project Analysis

The plugin automatically analyzes your project to:
- Detect technology stack and frameworks
- Identify coding patterns and conventions
- Understand project structure
- Match existing code style

For new projects, it recommends best practices for your chosen stack.

## File Structure

```
software-engineer/
├── .claude-plugin/
│   └── plugin.json           # Plugin manifest
├── commands/
│   ├── plan.md               # Task planning command
│   ├── develop.md            # Task development command
│   ├── status.md             # Progress status command
│   └── git.md                # Git integration command
├── agents/
│   ├── task-planner.md       # Planning specialist agent
│   └── developer.md          # Development specialist agent
├── skills/
│   └── project-analyzer/
│       ├── SKILL.md          # Project analysis skill
│       └── references/
│           └── patterns.md   # Common patterns reference
├── assets/
│   ├── task-template.md      # Template for task files
│   └── index-template.md     # Template for index file
└── README.md                 # This file
```
