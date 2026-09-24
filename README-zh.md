# AI 绘画提示词工程模板库

> AI 绘画构图细节模板 —— 权重与比例精确控制版 v2.8（全模型适配：设定层通用，语法层分模型）

本仓库是一份 AI 图像 / 视频 / 3D 生成质量控制工作簿的版本化导出。原始文件为腾讯文档表格，本仓库以纯 CSV 格式（每个子表一个文件）存储，外加本说明文档。

## 这是什么

一个用于构建**高一致性角色提示词**的实操控制台，覆盖五大提示词语法体系：

- 自然语言流（Flux / DALL·E 3 / SD3）
- 对话式图像模型（GPT-4o / Gemini）
- Midjourney / Niji
- Stable Diffusion
- 国内 API 模型（即梦 / 可灵 / 豆包 / 通义万相）

### v2.8 主要更新

数据标准与交互工作台分离。21 张 CSV 数据表保持不变；Cloudflare Pages 工作台（[www.nohnlins.com/ai-draw/](https://www.nohnlins.com/ai-draw/)）升级漫画模式：支持拖放上传 Word/TXT，mammoth.js 解析 .docx，自动节拍拆分，跨 4 个模型族逐格提示词组装，气泡配置自动化，P0 时序一致性清单自动生成。企业 IP 预设库升级支持 JSON 导入导出与 localStorage 持久化。

更多版本历史见 `sheets/ChangeLog.csv`。

## 快速开始

1. **锚定角色** — 在 `sheets/CharacterAnchors.csv` 中填写角色锚点（硬锚权重 ≥ 1.6，不可替换）。
2. **选择模型与参考策略** — 在 `sheets/ModelsAndReferences.csv` 与 `ReferenceImageCapabilityMatrix.csv` 中确定目标模型与一致性方法（MJ `--cref` / SD LoRA / Flux Kontext / 对话式参考）。
3. **组装提示词** — 按 `sheets/NaturalLanguagePromptTemplate.csv` 中的优先级构建（硬锚 → 核心特征 → 基线描述 → 氛围）；跨模型语法注意「跨模型语法红线」。
4. **校验** — 用 `sheets/Checklist.csv` 跑 P0/P1/P2；多角色场景追加 `MultiCharacterSpatialRelations.csv`，漫画场景追加 `PanelLayoutRules.csv` / `SpeechBubblePositioning.csv` / `TemporalConsistencyChecklist.csv`。
5. **记录迭代** — 每次生成记入 `sheets/GenerationIterationLog.csv`；同类失败连续 3 次后切换模型或参数路线。

完整示例见 [`examples/nanwang_spring_garden_prompt.md`](examples/nanwang_spring_garden_prompt.md)（同一角色设定在 4 种语法流下的成品提示词）。

## 子表一览（`/sheets` 目录）

> 文件名已统一为英文以便 GitHub 渲染，括号内为原始中文名。全部 21 张表与此前中文导出一一对应。

| 文件 | 说明 |
|---|---|
| `Usage.csv`（使用说明） | 工作流、权重语义、权重→叙述映射、P0/P1/P2 校验、跨模型红线 |
| `CharacterAnchors.csv`（角色锚点） | 各角色锚点；锚权重 ≥ 1.6，永不替换 |
| `CompositionAndShots.csv`（构图与镜头） | 构图类型、镜头、光影、分层、姿势模板；多角色空间字段 |
| `FeatureDetails.csv`（特征细节） | 特征级描述词 |
| `NaturalLanguagePromptTemplate.csv`（自然语言叙述模板） | 各语法族组装提示词模板 |
| `ModelsAndReferences.csv`（模型与参考） | 模型参考图手段与一致性策略 |
| `NegativeWordBank.csv`（负面词库） | 各模型负面提示词（MJ `--no` 4-6 词；SD Negative 框；无负面框模型用肯定写法） |
| `Checklist.csv`（校验清单） | P0 硬校验 / P1 建议 / P2 可选 |
| `AspectRatioBaselines.csv`（比例基准表） | 各画风头身比（Q版 2-3、萝莉 4-5、少女 6-6.5、少年 6.5-7、成年 7-8、写实 7.5+）；容差 ≤5% |
| `ReferenceImageCapabilityMatrix.csv`（参考图能力矩阵） | 各模型参考图能力（MJ `--cref`、SD LoRA、Flux Kontext/Redux、GPT-4o/Gemini 原生、DALL·E 3 无） |
| `GenerationIterationLog.csv`（生成迭代日志） | 每次生成的迭代记录 |
| `VideoGenerationPromptTemplate.csv`（视频生成模板） | 各模型视频提示词语法（Sora/可灵/Runway/Pika/国内 API）含运镜、时序结构、跨帧锚点一致性 |
| `MultiCharacterSpatialRelations.csv`（多角色空间关系） | 3+ 角色空间排布、深度分层、视线链、互动链、遮挡规则、尺度透视 |
| `LoRAManagement.csv`（LoRA管理） | LoRA 类型分类（角色/风格/服装/概念/背景）、权重范围、冲突检测、叠加顺序、跨模型适用性 |
| `ThreeDGenerationMatrix.csv`（3D生成矩阵） | 各模型 3D 生成能力（Meshy/Tripo3D/Rodin/混元3D-2/Stable Fast3D/CRM）——输入格式、输出格式、纹理、拓扑、身份一致性 |
| `ConversationalEditChain.csv`（对话式编辑链） | GPT-4o/Gemini 逐轮单点修正协议；锚点边界规则；各轮失败处理 |
| `PanelLayoutRules.csv`（面板排布规则） | 5 种漫画版式（4格/6格/电影条/跨页/竖屏条漫）——格子排布、宽高比、构图法则、角色站位、背景连续性、提示词组装、视觉节奏控制、常见失败 |
| `SpeechBubblePositioning.csv`（对话气泡定位） | 7 种气泡类型（普通对白/内心独白/旁白/音效/低语/喊叫/电子音）——尾巴方向、位置规则、大小规则、文本容量、形状与风格、重叠规则、层级优先级、提示词组装、常见失败 |
| `TemporalConsistencyChecklist.csv`（时序一致性验收） | 6 大类 13 项校验（角色身份/空间/时序/动作/表情/服装道具）——严重度 P0/P1/P2、检查时机、校验方法、通过标准、失败标准、修复协议 |
| `StoryboardSkeletonTemplate.csv`（分镜骨架模板） | 漫画分镜骨架——10 种格子职能、3 条镜头连续性规则、4 种页面版式；每行含提示词组装规则、连续性校验、常见失败 |
| `ChangeLog.csv`（修改日志） | 模板修订历史 |

## 权重语义（SD / MJ 数值体系）

| 区间 | 含义 | 示例 |
|---|---|---|
| 1.6 – 2.0 | 硬锚：绝对不可变 | 左眼下泪痣 (1.8) |
| 1.3 – 1.5 | 核心特征：所有场景保留 | 浅青色棉麻连衣裙 (1.4) |
| 1.0 – 1.2 | 基线：默认强度 | 温柔安静的气质 (1.0) |
| 0.7 – 0.9 | 氛围辅助：按场景可调 | 春日庭院 (0.8) |
| < 0.7 | 弱提示：易被忽略 | 微风 (0.5) |

自然语言模型无数值权重；将数值映射为叙述位置/精度即可（见使用说明表）。

## 跨模型语法红线

- 权重语法 `(词:1.3)` 仅在 SD 有效；MJ 靠 token 位置与重复；自然语言模型禁用括号权重。
- 负面提示词：MJ `--no` 4-6 个短词；SD Negative Prompt 框；Flux/DALL·E/GPT-4o/Gemini 无负面框 → 以肯定写法为主，否定作兜底；国内 API 模型各有差异，以官方文档为准。
- 参考图：MJ `--cref`；SD LoRA；Flux Kontext/Redux；GPT-4o/Gemini 原生；DALL·E 3 无（多图系列已不推荐）→ 以描述为主；国内 API 模型见能力矩阵。
- 锚点复用：自然语言模型必须跨图**逐字复用**锚点句子，不得用同义词替换（如「泪痣」不能换成「斑点」或「小痣」）。

## 校验优先级

- **P0** — 角色核心设定；失败 = 废图，必须重生成。
- **P1** — 画质与比例；影响可用性，优先修正，允许一次重试。
- **P2** — 美学与细节；记录并在下一轮改进。

## 来源

原始腾讯文档：https://docs.qq.com/sheet/DT05rb0tCVmVSSVpR

## 许可

基于 Apache License 2.0 授权。参见 [LICENSE](LICENSE)。
版权所有 © 2026 NOHN AI TECHNOLOGY PTE LTD。联系邮箱：ai@nohnlins.com。
