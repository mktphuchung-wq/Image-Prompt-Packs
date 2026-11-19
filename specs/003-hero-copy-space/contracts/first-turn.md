# Contract: Lượt đầu (khởi tạo)

Thay bảng "Khi nào dừng chờ, khi nào xuất luôn" của `specs/002-prompt-pack-optimize/contracts/brief-card.md`.

## Khi nào dừng

| Tình huống | Kết quả |
|---|---|
| Có ≥ 1 trường hợp kích hoạt: (1) chữ, (2) phong cách, (3) nội dung đặc biệt, (4) format mới lạ (định nghĩa ở spec FR-215) | Chốt nhanh + Kịch bản Media, **không prompt**, dừng chờ |
| Không có trường hợp nào | Xuất pack ngay; khối "Đã dùng mặc định" ở đầu |
| Người dùng nói "đưa luôn"/"không cần hỏi", hoặc không có người trả lời | Xuất pack ngay; khối "Đã dùng mặc định" ở đầu |

Số ảnh hay độ dài bài một mình không là lý do dừng.

## Mẫu khối khi dừng

```markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Banner (lý do: bài có ảnh hero, chưa chốt chữ)
   a. Tiêu đề: "<tiêu đề bài, ≤ 6 từ>", 1 dòng (mặc định) · hoặc gửi tiêu đề khác
   b. Cách đặt chữ: chừa vùng, thêm tiêu đề sau bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề · hai lượt
   c. Vùng chữ: 1/3 trái trên mảng tường xám đậm (mặc định — cảnh có tường trơn) · làm mềm hậu cảnh bên trái
   d. Khung: hero 16:9 + ảnh chia sẻ 1.91:1 (mặc định) · thêm Pinterest 2:3
2. <Phong cách / Sản phẩm / Format mới lạ — chỉ khi kích hoạt, kèm lý do>

## Kịch bản Media
… bảng đủ cột 002, cột Chữ có vị trí vùng …
Sửa format theo số dòng, ví dụ "ảnh 3 đổi 4:5, bỏ ảnh 5", hoặc trả "ok".
```

## Bất biến

- ≤ 4 mục; Banner = 1 mục; mỗi mục có lý do kích hoạt + mặc định + ≤ 3 lựa chọn.
- Không sơ đồ ký tự; không preset ID, tên công cụ, tham số kỹ thuật.
- Trả lời sửa theo số dòng → chỉ áp dòng đó.
