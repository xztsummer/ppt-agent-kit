# PPT Master — AI 生成原生可编辑 PowerPoint 的 Agent Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/downloads/)
[![Skill Version](https://img.shields.io/badge/skill%20version-6.7.2-green.svg)](./SKILL.md)

> **English TL;DR** — PPT Master is an agentic-skill workflow that turns source material into
> **natively editable** PowerPoint files (real DrawingML shapes, charts, tables, formulas and
> master/layout inheritance — not screenshots). It runs inside any agent-capable AI tool
> (Claude Code, Cursor, Zed, Codex CLI, …), works fully locally, and ships with a rich
> template asset library. This repo is the extracted skill package; see
> [Relationship to upstream](#与上游仓库的关系) for attribution.

丢进原材料（PDF / Word / 网页 / 主题），拿回一份**带完整 PowerPoint 行为的成品**：原生形状、连接符、可编辑图表与表格、OMML 公式、母版与版式继承、页间转场、演讲者备注一键合成旁白音频——点开任意元素都是原生 PowerPoint 对象，可以继续编辑。

它不是应用或服务，而是一套在具备 Agent 能力的 AI 工具里运行的**工作流技能包**（skill）：你在对话框里说「用这份 PDF 做一份 PPT」，它就按流程在本机生成并导出 `.pptx`。

## 五条工作路线

| 路线 | 用途 |
|---|---|
| **Generate PPTX** | 从材料 / 主题生成全新 deck；Default 走策略师 + 确认流程，Quick（显式「快速生成」）一次性直出 |
| **Beautify** | 对已有 PPTX 做 1:1 美化重构，不改内容结构 |
| **Image to PPTX** | 页面图片重建：文字原生恢复、低清图形重建为可编辑对象 |
| **Create Template** | 从 PPTX / 图片 / 文档 / 品牌资产提炼可复用的 Brand / Style / Layout / Deck 模板工作区 |
| **Edit Native PPTX** | 「套模板」：新内容填入你已有的 `.pptx`，未改动页面逐字节保留 |

## 核心能力

- **原生对象模型** — 187 种 Office 预设形状、布尔合并、连接符与自由曲线；图表 / 表格默认导出为可逐形状编辑的 DrawingML，可选 `--native-charts-and-tables` 升级为带数据源的 PowerPoint 原生 Chart / Table 对象；LaTeX 公式编译为 PowerPoint 2010+ 可编辑 OMML；模板路线产出真正的母版 / 版式（`p:sldMaster` / `p:sldLayout`）继承。
- **质量门禁** — 文本宽度预校准、SVG 质量检查器、视觉审查、导出 postflight 报告，多道闸口守住排版与结构质量。
- **图片管线** — 15+ AI 生图后端（OpenAI / Gemini / 通义 / 智谱 / 火山引擎 / SiliconFlow / fal / Replicate …），网络图片搜索零配置可用（Openverse / Wikimedia），配置 Pexels / Pixabay 后质量更稳；图片许可自动处理，需署名图片自动加注。
- **旁白音频** — 默认 `edge-tts` 无需任何 Key；可选 ElevenLabs / MiniMax / 通义 / CosyVoice 云端旁白，四家均支持复刻音色 `voice_id`。
- **模板资产库** — 23 个品牌预设、16 种视觉风格、9 套版式、5 个成品 deck 模板、33 个图表模板、12000+ 图标（含第三方许可声明）、191 个音效文件。
- **本地运行** — 除与 AI 模型的对话外，全流程在你的电脑上完成，数据不出本地。

## 仓库结构

本仓库即 skill 技能包本体（`SKILL.md` 位于仓库根目录）：

```
├── SKILL.md            # Skill 入口：全局执行纪律 + 路由选择
├── workflows/          # 5 条路线的流程权威 + 阶段 / profile（23 篇）
├── references/         # 角色核心与技术参考（117 篇）
├── scripts/            # 工具链：source→md、项目初始化、SVG 检查/导出、
│                       #   生图、图搜、TTS、模板物化等（303 个 Python 脚本）
├── templates/          # 品牌 / 风格 / 版式 / deck / 图表 / 图标 / 音效资产库
├── .env.example        # API Key 配置模板（全部为占位注释）
└── requirements.txt    # 可选依赖清单
```

## 快速开始

### 1. 前置条件

- **Python 3.10+**（Windows 安装时记得勾选 *Add to PATH*）
- 任一具备 Agent 能力的 AI 工具（可读写文件、执行命令、多轮对话）：Claude Code、Cursor、Zed、Codex CLI、Windsurf 等

### 2. 获取并安装

```bash
git clone https://github.com/xztsummer/ppt-master.git
cd ppt-master
pip install -r requirements.txt
```

或直接下载 ZIP 解压。也可以把整个目录复制进你所用工具的 skills 目录（如 `~/.agents/skills/ppt-master`），skill 从任意绝对路径运行均可。

### 3. 配置 API Key（可选）

> ⚠️ **安全说明**：仓库不含任何 `.env`（已列入 `.gitignore`）。本地配置请先复制模板：
> `cp .env.example .env`，再取消注释并填入你自己的 key——真实 key 不会被提交进仓库。完整配置示例见 [`.env.example`](./.env.example)。

配置通过 `.env` 完成，读取顺序：当前进程环境变量 → `./.env`（当前目录）→ skill 目录 `.env` → `~/.ppt-master/.env`（首个存在的文件生效，不合并）。

| 用途 | 变量 | 说明 |
|---|---|---|
| AI 生图 | `IMAGE_BACKEND` + 对应 `*_API_KEY` | 后端见 `python scripts/image_gen.py --list-backends` |
| 网络图片搜索 | `PEXELS_API_KEY` / `PIXABAY_API_KEY` | 均可免费申请；不配置则用零配置的 Openverse / Wikimedia |
| 旁白音频 | `ELEVENLABS_API_KEY` 等 | 默认 `edge-tts` 无需任何 Key |

### 4. 开始创作

在 AI 工具里打开仓库文件夹（IDE 用 *文件 → 打开文件夹*，CLI 先 `cd` 再启动），把材料放进 `projects/`，然后在聊天框里说：

```
你：请用 projects/q3-report/sources/report.pdf 这份文件生成一份 PPT
```

```
你：用这份材料快速生成一份 5 页 PPT，不用跟我确认      ← Quick 模式
你：我有一份做好的 pptx，请套用它的模板填充新内容       ← Edit Native PPTX
```

AI 全程处理：内容分析、视觉设计、SVG 生成、质量检查、PPTX 导出。若 AI 迷失上下文，让它先读 `SKILL.md`。

## 与上游仓库的关系

本仓库是从 [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) **v6.7.2（MIT License）** 提取的纯 skill 技能包，并在本地定制基础上再发布（含新增的 `中国电子云` deck 模板等）。

感谢原作者 [Hugo He](https://github.com/hugohe3) 的开源贡献。上游完整仓库还包含用户文档（快速入门 / FAQ / Windows 安装指南 / 技术设计）、示例工程与持续更新，推荐访问：

- 官方仓库：<https://github.com/hugohe3/ppt-master>
- 在线示例：<https://hugohe3.github.io/ppt-master-examples/>

## 许可证

[MIT License](./LICENSE) — Copyright (c) 2025-2026 Hugo He。本仓库为 MIT 许可下的再发布，依许可要求完整保留原版权声明与 `LICENSE` / `SPONSORS.md` / `SPONSORS_CN.md` 署名文件（skill 内置的完整性校验亦会验证这些文件）。
