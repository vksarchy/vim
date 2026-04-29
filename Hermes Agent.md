# Hermes Agent

Let me first search for what Hermes is in the context of Claude Code, since this is a relatively recent development.Alright Sid, I've got a solid picture now. Let me break this down for you.

## What is Hermes Agent?

Hermes Agent is a self-improving AI agent built by Nous Research. It's the only agent with a built-in learning loop — it creates skills from experience, improves them during use, nudges itself to persist knowledge, searches its own past conversations, and builds a deepening model of who you are across sessions.

Think of it this way: Claude Code is a *session-based* coding agent — you open it, do work, close it, and the next session starts fresh (aside from CLAUDE.md). Hermes is an orchestration framework that introduces planning, persistent memory, and task decomposition so the agent can handle complex goals without requiring manual step-by-step guidance.

The key differentiators from plain Claude Code:

**Self-improving skills** — After completing a complex task (typically five or more tool calls), the agent can synthesize that experience into a permanent, reusable skill document stored as structured markdown. The next time a similar task comes up, the agent loads the skill instead of solving from scratch. And skills self-improve during use.

**Persistent memory** — The agent writes its own notes about your environment, conventions, and things it learned in MEMORY.md. It also stores info about you in USER.md. Beyond those, it stores all past conversations in SQLite with FTS5 full-text search, so it can recall conversations from weeks ago.

**Multi-platform gateway** — Telegram, Discord, Slack, WhatsApp, Signal, and CLI — all from a single gateway process. You can talk to it from your phone while it works on a cloud VM or your local machine.

**Model agnostic** — It works with Nous Portal, OpenRouter (200+ models), OpenAI, or your own endpoint. Switch with `hermes model` — no code changes, no lock-in.

**Six terminal backends** — local, Docker, SSH, Daytona, Modal, Singularity. So it can execute commands locally or in an isolated container.

Now, importantly — Hermes is **separate from Claude Code**. It's not a plugin for Claude Code. It's a standalone agent that *can use Claude as its underlying model* (via Anthropic API or OpenRouter), but it runs its own agent loop, memory system, and skill framework. There's also a port called hermes-CCC that brings Hermes patterns *into* Claude Code natively, but the main project is standalone.

## Installing Hermes on your CachyOS machine

Since you already have Claude Code set up, you have the Anthropic API key ready. Let's get Hermes installed. The one-line installer handles Python, Node.js, dependencies, and the `hermes` command. It works on Linux, macOS, and WSL2.

Here's the step-by-step plan for your CachyOS box:

**Step 1 — Run the installer:**
```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

This will clone the repo, create a Python 3.11 venv via `uv`, install all dependencies, and symlink the `hermes` command to `~/.local/bin/`.

**Step 2 — Run initial setup:**
```bash
hermes setup
```
This interactive wizard walks you through choosing your LLM provider. Since you have an Anthropic API key, you can pick `anthropic` as your provider and set the model to `claude-sonnet-4-6` (or Opus if you want to burn tokens). Alternatively, you can use OpenRouter and pick any model.

**Step 3 — Verify:**
```bash
hermes doctor    # diagnostics
hermes version   # confirm installed
hermes           # launch the TUI
```

**Step 4 — Configure directories** (the installer usually does this, but just in case):
```bash
mkdir -p ~/.hermes/{cron,sessions,logs,memories,skills,pairing,hooks,image_cache,audio_cache}
```

**Step 5 — Optional config tweaks** in `~/.hermes/config.yaml`:
```yaml
terminal:
  backend: local      # or docker for isolation
  cwd: "."
  timeout: 180

agent:
  reasoning_effort: "medium"
```

## Building a test project

Once Hermes is running, here's a solid first test to see the learning loop in action:

```
# In the Hermes TUI, type:
❯ Create a Python FastAPI app in ~/projects/hermes-test with three endpoints: 
  GET /health, GET /items, POST /items. Include a requirements.txt 
  and a README.md. Then run the tests.
```

This exercises file creation, shell commands, and is complex enough that Hermes might auto-create a skill from the experience. After it finishes, you can check:

```bash
ls ~/.hermes/skills/          # see if it created a new skill
cat ~/.hermes/memories/MEMORY.md   # see what it learned about your system
```

For the Claude Code integration path specifically (using Hermes to orchestrate Claude Code), you'd use Hermes's terminal tool to invoke `claude -p` in print mode — but that's a more advanced pattern. Start with the standalone Hermes TUI first to get familiar with the workflow.

Want me to walk through any specific part in more detail — the config for using your Anthropic API key, setting up the Telegram gateway, or the Docker backend for sandboxed execution?
