# Chạy thử khô US2 (v0.2): Chốt nhanh

**Phạm vi:** kịch bản A (fixture `05-christmas-article.md`, dừng chờ), B ("ok"), trả lời một phần ("hướng B, còn lại ok"), F (fixture `02-one-line-request.md`, xuất luôn), G (đổi hướng sau khi có pack), và biến thể "hỏi việc khác khi đang chờ". Chuẩn: `tests/acceptance.md` mục "v0.2 — US2".

**Cách chạy:** worker đóng vai model, đọc `SKILL.md` (đã có Chốt nhanh, 121 dòng) và `references/brief-card.md`, rồi làm theo. Số từ đếm bằng `wc -w`; từ cấm và số chẵn quét bằng `grep`.

**Giới hạn:** chạy khô, cùng một worker viết skill và chấm. Chưa chạy trên Claude Code, Codex hay ChatGPT, nên hành vi "dừng chờ" (SC-104) chưa được kiểm thật. Riêng trường hợp trả lời một phần, bảng Kịch bản Media và trạng thái mặc định được kiểm đầy đủ; các prompt Biên tập của fixture 05 được kiểm ở G (cùng quy tắc, cùng ràng buộc).

---

## A: fixture 05, dừng chờ

## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Hướng hình: Đời thường (mặc định — bài hướng dẫn trang trí trong nhà, người đọc cần thấy nhà thật) · Biên tập: ảnh chỉn chu kiểu tạp chí nhà cửa cho hero · Minh họa: tranh giấy cắt cho ảnh bố cục nhà
2. Chữ trong ảnh: hero và ảnh chia sẻ chừa vùng để chèn tiêu đề sau bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề "Indoor Christmas Decorations" · Không chữ. Các ảnh khác: không chữ.
3. Sản phẩm: bài có 2 chỗ chờ sản phẩm, chăn trên sofa (phòng khách) và chăn trên giường (phòng ngủ). Làm mockup ở hai chỗ đó không? Mặc định: không.
4. Số ảnh: 7 ảnh; hero 16:9, bốn ảnh minh họa trong bài 4:3, một infographic 4:3, ảnh chia sẻ 1.91:1. Giữ nguyên?

## Kịch bản Media
**Nội dung:** Bài hướng dẫn trang trí Giáng sinh trong nhà theo từng phòng, kèm bảng kích thước và an toàn.
**Mục tiêu:** Giúp người đọc trang trí nhà đủ đẹp mà không cần mua đồ mới. · **Đối tượng:** Người có nhà ở. · **Kênh:** Blog; chia sẻ mạng xã hội.
**Hướng hình ảnh:** Ảnh chụp điện thoại trong nhà; không dựng cảnh kiểu showroom.

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | Phòng khách trang trí dở dang | hero | 16:9 | Đời thường | toàn cảnh | ngang tầm mắt | lạnh u ám, cửa sổ | chiều đông u ám | không | 2 chèn chữ sau |
| 2 | Sofa | Mục Cozy Up the Sofa | Chăn caro trên sofa | minh họa | 4:3 | Đời thường | qua vai | thấp | ấm tungsten, đèn bàn | tối | tay | 0 không chữ |
| 3 | Hành lang | Mục Entryway & Staircase | Cầu thang có garland | minh họa | 4:3 | Đời thường | cận chi tiết | ngang tầm mắt | trung tính ban ngày | sáng mưa | không | 0 không chữ |
| 4 | Bếp | Mục Christmas Kitchen | Góc bếp đang làm dở | minh họa | 4:3 | Đời thường | đang làm dở | trên cao | huỳnh quang xanh nhạt | sáng sớm | tay | 0 không chữ |
| 5 | Phòng ngủ | Mục Cozy Christmas Bedroom | Giường có chăn caro, sách bỏ dở | minh họa | 3:2 | Đời thường | trung cảnh | thấp | ấm tungsten, đèn ngủ | tối | không | 0 không chữ |
| 6 | Infographic | Mục Sizing & Placement | Sơ đồ ba khu vực | infographic | 4:3 | Minh họa | toàn cảnh | đứng nhìn xuống | trung tính ban ngày | ban ngày | không | 2 chèn chữ sau |
| 7 | Ảnh chia sẻ | Ảnh đại diện khi chia sẻ | Cảnh sàn gỗ buổi tối | OG | 1.91:1 | Đời thường | trung cảnh | đứng nhìn xuống | ấm tungsten, đèn sàn | tối | không | 2 chèn chữ sau |

Lượt này dừng ở đây. Chưa có prompt nào.

**Kết quả chấm A:** khối Chốt nhanh đứng trên, có 4 mục (đủ 4, không thêm), mỗi mục có mặc định và tối đa 3 lựa chọn; mục 1 có hướng mặc định và một câu lý do; mục 3 nêu đúng 2 chỗ chờ (sofa, phòng ngủ) với mặc định "không"; không có tên preset, tên công cụ hay tham số kỹ thuật; không có khối prompt; dừng chờ. Đạt V2-US2-1…5.

