# Contract: Đầu ra cho người dùng (v0.2)

Thay `specs/001-image-prompt-pack/contracts/prompt-pack-output.md` §1 và §3. §2 (sửa prompt) và §4 (lưu
file) của 001 giữ nguyên, trừ phần chẩn đoán dùng thêm 4 tell mới và QC chữ.

## 1a. Lượt đầu khi phải dừng chờ (bài dài hoặc ≥ 4 ảnh)

```markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
<khối theo contracts/brief-card.md>

## Kịch bản Media
**Nội dung:** <1–3 câu> · **Mục tiêu:** … · **Đối tượng:** … · **Kênh:** …

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | … | hero | 16:9 | Đời thường | toàn cảnh | đứng | lạnh u ám, cửa sổ | sáng mưa | không | 2 chèn chữ sau |
```

Bất biến: **không có khối prompt nào** trong lượt này.

## 1b. Pack (sau "ok", hoặc xuất luôn)

```markdown
## Đã dùng mặc định        ← chỉ khi xuất luôn không qua lượt chờ; 1 dòng mỗi mục
## Kịch bản Media           ← như 1a (bảng đã cập nhật theo câu trả lời)
<lý do nếu prompt nào vượt 80 từ>

## Prompt Pack
<ghi chú phong cách chung, 1–2 câu>

### Ảnh 1 — Hero
```text
<prompt 30–80 từ, tiếng Anh>
```
**Chữ:** <chỉ với chế độ 2/3/4 — vùng trống ở đâu / chuỗi chữ / cảnh báo tiếng Việt>
**Reference:** <chỉ khi cần tệp>

### Ảnh 4 — Banner (hai lượt)
```text
<lượt 1>
```
```text
<lượt 2: Image 1 = approved scene. Add the headline only; keep everything else unchanged. …>
```
**Reference:** lượt 2 cần ảnh tạo từ lượt 1.
```

Bất biến (thêm vào bất biến của 001):

- Mỗi khối prompt đạt tiêu chí tự kiểm FR-101…FR-105.
- Bảng đạt FR-108 (pack ≥ 4 ảnh).
- Không có prompt mockup, mục "Bonus" hay prompt sản phẩm khi mockup không được chọn (FR-127).
- Không có mục Giả định ở cuối; mặc định đã dùng nằm ở đầu (FR-114).

## 3. Khi thiếu nội dung

Giữ như 001. Câu hỏi làm rõ (nếu có) nằm trong khối Chốt nhanh, không thành chuỗi câu hỏi riêng.
