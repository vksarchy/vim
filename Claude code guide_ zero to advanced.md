# Source : https://x.com/zostaff/status/2042902138322407586


To view keyboard shortcuts, press question mark
View keyboard shortcuts
Article

See new posts
Conversation
zostaff
@zostaff
The Complete Claude Code Guide: Zero to Advanced
90% of people use Claude Code like a chatbot and complain that "AI doesn't work."
The problem isn't AI. The problem is you.
I spent 20+ hours putting together a complete guide: from first launch to the level where the agent closes tasks for you while you drink coffee.
Setup -> config -> skills -> subagents -> context -> deploy -> process.
Everything you need to know in 2026.
Claude Code is not a chatbot.
It's an agent with access to your computer.
It can read, create, modify, and delete files. Search the web. Open pages. Run terminal commands.
You say "create a folder" - it creates one. No magic, just tools.

❯ claude
╭─────────────────────────────────╮
│  Claude Code v1.0.80            │
╰─────────────────────────────────╯

❯ Create a Chrome extension with a checklist
  based on @course.md

⠋ Thinking it through...

  ✓ Read: course.md (2.4KB)
  ✓ Created: manifest.json
  ✓ Created: sidepanel.html
  ✓ Created: styles.css
  ✓ Created: app.js

✓ Done · 18.5K tokens · 2% context
If you're still copying code from ChatGPT and pasting it by hand - you're working in 2023.
Two ways to work
IDE Extension (VS Code / Windsurf / Cursor) — nicer UI, fewer features
Terminal (recommended) — more capabilities, status line, voice, btw commands, split screen = multiple sessions in parallel
For terminal I recommend Warp or iTerm2.
Most people are scared of the terminal. Then they wonder why their results are worse than those who aren't.
First things after install
Create an alias for bypass permissions:
alias claude='claude --dangerously-skip-permissions'
Yes, it sounds scary. No, in 6+ months - zero problems. You're more likely to accidentally delete your root folder yourself than Claude is.
2.     Install Whisper (Whisper Flow or Aqua Voice) - speaking is faster than typing. If you're still typing prompts by hand - you're losing 40% of your speed.
# ~/.zshrc

# ── Claude Code ──────────────────
alias claude='claude --dangerously-skip-permissions'

# ── shortcuts ────────────────────
alias cc='claude'
alias ccr='claude --resume'

❯ source ~/.zshrc
❯ claude
⚠ Bypass permissions enabled
✓ Ready. No confirmations.
Pricing
 Pro ($20/mo) - good starting point
 Max 5x ($100/mo) - enough for most people
Max 20x ($200/mo) - multiple projects + Agent Teams
Start with Pro. If you hit limits - upgrade to 5x, they prorate the difference.
The same tasks through API cost ~$500/mo. The $100 subscription is a 5x saving. If you're still paying for API directly - do the math.
This is where 90% of people waste money and patience
Every new session = blank slate. The agent knows nothing about your project. Without CLAUDE.md it spends tokens exploring your project structure every time. Small project - 33K tokens wasted. Large project - hundreds of thousands.
# Without CLAUDE.md:
❯ claude
  Scanning project structure...
  Reading package.json...
  Reading tsconfig.json...
  Analyzing 47 files...

  Tokens: 33K used just to understand the project
  Your messages: 0

# With CLAUDE.md:
❯ claude
  Loaded CLAUDE.md (86 lines)
  Ready.

  Tokens: 1.2K
  Your messages: 0

  → 27x cheaper on every session start
Fix: run /init - creates a CLAUDE.md describing your project. Next session starts with context.
Rule: CLAUDE.md = what the agent must know EVERY session. Keep it short (<500 lines). If it's longer - you're doing something wrong.
Auto Memory - the agent's automatic notes
Honestly? I don't love it. Too much magic. Stored at user/project level, can't share with team, hard to control.
❯ /init

⠋ Analyzing project structure...

