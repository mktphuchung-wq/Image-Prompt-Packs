# Chốt nhanh: khi nào dừng, bốn mục và mặc định

Đọc file này khi lập Kịch bản Media, để quyết định có hỏi không, hỏi mục nào và mặc định là gì. Khối Chốt nhanh chỉ in các mục chưa quyết. Khối này không bao giờ chứa tên preset, tên công cụ hay tham số kỹ thuật.

## Khi nào dừng chờ, khi nào xuất luôn

| Tình huống | Khối | Dừng chờ |
|---|---|---|
| Pack dự kiến từ 4 ảnh, hoặc bài dài (khoảng 800 từ trở lên, hoặc từ 4 mục lớn trở lên) | "Chốt nhanh" | Có. Không kèm prompt; chờ một câu trả lời |
| 1–3 ảnh; hoặc người dùng nói "đưa luôn" hoặc "không cần hỏi"; hoặc không có người để trả lời | "Đã dùng mặc định" (ngắn), đặt đầu phản hồi | Không. Xuất pack ngay |
| Intake đã quyết mọi mục | Không có khối | Không |

Bài chưa đạt ngưỡng dài (dưới khoảng 800 từ và chưa đến 4 mục lớn) mà dự kiến từ 3 ảnh trở xuống thì được coi là yêu cầu ngắn.

## Bốn mục

| Mục | Vì sao hỏi | Mặc định | Bỏ qua khi |
|---|---|---|---|
| 1. Hướng hình và mức đời thường | Quyết định cả pack trông như thế nào; là nguyên nhân chính của ảnh dàn dựng | Model chọn theo loại bài và kênh, kèm một câu lý do (xem ba hướng bên dưới) | Người dùng đã nêu phong cách, hoặc có brand guideline trong context |
| 2. Chữ trong ảnh | Đổi cấu trúc prompt và cần công cụ thiết kế | Hero, ảnh chia sẻ, thumbnail: chèn chữ sau (chế độ 2); ảnh khác: không chữ | Người dùng đã nêu chữ hoặc chế độ |
| 3. Sản phẩm và mockup | Cần ảnh tham chiếu thật và quy tắc trung thực | Không làm mockup | Intake không nhắc sản phẩm và không có chỗ chờ sản phẩm; khi đó mục không xuất hiện |
| 4. Số ảnh, tỉ lệ, kênh | Ảnh chia sẻ, Pinterest, story cần khung khác | Số ảnh theo cấu trúc bài và loại ảnh trong `image-types.md` | Người dùng đã nêu số ảnh và tỉ lệ |

## Ba hướng hình và cách chọn

- **Đời thường**: ảnh như chụp bằng điện thoại trong nhà, có người hoặc đồ đang dùng dở, có vật lạc chủ đề. Dùng preset nhóm R.
- **Biên tập/chuyên nghiệp**: ảnh chỉn chu kiểu tạp chí, thời trang, sản phẩm có ánh sáng rõ. Dùng preset nhóm E.
- **Minh họa thủ công**: tranh giấy cắt, risograph, màu nước, linocut cho ảnh khái niệm. Dùng preset nhóm S.

Gợi ý ánh xạ: bài hướng dẫn đời sống, how-to → Đời thường; thời trang, mỹ phẩm, thương hiệu cao cấp, trang bán hàng → Biên tập; khái niệm trừu tượng → Minh họa. Một pack có thể phối hướng theo từng ảnh; ghi hướng của từng ảnh ở cột Hướng. Mục 1 luôn kèm một câu lý do, ví dụ "bài hướng dẫn trong nhà, người đọc cần thấy nhà thật".

## Quy tắc trình bày khối

- Chỉ in mục chưa quyết; đánh số lại liên tục từ 1.
- Mỗi mục có một mặc định và tối đa ba lựa chọn, mô tả bằng kết quả nhìn thấy (ảnh trông thế nào, chữ nằm ở đâu, bao nhiêu ảnh).
- Không có preset ID, tên công cụ tạo ảnh hay thiết kế, tham số kỹ thuật. Tỉ lệ khung như "16:9" là kết quả nhìn thấy nên được phép.
- Khối đặt trên Kịch bản Media. Ở lượt chờ không có khối prompt nào.
- "ok" → xuất pack theo mặc định, không hỏi thêm. Trả lời một phần, ví dụ "hướng B, còn lại ok" → mục đã nêu theo lựa chọn, mục còn lại theo mặc định.
- Người dùng hỏi việc khác khi đang chờ → không tự xuất pack. Khi họ quay lại, giữ khối đã đưa.
- Sau khi có pack, người dùng đổi một mục → chỉ viết lại các prompt bị ảnh hưởng, và nói ngắn những ảnh nào đã đổi.

## Mẫu khối (lượt chờ)

```markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Hướng hình: <mặc định> (mặc định — <một câu lý do>) · <lựa chọn 2> · <lựa chọn 3>
2. Chữ trong ảnh: Hero và ảnh chia sẻ chừa vùng để chèn tiêu đề sau bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề "<chuỗi>" · Không chữ. Các ảnh khác: không chữ.
3. Sản phẩm: bài có <N> chỗ chờ sản phẩm (<vị trí>). Làm mockup ở đó không? Mặc định: không.
4. Số ảnh: <N> ảnh; hero <tỉ lệ>, ảnh chia sẻ <tỉ lệ>. Giữ nguyên?
```

Khi một mục đã rõ từ intake, bỏ mục đó và đánh số lại. Khi mọi mục đã rõ, không có khối.

## Ví dụ điền sẵn: bài trang trí Giáng sinh trong nhà

Bài dài (khoảng 2.900 từ, sáu mục lớn) có hai chỗ chờ sản phẩm: chăn trên sofa và chăn trên giường. Pack dự kiến 7 ảnh, nên Chốt nhanh dừng chờ.

```markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Hướng hình: Đời thường (mặc định — bài hướng dẫn trang trí trong nhà, người đọc cần thấy nhà thật) · Biên tập: ảnh chỉn chu kiểu tạp chí nhà cửa cho hero · Minh họa: tranh giấy cắt cho ảnh bố cục nhà
2. Chữ trong ảnh: hero và ảnh chia sẻ chừa vùng để chèn tiêu đề sau bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề "Indoor Christmas Decorations" · Không chữ. Các ảnh khác: không chữ.
3. Sản phẩm: bài có 2 chỗ chờ sản phẩm, chăn trên sofa (phòng khách) và chăn trên giường (phòng ngủ). Làm mockup ở hai chỗ đó không? Mặc định: không.
4. Số ảnh: 7 ảnh; hero 16:9, bốn ảnh minh họa trong bài 4:3, một infographic 4:3, ảnh chia sẻ 1.91:1. Giữ nguyên?
```

## Mẫu "Đã dùng mặc định" (xuất luôn)

Khối ngắn, một dòng cho mỗi mục đã quyết bằng mặc định, đặt ở đầu phản hồi và trước Kịch bản Media. Mục nào đã có trong intake thì không xuất hiện:

```markdown
## Đã dùng mặc định
- Hướng hình: Đời thường, vì bài cần cảm giác chụp thật trong nhà.
- Chữ: hero chèn chữ sau; các ảnh khác không chữ.
- Số ảnh: 3 ảnh, theo loại ảnh trong image-types.md.
```
