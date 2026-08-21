---
name: keynote-prompt-system
description: 将 txt、md、html、docx、pdf、pptx、截图等单一主要需求整理为整套 PPT Deck Plan、精简视觉系统和逐页 Image2 Prompt；用户确认后可调用 Image2 生成视觉稿并制作整套预览。
---

# Keynote Prompt System V1

目标：用少量稳定约束、准确内容和正确 Reference，规划并生成统一且可修正的发布会 PPT 视觉稿。当前 v0.9.3 生产模式固定为 Image2 整页生图；文字、数字和复杂关系必须在生成后验证。V1 暂不解决完整母版库或自动视觉校准。

## 固定产出

1. `content-brief.md`：整套叙事、准确内容与事实来源。
2. `storyboard.md`：逐页核心信息、观众记忆、Page Type、视觉强弱与特殊风险。
3. `global-visual-contract.md`：6–8 条共享视觉规则与唯一 `style_id`。
4. `prompt-pack.md`：逐页最终 Prompt、Reference 路由与调用参数。

执行阶段另产出：

- `execution-log.md`：真实调用、结果和定点重生记录；
- `qa/contact-sheet-pass-01.png`：首轮全部页面的 Contact Sheet；
- `qa/qa.md`：只记录明显问题及逐页处理动作；
- `qa/contact-sheet-final.png`：问题页修正后的整套复查图；
- `deck-preview.pptx`：可选下游预览文件，由 `slides` / `ppt` Skill 在用户明确需要时封装。

## 工作流程

### 1. 读取需求

默认处理一个主要需求文件。其他文件只有在用户明确指定为参考时才参与。

每轮任务都按新的独立项目开始：新建运行目录，重新建立本轮来源清单，重新编写 `content-brief.md`、`storyboard.md`、`global-visual-contract.md` 和 `prompt-pack.md`。历史项目的 Prompt、Storyboard、视觉规则、图片和 QA 默认不可见；只有用户明确指定为本轮 Reference 时才能使用。

来源优先级：

```text
用户明确说明 > 需求正文 > 已核验事实 > 参考材料 > Skill 默认规则
```

参考材料只用于本轮明确指定的内容或视觉参考；未被指定的历史项目不参与本轮。参考发布会只用于学习叙事、节奏和审美逻辑，不复制具体页面。

### 2. 确认关键缺失

页数、受众、产品与数据事实、浅色/深色方向、参考材料用途、产品资产、交付格式或生图方式不明确时，先确认。不得猜测参数、排名、身份、业务主张或 Logo。

### 3. 生成 Storyboard

在编译逐页 Prompt 前创建 `storyboard.md`，一次性规划整套，不逐页边生成边决定。每页按 [prompt-schema.md](references/prompt-schema.md) 的分组模板记录内容任务、视觉关系和风险字段。字段必须真实落盘，不能只在 Prompt 编译阶段临时补写。

Storyboard 是逐页 Prompt 的内容依据，不规定固定版式、坐标、字号、卡片数量或组件尺寸。Page Type 读取 [page-families.md](references/page-families.md)，它只定义页面意图，不规定固定母版。准确文字、数据和事实仍以 `content-brief.md` 为准。

### 4. 固定 Global Visual Contract

先从 [style-presets.md](references/style-presets.md) 选择一个风格。`validated` 可直接使用；`project-validated` 保留 Contact Sheet QA；`experimental` 必须先做 1–2 页试样并经用户确认后才能扩展全套。声明：

```yaml
style_id: [唯一风格 ID]
style_scope: whole-deck
style_mix: forbidden
```

