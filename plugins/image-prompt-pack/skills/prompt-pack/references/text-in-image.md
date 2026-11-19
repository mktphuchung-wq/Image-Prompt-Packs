# Chữ trong ảnh: năm chế độ, quy tắc và QC

Mỗi ảnh có đúng một chế độ chữ, ghi ở cột Chữ của Kịch bản Media. Mặc định: hero, ảnh chia sẻ (OG) và thumbnail dùng chế độ 2 (chèn chữ sau); ảnh khác dùng chế độ 0 (không chữ); chế độ 3 và 4 chỉ khi người dùng chọn.

## Năm chế độ

| Chế độ | Khi dùng | Cách viết prompt |
|---|---|---|
| 0 Không chữ | Ảnh minh họa, lifestyle, phần lớn ảnh trong bài | Câu chặn chữ tự thêm, nêu vật nền: "plain unlabeled packaging, no readable text anywhere" |
| 1 Chữ trong cảnh | Biển, bảng, nhãn tự nhiên trong ảnh | Tối đa 3 từ trong ngoặc kép, "appears once"; nói viết tay hay in và nằm trên vật gì |
| 2 Chèn chữ sau | Hero, OG, thumbnail; tiếng Việt có dấu; chữ dài; cần nhiều biến thể | Dựng bố cục banner: vị trí chủ thể, vị trí vùng chữ, một cách tạo vùng (a/b/c), tông vùng, câu chặn chữ (mục "Dựng vùng chữ"). Không có chữ trong ảnh; ghi chú người dùng thêm tiêu đề bằng công cụ thiết kế |
| 3 AI vẽ chữ | Hero, OG, Pinterest cần một bước; người dùng chọn | Theo quy tắc chế độ 3 bên dưới |
| 4 Hai lượt | Cần chữ chắc chắn mà không đổi cảnh; người dùng chọn | Hai prompt: lượt 1 là prompt chế độ 2 nguyên văn; lượt 2 dùng câu chuẩn ở mục Chế độ 4 |

## Dựng vùng chữ (chế độ 2, dùng lại ở 3 và 4)

Ảnh chế độ 2 là một bố cục banner có chủ đích, không chỉ là "khoảng trống" chung chung. Prompt nêu lần lượt: chủ thể nằm phía nào (ví dụ một phần ba bên phải), vùng chữ ở phần còn lại, đúng một trong ba cách tạo vùng dưới đây, tông vùng, và câu chặn chữ.

- **(a) Khoảng trống thật.** Gọi tên một bề mặt trơn có thật trong cảnh (tường, trời, sàn, mặt bàn, vải trơn), nêu tông, rồi viết "nothing in that area". Ví dụ: "The left third is a plain dark-grey wall, nothing in that area."
- **(b) Làm mềm hậu cảnh nhẹ.** Chủ thể và tiền cảnh giữ nét; hậu cảnh phía vùng chữ mềm, ít chi tiết, vật vẫn nhận ra được. Ví dụ: "subject and foreground sharp; the background behind the left side softly blurred, low detail, shapes still recognisable". Không dùng từ bokeh và thuật ngữ thông số máy ảnh trong prompt.
- **(c) Mảng phẳng.** Chỉ cho hướng Minh họa: một mảng giấy hoặc màu phẳng ở phía vùng chữ, không có gì khác trên mảng đó. Ví dụ: "a wide flat area of cream paper on the left, nothing else on it".

**Cách chọn** (FR-203): (a) khi cảnh có bề mặt trơn tự nhiên; (b) khi cảnh đông, không có bề mặt trơn (chợ, phố, phòng chật), hoặc hướng Biên tập cần chiều sâu; (c) khi hướng hình là Minh họa. Nếu cảnh đông nhưng có thể đổi góc máy để có tường, trời hoặc sàn trơn làm vùng chữ thì dùng (a). Khối Vùng chữ nói rõ đã chọn cách nào.

