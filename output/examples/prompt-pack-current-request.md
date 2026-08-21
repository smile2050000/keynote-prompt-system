# Prompt Pack 示例：Skill 视觉执行流程

> 用途：根据当前“Skill 视觉执行流程”教程内容，编译一套 5 页说明型 PPT 的示例 Prompt Pack。
>
> 语言规则：页面可见文字全部使用中文；仅保留固定文件名、工具名、模型名、`style_id`、`Page Type` 和 `Reference` 等技术标识。此文件用于检查 Prompt Pack 的语言策略，不代表已经执行生图。

## Global Visual Contract

```yaml
style_id: neutral-modern-home
style_scope: whole-deck
style_mix: forbidden
language: zh-CN
ratio: 16:9
```

1. 生成一套 16:9 的说明型发布会 PPT 页面，主题是 Keynote Prompt System 的视觉执行流程。
2. 全套使用清透、明亮、克制的现代无衬线视觉语言，中文以苹方或同类现代无衬线字体呈现。
3. 页面可见标题、副标题、标签和说明全部使用简体中文，不主动加入英文翻译，不做中英双语重复排版。
4. 文件名、工具名、模型名、`style_id`、`Page Type`、`Reference`、`Prompt Pack`、`Contact Sheet` 和 `PPTX` 等固定技术标识可以保留原文。
5. 背景使用明亮白色、浅灰白和非常轻的冷灰层次，文字使用深石墨黑和中性灰，重点色只使用湖蓝。
6. 标题统一深石墨黑、粗体、水平排版；副标题和说明统一中性灰、常规字重；禁止彩色标题、细粗混用和装饰性英文标题。
7. 使用 Open Stage 和单层 Simple Media Frame 两类容器；图片和文字只允许一个简洁外框，禁止嵌套边框、双重描边、胶囊和玻璃面板。
8. 画面保持真实的中间调和自然彩度，禁止灰雾、曝光不足、全局去饱和、过度发光和科技模板化装饰。
9. 每页只表达一个核心关系，保持标题区、主视觉区和说明区之间有清晰留白，不使用模板化三栏卡片墙。
10. 所有文字正视画布、水平基线、无透视、无旋转；不添加页码、Logo、日期、虚构数据或未经确认的产品事实。

## Page 01

- Page Type: Opening
- Visual Strength: Strong
- Title Structure: 上方居中
- Core Message: Skill 负责把视觉需求整理成可执行流程。
- Audience Memory: 这是一个负责规划、编译和检查的视觉执行系统，不是单独的图片平台。
- Visual Relationship: 一个清晰的流程中枢连接需求、Prompt、图片和 QA。
- Exact Text:
  - 标题：Skill 视觉执行流程
  - 副标题：从需求理解到图片版 PPTX 的完整路径
  - 标签：需求 / 规划 / Prompt / 图片 / QA
- Reference: 无
- Must Preserve:
  - 标题和副标题必须为简体中文。
  - 标题上方水平居中，粗体，深石墨黑。
  - 流程关系清晰，不生成复杂软件界面或虚构产品截图。
- Page-specific Quality: premium keynote information design, clear hierarchy, restrained depth, generous negative space
- Avoid:
  - 中英双语重复标题。
  - 英文大标题或英文副标题。
  - 过多箭头、发光线条、仪表盘和装饰性科技元素。
  - 低对比度灰雾背景。

## Page 02

- Page Type: Process
- Visual Strength: Medium
- Title Structure: 上方居中
- Core Message: Skill、Image2、外部图片平台和 slides 各自承担不同职责。
- Audience Memory: Skill 负责想清楚和写清楚，图片工具负责生成，slides 负责封装和验证。
- Visual Relationship: 四个职责模块围绕一条从规划到交付的水平流程展开。
- Exact Text:
  - 标题：四个环节，各自负责什么
  - 副标题：规划、生成、检查和封装必须分开
  - 模块一：Skill / 需求、叙事、视觉规则、Prompt
  - 模块二：Image2 / 生成或编辑图片
  - 模块三：QA / Contact Sheet、问题记录、定点重生
  - 模块四：slides / 图片版 PPTX 和渲染检查
- Reference: 无
- Must Preserve:
  - 四个模块必须同等级、等距、统一样式。
  - 页面主要文字使用中文，英文只保留固定工具名和文件名。
  - 禁止把 Skill 画成软件产品界面。
