# Ví dụ chuẩn đầu ra

Hai ví dụ minh họa đúng hình dạng đầu ra trong `SKILL.md`. Ví dụ A là một bài có hero cần chữ, đi qua hai lượt: Chốt nhanh dừng chờ vì cách đặt chữ chưa chốt, rồi pack sau "ok". Ví dụ B là một lượt sửa prompt. Các prompt ở đây là ví dụ, không phải khuôn bắt buộc.

## Ví dụ A: bài có hero cần chữ, hai lượt

Intake giả định: bài blog tiếng Việt khoảng 1.500 từ, chủ đề "Cách bố trí góc làm việc tại nhà trong căn hộ nhỏ". Bài có ba phần: chọn vị trí gần cửa sổ, tách khu làm việc khỏi khu ngủ bằng kệ hoặc rèm, và giữ bàn gọn. Bài không nêu sản phẩm và không yêu cầu mockup. Intake chưa nói hero và ảnh chia sẻ có chữ hay không, nên trường hợp đặc biệt (1) kích hoạt.

### Lượt 1: Chốt nhanh và Kịch bản Media (dừng chờ)

## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Banner (lý do: hero và ảnh chia sẻ có chỗ đặt chữ, nhưng intake chưa chốt cách đặt chữ; thấy ở ảnh 1 và ảnh 5 của bảng dưới)
   a. Tiêu đề: "Góc làm việc trong căn hộ nhỏ", 1 dòng (mặc định) · "Góc làm việc trong căn hộ nhỏ: bố trí ba khu", 2 dòng
   b. Cách đặt chữ: chừa vùng, ảnh cố ý không có chữ, thêm tiêu đề sau bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề · hai lượt
   c. Vùng chữ: 1/3 trái trên mảng tường xám trung tính (mặc định — cảnh có tường trơn cạnh cửa sổ) · làm mềm hậu cảnh bên trái
   d. Khung: hero 16:9 + ảnh chia sẻ 1.91:1 (mặc định) · thêm Pinterest 2:3

## Kịch bản Media
**Nội dung:** Hướng dẫn bố trí một góc làm việc tại nhà trong căn hộ dưới 50 m². Trọng tâm là chọn vị trí gần cửa sổ, tách khu làm việc khỏi khu ngủ và giữ bàn gọn để làm việc được cả ngày.
**Mục tiêu:** Giúp người đọc có một góc làm việc đủ sáng, ít rối, không cần đổi cả căn hộ. · **Đối tượng:** Người đi làm tại nhà, sống trong căn hộ nhỏ ở thành phố. · **Kênh:** Blog và chia sẻ trên mạng xã hội.
**Hướng hình ảnh:** Ảnh đời thường, ánh sáng cửa sổ thật, không dựng studio. Bảng màu chung: be ấm, xanh sage, than chì.

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | Một góc làm việc gọn, sáng, ngay đầu bài | hero | 16:9 | Đời thường | toàn cảnh | ngang tầm mắt | trung tính ban ngày, cửa sổ | sáng sớm | một người | 2 chèn chữ sau — 1/3 trái |
| 2 | Minh họa tách khu | Mục tách khu làm việc khỏi khu ngủ | Gợi ý bằng hình: kệ thấp chia khu | minh họa | 4:3 | Minh họa | trung cảnh | đứng nhìn xuống | trung tính ban ngày | ban ngày | không | 0 không chữ |
| 3 | Minh họa ánh sáng | Mục chọn vị trí gần cửa sổ | Ánh đèn bàn buổi tối trên trang giấy | minh họa | 3:2 | Biên tập | cận chi tiết | ngang tầm mắt | ấm tungsten tối, đèn bàn | tối | tay | 0 không chữ |
| 4 | Infographic ba khu | Cuối bài | Tóm tắt ba khu bố trí; tiêu đề thêm sau | infographic | 4:3 | Minh họa | toàn cảnh | đứng nhìn xuống | trung tính ban ngày | ban ngày | không | 2 chèn chữ sau — 1/3 phải |
| 5 | Ảnh chia sẻ | Ảnh đại diện khi chia sẻ | Bàn làm việc nhìn từ trên xuống cho link preview | OG | 1.91:1 | Đời thường | trung cảnh | đứng nhìn xuống | lạnh u ám, cửa sổ | chiều nhiều mây | không | 2 chèn chữ sau — 1/3 trái |

Sửa format theo số dòng, ví dụ "ảnh 3 đổi 4:5, bỏ ảnh 5", hoặc trả "ok".

