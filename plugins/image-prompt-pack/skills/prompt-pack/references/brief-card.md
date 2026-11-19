# Chốt nhanh: khi nào dừng, các mục và mặc định

Đọc file này khi lập Kịch bản Media, để quyết định có dừng chờ không, mục nào được hỏi và mặc định là gì. Khối Chốt nhanh chỉ in các mục đã kích hoạt và chưa quyết. Khối này không bao giờ chứa tên preset, tên công cụ hay tham số kỹ thuật.

## Khi nào dừng chờ, khi nào xuất luôn

Lượt đầu luôn quét intake trước khi viết prompt. Chỉ dừng khi có ít nhất một trường hợp đặc biệt:

| Tình huống | Kết quả |
|---|---|
| Có ít nhất một trường hợp kích hoạt (mục bên dưới) | Khối Chốt nhanh và Kịch bản Media, không kèm prompt; dừng chờ một câu trả lời |
| Không có trường hợp nào | Xuất pack ngay; khối "Đã dùng mặc định" ở đầu |
| Người dùng nói "đưa luôn" hoặc "không cần hỏi", hoặc không có người trả lời | Xuất pack ngay; khối "Đã dùng mặc định" ở đầu |

Số ảnh hay độ dài bài một mình không là lý do dừng (FR-217). Bài dài hay pack nhiều ảnh vẫn xuất luôn nếu intake đã chốt đủ chữ, phong cách, nội dung và format.

## Bốn trường hợp kích hoạt (FR-215)

1. **Chữ**: có banner, hero, ảnh chia sẻ hoặc thumbnail mà intake chưa chốt cách đặt chữ; hoặc có tiêu đề hay chữ trong ảnh chưa chốt nội dung hoặc ngôn ngữ.
2. **Phong cách**: nội dung hợp với hơn một hướng hình, chọn sai sẽ phải làm lại cả pack, và không có brand guideline trong context. Ví dụ: landing bán hàng có thể đi theo Biên tập hoặc Đời thường.
3. **Nội dung đặc biệt**, phát hiện khi quét bài: chỗ chờ sản phẩm, người hoặc thương hiệu thật, chủ đề nhạy cảm (y tế, tài chính, trẻ em), số liệu cần infographic, nhiều ngôn ngữ.
4. **Format mới lạ**: dạng ảnh không có trong `references/image-types.md` (ví dụ carousel, before/after, chuỗi ảnh kể chuyện, ảnh so sánh, ảnh in ấn), hoặc tỉ lệ và kênh không có ở cột Tỉ lệ.

Điểm nào intake đã chốt rõ thì không được hỏi lại.

## Các mục của khối Chốt nhanh

Tối đa 4 mục. Mục Banner tính là một mục dù có 4 điểm con. Mỗi trường hợp (2), (3), (4) tối đa một mục.

- **Banner** (trường hợp 1, khi chữ thuộc banner, hero, ảnh chia sẻ hoặc thumbnail): bốn điểm, mỗi điểm một mặc định.
  - a. Tiêu đề và số dòng: tiêu đề bài rút gọn tối đa 6 từ, 1 dòng (mặc định), hoặc gửi tiêu đề khác.
  - b. Cách đặt chữ: chèn chữ sau, ảnh cố ý không có chữ (mặc định); AI vẽ luôn tiêu đề; hoặc hai lượt.
  - c. Vùng chữ: phía nào và cách tạo (khoảng trống thật hoặc làm mềm hậu cảnh). Mặc định do model đề xuất theo cảnh, kèm một câu lý do.
  - d. Các khung: ví dụ hero 16:9, ảnh chia sẻ 1.91:1, Pinterest 2:3. Mặc định theo kênh trong bài.
  - Màu chữ lấy từ brand guideline nếu có. Không hỏi màu, kiểu chữ, CTA hay logo.
- **Trường hợp 1 do chữ thuộc ảnh khác** (infographic, biển, bảng): không dùng mục Banner; thay bằng một mục Chữ hỏi nội dung và ngôn ngữ của chữ đó, kèm mặc định.
- **Phong cách** (trường hợp 2): chọn Đời thường, Biên tập/chuyên nghiệp hoặc Minh họa, mặc định kèm một câu lý do.
- **Sản phẩm** (trường hợp 3, khi có chỗ chờ sản phẩm): số chỗ và vị trí; làm mockup ở đó không; mặc định không.
- **Format mới lạ** (trường hợp 4): nêu đúng format đó, lý do "format mới lạ", và mặc định là format gần nhất trong bảng loại ảnh, hoặc bỏ format này.

Mỗi mục nêu lý do kích hoạt (trường hợp nào, thấy ở đâu trong bài), một mặc định và tối đa ba lựa chọn (FR-217). Trường hợp không kích hoạt thì mục không xuất hiện.

## Ba hướng hình và cách chọn

- **Đời thường**: ảnh như chụp bằng điện thoại trong nhà hoặc ngoài đời, có người hoặc đồ đang dùng dở, có vật lạc chủ đề. Dùng preset nhóm R.
- **Biên tập/chuyên nghiệp**: ảnh chỉn chu kiểu tạp chí, thời trang, sản phẩm có ánh sáng rõ. Dùng preset nhóm E.
- **Minh họa thủ công**: tranh giấy cắt, risograph, màu nước, linocut cho ảnh khái niệm. Dùng preset nhóm S.

