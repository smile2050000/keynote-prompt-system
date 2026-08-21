# 杨柳前 5 页统一生图执行日志

## 健康测试
- MCP tool: `mcp__image_mcp_demo__generate_image`
- Provider: `T8Star`
- Model: `gpt-image-2`
- Ratio / size: `16:9 / 1536×864`
- Preset: `1k`
- Reference: 无
- Output: `output/yangliu-first5/health-test/2026-08-20T12-09-37-222Z-生成一张-16-9-的最小健康测试图-明亮纯净的中性白发布会背景-清晰中间调-中央一-1.png`
- Result: pass

## Page 01
- Page Type: Cover
- MCP tool / provider / model: `mcp__image_mcp_demo__generate_image` / `T8Star` / `gpt-image-2`
- Ratio / size / preset: `16:9 / 2048×1152 / 2k`
- Reference: 无
- Output: `output/yangliu-first5/generated-2k-v2/page-01-2k-v2.png`
- Result: pass
- Observed: 家庭全景、标题上方居中、人物行为自然；未出现摄像机实物。

## Page 02
- Page Type: Scenario Comparison
- MCP tool / provider / model: `mcp__image_mcp_demo__generate_image` / `T8Star` / `gpt-image-2`
- Ratio / size / preset: `16:9 / 2048×1152 / 2k`
- Reference: 无
- Output: `output/yangliu-first5/generated-2k-v2/page-02-2k-v2.png`
- Result: pass with QA note
- Observed: 同一客厅左右对照成立；模型额外生成了“环境舒适、老人看电视、孩子写作业、宠物休息”等白色信息小卡片，属于未要求的额外模块，且底部标签出现黑色胶囊容器。
- Next single variable: 后续重生只收紧“只允许平面文字标注，不生成任何白色信息卡片或胶囊”。

## Page 03
- Page Type: Feature / Editorial Diagram
- MCP tool / provider / model: `mcp__image_mcp_demo__generate_image` / `T8Star` / `gpt-image-2`
- Ratio / size / preset: `16:9 / 2048×1152 / 2k`
- Reference: 无
- Output: `output/yangliu-first5/generated-2k-v2/page-03-2k-v2.png`
- Result: pass with text QA note
- Observed: 中心汇聚关系成立，未做五张等大卡片；部分任务词被模型改写或丢失，需逐字核对。

## Page 04
- Page Type: Data Proof
- MCP tool / provider / model: `mcp__image_mcp_demo__generate_image` / `T8Star` / `gpt-image-2`
- Ratio / size / preset: `16:9 / 2048×1152 / 2k`
- Reference: 无
- Output: `output/yangliu-first5/generated-2k-v2/page-04-2k-v2.png`
- Result: pass with major QA note
- Observed: 数字主视觉、蓝色重点色和行为证据切片成立；模型自行生成了未提供的桌面设备和设备界面，违反“无 Reference 不出现具体产品外观”约束；底部出现额外关系线。
- Next single variable: 后续重生明确“行为证据只能是人物/家庭场景照片，禁止任何设备、屏幕、摄像机或产品界面”。

## Page 05
- Page Type: System
- MCP tool / provider / model: `mcp__image_mcp_demo__generate_image`
- Provider / model: `T8Star` / `gpt-image-2`
- Ratio / size / preset: `16:9 / 2048×1152 / 2k`
- Reference: 无
- Output: `output/yangliu-first5/generated-2k-v2/page-05-2k-v2.png`
- Result: pass with QA note
- Observed: 三阶段输入→理解→行动关系清楚；模型使用了轻微立体阶梯台面，仍接近开放舞台，但后续可收紧为纯平面阶梯，避免被理解为第三种容器。

## 统一 QA 结论

- 实际 provider/model 全程保持 `T8Star / gpt-image-2`，未切换通道。
- 五页均为 `16:9`、`2048×1152`，无生成失败。
- 页面差异已经出现，但 Image2 仍可能自行添加信息模块或产品实物；后续应优先加强页面级硬约束，而不是继续增加共享规则长度。
- 本轮未覆盖旧版目录和旧版产物。
