# Data Model: v0.3.0 (chỉ phần thêm/đổi so với 002)

## Vùng chữ (mới)

| Trường | Giá trị / quy tắc |
|---|---|
| vị trí | khung ngang: "1/3 trái", "1/3 phải", "nửa trái", "nửa phải"; khung dọc: "dải trên", "dải dưới" |
| cỡ | 35–50% khung; tiêu đề dài hoặc tiếng Việt nhiều dòng 45–50% |
| cách tạo | `a` khoảng trống thật (gọi tên bề mặt) · `b` làm mềm hậu cảnh nhẹ · `c` mảng phẳng (Minh họa) |
| tông nền | tối trung bình / sáng dịu; ít chi tiết; không vật lấn vào |
| màu chữ gợi ý | trắng/kem trên nền tối, gần đen trên nền sáng; màu thương hiệu (mã hex) nếu đủ tương phản, không thì gợi ý dải màu đặc |
| lề an toàn | ~5% mỗi cạnh |
| số dòng dự kiến | 1–2 (theo tiêu đề) |
| khi cắt khung | "còn nguyên ở 1.91:1" / "mất ở 2:3 → dùng prompt khung dọc" |

Quan hệ: 1 ảnh chế độ 2/3/4 ↔ 1 Vùng chữ. Đổi 2 → 3/4: giữ Vùng chữ (FR-211).

## Khối Vùng chữ (mới, hiển thị)

Đặt ngay dưới khối prompt của ảnh chế độ 2. Gồm mọi trường trên + câu cố định: "Ảnh cố ý không có chữ; thêm
tiêu đề bằng công cụ thiết kế." (FR-207)

## Cột Chữ (đổi)

Chế độ 2/3/4: "<số chế độ> <tên> — <vị trí vùng>", ví dụ "2 chèn chữ sau — 1/3 trái" (FR-208).

## Khối Chốt nhanh (đổi)

| Trường | Quy tắc |
|---|---|
| điều kiện có khối | ≥ 1 trường hợp kích hoạt FR-215 (chữ / phong cách / nội dung đặc biệt / format mới lạ); không còn điều kiện theo số ảnh hay độ dài (FR-217) |
| mục | ≤ 4; mục Banner tính một mục; mỗi loại trường hợp (2)–(4) tối đa một mục (FR-220) |
| mỗi mục | lý do kích hoạt (trường hợp nào, thấy ở đâu) + mặc định + ≤ 3 lựa chọn (FR-217) |
| mục Banner | 4 điểm: a tiêu đề + số dòng · b cách đặt chữ (mặc định chèn chữ sau) · c vùng chữ phía nào + cách tạo (mặc định model đề xuất kèm lý do) · d các khung cần; điểm đã chốt thì bỏ; mô tả bằng lời, không sơ đồ ký tự (FR-218) |
| format ảnh khác | qua bảng Kịch bản Media + dòng "sửa theo số dòng… hoặc trả 'ok'"; chỉ ảnh format mới lạ có câu hỏi riêng (FR-219) |

## Khối "Đã dùng mặc định" (đổi)

Dòng Chữ phải có: "hero chừa vùng chèn tiêu đề ở <vị trí>; ảnh cố ý không có chữ" (FR-216, FR-210).
