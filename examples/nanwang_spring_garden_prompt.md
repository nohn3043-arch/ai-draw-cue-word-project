# 示例：南望 · 春日花园版 — 四类语法流成品 Prompt

> 本示例演示同一角色设定（**南望 · 素裙花园版 v1.2**，见 `sheets/角色锚点.csv`）在四类语法流下的完整 Prompt 组装。核心规则：**角色锚点句跨图逐字复用，禁止同义改写**。

## 角色锚点摘要（引用自 `sheets/角色锚点.csv`）

| 字段 | 值 |
|---|---|
| 核心身份锚点 (≥1.6) | 16岁少女，左眼角1mm淡褐色泪痣，发间常别白色小雏菊 (1.8) |
| 核心气质标签 (≥1.3) | 柔和安静，微怯生，肢体语言收敛 (1.3) |
| 色彩方案 · 主色 | 浅青色 #A8D8C9 |
| 色彩方案 · 辅助/强调 | 白（雏菊、裙摆暗纹）/ 淡褐（泪痣）、浅粉（唇） |
| 肤色 / 发色 / 瞳色 | 暖白 / 黑发 / 深褐瞳 |
| 使用限制（负面锚定） | 禁止红色系 / 深色系 / 华丽礼服 |

**场景**：春日花园 · 黄昏逆光 · 85mm 人像

---

## 1. 自然语言叙述流（Flux / DALL-E 3 / SD3）

> 组装顺序：【画面总览+景别】→【角色锚点】→【姿态微表情】→【光影色彩】→【背景层次】；禁止权重括号与加号；锚点句置于角色段句首。

一张85mm人像景别平视镜头。16岁少女南望站在春日花园深处。她穿着浅青色棉质素裙，裙摆带有精致的白色雏菊暗纹。她的黑色长直发垂至腰间，发间别着一朵白色小雏菊。她左眼角下方有一颗极细小的淡褐色泪痣。她带着温和安静的表情看向镜头。金黄色的黄昏逆光勾勒出头发与服饰的暖光边框。前景是虚化的白色雏菊花丛，背景是微风拂过的花园围墙。

排异：肯定式写死（裙装已天然排除红裙/皮衣）+ 兜底 `without heavy makeup, no other hair accessories`。

## 2. 对话式图像模型（GPT-4o / Gemini 2.5 Flash Image）

> 首轮给完整描述，后续对话式单点修正；改动只动单点，不动锚点句。

**首轮**：16岁少女南望，浅青色棉质素裙配白色雏菊暗纹，黑长直发及腰，左眼角极细小淡褐色泪痣，发间白色小雏菊，春日花园，黄昏逆光，85mm半身像。

**修正轮**：泪痣再细小一点；裙子保持浅青色不要偏蓝。

## 3. 混合语法 Tag + 参数流（Midjourney v6 / Niji v6）

> 核心锚点放前 20 token；中段叠加景别、光影；末尾统一追加 CLI 参数。

```
16岁少女南望，左眼角淡褐色泪痣，发间白色小雏菊，浅青色棉质素裙，黑色及腰长直发，三分法构图，85mm镜头，侧逆光，黄昏暖光，春日花园，浅景深。 --ar 3:4 --cref https://example.com/nanwang.png --cw 100 --style cute --niji 6
```

`--no` 只筛 4-5 个最高风险词：`--no heavy makeup, red dress, short hair, dark lighting`

## 4. 权重 Tag 流（Stable Diffusion 1.5 / XL / SD3）

> 组装顺序（v2.2）：身份锚点(1.5+) → 核心特征(1.3-1.5) → 姿态/构图 → 光影/氛围(0.7-0.9)。

```
(16yo girl Nanwang:1.2), (mole under left eye:1.5), (single white daisy in hair:1.3), (light mint green plain dress:1.4), (black waist-length straight hair:1.2), rule of thirds, 85mm portrait shot, side-backlighting, golden hour, spring garden, soft bokeh, masterwork, high quality
```

Negative Prompt 框：`(deformed hands, bad anatomy, extra fingers, missing fingers:1.4), (mole under right eye, heavy makeup, red dress, short hair:1.3), (blurry, low quality, watermark, text:1.2)`

---

## 排异机制速查

| 语法流 | 排异方式 |
|---|---|
| 自然语言流 | 首选肯定式写死；否定式兜底 |
| 对话式 | 无负面词概念，对话中直接排除 |
| MJ | `--no` 只筛最高风险词，其余靠 `--cref` 与正面描述兜底 |
| SD | 单独填 Negative Prompt 框 |