- Page-specific Quality: premium keynote information design, precise alignment, restrained depth, no template dashboard
- Avoid:
  - 中英混排成两套语言层级。
  - 复杂流程图、管道、河流、物流路径或箭头海洋。
  - 四个模块大小不一致。

## Page 03

- Page Type: Comparison
- Visual Strength: Medium
- Title Structure: 上方居中
- Core Message: 有 MCP 和没有 MCP 都可以完成整套流程。
- Audience Memory: MCP 是可选自动生图通道，不是 Skill 的使用前提。
- Visual Relationship: 左右两条等权路线从同一个规划起点分流，再汇合到 QA 和 PPTX。
- Exact Text:
  - 标题：两种使用方式
  - 副标题：有 MCP 自动执行，没有 MCP 复制 Prompt 执行
  - 左侧标题：有 MCP
  - 左侧说明：规划确认 → 健康测试 → 自动生图 → QA → PPTX
  - 右侧标题：没有 MCP
  - 右侧说明：规划确认 → Prompt Pack → 外部图片平台 → QA → PPTX
- Reference: 无
- Must Preserve:
  - 左右两条路线必须等宽、等高、同一容器样式。
  - “没有 MCP”不能被表达成失败或低级方案。
  - 所有路线文字使用简体中文，箭头只用于表达流程方向。
- Page-specific Quality: premium keynote information design, balanced comparison, clear route separation
- Avoid:
  - 用颜色暗示某条路线更正确。
  - 添加未经确认的平台排名、价格或成功率。
  - 胶囊标签、透视卡片和嵌套边框。

## Page 04

- Page Type: System
- Visual Strength: Medium
- Title Structure: 上方居中
- Core Message: Prompt Pack 是可复制、可交接、可检查的中间产物。
- Audience Memory: 每页 Prompt 必须同时写清文字、Reference、尺寸、保留项和风险。
- Visual Relationship: 一份 Prompt Pack 展开为四个明确字段组，并指向最终图片。
- Exact Text:
  - 标题：Prompt Pack 要写清什么
  - 副标题：让自己、团队成员和外部图片平台都能直接执行
  - 字段一：准确文字
  - 字段二：Reference 与上传方式
  - 字段三：比例、尺寸与生成模式
  - 字段四：Must Preserve、Avoid 与检查项
- Reference: 无
- Must Preserve:
  - 四个字段组必须有明确阅读顺序。
  - “准确文字”必须是第一等级信息。
  - 禁止生成真实代码编辑器、虚构平台截图或密集表格。
- Page-specific Quality: premium keynote information design, content-driven visual hierarchy, generous negative space
- Avoid:
  - 把英文字段名全部直接展示成页面主文案。
  - 伪造 Prompt Pack 的代码窗口。
  - 密集小字、过多说明和无语义图标。

## Page 05

- Page Type: Closing
- Visual Strength: Quiet
- Title Structure: 上方居中
- Core Message: 先规划，再确认，问题页定点修正。
- Audience Memory: 质量来自可追踪的流程和明确的 QA，而不是一次性碰运气。
- Visual Relationship: 一条简洁的复查闭环连接规划、生成、QA 和最终交付。
- Exact Text:
  - 标题：把问题留在流程里解决
  - 副标题：先规划，再确认；保留真实错误；只修正明确的问题
  - 标签：规划 / 生成 / QA / 定点重生 / PPTX
- Reference: 无
- Must Preserve:
  - 结尾保持明亮、清晰和有呼吸感。
  - 标题和副标题继续水平居中，字重和颜色与前四页一致。
  - 不添加口号、品牌 Logo、版本徽章或虚构成果数字。
- Page-specific Quality: premium keynote information design, calm closing frame, clear midtones, restrained depth
- Avoid:
  - 过暗收尾页。
  - 大面积发光、奖章、勋章或完成百分比。
  - 把 QA 画成复杂监控仪表盘。

## Execution Notes

- 当前示例不包含产品，因此 5 页均使用 `generate_image`，不需要产品 Reference。
- 如果实际需求包含产品页，改用 `edit_image`，并在对应页面补充产品 Reference 路径和用途。
- 生成前先做最小健康测试；测试失败时记录 `image_mcp_demo` 的真实错误并停止。
- 生成后制作 `qa/contact-sheet-pass-01.png`，只记录明显问题页，再定点重生。
- 最终通过 QA 后制作 `qa/contact-sheet-final.png` 和图片版 `deck-preview.pptx`。
