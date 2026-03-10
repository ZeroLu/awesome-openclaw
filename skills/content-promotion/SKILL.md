---
name: content-promotion
description: Multi-platform content promotion workflow for open source projects, articles, and products. Use when user asks to promote/publish content to multiple platforms (知乎, 掘金, Dev.to, 开源中国, Product Hunt, HelloGitHub, 阮一峰 Weekly, etc.). Handles account management, content adaptation, publishing workflow, and screenshot confirmation.
---

# Content Promotion Skill

自动化多平台内容推广流程，支持开源项目、文章、产品推广。

## 核心规则

### 发布前必须确认 ⚠️

**任何内容发布到公开平台前，必须截图给用户确认！**

正确流程：
1. 准备好内容 → 截图给用户看 → 用户说"发送"/"发布" → 点击发送
2. 错误做法：准备好内容 → 直接点击发送

## 推广流程

### Step 1: 收集推广信息

向用户确认：
- 推广内容类型：开源项目 / 文章 / 产品
- GitHub 链接（如有）
- 封面图链接（如有）
- 特殊要求
- 目标平台列表

### Step 2: 准备推广内容

根据内容类型准备文案，适应各平台风格。

### Step 3: 平台发布

按用户指定的平台顺序发布。每个平台：
1. 检查是否已登录
2. 如需登录，截图通知用户
3. 填写内容
4. **截图预览给用户确认**
5. 用户确认后发布
6. 记录发布链接

### Step 4: 汇总报告

发布完成后，生成汇总表格。

## 支持平台

- 知乎
- 掘金
- Dev.to
- 开源中国
- Product Hunt
- HelloGitHub
- 阮一峰 Weekly

## 安装

完整技能位于 OpenClaw workspace：

```bash
# 技能目录
~/.openclaw/skills/content-promotion/
```

参考 [OpenClaw 技能开发文档](https://docs.openclaw.ai/tools/skills) 了解如何安装和使用技能。
