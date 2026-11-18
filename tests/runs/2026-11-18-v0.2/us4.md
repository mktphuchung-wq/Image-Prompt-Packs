# Chạy thử khô US4 (v0.2): mockup có xác nhận

**Phạm vi:** B (fixture 05, giữ mặc định), D (fixture 05, chọn "có" ở mục 3), fixture 01 (bài có nhắc một mẫu hoodie của shop, không có chỗ chờ ảnh), fixture 03 (log không nhắc sản phẩm). Chuẩn: `tests/acceptance.md` mục "v0.2 — US4".

**Cách chạy:** worker đóng vai model, đọc `SKILL.md` (mục Tiêu chí, Cách hỏi, Ranh giới đã cập nhật US4) và `references/anti-slop.md` mục 5, rồi làm theo. Số từ đếm bằng `wc -w`; từ cấm và số chẵn quét bằng `grep`.

**Giới hạn:** chạy khô, cùng một worker viết skill và chấm. Chưa có ảnh sản phẩm thật, nên "Reference ảnh sản phẩm thật" chỉ được ghi là yêu cầu bắt buộc trong pack, không được kiểm bằng ảnh. Hành vi hỏi ở mục 3 của Chốt nhanh trên harness thật cần người chạy.

---

## B: fixture 05, giữ mặc định (không mockup)

Pack của B là pack trong `us1.md` (7 prompt). Kiểm:
- Không có prompt mockup: 7 khối prompt đều là ảnh bối cảnh, hero, minh họa, infographic hoặc ảnh chia sẻ; không có khối nào tạo sản phẩm hay thiết kế.
- Không có mục "Bonus", "Product-locked" hay tiêu đề sản phẩm ở Prompt Pack (kiểm `grep` trên `us1.md`: chỉ xuất hiện trong dòng Giả định, nơi nêu rõ là không có).
- Mục 3 của Chốt nhanh đã được trả lời mặc định "không" nên pack không có mục sản phẩm.

Đạt V2-US4-1.

---

## D: fixture 05, mục 3 chọn "có" (2 chỗ: sofa và phòng ngủ)

Người dùng chọn "có" ở mục 3. Pack thêm hai ảnh mockup (ảnh 8: sofa; ảnh 9: phòng ngủ). Mỗi ảnh có Reference bắt buộc là ảnh chăn thật của shop, nhãn "chờ sản phẩm xác minh"; prompt chỉ tạo bối cảnh, người và ánh sáng, để trống vùng thiết kế.

**Hai dòng thêm vào bảng Kịch bản Media:**

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | Mockup sofa | Mục Cozy Up the Sofa (chỗ chờ 1) | Chăn trên sofa, bối cảnh thật | mockup | 4:5 | Biên tập | trung cảnh | thấp | ấm tungsten, đèn bàn | tối | tay | 0 không chữ |
| 9 | Mockup phòng ngủ | Mục Cozy Christmas Bedroom (chỗ chờ 2) | Chăn trên giường, bối cảnh thật | mockup | 4:5 | Đời thường | toàn cảnh | thấp | ấm tungsten, đèn ngủ | tối | không | 0 không chữ |

Kiểm FR-108 với pack 9 ảnh: cặp liền kề 7–8 (trung cảnh, đứng nhìn xuống, ấm tungsten | trung cảnh, thấp, ấm tungsten) khác ở Độ cao máy; 8–9 (trung cảnh, thấp, ấm tungsten | toàn cảnh, thấp, ấm tungsten) khác ở Khung. Ánh lạnh u ám có ở ảnh 1 (không đổi); người hoặc tay có ở ảnh 2, 4, 8 (≥2); Khung cao nhất là toàn cảnh, 3 trên 9 ảnh (không quá nửa). Đạt.

### Ảnh 8 — Mockup sofa (chờ sản phẩm xác minh)
```text
Lifestyle photo of a living room sofa in late afternoon light: a folded blanket in a plain cream tone drapes over one arm, with an empty flat area in the centre of the fabric for the real product to be composited later. A hand smooths the blanket. Warm desk lamp light from the left, soft shadows across the cushions. Shot on a recent smartphone at eye level, unposed, not retouched. No readable text anywhere.
```
**Reference:** ảnh chăn thật của shop (ảnh sản phẩm thật, không do AI tạo). Bắt buộc.
**Ghi chú:** nhãn "chờ sản phẩm xác minh". Ghép thiết kế thật sau khi tạo; giữ nguyên metadata AI (C2PA, IPTC) khi xuất file, không xóa khi nén hay đăng.

### Ảnh 9 — Mockup phòng ngủ (chờ sản phẩm xác minh)
```text
Medium shot of a small bedroom at night: a folded blanket in a plain cream tone lies across the foot of the bed, with an empty flat area on the fabric for the real product to be composited later. A paperback lies face-down beside a bedside lamp. Warm tungsten light, low and amber. Shot at a low angle on a recent smartphone, unposed, not retouched. No readable text anywhere.
```
**Reference:** ảnh chăn thật của shop (ảnh sản phẩm thật, không do AI tạo). Bắt buộc.
**Ghi chú:** nhãn "chờ sản phẩm xác minh". Ghép thiết kế thật sau khi tạo; giữ nguyên metadata AI (C2PA, IPTC).

