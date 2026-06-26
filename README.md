# own_harness

A minimal coding agent loop with a single tool: `bash`.

The agent takes a task as a command-line argument, calls a local or remote LLM, and iteratively executes shell commands until the task is complete.

## Requirements

- Python 3.10+
- [uv](https://docs.astral.sh/uv/)
- [Ollama](https://ollama.com/) (or any OpenAI-compatible LLM endpoint)

## Setup

```bash
# Install dependencies
uv sync

# Copy and configure environment
cp .env.example .env
```

Edit `.env` with your LLM settings:

```env
LLM_BASE_URL=http://localhost:11434/v1
LLM_API_KEY=ollama
LLM_MODEL=gemma4:latest
```

### Ollama quick start

```bash
ollama pull gemma4
ollama serve
```

## Usage

```bash
uv run agent.py "your task here"
```

**Examples:**

```bash
uv run agent.py "list all Python files and count lines of code"
uv run agent.py "find TODO comments in the codebase"
uv run agent.py "write a fizzbuzz function and run it"
```

## How it works

1. Sends the task + system prompt to the LLM
2. LLM responds with a `bash` tool call
3. Agent executes the command and feeds the output back
4. Repeats until the LLM responds without a tool call

## Linting

```bash
uv run ruff check agent.py
uv run ruff format agent.py
```
