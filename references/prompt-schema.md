# V1 Image2 Prompt Schema

本文件只定义 Prompt 的组装方式，不重复风格和页面类型规则。

## Project Artifacts

### storyboard.md

```markdown
| Page | Core Message | Audience Memory | Page Type | Visual Strength | Special Risk |
|---|---|---|---|---|---|
| 01 | [唯一核心信息] | [翻页后应记住什么] | [Page Type] | Strong / Medium / Quiet | [最关键风险] |
```

Storyboard 只定义内容任务、观众记忆和视觉节奏，不定义版式、像素坐标、字号、卡片数量或组件尺寸。

### global-visual-contract.md

```yaml
style_id: [唯一风格 ID]
style_scope: whole-deck
style_mix: forbidden
```

YAML 后写 8–12 条共享视觉规则。该文件是唯一来源；旧项目的 `design-system.md` 只作为兼容输入。

## Global Visual Contract

整套 Deck 只定义一次，控制在 6–8 条短规则：

```text
16:9 与发布会定位
唯一 Style Lock
整体气质与视觉尺度
色彩、背景、光线与摄影
Typography 角色与文字反差
产品和人物原则
统一容器、文字可读性与产品保真
光线、材质和影调基线
```

## Per-page Prompt

每页按以下顺序编译：

```text
生成一张完整的 16:9 发布会 PPT 页面，画面和准确文字一次生成。

[全局视觉规则来源]
[完整粘贴 6–8 条短规则。每条只表达一个跨页稳定契约。]

[Storyboard Source: Page XX]
Page Type: [页面类型]
Visual Strength: [Strong / Medium / Quiet]
Title Structure: [上方居中 / 左右结构 / 金句居中]
Visual Mode: [仅信息页填写]
Core Message: [一个核心信息]
Audience Memory: [观众翻页后应记住什么]
Composition Brief: [镜头尺度与视角；主体位置；每个角色/产品的行为、尺度、接触、遮挡与视线关系；文字安全区；第一视觉和次级信息的层级]
Visual Relationship: [用画面关系解释内容，不写抽象气氛词]
Audience Question: [观众此页正在问什么]
Evidence Type: [真实场景 / 对比 / 产品实物 / 数据 / 系统关系 / 演示结果]
Dominant Carrier: [人物行为 / 产品 / 空间状态 / 数字 / 关系图 / 界面 / 视频帧]
Spatial Grammar: [同一场景对照 / 中心汇聚 / 分层协作 / 尺度递进 / 局部放大 / 证据并置]
Distinct From: [当前页必须与哪一页区分；明确改变主视觉载体或空间语法]
Exact Text: [逐字标题、数字、标签]
Reference: [无 / Style / Product；路径与用途]
Must Preserve: [2–5 个事实或产品硬约束]
Page-specific Quality: [按当前 Page Type / Visual Mode 动态选择的正向质量描述]
Avoid: [最多 3 个当前页最高风险]
```

逐页 Prompt 不重新定义风格，不发送内部推理、验收清单或设计原因。项目文件中的 Source 声明用于追踪来源；真正调用 Image2 时必须把 Global Visual Contract 完整注入，因为模型不能自行读取 Markdown 文件，也不会继承其他页面的上下文。

## 内容保真

- 文字、数字、参数、功能与模块必须来自 `content-brief.md` 或原始文件。
- 禁止占位数据、临时文案和未经确认的补充说明。
- 内容缺失时停止生成并向用户确认，不把“待确认”发送给 Image2。
- 信息页只保留一个主结论、一个主关系和必要标签。

## Reference 路由

### 无目标产品

调用 `image_mcp_demo.generate_image`。Style Reference 只有在测试轮次明确启用时才输入。

### 出现目标产品

调用 `image_mcp_demo.edit_image`。输入图只用于识别同一产品，不得直接展示参考板、多角度阵列或产品拼图。产品必须匹配当前场景的视角、尺度、光线、接触面和遮挡关系。

具体路径、产品结构和 `strength` 写入项目 `prompt-pack.md`。

