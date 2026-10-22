---
deck_id: 中国电子云
kind: deck
category: brand
summary: 中国电子云品牌对外汇报、方案宣讲与内部评审，覆盖封面、目录、章节、开放内容与封底五页；采用克制的科技蓝视觉。
keywords: [中国电子云, 中电云, 简版, 科技蓝, 企业汇报]
primary_color: "#0058FF"
canvas_format: ppt169
canvas_width: 1280
canvas_height: 720
canvas_viewbox: "0 0 1280 720"
source_canvas_width: 1280
source_canvas_height: 720
source_viewbox: "0 0 1280 720"
replication_mode: fidelity
native_structure_mode: structured
page_count: 5
placeholders:
  01_cover: ["{{TITLE}}", "{{SUBTITLE}}", "{{AUTHOR}}", "{{DATE}}"]
  02_toc: ["{{TOC_ITEM_1_TITLE}}", "{{TOC_ITEM_2_TITLE}}", "{{TOC_ITEM_3_TITLE}}", "{{TOC_ITEM_4_TITLE}}", "{{PAGE_NUM}}"]
  03_chapter: ["{{CHAPTER_NUM}}", "{{CHAPTER_TITLE}}"]
  04_content: ["{{PAGE_TITLE}}", "{{PAGE_SUBTITLE}}", "{{CONTENT_AREA}}", "{{PAGE_NUM}}"]
  05_ending: ["{{THANK_YOU}}", "{{CONTACT_INFO}}"]
---

# 中国电子云 — Design Specification

## I. Template Overview

| Application context | Definition |
| --- | --- |
| Recurring presentation family | 中国电子云品牌对外汇报、产品与解决方案宣讲、生态合作交流与内部评审 |
| Intended audiences and outcomes | 面向政企客户决策者、生态合作伙伴与内部评审者；帮助受众快速建立品牌认知、理解方案要点并形成判断与下一步 |
| Delivery and reading assumptions | 以会议讲解为主，同时需要会后流转与独立阅读；页面保留关键结论与必要证据，不依赖口头说明也能辨认主题 |
| Representative narrative/page roles | 当前原型覆盖封面、目录、章节、开放内容与结束语；具体选页、重复、顺序与内容处理由当前项目的 Strategist 根据材料决定 |

- 本模板覆盖封面、目录、章节、开放内容与封底五个可复用页面角色，不含卡片网格、流程逻辑与数据指标类内容变体页。
- 视觉基调为品牌科技蓝（#0058FF）深蓝封面/章节/封底与白底浅色内容页的混合模式；强调色克制，只赋重点信息；整体可辨识来自品牌蓝底图、白/蓝双色 logo 体系与蓝色渐变图形语言。
- 结构上分为两个可复用 Master 家族：中国电子云品牌服务封面、章节页与封底（Master 携带全幅品牌深蓝背景图），中国电子云内容服务目录页与内容页（白色 Master 背景）；它们按视觉体系分工，不是按单个 Layout 拆分出的重复 Master。

## II. Color Scheme

| Role | Color | Application |
| --- | --- | --- |
| 强调蓝 | #0058FF | 页标题、强调色块、章节号、目录编号、内容页左上强调条 |
| 一级文本 | #090909 | 内容页副标题与正文 |
| 二级文本 | #464646 | 目录项 |
| 页码灰 | #C2C2C2 | 页码与禁用文本 |
| 白 | #FFFFFF | 深蓝页面反白文字、目录页底色、内容页底色 |

- 源模板规范页明确要求：颜色统一点选主题色、浅色风格为主、忌大面积高纯度色、强调色只给重点信息、文字与背景保持较大对比度。

## III. Typography

| Role | Font stack | Application |
| --- | --- | --- |
| 中文标题与正文 | `Microsoft YaHei, PingFang SC, Arial, sans-serif` | 标题、副标题、正文、目录项 |
| 数字与英文 | `Arial, Microsoft YaHei, sans-serif` | 章节号、日期、页码、CONTENTS/THANKS |

- 源规范：标题 24pt、内文 12–20pt，密集阅读内容可小于 12 号；本模板原型按 1280×720 画布以 px 落位（页标题 32、内容页副标题 21.33、封面主标题 80、封面副标题 53.33、章节号 117.33）。

## IV. Signature Design Elements

- 双 Master 分工：`cec_cloud_brand_master`（中国电子云品牌）承载全幅品牌深蓝背景图，服务封面/章节/封底（白字反白）；`cec_cloud_content_master`（中国电子云内容）承载白色背景，服务目录页与内容页。
- 内容页页眉语法：左上蓝色强调条（32.53×34）+ 蓝色 32px 加粗页标题 + 全宽副标题行 + 右上蓝色 logo；页码位于右下角灰色 14.67px。
- 双色 logo 体系：深蓝页用白色 logo（封面左上、章节右上、封底居中），浅色页用蓝色 logo（目录与内容页右上）。
- 标题与正文保持左对齐；仅章节号、目录编号、封面居中 THANKS 等短焦点内容使用居中或右对齐（源模板语法内的既定例外）。

## V. Page Roster

| File | Master | Layout key | PowerPoint picker name | Visual character | Reusable slots |
| --- | --- | --- | --- | --- | --- |
| `01_cover.svg` | 中国电子云品牌 | cover | 封面-主副标题 | 品牌深蓝底、右侧品牌插画、左上白色 logo、白色标题簇 | 主标题、副标题、汇报人、日期 |
| `02_toc.svg` | 中国电子云内容 | toc | 目录页 | 白底、左侧品牌蓝竖版面板 + CONTENTS、右侧四行蓝色编号目录 | 四个目录项、页码 |
| `03_chapter.svg` | 中国电子云品牌 | chapter | 章节页 | 全幅品牌蓝底、右侧白色大号章节数字 + 细分隔线 + 章节标题、右上白色 logo | 章节号、章节标题 |
| `04_content.svg` | 中国电子云内容 | content | 内容页-浅色 | 白底、蓝色页标题页眉、全幅开放内容区 | 页标题、副标题、内容对象、页码 |
| `05_ending.svg` | 中国电子云品牌 | ending | 封底 | 品牌深蓝底、居中反白 THANKS 与白色 logo、下方联系信息 | 结束语、联系信息 |

## VI. Assets

| File | Dimensions | Intended usage |
| --- | --- | --- |
| `brand_bg_blue.png` | 2000×1125 | Master 全幅品牌深蓝背景（封面/章节/封底显示） |
| `cover_illustration.png` | 1094×800 | 封面右侧品牌插画 |
| `logo_white.png` | 497×110 | 封面左上白色 logo |
| `toc_side_panel.png` | 637×1133 | 目录页左侧品牌蓝竖版面板 |
| `logo_blue.png` | 315×69 | 目录页与内容页右上蓝色 logo |
| `chapter_bg.png` | 2007×1127 | 章节页全幅品牌蓝底图 |
| `logo_white_small.png` | 315×69 | 章节页右上白色 logo |
| `logo_ending.png` | 439×97 | 封底居中白色 logo |

## VII. Placeholder Overrides

- 本模板五页均沿用规范占位词汇（`{{TITLE}}`、`{{CHAPTER_NUM}}`、`{{CONTENT_AREA}}` 等），已在 frontmatter `placeholders:` 声明为模板契约，无自定义槽位词汇。
- 目录页采用规范索引形式 `{{TOC_ITEM_N_TITLE}}`，行数固定为四行；更多条目由下游项目按需扩展版式，不在本模板内预置。
