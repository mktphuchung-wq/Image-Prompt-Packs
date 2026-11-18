# Chạy khô US2: yêu cầu một câu, log nhiều chủ đề, intake rỗng

- Ngày chạy: 2026-11-18
- Loại chạy: **chạy khô**. Worker tự đóng vai model, làm theo `SKILL.md` (đã có dòng tự kiểm mới) và bốn file trong `references/`. Không gọi model ngoài, không tạo ảnh.
- Giới hạn: người viết skill và người chấm là cùng một worker; kiểm tra nội bộ, chỉ bắt được lỗi rõ ràng.
- Số vòng sửa SKILL/references: **1** (cùng sửa với us1.md). Bản nháp của US2 được viết trước sửa này và đã được chạy lại.

## Vòng 1: bản nháp trước khi sửa

Khi đối chiếu với `anti-slop.md` mục 2, bản nháp có các lỗi sau (đều không thuộc US2-1 đến US2-8 trực tiếp, nhưng vi phạm FR-010):

| Fixture | Ảnh | Lỗi trong bản nháp |
|---|---|---|
| 02 | 1 | Chỉ có một vật đời thường (cốc giấy) |
| 02 | 2 | Chỉ có một vật đời thường (dây ba lô) |
| 03 | 2 | Có hai khuyết điểm: hạt phim và phơi sáng lố |

Sau vòng sửa: thêm vật đời thường cho fixture 02 ảnh 1 và 2; bỏ hạt phim ở fixture 03 ảnh 2, giữ một khuyết điểm.

## Fixture 02: yêu cầu một câu

Input: `tests/fixtures/02-one-line-request.md`, một dòng: "Cần 3 ảnh cho landing page bán áo hoodie unisex, đăng Facebook ads."

### Đầu ra (vòng 2)

## Kịch bản Media
**Nội dung:** Landing page bán áo hoodie unisex, dùng cho quảng cáo Facebook. Ảnh cần cho thấy chiếc hoodie trong đời sống để người xem tin và bấm vào trang.
**Mục tiêu:** Tăng tỉ lệ nhấp và đặt mua từ quảng cáo. · **Đối tượng:** Người trẻ và người đi làm, mua đồ mặc thoải mái dùng chung được cho nam và nữ. · **Kênh:** Landing page và quảng cáo Facebook (feed).
**Hướng hình ảnh:** Ảnh đời thường, ánh sáng tự nhiên, không dựng studio; bảng màu be, xám đá và xanh rêu cho cả pack.
**Giả định:**
- Số ảnh là 3 theo đúng yêu cầu. Tỉ lệ dùng: ảnh feed 4:5, hero landing 16:9, ảnh chi tiết 1:1.
- Đối tượng và kênh suy từ yêu cầu, chưa có số liệu thật.
- Áo là áo trơn unisex, không nêu mẫu hay thương hiệu, nên không có ảnh mockup. Ảnh lifestyle chỉ gợi bối cảnh và không thể hiện đúng mẫu thật của bạn. Nếu landing cần đúng mẫu thật, bạn nói rõ vị trí cần mockup.

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Ưu tiên |
|---|---|---|---|---|---|---|
| 1 | Hero landing | Đầu trang landing | Mở đầu bằng cảm giác thoải mái khi mặc hoodie | hero | 16:9 | cao |
| 2 | Ảnh feed | Quảng cáo Facebook | Ảnh dọc, đọc được ngay trong feed | mạng xã hội | 4:5 | cao |
| 3 | Ảnh chi tiết | Giữa trang landing | Nhấn vào bo tay và chất vải | lifestyle | 1:1 | trung bình |

## Prompt Pack
Phong cách chung: ảnh đời thường, ánh sáng tự nhiên; áo trơn màu be (oatmeal), không logo, không chữ. Người và nơi chốn đổi giữa các ảnh.

