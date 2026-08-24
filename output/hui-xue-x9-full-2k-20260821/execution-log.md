# 慧雪 X9 Ultra 13 页 2K 执行日志

## 健康测试
- MCP tool: `mcp__image_mcp_demo__generate_image`
- Provider / model: `T8Star / gpt-image-2`
- Ratio / size: `16:9 / 1536×864`
- Preset: `1k`
- Reference: 无
- Output: `health-test/2026-08-21T03-05-45-372Z-生成一张-16-9-的最小健康测试图-明亮纯净的中性白发布会背景-清晰中间调-中央一-1.png`
- Result: pass

## 正式生成

统一参数：`16:9 / 2048×1152 / preset=2k / PNG`。实际 provider/model 全程为 `T8Star / gpt-image-2`。

| Page | Route | Reference | Output | Result |
|---|---|---|---|---|
|01|edit_image|P0-01 右前 3/4|generated-2k/page-01-2k.png|pass|
|02|edit_image|P0-05 正面|generated-2k/page-02-2k.png|pass|
|03|generate_image|无|generated-2k/page-03-2k.png|pass|
|04|generate_image|无|generated-2k/page-04-2k.png|pass with QA note|
|05|edit_image|P0-01 右前 3/4|generated-2k/page-05-2k.png|pass with QA note|
|06|edit_image|P0-02 右前产品角度|generated-2k/page-06-2k.png|pass|
|07|edit_image|P0-08 低角度/屏幕识别|generated-2k/page-07-2k.png|pass|
|08|edit_image|P0-03 左前 3/4|generated-2k/page-08-2k.png|pass|
|09|edit_image|P0-04 + P0-06 结构参考|generated-2k/page-09-2k.png|pass|
|10|generate_image|无|generated-2k/page-10-2k.png|pass|
|11|edit_image|P0-01 右前 3/4|generated-2k/page-11-2k.png|pass|
|12|edit_image|P0-03 + P0-04|generated-2k/page-12-2k.png|pass with QA note|
|13|edit_image|P0-03 左前 3/4|generated-2k/page-13-2k.png|pass|

## 真实错误记录

首次产品页调用返回真实错误：`MCP error -32602: Input validation error: Invalid arguments for tool edit_image ... inputImagePaths ... expected array to have >=1 items`。未切换 provider、model 或通道；随后按当前工具要求将主 Reference 同时放入 `inputImagePaths` 重试成功。

## 产物

- Contact Sheet：`contact-sheet-2k.png`
- PPTX：`慧雪_X9_Ultra_13页_2K_图片版.pptx`
- PPTX PDF 渲染：`rendered-pptx/慧雪_X9_Ultra_13页_2K_图片版.pdf`
- PPTX 渲染 Contact Sheet：`rendered-pptx-contact-sheet.png`

## 前 5 页 Prompt 审核修订（2026-08-21）

- 废弃旧版 `prompt-pack.md`，本轮审核以 `prompt-pack-first5-review-v2.md` 为准，暂未调用 Image2。
- 第 04、05 页补齐左右对比的正负情绪、产品解决结果主角关系、单层 Simple Media Frame 几何参数和同曝光约束。
- 第 04、05 页统一使用 `edit_image` + `P0-01.png`；第 03 页统一为无 Reference 的 `generate_image`，与正文“直接生成”保持一致。
- 第 04、05 页复用同一 2K 双栏 Blueprint：两个 `880×720 px` 外框，`x=128/1040`、`y=293`、间距 `32 px`、圆角 `16 px`、`1 px` 描边、`32 px` 内边距。

## 新版 Prompt Pack 真实生图测试（2026-08-21）

### 健康测试
- Tool：`mcp__image_mcp_demo__generate_image`
- Provider / model：`T8Star / gpt-image-2`
- Ratio / size：`16:9 / 1536×864`
- Preset：`1k`
- Result：pass
- Output：`health-test-new/2026-08-21T07-12-38-397Z-生成一张最小健康测试图-完整16-9发布会页面-明亮纯净的中性白背景-清晰中间调-中-1.png`

### 前 5 页 2K 输出
统一：`16:9 / 2048×1152 / PNG / T8Star / gpt-image-2`

| Page | Route | Reference | Output |
|---|---|---|---|
|01|`edit_image`|`P0-01.png`，右前 3/4|`generated-first5-v2/2026-08-21T07-15-47-298Z-生成一张完整的-16-9-中文发布会-ppt-页面-当前使用-image2-整页生图-1.png`|
|02|`edit_image`|`P0-05.png`，正面|`generated-first5-v2/2026-08-21T07-17-17-451Z-生成一张完整的-16-9-中文发布会-ppt-页面-当前使用-image2-整页生图-1.png`|
|03|`generate_image`|无|`generated-first5-v2/2026-08-21T07-14-45-881Z-生成一张完整的-16-9-中文发布会-ppt-页面-当前使用-image2-整页生图-1.png`|
|04|`edit_image`|`P0-01.png`，右前 3/4|`generated-first5-v2/2026-08-21T07-16-40-631Z-生成一张完整的-16-9-中文发布会-ppt-页面-当前使用-image2-整页生图-1.png`|
|05|`edit_image`|`P0-01.png`，右前 3/4|`generated-first5-v2/2026-08-21T07-14-02-201Z-生成一张完整的-16-9-中文发布会-ppt-页面-当前使用-image2-整页生图-1.png`|

- Contact Sheet：`contact-sheet-first5-v2.png`

## Prompt 权重收敛修订 v3（2026-08-21）

