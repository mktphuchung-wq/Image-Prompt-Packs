# Chạy khô US1: fixture 01 và lượt đổi ảnh 2 thành mockup

- Ngày chạy: 2026-11-18
- Loại chạy: **chạy khô**. Worker tự đóng vai model, làm theo `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` và bốn file trong `references/` (anti-slop, presets, image-types, example-pack). Không gọi model ngoài, không tạo ảnh.
- Giới hạn: người viết skill và người chấm là cùng một worker, nên đây là kiểm tra nội bộ, chỉ bắt được lỗi rõ ràng. Chạy trên harness thật và blind test vẫn cần làm (xem `docs/verification.md`).
- Số vòng sửa SKILL/references: **1**. Sau vòng 1 thêm một dòng tự kiểm vào SKILL.md (mục Tiêu chí thành công, khi lập pack). Cả ba run được chạy lại sau sửa này.

## Vòng 1: bản nháp trước khi sửa

Bản nháp đầu không đạt US1-3. Khi đối chiếu từng prompt với `anti-slop.md` mục 2, phát hiện:

| Ảnh | Lỗi trong bản nháp |
|---|---|
| 2 | Thiếu tỉ lệ khung trong prompt (bảng ghi 4:3 nhưng prompt không ghi) và không nêu nguồn sáng |
| 3 | Chỉ có một vật đời thường (túi vải); bản nháp còn lặp "overcast" hai lần |
| 4 | Không nêu nguồn sáng |
| 5 | Có hai khuyết điểm: sợi chỉ lỏng ở tay áo và đồ vật lệch |
| Mockup (lượt 2) | 83 từ, vượt ngưỡng 80; chỉ có một vật đời thường |

Kết luận: US1-3 trượt ở vòng 1, vì vi phạm FR-010 (nguồn sáng, khuyết điểm, vật đời thường, tỉ lệ). Sửa: thêm dòng tự kiểm vào SKILL.md; sửa bốn prompt và prompt mockup; chạy lại từ đầu (vòng 2).

## Vòng 2: lượt 1, dán fixture 01

Input: nội dung `tests/fixtures/01-blog-article.md` (1.384 từ), không kèm yêu cầu nào thêm.

### Đầu ra

## Kịch bản Media
**Nội dung:** Bài hướng dẫn chọn áo hoodie cotton cho mùa đông: nhận biết ba loại cotton (nỉ, bông, da cá), đọc chỉ số gsm, chọn form và size, nhìn kỹ mũ, khóa kéo, túi, bo và lớp lót, cùng cách giặt để áo bền. Bài có nhắc một mẫu của shop nhưng không yêu cầu ảnh sản phẩm.
**Mục tiêu:** Giúp người đọc chọn được chiếc hoodie cotton bền, đủ ấm và đúng form, thay vì mua theo cảm tính. · **Đối tượng:** Người mua đồ mùa đông, đặc biệt người mua online. · **Kênh:** Blog và chia sẻ trên mạng xã hội.
**Hướng hình ảnh:** Ảnh đời thường, ánh sáng tự nhiên, không dựng studio; bảng màu be ấm, xám đá và xanh rêu cho cả pack.
**Giả định:** Bài khoảng 1.500 từ. Áo trong ảnh là áo trơn chung, không phải mẫu của shop, nên không có vị trí mockup. Chưa có tên thương hiệu để đặt trong ảnh.

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Ưu tiên |
|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | Thể hiện cảm giác mùa đông và chiếc hoodie trong đời sống | hero | 16:9 | cao |
| 2 | Minh họa chất liệu | Mục Hiểu đúng về chất liệu cotton | Gợi ba loại cotton bằng hình, không cần chữ | minh họa | 4:3 | trung bình |
| 3 | Minh họa cách mặc | Mục Màu sắc và cách phối đồ | Gợi cách mặc hoodie dưới áo khoác | minh họa | 3:2 | trung bình |
| 4 | Infographic | Mục Tóm tắt nhanh khi chọn mua | Tóm tắt năm điều cần kiểm tra | infographic | 4:3 | thấp |
| 5 | Ảnh chia sẻ | Ảnh đại diện khi chia sẻ | Ảnh nhìn từ trên cho link preview | mạng xã hội (OG) | 1.91:1 | cao |

