---
name: keynote-prompt-system
description: 将 txt、md、html、docx、pdf、pptx、截图等单一主要需求整理为整套 PPT Deck Plan、精简 Global Visual Contract 和逐页 Image2 Prompt；用户确认后可调用 Image2 生成整套视觉稿并进行 contact sheet 复核。
---

# Keynote Prompt System V1

本 Skill 的第一阶段目标只有一个：验证 Image2 能否在少量稳定约束和正确 Reference 下，生成一整套高质量、统一且可修正的发布会 PPT 视觉稿。

暂不解决 Keynote 可编辑化、完整 Layout Library、多 Agent 校准或自动重建设计系统。

## 固定产出

1. `content-brief.md`：整套 Deck Plan。
2. `design-system.md`：精简 Global Visual Contract。
3. `prompt-pack.md`：Page Type、逐页最终 Prompt、Reference 路由和调用参数。

执行生图时另存 `execution-log.md`，记录真实发送内容，不作为规划阶段的固定产出。

执行阶段还必须生成两种整套预览：

- `montage-all.png`：完整展示所有页面，按页码标注，不截断、不只展示前 6 页；
- `deck-preview.pptx`：每页一张整页图片铺满画布的预览 PPTX，仅用于统一查看，不承诺可编辑。

## 工作流程

### 1. 读取需求

默认处理一个主要需求文件，支持 `txt`、`md`、`html`、`docx`、`pdf`、`pptx`、截图和其他可读取文本。其他文件只有在用户明确指定为参考材料时才参与。

来源优先级：

```text
用户明确说明 > 需求正文 > 已核验事实和数据 > 参考材料 > Skill 默认规则
```

参考发布会默认用于学习叙事、页面节奏和审美逻辑，不复制具体页面。

### 2. 确认关键缺失

以下信息不明确时先确认：页数、目标受众、产品与数据事实、浅色/深色方向、参考材料用途、是否整页生图、产品资产位置和交付格式。

不得猜测产品参数、排名、人物身份、业务主张或 Logo。

### 3. 生成 Deck Plan

先一次性规划整套 PPT，不逐页边生成边决定。每页只记录：

- 一个核心信息；
- Page Type；
- 视觉强弱与信息密度；
- 第一视觉对象；
- 必须保留的文字、数字和事实；
- 是否需要人物、产品或其他 Reference；
- 标题结构：从 [title-structure.md](references/title-structure.md) 选择一种主结构；
- 与前后页的节奏关系。

Page Type 读取 [page-families.md](references/page-families.md)。它只约束页面意图，不规定固定坐标或母版。

标题位置默认只允许三种主结构：

1. **左右居中上方结构**：适合主结构页、产品页、观点页；标题区域位于页面上方，并保持左右视觉平衡。
2. **左右排布上下居中结构**：适合左右关系、对比、流程和部分功能页；标题区域在页面上下方向居中。
3. **金句居中结构**：适合 Hero、Ending 和单一主张页；标题区域上下左右居中。

除非内容确实需要，默认不使用左上角长标题、右上角标题、底部标题或自由漂移标题。特殊结构必须在 `content-brief.md` 记录原因。

### 4. 生成 Global Visual Contract

全套只使用一份 Global Visual Contract，并控制在 8–12 条。只锁定真正需要跨页一致的内容：

- 画布比例和发布会定位；
- 整体气质与视觉尺度；
- 背景和色彩边界；
- 标题、副标题和说明的角色关系；
- 产品、人物和摄影处理原则；
- Typography Contract 和信息设计语言；
- 信息密度和视觉中心；
- 明显错误禁止项。

不要写像素坐标、固定卡片尺寸、统一留白比例或大量近义质量词。不要把“统一”变成“每页相同”。

### 5. 编译逐页 Prompt

读取 [prompt-schema.md](references/prompt-schema.md)。每页 Prompt 只包含：

```text
Global Visual Contract
+ Page Type
+ 当前页核心信息和画面对象
+ 准确文字/数字
+ Reference 路由
+ 当前页不可改变项
```

每页不得重新定义全局颜色、字体、影调和发布会气质。每页必须显式写入 `Title Structure`；图表、流程、逻辑和数据页还必须显式写入 `Visual Mode`。内部推理、验收解释和设计术语不发送给 Image2。