将共享规则独立保存为 `global-visual-contract.md`。Global Visual Contract 固定为 6–8 条短规则，只锁定跨页稳定契约：发布会定位、整体气质、基础色彩、字体角色、产品保真、统一容器边界、文字可读性和光线/材质基线。Style Lock 只锁定品牌气质和视觉材料，不锁定页面布局、主视觉载体、标题位置或信息图语法。Prompt 编译前必须确认该文件存在且已选定唯一 `style_id`。不要把项目内容、页级构图、跨页差异、像素坐标、固定字号、固定卡片尺寸或长篇禁止词写入共享规则。

`global-visual-contract.md` 是唯一视觉规则来源。旧项目的 `design-system.md` 可作为兼容输入；继续执行时先确认其内容，再映射为 `global-visual-contract.md`，不要求批量改写历史项目。

### 5. 编译逐页 Prompt

按 [prompt-schema.md](references/prompt-schema.md) 组装。逐页 Prompt 只包含：

```text
Global Visual Contract（每页完整原样注入）
+ Page Type / Title Structure / Visual Mode
+ 当前页 Storyboard 与真实内容
+ Composition Brief（镜头、主体位置、角色/产品关系、文字安全区）
+ Audience Question / Evidence Type / Dominant Carrier / Spatial Grammar
+ Distinct From（当前页与其他页的明确结构差异）
+ Reference 路由
+ 2–5 个不可改变项
+ 页面类型对应的动态质量描述
+ 3 个以内页面级最高风险
```

每页都声明 `global-visual-contract.md` 和对应 Storyboard 条目为来源。由于 Image2 不读取项目文件，也没有上一页或下一页记忆，实际调用时必须将 Global Visual Contract 的完整正文原样注入每个最终 Prompt。禁止写“沿用上一页规则”“避免与其他页重复”或“见全局文件”来代替正文。跨页差异必须在当前页 Prompt 中直接写明。

内容必须来自 `content-brief.md`、`storyboard.md` 或用户原始文件；缺失事实先停止并确认，不发送“待确认”给 Image2。Data、System、Process、Logic、Comparison、Product Launch 页读取 [type-and-visual-grammar.md](references/type-and-visual-grammar.md)，先完成语义到视觉关系的映射，再写 Prompt。禁止把“新品发布”“功能介绍”“用户场景”全部归入泛化的 Feature；必须先确定观众问题和证据类型。

### 6. Reference 路由

- 无目标产品：`image_mcp_demo.generate_image`。
- 出现目标产品：必须使用用户确认的产品 Reference，调用 `image_mcp_demo.edit_image`；不得凭空生成相似产品。
- 产品多角度图只用于识别，不得出现在最终画面。
- 产品路径、结构特征、数量与调用参数属于项目配置，写入 `prompt-pack.md`，不写入通用 Skill。

### 7. 执行闸门

规划阶段不调用生图 MCP。用户确认项目规划、Global Visual Contract、Reference 和整体方向后才执行。

- 默认 16:9；分辨率按用户要求，未指定则遵循 Image2 Skill 默认值。
- MCP 失败时返回真实错误，不静默切换模型。
- 缺少 Active Style、准确内容或必要 Reference 时不得生成。

### 8. Contact Sheet 与 QA

首轮生成完成后，先制作包含全部页面和页码的 `qa/contact-sheet-pass-01.png`，再创建 `qa/qa.md`。QA 只记录用户可见的明显问题：

- 风格漂移或跨页产品表现不一致；
- 构图明显重复或标题层级异常；
- 普通商务 PPT、模板卡片墙或海报化；
- 文字、数字、产品身份、裁切或结构错误；
- 信息页的视觉关系没有解释内容。

`qa.md` 按 `Page / Issue / Action` 记录，只列问题页；无明显问题的页面不制造修改任务。每个 Action 写清本次改变和必须保持不变的部分。

只重生问题页，不全套重跑。重生文件使用新版本名，不覆盖首轮结果；真实 Prompt、Reference、参数、输出路径和结果继续写入 `execution-log.md`。问题页修正后更新 `qa/contact-sheet-final.png`，再检查一次整套上下文。只有同一问题跨多页出现并证明来自共享规则时，才考虑修改 Global Visual Contract；修改共享规则可能影响全套，必须先向用户说明。

