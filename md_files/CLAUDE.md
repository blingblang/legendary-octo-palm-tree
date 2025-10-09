# Agents in this Repository

## Overview

This repository demonstrates building agents using LangGraph, focusing on an email assistant that
can:

- Triage incoming emails
- Draft appropriate responses
- Execute actions (calendar scheduling, etc.)
- Incorporate human feedback
- Learn from past interactions

## Environment Setup

### Recommended: Using uv (faster and more reliable)

```bash
# Install uv if you haven't already
pip install uv

# Install the package with development dependencies
uv sync --extra dev
```

### Alternative: Using pip

```bash
# Create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Ensure you have a recent version of pip (required for editable installs with pyproject.toml)
python3 -m pip install --upgrade pip

# Install the package in editable mode
pip install -e .
```

The package is installed as `interrupt_workshop` with import name `email_assistant`, allowing you to
import from anywhere with `from email_assistant import ...`

## Agent Implementations

### Scripts

The repository contains several implementations with increasing complexity in `src/email_assistant`:

1. **LangGraph 101** (`langgraph_101.py`)
   - Basics of LangGraph

2. **Basic Email Assistant** (`email_assistant.py`)
   - Core email triage and response functionality

3. **Human-in-the-Loop** (`email_assistant_hitl.py`)
   - Adds ability for humans to review and approve actions

4. **Memory-Enabled HITL** (`email_assistant_hitl_memory.py`)
   - Adds persistent memory to learn from feedback

5. **Gmail Integration** (`email_assistant_hitl_memory_gmail.py`)
   - Connects to Gmail API for real email processing

### Notebooks

Each aspect of the agent is explained in dedicated notebooks:

- `notebooks/langgraph_101.ipynb` - LangGraph basics
- `notebooks/agent.ipynb` - Basic agent implementation
- `notebooks/evaluation.ipynb` - Agent evaluation
- `notebooks/hitl.ipynb` - Human-in-the-loop functionality
- `notebooks/memory.ipynb` - Adding memory capabilities

## Running Tests

### Testing Scripts

Test to ensure all implementations work:

```bash
# Test all implementations
python tests/run_all_tests.py --all
```

(Note: This will leave out the Gmail implementation `email_assistant_hitl_memory_gmail` from
testing.)

### Testing Notebooks

Test all notebooks to ensure they run without errors:

```bash
# Run all notebook tests directly
python tests/test_notebooks.py
```

## Documentation Generation with ReadMeReady

### Environment Variables

ReadMeReady requires the following environment variables:

- **`OPENAI_API_KEY`**: Set to `dummy` to use open-source models, or provide a valid OpenAI API key
  for GPT-based generation
- **`HF_TOKEN`** (optional): Hugging Face token for accessing models hosted on Hugging Face Hub

### Installation

ReadMeReady is included in the development dependencies. To install manually:

```bash
pip install readme_ready==1.1.5 python-magic-bin  # Windows
# or
pip install readme_ready==1.1.5 python-magic  # Linux/Mac
```

### Usage

Generate documentation for this repository:

```bash
# Using the helper script (recommended)
python scripts/generate_readme.py

# Or run directly
OPENAI_API_KEY=dummy python -m readme_ready
```

When prompted:

1. Select "Readme" mode
2. Enter the repository root path
3. Specify output path as `docs/README.ReadMeReady.md`

### Workflow Guidelines

1. **When to regenerate**: Run ReadMeReady when significant structural changes are made to the
   codebase
2. **Review output**: Always review the generated markdown before incorporating into official
   documentation
3. **Preserve customizations**: The generated README is a draft - merge relevant sections into
   existing docs rather than replacing them entirely
4. **Ignore patterns**: The tool respects `.gitignore` patterns by default
