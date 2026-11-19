# Loại ảnh và cách chọn

Dùng bảng này khi lập Kịch bản Media: mỗi vị trí ảnh chọn đúng một loại, rồi chọn tỉ lệ, hướng, chế độ chữ và preset phù hợp. Tỉ lệ viết bằng lời trong prompt, ví dụ "vertical 4:5 frame".

| Loại | Mục đích và kênh | Tỉ lệ thường dùng | Hướng gợi ý | Chữ mặc định | Preset hợp | Rủi ro và cách tránh |
|---|---|---|---|---|---|---|
| Hero (ảnh bìa bài viết) | Mở bài, thể hiện chủ đề trong một cảnh; blog, trang landing | 16:9 hoặc 3:2 | Đời thường; Biên tập cho thương hiệu, thời trang | 2 chèn chữ sau — 1/3 trái hoặc phải (khung dọc: dải trên/dưới) | R02, R08, R03; E01, E02 khi hướng Biên tập | Cảnh quá đẹp kiểu poster; chọn cảnh đời thường có vật lộn xộn; chừa vùng trống khi chèn chữ |
| Minh họa trong bài | Gợi một ý chính, thường mỗi H2 lớn một ảnh khi ý đó cần hình; blog | 4:3 hoặc 3:2 | Minh họa; Đời thường cho cảnh sinh hoạt | 0 không chữ | S01, S02, S06; R01 hoặc R10 cho cảnh đời thường | Một phong cách lặp cho cả bài; xen kẽ phong cách nhưng giữ chung bảng màu |
| Infographic (sơ đồ có chữ) | Tóm tắt các bước hoặc con số; blog, mạng xã hội | 4:3 hoặc vuông | Minh họa | 2 (tiêu đề) hoặc 1 (số ngắn trong cảnh) | S01, S02 | Chữ vỡ, méo; theo chế độ 1 hoặc 2 trong `references/text-in-image.md` |
| Ảnh chia sẻ mạng xã hội (OG) | Ảnh khi bài được chia sẻ; Facebook, LinkedIn, link preview | 1.91:1 (khoảng 1200×630); 1:1 khi cần | Đời thường | 2 chèn chữ sau — 1/3 hoặc nửa trái/phải | R01, R09, R10 | Giữ vùng trống ở một bên để chèn chữ sau; chủ thể không nằm sát mép khung |
| Thumbnail hoặc banner có tiêu đề | Ảnh có tiêu đề ngắn; video, bài nổi bật, Pinterest | 16:9; Pinterest 2:3; story 9:16 | Biên tập hoặc Đời thường | 2 chèn chữ sau — 1/3 trái hoặc phải (khung dọc: dải trên/dưới) | S05, S08; E01 cho thương hiệu thời trang | Chữ tiếng Việt có dấu dễ méo; dùng chế độ 2, hoặc chế độ 1 với chữ rất ngắn trong ngoặc kép |
| Lifestyle hoặc UGC | Người thật trong đời sống, cầm vật, dùng sản phẩm; mạng xã hội, trang sản phẩm | 4:5 (Instagram), 9:16 (story), 1:1 | Đời thường | 0 không chữ | R01, R05, R08, R12 | Sản phẩm có thiết kế thật phải có Reference và ghép sau; không làm người trông giống một người nổi tiếng hay người thật cụ thể |
| Mockup sản phẩm (chỉ khi người dùng xác nhận ở Chốt nhanh mục 3, hoặc tự yêu cầu) | Cho thấy sản phẩm trong bối cảnh; trang bán hàng | Theo nền tảng, thường 1:1 hoặc 4:5 | Biên tập hoặc Đời thường | 0 không chữ | R06 hoặc E03, kèm Reference | Không tự đề xuất khi người dùng chưa chọn; AI không vẽ lại thiết kế hay logo; ghi chú ghép thiết kế thật và giữ metadata AI (anti-slop mục 5) |

Ghi chú: khung OG 1.91:1 là khung chia sẻ, nên đặt chủ thể không nằm sát mép. Pinterest 2:3 và Instagram 4:5 là khung dọc; story và reel là 9:16.

**Vùng chữ theo khung (FR-209):** khung ngang (16:9, 3:2, 1.91:1) đặt vùng chữ ở một phần ba hoặc nửa bên trái/phải; khung dọc (2:3, 4:5, 9:16) đặt vùng chữ ở dải trên hoặc dải dưới. Hero 16:9 cắt sang 1.91:1 thường còn nguyên vùng chữ nếu vùng nằm ở hai bên; cắt sang 2:3 hoặc 9:16 thì vùng chữ thường mất, khi đó cần một prompt khung dọc riêng.

**Format mới lạ (FR-215 mục 4):** loại ảnh không có trong bảng này (ví dụ carousel, before/after, chuỗi ảnh kể chuyện, ảnh so sánh, ảnh in ấn), hoặc tỉ lệ và kênh không có ở cột Tỉ lệ. Chỉ ảnh có format mới lạ mới có câu hỏi riêng ở lượt đầu (xem `references/brief-card.md`).

## Đề xuất số ảnh (FR-006)

- Bài khoảng 1.500 từ thường có 3–8 ảnh: một hero, một minh họa cho mỗi ý chính lớn khi ý đó cần hình, và một ảnh chia sẻ mạng xã hội.
- Nội dung dài nhiều nghìn từ: đề xuất số ảnh theo cấu trúc bài, không làm ảnh cho mọi đoạn; nói rõ người dùng có thể tăng hoặc giảm.
- Người dùng đã nêu số ảnh hoặc tỉ lệ: theo đúng số và tỉ lệ đó.
- Yêu cầu ngắn không nêu số ảnh: chọn 3 ảnh đủ dùng cho mục đích đã nêu, và ghi số đó trong khối "Đã dùng mặc định".
- Số ảnh và độ dài bài không là lý do dừng lượt đầu; chỉ trường hợp đặc biệt mới dừng (xem `references/brief-card.md`).

## Chữ trong ảnh

Mỗi ảnh có một chế độ chữ (0–4), xem `references/text-in-image.md`: không chữ, chữ ngắn trong cảnh, chèn chữ sau, AI vẽ chữ hoặc hai lượt. Cột Chữ của Kịch bản Media ghi chế độ đó. Hero, ảnh chia sẻ và thumbnail mặc định chèn chữ sau.
