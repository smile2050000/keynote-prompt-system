# 慧雪 X9 Ultra 13 页新版 Storyboard

| 页 | Page Type | Core Message | Audience Question | Dominant Carrier | Spatial Grammar | Distinct From | Special Risk |
|---|---|---|---|---|---|---|---|
|01|Product Launch|一块屏开始照顾每一天|这块屏改变什么|产品+家庭|英雄开放舞台|不做纯产品白底|产品被裁切|
|02|Data Proof|5500万家庭|是否已有真实基础|数字+产品|尺度递进|不做产品英雄|数字错误|
|03|Insight|五口之家的一天|家庭任务如何交错|人物行为|四格时间叙事|不做卡片指标|四图降质|
|04|Scenario Comparison|事务从混乱到接力|为什么需要家庭协作|人物+消息|同场景左右因果|不做时间轴|黑暗表达压力|
|05|Scenario Comparison|作业从家长忙到孩子自主|谁承担作业过程|亲子+产品|同场景前后|不做信息图|产品落地错误|
|06|System|跨端协作产品|三端如何分工|手机/Agent/产品|输入-规划-可视入口|不做普通流程箭头|产品身份漂移|
|07|Demo|消息变成完整作业现场|真实演示如何发生|手机/屏/动作|分段流程|不做九宫格|文字过多|
|08|Capability|家庭事务有人提醒接力|主动协同体现在哪|家庭行为|四节点路径|不做单一场景|节点重复|
|09|System|孩子自主与家长知悉闭环|如何同时守护两端|亲子+产品|中心场景三层环绕|不做标签云|监控感过强|
|10|Capability|成长陪伴与一句话生成应用|AI如何激发成长|孩子行为+界面|左右能力对照|不做幼儿园海报|技能卡同质|
|11|Product Launch|X9 Ultra 是全家主动看护入口|新品定位是什么|产品+三类角色|产品中心辐射|不做规格页|产品与文案重叠|
|12|Product Detail|硬件能力支撑全场景|为什么流畅、清晰、智能|产品+局部细节|四证据区域|不做四张独立产品图|参数乱码|
|13|Ending|一块屏照顾家庭每一天|最后留下什么记忆|产品+家庭|开放舞台收束|呼应第01但更安静|结束页过度拥挤|

产品角色与 Reference 详见 `content-brief.md` 和 `prompt-pack.md`；每页 Prompt 独立注入跨页差异，Image2 不依赖前后页记忆。

## 前 5 页详细编译依据 v2

### Page 01｜一块屏，让家庭AI伙伴开始照顾每一天

#### 内容任务
- Core Message：X9 Ultra 不只是显示信息，而是进入家庭公共空间、开始主动照顾每一天的家庭 AI 入口。
- Audience Memory：这是一台真正进入家庭关系、承担日常照顾的智能屏。
- Audience Question：这块屏究竟为家庭带来了什么改变？

#### 视觉关系
- Page Type：Product Launch
- Visual Strength：Strong
- Evidence Type：产品实物 + 真实家庭使用语境
- Dominant Carrier：完整 X9 Ultra 产品英雄图
- Spatial Grammar：开放舞台中的产品英雄与家庭纵深
- Composition Brief：平视略低机位的宽幅现代客厅。顶部 18% 为连续明亮留白；产品位于中下部偏右，采用右前 3/4 角度，完整落在低矮边柜或桌面上，接触阴影真实。屏幕、双摄、扬声器孔、支架和底部边缘全部可见。背景家庭成员只做自然生活关系，不遮挡产品，不直视镜头。
- Distinct From：本页以产品为唯一第一视觉；禁止使用第 02 页的大数字结构、第 03 页的四格阵列、第 04–05 页的双栏比较结构。

#### 风险与约束
- Special Risk：产品裁切、产品落地、家庭背景抢过产品。
- Product Role：新品英雄与家庭 AI 入口。
- Reference Route：`P0-01.png`，用于右前 3/4 产品身份、结构、比例和材质；`edit_image`，`editMode=reimagine`，`strength=medium`。

### Page 02｜小度已进入超 5500 万家庭

#### 内容任务
- Core Message：5500 万家庭构成小度智能屏进入家庭、服务一老一小的真实规模基础。
- Audience Memory：5500 万不是装饰数字，而是家庭覆盖证据。
- Audience Question：小度智能屏是否已经具备真实而广泛的家庭基础？