Gợi ý ánh xạ: bài hướng dẫn đời sống, how-to → Đời thường; thời trang, mỹ phẩm, thương hiệu cao cấp, trang bán hàng → Biên tập; khái niệm trừu tượng → Minh họa. Hướng hình do model chọn cho mọi pack; khi mục Phong cách hiện ra, nêu hướng mặc định kèm một câu lý do. Một pack có thể phối hướng theo từng ảnh; ghi hướng của từng ảnh ở cột Hướng.

## Quy tắc trình bày khối

- Chỉ in mục đã kích hoạt và chưa quyết; đánh số lại liên tục từ 1.
- Mỗi mục có lý do kích hoạt, một mặc định và tối đa ba lựa chọn, mô tả bằng kết quả nhìn thấy (ảnh trông thế nào, chữ nằm ở đâu, bao nhiêu ảnh).
- Không có preset ID, tên công cụ tạo ảnh hay thiết kế, tham số kỹ thuật, và không vẽ sơ đồ bố cục bằng ký tự; vùng chữ mô tả bằng lời. Tỉ lệ khung như "16:9" là kết quả nhìn thấy nên được phép.
- Khối đặt trên Kịch bản Media. Ở lượt chờ không có khối prompt nào.
- Format các ảnh còn lại chốt qua bảng Kịch bản Media, dưới bảng có dòng: sửa theo số dòng, ví dụ "ảnh 3 đổi 4:5, bỏ ảnh 5", hoặc trả "ok". Không hỏi từng ảnh.
- "ok" → xuất pack theo mặc định, không hỏi thêm. Trả lời một phần, ví dụ "Phong cách: lựa chọn 2, còn lại ok" → mục đã nêu theo lựa chọn, mục còn lại theo mặc định.
- Trả lời sửa theo số dòng → chỉ áp đúng dòng đó, giữ nguyên các dòng khác.
- Người dùng hỏi việc khác khi đang chờ → không tự xuất pack. Khi họ quay lại, giữ khối đã đưa.
- Sau khi có pack, người dùng đổi một mục → chỉ viết lại các prompt bị ảnh hưởng, và nói ngắn những ảnh nào đã đổi.

## Mẫu khối khi dừng

```markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Banner (lý do: <trường hợp 1, thấy ở đâu trong bài>)
   a. Tiêu đề: "<tiêu đề bài, tối đa 6 từ>", 1 dòng (mặc định) · <lựa chọn 2>
   b. Cách đặt chữ: chừa vùng, ảnh cố ý không có chữ, thêm tiêu đề sau bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề · hai lượt
   c. Vùng chữ: <phía và cách tạo> (mặc định — <một câu lý do>) · <lựa chọn 2>
   d. Khung: <các khung> (mặc định theo kênh) · <lựa chọn 2>
2. <Phong cách, Sản phẩm hoặc Format mới lạ: chỉ mục kích hoạt, mỗi mục kèm lý do và mặc định>

## Kịch bản Media
… bảng đủ cột như SKILL.md, cột Chữ có vị trí vùng …
Sửa format theo số dòng, ví dụ "ảnh 3 đổi 4:5, bỏ ảnh 5", hoặc trả "ok".
```

## Ví dụ điền sẵn: bài trang trí Giáng sinh trong nhà

Bài dài (khoảng 2.900 từ) có hero đã có tiêu đề nhưng chưa chốt cách đặt chữ, và hai chỗ chờ sản phẩm. Trường hợp 1 (Chữ) và 3 (Nội dung đặc biệt) kích hoạt, nên dừng. Trường hợp 2 và 4 không kích hoạt, nên không có mục Phong cách hay Format mới lạ.

```markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Banner (lý do: hero có tiêu đề "Indoor Christmas Decorations" nhưng chưa chốt cách đặt chữ; thấy ở đầu bài)
   a. Tiêu đề: "Indoor Christmas Decorations", 1 dòng (mặc định) · "Indoor Christmas Decorations: Easy Room-by-Room Ideas", 2 dòng
   b. Cách đặt chữ: chừa vùng, ảnh cố ý không có chữ, thêm tiêu đề sau bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề · hai lượt
   c. Vùng chữ: 1/3 trái trên mảng tường xám đậm (mặc định — cảnh có tường trơn) · làm mềm hậu cảnh bên trái
   d. Khung: hero 16:9 + ảnh chia sẻ 1.91:1 (mặc định) · thêm Pinterest 2:3
2. Sản phẩm (lý do: bài có hai chỗ chờ sản phẩm, chăn trên sofa ở phòng khách và chăn trên giường ở phòng ngủ)
   Làm mockup ở hai chỗ đó không? Mặc định: không · chỉ chỗ sofa · cả hai chỗ
```

## Mẫu "Đã dùng mặc định" (xuất luôn)

Khối ngắn, một dòng cho mỗi mục đã quyết bằng mặc định, đặt ở đầu phản hồi và trước Kịch bản Media. Mục nào đã có trong intake thì không xuất hiện. Khi có hero hoặc ảnh chia sẻ, dòng Chữ phải nêu vùng chừa sẵn (FR-216):

```markdown
## Đã dùng mặc định
- Hướng hình: Đời thường, vì bài cần cảm giác chụp thật trong nhà.
- Chữ: hero chừa vùng chèn tiêu đề ở 1/3 trái; ảnh cố ý không có chữ. Các ảnh khác không chữ.
- Số ảnh: 3 ảnh, theo loại ảnh trong image-types.md.
```
