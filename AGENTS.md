# Repository Guidelines

## Project Structure & Module Organization

This repository centers on operational playbooks for autonomous agents. The root keeps lightweight
entry points like `README.md` and this guide. Authoritative resources live in `md_files/`, where
published references sit alongside working drafts. Agent briefs live under
`md_files/.claude/agents/` (for example, `md_files/.claude/agents/backend-engineer.md`) and command
snippets in `md_files/.claude/commands/`. Keep new role profiles and shared assets in those folders
to maintain discoverability.

## Build, Test, and Development Commands

Content is Markdown-only, so no build step is required. During editing run
`npx markdownlint-cli "**/*.md"` to enforce formatting; install locally with
`npm install --save-dev markdownlint-cli` if needed. Use `npx prettier --check md_files/**/*.md`
before opening a PR, and `npx prettier --write md_files/**/*.md` when formatting fixes are required.

## Coding Style & Naming Conventions

Write in clear, direct English with second-person instructions where possible. Wrap Markdown at ~100
characters, use sentence-case headings, and prefer unordered lists for task lists. Name new agent
files with lowercase kebab-case (e.g., `risk-analyst.md`) and place supporting assets beside the
document they serve. Code snippets should declare the language for syntax highlighting.

## Testing Guidelines

Lint Markdown locally with `markdownlint` and ensure Prettier runs clean; both commands should exit
with code 0. When adding runnable snippets, confirm they execute in a clean shell and annotate
prerequisites inline. For large tables or workflows, preview the file in a Markdown renderer
(`code --preview` or GitHub web UI) to verify layout and link integrity.

## Commit & Pull Request Guidelines

History so far relies on short imperative subjects (`initial`), so keep using one-line summaries
under 60 characters and, when applicable, scope prefixes like `docs:`. Group related changes per
commit and document validation steps in the body. Pull requests should describe the motivation, list
validation commands, and link any tracking issues. Include screenshots or terminal captures when the
change affects rendered guidance.
