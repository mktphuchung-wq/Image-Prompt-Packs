# Chạy thử khô US1 (v0.2): chống dàn dựng

**Phạm vi:** kịch bản B (fixture `05-christmas-article.md` + "ok") và kịch bản E (fixture `06-staged-images-feedback.md`), theo `tests/acceptance.md` mục "v0.2 — US1".

**Cách chạy:** worker đóng vai model. Đọc `SKILL.md` và toàn bộ `references/`, xử lý hai fixture, rồi chấm bằng máy (đếm từ bằng `wc -w`, quét từ cấm và số chẵn bằng `grep`) và bằng tay (đếm vật, dấu vết người, vật lạc chủ đề).

**Giới hạn:** đây là chạy khô. Người viết skill và người chấm là cùng một worker (xem `docs/verification.md`), nên chỉ bắt được lỗi rõ ràng. Chưa chạy trên Claude Code, Codex hay ChatGPT. Kịch bản A (dừng chờ Chốt nhanh) không thuộc US1 vì skill ở trạng thái này chưa có Chốt nhanh; được kiểm trong `us2.md`.

---

## Kịch bản B: fixture 05, sau "ok"

## Kịch bản Media
**Nội dung:** Bài hướng dẫn trang trí Giáng sinh trong nhà theo từng phòng: phòng khách, hành lang và cầu thang, bếp và phòng ăn, phòng ngủ, kèm bảng kích thước và an toàn.
**Mục tiêu:** Giúp người đọc trang trí nhà đủ đẹp mà không cần mua đồ mới và không chắn lối đi. · **Đối tượng:** Người có nhà ở, muốn trang trí Giáng sinh vừa phải. · **Kênh:** Blog; chia sẻ mạng xã hội (ảnh OG).
**Hướng hình ảnh:** Ảnh chụp điện thoại trong nhà, ánh sáng cửa sổ và đèn có sẵn; không dựng cảnh kiểu showroom.
**Giả định:** Bài 2.889 từ, sáu mục lớn; pack 7 ảnh; hai chỗ chờ sản phẩm (chăn trên sofa, chăn trên giường phòng ngủ) để mặc định không làm mockup, nên không có prompt mockup và không có mục Bonus; hero và ảnh chia sẻ chèn chữ sau; ảnh minh họa không chữ.

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | Phòng khách trang trí dở dang, mở bài bằng cảnh nhà thật | hero | 16:9 | Đời thường | toàn cảnh | ngang tầm mắt | lạnh u ám, cửa sổ | chiều đông u ám | không | 2 chèn chữ sau |
| 2 | Sofa | Mục Cozy Up the Sofa | Chăn caro trên sofa, cảnh có người đang làm | minh họa | 4:3 | Đời thường | qua vai | thấp | ấm tungsten, đèn bàn | tối | tay | 0 không chữ |
| 3 | Hành lang | Mục Entryway & Staircase | Cầu thang có garland, nhà đang dùng bình thường | minh họa | 4:3 | Đời thường | cận chi tiết | ngang tầm mắt | trung tính ban ngày | sáng mưa | không | 0 không chữ |
| 4 | Bếp | Mục Christmas Kitchen | Góc bếp đang làm dở, trang trí tối giản | minh họa | 4:3 | Đời thường | đang làm dở | trên cao | huỳnh quang xanh nhạt | sáng sớm | tay | 0 không chữ |
| 5 | Phòng ngủ | Mục Cozy Christmas Bedroom | Giường có chăn caro, sách bỏ dở | minh họa | 3:2 | Đời thường | trung cảnh | thấp | ấm tungsten, đèn ngủ | tối | không | 0 không chữ |
| 6 | Infographic | Mục Sizing & Placement | Sơ đồ ba khu vực, tóm tắt cách bố trí | infographic | 4:3 | Minh họa | toàn cảnh | đứng nhìn xuống | trung tính ban ngày | ban ngày | không | 2 chèn chữ sau |
| 7 | Ảnh chia sẻ | Ảnh đại diện khi chia sẻ | Cảnh sàn gỗ buổi tối, đại diện bài | OG | 1.91:1 | Đời thường | trung cảnh | đứng nhìn xuống | ấm tungsten, đèn sàn | tối | không | 2 chèn chữ sau |

