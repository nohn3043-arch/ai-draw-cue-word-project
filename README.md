# AI Drawing Cue-Word Project

> AI Painting Composition Detail Template — Weight & Ratio Precision Control Edition v2.5 (Adaptable Across All Models: setting-layer universal, syntax-layer per-model)

This repository is a version-controlled export of a quality-control workbook for single- and
multi-character AI image, video, and 3D generation. The original is a Tencent Docs spreadsheet;
this repo stores the content as plain CSV (one file per sub-table) plus this README.

## What it is

A practical control desk for building high-consistency character prompts across five prompt syntax families:

- Natural-language flow (Flux / DALL·E 3 / SD3)
- Conversational image models (GPT-4o / Gemini)
- Midjourney / Niji
- Stable Diffusion
- Domestic API models (Jimeng / Kling / Doubao / Tongyi Wanxiang)

v2.5 (vs v2.4) adds: 5 new sheets covering previously uncovered generation modalities —
video generation (Sora/Kling/Runway/Pika/domestic API with camera movement and temporal structure),
multi-character spatial relations (3+ characters with depth layering, gaze chain, interaction chain),
LoRA management (character/style/outfit/concept/background types with conflict detection and stacking order),
3D generation matrix (Meshy/Tripo3D/Rodin/Hunyuan3D-2/Stable Fast3D/CRM), and
conversational edit chain (round-by-round single-point fix protocol for GPT-4o/Gemini with anchor boundary rules).
Total sheet count 12→17.
v2.4 (vs v2.3) adds: a posture-to-emotion reference table (Section D in Composition & Shots),
mapping character temperament labels to pose/gaze/center-of-gravity combinations. Also
adds a per-character posture-difference field for dual-character scenes.
v2.3 (vs v2.2) adds: a domestic API-family syntax flow, a DALL·E 3 deprecation note,
and an honest Adaptable framing.

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
| 视频生成模板.csv (Video Generation Template) | Per-model video prompt syntax (Sora/Kling/Runway/Pika/domestic API) with camera movement, temporal structure, and cross-frame anchor consistency |
| 多角色空间关系.csv (Multi-Character Spatial Relations) | 3+ character spatial arrangement, depth layering, gaze chain, interaction chain, occlusion rules, scale perspective |
| LoRA管理.csv (LoRA Management) | LoRA type classification (character/style/outfit/concept/background), weight ranges, conflict detection, stacking order, cross-model applicability |
| 3D生成矩阵.csv (3D Generation Matrix) | Per-model 3D generation capability (Meshy/Tripo3D/Rodin/Hunyuan3D-2/Stable Fast3D/CRM) — input format, output format, texture, topology, identity consistency |
| 对话式编辑链.csv (Conversational Edit Chain) | Round-by-round single-point fix protocol for GPT-4o/Gemini; anchor boundary rules; failure handling per round |
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
  Flux/DALL·E/GPT-4o/Gemini have no negative box → write affirmatively, negate as fallback;
  domestic API models: negative-prompt support varies, check official docs.
- Reference images: MJ `--cref`; SD LoRA; Flux Kontext/Redux; GPT-4o/Gemini native;
  DALL·E 3 none (deprecated for multi-image series) → description-led;
  domestic API models: capability per official docs (see matrix).
- Anchor reuse: natural-language models must reuse anchor sentences verbatim across images;
  no synonym substitution (e.g. "tear mole" must not become "spot" or "small mole").

## Validation priority

- **P0** — core character settings; failure = wasted image; must regenerate.
- **P1** — image quality & ratio; affects usability; fix first, one retry allowed.
- **P2** — aesthetics & detail; record and improve next round.

## Source

Original Tencent Docs: https://docs.qq.com/sheet/DT05rb0tCVmVSSVpR

## License

Licensed under the Apache License 2.0. See [LICENSE](LICENSE).
Copyright (c) 2026 NOHN AI TECHNOLOGY PTE LTD. Contact: ai@nohnlins.com.