**Kiểm D:** có đúng hai prompt mockup, mỗi chỗ một prompt; mỗi prompt có Reference ảnh sản phẩm thật, nhãn "chờ sản phẩm xác minh", ghi chú ghép thiết kế và giữ metadata AI; prompt chỉ tạo bối cảnh, người và ánh sáng, không vẽ lại thiết kế hay logo (vùng thiết kế để trống). Đạt V2-US4-2.

---

## Fixture 01: bài có nhắc một mẫu hoodie, không có chỗ chờ

Bài là blog tiếng Việt khoảng 1.500 từ về cách chọn áo hoodie cotton. Bài nhắc một mẫu của "Nhà May Lá Xanh" và không yêu cầu ảnh hay mockup. Bài dài nên khối Chốt nhanh dừng chờ.

## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Hướng hình: Đời thường (mặc định — bài hướng dẫn mua hàng, người đọc cần thấy chất vải và cảm giác mặc thật) · Biên tập: ảnh chỉn chu cho hero · Minh họa: sơ đồ chất liệu
2. Chữ trong ảnh: hero và ảnh chia sẻ chừa vùng để chèn tiêu đề sau bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề · Không chữ. Các ảnh khác: không chữ.
3. Sản phẩm: bài nhắc một mẫu hoodie của Nhà May Lá Xanh nhưng không có chỗ chờ ảnh. Làm mockup mẫu đó không? Mặc định: không.
4. Số ảnh: 5 ảnh; hero 16:9, ảnh chia sẻ 1.91:1. Giữ nguyên?

Kiểm: mục 3 có mặt vì intake nhắc sản phẩm; mặc định "không". Đạt V2-US4-3.

---

## Fixture 03: log không nhắc sản phẩm để chụp

Log có ba chủ đề; media được yêu cầu là phần bài "5 thói quen buổi sáng cho người làm việc tại nhà" (khoảng 1.300 từ). Tác giả nói rõ: "Đừng vẽ logo hay sản phẩm nào vào ảnh, bài này không bán gì cả." Skill áp dụng quy tắc "log nhiều chủ đề: nói rõ đã chọn phần nào", và nêu phần đã chọn trong Kịch bản Media. Bài dài và dự kiến 4 ảnh nên dừng chờ.

## Chốt nhanh (trả lời "ok" để dùng mặc định)
Đã chọn phần: bài "5 thói quen buổi sáng cho người làm việc tại nhà" (bỏ phần sửa plugin cache và lịch đăng tuần sau).
1. Hướng hình: Đời thường (mặc định — bài về thói quen sinh hoạt, người đọc cần thấy buổi sáng thật bên cửa sổ và bàn làm việc) · Biên tập: ảnh chỉn chu kiểu tạp chí · Minh họa: tranh giấy cắt cho năm thói quen
2. Chữ trong ảnh: ảnh bìa và ảnh chia sẻ chừa vùng để chèn tiêu đề sau bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề "5 thói quen buổi sáng cho người làm việc tại nhà" · Không chữ. Các ảnh khác: không chữ.
3. Số ảnh: 4 ảnh (bìa, thói quen dậy sớm, uống nước hoặc viết việc, chia sẻ mạng xã hội); bìa 16:9, chia sẻ 1.91:1. Giữ nguyên?

Kiểm: không có mục 3 sản phẩm, vì tác giả nói không bán gì và không cần mockup. Mục đã rõ (chữ, số ảnh) vẫn được hỏi vì người dùng chưa chọn; kết quả là 3 mục, không có mục sản phẩm. Đạt V2-US4-4.

---

## Rà skill (V2-US4-5)

Kiểm `grep` trên `SKILL.md`:
- Câu cũ "Mockup sản phẩm chỉ khi người dùng yêu cầu đúng vị trí đó" không còn ở mục Ranh giới; mục đã thay bằng điều kiện mới (Chốt nhanh mục 3, mặc định không, Reference bắt buộc khi chọn có) và trỏ `references/anti-slop.md` mục 5.
- Mục Tiêu chí: "Không tự thêm ảnh mockup sản phẩm. Mockup chỉ lập khi người dùng chọn "có" ở mục 3 của Chốt nhanh hoặc tự yêu cầu đúng vị trí đó (FR-020, FR-126…FR-128)."

Đạt V2-US4-5 (kiểm bằng `grep` ở bước đếm bên dưới).

---

## Chấm máy

| Khối | Số từ | Từ cấm | Số chẵn | Vật gọi tên |
|---|---|---|---|---|
| Ảnh 8 (mockup sofa, Biên tập) | 74 | 0 | 0 | blanket, sofa, lamp, cushions (4) |
| Ảnh 9 (mockup phòng ngủ, Đời thường) | 69 | 0 | 0 | blanket, bed, paperback, lamp (4) |

Số từ đếm bằng `wc -w` trên các khối code của file này; cả hai khối nằm trong 30–80 từ.

Ghi chú về vật lạc chủ đề: ảnh 9 có hướng Đời thường nên phải có một vật lạc chủ đề và một dấu vết người; đó là cuốn sách úp (vật lạc, dấu vết người). Ảnh 8 có hướng Biên tập nên không bắt buộc vật lạc chủ đề (FR-116).

**Vòng sửa US4:** vòng 1 không có tiêu chí trượt. Số vòng sửa skill/references: 0.
