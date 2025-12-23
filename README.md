# diffray Custom Rules Examples

[![diffray - AI Code Review](https://diffray.ai/og-image.jpg)](https://diffray.ai?utm_source=github-rules)

A collection of project-specific rules and configuration examples for [diffray](https://diffray.ai?utm_source=github-rules) — AI-powered code review platform.

## What is diffray?

**[diffray](https://diffray.ai?utm_source=github-rules)** is an AI-powered code review platform that automatically reviews your GitHub Pull Requests using Claude AI. It catches bugs, security vulnerabilities, performance issues, and code quality problems before they reach production.

### Key Features

- **Intelligent Code Analysis** — Goes beyond linting to understand context and intent
- **Security-First** — Detects OWASP Top 10 vulnerabilities, secrets exposure, injection attacks
- **Customizable Rules** — Define your own rules that match your team's standards
- **Multi-Language Support** — TypeScript, JavaScript, Python, Go, Java, and more
- **PR-Level Analysis** — Reviews commit messages, PR descriptions, and change scope

## Repository Structure

```
.
├── config.example.yaml          # Full configuration example
└── rules/
    ├── architecture-docs/       # Architecture documentation rules
    │   ├── adr-reference.yaml
    │   └── breaking-changes.yaml
    ├── git-commits/             # Commit message rules
    ├── pr-quality/              # PR-level quality checks
    │   ├── description-explain-why.yaml
    │   ├── single-responsibility.yaml
    │   └── ticket-reference.yaml
    ├── testing-coverage/        # Test coverage rules
    ├── typescript-avoid-any.yaml
    ├── typescript-style-preferences.yaml
    ├── code-complexity-thresholds.yaml
    ├── aws-cdk-best-practices.yaml
    ├── go-uber-style.yaml
    └── ... and more
```

## Quick Start

### 1. Install diffray

Visit [diffray.ai](https://diffray.ai?utm_source=github-rules) and install the GitHub App to your repository.

### 2. Add Configuration

Create `.diffray/config.yaml` in your repository:

```yaml
version: 1

filters:
  useDefaults: true
  exclude:
    - 'vendor/**'
    - '**/*.generated.ts'

review:
  model: sonnet
  minConfidence: 60
  minImportance: 3

rules:
  tags:
    exclude:
      - documentation
```

### 3. Add Custom Rules

Create `.diffray/rules/` directory and add your YAML rules:

```yaml
rules:
  - id: ts_avoid_the_any_type
    agent: bugs
    title: Avoid the 'any' type
    description: |
      Detect the use of the 'any' type in TypeScript.
      Using 'any' disables type checking.
    importance: 8
    match:
      file_glob:
        - '**/*.ts'
        - '**/*.tsx'
    examples:
      bad: 'let foo: any = "bar";'
      good: 'let foo: string = "bar";'
    tags:
      - typescript
      - type-safety
```

## Rule Structure

Each rule consists of:

| Field | Description |
|-------|-------------|
| `id` | Unique identifier for the rule |
| `agent` | AI agent that processes this rule (`security`, `bugs`, `performance`, `architecture`, `quality`, `general`) |
| `title` | Short human-readable title |
| `description` | Detailed explanation for the AI reviewer |
| `importance` | Priority level (1-10) |
| `match.file_glob` | File patterns this rule applies to |
| `checklist` | Step-by-step verification instructions |
| `examples` | Good and bad code examples |
| `tags` | Categories for filtering |

## Example Rules

### PR Quality: Explain Why

```yaml
rules:
  - id: pr_description_explain_why
    agent: general
    title: PR description should explain motivation
    always_run: true
    importance: 7
    checklist:
      - Check if PR description explains the business reason
      - Verify changes have context about the problem being solved
      - Look for explanations of "why this approach" vs alternatives
```

### Security: AWS CDK Best Practices

```yaml
rules:
  - id: cdk_no_hardcoded_secrets
    agent: security
    title: No hardcoded secrets in CDK
    importance: 10
    match:
      file_glob:
        - '**/cdk/**/*.ts'
        - '**/infrastructure/**/*.ts'
```

### Architecture: Layered Dependencies

```yaml
rules:
  - id: arch_layered_deps
    agent: architecture
    title: Enforce layered architecture boundaries
    description: |
      Controllers should not import from repositories directly.
      Services should be the intermediary layer.
```

## Configuration Options

### File Filtering

```yaml
filters:
  useDefaults: true          # Use default exclusions
  exclude:
    - 'legacy/**'
    - '**/*.test.ts'
  include:
    - 'package.json'         # Re-include despite defaults
```

### Review Settings

```yaml
review:
  maxFiles: 150              # Max files per PR
  model: sonnet              # opus | sonnet | haiku
  minConfidence: 60          # 0-100
  minImportance: 3           # 0-10
```

### Agent Filtering

```yaml
rules:
  agents:
    only:                    # Only run these agents
      - security
      - bugs
    exclude:                 # Or exclude specific agents
      - documentation
```

### Tag Filtering

```yaml
rules:
  tags:
    only:
      - typescript
      - react
      - security
```

## Available Tags

**Languages:** `typescript`, `javascript`, `python`, `go`, `java`, `rust`

**Frameworks:** `react`, `nextjs`, `vue`, `angular`, `express`, `nestjs`

**Categories:** `security`, `performance`, `bugs`, `error-handling`, `maintainability`, `readability`, `type-safety`, `architecture`, `testing`, `documentation`

**Compliance:** `compliance-gdpr`, `compliance-soc2`, `compliance-pci-dss`, `privacy`

## Why diffray?

| Feature | Traditional Linters | diffray |
|---------|-------------------|---------|
| Syntax errors | Yes | Yes |
| Security vulnerabilities | Limited | Comprehensive |
| Business logic bugs | No | Yes |
| Performance issues | Limited | Yes |
| Architecture violations | No | Yes |
| Context-aware suggestions | No | Yes |
| Custom rules (natural language) | No | Yes |

## Get Started

1. Visit [diffray.ai](https://diffray.ai?utm_source=github-rules)
2. Install the GitHub App
3. Get AI-powered reviews on your next PR

---

**[diffray](https://diffray.ai?utm_source=github-rules)** — Ship better code, faster.
