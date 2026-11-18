# Chữ trong ảnh: năm chế độ, quy tắc và QC

Mỗi ảnh có đúng một chế độ chữ, ghi ở cột Chữ của Kịch bản Media. Mặc định: hero, ảnh chia sẻ (OG) và thumbnail dùng chế độ 2 (chèn chữ sau); ảnh khác dùng chế độ 0 (không chữ); chế độ 3 và 4 chỉ khi người dùng chọn.

## Năm chế độ

| Chế độ | Khi dùng | Cách viết prompt |
|---|---|---|
| 0 Không chữ | Ảnh minh họa, lifestyle, phần lớn ảnh trong bài | Câu chặn chữ tự thêm, nêu vật nền: "plain unlabeled packaging, no readable text anywhere" |
| 1 Chữ trong cảnh | Biển, bảng, nhãn tự nhiên trong ảnh | Tối đa 3 từ trong ngoặc kép, "appears once"; nói viết tay hay in và nằm trên vật gì |
| 2 Chèn chữ sau | Hero, OG, thumbnail; tiếng Việt có dấu; chữ dài; cần nhiều biến thể | Chủ thể chiếm một phần khung; vùng trống có vị trí rõ, tương phản trung bình hoặc tối; không có chữ trong ảnh; ghi chú người dùng thêm tiêu đề bằng công cụ thiết kế |
| 3 AI vẽ chữ | Hero, OG, Pinterest cần một bước; người dùng chọn | Theo quy tắc chế độ 3 bên dưới |
| 4 Hai lượt | Cần chữ chắc chắn mà không đổi cảnh; người dùng chọn | Hai prompt: lượt 1 tạo cảnh có vùng trống; lượt 2 dùng câu chuẩn ở mục Chế độ 4 |

## Quy tắc chế độ 3: AI vẽ chữ

- Tiêu đề tối đa khoảng 6 từ, 1–2 dòng; dòng phụ chỉ khi cần, vì mỗi dòng thêm làm tăng nguy cơ sai chính tả.
- Chuỗi chữ chính xác trong ngoặc kép. Nêu kiểu hoa/thường (ví dụ "title case" hoặc "all capitals").
- Kiểu chữ mô tả bằng đặc điểm ("bold condensed sans-serif", "hand-lettered brush script"), không dùng tên font.
- Màu chữ: tên màu; nếu là màu thương hiệu thì ghi mã hex.
- Vị trí và canh lề ("left third, left-aligned"); cỡ tương đối ("about 45% of the frame width").
- Bề mặt nền tương phản phía sau chữ: tường trung tính tối hoặc dải màu đặc. Chữ trắng trên tường sáng đọc được ở ảnh lớn nhưng yếu khi thu nhỏ; đây là bài học từ lượt thử.
- Lề an toàn khoảng 5% mỗi cạnh, vì OG, Pinterest và thumbnail cắt khung khác nhau.
- Luôn kèm câu: "the headline appears once; no other text anywhere".

## Tiếng Việt có dấu (chế độ 3 và 4)

- Khi tiêu đề tiếng Việt có dấu được chọn, pack cảnh báo người dùng thử một ảnh mẫu trên công cụ đang dùng trước khi tạo cả loạt.
- Sai một dấu trong ảnh mẫu thì chuyển tiêu đề đó sang chế độ 2 (chèn chữ sau bằng công cụ thiết kế).
- Khối prompt vẫn viết bằng tiếng Anh; chuỗi chữ trong ảnh giữ nguyên tiếng Việt người dùng cung cấp.

## Chế độ 4: hai lượt

- Lượt 1: cảnh theo chế độ 2 (có vùng trống, không chữ).
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

Cảnh lấy từ bài trang trí Giáng sinh trong nhà. Đã áp hai chỉnh sửa gợi ý từ lượt thử: tường xám trung tính thay cho tường nhạt, và đèn tràn khỏi hộp thay cho đèn rối.

```text
16:9 phone photo of an ordinary living room a week before Christmas. A crooked tree on the right, bare gaps; beside it a box with lights spilling out. A laptop and a kid's sock lie on the floor. Cool overcast window light. The left third is a plain mid-grey wall carrying the headline "Indoor Christmas Decorations" in title case, bold white condensed sans-serif, one line, 45% of frame width, five percent margin. The headline appears once; no other text anywhere.
```

Số từ: 80 (trong khoảng 30–80). Vật gọi tên: cây, hộp, đèn, laptop, tất (5).

## Ví dụ: hero chế độ 2 cùng cảnh

```text
16:9 phone photo of an ordinary living room a week before Christmas. A crooked tree on the right, bare gaps; beside it a box with lights spilling out. A laptop and a kid's sock lie on the floor. Cool overcast window light. The left third is a plain mid-grey wall with clean empty space for a headline added later. No readable text anywhere.
```

Số từ: 63. Vật gọi tên: cây, hộp, đèn, laptop, tất (5). Ghi chú cho người dùng: thêm tiêu đề "Indoor Christmas Decorations" bằng công cụ thiết kế vào vùng tường bên trái.
