# Implementation Plan: Vùng chữ dựng sẵn cho hero + khâu khởi tạo theo trường hợp đặc biệt

**Branch**: `mktphuchung-wq/Feature` (feature dir `003-hero-copy-space`) | **Date**: 2026-11-19 | **Spec**: [spec.md](./spec.md)

**Input**: `specs/003-hero-copy-space/spec.md` (Clarifications 2026-11-19: dừng hỏi theo trường hợp đặc biệt;
mục Banner 4 điểm; chốt format qua bảng; không vẽ sơ đồ ký tự)

## Summary

Nâng plugin `image-prompt-pack` từ 0.2.1 lên **0.3.0**, chỉ sửa tri thức và mô tả kỹ năng:

1. **Vùng chữ dựng sẵn** cho ảnh chế độ 2 (FR-201…FR-214): prompt dựng bố cục banner (chủ thể một phía,
   vùng chữ phía còn lại) bằng một trong ba cách — (a) khoảng trống thật, (b) làm mềm hậu cảnh nhẹ,
   (c) mảng phẳng; pack có khối **Vùng chữ** dưới prompt; cột Chữ ghi vị trí; chế độ 3/4 dùng lại vùng.
   Ngoại lệ bokeh có giới hạn ghi trong `anti-slop.md`.
2. **Khâu khởi tạo theo trường hợp đặc biệt** (FR-215…FR-220): thay điều kiện dừng theo số ảnh/độ dài
   (002) bằng 4 trường hợp kích hoạt (chữ, phong cách, nội dung đặc biệt, format mới lạ); mục **Banner**
   4 điểm; chốt format các ảnh khác qua bảng Kịch bản Media, sửa theo số dòng.

## Technical Context

**Language/Version**: Markdown, JSON, YAML. Không ngôn ngữ lập trình.

**Primary Dependencies**: Không.

**Storage**: N/A.

**Testing**: Fixture + `tests/acceptance.md` phần v0.3; chạy thử khô; lệnh kiểm manifest (`OK 0.3.0`);
tạo ảnh thật cho SC-202 (người chạy).

**Target Platform**: Claude Code, Codex, ChatGPT.

**Project Type**: Plugin tri thức (skill + references), marketplace Git.

**Performance Goals**: Lượt đầu không dừng khi intake không có trường hợp đặc biệt (SC-206); chốt trong một
câu trả lời (SC-207).

**Constraints**: `SKILL.md` hiện 138 dòng, giới hạn ~150 → phần mới trong `SKILL.md` chỉ là tiêu chí ngắn,
chi tiết đặt ở `text-in-image.md` và `brief-card.md`; được phép rút gọn câu cũ trùng lặp trong `SKILL.md`
để giữ ≤ ~150. Không quy trình đánh số, không tên công cụ, không thuật ngữ thông số máy ảnh (f-stop, khẩu
độ). Prompt chế độ 2 vẫn 30–80 từ.

**Scale/Scope**: Sửa 6 file trong skill, thêm 3 fixture, cập nhật acceptance/docs/CHANGELOG/manifest/
metadata/README/CLAUDE.md.

## Constitution Check

| Nguyên tắc | Kiểm | Kết quả |
|---|---|---|
| I. Mục tiêu cốt lõi | Sửa đúng lỗi thật (hero không có chỗ chữ, người dùng tưởng thiếu chữ) và tăng chất lượng khâu khởi tạo | ĐẠT |
| II. Đơn giản | Không script; thêm 3 fixture và 2 mục tri thức; không file reference mới | ĐẠT |
| III. Năng lực model | Cách tạo vùng chữ và việc phát hiện trường hợp đặc biệt là phán đoán của model dựa trên tiêu chí + ví dụ, không thủ tục | ĐẠT |
| IV. Đa harness | Toàn văn bản; "dừng hỏi" vẫn có đường lui "đưa luôn"/không có người trả lời | ĐẠT |
| V. Marketplace | 0.3.0 ở hai `plugin.json` + CHANGELOG; metadata cập nhật | ĐẠT |

**Post-design re-check**: ĐẠT. Không cần Complexity Tracking.

## Project Structure

### Documentation (this feature)

```text
specs/003-hero-copy-space/
├── plan.md · research.md · data-model.md · quickstart.md
├── contracts/
│   ├── copy-space.md        # Hợp đồng prompt chế độ 2 + khối Vùng chữ
│   └── first-turn.md        # Hợp đồng lượt đầu: trường hợp kích hoạt, mục Banner, chốt format qua bảng
└── tasks.md
```

### Source Code (repository root) — file bị đổi/thêm

```text
plugins/image-prompt-pack/
├── .claude-plugin/plugin.json · .codex-plugin/plugin.json   # 0.3.0 + mô tả nêu vùng chữ
├── README.md
└── skills/prompt-pack/
    ├── SKILL.md                    # SỬA: tiêu chí dừng theo trường hợp đặc biệt; vùng chữ; mẫu đầu ra có khối Vùng chữ
    ├── agents/openai.yaml          # SỬA nhẹ mô tả nếu cần
    └── references/
        ├── text-in-image.md        # SỬA: mục "Dựng vùng chữ" (a/b/c), mẫu khối Vùng chữ, chế độ 3/4 dùng lại vùng, 3 ví dụ mới
        ├── brief-card.md           # SỬA: 4 trường hợp kích hoạt thay bảng dừng cũ; mục Banner 4 điểm; chốt format qua bảng
        ├── anti-slop.md            # SỬA: ngoại lệ bokeh cạnh tell + mục QC
        ├── image-types.md          # SỬA: vị trí vùng chữ theo khung ngang/dọc; "format mới lạ" = không có trong bảng
        └── example-pack.md         # SỬA: Ví dụ A lượt 1 có mục Banner; hero chế độ 2 có khối Vùng chữ; sửa theo số dòng
.agents/plugins/marketplace.json · .claude-plugin/marketplace.json   # mô tả nêu vùng chữ (giữ cấu trúc)
tests/fixtures/
├── 07-crowded-hero-request.md      # MỚI: hero cảnh chợ đông, không bề mặt trơn → cách (b)
├── 08-carousel-request.md          # MỚI: carousel 5 slide → format mới lạ, phải dừng
└── 09-clear-request.md             # MỚI: 3 ảnh minh họa đã chốt chữ/phong cách → xuất luôn
tests/acceptance.md                 # SỬA: phần v0.3
tests/runs/2026-11-19-v0.3/         # MỚI
docs/verification.md · docs/blind-test.md · CHANGELOG.md · README.md · CLAUDE.md
```

**Structure Decision**: Không thêm reference mới; vùng chữ thuộc `text-in-image.md`, khâu khởi tạo thuộc
`brief-card.md`.

## Complexity Tracking

Không có vi phạm.
