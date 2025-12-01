---
name: project-analyzer
description: Analyzes project structure, technology stack, patterns, and conventions. Use when starting development tasks, reviewing code, or understanding an existing codebase.
---

# Project Analyzer Skill

This skill enables comprehensive analysis of software projects to understand their structure, patterns, and conventions before making changes.

## When to Use This Skill

- Starting work on a new task in an existing project
- Creating a task breakdown for a feature
- Understanding project conventions before coding
- Reviewing code for consistency
- Setting up a new project with best practices

## Analysis Framework

### 1. Project Structure Analysis

**Directory Layout**
- Identify the project type (monorepo, single app, library, etc.)
- Map the directory structure
- Understand the organization pattern (by feature, by layer, etc.)

**Key Directories to Look For**
```
src/              # Source code
lib/              # Library code
app/              # Application code
tests/            # Test files
docs/             # Documentation
config/           # Configuration
scripts/          # Build/utility scripts
public/           # Static assets
dist/             # Build output
```

### 2. Technology Stack Detection

**Package Managers & Dependencies**
| File | Technology |
|------|------------|
| `package.json` | Node.js/JavaScript |
| `composer.json` | PHP |
| `requirements.txt`, `pyproject.toml` | Python |
| `Gemfile` | Ruby |
| `Cargo.toml` | Rust |
| `go.mod` | Go |
| `pom.xml`, `build.gradle` | Java |

**Frameworks**
- Check dependencies for framework indicators
- Look for framework-specific config files
- Identify framework version

**Build Tools**
- Webpack, Vite, esbuild (JavaScript)
- Make, CMake (C/C++)
- Maven, Gradle (Java)
- Cargo (Rust)

### 3. Code Patterns & Conventions

**Coding Style**
- Check for `.editorconfig`
- Look for linter configs (`.eslintrc`, `.prettierrc`, `phpcs.xml`)
- Analyze existing code for patterns:
  - Naming conventions (camelCase, snake_case, PascalCase)
  - Indentation style
  - Quote style
  - Semicolon usage

**Architecture Patterns**
- MVC (Model-View-Controller)
- Clean Architecture / Hexagonal
- Repository Pattern
- Service Layer
- Domain-Driven Design

**Design Patterns in Use**
- Factory
- Singleton
- Observer
- Strategy
- Decorator
- Dependency Injection

### 4. Testing Strategy

**Test Framework Detection**
| Framework | Language |
|-----------|----------|
| Jest, Mocha, Vitest | JavaScript |
| PHPUnit, Pest | PHP |
| pytest, unittest | Python |
| RSpec, Minitest | Ruby |
| JUnit | Java |

**Test Organization**
- Unit tests location
- Integration tests location
- Test naming conventions
- Mocking patterns

### 5. Documentation Standards

**README Structure**
- Project description
- Installation instructions
- Usage examples
- Contributing guidelines

**Code Documentation**
- JSDoc, PHPDoc, docstrings
- Inline comments style
- API documentation

## Analysis Output Template

When analyzing a project, report findings in this format:

```markdown
## Project Analysis Report

### Overview
- **Type**: [Web App / API / Library / CLI / etc.]
- **Primary Language**: [Language + version]
- **Framework**: [Framework + version]

### Structure
[Description of directory organization]

### Dependencies
- **Runtime**: [key dependencies]
- **Development**: [key dev dependencies]

### Patterns & Conventions

#### Coding Style
- Naming: [convention]
- Formatting: [tool/standard]
- Linting: [tool/rules]

#### Architecture
- Pattern: [architecture pattern]
- Key abstractions: [list]

#### Testing
- Framework: [test framework]
- Coverage: [if measurable]
- Organization: [how tests are organized]

### Recommendations
[Recommendations for maintaining consistency]
```

## Empty Project Guidance

When project is new/empty, recommend:

### JavaScript/TypeScript
- TypeScript for type safety
- ESLint + Prettier for formatting
- Jest or Vitest for testing
- Clear src/ structure

### Python
- Type hints throughout
- Black + isort for formatting
- pytest for testing
- src layout or flat layout

### PHP
- PSR-4 autoloading
- PHP-CS-Fixer or PHP_CodeSniffer
- PHPUnit for testing
- Proper namespace organization

### General Best Practices
- README with setup instructions
- .editorconfig for consistency
- .gitignore appropriate for stack
- CI/CD configuration
- Environment variable handling

## Integration with Development

After analysis, use findings to:
1. Match existing code style in new code
2. Follow established patterns
3. Use same testing approaches
4. Maintain documentation standards
5. Respect architectural boundaries

See [references/patterns.md](references/patterns.md) for detailed pattern examples.