## Prompt Pack
Phong cách chung: ánh sáng tự nhiên, bảng màu be ấm, xám đá và xanh rêu; không dựng studio. Mỗi ảnh một người, nơi chốn và giờ khác nhau.

### Ảnh 1 — Hero
```text
Photo of a man in his late 20s in a stone-grey cotton hoodie, pulling the hood up while walking along a damp street at dusk, a paper coffee cup in one hand. A half-lit shop sign at the edge of the frame. Warm light from a shop window on the right, plain grey street light from above. Shot on a recent smartphone, eye level, slightly off-center, horizontal 16:9 frame. Unposed, not retouched, not cinematic. Sharp focus throughout.
```

### Ảnh 2 — Minh họa chất liệu
```text
Hand-cut paper collage of three cotton swatches laid on cream paper: a loose fleece-back swatch, a smooth jersey swatch and a ribbed terry swatch, each with a visible fiber edge. Layered torn paper edges, visible glue wrinkles, limited palette of stone grey, moss green and warm beige. Soft light from the top left, flat top-down view, soft shadow under each swatch, horizontal 4:3 frame, no text.
```

### Ảnh 3 — Minh họa cách mặc
```text
Street photo of a woman in her 30s in a beige hoodie tucked under a light denim jacket, waiting at a bus stop on a quiet morning with a paper cup in one hand and a canvas bag strap over one shoulder. Shot from across the road with an 85mm lens look, subject unaware of the camera, other pedestrians partly cut by the frame edge, deep focus. Neutral overcast daylight, true colors. Unposed, not cinematic, horizontal 3:2 frame.
```

### Ảnh 4 — Infographic
```text
Risograph-style top-down layout of five numbered checkpoints around a folded stone-grey hoodie: sleeve cuff, hood seam, zipper, kangaroo pocket and hem. The numerals "1" to "5" appear once each, nothing else written. Two spot colors, moss green and cream, visible misregistration, grainy halftone, paper texture, flat shapes. Flat light from above. Clean empty area across the top third for a headline added later, horizontal 4:3 frame.
```

### Ảnh 5 — Ảnh chia sẻ
```text
Overhead photo of a folded stone-grey hoodie on a wooden table next to a mug of tea and a pair of gloves, daylight from the side, items slightly misaligned. Shot from directly above, horizontal 1.91:1 frame with the subject kept away from the edges. Unposed, not retouched, sharp focus throughout.
```

Kiểm lại theo `anti-slop.md` mục 2, sau vòng 2:

| Ảnh | Số từ | Cụm camera | Khuyết điểm | Nguồn sáng | Vật đời thường | Tỉ lệ viết bằng lời |
|---|---|---|---|---|---|---|
| 1 | 77 | 1 (smartphone) | 0 | cửa sổ bên phải và đèn đường | 2 (cốc giấy, biển hiệu) | 16:9 |
| 2 | 66 | 0 | 1 (glue wrinkles) | góc trên bên trái | minh họa vải, không áp dụng | 4:3 |
| 3 | 78 | 1 (85mm look) | 0 | trời u | 2 (cốc giấy, túi vải) | 3:2 |
| 4 | 66 | 0 | 1 (misregistration) | ánh sáng từ trên | số 1 đến 5 | 4:3 |
| 5 | 50 | 0 | 1 (misaligned) | ánh sáng từ một bên | 2 (cốc trà, đôi găng tay) | 1.91:1 |

### Chấm lượt 1, vòng 2