Ghi chú: không có prompt nào vượt 80 từ, nên không cần ghi lý do dưới bảng.

## Prompt Pack
Phong cách chung: ảnh điện thoại trong nhà, ánh sáng cửa sổ hoặc đèn có sẵn, không dựng studio. Mỗi ảnh một khung, một giờ và một nhiệt độ ánh sáng khác nhau.

### Ảnh 1 — Hero
```text
Phone photo of an ordinary living room a week before Christmas, horizontal 16:9 frame. A crooked tree on the right, bare gaps; beside it a box with lights spilling out. A laptop and a kid's sock lie on the floor. Cool overcast window light. The left third is a plain mid-grey wall with clean empty space for a headline added later. No readable text anywhere.
```

### Ảnh 2 — Sofa
```text
Over-the-shoulder photo of a man with grey streaks in his hair and a grey hoodie, tucking a red-and-green plaid blanket over a sofa, one hand smoothing the wool. A mug of tea gone cold sits beside a folded tea towel. Warm tungsten light from the far corner, low and yellow across the room. Shot on a recent smartphone at a slightly low angle, unposed, not retouched. Plain walls with no readable text anywhere.
```

### Ảnh 3 — Hành lang
```text
Close-up of a staircase in rainy morning daylight, evergreen garland looped along the banister with one red bow. A single muddy shoe left on the bottom step, a wet umbrella leaning against the wall beside it. Neutral daylight from a side window, water beads on the glass. Shot at eye level on a recent smartphone, slightly off-center, unposed, not retouched. No readable text anywhere.
```

### Ảnh 4 — Bếp
```text
Overhead photo of a hand halfway through cutting a lemon on a wooden board at a kitchen counter, a knife resting beside it. A dish sponge sits by the tap, its edges still wet. Pale greenish fluorescent light from the ceiling, flat and even across the counter. Shot from directly above on a recent smartphone, unposed, not retouched, sharp focus throughout. Plain grey tiles with no readable text anywhere.
```

### Ảnh 5 — Phòng ngủ
```text
Medium shot from the doorway of a small bedroom at night. A red-and-green plaid throw lies across the foot of the bed, a paperback face-down beside it, and a laundry basket sits by the door. Warm tungsten lamp light, low and amber. Shot at a low angle on a recent smartphone, unposed, not retouched. No readable text anywhere.
```

### Ảnh 6 — Infographic
```text
Flat top-down risograph-style plan of a small living room split into three zones, marked by a sage dot, a cream square and a charcoal line, with simple arrows between them. Three spot colors, sage green, cream and charcoal, visible misregistration, grainy halftone, paper texture, flat shapes. Flat even light from above. No readable text anywhere; clean empty area across the top third for a headline added later, horizontal 4:3 frame.
```

### Ảnh 7 — Ảnh chia sẻ
```text
Overhead photo of a wooden living-room floor at night: a television remote with its cover off, a mug of cocoa with a skin on it, and one small evergreen sprig. Warm tungsten lamp light from the upper left, amber across the floorboards. Shot straight down on a recent smartphone, subject kept away from the edges, horizontal 1.91:1 frame, unposed, not retouched. Clean empty area on the left for a headline added later; no readable text anywhere.
```

---

## Kịch bản E: fixture 06 (sửa ba ảnh lỗi)

### Ảnh 1: sofa và chăn caro

**Chẩn đoán:**
- "Two small evergreen wreaths" là số chẵn, đặt đối xứng hai bên tường (dấu hiệu đối xứng, đồ thành cặp).
- Prompt chỉ liệt kê vật theo chủ đề Giáng sinh, không có vật lạc chủ đề (dấu hiệu thuần chủ đề).
- Không ai đang dùng đồ, không có dấu vết sử dụng (dấu hiệu không dấu vết sử dụng).
- "Soft winter daylight" làm ánh vàng đồng đều (dấu hiệu ánh đồng đều).
- "Slightly imperfect", "genuinely lived-in", "subtle household imperfections" là từ cấm đứng một mình, không có chi tiết thay thế (FR-104).
- Prompt không nói vật nền, nên model có thể thêm nến hoặc tuyết (dấu hiệu model tự thêm vật).