Lượt này chưa có prompt. Trả lời "ok" để nhận pack theo mặc định. Nếu người dùng trả "ảnh 3 đổi 4:5, bỏ ảnh 5, còn lại ok", pack chỉ đổi ảnh 3 sang khung 4:5 và bỏ ảnh 5; bốn ảnh còn lại giữ nguyên dòng trong bảng.

### Lượt 2: sau "ok" (pack theo mặc định)

## Kịch bản Media
(Bảng như trên; không đổi vì người dùng trả lời "ok".)

## Prompt Pack
Phong cách chung: ánh sáng cửa sổ thật, bảng màu be ấm, xanh sage và than chì, không dựng studio. Số từ tự kiểm: ảnh 1 — 75; ảnh 2 — 69; ảnh 3 — 55; ảnh 4 — 77; ảnh 5 — 67.

### Ảnh 1 — Hero
```text
Photo of a woman with her hair tied back typing on a laptop at a wooden desk, on the right third of the frame. Half-finished tea, a coiled phone charger and a stack of paper on the desk. The left third is a plain mid-grey wall, nothing in that area. Soft morning daylight from the left. Shot on a recent smartphone, eye level, horizontal 16:9 frame. Unposed, not retouched, not cinematic. No readable text anywhere.
```
**Vùng chữ:** 1/3 trái, khoảng 40% khung · cách tạo: tường xám trung tính có thật (a) · nền tối trung bình → chữ trắng hoặc kem · lề an toàn ~5% · tiêu đề 1 dòng · cắt sang 1.91:1 vẫn còn nguyên; khung 2:3 dùng prompt dọc riêng.
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.

### Ảnh 2 — Minh họa tách khu
```text
Hand-cut paper collage of a small apartment corner split by a low bookshelf: a desk with a lamp and a potted plant on one side, a folded futon on the other. Layered torn paper edges, visible glue wrinkles, limited palette of warm beige, sage green and charcoal. Soft light from the top left, flat top-down view, soft shadow under each cut-out piece, horizontal 4:3 frame. No readable text anywhere.
```

### Ảnh 3 — Minh họa ánh sáng
```text
Editorial still-life photo of a hand resting on a blank printed sheet beside a ceramic mug and a small plant on a light wooden desk at night. Warm tungsten desk lamp from the left, a soft pool of light across the sheet. Shot straight-on, deep focus, not retouched. No readable text anywhere, horizontal 3:2 frame.
```

### Ảnh 4 — Infographic ba khu
```text
Flat top-down plan of a small apartment corner in three zones: a desk zone, a shelf zone and a light zone, marked by a sage dot, a cream square and a charcoal line. The right third of the frame is a wide flat area of cream paper, nothing else on it. Three spot colors, sage green, cream and charcoal, visible misregistration, grainy halftone, flat shapes. Flat even light from above. No readable text anywhere, horizontal 4:3 frame.
```
**Vùng chữ:** 1/3 phải, khoảng 35% khung · cách tạo: mảng giấy kem phẳng, cho hướng Minh họa (c) · nền sáng dịu → chữ gần đen · lề an toàn ~5% · tiêu đề 1 dòng · cắt sang 1.91:1 vẫn còn nguyên; khung 2:3 dùng prompt dọc riêng.
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế. Số thứ tự của ba khu cũng thêm bằng công cụ thiết kế.

### Ảnh 5 — Ảnh chia sẻ
```text
Overhead photo of a half-finished cup of tea and an open notebook on a wooden desk, a phone face-down and a pencil across the page, cool overcast afternoon daylight from the window side. Shot from directly above, horizontal 1.91:1 frame. The left third is plain bare wooden desk, nothing in that area. Subject kept away from the edges. Unposed, not retouched, not cinematic. No readable text anywhere.
```
**Vùng chữ:** 1/3 trái, khoảng 35% khung · cách tạo: mặt bàn gỗ trơn có thật (a) · nền sáng dịu → chữ gần đen · lề an toàn ~5% · tiêu đề 1 dòng · cắt sang 16:9 vẫn còn nguyên; khung 2:3 dùng prompt dọc riêng.
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.
**Alt gợi ý:** "Bàn làm việc nhỏ cạnh cửa sổ, nhìn từ trên xuống."

