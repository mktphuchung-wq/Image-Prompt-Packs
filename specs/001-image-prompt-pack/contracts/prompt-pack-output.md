# Contract: Đầu ra cho người dùng

Đây là hợp đồng mà `SKILL.md` phải bảo đảm. Hình dạng chi tiết của từng trường: [data-model.md](../data-model.md).
Ngôn ngữ: phần giải thích theo ngôn ngữ người dùng; khối prompt bằng tiếng Anh.

## 1. Chế độ tạo pack (US1, US2)

Thứ tự trình bày:

```markdown
## Kịch bản Media
**Nội dung:** <1–3 câu>
**Mục tiêu:** … · **Đối tượng:** … · **Kênh:** …
**Hướng hình ảnh:** <phong cách chung, brand nếu có>
**Giả định:** <chỉ khi có>

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Ưu tiên |
|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | … | hero | 16:9 | cao |
| … |

## Prompt Pack
<ghi chú phong cách chung, 1–2 câu>

### Ảnh 1 — Hero
```text
<một prompt liền mạch, tiếng Anh, copy dùng ngay>
```
**Reference:** <chỉ khi cần tệp đính kèm — tệp gì, vai trò>
<ghi chú mockup / ghi chú phụ nếu có>

### Ảnh 2 — …
```

Bất biến:

- Mỗi hàng bảng ↔ đúng một mục `### Ảnh N`.
- Khối prompt nằm trong code block để copy một lần; không chứa nhãn khe, chú thích, placeholder `[...]`
  chưa điền, cú pháp riêng công cụ, buzzword chất lượng.
- Không có mục Reference ở ảnh không cần tệp.
- Không tạo ảnh, không gọi công cụ tạo ảnh.
- Không tự thêm ảnh mockup sản phẩm.

## 2. Chế độ sửa prompt (US3)

```markdown
**Chẩn đoán:** <lỗi trong ảnh → nguyên nhân trong prompt>

```text
<prompt đã sửa, copy dùng ngay>
```
**Đã đổi:** <1–3 dòng>
```

Bất biến: chỉ trả prompt của ảnh bị phàn nàn; giữ phong cách pack; nếu harness xem được ảnh thì chẩn
đoán từ ảnh, nếu không thì từ mô tả.

## 3. Khi thiếu nội dung

Không tìm thấy nội dung để làm media → một câu nói rõ không tìm thấy + xin nội dung/đường dẫn. Thiếu
thông tin làm đổi hẳn kết quả → tối đa 3 câu hỏi ngắn, mỗi câu có đề xuất mặc định. Không bịa nội dung.

## 4. Lưu file (FR-014)

Chỉ khi người dùng yêu cầu và harness cho ghi: một file Markdown chứa nguyên mục 1, tên gợi ý
`prompt-pack-<chủ-đề>.md` ở thư mục làm việc hiện tại.
