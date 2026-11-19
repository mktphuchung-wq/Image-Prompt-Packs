# Chạy thử khô US3 — dùng lại vùng chữ ở chế độ 3 và 4 (v0.3.0)

**Cách chạy:** như `us1.md`. Kịch bản N: sau I, người dùng viết "hero cho AI vẽ luôn tiêu đề". Tiêu đề mặc định là "Indoor Christmas Decorations" (điểm a của Banner, đã có trong H).

---

## Kịch bản N — bản nháp 1 (trượt)

Bản nháp giữ mọi câu của prompt chế độ 2 và thay câu vùng chữ bằng câu chế độ 3:

```text
Photo of a living room in December, horizontal 16:9 frame. A Christmas tree with bare gaps stands on the right third, its ornaments in a box beside it. A phone charger lies coiled on the floor beside a half-drunk mug. The left third is a plain mid-grey wall carrying the headline "Indoor Christmas Decorations" in title case, bold white condensed sans-serif, left-aligned, about 45% of the frame width. Low winter light from the window, shot on a recent smartphone, eye level. Unposed, not retouched, not cinematic. The headline appears once; no other text anywhere.
```

**Kết quả:** 94 từ. Trượt V3-US3-4 (prompt chế độ 3 phải trong 30–80 từ). Nguyên nhân: không có quy tắc nào nói cách rút khi thêm tiêu đề vào prompt chế độ 2.

**Sửa (references, không sửa tiêu chí):**
- `references/text-in-image.md`, mục "Quy tắc chế độ 3": thêm quy tắc prompt chế độ 3 dưới 80 từ; khi chuyển từ chế độ 2 thì giữ câu chủ thể, câu vùng chữ, câu ảnh thật ("unposed, not retouched, not cinematic") và câu chặn chữ; rút câu ánh sáng, câu máy ảnh và chi tiết vật thừa.
- `references/text-in-image.md`, ví dụ chế độ 3: bỏ câu ánh sáng, thêm câu ảnh thật, còn 78 từ (trước đó 79 từ và thiếu câu ảnh thật, tức không đúng quy tắc ảnh thật của `anti-slop.md` mục 2).

---

## Kịch bản N — bản nháp 2 (đạt)

```text
Photo of a living room in December, horizontal 16:9 frame. A Christmas tree with bare gaps stands on the right third. A phone charger lies coiled on the floor beside a half-drunk mug. The left third is a plain mid-grey wall carrying the headline "Indoor Christmas Decorations" in title case, bold white condensed sans-serif, left-aligned, about 45% of the frame width. Unposed, not retouched, not cinematic. The headline appears once; no other text anywhere.
```

**Số từ: 74.** Vật gọi tên: cây, sạc, cốc (3). Không số chẵn, không từ cấm.

**Cột Chữ của hero:** "3 AI vẽ chữ — 1/3 trái". Các dòng khác của bảng giữ nguyên.

**Không có khối Vùng chữ** ở ảnh chế độ 3, theo quy tắc trong `text-in-image.md`: vùng chữ đã nằm trong prompt và được ghi ở cột Chữ.

---

## Rà chế độ 4 (văn bản `references/text-in-image.md`)

Mục "Chế độ 4: hai lượt": lượt 1 là prompt chế độ 2 nguyên văn kèm khối Vùng chữ; lượt 2 dùng đúng câu chuẩn "Image 1 = approved scene. Add the headline only; keep everything else unchanged." và đặt tiêu đề trong vùng đã xác định; mục Reference của lượt 2 là ảnh lượt 1.

---

## Bảng chấm US3 (tiêu chí `tests/acceptance.md`, mục v0.3 — US3)

| # | Kịch bản | Kết quả | Bằng chứng |
|---|---|---|---|
| V3-US3-1 | N | Đạt | Cây ở phần ba bên phải, tường ở phần ba bên trái, cùng bố cục với prompt chế độ 2 |
| V3-US3-2 | N | Đạt | Chuỗi trong ngoặc kép, "title case", "bold white condensed sans-serif", màu trắng, "left-aligned", "about 45% of the frame width", "The headline appears once; no other text anywhere." |
| V3-US3-3 | N | Đạt | Cột Chữ của hero đổi thành "3 AI vẽ chữ — 1/3 trái"; các dòng khác không đổi |
| V3-US3-4 | N | Đạt sau vòng sửa 1 | Bản nháp 1: 94 từ (trượt). Sau sửa: 74 từ |
| V3-US3-5 | Rà | Đạt | Mục chế độ 4 và quy tắc chế độ 3 đúng như mô tả ở trên |

**Tổng US3:** 5/5 đạt; V3-US3-4 đạt sau vòng sửa 1.