**Vì sao đạt:**
- Đời thường có vật lạc chủ đề và dấu vết người: ảnh 1 có sạc điện cuộn và trà uống dở; ảnh 5 có điện thoại úp mặt và cốc trà uống dở; mỗi vật lạc chủ đề chỉ dùng một lần trong pack.
- Hướng Biên tập ở ảnh 3 không bắt vật lạc đề, nhưng vẫn đủ độ dài, số vật và không có số chẵn.
- Vùng chữ: ảnh 1 và ảnh 5 dùng cách (a) vì có tường và mặt bàn trơn thật; ảnh 4 dùng cách (c) vì hướng Minh họa. Mỗi ảnh chế độ 2 nêu vị trí chủ thể, vị trí vùng, tông và câu chặn chữ, và có khối Vùng chữ đủ trường.
- Bảng đạt FR-108: không hai ảnh liền nhau trùng cả Khung, Độ cao máy và Ánh sáng; ảnh 5 là ánh lạnh u ám; ảnh 1 và ảnh 3 có người hoặc tay; Khung cao nhất là 2 trên 5 ảnh.

## Ví dụ B: sửa ảnh dàn dựng

Ảnh bếp của bài trang trí Giáng sinh (fixture `tests/fixtures/06-staged-images-feedback.md`) ra như một cảnh được sắp đặt. Prompt ban đầu kiểu danh mục, nêu số chẵn, có từ cấm đứng một mình. Đây là ví dụ của thứ cần tránh, dài 117 từ.

```text
Festive kitchen corner at Christmas with two ceramic holiday mugs on a wooden tray, two brushed brass candleholders with red taper candles, a small evergreen wreath on the cabinet door, a red-and-green dish towel on the oven handle, a jar of cinnamon sticks and a bowl of clementines on the counter, a pine garland along the window sill, four cookies on a plate, a small brass bell beside a sugar bowl and two linen napkins folded in a tidy stack. Soft winter daylight from the window, the scene feels cozy and welcoming, slightly imperfect, genuinely lived-in, with subtle household imperfections. Shot on a recent smartphone, eye level, horizontal 3:2 frame. Clean, festive and natural, sharp focus throughout.
```

Mô tả lỗi của người dùng: "Ảnh đơn điệu, quá clean, như được sắp đặt."

**Chẩn đoán:**
- "Two ceramic holiday mugs", "two brushed brass candleholders", "four cookies": số chẵn và đồ thành cặp. Model kiểm kê và xếp đều (dấu hiệu đối xứng, đồ thành cặp).
- Mọi vật đều thuộc Giáng sinh hoặc đồ bếp được styling, không có vật lạc chủ đề (dấu hiệu thuần chủ đề).
- Không ai đang dùng đồ, không có dấu vết sử dụng (dấu hiệu không dấu vết sử dụng).
- Prompt không nói vật nền nên model có thể tự thêm vật không được yêu cầu; cảnh kiểu này hay có tuyết ngoài cửa sổ, nến, chữ trên bảng (dấu hiệu model tự thêm chữ hoặc vật).
- "Soft winter daylight" làm ánh vàng đồng đều. "Slightly imperfect", "genuinely lived-in", "subtle household imperfections" là từ cấm đứng một mình, không kèm chi tiết cụ thể (FR-104).
- Hơn mười vật được gọi tên theo kiểu danh mục, vượt xa mức 5 vật.

Prompt đã sửa (77 từ):

```text
Phone photo of a kitchen counter in late afternoon: one ceramic mug of tea left half-drunk beside a coiled phone charger and a lemon halved on a wooden board, a brass candleholder near the window. Cool overcast window light from the left, uneven across the counter. Shot at standing height, horizontal 3:2 frame, a thumb holding the lemon half steady. Background slightly out of focus, a plain grey tile wall with no readable text on any packaging.
```

**Tự kiểm:** 77 từ (30–80); 5 vật gọi tên (mug, charger, lemon, board, candleholder); không số chẵn và không bố trí đối xứng; có vật lạc chủ đề (dây sạc) và hai dấu vết người (trà uống dở, chanh đang cắt dở); không từ cấm đứng một mình; có câu chặn chữ trên bao bì.

**Đã đổi:**
- Bỏ cặp (hai cốc, hai chân nến) và các số chẵn; giữ một cốc trà uống dở và một chân nến, thêm dây sạc cuộn làm vật lạc chủ đề.
- Thay "soft winter daylight" và các tính từ cấm bằng ánh sáng cửa sổ lạnh u ám, và dấu vết người cụ thể: trà uống dở, chanh đang cắt dở.
- Thêm vật nền (bảng gỗ, tường gạch men xám trơn) và câu chặn chữ trên bao bì: model không còn tự thêm tuyết hay chữ.
