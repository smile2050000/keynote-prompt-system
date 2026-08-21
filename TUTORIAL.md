# Keynote Prompt System 使用教程

## 1. 这是什么

`keynote-prompt-system` 是一个 PPT 视觉规划 Skill。它把一份 PPT 需求整理成：

```text
PPT 需求 → 内容简报 → Storyboard → 全局视觉规则 → 逐页 Prompt → 图片生成 → QA → PPTX 预览
```

它负责梳理叙事、准确文案、页面任务、整套视觉风格、逐页图片 Prompt、Reference 路由和 QA 规则。

它不绑定某一个图片生成平台。MCP 只是可选的自动生图通道；没有 MCP 也可以完整使用规划和 Prompt 生成能力。

## 2. 两种使用方式

### 有 MCP

```text
Skill 规划 → MCP 健康测试 → 自动生成图片 → Contact Sheet → QA → PPTX
```

### 没有 MCP

```text
Skill 规划 → 生成 Prompt Pack → 复制到外部图片平台 → 下载图片 → Contact Sheet / QA → PPTX
```

外部平台可以是 ChatGPT 图片、Midjourney、即梦、豆包、可灵、通义万相、Stable Diffusion 等。

> Skill 负责把需求想清楚、写清楚；图片平台负责生成图片。

## 3. 安装

### 在 Codex 中

将项目放入 Codex Skill 目录：

```text
~/.codex/skills/keynote-prompt-system/
```

目录至少包含：

```text
keynote-prompt-system/
├── SKILL.md
├── agents/openai.yaml
└── references/
```

当前项目目录：

```text
/Users/smile/Documents/ChatGPT/image2 版本/keynote-prompt-system-v0.9
```

调用：

```text
使用 $keynote-prompt-system。
```

### 没有 Codex 时

图片平台不需要安装这个 Skill。让有 Codex 的人生成 `content-brief.md`、`storyboard.md`、`global-visual-contract.md` 和 `prompt-pack.md`，再把每页 Prompt 复制到图片平台执行。

## 4. 完整流程产物

| 文件 | 作用 |
|---|---|
| `content-brief.md` | 产品事实、准确文案、叙事目标和数据来源 |
| `storyboard.md` | 每页内容任务、观众问题、证据类型、主视觉载体、空间语法和风险 |
| `global-visual-contract.md` | 全套共享视觉规则和唯一 `style_id` |
| `prompt-pack.md` | 每页完整 Prompt、Reference、调用方式和质量约束 |
| `execution-log.md` | 真实调用、Provider、Model、参数、输出和失败记录 |
| `qa/contact-sheet-pass-01.png` | 首轮全部页面缩略图 |
| `qa/qa.md` | 明显问题页和修正动作 |
| `qa/contact-sheet-final.png` | 修正后的整套复查图 |
| `deck-preview.pptx` | 可选下游产物，由 `slides` / `ppt` Skill 封装 |

## 5. 推荐调用话术

### 只做规划

```text
使用 $keynote-prompt-system。

请根据以下 PPT 需求，先只做规划，不生成图片：
[粘贴需求或提供文件路径]

请输出：
- content-brief.md
- storyboard.md
- global-visual-contract.md
- prompt-pack.md

要求：
- 从 references/style-presets.md 选择已有风格；
- 不创造新的 style_id；
- 不猜测缺失的数据、文案、功能或品牌信息；
- 产品页记录明确的 Reference；
- 每页记录 Page Type、核心信息和特殊风险；
- 完成后等待我确认。
```

### 只要 Prompt

```text
只生成 prompt-pack.md。
不要调用 MCP，不生成图片，不生成 PPTX。
Prompt 必须可以直接复制到外部图片平台使用。
每页写清楚：准确文字、Page Type、Reference、上传方式、比例、尺寸、Must Preserve、Avoid 和生成后检查项。
```

### 有 MCP 时生成

```text
开始使用 image_mcp_demo 生成。

要求：
- 先做最小健康测试；
- 成功后生成正式页面；
- 产品页使用 edit_image；
- 无产品页使用 generate_image；
- 记录 Provider、Model、尺寸、Reference 和输出路径；
- 生成 Contact Sheet 和 PPTX；
- 失败时保留真实错误，不切换其他通道。
```

### 没有 MCP 时生成 Prompt

```text
我没有接入 MCP。
请不要调用任何生图工具，只输出可以复制到外部图片平台的完整 Prompt。

请按页面分别输出 Page 01–05 Prompt，并同时列出：
- 需要上传的 Reference 及用途；
- 推荐模式：文生图 / 图生图；
- 比例和尺寸；
- 生成后检查项。
```

## 6. 外部图片平台的用法

### 无产品 Reference

选择文生图，粘贴对应页面完整 Prompt。

```text
比例：16:9
尺寸：平台支持的 2K 或 2048×1152
数量：1 张
```

### 有产品 Reference

