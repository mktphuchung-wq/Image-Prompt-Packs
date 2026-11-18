# Data Model: Prompt Pack v0.2

Chỉ ghi phần **thêm/đổi** so với `specs/001-image-prompt-pack/data-model.md`. Không có schema máy.

## Khối Chốt nhanh (mới)

| Trường | Bắt buộc | Quy tắc |
|---|---|---|
| trạng thái | có | `đang chờ` (dừng, chưa có prompt) hoặc `đã dùng mặc định` (pack xuất cùng lượt) — FR-110, FR-114 |
| mục 1 Hướng hình | khi intake chưa quyết | Mặc định do model chọn trong {Đời thường, Biên tập/chuyên nghiệp, Minh họa thủ công} hoặc phối theo ảnh; kèm 1 câu lý do (FR-116) |
| mục 2 Chữ trong ảnh | khi intake chưa quyết | Mặc định: hero/OG/thumbnail = chèn chữ sau; ảnh khác = không chữ (FR-123) |
| mục 3 Sản phẩm/mockup | chỉ khi intake nhắc sản phẩm hoặc có chỗ chờ sản phẩm | Nêu số chỗ + vị trí; mặc định "không" (FR-126) |
| mục 4 Số ảnh-tỉ lệ-kênh | khi intake chưa quyết | Theo `image-types.md` |

Ràng buộc: ≤ 4 mục; mỗi mục 1 mặc định + ≤ 3 lựa chọn mô tả bằng kết quả nhìn thấy; không preset ID, tên
công cụ, tham số (FR-111). Không mục nào chưa quyết → không có khối (FR-112).

Chuyển trạng thái: `đang chờ` → người dùng "ok" / trả lời một phần → pack xuất (FR-113). Sau khi có pack,
đổi một mục → chỉ viết lại prompt bị ảnh hưởng (FR-115).

## Kịch bản Media (đổi)

Bảng Vị trí ảnh có các cột: `# | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy |
Ánh sáng | Thời tiết/giờ | Người | Chữ`.

| Cột mới | Giá trị |
|---|---|
| Hướng | Đời thường / Biên tập / Minh họa |
| Khung | toàn cảnh / trung cảnh / cận chi tiết / qua vai / đang làm dở |
| Độ cao máy | thấp / ngang tầm mắt / đứng nhìn xuống / trên cao |
| Ánh sáng | nhiệt độ + nguồn, ví dụ "lạnh u ám, cửa sổ", "ấm tungsten, đèn bàn" |
| Thời tiết/giờ | ví dụ "sáng mưa", "tối" |
| Người | không / tay / một người / nhóm |
| Chữ | 0 không chữ / 1 chữ trong cảnh / 2 chèn chữ sau / 3 AI vẽ chữ / 4 hai lượt |

Bỏ cột "Ưu tiên" của 001 nếu cần chỗ (ghi trong mô tả mục đích). Quy tắc đa dạng FR-108 kiểm trên bảng
này. Prompt vượt 80 từ: ghi lý do dưới bảng.

## Prompt (đổi)

| Trường | Quy tắc |
|---|---|
| prompt | 30–80 từ (FR-101); ≤ 5 vật gọi tên, không số chẵn/đối xứng (FR-102); ảnh Đời thường có 1 vật lạc đề + 1 dấu vết người (FR-103); không từ cấm đứng một mình (FR-104); ảnh không chữ có câu chặn chữ tự thêm (FR-105) |
| prompt lượt 2 | chỉ ở chế độ hai lượt (FR-121) |
| Reference | thêm trường hợp: lượt 2 cần ảnh lượt 1; mockup đã xác nhận (nhãn "chờ sản phẩm xác minh") |
| ghi chú chữ | chế độ 2: vùng trống ở đâu, thêm chữ bằng công cụ thiết kế; tiếng Việt ở chế độ 3/4: cảnh báo thử mẫu (FR-122) |
| alt | ảnh có chữ phục vụ web vẫn có gợi ý alt (FR-125) |

## Chế độ chữ (mới)

Enum 0–4. Quan hệ: 1 ảnh ↔ đúng 1 chế độ; chế độ 4 ↔ 2 prompt.

## Tell (đổi)

15 dòng = 11 cũ + 4 mới có nhãn "suy luận từ một lượt test, chưa đo".

## QC chữ (mới)

7 mục đạt/không đạt (FR-124), nằm trong `text-in-image.md`.

## Preset (đổi)

Thêm nhóm **E** E01–E04 (biên tập/chuyên nghiệp), trạng thái `v0.1 chưa test`. Tổng 28 preset.