- 基线：保留 `prompt-pack-first5-review-v2.md` 及本轮 5 张真实输出不变。
- 新稿：`prompt-pack-first5-review-v3.md`，尚未调用 Image2。
- 仅调整两类信号：空间主材继续以白灰为主，木色降为小面积点缀；逐页页面质量增加“关键主体清晰度优先于背景/道具丰富度”。
- 未改变 Storyboard、准确文字、构图 Blueprint、人物关系、产品 Reference、调用路由、`editMode` 或 `strength`。

## Prompt v3 真实生图测试（2026-08-21）

### 健康测试
- Tool：`mcp__image_mcp_demo__generate_image`
- Provider / model：`T8Star / gpt-image-2`
- Ratio / size：`16:9 / 1536×864`
- Preset：`1k`
- Result：pass
- Output：`health-test-v3/2026-08-21T08-21-15-588Z-生成一张最小健康测试图-完整16-9发布会页面-明亮纯净的中性白与浅灰背景-清晰中间-1.png`

### 前 5 页 2K 输出
统一：`16:9 / 2048×1152 / PNG / T8Star / gpt-image-2`

| Page | Route | Reference | Output |
|---|---|---|---|
|01|`edit_image`|`P0-01.png`，右前 3/4|`generated-first5-v3/2026-08-21T08-25-07-149Z-生成一张完整的-16-9-中文发布会-ppt-页面-当前使用-image2-整页生图-1.png`|
|02|`edit_image`|`P0-05.png`，正面|`generated-first5-v3/2026-08-21T08-24-24-599Z-生成一张完整的-16-9-中文发布会-ppt-页面-当前使用-image2-整页生图-1.png`|
|03|`generate_image`|无|`generated-first5-v3/2026-08-21T08-23-41-644Z-生成一张完整的-16-9-中文发布会-ppt-页面-当前使用-image2-整页生图-1.png`|
|04|`edit_image`|`P0-01.png`，右前 3/4|`generated-first5-v3/2026-08-21T08-27-02-257Z-生成一张完整的-16-9-中文发布会-ppt-页面-当前使用-image2-整页生图-1.png`|
|05|`edit_image`|`P0-01.png`，右前 3/4|`generated-first5-v3/2026-08-21T08-26-11-789Z-生成一张完整的-16-9-中文发布会-ppt-页面-当前使用-image2-整页生图-1.png`|

- Contact Sheet：`contact-sheet-first5-v3.png`

## 第 01 页执行优化版单页测试（2026-08-24）

- Prompt：`prompt-page01-execution-optimized-v1.md`
- Tool：`mcp__image_mcp_demo__edit_image`
- Provider / model：成功结果均为 `T8Star / gpt-image-2`
- Reference：`P0-01.png`，右前 3/4
- 参数：`editMode=reimagine`、`strength=medium`、`16:9`、`2K`、`2048×1152`
- 首轮并行 3 次：2 次成功，1 次真实错误 `mcp_workspace_route_unavailable`
- 同参数补试：成功，补齐第 3 张
- 输出目录：`generated-page01-optimized-v1/`
- Contact Sheet：`contact-sheet-page01-optimized-v1-3x.png`
- 初步观察：三张图的产品完整度、标题留白和摄影清晰度较稳定；木质桌面/柜体仍有模型默认倾向，说明单页执行优化版提升了优先级，但没有完全改变家庭空间材质先验。

## 第 01 页执行优化版 v2 三方向测试（2026-08-24）

- Prompt：`prompt-page01-execution-optimized-v2-options.md`
- Tool：`mcp__image_mcp_demo__edit_image`
- Provider / model：成功结果均为 `T8Star / gpt-image-2`
- Reference：`P0-01.png`，右前 3/4
- 参数：`editMode=reimagine`、`strength=medium`、`16:9`、`2K`、`2048×1152`
- A、B 首轮成功；C 首轮真实错误：`mcp_upstream_connection_failed`（未收到上游 HTTP 响应），使用相同参数重试成功。
- 输出目录：`generated-page01-options-v2/`
- Contact Sheet：`contact-sheet-page01-options-v2.png`

## 执行优化层修订：连续标题背景（2026-08-24）

- 已同步更新 `prompt-page01-execution-optimized-v1.md` 与 `prompt-page01-execution-optimized-v2-options.md`。
- 新增约束：标题区与室内场景使用同一连续背景；标题直接叠加，不生成白色横条、标题底板、不透明色块、圆角白色卡片、页面外框或黑色外部背景。
- 本次只处理标题背景/画布连续性，未修改摄影、室内设计、人物脚本、产品 Reference 或调用参数。
- 尚未重新生图，等待下一轮摄影方向讨论后再测试。

## 第 01 页 B/C 版本 4K 测试（2026-08-24）

- Prompt：`prompt-page01-execution-optimized-v2-options.md` 的 B、C 版本。
- Tool：`mcp__image_mcp_demo__edit_image`
- Provider / model：`T8Star / gpt-image-2`
- Reference：`P0-01.png`，右前 3/4
- 参数：`editMode=reimagine`、`strength=medium`、`16:9`、`preset=4k`
- 实际返回尺寸：B、C 均为 `3072×1728`，不是请求文本中的 `4096×2304`；按 MCP 实际返回记录。
- 输出目录：`generated-page01-options-v2-4k/`
- Contact Sheet：`contact-sheet-page01-options-v2-4k.png`

## 执行方向确认（2026-08-24）

- 用户选定：B｜广告强化版。
- 后续生图与 Prompt 编译暂以 B 的商业摄影和高端科技住宅方向为基线。
- 暂不自动扩展到全套页面，也不混入 C 的逐条脚本强化规则。