#### 视觉关系
- Page Type：Data Proof
- Visual Strength：Strong
- Evidence Type：核心数字 + 产品实物 + 家庭覆盖语义
- Dominant Carrier：超大数字“5500 万”
- Spatial Grammar：数字与产品的尺度递进、证据并置
- Composition Brief：顶部 18% 保留标题安全区。画面左侧约 58% 使用超大“5500 万”作为第一视觉；右侧约 30% 放置一台正面 X9 Ultra，完整站立在桌面上。数字背后或下方以克制的家庭窗格/住宅轮廓密度表达覆盖规模，不生成统计图、地图或第二组数据。说明文字紧邻数字，产品保持第二视觉。
- Distinct From：本页由数字主导，产品只承担可信锚点；禁止复制第 01 页的产品英雄尺度，也禁止采用三栏指标卡或产品家族陈列。

#### 风险与约束
- Special Risk：数字错误、虚构销量/排名、产品抢过数字。
- Product Role：证明 5500 万家庭覆盖的真实产品锚点。
- Reference Route：`P0-05.png`，用于正面产品身份和结构；`edit_image`，`editMode=reimagine`，`strength=low`。

### Page 03｜先看一个五口之家的真实一天

#### 内容任务
- Core Message：一个五口之家的日常由多个时间尺度、家庭角色与责任同时交错组成。
- Audience Memory：家庭需要被照顾的不是单一事件，而是一整天持续发生的事务关系。
- Audience Question：真实家庭的一天里，究竟有多少事情在同时发生？

#### 视觉关系
- Page Type：Insight / Image-led
- Visual Strength：Medium
- Evidence Type：四个真实生活时段
- Dominant Carrier：同一五口之家在四个时段的行为
- Spatial Grammar：四幅等权时间阵列
- Composition Brief：顶部 18% 为标题和副标题安全区；下方横向排列四幅严格等宽、等高、同裁切比例、同圆角、同间距的商业摄影画面。四幅使用同一套家庭人物、同一住宅、同一镜头高度与自然色彩。早晨：父母准备出门，孩子整理书包，老人关注早餐；白天：父母工作，老人处理家务或健康事务；下午：孩子回家、家庭消息和接送安排开始汇聚；晚上：孩子写作业，父母与老人协同陪伴。每幅只保留一个主动作和清楚主体，不塞入多个小场景。
- Distinct From：本页以四幅同等级摄影展开家庭多样性；禁止采用第 02 页的大数字、环形时间轴、错落拼贴或大小混排。

#### 风险与约束
- Special Risk：四图整体降质、人物身份漂移、每格塞入过多动作。
- Product Role：无目标产品。
- Reference Route：无；`generate_image`。

### 第 04、05 页共享 Blueprint

- 输出画布：2048×1152 px，16:9。
- 安全区：左右 128 px；顶部 85 px；底部 75 px。
- 标题区：x=256 px，y=75 px，w=1536 px，h=80 px；上方居中，统一 700 粗体。
- 副标题区：x=341 px，y=171 px，w=1365 px，h=35 px；上方居中，统一 400 常规字重。
- 左侧 Simple Media Frame：x=128 px，y=293 px，w=880 px，h=720 px。
- 右侧 Simple Media Frame：x=1040 px，y=293 px，w=880 px，h=720 px。
- 中间间距：32 px；两个外框顶部、底部、宽度、高度和视觉重量完全一致。
- 外框：16 px 圆角、1 px 中性灰描边、无阴影、无第二层描边。
- 内边距：32 px；图片区 w=816 px、h=480 px、16 px 圆角；图片区不再加边框或底板。
- 图片与说明间距：32 px；说明区主句居中，辅助说明使用中性灰。
- 两页必须复用同一 Blueprint，只改变内容、产品角色和情绪状态，不改变框体几何。

### Page 04｜场景一：家庭事务

#### 内容任务
- Core Message：家庭事务的痛点不只是消息多，而是信息集中在一个人身上；产品介入后，家庭成员共同看见并接力完成。
- Audience Memory：从“一个人记、一个人催”变为“产品让全家共同承担、共同完成”。
- Audience Question：为什么家庭事务总让一个人疲惫，又如何通过产品真正变成家庭协作？