Created: CLAUDE.md

  # My Project
  ## Overview
  Chrome extension - markdown to checklist
  ## Architecture
  ├── chrome-extension/
  │   ├── manifest.json
  │   ├── sidepanel.html
  │   └── app.js
  ├── landing/
  └── CLAUDE.md
  ## Rules
  - Always update extension version on changes
  - Use conventional commits

✓ CLAUDE.md saved · 86 lines
Advice: important things go explicitly in CLAUDE.md. Let Auto Memory run in the background, but don't rely on it. Magic is when you don't understand what's happening. And when you don't understand - you can't fix it.
MCP = descriptions of API endpoints the agent can call
Example: install Chrome DevTools MCP -> agent can open tabs, take screenshots, click elements.
# Install globally (needed everywhere):
❯ claude mcp add chrome-devtools \
    --scope user \
    npx @anthropic/chrome-devtools-mcp

# Install per project (not needed everywhere):
❯ claude mcp add supabase \
    --scope project \
    npx supabase-mcp

# Verify:
❯ /mcp
  chrome-devtools  ✓ connected (user)
  exa-search       ✓ connected (user)
  supabase         ✓ connected (project)
Install globally - only what you need EVERYWHERE (Exa, Chrome DevTools). Per project - everything else (Supabase, Playwright, etc.).
Rookie mistake: installing 15 MCPs globally and wondering why context runs out on the third message.
But MCP has a problem that almost nobody talks about
 Can bloat context (in tools other than Claude Code)
 Fixed scenarios - can't customize
You want 1 task from a tracker, but MCP fetches ALL tasks. Agent searches through them - burns context on garbage.
The fix that few people know -> Skills + CLI.
Skills - the next level after MCP, and most people never get there
A skill = folder with instructions + helper files. Only the header (name + description) goes into context. Triggered by description. Loaded on demand.
Where to find them: skills.sh - skill marketplace by Vercel. 100+ ready solutions.
# MCP (old approach):
  → All endpoints loaded into context
  → Fixed scenarios
  → Can't customize
  → 5.7K+ tokens per MCP

# Skills (new approach):
  → Only header in context (~50 tokens)
  → Loaded on demand
  → Editable and combinable
  → Any API = skill without MCP

# Example:
❯ Create a landing page for the app

  Loaded skill: Landing Page Creator
  Loaded skill: Frontend Design
  Combined: 2 skills · 0.3K tokens

  vs MCP: 11.4K tokens to load same tools
If a tool has Skill + CLI - use it instead of MCP. More flexible, more efficient. All top tools are moving to skills. If you haven't - you're behind.
Creating your own skills
 Install Skill Creator (available in the official marketplace)
 Describe what you need: "create a skill for generating landing pages from a reference image"
 Iterate - it won't be perfect on the first try
Skills can be combined. Landing Creator + Frontend Design = landing page with great design.
Any API with documentation can become a skill - no MCP needed. If you're paying for an MCP that a free skill can replace - you're paying for laziness.
Now for what actually separates beginners from advanced users: subagents
Two problems with the main session: can't parallelize and context is finite.
Subagents solve both: isolated context, parallel execution, results return to the orchestrator.
Numbers:
3 landing pages sequentially = 15 min, 300K tokens
3 landing pages via subagents = 5 min, 50K tokens in main session
3x faster, 6x cheaper. And you're still doing everything in one session?
Subagents: limited functionality, receive only the context passed to them
You can set the model:
 Opus for plans
Sonnet for code
 Haiku for search
You can preload skills.
# Without subagents (sequential):
  Landing v1  ████████░░  5 min · 100K tokens
  Landing v2  ████████░░  5 min · 100K tokens
  Landing v3  ████████░░  5 min · 100K tokens
  ─────────────────────────────────────
  Total:      15 min · 300K tokens
  Main ctx:   300K (overflowed ☠)

