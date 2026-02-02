# Repository Guidelines

## Project Structure & Module Organization
This repository is configuration-only: a flat set of YAML agent definitions in the root directory. Key files:
- `*.yaml`: agent definition files (control and functional agents).
- `README.md`: project overview, agent catalog, and naming conventions.
- `CLAUDE.md`: tool-specific guidance for Claude Code.
- `AGENTS.md`: repository guidelines (this file).
- `.gitattributes`: git settings.

Each agent file has a YAML frontmatter block (`---`, `name`, `description`) followed by a Markdown body with headings, lists, and output instructions.

## Build, Test, and Development Commands
There is no build system or runtime to execute. Optional local checks:
- `rg -n "^name:" *.yaml` — list agent identifiers.
- `yamllint *.yaml` — lint YAML files (if you have yamllint installed).

## Coding Style & Naming Conventions
- File names use lower-kebab-case and must match the frontmatter `name` plus `.yaml`.
- Common patterns:
  - `*-request.yaml`: control agents (workflow orchestrators)
  - `*-writer.yaml`: content creation agents
  - `*-maintainer.yaml`: maintenance agents
- Frontmatter fields should stay minimal and consistent: `name` (kebab-case) and `description` (single-line summary).
- Markdown body uses `#` for the title, `##`/`###` for sections, and bullet lists for requirements and output instructions.
- Keep content action-oriented and structured (Requirements, Output (TODO Only), Output Format (Task-Based), Quality Assurance Task Checklist).

## Testing Guidelines
No automated test suite is present. Validate changes by:
- Ensuring YAML frontmatter is valid.
- Confirming each YAML filename matches its frontmatter `name` (e.g., `name: foo` => `foo.yaml`).
- Confirming section structure and heading hierarchy remain consistent.
- Spot-checking that the `**RULE:**` TODO filename matches the agent `name`.

## Commit & Pull Request Guidelines
The git history currently contains a single “Initial commit,” so there is no established commit convention. Suggested approach:
- Use short, imperative summaries (e.g., “Add docs-maintainer agent”, “Update security audit output format”).

For PRs:
- Include a concise summary and list of changed agent files.
- Note any new agent types and update `README.md` if the catalog changes.
- Call out required output file names introduced by the agent rules (TODO files).

## Agent-Specific Instructions
Most agents end with a **RULE** that requires generating a `TODO_<agent-name>.md` file. When editing or adding agents, keep that rule accurate and aligned with the `name` field and any referenced outputs.
