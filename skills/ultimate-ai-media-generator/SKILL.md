---
name: ultimate-ai-media-generator
description: Generate and monitor CyberBara Public API v1 image and video tasks end-to-end. Use when work involves CyberBara `/api/v1` endpoints for listing models, uploading reference images, quoting credits, creating generation tasks, polling task status, or checking credits balance and usage.
---

# Ultimate AI Media Generator Skill

通过 CyberBara Public API 生成图像和视频的技能。

## 概述

使用此技能可靠地调用 CyberBara API，创建图像/视频生成任务，并返回最终媒体 URL。

## 功能

- **模型发现** - 列出可用的图像和视频模型
- **图片上传** - 上传参考图片用于生成任务
- **积分估算** - 在创建任务前估算所需积分
- **图像生成** - 创建图像生成任务
- **视频生成** - 创建视频生成任务
- **任务轮询** - 等待任务完成并获取结果
- **余额查询** - 检查积分余额和使用记录

## 支持的模型

### 视频模型
- Sora 2
- Kling 2.6
- Seedance 2.0
- Veo 3.1

### 图像模型
- Nano Banana Pro

## 快速开始

### 设置 API Key

```bash
python3 scripts/cyberbara_api.py setup-api-key "<your-api-key>"
```

API Key 获取地址：https://cyberbara.com/settings/apikeys

### 生成视频

```bash
python3 scripts/cyberbara_api.py generate-video --json '{
  "model": "sora-2",
  "prompt": "A calm drone shot over snowy mountains at sunrise",
  "scene": "text-to-video",
  "options": {"duration": "10", "resolution": "standard"}
}'
```

### 生成图像

```bash
python3 scripts/cyberbara_api.py generate-image --json '{
  "model": "nano-banana-pro",
  "prompt": "A cinematic portrait under neon rain",
  "scene": "text-to-image",
  "options": {"resolution": "1k"}
}'
```

## 核心规则

### 积分确认 ⚠️

每次生成任务前，技能会自动估算所需积分并请求用户确认。

### 自动保存

生成的媒体文件默认保存到 `./media_outputs/` 目录并自动打开。

## 安装

完整技能位于 OpenClaw workspace：

```bash
# 技能目录
~/.openclaw/skills/ultimate-ai-media-generator/
```

参考 [OpenClaw 技能开发文档](https://docs.openclaw.ai/tools/skills) 了解如何安装和使用技能。

## 相关链接

- [CyberBara 官网](https://cyberbara.com)
- [API Key 设置](https://cyberbara.com/settings/apikeys)