### Ảnh 1 — Hero landing
```text
Photo of two friends in their 20s on a riverside walkway in the late afternoon, one wearing an oatmeal unisex hoodie and the other a grey T-shirt, mid-laugh while leaning on a railing. A paper cup of coffee and a folded map on the rail. Soft warm sunlight from the right. Shot on a recent smartphone, eye level, horizontal 16:9 frame. Visible fabric texture of the fleece on the hoodie. Unposed, not retouched, not cinematic.
```

### Ảnh 2 — Ảnh feed
```text
Photo of a young man in his early 20s in an oatmeal unisex hoodie with the hood down, standing in a narrow café doorway in the morning and looking toward the street, a backpack strap on one shoulder and a paper cup in one hand. Overcast daylight from the front, flat and even. Shot on a recent smartphone, eye level, vertical 4:5 frame. Plain front with no logo or print. Unposed, not retouched, not cinematic.
```

### Ảnh 3 — Ảnh chi tiết
```text
Close-up photo of hands in an oatmeal hoodie sleeve folding the ribbed cuff back, a bare wooden table with a phone face-down beside a cup, daylight from a window on the left. Visible knit texture on the ribbing, short unpolished nails. Shot on a recent smartphone, square 1:1 frame, slightly off-center. Unposed, not retouched.
```

### Chấm fixture 02

| # | Tiêu chí | Kết quả | Bằng chứng |
|---|---|---|---|
| US2-1 | Có mục Giả định nêu rõ giả định đã dùng | Đạt | Mục Giả định ghi số ảnh, tỉ lệ, đối tượng và lý do không có mockup |
| US2-2 | Đúng 3 ảnh theo số người dùng nêu | Đạt | Ba ảnh trong bảng và ba khối prompt |
| US2-3 | Không tự thêm mockup dù có chữ "bán" | Đạt | Không có Reference, không có ảnh mockup; giải thích ở Giả định |
| US2-4 | Nếu hỏi thì tối đa 3 câu, mỗi câu có mặc định | Đạt (không cần hỏi) | Yêu cầu đủ thông tin để lập pack; đầu ra không có câu hỏi |
| US2-5 | Pack đủ cấu trúc theo contract mục 1 | Đạt | Kịch bản, bảng, Prompt Pack, khối prompt cho từng ảnh |

## Fixture 03: log nhiều chủ đề

Input: `tests/fixtures/03-messy-log.md`, gồm ba chủ đề: sửa form liên hệ bị gửi hai lần, lịch đăng bài tuần sau, và bản nháp bài "5 thói quen buổi sáng cho người làm việc tại nhà". Câu cuối là "Làm media cho bài 5 thói quen buổi sáng đi."

### Đầu ra (vòng 2)

Phần đã chọn làm media: bản nháp bài "5 thói quen buổi sáng cho người làm việc tại nhà", vì đây là nội dung người dùng yêu cầu ở cuối log. Bỏ qua phần sửa form liên hệ, lịch đăng bài và nén ảnh cũ, vì đó không phải nội dung cần ảnh.

## Kịch bản Media
**Nội dung:** Bài năm thói quen buổi sáng cho người làm việc tại nhà: dậy đúng giờ và đón ánh sáng, uống nước trước khi mở máy, đi bộ mười phút, viết ba việc quan trọng và tắt thông báo trong hai giờ đầu. Bài dài khoảng 1.300 từ.
**Mục tiêu:** Giúp người làm việc tại nhà có buổi sáng đều nhịp và ít bị phân tâm. · **Đối tượng:** Người làm việc tại nhà và freelancer. · **Kênh:** Blog và chia sẻ trên mạng xã hội.
**Hướng hình ảnh:** Ảnh đời thường buổi sáng, ánh sáng cửa sổ thật, không dựng studio; bảng màu be ấm, xanh sage và than chì.
**Giả định:** Người dùng muốn đủ ảnh cho bài, không cần ảnh riêng cho từng thói quen, nên chọn bốn ảnh theo đề xuất trong log. Bài không có sản phẩm nên không có mockup.

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Ưu tiên |
|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | Cảm giác buổi sáng yên và có nhịp | hero | 16:9 | cao |
| 2 | Dậy sớm | Thói quen 1: dậy đúng giờ | Ánh sáng buổi sáng tràn vào phòng ngủ | minh họa | 3:2 | trung bình |
| 3 | Nước và việc trong ngày | Thói quen 2 và 4: uống nước, viết ba việc | Cốc nước cạnh tờ giấy ghi việc | minh họa | 4:3 | trung bình |
| 4 | Ảnh chia sẻ | Ảnh đại diện khi chia sẻ | Ảnh nhìn từ thấp cho link preview | mạng xã hội (OG) | 1.91:1 | cao |

