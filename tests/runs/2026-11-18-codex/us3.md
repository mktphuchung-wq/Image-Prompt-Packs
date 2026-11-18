# Chạy khô US3: sửa prompt khi ảnh ra chưa đạt

- Ngày chạy: 2026-11-18
- Loại chạy: **chạy khô**. Worker tự đóng vai model, làm theo `SKILL.md` (mục Sửa prompt, đã có dòng tự kiểm mới) và `references/anti-slop.md` (bảng dấu hiệu, checklist QC), có đọc thêm `example-pack.md` Ví dụ B. Không gọi model ngoài, không tạo ảnh.
- Giới hạn: không có ảnh kết quả thật để xem, nên chẩn đoán dựa trên mô tả lỗi của người dùng (đúng theo SKILL khi harness không xem được ảnh). SC-004 cần ảnh thật, không kiểm ở đây.
- Số vòng sửa SKILL/references: **1** (dùng chung với us1.md).

## Vòng 1: bản nháp trước khi sửa

Bản nháp đầu của prompt sửa có 85 từ, vượt ngưỡng 80 của `anti-slop.md` mục 2, và không ghi tỉ lệ khung. Đã sửa: rút còn 78 từ, thêm "horizontal 4:3 frame".

## Fixture 04: prompt ba ảnh và lời phàn nàn về ảnh 2

Input: `tests/fixtures/04-failed-image-feedback.md`. Lời người dùng: "Ảnh 2 ra tay cầm cốc bị dính ngón, chữ trên cốc méo, ánh sáng như studio dù cảnh là trong bếp nhà. Sửa giúp ảnh 2 thôi, ảnh 1 và 3 ổn rồi."

### Đầu ra (vòng 2)

**Chẩn đoán:**
- "Tay cầm cốc bị dính ngón" đến từ câu "Her fingers stiff and pressed flat against the mug". Mô tả tay cứng, ép phẳng khiến model dựng ngón dính vào vật: dấu hiệu tay cầm vật sai.
- "Chữ trên cốc méo" đến từ câu "with the word "MORNING" printed on it" trên một vật cong, không nêu số lần xuất hiện: dấu hiệu chữ méo.
- "Ánh sáng như studio" đến từ câu "Soft studio-style light from above, even and flattering" trong khi cảnh là bếp nhà: dấu hiệu ánh sáng studio sai bối cảnh.
- Phần "Visible skin texture" và bối cảnh bếp đã ổn, giữ nguyên.

```text
Photo of a woman in her 20s in a bright home kitchen, one hand curled around the handle of a white ceramic mug with the thumb on the rim, the other hand cupping the base. Plain white mug, no text. Morning daylight from a window on the left, a folded dish towel and a bottle of oil on the countertop. Visible skin texture. Shot on a recent smartphone, eye level, horizontal 4:3 frame. Unposed, not retouched, not cinematic.
```

**Đã đổi:**
- Thay "fingers stiff and pressed flat" bằng cách cầm cụ thể: một tay quấn quanh quai, ngón cái tựa trên miệng cốc, tay kia đỡ đáy cốc. Hết tay cầm vật sai.
- Bỏ chữ "MORNING" trên cốc, dùng cốc trơn "no text". Hết chữ méo.
- Thay "studio-style light from above" bằng nắng sớm từ cửa sổ bên trái. Thêm "horizontal 4:3 frame" vì prompt cũ không ghi tỉ lệ. Hết ánh sáng studio.

Kiểm nhanh: 78 từ; một cụm camera ("recent smartphone"); một khuyết điểm ("visible skin texture" là chi tiết thực, không tính); hai vật đời thường (khăn lau, chai dầu); nguồn sáng là cửa sổ bên trái; tỉ lệ 4:3 viết bằng lời.

### Chấm US3

| # | Tiêu chí | Kết quả | Bằng chứng |
|---|---|---|---|
| US3-1 | Chẩn đoán trỏ đúng ba lỗi: tay cầm vật sai, chữ méo, ánh sáng studio sai bối cảnh | Đạt | Ba gạch đầu dòng đầu tiên, mỗi dòng trỏ đúng một câu trong prompt cũ |
| US3-2 | Chỉ trả prompt ảnh 2; ảnh 1 và 3 không xuất hiện lại | Đạt | Chỉ có một khối prompt, không có khối ảnh 1 hay ảnh 3 |
| US3-3 | Prompt đã sửa mô tả cách cầm cốc cụ thể | Đạt | Một tay quấn quai, ngón cái trên miệng cốc, tay kia đỡ đáy |
| US3-4 | Chữ trên cốc trong ngoặc kép kèm "appears once", hoặc bỏ hẳn chữ | Đạt | Bỏ hẳn chữ: "Plain white mug, no text" |
| US3-5 | Nguồn sáng thật, hợp bối cảnh bếp nhà; không có đèn studio | Đạt | Nắng sớm từ cửa sổ bên trái |
| US3-6 | Có 1–3 dòng "Đã đổi" nêu thay đổi và lỗi nhắm tới | Đạt | Ba dòng, mỗi dòng gắn với một lỗi |
| US3-7 | Tỉ lệ thành công sau tối đa một lần sửa (SC-004) | Chưa kiểm | Cần ảnh kết quả thật từ prompt đã sửa; không kiểm được bằng chạy khô |

## Kết quả US3

- Đạt: 6 trên 7 tiêu chí (US3-1 đến US3-6).
- Chưa kiểm: 1 (US3-7, SC-004, cần ảnh thật).
- Trượt: 0.
- Số vòng sửa SKILL/references: 1 (dùng chung với us1.md).