选择图生图或参考图生成，上传产品图，再粘贴完整 Prompt。

```text
产品图只用于识别产品身份、结构和材质；不复制参考图背景，不把参考图直接拼入最终页面。
```

### 多 Reference

```text
Reference 1：上一页最终图
用途：只继承布局、摄影尺度和视觉风格

Reference 2：产品图
用途：只识别产品身份、结构和材质

禁止：把两张图拼贴到最终画面，复制参考图文字或错误容器。
```

如果平台不支持多 Reference，先用布局图生成结构，再用产品图做第二次图生图修正。

## 7. 只要某个流程时的话术

### 只要内容规划

```text
只生成 content-brief.md。
不要生成视觉风格、Prompt 或图片。
```

### 只要 Storyboard

```text
只生成 storyboard.md。
每页记录 Core Message、Audience Memory、Page Type、Visual Strength 和 Special Risk。
不要调用生图工具。
```

### 只要视觉风格

```text
只生成 global-visual-contract.md。
请从 references/style-presets.md 选择已有风格，不要创造新的风格名称。
```

### 只生成一页 Prompt

```text
只编译 Page 03 的完整 Prompt。
同时列出 Reference、上传方式、生成模式、比例、尺寸和检查项。
```

### 只生成一页图片

```text
只生成第 01 页，不生成其他页面。
使用 prompt-pack.md 中的完整 Prompt 和指定 Reference，保持准确文字、产品身份和输出尺寸，不覆盖旧版本。
```

### 只做 Contact Sheet / QA

```text
以下图片已经生成，请不要重新生成：
[图片路径列表]

请输出 qa/contact-sheet-pass-01.png 和 qa/qa.md。
只检查文字、数字、产品身份、裁切、标题层级、跨页风格、多图质量和明显容器错误。
```

### 只封装 PPTX

```text
这些整页图片已经确认，请只封装图片版 PPTX。
每页一张整页图片铺满，不添加 PowerPoint 原生文字，保持 16:9，检查页数和文件是否可打开，输出 deck-preview.pptx。
```

### 只修正一页

```text
只修正第 05 页，不重跑整套。
保持全局 Style Preset、准确文字、产品 Reference、比例和输出尺寸。
只改变：[一个明确问题]
使用新输出文件名，不覆盖旧图，并记录到 execution-log.md。
```

## 8. 风格选择

唯一入口：

```text
references/style-presets.md
```

| style_id | 适用场景 | 状态 |
|---|---|---|
| `neutral-modern-home` | 家用智能硬件、家庭陪伴、桌面智能屏 | `validated` |
| `nordic-urban-family` | 现代都市家庭、品质生活 | `project-validated` |
| `lavender-premium-women` | 女性消费、轻奢陪伴设备 | `validated` |
| `young-urban-consumer-tech` | 年轻消费电子、桌面设备 | `project-validated` |
| `dark-tech-keynote` | 深色科技、安防、技术架构 | `experimental` |

`validated` 可直接使用；`project-validated` 要保留 Contact Sheet QA；`experimental` 先做 1–2 页试样。

例如家庭桌面智能屏：

```yaml
style_id: neutral-modern-home
style_scope: whole-deck
style_mix: forbidden
```

## 9. 生成后检查

### 单页

- 标题、副标题、数字是否准确；
- 产品是否完整、未被裁切；
- 产品是否位于合理桌面、餐桌、边柜或置物架；
- 是否出现额外 Logo、页码或未指定文字；
- 是否出现多余边框、胶囊、玻璃面板或乱码。

### 跨页

- 标题字重和副标题颜色是否统一；
- 背景明度和摄影色彩是否统一；
- 人物、产品和空间是否漂移；
- 多图页面是否明显降质；
- 是否某页突然变成另一种风格或模板。

### QA 格式

```markdown
| Page | Issue | Action |
|---|---|---|
| 03 | 四图中第 02 张曝光偏暗 | 只重生第 03 页，保持四图结构和准确文案 |
| 05 | 产品落在地面 | 只重生第 05 页，改为桌面承托 |
```

## 10. 团队协作

可以拆成四步：

1. 需求整理：`content-brief.md`、`storyboard.md`
2. 视觉规划：`global-visual-contract.md`、`prompt-pack.md`
3. 图片生成：MCP 或外部图片平台
4. QA 和交付：Contact Sheet、`qa.md`、PPTX

这样团队成员可以使用不同图片平台，但共享同一套内容、风格、Prompt 和质量标准。

## 11. 一句话记忆

有 MCP：

```text
规划 → 确认 → 健康测试 → MCP 生图 → Contact Sheet → QA → PPTX
```

没有 MCP：

```text
规划 → Prompt Pack → 外部平台生图 → 下载图片 → Contact Sheet → QA → PPTX
```

> `keynote-prompt-system` 不等于某个图片生成平台；它负责把 PPT 需求变成可复用、可检查、可交接的视觉生产流程。
