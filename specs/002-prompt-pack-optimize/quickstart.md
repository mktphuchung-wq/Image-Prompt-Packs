# Quickstart: Kiểm chứng Prompt Pack v0.2

Dựa trên `specs/001-image-prompt-pack/quickstart.md` (cài đặt, lệnh kiểm manifest). Chỉ ghi phần mới.

## 1. Manifest

Chạy lệnh ở quickstart 001 §1. Kỳ vọng: `OK 0.2.0`.

## 2. Cập nhật plugin

Claude Code: `/plugin marketplace update image-prompt-packs`. Codex: mở phiên mới sau khi git source
được kéo lại. Kiểm `SKILL.md` đã có mục Chốt nhanh và hai reference mới.

## 3. Kịch bản v0.2

| # | Đầu vào | Kỳ vọng (đầy đủ ở `tests/acceptance.md` phần v0.2) |
|---|---|---|
| A | `tests/fixtures/05-christmas-article.md` + "làm prompt ảnh cho bài này" | Lượt 1: Chốt nhanh ở đầu (4 mục, mục 3 nêu 2 chỗ chờ sản phẩm, mặc định không), Kịch bản Media có đủ cột mới, **không có prompt**, dừng chờ |
| B | trả "ok" sau A | Pack theo mặc định; mọi prompt 30–80 từ, ≤ 5 vật, không số chẵn, ảnh đời thường có vật lạc đề + dấu vết người, không từ cấm, ảnh không chữ có câu chặn chữ; bảng đạt FR-108; hero chế độ 2 chèn chữ sau; không mockup/"Bonus" |
| C | sau B: "hero cho AI vẽ luôn tiêu đề Indoor Christmas Decorations" | Chỉ prompt hero đổi; có chuỗi trong ngoặc kép, kiểu chữ theo đặc điểm, nền tương phản, lề an toàn, "appears once; no other text anywhere" |
| D | sau B: "mục 3 chọn có" | Thêm prompt mockup cho 2 chỗ, Reference bắt buộc, nhãn "chờ sản phẩm xác minh" |
| E | `tests/fixtures/06-staged-images-feedback.md` | Chẩn đoán nêu đúng nguyên nhân [R03] mục A; prompt sửa đạt tự kiểm |
| F | `tests/fixtures/02-one-line-request.md` (3 ảnh) | Xuất luôn, khối "Đã dùng mặc định" ở đầu, không dừng |
| G | sau B: "đổi sang hướng biên tập chuyên nghiệp" | Chỉ prompt bị ảnh hưởng đổi; dùng tinh thần nhóm E; vẫn đạt FR-101/102/104/105 |

Chạy A–G trên Claude Code, Codex, ChatGPT (SC-104, kiểm hành vi dừng chờ giữa harness).

## 4. Ảnh thật

1. Tạo ảnh từ pack B trên công cụ đang dùng; so cạnh 3 ảnh cũ trong blind test (`docs/blind-test.md`,
   SC-103).
2. Tạo hero ở C 5 lần, kiểm QC chữ (SC-106).
