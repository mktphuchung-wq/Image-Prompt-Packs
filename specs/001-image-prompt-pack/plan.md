# Implementation Plan: Image Prompt Pack Plugin

**Branch**: `mktphuchung-wq/Feature` (feature dir `001-image-prompt-pack`) | **Date**: 2026-11-18 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `specs/001-image-prompt-pack/spec.md`

## Summary

Plugin dùng chung cho Claude Code, Codex và ChatGPT. Từ bất kỳ intake nào (bài viết, log, lịch sử,
output trước, yêu cầu ngắn), model tạo **Kịch bản Media** và **Prompt Pack**: mỗi ảnh một prompt liền
mạch copy dùng ngay, chống slop, chạy trên mọi công cụ tạo ảnh. Plugin không tạo ảnh.

Cách làm: plugin là **một skill duy nhất** (`prompt-pack`) gồm `SKILL.md` nêu mục tiêu, tiêu
chuẩn và hợp đồng đầu ra, cùng 4 file tri thức trong `references/` (chống slop + QC, preset R/S/C,
loại ảnh, ví dụ mẫu). Không có script, build hay runtime. Repo gốc vừa là marketplace Claude
(`.claude-plugin/marketplace.json`) vừa là marketplace Codex (`.agents/plugins/marketplace.json`),
cài qua link Git `https://github.com/mktphuchung-wq/Image-Prompt-Packs.git`. ChatGPT dùng chính thư
mục skill đó (tải lên dạng skill hoặc đính kèm vào Project). Cấu trúc theo mẫu đã chạy được của
plugin `studio-director` của team.

## Technical Context

**Language/Version**: Markdown (CommonMark/GFM) cho skill và tri thức; JSON cho manifest; YAML cho
`agents/openai.yaml`. Không có ngôn ngữ lập trình.

**Primary Dependencies**: Không. Chỉ dựa vào harness: Claude Code plugin system, Codex plugin system,
ChatGPT Skills/Projects.

**Storage**: N/A. Không lưu dữ liệu người dùng; đầu ra chỉ trong hội thoại, hoặc file khi người dùng
yêu cầu và harness cho ghi (FR-014).

**Testing**: Kiểm thủ công theo kịch bản: 4 intake mẫu trong `tests/fixtures/` chạy trên từng
harness, đối chiếu tiêu chí đạt trong `tests/acceptance.md`; blind test preset theo
`docs/blind-test.md` (SC-003); checklist QC (SC-008). Kiểm máy chỉ gồm: JSON hợp lệ và phiên bản khớp
giữa các manifest (lệnh một dòng trong quickstart, không thêm file script).

**Target Platform**: Claude Code (CLI/desktop/IDE), Codex (CLI/app), ChatGPT (Skills hoặc Projects).

**Project Type**: Plugin tri thức cho agent (skill + references), phân phối qua marketplace Git.

**Performance Goals**: Prompt Pack cho bài ~1.500 từ trong < 3 phút (SC-001); phụ thuộc model,
plugin chỉ cần giữ `SKILL.md` gọn để không tốn context.

**Constraints**: `SKILL.md` ≤ ~150 dòng; mỗi file references ≤ ~300 dòng; tổng tri thức nạp khi chạy
nhỏ để hợp với giới hạn context của cả ba harness. Không chứa adapter theo công cụ tạo ảnh (FR-012).
Không hướng dẫn thủ tục từng bước (Constitution III).

**Scale/Scope**: 1 plugin, 1 skill, 4 file tri thức, 24 preset (R12/S8/C4), khoảng 7 loại ảnh,
4 intake mẫu.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Nguyên tắc | Kiểm | Kết quả |
|---|---|---|
| I. Bám mục tiêu cốt lõi | Mọi file phục vụ intake → Kịch bản Media → Prompt Pack hoặc sửa prompt. Không gọi API tạo ảnh (FR-013). Mockup chỉ khi người dùng yêu cầu (FR-020). | ĐẠT |
| II. Đơn giản trước | Chỉ Markdown/JSON/YAML; 1 skill; không script, build, dependency; kiểm manifest bằng lệnh một dòng thay cho bộ test code. | ĐẠT |
| III. Năng lực model, không procedure | `SKILL.md` viết theo Mục tiêu → Tiêu chí thành công → Hợp đồng đầu ra → Tri thức tham chiếu → Ranh giới; preset/template là tri thức để model tự chọn, không phải biểu mẫu bắt buộc (FR-007, FR-009). | ĐẠT |
| IV. Chạy trên nhiều harness | Một thư mục skill dùng chung; manifest riêng Claude/Codex chỉ là vỏ mỏng; ChatGPT dùng cùng thư mục skill. References nằm trong thư mục skill để gói ChatGPT tự đủ. | ĐẠT |
| V. Marketplace Git repo | Repo gốc chứa cả hai marketplace manifest; semver đồng bộ ở 2 `plugin.json`; `CHANGELOG.md`. | ĐẠT (ChatGPT là đường lui, đã ghi trong spec Assumptions) |