#### 视觉关系
- Page Type：Scenario Comparison
- Visual Strength：Strong
- Evidence Type：同一家庭、同一空间、同一下午的负面状态 → 产品介入后的正面结果
- Dominant Carrier：左侧过载人物情绪；右侧前景 X9 Ultra 与家庭共同注意
- Spatial Grammar：共享 Blueprint 的左右等权因果对照
- Emotional Arc：紧张、孤立、注意力分裂 → 放松、共同注意、责任接力
- Left Affective State：母亲眉头紧、肩膀前倾、视线在手机、纸张和家人之间切换；其他成员没有接住任务，空间关系体现孤立和被追赶。
- Right Affective State：X9 Ultra 位于前景主角位置；家庭成员围绕产品共同确认任务，身体打开、视线集中、有人接过具体任务，情绪是安心和共同完成。
- Solution Carrier：X9 Ultra 是右侧解决结果的第一视觉与可视入口，人物行为作为产品产生协作结果的证据。
- Composition Brief：严格使用共享 Blueprint；左右同一中国家庭、同一现代客厅/餐厅、同一下午、同一人物身份、同一机位。左侧表现母亲独自处理手机、日历、接送和便签，压力由动作、视线和事务密度表达；右侧前景放置右前 3/4 X9 Ultra，完整落在桌面或边柜上，屏幕朝向家庭成员，产品占右侧图片区约 25%–30%，家庭成员位于产品后方或两侧共同确认一个共享任务安排。两侧曝光、白平衡、肤色和彩度完全一致。
- Distinct From：本页只表达“责任集中 → 产品介入后的共同承担”；禁止四格时间阵列、两个软件界面、时间轴、普通卡片对比或把右侧做成无产品的家庭合影。

#### 风险与约束
- Special Risk：左侧用暗化表达压力；右侧产品退居背景；左右变成两个不同家庭。
- Product Role：右侧解决家庭事务问题的主角与共同可视入口。
- Reference Route：`P0-01.png`，用于右前 3/4 产品身份、结构、比例和材质；`edit_image`，`editMode=reimagine`，`strength=medium`。

### Page 05｜场景二：孩子课业

#### 内容任务
- Core Message：X9 Ultra 将作业过程从家长全程忙碌，转变为孩子自主学习、老人轻松陪伴、妈妈安心工作。
- Audience Memory：产品改变的不是一个功能，而是谁来承担作业过程。
- Audience Question：孩子写作业时，能否通过产品不再让家长承担每一个环节？

#### 视觉关系
- Page Type：Scenario Comparison
- Visual Strength：Strong
- Evidence Type：同一家庭作业场景的负面状态 → 产品介入后的正面结果
- Dominant Carrier：左侧家长过载情绪；右侧前景 X9 Ultra 与孩子自主学习行为
- Spatial Grammar：复用第 04 页共享 Blueprint 的左右等权承担者变化对照
- Emotional Arc：焦虑、被监督、作业过程卡住 → 专注、自主、家人被释放
- Left Affective State：母亲不断介入，眉头紧、动作急，孩子被提醒和打断，桌面有多个学习环节但不使用暗色或灰雾。
- Right Affective State：孩子专注而自信，X9 Ultra 成为清晰可见的前景支点；老人平静陪伴，母亲退到背景独立工作，整体情绪是安心、松弛和被支持。
- Solution Carrier：X9 Ultra 是右侧作业过程的第一视觉与可视入口，孩子的自主行为和家人的释放状态证明产品结果。
- Composition Brief：严格复用第 04 页 Blueprint 的全部 2K 几何参数。左侧同一孩子在书桌写作业，母亲同时找作业、打印试卷、播放听力、讲解错题并关注走神；右侧前景放置右前 3/4 X9 Ultra，完整落在书桌上，屏幕朝向孩子，产品占右侧图片区约 25%–30%，不遮挡孩子脸、手或作业本。孩子专注学习，老人位于侧后方轻松陪伴，母亲在背景独立工作。左右家庭身份、空间、机位、曝光、白平衡、肤色和彩度一致。
- Distinct From：本页只表达“家长全程承担 → 产品介入后孩子自主、家人轻松”；禁止复用第 04 页的家庭消息、共享任务板、多乱杂标签或事务接力画面。

#### 风险与约束
- Special Risk：左侧用暗化表达压力；右侧产品不成为主角；产品落地、裁切或遮挡孩子。
- Product Role：右侧孩子自主学习的主角、桌面陪伴和可视操作入口。
- Reference Route：`P0-01.png`，用于右前 3/4 产品身份、结构、比例和材质；`edit_image`，`editMode=reimagine`，`strength=medium`。
