# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains YAML configuration files for defining AI agent roles and control workflows. The system is designed to orchestrate specialized AI agents for software engineering, security analysis, quality assurance, and documentation tasks.

All agent definitions are stored as flat YAML files in the root directory. There is no build system, no tests, and no application code - this is a purely configuration-based framework.

## Documentation

- **README.md** - Project overview, quick reference, and usage guide
- **AGENTS.md** - Repository guidelines (structure, conventions, and editing rules)
- **CLAUDE.md** - This file (guidance for Claude Code)

## File Structure

The repository contains 9 YAML files organized into two categories:

### Control Agents (Request Definitions)
Files that orchestrate workflows and produce a single TODO output file:

| File | Purpose |
|------|---------|
| `cyber-security-audit-request.yaml` | Unified cybersecurity audit (systems + codebase + agent/prompt workflows) |
| `code-review-request.yaml` | Comprehensive code review automation |
| `post-implementation-self-audit-request.yaml` | Post-implementation self-audit |
| `quality-engineering-request.yaml` | Quality engineering strategy design |
| `root-cause-analysis-request.yaml` | Root cause analysis |
| `seo-optimization-request.yaml` | SEO optimization analysis |

### Functional Agents (Role Definitions)
Files that perform specific specialized tasks:

| File | Purpose |
|------|---------|
| `prd-writer.yaml` | Product Requirements Document creation |
| `docs-maintainer.yaml` | Documentation creation and maintenance |
| `test-writer.yaml` | Test code generation |

See `README.md` for the quick reference. Each `*.yaml` file is self-contained and includes its scope, output instructions, and RULE section.

## YAML Structure Convention

All agent files follow a consistent structure:

```yaml
---
name: [agent-identifier]
description: [one-line description]
---

# [Human-Readable Title]

[Detailed role description]

## Category
### Subcategory
- **Item**: Description

## Output (TODO Only)
...

## Output Format (Task-Based)
...

## Quality Assurance Task Checklist
...

## Additional Focus Areas
...

---
**RULE:** When using this prompt, you must create a file named `TODO_<agent-name>.md`. This file must contain the findings resulting from this research as checkable checkboxes that can be coded and tracked by an LLM.
```

When modifying agent files:
- Maintain the frontmatter (`---` delimited YAML header)
- Keep the description field concise
- Follow the hierarchical heading structure (## Main Category, ### Subcategory)
- Use bullet points with **bold** prefixes for checklist items
- End each file with the output rule

## Naming Conventions

**Primary rule:** YAML filename must match the frontmatter `name` plus `.yaml`.

| Pattern | Meaning | Example |
|---------|---------|---------|
| `*-request.yaml` | Control agent / workflow request | `code-review-request.yaml` |
| `*-writer.yaml` | Content creation | `prd-writer.yaml`, `test-writer.yaml` |
| `*-maintainer.yaml` | Maintenance | `docs-maintainer.yaml` |

When adding new agent files, follow existing patterns and use descriptive, hyphenated names.

## Key Architectural Concepts

### Control vs Functional Agents
- **Control agents** orchestrate workflows and produce a single TODO output file
- **Functional agents** perform specific tasks like writing documentation or tests

### Content Structure
Most control agent files include:
1. **Requirements sections** - Categorized by domain (Security, Performance, Correctness, etc.)
2. **Output (TODO Only)** - Single output file (`TODO_<agent-name>.md`) for all results
3. **Output Format (Task-Based)** - Template for how findings should be structured inside the TODO
4. **Quality Assurance Task Checklist** - Evidence standards and validation criteria
5. **Additional Focus Areas** - Modern practices and compliance considerations

## Recent Refactoring

The project was recently simplified from a nested directory structure (`agents/` and `control/` subdirectories with 100+ files) to a flat 9-file structure. When working with this codebase, prefer simplicity and flat organization over deep hierarchies.

## Quick Start

1. **Choose an agent** - Review `README.md` for agent purposes
2. **Read the file** - Open the corresponding YAML file to understand its requirements
3. **Execute** - The agent will generate output following its RULE section
4. **Results** - Find output in `TODO_<agent-name>.md`