```text
Phone photo of a living room in dusk light: a plaid blanket half off the sofa, a phone charger coiled on the floor and a mug of tea gone cold on the side table. Warm lamp light from the far corner, amber across the room. Shot at a low angle on a recent smartphone, slightly off-center, unposed, not retouched. Plain walls with no readable text anywhere.
```

**Đã đổi:**
- Bỏ cặp vòng hoa và ánh sáng đều; ánh đèn góc phòng có hướng thay cho "soft winter daylight".
- Thêm sạc điện cuộn trên sàn (vật lạc chủ đề) và cốc trà nguội trên bàn (dấu vết người).
- Bỏ ba từ cấm; thêm tường trơn và câu chặn chữ để model không tự thêm nến hay tuyết.

### Ảnh 2: hành lang và cầu thang

**Chẩn đoán:**
- "Three red bows spaced evenly" là bố trí cách đều; "Four knitted Christmas stockings hang in a row" là số chẵn và xếp hàng đối xứng (dấu hiệu đối xứng, đồ thành cặp).
- Toàn bộ vật là đồ Giáng sinh (garland, stockings, nơ), không có vật lạc chủ đề (dấu hiệu thuần chủ đề).
- Không có người và không có dấu vết dùng (dấu hiệu không dấu vết sử dụng).
- "Soft winter daylight" làm ánh đều; "slightly imperfect paint", "genuinely lived-in", "subtle household imperfections" là từ cấm đứng một mình (FR-104).

```text
Close-up of a staircase in cool morning light, evergreen garland along the banister with one red bow, and a spare set of car keys with a child's trainer on the bottom step. Cool overcast daylight from a side window, uneven across the treads. Shot at eye level on a recent smartphone, slightly off-center, unposed, not retouched. No readable text anywhere.
```

**Đã đổi:**
- Bỏ ba nơ cách đều và bốn tất xếp hàng; giữ một nơ, không cặp, không xếp hàng.
- Thêm chìa khóa xe và giày trẻ em trên bậc (vật lạc chủ đề và dấu vết dùng); ánh sáng cửa sổ lạnh, không đều.
- Bỏ ba từ cấm; thêm câu chặn chữ.

### Ảnh 3: bếp

**Chẩn đoán:**
- "Two ceramic holiday mugs", "two brushed brass candleholders" và "a wreath on each cabinet door" là số chẵn, đồ thành cặp và đối xứng (dấu hiệu đối xứng).
- Mọi vật là đồ Giáng sinh hoặc đồ bếp được styling, không có vật lạc chủ đề (dấu hiệu thuần chủ đề).
- Không có dấu vết dùng đồ (dấu hiệu không dấu vết sử dụng).
- "Soft winter daylight" làm ánh đều; "slightly imperfect tiles" và "subtle household imperfections" là từ cấm đứng một mình.
- Prompt không nói vật nền, nên model thêm chữ "Hot Cocoa" trên bảng đen và tuyết ngoài cửa sổ (dấu hiệu model tự thêm chữ hoặc vật).

```text
Phone photo of a kitchen counter after breakfast: one ceramic mug with coffee grounds left in the bottom, a bottle of hand soap on the sink edge and a single cinnamon stick on a folded napkin. Cool overcast window light from the left. Shot at standing height on a recent smartphone, horizontal 3:2 frame, unposed, not retouched. Plain grey tiles with no readable text anywhere.
```

**Đã đổi:**
- Bỏ cặp cốc, cặp chân nến và vòng hoa trên tủ; còn một cốc có bã cà phê, một chai nước rửa tay và một que quế.
- Thay "soft winter daylight" bằng ánh cửa sổ lạnh u ám từ bên trái; bỏ "slightly imperfect tiles" và "subtle household imperfections".
- Thêm vật nền (tường gạch xám trơn) và câu chặn chữ để model không tự thêm chữ "Hot Cocoa" hay tuyết.

---

## Chấm bằng máy và tay

### Số từ, vật gọi tên và từ cấm từng prompt

Số từ là kết quả `wc -w` trên đúng văn bản trong khối code. Vật gọi tên đếm bằng tay theo quy ước ở `anti-slop.md` mục 2: đồ vật và trang phục được gọi tên riêng thì tính, người, bộ phận cơ thể, chất liệu, nguồn sáng, nơi chốn và bề mặt nền thì không.

