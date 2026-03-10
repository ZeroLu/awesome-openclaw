# Awesome OpenClaw 🤖

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome) [![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

> A curated collection of **OpenClaw tutorials**, **skills**, and **use cases** for building your personal AI assistant.

[OpenClaw](https://github.com/openclaw/openclaw) is an open-source AI assistant framework that runs locally on your machine. It supports multiple LLM providers, extensible skills, and cross-platform messaging channels.

｜[English](#)｜[简体中文](README-zh-CN.md)｜

## 📖 Table of Contents

1. [What is OpenClaw](#1-what-is-openclaw)
2. [Getting Started](#2-getting-started)
3. [Core Concepts](#3-core-concepts)
4. [Official Skills](#4-official-skills)
5. [Community Skills](#5-community-skills)
6. [Use Cases](#6-use-cases)
7. [Skill Development](#7-skill-development)
8. [Multi-Agent Routing](#8-multi-agent-routing)
9. [Resources](#9-resources)
10. [Contributing](#10-contributing)

---

## 1. What is OpenClaw

OpenClaw is a **self-hosted gateway** that connects your favorite chat apps — WhatsApp, Telegram, Discord, iMessage, and more — to AI coding agents like Pi. You run a single Gateway process on your own machine (or a server), and it becomes the bridge between your messaging apps and an always-available AI assistant.

### Key Features

| Feature | Description |
|---------|-------------|
| **Multi-channel Gateway** | WhatsApp, Telegram, Discord, iMessage with a single Gateway process |
| **Plugin Channels** | Add Mattermost and more with extension packages |
| **Multi-agent Routing** | Isolated sessions per agent, workspace, or sender |
| **Media Support** | Send and receive images, audio, and documents |
| **Web Control UI** | Browser dashboard for chat, config, sessions, and nodes |
| **Mobile Nodes** | Pair iOS and Android nodes for Canvas, camera/screen, and voice workflows |
| **Self-hosted** | Runs on your hardware, your rules |
| **Open Source** | MIT licensed, community-driven |

### How it Works

```
┌─────────────────┐    ┌─────────────┐    ┌──────────────────┐
│  Chat Apps      │    │  Gateway    │    │  AI Agent (Pi)   │
│  - WhatsApp     │───▶│             │───▶│                  │
│  - Telegram     │    │  (Port      │    │  - Claude        │
│  - Discord      │    │   18789)    │    │  - GPT           │
│  - iMessage     │    │             │    │  - Gemini        │
└─────────────────┘    └─────────────┘    └──────────────────┘
                              │
                              ▼
                       ┌─────────────┐
                       │  Web UI     │
                       │  Dashboard  │
                       └─────────────┘
```

---

## 2. Getting Started

### Prerequisites

- Node.js `>=22`
- pnpm (optional; recommended if building from source)
- **Recommended:** Brave Search API key for web search

### Installation

**Via npm:**
```bash
npm install -g openclaw@latest
```

**Via curl (recommended):**
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

**Windows (PowerShell):**
```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

### Quick Start (3 steps)

```bash
# 1. Run onboarding wizard
openclaw onboard --install-daemon

# 2. Pair WhatsApp (or other channels)
openclaw channels login

# 3. Start the Gateway
openclaw gateway --port 18789
```

### Dashboard

Open the browser Control UI after the Gateway starts:

- Local default: http://127.0.0.1:18789/
- Remote access: [Web surfaces](https://docs.openclaw.ai/web) and [Tailscale](https://docs.openclaw.ai/gateway/tailscale)

### Pairing Your First Channel

#### WhatsApp (QR Login)

```bash
openclaw channels login
```

Scan the QR code via WhatsApp → Settings → Linked Devices.

#### Telegram / Discord

The wizard can write tokens/config for you. For manual setup:

- **Telegram:** Create a bot via [@BotFather](https://t.me/botfather), get the token
- **Discord:** Create a bot in [Developer Portal](https://discord.com/developers/applications)

### Private Message Security

By default, unknown private messages receive a pairing code. Approve before the bot responds:

```bash
openclaw pairing list whatsapp
openclaw pairing approve whatsapp <code>
```

---

## 3. Core Concepts

### Agent Workspace

Each agent has a workspace containing:

```
~/.openclaw/workspace/
├── AGENTS.md      # Agent behavior rules
├── SOUL.md        # Personality and tone
├── USER.md        # User preferences
├── MEMORY.md      # Long-term memory
├── HEARTBEAT.md   # Periodic task config
├── TOOLS.md       # Local tool notes
├── memory/        # Daily logs
│   └── 2026-03-10.md
└── skills/        # Custom skills
```

### Memory System

OpenClaw has a two-tier memory system:

- **Daily notes:** `memory/YYYY-MM-DD.md` — raw logs of what happened
- **Long-term:** `MEMORY.md` — curated memories (only loaded in main session)

**Important:** Load `MEMORY.md` only in direct chats with your human, NOT in shared contexts (Discord, group chats) for security.

### Heartbeats

Heartbeats are periodic checks that run when the agent receives a poll. Use them for:

- Checking emails, calendar, notifications
- Updating memory files
- Background maintenance tasks
- Proactive outreach (with care)

Configure in `HEARTBEAT.md`:

```markdown
# Heartbeat Tasks

## 1. Email Check
- Check for urgent unread messages

## 2. Calendar
- Look for upcoming events in next 24h
```

### Skills

Skills teach the agent how to use tools. Each skill is a folder with `SKILL.md`:

```markdown
---
name: my-skill
description: What this skill does
---

# Instructions
How to use this skill...
```

Skill locations (precedence from high to low):
1. `<workspace>/skills` — per-agent skills
2. `~/.openclaw/skills` — shared skills
3. Bundled skills — shipped with OpenClaw

---

## 4. Official Skills

OpenClaw comes with 50+ built-in skills for various tasks.

### 🤖 AI & Coding

| Skill | Description |
|-------|-------------|
| [coding-agent](https://github.com/openclaw/openclaw/tree/main/skills/coding-agent) | Delegate coding tasks to Codex, Claude Code, or Pi agents |
| [gh-issues](https://github.com/openclaw/openclaw/tree/main/skills/gh-issues) | Fetch GitHub issues, spawn sub-agents to implement fixes and open PRs |
| [github](https://github.com/openclaw/openclaw/tree/main/skills/github) | GitHub operations via `gh` CLI: issues, PRs, CI runs |
| [summarize](https://github.com/openclaw/openclaw/tree/main/skills/summarize) | Text summarization |
| [gemini](https://github.com/openclaw/openclaw/tree/main/skills/gemini) | Use Gemini CLI for coding assistance |

### 📝 Productivity

| Skill | Description |
|-------|-------------|
| [notion](https://github.com/openclaw/openclaw/tree/main/skills/notion) | Notion integration |
| [obsidian](https://github.com/openclaw/openclaw/tree/main/skills/obsidian) | Obsidian note-taking |
| [apple-notes](https://github.com/openclaw/openclaw/tree/main/skills/apple-notes) | Apple Notes integration |
| [apple-reminders](https://github.com/openclaw/openclaw/tree/main/skills/apple-reminders) | Apple Reminders integration |
| [things-mac](https://github.com/openclaw/openclaw/tree/main/skills/things-mac) | Things 3 task manager |
| [trello](https://github.com/openclaw/openclaw/tree/main/skills/trello) | Trello board management |
| [bear-notes](https://github.com/openclaw/openclaw/tree/main/skills/bear-notes) | Bear notes integration |

### 💬 Messaging Channels

| Skill | Description |
|-------|-------------|
| [discord](https://github.com/openclaw/openclaw/tree/main/skills/discord) | Discord bot integration |
| [slack](https://github.com/openclaw/openclaw/tree/main/skills/slack) | Slack bot integration |
| [imsg](https://github.com/openclaw/openclaw/tree/main/skills/imsg) | iMessage integration |
| [bluebubbles](https://github.com/openclaw/openclaw/tree/main/skills/bluebubbles) | BlueBubbles iMessage server |

### 🔧 Utilities

| Skill | Description |
|-------|-------------|
| [weather](https://github.com/openclaw/openclaw/tree/main/skills/weather) | Weather forecasts via wttr.in or Open-Meteo |
| [tmux](https://github.com/openclaw/openclaw/tree/main/skills/tmux) | Remote-control tmux sessions |
| [video-frames](https://github.com/openclaw/openclaw/tree/main/skills/video-frames) | Extract frames from videos using ffmpeg |
| [session-logs](https://github.com/openclaw/openclaw/tree/main/skills/session-logs) | Search and analyze session logs using jq |
| [skill-creator](https://github.com/openclaw/openclaw/tree/main/skills/skill-creator) | Create and package new skills |
| [healthcheck](https://github.com/openclaw/openclaw/tree/main/skills/healthcheck) | Host security hardening and risk-tolerance configuration |

### 🎨 Media & Generation

| Skill | Description |
|-------|-------------|
| [openai-image-gen](https://github.com/openclaw/openclaw/tree/main/skills/openai-image-gen) | DALL-E image generation |
| [openai-whisper](https://github.com/openclaw/openclaw/tree/main/skills/openai-whisper) | Local Whisper transcription |
| [openai-whisper-api](https://github.com/openclaw/openclaw/tree/main/skills/openai-whisper-api) | OpenAI Whisper API transcription |
| [sag](https://github.com/openclaw/openclaw/tree/main/skills/sag) | ElevenLabs TTS integration |
| [sherpa-onnx-tts](https://github.com/openclaw/openclaw/tree/main/skills/sherpa-onnx-tts) | Local TTS with Sherpa-ONNX |

### 🏠 Smart Home

| Skill | Description |
|-------|-------------|
| [sonoscli](https://github.com/openclaw/openclaw/tree/main/skills/sonoscli) | Sonos speaker control |
| [openhue](https://github.com/openclaw/openclaw/tree/main/skills/openhue) | Philips Hue control |
| [spotify-player](https://github.com/openclaw/openclaw/tree/main/skills/spotify-player) | Spotify playback control |

### 🔒 Security & DevOps

| Skill | Description |
|-------|-------------|
| [1password](https://github.com/openclaw/openclaw/tree/main/skills/1password) | 1Password integration |

---

## 5. Community Skills

Community-contributed skills for specialized workflows.

### 📣 Content & Marketing

| Skill | Description | Author |
|-------|-------------|--------|
| [content-promotion](skills/content-promotion/SKILL.md) | Multi-platform content promotion workflow (知乎, 掘金, Dev.to, Product Hunt, etc.) | [@ZeroLu](https://github.com/ZeroLu) |
| [ultimate-ai-media-generator](skills/ultimate-ai-media-generator/SKILL.md) | CyberBara Public API v1 image/video generation tasks | [@ZeroLu](https://github.com/ZeroLu) |

### 📚 Feishu Integration

OpenClaw has built-in Feishu (Lark) support with these capabilities:

- **Documents:** Read, write, append, create tables, upload images
- **Bitable:** CRUD operations on records and fields
- **Drive:** File and folder management
- **Wiki:** Knowledge base navigation
- **Chat:** Get chat info and members

---

## 6. Use Cases

Real-world examples of how people use OpenClaw.

### 6.1. Content Creator Assistant

Automate content creation and cross-platform publishing:

```
User: "Check my X bookmarks and recommend content to repost to Jike"
```

**Workflow:**
1. Agent opens X bookmarks via browser
2. Scrapes recent bookmarks with metadata (views, likes)
3. Filters by engagement (views > 100K, likes > 1000)
4. Translates content to Chinese
5. Downloads media (videos/images)
6. Writes recommendations to `daily_recommendations.md`
7. Waits for user confirmation before posting

**Related Skills:** `browser`, `web_fetch`, `video-frames`

### 6.2. Developer Productivity

**Code Review:**
```
User: "Review the latest PR in openclaw/openclaw"
```

Agent:
1. Uses `gh` CLI to fetch PR details
2. Reads changed files
3. Analyzes code quality, suggests improvements
4. Posts review comments via `gh pr comment`

**Issue Management:**
```
User: "Create a PR to fix issue #123"
```

Agent:
1. Reads issue details
2. Explores codebase to understand context
3. Implements fix
4. Creates branch, commits, pushes
5. Opens PR with description

**Related Skills:** `github`, `coding-agent`, `gh-issues`

### 6.3. Personal Knowledge Management

**Obsidian Integration:**
```
User: "What did I write about AI agents last month?"
```

Agent:
1. Searches Obsidian vault for relevant notes
2. Summarizes findings
3. Links to specific notes

**Session Memory:**
```
User: "What did we discuss about the server migration?"
```

Agent:
1. Searches session logs via `memory_search`
2. Retrieves relevant context from `MEMORY.md`
3. Provides summary with citations

**Related Skills:** `obsidian`, `session-logs`, memory system

### 6.4. Smart Home Automation

**Voice Control:**
```
User: "Announce dinner time on all speakers"
```

Agent:
1. Uses TTS to generate announcement
2. Plays on Sonos speakers via `sonoscli`

**Scene Control:**
```
User: "Set movie mode"
```

Agent:
1. Dims lights via `openhue`
2. Pauses music on Spotify
3. Announces via TTS

**Related Skills:** `sonoscli`, `openhue`, `sag`, `spotify-player`

### 6.5. Multi-Agent Routing

Separate agents for different contexts:

```json5
{
  agents: {
    list: [
      {
        id: "personal",
        workspace: "~/.openclaw/workspace-personal",
        model: "anthropic/claude-sonnet-4-5",
      },
      {
        id: "work",
        workspace: "~/.openclaw/workspace-work",
        model: "anthropic/claude-opus-4-5",
      },
    ],
  },
  bindings: [
    { agentId: "personal", match: { channel: "whatsapp", accountId: "personal" } },
    { agentId: "work", match: { channel: "telegram" } },
  ],
}
```

---

## 7. Skill Development

### Creating a New Skill

1. **Create skill directory:**
```bash
mkdir -p ~/.openclaw/skills/my-skill
```

2. **Create `SKILL.md`:**
```markdown
---
name: my-skill
description: What this skill does. This is used for automatic skill activation.
---

# My Skill

## What it does
Detailed description of the skill.

## How to use
Step-by-step instructions.

## Tools
List of tools this skill provides or uses.

## Configuration
Any required API keys or settings.
```

3. **Add optional files:**
```
my-skill/
├── SKILL.md          # Required
├── skill.json        # Optional: metadata
├── scripts/          # Optional: shell scripts
└── assets/           # Optional: images, templates
```

### Skill Metadata

The frontmatter supports these fields:

```yaml
---
name: skill-name
description: Brief description (used for activation)
homepage: https://example.com
user-invocable: true
disable-model-invocation: false
metadata:
  openclaw:
    emoji: "🤖"
    requires:
      bins: ["required-cli"]
      env: ["API_KEY"]
      config: ["some.config.path"]
---
```

### Gating Rules

Skills are filtered at load time based on:

- `requires.bins` — CLI binaries that must exist
- `requires.env` — Environment variables required
- `requires.config` — Config paths that must be truthy
- `os` — Platform restriction (`darwin`, `linux`, `win32`)

### Best Practices

1. **Keep `SKILL.md` concise** — Focus on actionable instructions
2. **Use clear triggers** — Description determines automatic activation
3. **Document requirements** — API keys, configuration, dependencies
4. **Test across providers** — Ensure compatibility with different LLMs
5. **Security first** — Don't expose secrets in prompts or logs

---

## 8. Multi-Agent Routing

### What is Multi-Agent?

Each **agent** is a fully isolated "brain" with its own:

- **Workspace** — Files, AGENTS.md, SOUL.md, USER.md
- **State directory** — Auth profiles, model registry
- **Session storage** — Chat history + routing state

### Use Cases

1. **Multiple people, one server** — Each person gets their own agent
2. **Multiple personas** — Work assistant vs personal assistant
3. **Model routing** — Fast model for chat, powerful model for deep work
4. **Sandbox isolation** — Restrict tools for certain agents

### Example: Two WhatsApp Numbers, Two Agents

```json5
{
  agents: {
    list: [
      {
        id: "home",
        workspace: "~/.openclaw/workspace-home",
      },
      {
        id: "work",
        workspace: "~/.openclaw/workspace-work",
      },
    ],
  },
  bindings: [
    { agentId: "home", match: { channel: "whatsapp", accountId: "personal" } },
    { agentId: "work", match: { channel: "whatsapp", accountId: "biz" } },
  ],
}
```

### Routing Priority

Bindings are deterministic, most specific wins:

1. `peer` match (exact DM/group/channel ID)
2. `guildId` (Discord)
3. `teamId` (Slack)
4. `accountId` match
5. Channel-level match
6. Default agent

### Adding Agents

```bash
# Interactive
openclaw agents add work

# Non-interactive
openclaw agents add work \
  --workspace ~/.openclaw/workspace-work \
  --model anthropic/claude-opus-4-5 \
  --bind whatsapp:biz \
  --non-interactive
```

---

## 9. Resources

### Official

- 🌐 [OpenClaw Website](https://openclaw.ai)
- 📚 [Documentation](https://docs.openclaw.ai)
- 📖 [中文文档](https://docs.openclaw.ai/zh-CN/)
- 💻 [GitHub Repository](https://github.com/openclaw/openclaw)
- 💬 [Discord Community](https://discord.com/invite/clawd)
- 🛒 [ClawHub](https://clawhub.com) — Discover and share skills

### Documentation Hubs

| Hub | Description |
|-----|-------------|
| [Getting Started](https://docs.openclaw.ai/start/getting-started) | From zero to first message |
| [Configuration](https://docs.openclaw.ai/gateway/configuration) | Gateway settings, tokens, providers |
| [Channels](https://docs.openclaw.ai/channels) | WhatsApp, Telegram, Discord, iMessage setup |
| [Nodes](https://docs.openclaw.ai/nodes) | iOS and Android mobile nodes |
| [Skills](https://docs.openclaw.ai/tools/skills) | Skill development and configuration |
| [Security](https://docs.openclaw.ai/gateway/security) | Tokens, allowlists, safety controls |

### Related Projects

- [awesome-seedance](https://github.com/ZeroLu/awesome-seedance) — Seedance 2.0 prompts collection
- [awesome-nanobanana-pro](https://github.com/ZeroLu/awesome-nanobanana-pro) — Nano Banana Pro prompts
- [CyberBara](https://cyberbara.com) — Unified AI image & video generation platform

---

## 10. Contributing

Contributions are welcome! If you have:

- **A new skill** to share
- **A use case** to document
- **A tutorial** to add
- **Improvements** to existing content

Please submit a Pull Request.

### Guidelines

1. Follow the existing format and style
2. Include clear descriptions and examples
3. Link to original sources when applicable
4. Test any code examples before submitting

---

## Star History

<a href="https://star-history.com/#ZeroLu/awesome-openclaw&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=ZeroLu/awesome-openclaw&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=ZeroLu/awesome-openclaw&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=ZeroLu/awesome-openclaw&type=Date" />
 </picture>
</a>

---

**Sponsor**: This repository is maintained by [Zero君](https://x.com/zerolu_eth). Check out [CyberBara](https://cyberbara.com) for unified AI image & video generation with Sora 2, Kling 2.6, Seedance 2.0, and Veo 3.1.
