# Quickstart: Kiểm chứng v0.3.0

Cài đặt và lệnh kiểm manifest: `specs/001-image-prompt-pack/quickstart.md` (kỳ vọng `OK 0.3.0`).

## Kịch bản

| # | Đầu vào | Kỳ vọng (đầy đủ ở `tests/acceptance.md` phần v0.3) |
|---|---|---|
| H | `tests/fixtures/05-christmas-article.md` + "làm prompt ảnh cho bài này" | Dừng: Chốt nhanh có mục Banner 4 điểm (a–d), mục Sản phẩm (2 chỗ chờ), mỗi mục có lý do; bảng có cột Chữ "2 chèn chữ sau — <vị trí>"; dòng hướng dẫn sửa theo số dòng; không prompt |
| I | "ok" sau H | Hero prompt chế độ 2: vị trí chủ thể + vùng chữ + cách tạo + tông; 30–80 từ; khối Vùng chữ đủ trường; câu "ảnh cố ý không có chữ" |
| J | "ảnh 3 đổi 4:5, bỏ ảnh 5, còn lại ok" sau H | Chỉ hai thay đổi đó được áp |
| K | `tests/fixtures/07-crowded-hero-request.md` | Dừng (chữ); vùng chữ mặc định cách (b) làm mềm hậu cảnh; prompt không có "bokeh"/thông số máy ảnh |
| L | `tests/fixtures/08-carousel-request.md` | Dừng với mục "format mới lạ" có lý do |
| M | `tests/fixtures/09-clear-request.md` | Không dừng; pack xuất ngay, "Đã dùng mặc định" ở đầu |
| N | Sau I: "hero cho AI vẽ luôn tiêu đề" | Bố cục và vùng chữ giữ nguyên; tiêu đề đặt trong vùng |

## Ảnh thật

Tạo 5 ảnh từ prompt hero ở I, đặt tiêu đề rộng ~40% vào vùng chữ: ≥ 4/5 không che chủ thể, đọc được ở
~360 px (SC-202). Ghi vào `docs/verification.md`.
