# Contract: Prompt chế độ 2 và khối Vùng chữ

## Prompt chế độ 2 — bất biến

- Nêu vị trí chủ thể và vị trí vùng chữ (FR-201).
- Đúng một cách tạo vùng chữ, mô tả cụ thể (FR-202, FR-203):
  - a: gọi tên bề mặt + tông + "nothing in that area";
  - b: "subject and foreground sharp; background behind the [side] softly blurred, low detail, shapes still recognisable";
  - c: mảng giấy/màu phẳng (chỉ hướng Minh họa).
- Nêu tông vùng chữ; câu chặn chữ tự thêm (FR-204).
- 30–80 từ, ≤ 5 vật, không số chẵn, không từ cấm (FR-206).
- Không: thông số máy ảnh, "bokeh", cú pháp riêng công cụ, nhãn khe.

## Mẫu đầu ra

```markdown
### Ảnh 1 — Hero
```text
<prompt chế độ 2>
```
**Vùng chữ:** 1/3 trái, khoảng 40% khung · cách tạo: tường xám đậm có thật (a) · nền tối trung bình → chữ trắng hoặc kem · lề an toàn ~5% · tiêu đề 1–2 dòng · cắt sang 1.91:1 vẫn còn nguyên; khung 2:3 dùng prompt dọc riêng.
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.
```

Bảng Kịch bản Media, cột Chữ: `2 chèn chữ sau — 1/3 trái`.

## Chế độ 3/4

- Giữ nguyên câu bố cục và vùng chữ của prompt chế độ 2; thêm mô tả tiêu đề theo quy tắc chế độ 3 đặt
  **trong** vùng đó (FR-211).
- Chế độ 4: lượt 1 = prompt chế độ 2 nguyên văn.