### 9. 可编辑重建接口

图片版通过 QA 后，如果用户明确要求可编辑 PPTX，再将最终页面图、对应 Storyboard、准确文字、Global Visual Contract、Reference 路由和 QA 结论作为下游重建输入。可编辑派生产物与已批准视觉图分开保存，不覆盖 Image2 视觉基线。本 Skill 不默认执行可编辑重建。

## 核心边界

- 一个 Deck 只激活一个 Style Preset。
- 家庭浅色方向默认使用 `neutral-modern-home`：中性白灰为主，木色只作材质点缀，清洁自然日光与中性灰阴影；温馨由人物行为、产品作用和家庭关系表达，不使用黄色滤镜、黄金时刻或昏黄灯光。
- 标题结构默认上方居中，其他结构必须由内容关系触发。
- Style Lock 只锁定品牌气质、色彩、字体角色、材质和产品保真，不锁定所有页面使用同一版式。
- Typography 使用现代无衬线字体；文字颜色按背景反差选择，不使用彩色标题。
- 除 Hero、金句和 Ending 外，页面应具备标题、主视觉关系和必要辅助信息，不退化成海报。
- 产品、事实、准确文字和 Reference 是硬约束；构图、尺度与视觉隐喻保留给 Image2。
- 复杂度和创意同时受控：不靠特效制造设计，也不因删减退化成纯文字。
- 视觉关系必须具体到镜头尺度/视角、主体与角色位置、角色之间的行为关系、产品与环境的接触/遮挡/尺度关系、文字安全区和第一视觉，不得只写“有信息量”“围绕某主题展开”等抽象描述。
- 页面级质量描述必须按当前 Page Type 和 Visual Mode 动态选择并优先写正向画面质量；Avoid 最多保留 3 个当前页最高风险，不用一长串通用否定词替代构图指令。
- Prompt 编译采用“短全局契约 + 清晰页面任务 + 具体构图简报 + 正确内容 + 动态质量描述”的顺序；不要把所有规则、演讲稿、验收清单和历史背景一起塞给 Image2。
- 当前 v0.9.3 只使用 Image2 整页生图模式：画面与可见文字一次生成，不在执行中自动切换为底图排字或其他模式。所有页面仍必须标记文字、数字、复杂关系和产品身份风险；生成后的错误只能通过 QA 记录和问题页定点重生处理。底图排字属于未来实验方向，不是当前默认补救流程。
- 12 页以上 Deck 必须先生成“页面构图地图”，为每页分配不同的主视觉载体和空间语法；至少区分封面、真实场景/对比、新品/产品、数据证据、系统架构、演示结果和收束页。
- 大数字页不得只生成黑白数字排版。必须声明数据的证据关系、数字之外的视觉载体、重点色使用方式、空间层次和数据来源位置；若没有真实证据载体，必须明确使用编辑化抽象图形，而不是默认三栏白底数字。
- QA 必须至少逐页检查：准确文字与数字、产品 Reference/产品身份、Global Visual Contract、Page Type 与 Storyboard 视觉关系；本规则只定义检查要求，不要求本轮自动化或全套迭代。
- 不在 V1 建立完整 Layout Library、Blueprint、自动评分系统或多 Agent 路由。

## 参考文件

- [page-families.md](references/page-families.md)：页面意图分类。
- [style-presets.md](references/style-presets.md)：Deck 级风格边界。
- [title-structure.md](references/title-structure.md)：三种标题结构。
- [type-and-visual-grammar.md](references/type-and-visual-grammar.md)：信息页视觉语法。
- [prompt-schema.md](references/prompt-schema.md)：Prompt、Reference 与执行日志格式。
- [palette-systems.md](references/palette-systems.md)：旧项目术语兼容，不用于新项目选择。
