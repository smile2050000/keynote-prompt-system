# keynote-prompt-system

把单个 PPT 需求文件整理为：

- `content-brief.md`：内容和叙事地图；
- `storyboard.md`：逐页内容任务、观众问题、证据类型、主视觉载体、空间语法与风险；
- `global-visual-contract.md`：整套共享视觉规则；
- `prompt-pack.md`：逐页 Image2 提示词。

当前版本：`v0.9.3`

本包是 v0.9.1 之后的流程校准版，包含后续对 Storyboard、Prompt 编译、产品 Reference、MCP 路由和 QA 的修正。不要与 2026 年 8 月 20 日分发的旧 v0.9.1 包混用。

## v0.9.1 → v0.9.3

- Storyboard 增加内容任务、视觉关系、产品约束和风险规划；
- Prompt 增加具体构图、产品/人物/场景关系和跨页差异；
- 每页完整注入 Global Visual Contract，禁止用简称代替；
- 固定 Image2 整页生图，明确 `generate_image` / `edit_image` 路由；
- 强化产品镜头、朝向、数量、尺度和外观保真；
- 优化现代家居与浅紫高端女性风格的摄影、布光和材质；
- QA 增加文字、产品、全局规则和 Storyboard 检查，只定点重生问题页；
- 每轮独立建档，历史内容默认不继承，并补充团队使用与排查说明。

## 职责边界

`keynote-prompt-system` 负责需求理解、页面阅读任务、视觉规范和提示词规划。

- `image2`：按本 Skill 编译出的最终 Prompt 执行生成或编辑图片；实际执行只走 `image_mcp_demo`；
- `slides`：在用户确认图片后封装 PPTX，并做渲染和溢出检查。

PPTX 是可选下游产物，由 `slides` / `ppt` Skill 在用户明确需要时封装，不属于本 Skill 的固定规划产出。

规划阶段不会自动调用生图 MCP。用户确认风格、颜色、整体感觉并明确说“开始生成”后，才进入执行阶段。

## 输入

支持 `txt`、`md`、`html`、`docx`、`pdf`、`pptx`、截图和其他可读取文本格式。默认只处理一个主要需求文件；其他文件需用户明确说明为参考材料。

## 每轮独立开始

每轮任务都新建独立运行目录，重新建立本轮来源，重新编写 `content-brief.md`、`storyboard.md`、`global-visual-contract.md` 和 `prompt-pack.md`。历史项目的 Prompt、Storyboard、视觉规则、图片和 QA 默认不继承；只有用户明确指定为本轮 Reference 时才使用。

## 团队使用方法

### 1. 安装

注意：只把 ZIP 解压到桌面或其他工作目录，不会替换 Codex 正在加载的旧 Skill。安装时必须替换实际加载目录，不能只保留一个并列的新文件夹，也不能形成嵌套目录。

Codex 实际加载目录：

`/Users/smile/.codex/skills/keynote-prompt-system/`

推荐安装步骤：

1. 将现有目录备份或改名为 `keynote-prompt-system-v0.9.1-backup`；
2. 将本包中的 `keynote-prompt-system-v0.9.3` 文件夹复制为 `keynote-prompt-system`；
3. 确认 `/Users/smile/.codex/skills/keynote-prompt-system/VERSION` 内容为 `0.9.3`；
4. 新建对话或重新触发一次 Skill，让 Codex 重新加载版本。

正确结构应为：

```text
/Users/smile/.codex/skills/keynote-prompt-system/SKILL.md
/Users/smile/.codex/skills/keynote-prompt-system/VERSION
/Users/smile/.codex/skills/keynote-prompt-system/references/
```

不要出现以下嵌套结构：

```text
/Users/smile/.codex/skills/keynote-prompt-system/keynote-prompt-system-v0.9.3/
```

可直接发给 Codex 的安装话术：

