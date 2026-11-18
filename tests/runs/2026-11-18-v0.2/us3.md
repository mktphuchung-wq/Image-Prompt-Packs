# Chạy thử khô US3 (v0.2): chế độ chữ

**Phạm vi:** kịch bản B (cột Chữ của pack fixture 05), kịch bản C (hero do AI vẽ chữ "Indoor Christmas Decorations"), biến thể tiêu đề tiếng Việt có dấu ở chế độ 3, và chế độ 4 (hai lượt). Chuẩn: `tests/acceptance.md` mục "v0.2 — US3".

**Cách chạy:** worker đóng vai model, đọc `SKILL.md` (cập nhật US3, 138 dòng) và `references/text-in-image.md`, rồi làm theo. Số từ đếm bằng `wc -w`; từ cấm và số chẵn quét bằng `grep`.

**Giới hạn:** chạy khô, cùng một worker viết skill và chấm. Không tạo ảnh thật, nên SC-106 (7 mục QC chữ trên ảnh thật, 4/5 lần) được ghi là **cần người chạy**. Quy tắc tiếng Việt chỉ kiểm bằng văn bản; việc thử một ảnh mẫu trên công cụ thật là bước của người dùng.

---

## B: cột Chữ và hero chế độ 2 (pack fixture 05)

Bảng Kịch bản Media như `us1.md`, cột **Chữ** theo thứ tự ảnh 1–7: `2 chèn chữ sau`, `0 không chữ`, `0 không chữ`, `0 không chữ`, `0 không chữ`, `2 chèn chữ sau`, `2 chèn chữ sau`. Hero và ảnh chia sẻ là chế độ 2, mặc định; các ảnh minh họa là chế độ 0. Đạt V2-US3-1 và V2-US3-2.

Hero viết ở chế độ 2 (có dòng **Chữ** theo mẫu đầu ra):

### Ảnh 1 — Hero
```text
Phone photo of an ordinary living room a week before Christmas, horizontal 16:9 frame. A crooked tree on the right, bare gaps; beside it a box with lights spilling out. A laptop and a kid's sock lie on the floor. Cool overcast window light. The left third is a plain mid-grey wall with clean empty space for a headline added later. No readable text anywhere.
```
**Chữ:** chế độ 2. Vùng trống là bức tường xám trung tính ở một phần ba bên trái, tương phản trung bình; người dùng thêm tiêu đề bằng công cụ thiết kế.

Chế độ 2 yêu cầu chủ thể ở một phần khung, vùng trống có vị trí rõ và tương phản trung bình hoặc tối, không có chữ trong ảnh. Prompt đáp ứng cả ba. Đạt V2-US3-3.

---

## C: hero do AI vẽ chữ "Indoor Christmas Decorations"

Chỉ prompt hero đổi. Cột Chữ của hero đổi từ `2 chèn chữ sau` sang `3 AI vẽ chữ`. Ảnh 2–7 giữ nguyên.

### Ảnh 1 — Hero
```text
16:9 phone photo of an ordinary living room a week before Christmas. A crooked tree on the right, bare gaps; beside it a box with lights spilling out. A laptop and a kid's sock lie on the floor. Cool overcast window light. The left third is a plain mid-grey wall carrying the headline "Indoor Christmas Decorations" in title case, bold white condensed sans-serif, one line, 45% of frame width, five percent margin. The headline appears once; no other text anywhere.
```
**Chữ:** chế độ 3. Chuỗi "Indoor Christmas Decorations" trong ngoặc kép, kiểu chữ hoa/thường: title case; một dòng; bề mặt nền là tường xám trung tính ở phần ba bên trái; lề khoảng 5%. Nếu tiêu đề quá dài cho một dòng, rút xuống ít chữ hơn thay vì thêm dòng.

Đối chiếu từng yêu cầu của chế độ 3 trong `text-in-image.md`:
- Chuỗi chính xác trong ngoặc kép: có.
- Kiểu hoa/thường nêu rõ: "title case".
- Kiểu chữ theo đặc điểm, không tên font: "bold white condensed sans-serif".
- Màu: "white"; không là màu thương hiệu nên không cần mã hex.
- Vị trí và canh lề: "left third"; cỡ tương đối: "45% of frame width".
- Bề mặt nền tương phản: "plain mid-grey wall".
- Lề khoảng 5%: "five percent margin".
- Câu chuẩn: "The headline appears once; no other text anywhere."
- Số dòng: một dòng, trong khoảng 1–2 dòng.
Đạt V2-US3-4.

Số từ prompt hero chế độ 3: **80** (trong giới hạn 80; đếm trong bước kiểm dưới).

---

## Biến thể: tiêu đề tiếng Việt có dấu ở chế độ 3

Tiêu đề thử: "Trang trí Giáng sinh trong nhà" (dấu đầy đủ). Prompt hero:

```text
16:9 phone photo of an ordinary living room before Christmas. A crooked tree on the right, bare gaps; beside it a box with lights spilling out. Cool overcast window light. The left third is a plain mid-grey wall carrying the headline "Trang trí Giáng sinh trong nhà" in title case, bold white condensed sans-serif, one line, 45% of frame width, five percent margin. The headline appears once; no other text anywhere.
```
**Chữ:** chế độ 3, tiêu đề tiếng Việt có dấu. **Cảnh báo:** thử một ảnh mẫu trên công cụ đang dùng trước khi tạo cả loạt; nếu sai một dấu thì chuyển hero sang chế độ 2 (chèn chữ sau bằng công cụ thiết kế).

Kiểm: có cảnh báo thử mẫu; có quy tắc chuyển chế độ khi sai dấu. Đạt V2-US3-5.

---

