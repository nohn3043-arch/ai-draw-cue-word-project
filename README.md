# AI Drawing Cue-Word Project

> AI Painting Composition Detail Template — Weight & Ratio Precision Control Edition v2.2 (Universal for All Models)

This repository is a version-controlled export of a quality-control workbook for single- and
multi-character AI image generation. The original is a Tencent Docs spreadsheet; this repo stores
the content as plain CSV (one file per sub-table) plus this README.

## What it is

A practical control desk for building high-consistency character prompts across four prompt syntax families:

- Natural-language flow (Flux / DALL·E 3 / SD3)
- Conversational image models (GPT-4o / Gemini)
- Midjourney / Niji
- Stable Diffusion

v2.2 (vs v2.1) adds: conversational-model rows, affirmative exclusion strategy,
weight→narrative-intensity mapping, reference-image capability matrix, and P0 anchor-reuse checks.

## Sub-tables (in `/sheets`)

| File | Description |
|---|---|
| 使用说明.csv (Instructions) | Workflow, weight semantics, weight→narrative mapping, P0/P1/P2 validation, cross-model red lines |
| 角色锚点.csv (Character Anchors) | Per-character anchor points; anchor weight ≥ 1.6, never replaceable |
| 构图与镜头.csv (Composition & Shots) | Composition types, lens, light, layering, pose templates; multi-character spatial fields |
| 特征细节.csv (Feature Details) | Feature-level descriptors |
| 自然语言叙述模板.csv (NL Narrative Templates) | Assembled prompt templates per syntax family |
| 模型与参考.csv (Models & References) | Model reference-image means & consistency strategy |
| 负面词库.csv (Negative Word Library) | Negative prompts per model (MJ `--no` 4-6 words; SD Negative box; affirmative writing for no-negative models) |
| 校验清单.csv (Checklist) | P0 hard / P1 suggested / P2 optional validation |
| 比例基准表.csv (Ratio Baseline) | Head-body ratio per art style (Q-version 2-3, loli 4-5, girl 6-6.5, youth 6.5-7, adult 7-8, realistic 7.5+); tolerance ≤5% |
| 参考图能力矩阵.csv (Reference Capability Matrix) | Per-model reference-image capability (MJ `--cref`, SD LoRA, Flux Kontext/Redux, GPT-4o/Gemini native, DALL·E 3 none) |
| 生成迭代日志.csv (Generation Iteration Log) | Per-generation iteration records |
| 修改日志.csv (Change Log) | Template revision history |

## Weight semantics (SD / MJ numeric system)

| Range | Meaning | Example |
|---|---|---|
| 1.6 – 2.0 | Hard anchor: absolutely immutable | left under-eye mole (1.8) |
| 1.3 – 1.5 | Core feature: retained across all scenes | light-cyan cotton dress (1.4) |
| 1.0 – 1.2 | Baseline: default strength | gentle quiet temperament (1.0) |
| 0.7 – 0.9 | Ambient aid: adjustable per scene | spring garden (0.8) |
| < 0.7 | Weak hint: easily ignored | breeze (0.5) |

Natural-language models have no numeric weights; map the numeric value to narrative
position/precision (see Instructions sheet).

## Cross-model syntax red lines

- Weight syntax `(word:1.3)` works only in SD; MJ relies on token position & repetition;
  natural-language models forbid bracket weights.
- Negative prompts: MJ `--no` 4-6 short words; SD Negative Prompt box;
  Flux/DALL·E/GPT-4o/Gemini have no negative box → write affirmatively, negate as fallback.
- Reference images: MJ `--cref`; SD LoRA; Flux Kontext/Redux; GPT-4o/Gemini native;
  DALL·E 3 none → description-led (see matrix).
- Anchor reuse: natural-language models must reuse anchor sentences verbatim across images;
  no synonym substitution (e.g. "tear mole" must not become "spot" or "small mole").

## Validation priority

- **P0** — core character settings; failure = wasted image; must regenerate.
- **P1** — image quality & ratio; affects usability; fix first, one retry allowed.
- **P2** — aesthetics & detail; record and improve next round.

## Source

Original Tencent Docs: https://docs.qq.com/sheet/DT05rb0tCVmVSSVpR

## License

Content authorship and license are reserved by the original author. Set an explicit license before redistribution.
