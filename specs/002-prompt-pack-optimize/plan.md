# Implementation Plan: Prompt Pack v0.2 — chống ảnh dàn dựng, chế độ chữ, Chốt nhanh

**Branch**: `mktphuchung-wq/Feature` (feature dir `002-prompt-pack-optimize`) | **Date**: 2026-11-18 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `specs/002-prompt-pack-optimize/spec.md`

## Summary

Nâng plugin `image-prompt-pack` từ 0.1.0 lên 0.2.0 bằng cách **chỉ sửa nội dung tri thức và mô tả
kỹ năng**, không thêm code. Bốn thay đổi chính:

1. **Tự kiểm trước khi xuất** (FR-101…FR-106) và **bảng đa dạng cấp pack** (FR-107, FR-108) viết thành
   tiêu chí trong `SKILL.md` + quy tắc chi tiết trong `references/anti-slop.md`; thêm 4 tell (FR-109).
2. **Chốt nhanh** (FR-110…FR-116): reference mới `references/brief-card.md`; `SKILL.md` đổi thứ tự đầu
   ra (Chốt nhanh ở đầu, dừng chờ khi bài dài hoặc ≥ 4 ảnh). Hướng hình do model chọn và ghi rõ, gồm
   cả hướng chuyên nghiệp/thời trang → thêm nhóm preset **E (biên tập/chuyên nghiệp, 4 preset)**.
3. **Chế độ chữ** (FR-117…FR-125): reference mới `references/text-in-image.md` (5 chế độ, quy tắc,
   QC chữ); mặc định hero/OG/thumbnail = chèn chữ sau.
4. **Mockup có xác nhận** (FR-126…FR-128): sửa `anti-slop.md` mục 5 và Ranh giới trong `SKILL.md`.

Kèm fixture bài Giáng sinh thật + fixture ba ảnh lỗi, acceptance v0.2, chạy thử khô, version 0.2.0.

## Technical Context

**Language/Version**: Markdown, JSON (manifest), YAML (`agents/openai.yaml`). Không ngôn ngữ lập trình.

**Primary Dependencies**: Không. Hệ thống plugin của Claude Code, Codex; ChatGPT Skills/Projects.

**Storage**: N/A.

**Testing**: Kiểm thủ công theo fixture + `tests/acceptance.md` (phần v0.2); lệnh kiểm manifest của
quickstart 001 (kỳ vọng `OK 0.2.0`); đếm từ/đếm vật trên văn bản prompt do người kiểm hoặc model tự
kiểm; blind test so sánh v0.2 với ba ảnh cũ (SC-103).

**Target Platform**: Claude Code, Codex, ChatGPT.

**Project Type**: Plugin tri thức cho agent (skill + references), phân phối qua marketplace Git.

**Performance Goals**: Phản hồi đầu (Kịch bản Media + Chốt nhanh) ngắn, không kèm prompt; pack ra trong
một lượt sau "ok" (SC-104).

**Constraints**: `SKILL.md` ≤ ~150 dòng (hiện 93); mỗi reference ≤ ~300 dòng; không quy trình đánh số
bước; không tên công cụ tạo ảnh/thiết kế; khối prompt không chứa nhãn khe hay preset ID (giữ từ 001).