**Vị trí và cỡ.** Khung ngang (16:9, 3:2, 1.91:1): vùng chữ chiếm một phần ba hoặc nửa bên trái/phải, chủ thể ở phía đối diện. Khung dọc (2:3, 4:5, 9:16): vùng chữ là dải trên hoặc dải dưới. Cỡ vùng 35–50% khung; tiêu đề dài hoặc tiếng Việt nhiều dòng thì 45–50%.

**Tông và màu chữ gợi ý.** Nền tối trung bình: chữ trắng hoặc kem. Nền sáng dịu: chữ gần đen. Màu thương hiệu (ghi mã hex) chỉ khi đủ tương phản với tông nền; nếu không đủ, gợi ý thêm một dải màu đặc phía sau chữ. Chữ trắng trên tường sáng yếu đọc được ở ảnh lớn nhưng mất khi thu nhỏ, nên ưu tiên nền tối trung bình (bài học từ lượt thử).

Làm mềm hậu cảnh chỉ dùng ở vùng chữ của chế độ 2, 3 và 4 (ngoại lệ trong `references/anti-slop.md`, mục 3); ảnh chế độ 0 và 1 giữ nét toàn cảnh.

## Mẫu khối Vùng chữ (FR-207, FR-208)

Ngay dưới prompt của mỗi ảnh chế độ 2 (và lượt 1 của chế độ 4) là một khối Vùng chữ đủ tám trường. Viết ngắn, ghép bằng " · ", đúng thứ tự:

```markdown
**Vùng chữ:** <vị trí> · cỡ <% khung> · cách tạo: <a, b hoặc c, kèm tên bề mặt hoặc mô tả> · nền <tông> → chữ <màu gợi ý> · lề an toàn ~5% · tiêu đề <số dòng> dòng · <khi cắt khung>
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.
```

- **Vị trí:** phía và phần khung. Khung ngang: 1/3 trái, 1/3 phải, nửa trái hoặc nửa phải. Khung dọc: dải trên hoặc dải dưới.
- **Cỡ:** phần trăm khung (35–50%; tiêu đề dài hoặc tiếng Việt nhiều dòng thì 45–50%).
- **Cách tạo:** a (khoảng trống thật, gọi tên bề mặt), b (làm mềm hậu cảnh nhẹ) hoặc c (mảng phẳng, chỉ hướng Minh họa).
- **Nền → chữ:** nền tối trung bình thì chữ trắng hoặc kem; nền sáng dịu thì chữ gần đen. Màu thương hiệu ghi kèm mã hex, chỉ khi đủ tương phản với nền.
- **Lề an toàn:** khoảng 5% mỗi cạnh.
- **Số dòng tiêu đề:** dự kiến theo tiêu đề, thường 1–2 dòng.
- **Khi cắt khung khác (FR-209):** "còn nguyên ở 1.91:1" khi vùng nằm hai bên; "mất ở 2:3, cần prompt khung dọc riêng" khi vùng sẽ mất sau khi cắt.

Cột Chữ của Kịch bản Media (FR-208): với chế độ 2, 3 và 4, ghi "<số chế độ> <tên chế độ> — <vị trí vùng>", ví dụ "2 chèn chữ sau — 1/3 trái". Với chế độ 0 và 1 chỉ ghi số và tên chế độ. Ảnh chế độ 3 không cần khối riêng, vì vùng chữ đã nằm trong prompt và được ghi ở cột Chữ.

## Quy tắc chế độ 3: AI vẽ chữ