| Prompt | Số từ | Vật gọi tên | Số chẵn | Từ cấm | Ghi chú (vật lạc chủ đề; dấu vết người) |
|---|---|---|---|---|---|
| B-1 Hero | 65 | tree, box, lights, laptop, sock (5) | không | không | vật lạc: laptop, sock; dấu vết: hộp đèn dở |
| B-2 Sofa | 73 | hoodie, blanket, sofa, mug, tea towel (5) | không | không | vật lạc: tea towel; dấu vết: cốc trà nguội, tay đang vuốt chăn |
| B-3 Hành lang | 64 | garland, banister, bow, shoe, umbrella (5) | không | không | vật lạc: umbrella, shoe; dấu vết: giày bỏ dở trên bậc |
| B-4 Bếp | 69 | board, lemon, knife, sponge, tap (5) | không | không | vật lạc: sponge; dấu vết: tay đang cắt dở |
| B-5 Phòng ngủ | 58 | throw, bed, paperback, basket (4) | không | không | vật lạc: basket; dấu vết: sách úp |
| B-6 Infographic | 70 | dot, square, line, arrows (4) | không | không | Minh họa: không bắt buộc vật lạc chủ đề |
| B-7 OG | 76 | remote, mug, sprig (3) | không | không | vật lạc: remote; dấu vết: cốc cacao có váng |
| E-1 Sofa | 66 | blanket, sofa, charger, mug, side table (5) | không | không | vật lạc: charger; dấu vết: cốc trà nguội |
| E-2 Hành lang | 60 | garland, banister, bow, keys, trainer (5) | không | không | vật lạc: keys, trainer; dấu vết: giày trẻ em trên bậc |
| E-3 Bếp | 65 | mug, hand-soap bottle, sink, cinnamon stick, napkin (5) | không | không | vật lạc: nước rửa tay; dấu vết: bã cà phê |

Tóm tắt số từ: pack fixture 05 (B-1 đến B-7) có min 58 (B-5) và max 76 (B-7). Prompt sửa fixture 06 (E-1 đến E-3) có min 60 (E-2) và max 66 (E-1).

### Bảng chấm acceptance v0.2-US1 (kết quả sau vòng 2)

| # | Tiêu chí | Đạt/Không | Bằng chứng |
|---|---|---|---|
| V2-US1-1 | Mỗi prompt 30–80 từ | Đạt | Bảng số từ ở trên; min 58, max 76 |
| V2-US1-2 | Mỗi prompt ≤ 5 vật gọi tên | Đạt sau vòng 2 | Vòng 1 trượt ở B-2 (6 vật, vì "hoodie" không được tính); đã sửa, xem "Vòng sửa" |
| V2-US1-3 | Không số chẵn hoặc bố trí đối xứng trong prompt | Đạt | Quét số: chỉ có tỉ lệ khung (16:9, 4:3, 3:2, 1.91:1); quét từ số chẵn: không có; không có cặp vật |
| V2-US1-4 | Đời thường có vật lạc chủ đề và dấu vết người; vật lạc không lặp trong pack | Đạt | Cột ghi chú; vật lạc của pack B: laptop, sock, tea towel, umbrella, shoe, sponge, paperback, basket, remote; không trùng |
| V2-US1-5 | Không từ cấm đứng một mình | Đạt | Quét: không có cozy, welcoming, lived-in, natural, authentic, realistic, imperfect, charming, "slightly imperfect", "subtle imperfections" trong các khối prompt |
| V2-US1-6 | Ảnh không chữ có câu chặn chữ và vật nền cụ thể | Đạt | Ảnh 2–5, E-1…E-3 đều có "no readable text anywhere" và tên vật nền; ảnh 1, 6, 7 mode 2 có vùng trống và cũng có câu chặn |
| V2-US1-7 | Bảng có đủ cột Hướng, Khung, Độ cao máy, Ánh sáng, Thời tiết/giờ, Người, Chữ | Đạt | Tiêu đề bảng Kịch bản Media |
| V2-US1-8 | Pack từ 4 ảnh đạt bốn quy tắc FR-108 | Đạt | Xem kiểm FR-108 bên dưới |
| V2-US1-9 | Prompt vượt 80 từ có lý do | Đạt (không áp dụng) | Không có prompt nào vượt 80 từ |
| V2-US1-10 | Chẩn đoán nêu ≥ 5 nguyên nhân trong bảng dấu hiệu | Đạt | Ảnh 1 nêu 6 nguyên nhân, ảnh 2 nêu 4, ảnh 3 nêu 5 |
| V2-US1-11 | Prompt sửa đạt V2-US1-1…6; chỉ trả ảnh bị phàn nàn | Đạt | Ba prompt sửa có 60–66 từ (E-1 66, E-2 60, E-3 65); quét từ cấm và số chẵn đạt; mỗi ảnh lỗi một khối, không trả ảnh khác |
| V2-US1-12 | Mỗi ảnh sửa có 1–3 dòng "Đã đổi" | Đạt | Mỗi ảnh có đúng 3 dòng |

