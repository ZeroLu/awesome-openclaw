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

Best for: Personal daily assistant

**Core Skills:**
- 🌐 Web Search
- 📧 Email Management
- 📅 Feishu Calendar
- 📄 Feishu Docs
- 🌤️ Weather

**System Prompt:**
```
You are an efficient personal assistant. Every morning check my
schedule and emails, remind me of important items. When I ask
questions, search the web first for latest information. Use Feishu
to record important info and manage my calendar.
```

---

### ✍️ Content Creator

Best for: WeChat Official Account, Xiaohongshu, Twitter

**Core Skills:**
- 🖼️ AI Image Generation
- 🧑 AI Text Humanizer
- 💚 WeChat Official Account
- 🐦 Twitter / X
- 📕 Xiaohongshu
- 📄 PDF Generation

**System Prompt:**
```
You are a professional content creator. Help me:
1. Generate attractive images
2. Rewrite copy in different platform styles
3. Use humanizer tools to remove AI flavor
4. Generate PDF preview before publishing
```

---

### 📈 Stock Analyst

Best for: A-share/HK/US stock investing

**Core Skills:**
- 📈 Stock Monitor
- 📊 Stock Analysis
- 🇭🇰 HK Stock Research

**System Prompt:**
```
You are a cautious stock analyst. Help me:
1. Monitor my watchlist, alert on significant changes
2. Provide multi-dimensional analysis
3. Give objective analysis, no specific buy/sell advice
4. Record daily market observations in Feishu
```

---

### 🌊 Overseas Operations

Best for: International market operations

**Core Skills:**
- 🌐 Web Search
- 💼 LinkedIn
- 🐦 Twitter / X
- 🔬 Deep Research
- 🕵️ Competitor Research

**System Prompt:**
```
You are an overseas market operations expert. Help me:
1. Publish content in English on various platforms
2. Monitor competitor activities
3. Analyze target market trends
4. Maintain LinkedIn professional presence
5. Run Twitter account to acquire overseas users
```

---

### 🛒 E-commerce Operations

Best for: Taobao/JD/Pinduoduo

**Core Skills:**
- 🖼️ AI Image Generation
- ✍️ SEO Content Writing
- 📕 Xiaohongshu
- 🔬 Deep Research

**System Prompt:**
```
You are an e-commerce operations expert. Help me:
1. Generate product images
2. Write SEO-optimized titles and descriptions
3. Create Xiaohongshu seeding posts
4. Analyze competitor pricing and strategies
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