**Post-design re-check (sau Phase 1)**: vẫn ĐẠT. Thiết kế không thêm file nào ngoài cấu trúc dưới đây;
`agents/openai.yaml` là metadata Codex bắt buộc tối thiểu, không chứa nội dung.

## Project Structure

### Documentation (this feature)

```text
specs/001-image-prompt-pack/
├── plan.md              # File này
├── research.md          # Phase 0
├── data-model.md        # Phase 1
├── quickstart.md        # Phase 1
├── contracts/
│   ├── prompt-pack-output.md   # Hợp đồng đầu ra cho người dùng
│   ├── skill-interface.md      # Cách gọi skill trên từng harness, mô tả kích hoạt
│   └── plugin-manifests.md     # Trường bắt buộc của marketplace/plugin manifest
└── tasks.md             # Phase 2 (/speckit-tasks)
```

### Source Code (repository root)

```text
.claude-plugin/
└── marketplace.json                  # Marketplace Claude Code
.agents/plugins/
└── marketplace.json                  # Marketplace Codex
plugins/image-prompt-pack/
├── .claude-plugin/plugin.json        # Manifest Claude (version X.Y.Z)
├── .codex-plugin/plugin.json         # Manifest Codex (cùng version)
├── README.md                         # Plugin làm gì, ví dụ câu gọi
└── skills/prompt-pack/
    ├── SKILL.md                      # Mục tiêu, tiêu chí, hợp đồng đầu ra, ranh giới
    ├── agents/openai.yaml            # Metadata hiển thị cho Codex
    └── references/
        ├── anti-slop.md              # Mục tiêu chống slop, bảng 11 tell + đối phó, quy tắc viết prompt, checklist QC
        ├── presets.md                # 24 preset R/S/C (v0.1 chưa test) + slot biến thiên
        ├── image-types.md            # Loại ảnh theo kênh: hero, inline, infographic, social/OG, thumbnail, mockup…
        └── example-pack.md           # 1 ví dụ Kịch bản Media + Prompt Pack hoàn chỉnh, 1 ví dụ sửa prompt
docs/
├── blind-test.md                     # Quy trình blind test 5 người (SC-003) + bảng ghi kết quả
└── verification.md                   # Mức kiểm chứng từng hạng mục (mẫu studio-director)
tests/
├── fixtures/
│   ├── 01-blog-article.md            # Bài blog ~1.500 từ (US1)
│   ├── 02-one-line-request.md        # Yêu cầu một câu (US2)
│   ├── 03-messy-log.md               # Log hội thoại nhiều chủ đề (US2)
│   └── 04-failed-image-feedback.md   # Prompt + mô tả lỗi ảnh (US3)
├── acceptance.md                     # Tiêu chí đạt/không đạt cho từng fixture, ánh xạ FR/SC
└── runs/                             # Bằng chứng chạy thử theo ngày/harness
README.md                             # Giới thiệu + cài/cập nhật trên Claude, Codex, ChatGPT
CHANGELOG.md                          # Ghi chú thay đổi theo phiên bản (FR-019)
```

**Structure Decision**: Một repo vừa là marketplace vừa chứa plugin, theo đúng mẫu `studio-director`
(đã được cấu hình git marketplace trong `~/.codex/config.toml` và Claude `known_marketplaces.json` của
người dùng). Toàn bộ nội dung model cần nằm trong `skills/prompt-pack/` để ba harness dùng
chung một nguồn. `docs/` và `tests/` phục vụ người duy trì, không được skill nạp.

## Complexity Tracking

Không có vi phạm constitution cần biện minh.