Typography Contract 默认固定：中文使用苹方/思源黑体一类现代无衬线字体，英文和数字使用 Helvetica Neue/Arial 一类现代无衬线字体；主标题深石墨黑，副标题和说明中性灰，禁止彩色标题和彩色副标题。标题、正文、标签、注释使用稳定的相对字号层级、行距和安全边距，逐页只允许改变尺度，不允许重新发明字体规则。详细规则读取 [type-and-visual-grammar.md](references/type-and-visual-grammar.md)。

### 6. 产品 Reference 硬规则

页面中只要出现目标产品，无论是主视觉还是场景配角，都必须使用用户确认的产品 Reference，并调用 `image_mcp_demo.edit_image`；不得使用 `generate_image` 凭空生成相似产品。

当前小度 C1500 测试项目固定使用：

```text
/Users/smile/Desktop/PPT生图尝试/灵光-6m 0912/1200/contact-sheet.jpg
strength: low
ratio: 16:9
```

多角度参考板仅用于识别和重建同一产品，绝不能作为最终画面素材。禁止展示参考板、六面图、产品陈列图或多角度产品阵列；除非页面明确要求，否则只出现一个目标产品，并从参考板选择与当前场景匹配的单一视角。

必须保持产品身份、上方双镜头、下方单镜头、总共三颗镜头、头部/机身比例、连接结构、白色哑光材质和关键细节。产品英雄页可突出产品；场景融合页必须匹配透视、尺度、焦点、光线方向、色温、接触面、接触阴影和遮挡关系，产品不得像贴图、悬浮物或孤立抠图。

### 7. 执行闸门

规划阶段不调用生图 MCP。只有用户确认 Deck Plan、Global Visual Contract、Reference 和整体方向，并明确要求开始生成后才执行。

- 无产品页面：`image_mcp_demo.generate_image`
- 有目标产品页面：`image_mcp_demo.edit_image`
- 默认 16:9；分辨率按用户要求，未指定则按 Image2 Skill 默认值。
- MCP 失败时返回真实错误，不静默切换其他模型。

### 8. 整套复核

生成固定测试集或完整 Deck 后，先制作 contact sheet，再检查：

- 单页质量；
- 跨页一致性；
- 标题层级、色彩、背景、产品尺度和信息密度是否漂移；
- 连续页面是否过度同构；
- 某页是否突然变成电商页、B 端信息图或生活方式广告；
- 标题是否遵守三种主结构，是否出现未经记录的自由漂移标题；
- 字体、字号层级、行距、边距、标题区域大小和文字颜色是否跨页稳定；
- 图表、流程、逻辑和数据页是否具有主视觉隐喻，而不是图库图标行或模板卡片墙；
- 产品结构和准确文字是否正确。

修正时一次只改变一个变量，并记录修改前后的 Prompt、Reference、调用参数和结果。

## V1 约束

- 质量优先，避免通过堆叠规则换取表面统一。
- Page Type 负责信息意图，不负责固定布局。
- 所有页面共享同一 Global Visual Contract。
- 产品 Reference、事实数据和准确文字属于硬约束。
- 构图、尺度、摄影裁切和视觉隐喻保留给 Image2 发挥。
- 图表、流程、逻辑和数据页必须选择适合的 `Visual Mode`，默认采用平面编辑化信息设计，不把玻璃材质和发光 3D 当作默认答案。
- 图表页需要设计语言，不只是“扁平化”：必须有一个服务于内容的视觉隐喻、统一图形语法和明确的信息节奏。
- 不在第一阶段建立完整 Layout Library、Blueprint 或自动校准系统。

## 参考文件

- [page-families.md](references/page-families.md)：V1 Page Type。
- [prompt-schema.md](references/prompt-schema.md)：逐页 Prompt、Reference 路由和执行日志格式。
- [title-structure.md](references/title-structure.md)：三种默认标题结构和例外记录方式。
- [type-and-visual-grammar.md](references/type-and-visual-grammar.md)：Typography Contract 和图表/流程/逻辑/数据页的视觉语法。
- [palette-systems.md](references/palette-systems.md)：仅在用户尚未确定色彩方向时按需读取。