- Đổi từ chế độ 2 sang chế độ 3 hoặc 4: giữ nguyên câu mô tả bố cục, chủ thể và vùng chữ của prompt chế độ 2; tiêu đề đặt trong vùng đã xác định, không đặt ra ngoài vùng (FR-211).
- Prompt chế độ 3 phải dưới 80 từ. Khi chuyển từ chế độ 2, giữ câu chủ thể, câu vùng chữ, câu ảnh thật ("unposed, not retouched, not cinematic") và câu chặn chữ; rút câu ánh sáng, câu máy ảnh và chi tiết vật thừa trước.
- Tiêu đề tối đa khoảng 6 từ, 1–2 dòng; dòng phụ chỉ khi cần, vì mỗi dòng thêm làm tăng nguy cơ sai chính tả.
- Chuỗi chữ chính xác trong ngoặc kép. Nêu kiểu hoa/thường (ví dụ "title case" hoặc "all capitals").
- Kiểu chữ mô tả bằng đặc điểm ("bold condensed sans-serif", "hand-lettered brush script"), không dùng tên font.
- Màu chữ: tên màu; nếu là màu thương hiệu thì ghi mã hex.
- Vị trí và canh lề ("left third, left-aligned"); cỡ tương đối ("about 45% of the frame width").
- Bề mặt nền tương phản phía sau chữ: tường trung tính tối hoặc dải màu đặc. Chữ trắng trên tường sáng yếu đọc được ở ảnh lớn nhưng yếu khi thu nhỏ; đây là bài học từ lượt thử.
- Lề an toàn khoảng 5% mỗi cạnh, vì OG, Pinterest và thumbnail cắt khung khác nhau.
- Luôn kèm câu: "the headline appears once; no other text anywhere".

## Tiếng Việt có dấu (chế độ 3 và 4)

- Khi tiêu đề tiếng Việt có dấu được chọn, pack cảnh báo người dùng thử một ảnh mẫu trên công cụ đang dùng trước khi tạo cả loạt.
- Sai một dấu trong ảnh mẫu thì chuyển tiêu đề đó sang chế độ 2 (chèn chữ sau bằng công cụ thiết kế).
- Khối prompt vẫn viết bằng tiếng Anh; chuỗi chữ trong ảnh giữ nguyên tiếng Việt người dùng cung cấp.

## Chế độ 4: hai lượt

- Lượt 1: prompt chế độ 2 nguyên văn (cảnh có vùng chữ, không có chữ), kèm khối Vùng chữ như chế độ 2 (FR-211).
- Lượt 2: dùng đúng câu `Image 1 = approved scene. Add the headline only; keep everything else unchanged.`, rồi mô tả tiêu đề theo quy tắc chế độ 3 (chuỗi trong ngoặc kép, kiểu chữ, vị trí, nền, lề, "appears once").
- Mục Reference của lượt 2: ảnh tạo từ lượt 1 (ảnh đã duyệt). Ghi rõ điều này trong pack.

## SEO và alt

- Chữ trong ảnh không thay H1 và không thay alt text.
- Ảnh có chữ dùng cho web vẫn có gợi ý alt mô tả nội dung ảnh, một câu, không lặp lại tiêu đề.

## QC chữ: đạt/không đạt

Dùng khi người dùng xin kiểm ảnh có chữ, hoặc khi chẩn đoán ảnh có chữ bị lỗi. Mỗi mục chỉ đạt hoặc không đạt:

- [ ] Đúng chính tả từng ký tự so với chuỗi trong prompt.
- [ ] Đúng dấu tiếng Việt (nếu có).
- [ ] Chỉ xuất hiện một lần; không có chữ nào khác trong ảnh.
- [ ] Đọc được khi thu nhỏ còn khoảng 360 px bề rộng.
- [ ] Đủ tương phản giữa chữ và nền.
- [ ] Không có chữ lạ trên biển, sách hay bao bì.
- [ ] Nằm trong lề an toàn (khoảng 5% mỗi cạnh).

## Ví dụ: hero chế độ 3 (AI vẽ chữ)

Cùng cảnh với ví dụ chế độ 2 (a) bên dưới: đổi từ chế độ 2 sang 3 thì bố cục, chủ thể và vùng chữ giữ nguyên, chỉ thêm tiêu đề vào vùng đó. Cảnh có tường xám tối trung bình và đèn tràn khỏi hộp, hai chỉnh sửa đã thử trong lượt test.