| # | Tiêu chí | Kết quả | Bằng chứng |
|---|---|---|---|
| US1-1 | Kịch bản đủ trường: nội dung, mục tiêu, đối tượng, kênh, hướng hình ảnh, danh sách vị trí | Đạt | Các dòng Nội dung, Mục tiêu, Hướng hình ảnh và bảng vị trí |
| US1-2 | 3–8 ảnh | Đạt | 5 ảnh |
| US1-3 | Mỗi ảnh một khối prompt copy được; không placeholder; không cú pháp riêng; không buzzword; đạt FR-010 | Đạt (vòng 2) | Năm khối code, không có `[...]`; kiểm bằng grep không có 8K, masterpiece, ultra-detailed, stunning, flawless; bảng kiểm nhanh ở trên |
| US1-4 | Không có Reference ở ảnh không cần tệp | Đạt | Không có mục Reference trong lượt 1 |
| US1-5 | Không tự thêm mockup | Đạt | Không có ảnh mockup; Giả định nêu rõ áo là áo trơn chung |
| US1-6 | Không tạo ảnh | Đạt | Đầu ra chỉ là văn bản |
| US1-7 | Các ảnh khác nhau về người, nơi chốn, giờ | Đạt | Người nam cuối 20 tuổi lúc chạng vạng; người nữ 30 tuổi buổi sáng; ba ảnh không người |

## Lượt 2: "ảnh 2 cần mockup áo hoodie của shop"

Input: lượt nói tiếp theo, không dán lại bài. Theo FR-020, mockup chỉ được lập khi người dùng báo đúng vị trí cần mockup. Lượt này đã báo đúng vị trí ảnh 2.

### Đầu ra

Chỉ cập nhật ảnh 2. Các ảnh 1, 3, 4, 5 giữ nguyên.

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Ưu tiên |
|---|---|---|---|---|---|---|
| 2 | Mockup áo hoodie | Mục Hiểu đúng về chất liệu cotton (giữ nguyên) | Cho thấy chiếc hoodie của shop trong đời sống | mockup sản phẩm (theo yêu cầu) | 4:5 | cao |

Lưu ý: vị trí ảnh 2 giữ theo bài hiện có. Nếu muốn đặt mockup gần mục "Gợi ý một mẫu để tham khảo", bạn đổi vị trí và tôi sẽ cập nhật.

### Ảnh 2 — Mockup áo hoodie

**Reference:** Cần một tệp: ảnh chụp thật chiếc hoodie của shop, nhìn thẳng mặt trước, nền trơn, đủ sáng và không bóng loáng. Vai trò: Image 1 = product reference. Giữ đúng form, màu và vị trí túi, mũ, khóa kéo; không vẽ lại thiết kế hay logo. Đính kèm tệp này làm Image 1 khi dùng công cụ tạo ảnh.

```text
Photo of a young woman wearing the hoodie shown in Image 1, sitting on a wooden café chair by a window, a paper cup in both hands and a folded tote bag on the table, morning light from the left. Keep the garment's cut, color and pocket position as in Image 1. The chest area stays plain and unprinted for a later composite. Shot on a recent smartphone, eye level, vertical 4:5 frame. Unposed, not retouched, not cinematic.
```

**Ghi chú mockup:** Ghép thiết kế thật sau khi tạo ảnh, vào đúng vùng ngực đã để trống. Khi xuất file, giữ nguyên metadata AI (C2PA, IPTC); không xóa khi nén hoặc đăng. Trước khi đăng lên trang bán hàng, kiểm tra chính sách hiện hành của nền tảng về ảnh AI.

### Chấm lượt 2

| # | Tiêu chí | Kết quả | Bằng chứng |
|---|---|---|---|
| US1-9 | Ảnh 2 thành mockup: có Reference là ảnh sản phẩm thật; prompt không vẽ lại thiết kế hay logo; có ghi chú ghép thiết kế thật và giữ metadata AI | Đạt | Mục Reference nêu tệp và vai trò Image 1; prompt giữ cut, màu và vị trí túi, để vùng ngực trống; ghi chú có composite và C2PA/IPTC. Prompt 78 từ, có hai vật đời thường, một cụm camera |
| US1-8 | Lượt sau "làm prompt ảnh cho bài vừa rồi" tự lấy bài từ lịch sử | Chưa kiểm | Cần hội thoại thật trên harness; dry run không tái hiện được lịch sử |

## Kết quả US1

- Đạt: 8 trên 9 tiêu chí (US1-1 đến US1-7, US1-9), sau vòng 2.
- Chưa kiểm: 1 (US1-8, cần hội thoại thật).
- Trượt ở vòng 1: US1-3. Đã sửa, đạt ở vòng 2.
- Số vòng sửa SKILL/references: 1.