```text
请安装最新的 keynote-prompt-system v0.9.3。

源包：
/Users/smile/Desktop/PPT生图尝试/keynote-prompt-system-v0.9.3/

目标目录：
/Users/smile/.codex/skills/keynote-prompt-system/

要求：
1. 先检查目标目录当前版本；
2. 将旧版本目录备份为 keynote-prompt-system-v0.9.1-backup；
3. 用源包完整替换目标目录，不要形成嵌套目录；
4. 确认目标目录中的 VERSION 为 0.9.3；
5. 检查 SKILL.md、README.md、TUTORIAL.md 和 references/ 均存在；
6. 不修改其他 Skill；
7. 完成后报告实际加载路径、版本号和安装结果。
```

安装后可用以下话术验证：

```text
请验证当前实际加载的 keynote-prompt-system 是否为 v0.9.3。

检查：
- 实际加载路径；
- VERSION 内容；
- README 是否包含 v0.9.1 → v0.9.3 升级说明；
- README 是否包含安装、先规划后生成、MCP 路由和结果不一致排查说明；
- 是否存在嵌套目录；
- 是否仍残留旧版本文件影响触发。

只报告检查结果，不要修改文件。
```

### 2. 先规划，后生成

规划请求示例：

```text
使用 keynote-prompt-system，把这份需求整理为 content-brief.md、storyboard.md、global-visual-contract.md 和 prompt-pack.md，先不要生图。
```

确认规划文件无误后，再明确说：

```text
按已确认的 Prompt 开始生成，使用 image_mcp_demo，记录每页实际 provider、model、capability、尺寸和输出路径。
```

不要直接调用 image2 代替规划流程，也不要在没有确认 Reference 和风格契约时直接批量生成。

### 3. Reference 路由

- 无目标产品或本地输入图：使用 `image_mcp_demo.generate_image`；
- 有产品 Reference、已有页面图或其他本地输入图：使用 `image_mcp_demo.edit_image`；
- 产品 Reference 只用于识别产品，不把六面图、产品接触表或多角度阵列直接放进最终画面；
- 不得静默更换 provider、model、通道、尺寸或 preset。

每页执行日志至少记录：`skill_version`、`prompt_source`、`capability`、`provider`、`model`、`ratio`、`size`、`reference_paths`、`output_path`。

### 4. 结果不一致时先检查

如果团队生成结果与本机样张差异很大，按以下顺序排查：

- 是否真的加载了 `/Users/smile/.codex/skills/keynote-prompt-system/` 中的 `0.9.3`；
- 是否先生成了 `storyboard.md` 和 `global-visual-contract.md`；
- 是否使用了同一份最终 Prompt，而不是旧的 `prompt-pack.md`；
- 是否使用了相同的 `generate_image` / `edit_image` 路由、Reference、preset、ratio 和尺寸；
- 是否出现了本机专属的绝对路径，导致团队机器找不到产品 Reference；
- 是否把随机生成差异误判为流程差异。相同参数也不保证像素级复现，但产品身份、页面类型、整体色调和构图逻辑应保持一致。

若 MCP 返回错误，保留真实错误并停止该页，不要自动切换到其他生图通道。

## 当前设计原则

- 家用智能产品采用“浅色/深色基础版 + 气质变体”；家庭浅色默认风格为 canonical ID `neutral-modern-home`，`neutral-home-keynote` 仅作为兼容别名，温馨由生活关系而非黄色滤镜表达；
- 页面按观众阅读任务分类，而不是按装饰分类；
- 全套页面共享整体气质、标题层级、色彩边界和叙事节奏，不强制逐页母型；
- 人物不是默认主视觉，但按内容自然使用；留白和节奏作为软约束；
- Image2 的中文、排版和产品一致性风险暂记录，不在 v0.5 强行解决。

首轮生成后统一制作 Contact Sheet，并在 `qa/qa.md` 中建立全页验收账本；问题详情只记录明显问题页。修正默认采用定点重生，不全套重跑。图片版通过 QA 后，可按需将批准图、Storyboard、准确文字和共享视觉规则交给可编辑重建流程。
