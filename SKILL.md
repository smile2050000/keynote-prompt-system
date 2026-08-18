---
name: keynote-prompt-system
description: 将 txt、md、html、docx、pdf、pptx、截图等单一主要需求整理为整套 PPT Deck Plan、精简视觉系统和逐页 Image2 Prompt；用户确认后可调用 Image2 生成视觉稿并制作整套预览。
---

# Keynote Prompt System V1

目标：用少量稳定约束、准确内容和正确 Reference，生成统一且可修正的发布会 PPT 视觉稿。V1 暂不解决可编辑文字、完整母版库或自动视觉校准。

## 固定产出

1. `content-brief.md`：整套叙事、逐页内容与事实来源。
2. `design-system.md`：8–12 条 Global Visual Contract 与唯一 `style_id`。
3. `prompt-pack.md`：逐页最终 Prompt、Reference 路由与调用参数。

执行阶段另产出：

- `execution-log.md`：真实调用、结果和单变量修正记录；
- `montage-all.png`：按页码完整展示全部页面；
- `deck-preview.pptx`：每页一张整页图片铺满的预览文件。

## 工作流程

### 1. 读取需求

默认处理一个主要需求文件。其他文件只有在用户明确指定为参考时才参与。

来源优先级：

```text
用户明确说明 > 需求正文 > 已核验事实 > 参考材料 > Skill 默认规则
```

参考发布会只用于学习叙事、节奏和审美逻辑，不复制具体页面。

### 2. 确认关键缺失

页数、受众、产品与数据事实、浅色/深色方向、参考材料用途、产品资产、交付格式或生图方式不明确时，先确认。不得猜测参数、排名、身份、业务主张或 Logo。

### 3. 生成 Deck Plan

一次性规划整套，不逐页边生成边决定。每页只记录：

- 一个核心信息与必须保留的事实；
- Page Type 与信息密度；
- 第一视觉对象和内容关系；
- 人物、产品或 Style Reference；
- 从 [title-structure.md](references/title-structure.md) 选择的标题结构；
- 与前后页的视觉节奏。

Page Type 读取 [page-families.md](references/page-families.md)，它只定义页面意图，不规定固定母版。

### 4. 生成 Global Visual Contract

先从 [style-presets.md](references/style-presets.md) 选择一个风格，并声明：

```yaml
style_id: [唯一风格 ID]
style_scope: whole-deck
style_mix: forbidden
```

Global Visual Contract 控制在 8–12 条，只锁定：发布会定位、整体气质、色彩与背景、光线与摄影、排版角色、产品原则、信息密度、关键风险。不要加入项目内容、页面级创意、像素坐标或长篇禁止词。

### 5. 编译逐页 Prompt

按 [prompt-schema.md](references/prompt-schema.md) 组装。逐页 Prompt 只包含：

```text
Global Visual Contract
+ Page Type / Title Structure / Visual Mode
+ 当前页真实内容与第一视觉
+ Reference 路由
+ 2–5 个不可改变项
+ 一个页面类型质量后缀
```

内容必须来自 `content-brief.md` 或用户原始文件；缺失事实先停止并确认，不发送“待确认”给 Image2。Data、System、Process、Logic 页读取 [type-and-visual-grammar.md](references/type-and-visual-grammar.md)，先完成语义到视觉关系的映射，再写 Prompt。

### 6. Reference 路由

- 无目标产品：`image_mcp_demo.generate_image`。
- 出现目标产品：必须使用用户确认的产品 Reference，调用 `image_mcp_demo.edit_image`；不得凭空生成相似产品。
- 产品多角度图只用于识别，不得出现在最终画面。
- 产品路径、结构特征、数量与调用参数属于项目配置，写入 `prompt-pack.md`，不写入通用 Skill。

### 7. 执行闸门

规划阶段不调用生图 MCP。用户确认 Deck Plan、Global Visual Contract、Reference 和整体方向后才执行。

- 默认 16:9；分辨率按用户要求，未指定则遵循 Image2 Skill 默认值。
- MCP 失败时返回真实错误，不静默切换模型。
- 缺少 Active Style、准确内容或必要 Reference 时不得生成。

### 8. 复核与修正

先制作完整 contact sheet，再分别检查：

- 单页内容、产品与文字准确性；
- 跨页色彩、光线、标题结构、信息密度和产品尺度；
- 是否出现风格漂移、海报化、模板卡片墙或页面过度同构；
- 信息页的视觉关系是否真正解释内容；
- 背景是否抢占文字识别区域。

修正时一次只改变一个变量，记录原 Prompt、Reference、参数、问题和结果。

## 核心边界

- 一个 Deck 只激活一个 Style Preset。
- 家庭浅色方向默认使用 `neutral-home-keynote`：中性白灰为主，木色只作材质点缀，清洁自然日光与中性灰阴影；温馨由人物行为、产品作用和家庭关系表达，不使用黄色滤镜、黄金时刻或昏黄灯光。
- 标题结构默认上方居中，其他结构必须由内容关系触发。
- Typography 使用现代无衬线字体；文字颜色按背景反差选择，不使用彩色标题。
- 除 Hero、金句和 Ending 外，页面应具备标题、主视觉关系和必要辅助信息，不退化成海报。
- 产品、事实、准确文字和 Reference 是硬约束；构图、尺度与视觉隐喻保留给 Image2。
- 复杂度和创意同时受控：不靠特效制造设计，也不因删减退化成纯文字。
- 不在 V1 建立完整 Layout Library、Blueprint 或自动校准系统。

## 参考文件

- [page-families.md](references/page-families.md)：页面意图分类。
- [style-presets.md](references/style-presets.md)：Deck 级风格边界。
- [title-structure.md](references/title-structure.md)：三种标题结构。
- [type-and-visual-grammar.md](references/type-and-visual-grammar.md)：信息页视觉语法。
- [prompt-schema.md](references/prompt-schema.md)：Prompt、Reference 与执行日志格式。
- [palette-systems.md](references/palette-systems.md)：仅在未确定色彩方向时读取。