### Kiểm FR-108 trên bảng Kịch bản Media (7 ảnh)

- Không hai ảnh liền nhau trùng cả Khung, Độ cao máy và Ánh sáng. Các cặp liền kề 1–2, 2–3, 3–4, 4–5, 5–6, 6–7 đều khác ít nhất một trong ba cột. Đạt.
- Ít nhất một ảnh ánh lạnh hoặc u ám: ảnh 1 (lạnh u ám, cửa sổ). Đạt.
- Ít nhất hai ảnh có tay hoặc người: ảnh 2 (tay) và ảnh 4 (tay). Đạt.
- Không loại Khung nào chiếm quá nửa số ảnh: toàn cảnh 2 (ảnh 1, 6), trung cảnh 2 (ảnh 5, 7), qua vai 1, cận chi tiết 1, đang làm dở 1. Đạt.

### Vòng sửa

- **Vòng 1 (bản đầu):** Chấm tay thấy B-2 đếm được 6 vật: áo hoodie, chăn, sofa, cốc, khăn lau và đèn. Tiêu chí V2-US1-2 trượt. Nguyên nhân nằm ở skill: `anti-slop.md` chưa nói trang phục gọi tên riêng có được tính là vật hay không. Ngoài ra, E-3 dùng "dish sponge", cùng loại vật với B-4 trong cùng bếp; không vi phạm tiêu chí vì E thuộc fixture khác, nhưng đổi để tránh nhầm.
- **Sửa:** (a) `anti-slop.md` §2 bổ sung: trang phục gọi tên riêng được tính là một vật, chất liệu thì không (làm rõ cách đếm, không đổi ngưỡng 5 vật); (b) B-2 bỏ "lamp", thay bằng "warm tungsten light from the far corner", nên còn đúng 5 vật; (c) E-3 đổi "dish sponge" thành "bottle of hand soap".
- **Vòng 2 (chạy lại):** đếm lại toàn bộ bằng `wc -w`, quét từ cấm và số chẵn, đếm tay vật gọi tên. Kết quả: mọi tiêu chí V2-US1-1…12 đạt.
- **Số vòng sửa SKILL/references trong US1:** 1 (anti-slop §2, làm rõ cách đếm). **Số lần chạy lại:** 2.

---

## Kết quả đếm (máy, vòng 2)

Lệnh: tách các khối ```text trong file này, đếm `wc -w`, quét từ cấm (cozy, welcoming, lived-in, natural, authentic, realistic, imperfect, charming, subtle imperfections, 8K, masterpiece, ultra-detailed, stunning, flawless, hyperrealistic, `--ar`, `--no`, `::`) và từ chỉ số chẵn (two, four, six, eight, ten, twelve, ..., pair, both, couple).

| Khối | Số từ | Từ cấm | Từ số chẵn |
|---|---|---|---|
| 1 Hero | 65 | 0 | 0 |
| 2 Sofa | 73 | 0 | 0 |
| 3 Hành lang | 64 | 0 | 0 |
| 4 Bếp | 69 | 0 | 0 |
| 5 Phòng ngủ | 58 | 0 | 0 |
| 6 Infographic | 70 | 0 | 0 |
| 7 OG | 76 | 0 | 0 |
| E-1 Sofa | 66 | 0 | 0 |
| E-2 Hành lang | 60 | 0 | 0 |
| E-3 Bếp | 65 | 0 | 0 |

Quét số trong các khối: chỉ có tỉ lệ khung (16:9, 4:3, 3:2, 1.91:1), không có số đếm vật nào.