# With subagents (parallel):
  Sub 1 → v1  ████████░░  5 min · 100K (isolated)
  Sub 2 → v2  ████████░░  5 min · 100K (isolated)
  Sub 3 → v3  ████████░░  5 min · 100K (isolated)
  ─────────────────────────────────────
  Total:      5 min · 50K in main context
  Main ctx:   50K ✓ clean
Two ways to launch:
 On the fly: "spin up two subagents for two design versions"
 Pre-defined: file in .claude/agents/
Those who define agents upfront - control the result. Those who hope it "figures itself out" - get garbage.
Agent Teams - a team of full-fledged agents.
Unlike subagents: each teammate = full Claude session, shared task list, can communicate with each other, you can talk to each one.
Sounds like a dream? There's a catch.
DON'T use for writing code as a beginner. Seriously. You'll get a team made of chaos. Use for multi-perspective research, idea discussion, competing hypotheses.
# .claude/agents/landing-creator.md

---
name: landing-creator
model: sonnet
color: yellow
skills:
  - landing-page
  - frontend-design
---

# Model selection:
  Opus    -> plans, architecture, decisions
  Sonnet  -> writing code
  Haiku   -> searching documentation

# Opus without a plan = Ferrari on a dirt road
# Sonnet with a good plan = bullseye
Heavy on context. Without process understanding - it's money down the drain.
Context - the most important concept
 If you don't understand context, you don't understand anything.
Context window = your budget. Everything goes in: tools, CLAUDE.md, MCP, skills, your conversation.
Zones:
0-50% - effective work
50-70% - be careful
70-85% - problems ahead
85% - auto-compact (context loss)
Context: ██████████████████████░░░░░░░░░  67%

 0%━━━━━━50%━━━━━━70%━━━━━━85%━━━100%

# Your status line:
❯ ~/my-project · opus-4 · 1M ctx · 67% ■■■■■■░░

# 3 rules:
  1. CLAUDE.md < 500 lines
  2. 1 task = 1 session -> /clear
  3. Tools per project, not global
Install status line - see fill percentage in real time. If you can't see that number - you're driving blindfolded.
3 rules that will save you hundreds of dollars in tokens
 Don't bloat your tools - CLAUDE.md < 500 lines, only necessary MCPs/skills, no contradictions
 Eat the elephant one bite at a time - 1 task = 1 session, task done -> /clear -> new session
 Install tools per-project, not globally - global = only what's needed EVERYWHERE
Break even one - you lose context, money, and patience. Break all three? Then you're the one tweeting "AI is just hype."
Model selection - another point where people burn their budget
 Opus: planning, complex decisions, orchestration
Sonnet: writing code (with a good plan)
Haiku: searching documentation
Effort: low / medium / high. Default is medium.
No limit problems -> stay on Opus. Have limits -> Opus for plans, Sonnet for code in subagents.
Writing code on Opus without a plan is like driving a Ferrari on a dirt road. Power is there, results aren't.
Deploy
This is where vibe coders split into two types: those who share localhost links, and those who make money.
Fastest path: Vercel for frontend. npx vercel -> auth -> deploy. Done.
For backend: Railway, Supabase, Directus.
❯ npx vercel
  ? Set up and deploy? Yes
  ? Which scope? my-team
  ? Link to existing project? No
  ? What's your project's name? my-app
  ? In which directory is your code? ./landing

  🔗 https://my-app.vercel.app

  ✓ Production deployed
If building a public service with user data - think about backups, permissions, closing endpoints, legal risks. You can validate a hypothesis in an hour. But if you leak your user database - an hour won't help.
Git = save points in a game
No Git = no saves. Good luck replaying from scratch.
git init -> commit -> push -> pull. GitHub = cloud storage + collaboration + automations.
❯ git init
❯ git add .
❯ git commit -m "feat: initial chrome extension"

# Branches:
❯ git checkout -b feature/landing-v2
  Switched to new branch 'feature/landing-v2'

# Worktree (parallel work):
❯ git worktree add ./worktrees/v2 feature/landing-v2
❯ git worktree add ./worktrees/v3 feature/landing-v3

