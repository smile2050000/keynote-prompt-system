# V1 Image2 Prompt Schema

本文件只定义 Prompt 的组装方式，不重复风格和页面类型规则。

## Global Visual Contract

整套 Deck 只定义一次，控制在 8–12 条：

```text
16:9 与发布会定位
唯一 Style Lock
整体气质与视觉尺度
色彩、背景、光线与摄影
Typography 角色与文字反差
产品和人物原则
信息密度与视觉中心
3–5 个最高风险禁止项
```

## Per-page Prompt

每页按以下顺序编译：

```text
生成一张完整的 16:9 发布会 PPT 页面，画面和准确文字一次生成。

[原样复用 Global Visual Contract]

Page Type: [页面类型]
Title Structure: [上方居中 / 左右结构 / 金句居中]
Visual Mode: [仅信息页填写]
Core Message: [一个核心信息]
Visual Relationship: [一个内容驱动的主关系]
Exact Text: [逐字标题、数字、标签]
Reference: [无 / Style / Product；路径与用途]
Must Preserve: [2–5 个事实或产品硬约束]
Page-specific Quality: [选择一个短后缀]
Avoid: [当前页最关键的 3–5 个风险]
```

逐页 Prompt 不重新定义风格，不发送内部推理、验收清单或设计原因。

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

## 页面类型后缀

每页只选一个，不叠加全部后缀。

**场景摄影**

```text
premium commercial lifestyle photography, professional art direction, accurate perspective, clear midtones, crisp material detail, realistic skin and fabric, controlled highlights, no haze, no synthetic CGI look
```

**产品融合**

```text
the product is physically present in the environment, matched perspective, scale, focus, lighting and color temperature, real contact surface and shadow, natural occlusion, preserve exact product identity
```

**信息设计**

```text
premium keynote information design, content-driven visual hierarchy, precise alignment, restrained depth, generous negative space, no template dashboard, no decorative technology effects
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

- 制作包含全部页面和页码的 `montage-all.png`。
- 同步生成图片铺满的 `deck-preview.pptx`。
- 单页问题与跨页问题分开记录。
- 保存失败结果，一次只修改一个变量。