## 页面类型动态质量描述

每页根据当前 Page Type、Visual Mode、Evidence Type、Dominant Carrier 和 Spatial Grammar 选择一组正向质量描述，不得五页复用同一段。质量描述必须包含：视觉载体、镜头/空间关系、材质与光线、文字安全区、数据或产品的可信表达。质量描述应先说明希望模型生成什么，再用最多 3 个页面级风险限制当前页。不要用同一长串否定词覆盖所有页面。

### Prompt 长度与优先级

Image2 不会因为 Prompt 更长就自动更准确。编译时按以下优先级排序：

1. 页面准确文字、关键数字、产品身份和 Reference；
2. 当前页观众问题、证据类型、主视觉载体和空间语法；
3. 镜头、主体位置、角色/产品关系和文字安全区；
4. 共享色彩、字体、光线、材质和容器契约；
5. 页面级质量描述；
6. 不超过 3 条当前页最高风险。

删除演讲稿、内部推理、重复背景说明、跨页比较和无法由当前模型执行的抽象要求。共享规则建议保持 6–8 条短句，页面 Prompt 先完成结构和内容，再补质量描述。

**场景摄影**

```text
真实商业生活方式摄影，明确的镜头距离和主体关系，专业美术指导，透视准确，清晰中间调，真实肤色和织物，受控高光，空间留白稳定，适合标题叠加
```

**产品融合**

```text
产品真实存在于环境中，透视、尺度、焦点、光线和色温匹配，接触面和阴影真实，遮挡关系自然，保持产品身份、结构和材质准确
```

**信息设计**

```text
发布会信息设计，内容驱动的视觉层级，关系清晰，对齐精准，尺度和密度有变化，保留充足留白，文字可读，图形服务于信息关系
```

**大数字 / 数据证据**

```text
发布会数据证据页，数字是主锚点但不是唯一视觉内容；用清晰的证据关系、局部语义图形、真实场景细节或克制的编辑化图表解释数字来源；重点色用于数据关系和关键节点，背景保留明亮中间调，数字、标签、解释和来源形成明确层级，适合大屏投影阅读
```

**新品发布 / 产品英雄页**

```text
发布会新品英雄页，产品是唯一第一视觉，使用明确镜头距离、产品视角、接触面、尺度和光线方向；环境只承担产品语境，卖点通过产品动作、结构细节或真实使用关系表达；标题区与产品区有清晰留白，材质真实，产品边缘和屏幕细节锐利
```

**真实场景 / 对比页**

```text
真实场景关系页，使用同一空间和同一时间关系呈现前后或认知差异；人物行为、环境状态和视觉标注共同回答观众问题；镜头连续、角色位置可追踪、主次关系明确，场景真实而不摆拍，文字叠加区保持稳定反差
```

## 执行日志

```markdown
## Page XX
- Page Type:
- MCP tool / model / provider:
- Ratio / size:
- Input reference / strength:
- Exact prompt:
- Output file:
- Result: pass / fail
- Observed problems:
- Next single variable:
```

## 生成后

- 首轮制作包含全部页面和页码的 `qa/contact-sheet-pass-01.png`。
- 创建 `qa/qa.md`，只记录明显问题页：

```markdown
| Page | Issue | Action |
|---|---|---|
| 03 | [一个明显问题] | [只重生本页；改变什么；保持什么] |
```

- 只重生 `qa.md` 中的问题页，不覆盖首轮图片，不因单页问题修改共享规则。
- 定点重生完成后制作 `qa/contact-sheet-final.png` 并复查整套。
- 同步生成图片铺满的 `deck-preview.pptx`。
- 单页问题与跨页系统问题分开记录；保存失败结果，一次只修改一个变量。

## Editable Reconstruction Handoff

图片视觉通过 QA 后，可编辑重建只接收以下已批准输入：最终页面图、对应 Storyboard、准确文字、Global Visual Contract、Reference 路由、QA 结论。派生产物单独保存，不覆盖 Image2 页面图。本 Schema 不规定具体重建引擎。