# Two Claudes simultaneously:
  [Terminal 1] ~/worktrees/v2 ❯ claude
  [Terminal 2] ~/worktrees/v3 ❯ claude

  → Don't interfere with each other
Must: private repositories. Google "github leaked api keys" - thousands of people who thought "nobody cares about my project."
# ✗ WRONG (secrets in code):
  .env
  ├── OPENAI_KEY=sk-proj-abc123...
  ├── VERCEL_TOKEN=vrl_def456...
  └── DB_PASSWORD=supersecret

# ✓ RIGHT (secrets in GitHub):
  Settings → Secrets → Actions
  ├── OPENAI_KEY      ••••••••
  ├── VERCEL_TOKEN    ••••••••
  └── DB_PASSWORD     ••••••••

  → Local: test keys only
  → Production: CI/CD only
Git Worktree - a physical copy of your project in a separate folder. Two Claudes working in parallel, different branches, no conflicts. If you're not using worktree - you're standing in line for your own project.
GitHub Actions = automation
Push to main -> tests run -> deploy to Vercel.
Store secrets (API keys, passwords) in GitHub Secrets, NOT in code, NOT locally.
Production keys on your local machine - it's not a question of "if they leak," it's "when they leak." CI/CD only.
Now the most important part
 What separates people who "play with AI" from those who build products.
Process.
DORA 2025: strong teams with AI get stronger, weak teams discover more problems. The biggest ROI comes not from tools, but from process quality.
If you don't have a process - you're automating chaos. Fast chaos is still chaos.
Minimum: Planning -> Plan review -> Decomposition -> Implementation via subagents -> Code review
Every stage starts with a plan. No exceptions.
A ready-made solution used by 109K+ developers: Superpowers
Brainstorm -> Specification -> Plan -> Subagent Driven Development -> Code Review -> Merge/PR
Real case: 9 tasks completed, only 9% context used. Because everything ran in subagents.
Meanwhile someone else does one task and hits 85%. The difference isn't the model. The difference is the process.
# Without process:
  ❯ Build me an app
  ... 300K tokens later ...
  ✗ Context overflow
  ✗ Code doesn't work
  ✗ Start over

# With process (Superpowers):
  ❯ /brainstorm
  ❯ /plan
  ❯ /implement (subagent driven)
  ❯ /review

  Result:
  ├── 9 tasks completed
  ├── 9% context used
  ├── Tests passing
  └── PR ready to merge

  → Difference isn't the model. It's the process.
The minimum toolkit you need to stop working at half capacity
Exa MCP - search (better than built-in)
Context7 Skill + CLI - fresh library docs
 Chrome DevTools MCP - browser automation
 Frontend Design Skill - design without that "purple AI look"
 Skill Creator - build your own skills
 Find Skills - search skills from Claude Code
 Superpowers - development process
Every tool on this list is free or included in the subscription. No more excuses.
The path from zero to advanced:
0. Understand it's an agent, not a chatbot
1. Install + bypass permissions + Whisper
2. CLAUDE.md - context savings
3. MCP -> Skills -> Subagents -> Agent Teams
4. Understand context and monitor it
5. One-click deploy
6. Git for safety and parallel work
7. Process: plan -> decompose -> implement -> review
Secret level: it doesn't exist. Keep learning.
  0  ░░░░░░░░░░  agent ≠ chatbot
  1  ██░░░░░░░░  install + bypass + whisper
  2  ████░░░░░░  CLAUDE.md
  3  ██████░░░░  MCP → Skills → Subagents
  4  ████████░░  context
  5  █████████░  deploy
  6  █████████░  git
  7  ██████████  process

  Secret level: ██████████ doesn't exist
  Keep learning.
Study approaches, not tools. If Claude Code disappears tomorrow, you just move your process to another tool. Those who only learned the buttons? They start from zero. Again.
Want to publish your own Article?
Upgrade to Premium
3:16 PM · Apr 11, 2026
·
158K
 Views
Relevant
View quotes