## Chế độ 4: hai lượt (hero)

Lượt 1 là cảnh có vùng trống (chế độ 2), không chữ. Lượt 2 chỉnh ảnh theo câu chuẩn.

### Ảnh 1 — Hero (hai lượt)
```text
Phone photo of an ordinary living room a week before Christmas, horizontal 16:9 frame. A crooked tree on the right, bare gaps; beside it a box with lights spilling out. A laptop and a kid's sock lie on the floor. Cool overcast window light. The left third is a plain mid-grey wall with clean empty space for a headline added later. No readable text anywhere.
```
```text
Image 1 = approved scene. Add the headline only; keep everything else unchanged. Headline "Indoor Christmas Decorations" in title case, bold white condensed sans-serif, one line, 45% of frame width on the plain mid-grey wall, five percent margin. The headline appears once; no other text anywhere.
```
**Reference:** lượt 2 cần ảnh tạo từ lượt 1 (ảnh đã duyệt).

Kiểm: lượt 2 dùng đúng câu chuẩn "Image 1 = approved scene. Add the headline only; keep everything else unchanged."; Reference là ảnh lượt 1; chỉ thêm tiêu đề và nói rõ giữ nguyên. Đạt V2-US3-6.

---

## Alt và H1 (FR-125)

- Hero (ảnh có chữ phục vụ web): gợi ý alt "Phòng khách bình thường, cây Giáng sinh còn dở, hộp đèn bên cạnh" (mô tả nội dung, không lặp tiêu đề).
- Ảnh chia sẻ có chữ: cần một gợi ý alt tương tự.
- Chữ không đứng thay H1: tiêu đề bài vẫn là H1 của trang; tiêu đề trên ảnh chỉ là chữ trong ảnh.
Đạt V2-US3-7.

---

## QC chữ (FR-124): kiểm mẫu, không phải ảnh thật

Chưa có ảnh được tạo, nên 7 mục QC chỉ kiểm được trên văn bản prompt (kiểm được: câu chuẩn, chuỗi trong ngoặc, vị trí, nền, lề, số lần xuất hiện). Các mục về ảnh thật (chính tả từng ký tự, dấu tiếng Việt trên ảnh, đọc được ở 360 px, tương phản thực tế) chỉ kiểm khi có ảnh. Ghi nhận V2-US3-8 ở mức văn bản.

---

## Chấm máy

| Khối | Số từ | Từ cấm | Số chẵn | Ghi chú |
|---|---|---|---|---|
| Hero chế độ 2 (B) | 65 | 0 | 0 | có câu chặn chữ |
| Hero chế độ 3 (C) | 80 | 0 | 0 | đạt giới hạn 80 |
| Hero tiếng Việt chế độ 3 | 71 | 0 | 0 | có dấu đầy đủ |
| Hero chế độ 4, lượt 1 | 65 | 0 | 0 | giống chế độ 2 |
| Hero chế độ 4, lượt 2 | 46 | 0 | 0 | câu chuẩn đúng từng chữ |

Số liệu đếm bằng `wc -w` trên các khối code của file này. Mọi khối nằm trong 30–80 từ.

**Vòng sửa US3:** vòng 1 không phát hiện tiêu chí trượt. Hai điều chỉnh khi viết, trước khi chấm: (1) bỏ "about" trước "45%" để prompt chế độ 3 còn 80 từ, khớp `references/text-in-image.md`; (2) bản tiếng Việt: tiêu đề sáu từ làm prompt lên 83 từ, nên bỏ câu về laptop và tất cùng "a week" để còn 71 từ. Số vòng sửa skill/references: 0.

**SC-106:** cần người chạy trên công cụ tạo ảnh thật, 5 lần tạo hero với tiêu đề tiếng Anh, đếm số lần qua đủ 7 mục QC (ít nhất 4/5).

---

## Danh sách preset đã sửa (T006)

Đây là các chỉnh sửa tối thiểu trong `references/presets.md` để loại từ cấm đứng một mình và số chẵn trong khung. Không đổi ID preset.

| Preset | Thay đổi | Lý do |
|---|---|---|
| R01 | "[2 mundane objects]" → "[1 or 3 mundane objects]" | số chẵn |
| R02 | "natural color balance" → "neutral color balance" | từ cấm đứng một mình |
| R03 | "soft natural window light" → "soft window light"; "natural color balance" → "neutral color balance"; "small exposure imperfections" → "a blown highlight on the window frame" | từ cấm; "imperfections" thay bằng chi tiết cụ thể |
| R05 | "[2 mundane items]" → "[1 or 3 mundane items]" | số chẵn |
| R06 | "gentle natural shadow" → "a soft-edged shadow" | từ cấm |
| R08 | "natural light from [window]" → "light from [window]" | từ cấm |
| R12 | "[3 to 5 people with ages]" → "[3 or 5 people with ages]" | khoảng có số chẵn 4 |
| S01 | Tên "Risograph 2 màu" → "Risograph 3 màu"; "two spot colors" → "three spot colors" | số chẵn |
| S04 | "two colors on cream paper" → "three colors on cream paper" | số chẵn |
| S08 | "overprint creating a 4th color" → "overprint creating one extra mixed tone" | số chẵn (màu thứ tư) |
| Bảng slot | Hàng "Khung" đổi tên thành "Góc máy"; thêm hàng "Nhiệt độ ánh sáng" và "Loại khung"; tiêu đề đổi "(FR-011)" → "(anti-slop §4)" | tránh trùng cột Khung của Kịch bản Media |

Kiểm sau khi sửa: 28 ID duy nhất; bốn khung E 62–66 từ; không còn từ cấm và số chẵn trong khung (quét `grep`).