```text
Photo of a living room in December, horizontal 16:9 frame. A crooked tree stands on the right third with bare gaps, a box with lights beside it. A laptop and a kid's sock lie on the floor. The left third is a plain dark-grey wall carrying the headline "Indoor Christmas Decorations" in title case, bold white condensed sans-serif, left-aligned, about 45% of the frame width. Unposed, not retouched, not cinematic. The headline appears once; no other text anywhere.
```

Số từ: 78 (trong khoảng 30–80). Vật gọi tên: cây, hộp, đèn, laptop, tất (5). Câu ánh sáng của ví dụ (a) đã bỏ theo quy tắc chế độ 3, để prompt dưới 80 từ.

## Ví dụ chế độ 2 (chèn chữ sau)

### (a) Hero 16:9, khoảng trống thật

```text
Photo of a living room in December, horizontal 16:9 frame. A crooked tree stands on the right third with bare gaps, a box with lights beside it. A laptop and a kid's sock lie on the floor. Overcast window light from the left. The left third is a plain dark-grey wall, nothing in that area. Unposed, not retouched, not cinematic. No readable text anywhere.
```

Số từ: 64. Vật gọi tên: cây, hộp, đèn, laptop, tất (5).

**Vùng chữ:** 1/3 trái, khoảng 40% khung · cách tạo: tường xám đậm có thật (a) · nền tối trung bình → chữ trắng hoặc kem · lề an toàn ~5% · tiêu đề 1–2 dòng · cắt sang 1.91:1 vẫn còn nguyên; khung 2:3 dùng prompt dọc riêng.
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.

### (b) Hero 16:9, cảnh chợ đông (làm mềm hậu cảnh nhẹ)

Cảnh chợ đông không có bề mặt trơn nên dùng cách (b). Khớp fixture 07.

```text
Photo of a morning vendor at a crowded market, horizontal 16:9 frame. A vendor weighs mangoes on a brass scale on the right third, sharp, with mango crates in front also sharp, and a coiled phone charger on one crate. The left third is a softly blurred background, medium-dark and low in detail, shapes still recognisable as stacked boxes. Overcast daylight from the open side. Candid, slightly off-center. Unposed, not retouched, not cinematic. No readable text anywhere.
```

Số từ: 77. Vật gọi tên: xoài, cân đồng, thùng xoài, sạc điện thoại, hộp (5).

**Vùng chữ:** 1/3 trái, khoảng 40% khung · cách tạo: hậu cảnh làm mềm nhẹ (b), chủ thể và tiền cảnh nét · nền tối trung bình → chữ trắng hoặc kem; nếu hậu cảnh quá rối thì thêm dải màu đặc sau chữ · lề an toàn ~5% · tiêu đề 1–2 dòng · cắt sang 1.91:1 vẫn còn nguyên; khung 2:3 dùng prompt dọc riêng.
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.

### (c) Khung dọc 2:3 (Pinterest), vùng chữ là dải trên

```text
Photo of a half-finished cup of tea and an open notebook on a wooden desk, vertical 2:3 frame. The subject sits in the lower part of the frame: the cup sharp, a pencil across the open page, soft morning daylight from the left. The top band of the frame is a plain pale-cream wall, nothing in that area. Unposed, not retouched, not cinematic. No readable text anywhere.
```

Số từ: 67. Vật gọi tên: cốc, sổ, bút chì (3).

**Vùng chữ:** dải trên, khoảng 40% chiều cao khung · cách tạo: tường kem nhạt có thật (a) · nền sáng dịu → chữ gần đen · lề an toàn ~5% · tiêu đề 1–2 dòng · cắt sang khung ngang thì mất dải trên, cần prompt khung ngang riêng.
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.
