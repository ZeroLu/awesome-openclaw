# Awesome OpenClaw 🤖

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome) [![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

> 精选的 **OpenClaw 教程**、**技能** 和 **使用案例** 集合，帮助你构建个人 AI 助理。

[OpenClaw](https://github.com/openclaw/openclaw) 是一个开源的 AI 助理框架，在本地机器上运行。支持多种 LLM 提供商、可扩展技能和跨平台消息通道。

｜[English](README.md)｜[简体中文](#)｜

## 📖 目录

1. [OpenClaw 是什么](#1-openclaw-是什么)
2. [快速开始](#2-快速开始)
3. [核心概念](#3-核心概念)
4. [官方技能](#4-官方技能)
5. [社区技能](#5-社区技能)
6. [使用案例](#6-使用案例)
7. [技能开发](#7-技能开发)
8. [多智能体路由](#8-多智能体路由)
9. [资源](#9-资源)
10. [贡献指南](#10-贡献指南)

---

## 1. OpenClaw 是什么

OpenClaw 是一个**自托管的网关**，将你喜欢的聊天应用——WhatsApp、Telegram、Discord、iMessage 等——连接到 AI 编程智能体如 Pi。你只需在自己的机器（或服务器）上运行一个 Gateway 进程，它就成为了你的消息应用和随时可用的 AI 助理之间的桥梁。

### 核心特性

| 特性 | 描述 |
|------|------|
| **多通道网关** | 单个 Gateway 进程支持 WhatsApp、Telegram、Discord、iMessage |
| **插件通道** | 通过扩展包添加 Mattermost 等 |
| **多智能体路由** | 按智能体、工作空间或发送者隔离会话 |
| **媒体支持** | 发送和接收图片、音频、文档 |
| **Web 控制台** | 浏览器仪表板，用于聊天、配置、会话和节点管理 |
| **移动节点** | 配对 iOS 和 Android 节点，支持 Canvas、摄像头/屏幕、语音工作流 |
| **自托管** | 在你的硬件上运行，规则由你定 |
| **开源** | MIT 许可证，社区驱动 |

### 工作原理

```
┌─────────────────┐    ┌─────────────┐    ┌──────────────────┐
│  聊天应用        │    │  Gateway    │    │  AI Agent (Pi)   │
│  - WhatsApp     │───▶│             │───▶│                  │
│  - Telegram     │    │  (端口      │    │  - Claude        │
│  - Discord      │    │   18789)    │    │  - GPT           │
│  - iMessage     │    │             │    │  - Gemini        │
└─────────────────┘    └─────────────┘    └──────────────────┘
                              │
                              ▼
                       ┌─────────────┐
                       │  Web UI     │
                       │  控制台     │
                       └─────────────┘
```

---

## 2. 快速开始

### 环境要求

- Node.js `>=22`
- pnpm（可选；从源码构建推荐）
- **推荐：** Brave Search API key 用于网页搜索

### 安装

**通过 npm：**
```bash
npm install -g openclaw@latest
```

**通过 curl（推荐）：**
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

**Windows (PowerShell)：**
```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

### 三步启动

```bash
# 1. 运行配置向导
openclaw onboard --install-daemon

# 2. 配置 WhatsApp（或其他通道）
openclaw channels login

# 3. 启动 Gateway
openclaw gateway --port 18789
```

### 控制台

Gateway 启动后打开浏览器控制台：

- 本地默认：http://127.0.0.1:18789/
- 远程访问：[Web surfaces](https://docs.openclaw.ai/web) 和 [Tailscale](https://docs.openclaw.ai/gateway/tailscale)

### 配置第一个通道

#### WhatsApp（扫码登录）

```bash
openclaw channels login
```

通过 WhatsApp → 设置 → 已关联的设备 扫描二维码。

#### Telegram / Discord

向导可以帮你写入 token/配置。手动配置：

- **Telegram：** 通过 [@BotFather](https://t.me/botfather) 创建机器人，获取 token
- **Discord：** 在 [开发者门户](https://discord.com/developers/applications) 创建机器人

### 私信安全

默认情况下，未知的私信会收到配对码。批准后机器人才能响应：

```bash
openclaw pairing list whatsapp
openclaw pairing approve whatsapp <code>
```

---

## 3. 核心概念

### 智能体工作空间

每个智能体有一个工作空间，包含：

```
~/.openclaw/workspace/
├── AGENTS.md      # 智能体行为规则
├── SOUL.md        # 个性和语气
├── USER.md        # 用户偏好
├── MEMORY.md      # 长期记忆
├── HEARTBEAT.md   # 周期性任务配置
├── TOOLS.md       # 本地工具笔记
├── memory/        # 每日日志
│   └── 2026-03-10.md
└── skills/        # 自定义技能
```

### 记忆系统

OpenClaw 有两层记忆系统：

- **每日笔记：** `memory/YYYY-MM-DD.md` — 当天发生的原始日志
- **长期记忆：** `MEMORY.md` — 精选的记忆（仅在主会话加载）

**重要：** 仅在与你的主人的直接对话中加载 `MEMORY.md`，不要在共享环境（Discord、群聊）中加载，以确保安全。

### 心跳

心跳是智能体收到轮询时运行的周期性检查。可用于：

- 检查邮件、日历、通知
- 更新记忆文件
- 后台维护任务
- 主动联络（谨慎使用）

在 `HEARTBEAT.md` 中配置：

```markdown
# 心跳任务

## 1. 邮件检查
- 检查紧急未读消息

## 2. 日历
- 查看未来 24 小时内的事件
```

### 技能

技能教智能体如何使用工具。每个技能是一个包含 `SKILL.md` 的文件夹：

```markdown
---
name: my-skill
description: 这个技能做什么
---

# 说明
如何使用这个技能...
```

技能位置（优先级从高到低）：
1. `<workspace>/skills` — 每个智能体的技能
2. `~/.openclaw/skills` — 共享技能
3. 内置技能 — 随 OpenClaw 发布

---

## 4. 官方技能

OpenClaw 自带 50+ 内置技能。

### 🤖 AI 与编程

| 技能 | 描述 |
|------|------|
| [coding-agent](https://github.com/openclaw/openclaw/tree/main/skills/coding-agent) | 将编程任务委托给 Codex、Claude Code 或 Pi 智能体 |
| [gh-issues](https://github.com/openclaw/openclaw/tree/main/skills/gh-issues) | 获取 GitHub issues，派生子智能体实现修复并创建 PR |
| [github](https://github.com/openclaw/openclaw/tree/main/skills/github) | 通过 `gh` CLI 进行 GitHub 操作：issues、PRs、CI |
| [summarize](https://github.com/openclaw/openclaw/tree/main/skills/summarize) | 文本摘要 |
| [gemini](https://github.com/openclaw/openclaw/tree/main/skills/gemini) | 使用 Gemini CLI 进行编程辅助 |

### 📝 效率工具

| 技能 | 描述 |
|------|------|
| [notion](https://github.com/openclaw/openclaw/tree/main/skills/notion) | Notion 集成 |
| [obsidian](https://github.com/openclaw/openclaw/tree/main/skills/obsidian) | Obsidian 笔记 |
| [apple-notes](https://github.com/openclaw/openclaw/tree/main/skills/apple-notes) | Apple Notes 集成 |
| [apple-reminders](https://github.com/openclaw/openclaw/tree/main/skills/apple-reminders) | Apple 提醒事项集成 |
| [things-mac](https://github.com/openclaw/openclaw/tree/main/skills/things-mac) | Things 3 任务管理 |
| [trello](https://github.com/openclaw/openclaw/tree/main/skills/trello) | Trello 看板管理 |
| [bear-notes](https://github.com/openclaw/openclaw/tree/main/skills/bear-notes) | Bear 笔记集成 |

### 💬 消息通道

| 技能 | 描述 |
|------|------|
| [discord](https://github.com/openclaw/openclaw/tree/main/skills/discord) | Discord 机器人集成 |
| [slack](https://github.com/openclaw/openclaw/tree/main/skills/slack) | Slack 机器人集成 |
| [imsg](https://github.com/openclaw/openclaw/tree/main/skills/imsg) | iMessage 集成 |
| [bluebubbles](https://github.com/openclaw/openclaw/tree/main/skills/bluebubbles) | BlueBubbles iMessage 服务器 |

### 🔧 实用工具

| 技能 | 描述 |
|------|------|
| [weather](https://github.com/openclaw/openclaw/tree/main/skills/weather) | 通过 wttr.in 或 Open-Meteo 获取天气预报 |
| [tmux](https://github.com/openclaw/openclaw/tree/main/skills/tmux) | 远程控制 tmux 会话 |
| [video-frames](https://github.com/openclaw/openclaw/tree/main/skills/video-frames) | 使用 ffmpeg 从视频提取帧 |
| [session-logs](https://github.com/openclaw/openclaw/tree/main/skills/session-logs) | 使用 jq 搜索和分析会话日志 |
| [skill-creator](https://github.com/openclaw/openclaw/tree/main/skills/skill-creator) | 创建和打包新技能 |
| [healthcheck](https://github.com/openclaw/openclaw/tree/main/skills/healthcheck) | 主机安全加固和风险容忍配置 |

### 🎨 媒体与生成

| 技能 | 描述 |
|------|------|
| [openai-image-gen](https://github.com/openclaw/openclaw/tree/main/skills/openai-image-gen) | DALL-E 图像生成 |
| [openai-whisper](https://github.com/openclaw/openclaw/tree/main/skills/openai-whisper) | 本地 Whisper 转录 |
| [openai-whisper-api](https://github.com/openclaw/openclaw/tree/main/skills/openai-whisper-api) | OpenAI Whisper API 转录 |
| [sag](https://github.com/openclaw/openclaw/tree/main/skills/sag) | ElevenLabs TTS 集成 |
| [sherpa-onnx-tts](https://github.com/openclaw/openclaw/tree/main/skills/sherpa-onnx-tts) | 使用 Sherpa-ONNX 的本地 TTS |

### 🏠 智能家居

| 技能 | 描述 |
|------|------|
| [sonoscli](https://github.com/openclaw/openclaw/tree/main/skills/sonoscli) | Sonos 音箱控制 |
| [openhue](https://github.com/openclaw/openclaw/tree/main/skills/openhue) | Philips Hue 控制 |
| [spotify-player](https://github.com/openclaw/openclaw/tree/main/skills/spotify-player) | Spotify 播放控制 |

### 🔒 安全与 DevOps

| 技能 | 描述 |
|------|------|
| [1password](https://github.com/openclaw/openclaw/tree/main/skills/1password) | 1Password 集成 |

---

## 5. 社区技能

社区贡献的专项技能。

### 📣 内容与营销

| 技能 | 描述 | 作者 |
|------|------|------|
| [content-promotion](https://github.com/ZeroLu/awesome-openclaw/blob/main/skills/content-promotion/SKILL.md) | 多平台内容推广工作流（知乎、掘金、Dev.to、Product Hunt 等） | [@ZeroLu](https://github.com/ZeroLu) |
| [ultimate-ai-media-generator](https://github.com/ZeroLu/awesome-openclaw/blob/main/skills/ultimate-ai-media-generator/SKILL.md) | CyberBara Public API v1 图像/视频生成任务 | [@ZeroLu](https://github.com/ZeroLu) |

### 📚 飞书集成

OpenClaw 内置飞书（Lark）支持：

- **文档：** 读取、写入、追加、创建表格、上传图片
- **多维表格：** 记录和字段的 CRUD 操作
- **云盘：** 文件和文件夹管理
- **知识库：** 知识库导航
- **聊天：** 获取聊天信息和成员列表

---

## 6. 使用案例

真实世界中使用 OpenClaw 的案例。

### 6.1. 内容创作者助理

自动化内容创作和跨平台发布：

```
用户：检查我的 X 书签，推荐可以转发到即刻的内容
```

**工作流：**
1. 智能体通过浏览器打开 X 书签
2. 抓取最近书签的元数据（播放量、点赞数）
3. 按互动筛选（播放量 > 100K，点赞 > 1000）
4. 将内容翻译成中文
5. 下载媒体（视频/图片）
6. 将推荐写入 `daily_recommendations.md`
7. 等待用户确认后发布

**相关技能：** `browser`, `web_fetch`, `video-frames`

### 6.2. 开发者效率

**代码审查：**
```
用户：审查 openclaw/openclaw 最新的 PR
```

智能体：
1. 使用 `gh` CLI 获取 PR 详情
2. 阅读变更文件
3. 分析代码质量，提出改进建议
4. 通过 `gh pr comment` 发布审查评论

**Issue 管理：**
```
用户：创建一个 PR 来修复 issue #123
```

智能体：
1. 阅读 issue 详情
2. 探索代码库理解上下文
3. 实现修复
4. 创建分支、提交、推送
5. 打开 PR 并附上描述

**相关技能：** `github`, `coding-agent`, `gh-issues`

### 6.3. 个人知识管理

**Obsidian 集成：**
```
用户：我上个月写了什么关于 AI 智能体的内容？
```

智能体：
1. 在 Obsidian 库中搜索相关笔记
2. 总结发现
3. 链接到具体笔记

**会话记忆：**
```
用户：我们之前讨论的服务器迁移是什么？
```

智能体：
1. 通过 `memory_search` 搜索会话日志
2. 从 `MEMORY.md` 获取相关上下文
3. 提供带引用的总结

**相关技能：** `obsidian`, `session-logs`, 记忆系统

### 6.4. 智能家居自动化

**语音控制：**
```
用户：在所有音箱上播报开饭时间
```

智能体：
1. 使用 TTS 生成播报
2. 通过 `sonoscli` 在 Sonos 音箱上播放

**场景控制：**
```
用户：设置电影模式
```

智能体：
1. 通过 `openhue` 调暗灯光
2. 暂停 Spotify 音乐
3. 通过 TTS 播报

**相关技能：** `sonoscli`, `openhue`, `sag`, `spotify-player`

### 6.5. 多智能体路由

为不同场景分离智能体：

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

## 7. 技能开发

### 创建新技能

1. **创建技能目录：**
```bash
mkdir -p ~/.openclaw/skills/my-skill
```

2. **创建 `SKILL.md`：**
```markdown
---
name: my-skill
description: 这个技能做什么。用于自动技能激活。
---

# 我的技能

## 功能说明
技能的详细描述。

## 使用方法
分步说明。

## 工具
这个技能提供或使用的工具列表。

## 配置
所需的 API key 或设置。
```

3. **添加可选文件：**
```
my-skill/
├── SKILL.md          # 必需
├── skill.json        # 可选：元数据
├── scripts/          # 可选：shell 脚本
└── assets/           # 可选：图片、模板
```

### 技能元数据

frontmatter 支持以下字段：

```yaml
---
name: skill-name
description: 简短描述（用于激活）
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

### 过滤规则

技能在加载时根据以下条件过滤：

- `requires.bins` — 必须存在的 CLI 二进制文件
- `requires.env` — 必需的环境变量
- `requires.config` — 必须为真的配置路径
- `os` — 平台限制（`darwin`、`linux`、`win32`）

### 最佳实践

1. **保持 `SKILL.md` 简洁** — 专注于可执行的说明
2. **使用清晰的触发器** — 描述决定自动激活
3. **记录依赖** — API key、配置、依赖项
4. **跨提供商测试** — 确保与不同 LLM 的兼容性
5. **安全第一** — 不要在 prompt 或日志中暴露敏感信息

---

## 8. 多智能体路由

### 什么是多智能体？

每个**智能体**是一个完全隔离的"大脑"，拥有自己的：

- **工作空间** — 文件、AGENTS.md、SOUL.md、USER.md
- **状态目录** — 认证配置、模型注册
- **会话存储** — 聊天历史 + 路由状态

### 使用场景

1. **多人共享服务器** — 每个人有自己的智能体
2. **多角色** — 工作助理 vs 个人助理
3. **模型路由** — 快速模型用于聊天，强大模型用于深度工作
4. **沙箱隔离** — 限制某些智能体的工具

### 示例：两个 WhatsApp 号码，两个智能体

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

### 路由优先级

绑定是确定性的，最具体的匹配优先：

1. `peer` 匹配（精确的 DM/群组/频道 ID）
2. `guildId`（Discord）
3. `teamId`（Slack）
4. `accountId` 匹配
5. 通道级别匹配
6. 默认智能体

### 添加智能体

```bash
# 交互式
openclaw agents add work

# 非交互式
openclaw agents add work \
  --workspace ~/.openclaw/workspace-work \
  --model anthropic/claude-opus-4-5 \
  --bind whatsapp:biz \
  --non-interactive
```

---

## 9. 资源

### 官方资源

- 🌐 [OpenClaw 官网](https://openclaw.ai)
- 📚 [文档](https://docs.openclaw.ai)
- 📖 [中文文档](https://docs.openclaw.ai/zh-CN/)
- 💻 [GitHub 仓库](https://github.com/openclaw/openclaw)
- 💬 [Discord 社区](https://discord.com/invite/clawd)
- 🛒 [ClawHub](https://clawhub.com) — 发现和分享技能

### 文档中心

| 中心 | 描述 |
|------|------|
| [快速开始](https://docs.openclaw.ai/start/getting-started) | 从零到第一条消息 |
| [配置](https://docs.openclaw.ai/gateway/configuration) | Gateway 设置、token、提供商 |
| [通道](https://docs.openclaw.ai/channels) | WhatsApp、Telegram、Discord、iMessage 设置 |
| [节点](https://docs.openclaw.ai/nodes) | iOS 和 Android 移动节点 |
| [技能](https://docs.openclaw.ai/tools/skills) | 技能开发和配置 |
| [安全](https://docs.openclaw.ai/gateway/security) | Token、白名单、安全控制 |

### 相关项目

- [awesome-seedance](https://github.com/ZeroLu/awesome-seedance) — Seedance 2.0 提示词合集
- [awesome-nanobanana-pro](https://github.com/ZeroLu/awesome-nanobanana-pro) — Nano Banana Pro 提示词
- [CyberBara](https://cyberbara.com) — 统一 AI 图像与视频生成平台

---

## 10. 贡献指南

欢迎贡献！如果你有：

- **新技能**想分享
- **使用案例**想记录
- **教程**想添加
- 对现有内容的**改进建议**

请提交 Pull Request。

### 指南

1. 遵循现有格式和风格
2. 包含清晰的描述和示例
3. 适当时链接到原始来源
4. 提交前测试所有代码示例

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

**赞助者**：本仓库由 [Zero君](https://x.com/zerolu_eth) 维护。欢迎体验 [CyberBara](https://cyberbara.com)，统一 AI 图像与视频生成平台，集成 Sora 2、Kling 2.6、Seedance 2.0 和 Veo 3.1。
