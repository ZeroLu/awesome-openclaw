# Awesome OpenClaw 🤖

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

> A curated collection of OpenClaw tutorials, skills, and use cases.

[English](#) | [简体中文](README-zh-CN.md)

---

## 0. One Minute Introduction

### OpenClaw vs ChatGPT vs Claude Code

![OpenClaw vs ChatGPT vs Claude Code](openclaw-vs-chatgpt-vs-claude-code.png)

| Feature | ChatGPT | Claude Code | OpenClaw |
|---------|---------|-------------|----------|
| **Where it runs** | Cloud | Local | Local |
| **Data privacy** | ❌ Stored on servers | ✅ Local | ✅ Local |
| **Chat app integration** | ❌ | ❌ | ✅ WhatsApp/Telegram/Discord/iMessage |
| **Access local files** | ❌ | ✅ | ✅ |
| **Custom skills** | ❌ GPTs (limited) | ❌ | ✅ Unlimited |
| **Always on** | ❌ Need browser | ❌ Need terminal | ✅ Background service |
| **Multi-agent** | ❌ | ❌ | ✅ Multiple personas |
| **Primary use** | General chat | Coding assistant | Personal AI assistant |

---

## 1. How to Install

### Installation Options

| Method | Difficulty | Cost | Best for |
|--------|------------|------|----------|
| Official Install | ⭐⭐ | Free | Tech-savvy users wanting full control |
| EasyClaw | ⭐ | Free | Beginners, zero-config |
| Tencent Cloud | ⭐ | Paid | Enterprise users needing managed service |
| Alibaba Cloud | ⭐⭐ | Paid | Cloud-based, multi-device access |

### 1.1 Local Installation

#### Official (Recommended)

```bash
# macOS / Linux
curl -fsSL https://openclaw.ai/install.sh | bash

# Windows (PowerShell)
iwr -useb https://openclaw.ai/install.ps1 | iex

# Or via npm
npm install -g openclaw@latest
```

After installation:

```bash
openclaw onboard --install-daemon
openclaw channels login  # Configure chat channels
openclaw gateway --port 18789  # Start
```

#### Third-Party (More Beginner-Friendly)

**EasyClaw** - One-click install, zero config, no API key needed

👉 https://sanwan.ai/easyclaw.html

- Beginner-friendly
- Auto-configuration
- Runs locally, data stays private

**Tencent Cloud Manager** - Managed service

👉 https://claw.guanjia.qq.com

- Enterprise support
- 24/7 managed hosting
- Advanced features

### 1.2 Cloud Installation

**Miaoda (秒答)**

👉 https://miaoda.feishu.cn/bot-landing?open-from=claw_official_website

- 一键云端部署
- 开箱即用
- 无需配置

**Alibaba Cloud Wuying**

👉 https://help.aliyun.com/zh/wuying-workspace/use-cases/quickly-build-a-openclaw-through-a-cloud-computer-clawdbot

- Cloud-based
- Multi-device access
- Pay-as-you-go

**Tencent Cloud**

👉 https://www.tencentcloud.com/act/pro/intl-openclaw

- International support
- Enterprise deployment

---

## 2. Awesome Skills

OpenClaw has 5400+ community skills. Here are some popular ones.

> Full list: https://github.com/VoltAgent/awesome-openclaw-skills

### 🤖 AI & Coding

| Skill | Description |
|-------|-------------|
| [coding-agent](https://github.com/openclaw/skills/tree/main/skills/coding-agent) | Delegate coding tasks to Codex, Claude Code, or Pi agents |
| [github](https://github.com/openclaw/skills/tree/main/skills/github) | GitHub operations: PRs, Issues, CI, code search |
| [gemini](https://github.com/openclaw/skills/tree/main/skills/gemini) | Use Gemini CLI for coding assistance |
| [claude-code](https://github.com/openclaw/skills/tree/main/skills/claude-code-skill) | MCP integration for enhanced Claude Code |

### 🌐 Browser Automation

| Skill | Description |
|-------|-------------|
| [browser-vision](https://github.com/openclaw/skills/tree/main/skills/browser-vision) | Headless Chrome screenshots, web automation, visual debugging |
| [web-scraper](https://github.com/openclaw/skills/tree/main/skills/web-scraper) | Access anti-scraping sites: WeChat/Twitter/Reddit |
| [agent-browser](https://github.com/openclaw/skills/tree/main/skills/agent-browser) | Headless browser automation CLI optimized for AI agents |

### 🔍 Search & Research

| Skill | Description |
|-------|-------------|
| [deep-research](https://github.com/openclaw/skills/tree/main/skills/deep-research) | Multi-engine search + web extraction + structured analysis |
| [web-search](https://github.com/openclaw/skills/tree/main/skills/web-search) | Brave Search + DuckDuckGo multi-engine search |
| [academic-research](https://github.com/openclaw/skills/tree/main/skills/academic-research) | Search academic papers using OpenAlex API |

### 📝 Productivity

| Skill | Description |
|-------|-------------|
| [notion](https://github.com/openclaw/skills/tree/main/skills/notion) | Notion integration |
| [obsidian](https://github.com/openclaw/skills/tree/main/skills/obsidian) | Obsidian notes |
| [trello](https://github.com/openclaw/skills/tree/main/skills/trello) | Trello board management |
| [apple-notes](https://github.com/openclaw/skills/tree/main/skills/apple-notes) | Apple Notes integration |
| [apple-reminders](https://github.com/openclaw/skills/tree/main/skills/apple-reminders) | Apple Reminders integration |

### 💬 Messaging

| Skill | Description |
|-------|-------------|
| [discord](https://github.com/openclaw/skills/tree/main/skills/discord) | Discord bot integration |
| [slack](https://github.com/openclaw/skills/tree/main/skills/slack) | Slack bot integration |
| [imsg](https://github.com/openclaw/skills/tree/main/skills/imsg) | iMessage integration |
| [bluebubbles](https://github.com/openclaw/skills/tree/main/skills/bluebubbles) | BlueBubbles iMessage server |

### 🎨 Image & Video Generation

| Skill | Description |
|-------|-------------|
| [image-gen](https://github.com/openclaw/skills/tree/main/skills/image-gen) | Nano Banana Pro (Gemini 3) text-to-image, image-to-image |
| [video-gen](https://github.com/openclaw/skills/tree/main/skills/video-gen) | Video generation with Sora/Kling/Seedance/Veo 3 |
| [openai-image-gen](https://github.com/openclaw/skills/tree/main/skills/openai-image-gen) | DALL-E image generation |

### 🏠 Smart Home

| Skill | Description |
|-------|-------------|
| [sonoscli](https://github.com/openclaw/skills/tree/main/skills/sonoscli) | Sonos speaker control |
| [openhue](https://github.com/openclaw/skills/tree/main/skills/openhue) | Philips Hue control |
| [spotify-player](https://github.com/openclaw/skills/tree/main/skills/spotify-player) | Spotify playback control |

### ⚡ DevOps

| Skill | Description |
|-------|-------------|
| [n8n-automation](https://github.com/openclaw/skills/tree/main/skills/n8n-automation) | Design n8n workflow JSON |
| [security-audit](https://github.com/openclaw/skills/tree/main/skills/security-audit) | Skill security scanning + system hardening |

### Installing Skills

```bash
# From ClawHub
clawhub install <skill-slug>

# Or just send the skill link to your OpenClaw
# It will install automatically
```

---

## 3. Skill Packs

Pre-configured skill packs for specific use cases.

> Source: https://sanwan.ai/skills.html

### 🦸 Super Assistant

Best for: Office workers, managers, entrepreneurs

**Includes:** Email Management, Feishu Calendar, Feishu Docs, Web Search & Analysis, Weather, Basic Intelligence Pack

**One-Click Install Prompt:**
```
Please configure the "Super Assistant" skill pack with these skills:
- Email Management
- Feishu Calendar
- Feishu Docs
- Web Search & Analysis
- Weather
- Basic Intelligence Pack

Skill pack details: https://sanwan.ai/skills/pack-assistant.html

Please learn each skill's details page one by one, then tell me when you're ready.
```

---

### ✍️ Content Creator

Best for: Content creators, brand operators, personal IP builders

**Includes:** WeChat Official Account, Blog Writer, AI Image Generation, AI Text Humanizer

**One-Click Install Prompt:**
```
Please configure the "Content Creator" skill pack with these skills:
- WeChat Official Account
- Blog Writer
- AI Image Generation
- AI Text Humanizer

Skill pack details: https://sanwan.ai/skills/pack-creator.html

Please learn each skill's details page one by one, then tell me when you're ready.
```

---

### 📈 Stock Analyst

Best for: Stock traders, investors, quantitative enthusiasts

**Includes:** Web Search & Analysis, Deep Research, Coding Assistant, Basic Intelligence Pack

**One-Click Install Prompt:**
```
Please configure the "Stock Analyst" skill pack with these skills:
- Web Search & Analysis
- Deep Research
- Coding Assistant
- Basic Intelligence Pack

Skill pack details: https://sanwan.ai/skills/pack-trader.html

Please learn each skill's details page one by one, then tell me when you're ready.
```

---

### 🌏 Overseas Operations

Best for: Overseas enterprises, cross-border e-commerce, international markets

**Includes:** Twitter / X, SEO Writer, Web Search & Analysis, Deep Research, Basic Intelligence Pack

**One-Click Install Prompt:**
```
Please configure the "Overseas Operations" skill pack with these skills:
- Twitter / X
- SEO Writer
- Web Search & Analysis
- Deep Research
- Basic Intelligence Pack

Skill pack details: https://sanwan.ai/skills/pack-overseas.html

Please learn each skill's details page one by one, then tell me when you're ready.
```

---

### 🛒 E-commerce Operations

Best for: E-commerce sellers, brand owners, operations teams

**Includes:** AI Image Generation, SEO Writer, Web Search & Analysis, Deep Research

**One-Click Install Prompt:**
```
Please configure the "E-commerce Operations" skill pack with these skills:
- AI Image Generation
- SEO Writer
- Web Search & Analysis
- Deep Research

Skill pack details: https://sanwan.ai/skills/pack-ecommerce.html

Please learn each skill's details page one by one, then tell me when you're ready.
```

---

## 4. Awesome Use Cases

Real-world examples of how people use OpenClaw.

> Full list: https://github.com/hesamsheikh/awesome-openclaw-usecases

### 📰 Content Consumption

| Use Case | Description |
|----------|-------------|
| [Daily Reddit Digest](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/daily-reddit-digest.md) | Auto-summarize your favorite subreddits |
| [Daily YouTube Digest](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/daily-youtube-digest.md) | Daily summaries of your favorite channels |
| [Multi-Source Tech News](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/multi-source-tech-news-digest.md) | Aggregate tech news from 109+ sources |

### 🎬 Content Creation

| Use Case | Description |
|----------|-------------|
| [YouTube Content Pipeline](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/youtube-content-pipeline.md) | Automate video idea scouting and research |
| [Multi-Agent Content Factory](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/content-factory.md) | Multi-agent collaborative content production |
| [Podcast Production](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/podcast-production-pipeline.md) | Full podcast workflow automation |

### 💼 Productivity

| Use Case | Description |
|----------|-------------|
| [Personal CRM](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/personal-crm.md) | Auto-discover and track contacts |
| [Second Brain](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/second-brain.md) | Message the bot to record, searchable knowledge base |
| [Custom Morning Brief](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/custom-morning-brief.md) | Customized daily morning briefing |
| [Inbox De-clutter](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/inbox-declutter.md) | Auto-summarize newsletter subscriptions |

### 🏠 Automation

| Use Case | Description |
|----------|-------------|
| [Self-Healing Home Server](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/self-healing-home-server.md) | Self-healing home server with SSH access |
| [n8n Workflow Orchestration](https://github.com/hesamsheikh/awesome-openclaw-usecases/blob/main/usecases/n8n-workflow-orchestration.md) | Orchestrate automation via n8n webhooks |

---

## Resources

- 🌐 [OpenClaw Website](https://openclaw.ai)
- 📚 [Documentation](https://docs.openclaw.ai)
- 💻 [GitHub](https://github.com/openclaw/openclaw)
- 💬 [Discord](https://discord.com/invite/clawd)
- 🛒 [ClawHub](https://clawhub.com)

---

**Maintainer:** [Zero君](https://x.com/zerolu_eth) | [CyberBara](https://cyberbara.com) - Unified AI image & video generation platform
