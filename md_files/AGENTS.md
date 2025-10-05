# Repository Guidelines

## Project Structure & Module Organization
Core agent logic lives in `src/email_assistant`, with supporting PDF utilities in `src/pdf_generator`. Tests are collected under `tests` (scripts and notebook harnesses), while walkthrough notebooks live in `notebooks`. Operational collateral sits in `docs` and `observability`, and deploy automation is in `terraform`. Example scripts such as `run_map_agent.py` and configuration helpers stay at the repository root for quick experiments.

## Build, Test, and Development Commands
Run `uv sync --extra dev` to install runtime and tooling dependencies. Use `uv run python tests/run_all_tests.py --all` for the scripted regression suite and `uv run python tests/test_notebooks.py` to execute the notebook smoke tests. During ad-hoc development, `uv run python src/email_assistant/langgraph_101.py` spins up the introductory graph for local validation.

## Coding Style & Naming Conventions
We target Python 3.11 with Ruff enforcing `E`, `F`, `I`, `D`, `UP`, and `T201` rules; invoke `uv run ruff format` for layout fixes and `uv run ruff check --fix` to auto-resolve lint. Modules and packages use snake_case, public classes use CapWords, and async LangGraph node handlers should adopt verb-based function names (for example, `triage_inbox`). Type stubs (`py.typed`) ship with each distributable package, so keep annotations updated.

## Testing Guidelines
Pytest is the primary framework; name new tests `test_<feature>.py` and prefer parametrized cases for scenario coverage. Notebook regression relies on the harness in `tests/test_notebooks.py`; ensure long-running cells are gated or cached. When features touch Gmail or external APIs, provide mocks under `tests/fixtures` and guard network calls with feature flags.

## Commit & Pull Request Guidelines
Recent history follows Conventional Commit prefixes (`fix:`, `docs:`, etc.) with optional issue tags such as `(Issue #7)`. Scope your commits narrowly, include reproduction or validation notes in the body, and keep PR descriptions action oriented: summary, validation commands, and screenshots of UI artifacts when relevant. Link tracking issues via `Closes #<id>` so automation can reconcile task status.

## Agent-Specific Notes
Persisted memories and HITL artifacts are stored via LangGraph configuration files (see `langgraph.json`); update these alongside code changes. Document new planner or tool entry points inside `docs/` so operators understand required API keys, and scrub sensitive configuration before committing.