**Scale/Scope**: Sửa 6 file trong skill (SKILL.md, anti-slop, image-types, presets, example-pack,
openai.yaml không đổi), thêm 2 reference, thêm 2 fixture, cập nhật acceptance/docs/CHANGELOG/manifest,
cập nhật CLAUDE.md.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Nguyên tắc | Kiểm | Kết quả |
|---|---|---|
| I. Bám mục tiêu cốt lõi | Mọi thay đổi nhắm đúng 4 lỗi của lượt chạy thật; vẫn không tạo ảnh. Nhóm preset E phục vụ trực tiếp Clarification Q1 (hướng chuyên nghiệp/thời trang). | ĐẠT |
| II. Đơn giản trước | Không script, không build. Tiêu chí đếm là tiêu chí tự kiểm cho model và người nghiệm thu. Thêm 2 reference là để giữ `SKILL.md` ngắn. | ĐẠT |
| III. Năng lực model, không procedure | Chốt nhanh và tự kiểm viết thành tiêu chí ("phản hồi đầu gồm…", "mỗi prompt có…"), không "Bước 1…". Hướng hình do model chọn theo loại bài. | ĐẠT — rủi ro: tiêu chí nhiều dễ thành làm theo hình thức; giảm bằng ví dụ trong `example-pack.md` và quy tắc chọn vật lạc đề theo ngữ cảnh |
| IV. Chạy trên nhiều harness | Hai reference mới nằm trong thư mục skill; hành vi "dừng chờ" có đường lui khi không có người trả lời (FR-114). Phải kiểm cả 3 harness. | ĐẠT |
| V. Marketplace Git repo | Version 0.2.0 ở hai `plugin.json` + CHANGELOG. | ĐẠT |

**Post-design re-check**: vẫn ĐẠT. Không có vi phạm cần ghi Complexity Tracking.

## Project Structure

### Documentation (this feature)

```text
specs/002-prompt-pack-optimize/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   ├── prompt-pack-output.md   # Hợp đồng đầu ra v0.2 (thay contracts 001 §1 về thứ tự và cột)
│   └── brief-card.md           # Hợp đồng khối Chốt nhanh
└── tasks.md                    # /speckit-tasks
```

### Source Code (repository root) — chỉ liệt kê file bị đổi/thêm

```text
plugins/image-prompt-pack/
├── .claude-plugin/plugin.json          # version 0.2.0
├── .codex-plugin/plugin.json           # version 0.2.0
├── README.md                           # thêm 2 reference, nhóm E
└── skills/prompt-pack/
    ├── SKILL.md                        # SỬA: tiêu chí tự kiểm, Chốt nhanh, chế độ chữ, mockup, đầu ra mới
    └── references/
        ├── anti-slop.md                # SỬA: §2 tự kiểm + từ cấm, §3 thêm 4 tell (15), §4 đa dạng cấp pack, §5 mockup có xác nhận, §6 trỏ QC chữ
        ├── brief-card.md               # MỚI: Chốt nhanh — khi dừng/không dừng, 4 mục, mặc định, hướng hình, mẫu
        ├── text-in-image.md            # MỚI: 5 chế độ chữ, quy tắc từng chế độ, tiếng Việt, alt, QC chữ
        ├── image-types.md              # SỬA: thay mục "Ảnh có chữ" bằng chế độ chữ mặc định theo loại ảnh; cột Hướng hình gợi ý
        ├── presets.md                  # SỬA: thêm nhóm E (4); thêm cột/ghi chú nhiệt độ ánh sáng, loại khung vào bảng slot
        └── example-pack.md             # SỬA: Ví dụ A theo đầu ra v0.2; Ví dụ B sửa ảnh dàn dựng
tests/
├── fixtures/
│   ├── 05-christmas-article.md         # MỚI: bài "Indoor Christmas Decorations" của lượt test (có 2 chỗ chờ sản phẩm)
│   └── 06-staged-images-feedback.md    # MỚI: 3 prompt cũ + mô tả 3 ảnh lỗi
├── acceptance.md                       # SỬA: thêm phần v0.2 (US1–US4 của 002)
└── runs/2026-11-18-v0.2/               # MỚI: bằng chứng chạy thử khô v0.2
docs/
├── verification.md                     # SỬA: thêm dòng v0.2
└── blind-test.md                       # SỬA: thêm so sánh v0.2 vs 3 ảnh cũ (SC-103), nhóm E
CHANGELOG.md                            # SỬA: mục [0.2.0]
CLAUDE.md                               # SỬA: hợp đồng đầu ra trỏ contracts 002, thêm reference mới
```

**Structure Decision**: Giữ nguyên cấu trúc 001. Hai reference mới thay vì nhồi vào `SKILL.md` (FR-131,
research R1 của 002). Spec/contracts 001 giữ làm lịch sử; các điểm bị thay đã ghi ở spec 002.

## Complexity Tracking

Không có vi phạm constitution cần biện minh.