---

## B: "ok" sau A

Trạng thái: "ok" cho mọi mục mặc định (hướng Đời thường, chữ hero/OG chèn sau, không mockup, 7 ảnh). Skill không hỏi thêm và xuất pack theo đúng các mặc định đã nêu. Pack thu được giống hệt đầu ra của kịch bản B trong `us1.md` (7 prompt, 58–76 từ, đã chấm ở US1). Khối Chốt nhanh không còn; mục Giả định ở cuối không xuất hiện. Đạt V2-US2-6.

---

## Trả lời một phần: "hướng B, còn lại ok"

"B" là lựa chọn thứ hai của mục 1: Biên tập. Mục 1 áp theo lựa chọn; mục 2, 3, 4 theo mặc định.

**Kịch bản Media (cập nhật):** cột Hướng đổi thành Biên tập cho các ảnh đời thường (1, 2, 3, 4, 5, 7). Infographic (6) giữ Minh họa vì là sơ đồ. Các cột khác (Khung, Độ cao máy, Ánh sáng, Thời tiết/giờ, Người, Chữ) không đổi, nên bảng vẫn đạt FR-108.

**Prompt Pack (mẫu một ảnh, Biên tập):**
```text
Editorial interior photo of a living room in late afternoon: a tall window on the left, a grey sofa draped with a red-and-green plaid throw, a wooden coffee table with a small greenery arrangement. Window light falls across the rug, soft and directional. Shot at eye level with a 35mm lens look, straight verticals, the room tidy and calm. Clean empty space across the top third for a headline added later; no readable text anywhere.
```

Ảnh 1 (hero) viết theo mẫu này. Sáu ảnh còn lại theo cùng quy tắc (ràng buộc giống G, kiểm ở G). Đạt V2-US2-7 ở mức bảng và trạng thái mặc định; prompt đầy đủ của Biên tập được kiểm ở G.

---

## F: fixture 02, xuất luôn

Đầu vào: "Cần 3 ảnh cho landing page bán áo hoodie unisex, đăng Facebook ads." Số ảnh do người dùng nêu (3), nên xuất luôn (1–3 ảnh). Intake nhắc sản phẩm (áo hoodie) nên mục sản phẩm có mặt trong khối mặc định, mặc định "không làm mockup". Hướng hình: landing bán hàng thời trang gợi ý Biên tập cho hero.

## Đã dùng mặc định
- Hướng hình: Biên tập cho ảnh hero, vì landing bán áo thời trang cần ảnh chỉn chu ở đầu trang; Đời thường cho ảnh quảng cáo và ảnh chi tiết, vì quảng cáo cần cảm giác dùng thật.
- Chữ: hero và ảnh quảng cáo chèn chữ sau bằng công cụ thiết kế; ảnh chi tiết không chữ.
- Sản phẩm: không làm mockup. Bài không có chỗ chờ sản phẩm, và mockup chỉ khi bạn yêu cầu. Áo trong ảnh là áo xám trơn chung, không phải thiết kế thật của shop.

## Kịch bản Media

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Hero landing | Đầu trang | Người mặc áo trong bối cảnh thành phố | hero | 16:9 | Biên tập | trung cảnh | ngang tầm mắt | ấm, nắng chiều nghiêng | chiều | một người | 2 chèn chữ sau |
| 2 | Ảnh quảng cáo | Giữa trang | Người thật trên bậc café, cảm giác dùng thật | lifestyle | 4:5 | Đời thường | trung cảnh | ngang tầm mắt | lạnh u ám, cửa sổ | chiều | một người | 2 chèn chữ sau |
| 3 | Ảnh chi tiết | Cuối trang | Tay kéo khóa áo, chất liệu | lifestyle | 1:1 | Đời thường | cận chi tiết | ngang tầm mắt | trung tính ban ngày, cửa sổ | sáng | tay | 0 không chữ |

## Prompt Pack

### Ảnh 1 — Hero landing
```text
Editorial fashion photo of a young man in a plain grey hoodie turning on a city pavement, late-afternoon sun low from the right and long soft shadows across the stones. Medium-length lens look, eye level, subject slightly off-center, fabric folds and skin texture visible. Clean empty space across the top third for a headline added later; no readable text anywhere. Nothing else in the frame competes with the outfit.
```
**Chữ:** vùng trống phía trên để chèn tiêu đề bằng công cụ thiết kế.

### Ảnh 2 — Ảnh quảng cáo
```text
Candid phone photo of a young woman in a grey hoodie sitting on a café step, mid-laugh, holding a paper cup of coffee in one hand. A tote bag with a folded umbrella rests beside her. Cool, even daylight from an overcast sky. Shot at eye level on a recent smartphone, vertical 4:5 frame, unposed, not retouched. Clean empty space in the upper third for a headline added later; no readable text anywhere.
```
**Chữ:** vùng trống phía trên để chèn tiêu đề bằng công cụ thiết kế.