## Prompt Pack
Phong cách chung: ánh sáng cửa sổ buổi sáng, bảng màu be ấm, xanh sage và than chì; không dựng studio. Người, nơi chốn và góc khung khác nhau giữa các ảnh.

### Ảnh 1 — Hero
```text
Photo of a woman in her 30s standing by a window in a small apartment at sunrise, a mug of tea in both hands, looking out at the quiet street. A notebook and a pair of glasses on a wooden desk behind her. Soft early light from the window on the left, long gentle shadows across the floor. Shot on a recent smartphone, eye level, slightly off-center, horizontal 16:9 frame. Unposed, not retouched, not cinematic. Sharp focus throughout.
```

### Ảnh 2 — Dậy sớm
```text
Photo of a man in his 20s sitting up in bed in a grey T-shirt, pulling back linen curtains as morning light floods a small bedroom, a folded blanket and a phone on the nightstand. Soft diffused daylight from the window on the right. Shot on a 35mm film look, 50mm, horizontal 3:2 frame. A small exposure imperfection in the highlights. Unposed, not cinematic.
```

### Ảnh 3 — Nước và việc trong ngày
```text
Overhead photo of a glass of water beside a closed laptop and a sheet of paper with three handwritten lines, a pencil lying across the page, daylight from the window on the left, items slightly misaligned. Visible water droplets on the glass. Shot from directly above, horizontal 4:3 frame. Unposed, not retouched.
```

### Ảnh 4 — Ảnh chia sẻ
```text
Low-angle photo of an open notebook and a mug of tea on a sunlit windowsill, the street visible in sharp detail through the glass, a pencil lying across the page. Daylight from the left, subject kept away from the edges. Shot from a low angle, horizontal 1.91:1 frame. Unposed, not retouched, sharp focus throughout.
```

### Chấm fixture 03

| # | Tiêu chí | Kết quả | Bằng chứng |
|---|---|---|---|
| US2-6 | Nói rõ đã chọn phần "5 thói quen buổi sáng…" của log | Đạt | Mở đầu đầu ra nêu phần đã chọn và phần đã bỏ |
| US2-7 | Pack đủ cấu trúc; không lẫn nội dung hai chủ đề còn lại | Đạt | Không prompt nào nhắc WordPress, form, lịch đăng hay plugin; bốn ảnh khớp các thói quen trong bài |

## Intake rỗng: "làm ảnh cho bài này" khi không có bài trong context

Input: một câu "làm ảnh cho bài này" trong một hội thoại chưa có bài viết nào.

### Đầu ra

Trong hội thoại này tôi không thấy bài viết hay nội dung nào để làm ảnh. Bạn dán nội dung bài, hoặc gửi đường dẫn tới file để tôi đọc, rồi tôi sẽ lập Kịch bản Media và Prompt Pack. Nếu bạn mới có một ý tưởng, một câu mô tả cũng đủ để tôi bắt đầu.

### Chấm intake rỗng

| # | Tiêu chí | Kết quả | Bằng chứng |
|---|---|---|---|
| US2-8 | Báo không tìm thấy nội dung, xin nội dung hoặc đường dẫn, không bịa | Đạt | Đầu ra không có Kịch bản hay prompt; chỉ xin nội dung |

## Kết quả US2

- Đạt: 8 trên 8 tiêu chí (US2-1 đến US2-8), sau vòng 2.
- Trượt ở vòng 1: không trượt tiêu chí US2; có ba lỗi FR-010 trong bản nháp, đã sửa trước khi ghi lại.
- Số vòng sửa SKILL/references: 1 (dùng chung với us1.md).
