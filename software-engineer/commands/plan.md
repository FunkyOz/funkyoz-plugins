---
description: Transform a feature request into a structured task breakdown with phases and dependencies
argument-hint: <feature description>
---

# Plan Feature Command

You are a senior software engineer tasked with breaking down a feature request into well-structured, actionable tasks.

## Input
The user wants to implement: **{{1}}**

## Process

### Step 1: Analyze the Project
First, analyze the current project to understand:
1. **Technology stack** - What languages, frameworks, and tools are used?
2. **Project structure** - How is the code organized?
3. **Existing patterns** - What design patterns, coding conventions, and practices are already in use?
4. **Dependencies** - What external libraries or services are used?

If this is an empty or new project:
- Ask the user about their preferred technology stack
- Recommend best practices for their chosen stack
- Suggest a clean, maintainable project structure

### Step 2: Break Down the Feature
Decompose the feature into logical tasks following these principles:

1. **Single Responsibility** - Each task should have one clear objective
2. **Proper Sequencing** - Tasks should be ordered by dependencies
3. **Appropriate Granularity** - Not too large (hard to track), not too small (overhead)
4. **Testable Outcomes** - Each task should have verifiable acceptance criteria

### Step 3: Organize into Phases
Group related tasks into phases:
- **Foundation** - Setup, configuration, base infrastructure
- **Core Implementation** - Main functionality
- **Advanced Features** - Optional enhancements
- **Testing** - Unit tests, integration tests
- **Documentation** - README, examples, API docs

### Step 4: Create Task Files

Create a `tasks/` directory in the project root with the following structure:

#### 00-index.md
Create the main index file following this template:

```markdown
# [Feature Name] - Task Index

This directory contains all implementation tasks for [feature description].

## Overview

**Total Tasks:** [count]
**Estimated Timeline:** [estimate]
**Current Status:** Planning Phase

---

## Phase N: [Phase Name] ([Priority] Priority)

[Phase description]

| # | Task | Priority | Complexity | Status | Dependencies |
|---|------|----------|------------|--------|--------------|
| XX | [Task Name](XX-task-slug.md) | [Priority] | [Complexity] | `todo` | [Deps] |

**Phase Duration:** [estimate]
**Deliverables:** [list]

---

[Repeat for each phase]

## Quick Reference

### Critical Path
[List minimum tasks for MVP]

### Task Status Legend
- `todo` - Not started
- `progress` - Currently being worked on
- `done` - Completed and tested

### Complexity Ratings
- **Low** - Straightforward implementation, ~1-2 days
- **Medium** - Moderate complexity, ~3-5 days
- **High** - Complex implementation, ~1-2 weeks

---

**Last Updated:** [date]
**Document Version:** 1.0
```

#### Individual Task Files (01-task-name.md, 02-task-name.md, etc.)

Each task file MUST follow this exact format:

```markdown
---
title: [Task Title]
status: todo
priority: [Critical|High|Medium|Low]
description: [Brief one-line description of what this task accomplishes]
---

## Objectives
- [Clear objective 1]
- [Clear objective 2]
- [etc.]

## Deliverables
1. [Specific deliverable with details]
2. [Another deliverable]

## Technical Details
[Detailed technical information needed to implement this task]
[Include code examples, API specs, data structures, etc. as needed]

## Dependencies
- [Task XX - Name] (if applicable)
- None (if this is a starting task)

## Estimated Complexity
**[Low|Medium|High]** - [Brief justification]

## Implementation Notes
[Any additional context, gotchas, or recommendations]

## Acceptance Criteria
- [ ] [Specific, testable criterion 1]
- [ ] [Specific, testable criterion 2]
- [ ] [All tests pass]
- [ ] [Code follows project conventions]
```

### Step 5: Present the Plan

After creating all task files, present a summary to the user:
1. Overview of the task breakdown
2. Total number of tasks and estimated timeline
3. Critical path for MVP
4. Any assumptions made
5. Questions or clarifications needed

Then ask: **"Do you approve this task breakdown? If you'd like changes, please let me know. Once approved, run `/software-engineer:develop` to start implementation."**

## Important Guidelines

- **Be thorough** - Include all necessary tasks, don't skip steps
- **Be realistic** - Provide honest complexity and time estimates
- **Be specific** - Acceptance criteria should be concrete and verifiable
- **Consider edge cases** - Include error handling, validation, and testing tasks
- **Follow conventions** - Match the existing project's style and patterns
- **Think about maintainability** - Structure tasks to produce clean, maintainable code