### Ảnh 3 — Ảnh chi tiết
```text
Close-up phone photo of hands zipping a grey hoodie halfway up, a set of keys dangling from one finger, a folded tissue on the bench beside a sleeve. Daylight from a side window, uneven and soft. Shot from standing height, square 1:1 frame, unposed, not retouched. No readable text anywhere.
```

Không có mục Giả định ở cuối pack; mặc định đã dùng nằm ở đầu phản hồi (FR-114). Không có prompt mockup, không có mục Bonus (FR-127). Đạt V2-US2-8.

---

## G: đổi hướng sau khi có pack (blog Ví dụ A, lượt 2)

Đầu vào: pack Ví dụ A (lượt 2) đã có. Người dùng: "đổi sang hướng biên tập chuyên nghiệp".

**Ảnh bị ảnh hưởng:** ảnh 1 (hero) và ảnh 5 (ảnh chia sẻ) vì đang là Đời thường. Ảnh 2 (Minh họa tách khu) và ảnh 4 (Infographic) là Minh họa, giữ nguyên. Ảnh 3 đã là Biên tập, giữ nguyên.

### Ảnh 1 — Hero (viết lại)
```text
Editorial interior photo of a woman with her hair tied back, typing at a small wooden desk beside a tall window. Window light from the left falls across the desk and a linen armchair. A laptop, a stack of paper and one ceramic cup sit neatly on the desk. Shot at eye level, 35mm lens look, straight verticals, the room tidy and calm. Clean empty space across the top third for a headline added later; no readable text anywhere.
```

### Ảnh 5 — Ảnh chia sẻ (viết lại)
```text
Overhead editorial photo of a wooden desk with a ceramic cup of tea, an open notebook and a pencil laid neatly across the page, soft window light from the left, flat even shadows. Shot straight down, horizontal 1.91:1 frame with the subject kept away from the edges. Clean empty space on the left for a headline added later; no readable text anywhere.
```

**Đã đổi:** viết lại ảnh 1 và ảnh 5 theo hướng Biên tập; khung, độ cao máy, ánh sáng và người giữ nguyên trong bảng, nên FR-108 vẫn đạt. Ảnh 2, 3, 4 không viết lại (FR-115). Đạt V2-US2-9.

---

## Biến thể: hỏi việc khác khi đang chờ

Trạng thái: sau A (Chốt nhanh đang chờ), người dùng hỏi: "Bài này dài bao nhiêu từ?"

Phản hồi mô phỏng: trả lời câu hỏi (bài khoảng 2.889 từ), giữ khối Chốt nhanh đã đưa, và hỏi lại người dùng có chấp nhận các mục mặc định không. Không xuất prompt nào. Khi người dùng quay lại trả "ok", pack theo mặc định như B. Đạt V2-US2-10 (mức mô phỏng; hành vi thật cần kiểm trên harness).

---

## Kết quả đếm máy (prompt mới của US2)

Đếm trên các khối ```text của kịch bản F, G và mẫu hướng Biên tập ở trả lời một phần.

| Khối | Số từ | Từ cấm | Số chẵn | Có câu chặn chữ (chế độ 0 hoặc 2) |
|---|---|---|---|---|
| Trả lời một phần, ảnh 1 (Biên tập) | 75 | 0 | 0 | có |
| F-1 Hero landing (Biên tập, chế độ 2) | 69 | 0 | 0 | có |
| F-2 Ảnh quảng cáo (Đời thường, chế độ 2) | 73 | 0 | 0 | có |
| F-3 Ảnh chi tiết (Đời thường, chế độ 0) | 50 | 0 | 0 | có |
| G-1 Hero (Biên tập, chế độ 2) | 79 | 0 | 0 | có |
| G-2 Ảnh chia sẻ (Biên tập, chế độ 2) | 62 | 0 | 0 | có |

Vật gọi tên (đếm tay): trả lời một phần ảnh 1: 4 (sofa, throw, coffee table, greenery); F-1: 1 (hoodie); F-2: 4 (hoodie, cup, tote bag, umbrella); F-3: 5 (hoodie, keys, tissue, bench, sleeve); G-1: 5 (desk, laptop, paper, cup, armchair); G-2: 3 (cup, notebook, pencil). Tất cả ≤ 5.

**Vòng sửa US2:** vòng 1 phát hiện F-1 và F-2 (chế độ 2) thiếu câu "no readable text anywhere", đối chiếu với `references/text-in-image.md`. Đã thêm câu này và đếm lại (F-1 69 từ, F-2 73 từ). Không cần sửa skill ở vòng này. Số vòng sửa SKILL/references trong US2: 0. Số lần chạy lại: 1.

**Ghi nhận giới hạn:** các trường hợp dừng chờ trên Claude Code, Codex và ChatGPT chưa chạy thật (SC-104 cần người chạy). Trả lời một phần và hỏi việc khác khi đang chờ chỉ kiểm ở mức mô phỏng.
