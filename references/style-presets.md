# Style Presets

一个 Deck 只激活一个 `style_id`，不得混搭。这里是风格选择的唯一入口；每个 Preset 都包含色彩、空间、材质、光线、排版倾向、适用场景和最高风险，但不规定具体页面内容或图表结构。

## 使用状态

- `validated`：已在完整项目中验证，可直接选用。
- `project-validated`：已在单一项目中完成端到端验证，可选用，但应保留 Contact Sheet QA。
- `experimental`：只有规则草案或局部页面测试，不作为默认推荐；用户明确选择后才使用，并先做 1–2 页试样。

## A｜neutral-modern-home｜中性现代家居

```yaml
style_id: neutral-modern-home
status: validated
best_for: 家用智能硬件、家庭陪伴、看护、桌面智能屏、新品发布
```

- 70% 中性白、浅灰和柔和灰白；20% 浅灰木色、织物和真实家居材质；10% 深色产品、深石墨文字及产品屏幕原生暖色。产品颜色始终服从真实 Reference。
- 温馨来自人物行为、产品作用和家庭关系，不来自黄色滤镜、木色铺满或昏黄灯光。
- 使用清洁自然日光、完整中间调和中性灰接触阴影；家居空间开阔、现代、克制。
- 产品清晰、高对比、真实材质，是稳定视觉锚点；信息页采用平面编辑化语言。
- 最高风险：黄金时刻、奶油家居广告、棕黄阴影、软装堆积、产品低对比、整套都落入真实客厅。

兼容别名：`neutral-home-keynote`、`warm-home-editorial`。

## B｜nordic-urban-family｜现代北欧都市家庭

```yaml
style_id: nordic-urban-family
status: project-validated
best_for: 都市家庭智能产品、空间型产品发布、年轻品质生活叙事
```

- 现代北欧建筑骨架叠加年轻都市设计感，并保留柔软舒适的家庭触感。
- 冷白墙面、雾灰、浅白蜡木少量点缀；拉丝铝、银色金属、玻璃、石材与现代艺术构成清爽空间。
- 以模块化家具、柔软织物和真实生活动作建立亲和感；产品自然进入住宅、书房或共享起居空间。
- 光线清透、偏中性，可有克制的冷暖对照；排版保持现代无衬线、大留白和清晰产品层级。
- 最高风险：日式原木禅意、侘寂、暖黄滤镜、样板房空洞感、把家庭感做成软装堆砌。

## C｜lavender-premium-women｜浅紫高端女性消费

```yaml
style_id: lavender-premium-women
status: validated
best_for: 女性向陪伴设备、闺蜜机、审美消费产品、轻奢新品发布
```

- 浅紫、白和银灰为基底；紫色只承担视觉重点，不做大面积渐变。
- 质感来自克制留白、细腻材质、低反射金属和柔和但清晰的光线，不靠梦幻特效。
- 排版轻盈、优雅、秩序明确；产品与人物关系偏精致日常，而非甜美装饰。
- 最高风险：梦幻光球、粉紫渐变泛滥、少女化图标、过度蕾丝化或美妆广告化。

## D｜young-urban-consumer-tech｜年轻都市消费电子

```yaml
style_id: young-urban-consumer-tech
status: project-validated
best_for: 桌面智能音箱、个人消费电子、年轻用户产品、轻生活方式发布
```

- 白、浅灰和清透蓝为主，可使用一个小面积活力色作为语义重点。
- 场景是年轻都市住宅、书房、设计工作桌或轻社交空间；产品要自然、好用且具设计感。
- 材质偏金属、玻璃、亚克力和低反射哑光表面；排版利落、轻快，信息关系直接。
- 最高风险：颜色过多、玩具化、互联网海报感、贴纸元素堆积、背景抢过产品。

## E｜dark-tech-keynote｜深色科技发布会

```yaml
style_id: dark-tech-keynote
status: experimental
best_for: 夜间看护、技术架构、安防能力、沉浸式新品发布
```

- 深石墨、黑曜和冷白文字为基底，清透蓝/青色或少量真实产品暖色承担强调。
- 深色来自连续空间、受控光线和清晰层级，而不是黑色异形块、发光网格或赛博特效。
- 人物、产品和核心图形必须明亮可辨；信息页仍保持编辑化、可阅读的关系设计。
- 首次用于项目时，先生成 1–2 页试样并通过 Contact Sheet 检查后再扩展全套。
- 最高风险：纯黑压暗、发光科技模板、文字透视、强分割展板、无语义 3D 雕塑。

## 迁移规则

- 旧 `neutral-home-keynote-dark` 不再作为独立主风格；需要深色科技方向时改用 `dark-tech-keynote`，并遵守其 `experimental` 试样要求。
- 旧 `designed-keynote-stage` 不再作为用户可选主风格；它是可被各风格按页面需要调用的“发布会构图倾向”，不是独立色彩和材质系统。
- `palette-systems.md` 仅保留历史兼容信息，不能再作为 Style Preset 选择来源。

## Style Lock

```yaml
style_scope: whole-deck
style_mix: forbidden
```

Page Type 和 Visual Mode 只能改变信息表达，不得改写 Active Style。
