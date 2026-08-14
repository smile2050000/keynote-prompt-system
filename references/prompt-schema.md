# V1 Image2 Prompt Schema

## Global Visual Contract

全套 Deck 只定义一次，并原样复用。建议 8–12 条，包含：

```text
16:9 与发布会定位
整体气质和视觉尺度
背景与色彩边界
标题/副标题/说明的角色关系
摄影、人物和产品处理原则
信息密度与视觉中心
明显错误禁止项
```

不要加入固定坐标、统一留白比例、卡片尺寸、详细视觉推理或大量质量近义词。

## Per-page Prompt

每页按以下顺序编译：

```text
生成一张完整的 16:9 发布会 PPT 页面，画面和准确文字一次生成。

［原样复用 Global Visual Contract］

［原样复用 Typography Contract 与视觉语法］

Page Type：［Cover / Hero / Product / Big Number / Feature / Comparison / Data / System / Image-led / Ending］
Title Structure：［左右居中上方 / 左右排布上下居中 / 金句居中］
Visual Mode：［默认 / Editorial Diagram / Flat Data / Process Flow / System Relationship；仅图表、流程、逻辑、数据页填写］
当前页：［一个核心信息；第一视觉对象；必要的视觉关系；视觉强弱与信息密度］
准确文字：［逐字标题、副标题、数字、标签］
Reference：［无 / Style Reference / Product Reference；输入路径和角色］
不可改变：［本页 2–5 项事实、产品或身份硬约束］
```

页面 Prompt 不重新定义全局颜色、字体、影调和发布会气质。不要发送内部页面家族、视觉隐喻、验收清单或设计原因。
页面 Prompt 必须要求文字只使用深石墨黑和中性灰；任何蓝色、紫色、绿色或其他彩色只可出现在非文字图形中，并且只在内容确实需要时出现。

## Reference 路由

### 无目标产品

调用 `image_mcp_demo.generate_image`。Style Reference 只有在测试轮次明确启用时才输入，不默认混入第一轮。

### 出现目标产品

调用 `image_mcp_demo.edit_image`，默认 `strength: low`。当前 C1500 项目使用：

```text
inputImagePath: /Users/smile/Desktop/PPT生图尝试/灵光-6m 0912/1200/contact-sheet.jpg
ratio: 16:9
strength: low
```

Prompt 必须明确：输入图是同一产品的多角度识别参考，不是最终画面素材；不得展示参考板、六面图、产品陈列图或多角度阵列；除非页面明确要求，只出现一个目标产品，并从参考图选择匹配当前场景的单一视角。

产品英雄页强调产品形态和发布会记忆点。场景融合页必须明确：产品真实存在于环境中，匹配透视、尺度、焦点、光线方向和色温，具有真实接触面、接触阴影和自然遮挡，不得像贴图、悬浮物或孤立抠图。

### 质量后缀

按页面类型选择一个短后缀，不把所有后缀叠加到同一页。

**场景摄影**

```text
premium commercial lifestyle photography, professional art direction, realistic human anatomy and natural expressions, controlled soft daylight, accurate perspective and spatial depth, clear midtones, crisp edges, natural skin texture, subtle contact shadows, no haze, no smearing, no plastic skin, no overexposure, no synthetic CGI look
```

**产品融合**

```text
the product is physically present in the environment, matched perspective, scale, focus, lighting direction and color temperature, real contact surface and contact shadow, natural occlusion and depth, not pasted on, not floating, not isolated, preserve exact product geometry and material
```

**图表与逻辑页**

```text
premium keynote information design, flat editorial graphic language, precise alignment and spacing, one coherent icon family, clear hierarchy and generous whitespace, no glassmorphism, no glossy 3D, no random decorative lines, no dashboard, no template-like card grid
```

### 图表、流程、逻辑和数据页

当 `Visual Mode` 不是“默认”时，读取 [type-and-visual-grammar.md](type-and-visual-grammar.md)。页面必须先选择一个内容驱动的视觉隐喻，再决定图形表达；不能只生成一排图库图标。要求主关系通过尺度、方向、密度、空间层次或局部放大被看见。允许轻微纸张、建筑、产品空间或精致实体层次，但默认不使用玻璃 UI、发光平台、透明圆环、复杂卡片墙或随机科技线。Visual Mode 是软约束，服务于信息关系，不替代页面内容判断。

场景与文字关系必须使用真实空间留白、明确硬裁切或完整画面叠字；禁止 soft white fade split、blurred vertical transition、misty gradient divider、feathered photo-text boundary 和 artificial white fog between text and image。对于“规则引擎 → 任务引擎”页面，必须表达能力结构升级，不得把流程字面化为管道、河流、轨道、物流路径、箭头海洋或底部标签栏。

## 执行日志

每张生成图必须记录真实调用，不根据结果倒推 Prompt：

```markdown
## Page XX
- Page Type:
- MCP tool:
- Model/provider:
- Ratio/size:
- Input reference:
- Strength:
- Exact prompt:
- Output file:
- Result: pass / fail
- Observed problems:
- Next single variable:
```

## 生成后规则

- 先制作整套 contact sheet，再评价统一性。
- contact sheet 必须完整包含所有页面，并按页码标注；禁止只展示部分页面。
- 同步生成图片铺满的 `deck-preview.pptx`，用于统一查看；若未生成，必须在日志中说明原因。
- 单页问题和跨页问题分开记录。
- 一次只修改一个变量。
- 保存失败结果，不用新结果覆盖旧实验记录。
