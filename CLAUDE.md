# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A knowledge-only agent plugin, `image-prompt-pack` (one skill: `prompt-pack`). From any intake (article, log, chat history, previous output, short request) the model produces a **Media Brief** (Kịch bản Media) and a **Prompt Pack**: one copy-ready, anti-slop English prompt per image. The plugin never generates images. It ships to Claude Code, Codex and ChatGPT from a single source.

The source of truth for scope and decisions is `specs/001-image-prompt-pack/`: `spec.md` (see its Clarifications section), `plan.md`, `research.md`, `contracts/`, `tasks.md`. Principles are in `.specify/memory/constitution.md`.

## Non-negotiables (from the constitution and clarifications)

- **No code.** Content is Markdown/JSON/YAML only: no scripts, build step, runtime or dependencies.
- **SKILL.md states goals, success criteria, the output contract and when to read each reference.** No numbered step-by-step procedures, no harness-specific tool names, no `${CLAUDE_PLUGIN_ROOT}`-style variables. Reference knowledge by relative path (`references/<file>`) so the same folder works when uploaded to ChatGPT.
- **Output contract** (`specs/002-prompt-pack-optimize/contracts/prompt-pack-output.md` and `contracts/brief-card.md`, which replace 001's sections 1 and 3; v0.3 adds `specs/003-hero-copy-space/contracts/copy-space.md` and `contracts/first-turn.md`): when an intake has a special case (chữ, phong cách, nội dung đặc biệt, format mới lạ; never length or image count alone) the first reply is Kịch bản Media plus a Chốt nhanh block, with no prompts; each image gets one seamless prompt in a code block; the Chữ column holds one text mode per image. Structural slots and preset IDs are not shown to the user. A Reference section appears only when an attached file is needed. A mockup is added only when the user chooses it at the Sản phẩm item of Chốt nhanh or asks for it directly. Hero and share images in mode 2 carry a Vùng chữ block under the prompt.
- **Tool-agnostic prompts.** No per-tool adapters and no `--ar`, `--no` or `::` syntax. No quality buzzwords (8K, masterpiece, ultra-detailed, flawless). Phrase constraints positively.
- **Product mockups only when the user asks for one at that spot.** Then: a real product reference image is required, the AI generates only the scene, people and light, and the pack notes that the real design is composited later and the AI metadata is kept.
- Explanatory text is in Vietnamese with full diacritics. Prompt text is in English.

## Layout (planned; see plan.md › Project Structure)

- `.claude-plugin/marketplace.json` is the Claude marketplace.
- `.agents/plugins/marketplace.json` is the Codex marketplace.
- `plugins/image-prompt-pack/` holds a manifest for each harness:
  - `.claude-plugin/plugin.json`
  - `.codex-plugin/plugin.json`
- `plugins/image-prompt-pack/skills/prompt-pack/` holds:
  - `SKILL.md`
  - `agents/openai.yaml` (Codex metadata)
  - `references/` with `anti-slop.md`, `presets.md` (28 presets, groups R/S/C/E, v0.1 untested), `image-types.md`, `example-pack.md`, `brief-card.md`, `text-in-image.md`
- `tests/fixtures/` holds the sample intakes.
- `tests/acceptance.md` holds the pass/fail criteria for each fixture.
- `tests/runs/` holds dry-run evidence.
- `docs/verification.md` records how far each item has been verified (ĐÃ CHẠY THẬT / ĐỌC MẪU / ĐỌC TÀI LIỆU / CHƯA KIỂM CHỨNG).
- `docs/blind-test.md` holds the preset blind test.

The layout mirrors the team's working `studio-director` plugin (`~/.claude/plugins/marketplaces/studio-director`).

Anti-slop knowledge comes from `D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\01-landscape-tells-anti-slop.md` and `02-prompt-strategy-preset-library.md`. These files are read-only.

## Checks

There is no test suite. Validate by:

1. **Manifest check** (PowerShell, from the repo root). It confirms all 4 manifests are valid JSON, that both `plugin.json` files have the same version, and that `CHANGELOG.md` has a matching entry. Expected output: `OK <version>`. The exact one-liner is in `specs/001-image-prompt-pack/quickstart.md` §1.
2. **Fixture runs.** Run each `tests/fixtures/*` through the skill and grade the result against `tests/acceptance.md` (quickstart §3).
3. **Image quality.** Check generated images against the QC checklist in `references/anti-slop.md`, and run the blind test in `docs/blind-test.md`.

## Release

Bump `version` in both `plugin.json` files and add a `## [x.y.z]` entry to `CHANGELOG.md`. Users install and update through the Git marketplace URL `https://github.com/mktphuchung-wq/Image-Prompt-Packs.git`:

- Claude: `/plugin marketplace add mktphuchung-wq/Image-Prompt-Packs`, then `/plugin install image-prompt-pack@image-prompt-packs`.
- Codex: add a `[marketplaces.image-prompt-packs]` git source in `~/.codex/config.toml`.

## Spec Kit workflow

Feature work uses the `/speckit-*` skills in `.claude/skills/`. The active feature directory is recorded in `.specify/feature.json`.
