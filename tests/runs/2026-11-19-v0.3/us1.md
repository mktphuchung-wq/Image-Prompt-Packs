# Chạy thử khô US1 — vùng chữ trong prompt (v0.3.0)

**Cách chạy:** worker tự đóng vai model, đọc `SKILL.md` và các file `references/` ở trạng thái sau khi sửa vòng 1 (xem `us4.md`, mục Vòng sửa). Đây là chạy thử khô do cùng một tác giả đóng vai model, chưa phải bằng chứng độc lập; xem `docs/verification.md`.

**Phạm vi:** kịch bản I (fixture `05-christmas-article.md`, trả lời "ok" sau H) và K (fixture `07-crowded-hero-request.md`, trả lời "ok" sau Chốt nhanh).

**Số từ prompt chế độ 2 (đếm bằng PowerShell):** I-hero 74 · I-ảnh 5 (chia sẻ) 76 · K-hero 76. Prompt chế độ 0 của I: ảnh 2 là 65, ảnh 3 là 66, ảnh 4 là 69.

---

## Kịch bản I — pack sau "ok" (fixture 05)

Kịch bản Media và bảng: xem `us4.md` (H). Các prompt và khối Vùng chữ dưới đây là đầu ra của I.

### Ảnh 1 — Hero (chế độ 2, cách a) · 74 từ
```text
Photo of a living room in December, horizontal 16:9 frame. A Christmas tree with bare gaps stands on the right third, its ornaments in a box beside it. A phone charger lies coiled on the floor beside a half-drunk mug. The left third is a plain mid-grey wall, nothing in that area. Low winter light from the window, shot on a recent smartphone, eye level. Unposed, not retouched, not cinematic. No readable text anywhere.
```
**Vùng chữ:** 1/3 trái, khoảng 40% khung · cách tạo: tường xám trung bình có thật (a) · nền tối trung bình → chữ trắng hoặc kem · lề an toàn ~5% · tiêu đề 1 dòng · cắt sang 1.91:1 vẫn còn nguyên; khung 2:3 dùng prompt dọc riêng.
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.

### Ảnh 2 — Minh họa phòng khách (chế độ 0) · 65 từ
```text
Photo of a small living room corner at dusk, horizontal 4:3 frame. A tabletop tree with a few glass ornaments sits on a low cabinet, a crumpled scarf draped over the cabinet's edge. Warm lamp light from the left, shot on a recent smartphone, eye level, slightly off-center. Sharp focus throughout, not retouched, not cinematic. Plain unlabeled boxes on the floor, no readable text anywhere.
```

### Ảnh 3 — Lối vào (chế độ 0) · 66 từ
```text
Photo of a front door entryway in the morning, horizontal 3:2 frame. A hand hangs an evergreen wreath with a red ribbon on the door, the wreath slightly crooked. A key ring and a crumpled paper bag lie on the step beside the door. Grey daylight from the open doorway, shot on a recent smartphone, eye level. Candid, not retouched, not cinematic. No readable text anywhere.
```

### Ảnh 4 — Phòng ngủ, chăn Giáng sinh (chế độ 0) · 69 từ
```text
Photo of a bedroom at first light, horizontal 3:2 frame. A plaid blanket in red and green is folded across the foot of an unmade bed, one corner slipping onto the floor. A glass of water sits on the bedside table beside a knitted hat. Pale window light from the left, shot on a recent smartphone, eye level, slightly off-center. Unposed, not retouched, not cinematic. No readable text anywhere.
```

### Ảnh 5 — Ảnh chia sẻ 1.91:1 (chế độ 2, cách a) · 76 từ
```text
Photo of a fireplace mantel in December, horizontal 1.91:1 frame. A green garland with a few ornaments drapes across the right side, with a half-written card leaning against the candles and a tape measure beside them. The left third is a plain cream wall, nothing in that area. Warm lamp light from the right, shot on a recent smartphone, eye level, subject kept away from the edges. Unposed, not retouched, not cinematic. No readable text anywhere.
```
**Vùng chữ:** 1/3 trái, khoảng 35% khung · cách tạo: tường kem nhạt có thật (a) · nền sáng dịu → chữ gần đen · lề an toàn ~5% · tiêu đề 1 dòng · cắt sang 16:9 vẫn còn nguyên; khung 2:3 dùng prompt dọc riêng.
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.

---

## Kịch bản K — fixture 07 (cảnh chợ đông)

**Lượt 1 (dừng):** trường hợp (1) Chữ kích hoạt. Mục Banner chỉ giữ hai điểm chưa chốt: tiêu đề và vùng chữ. Điểm b (chèn chữ sau) và điểm d (khung 16:9) đã có trong intake nên bỏ.

```markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Banner (lý do: hero chưa có tiêu đề chốt và cảnh chợ đông chưa có chỗ đặt chữ rõ; thấy ở ảnh hero, bài chỉ cần một ảnh)
   a. Tiêu đề: "Buổi sáng ở chợ Bến Thành", 1–2 dòng (mặc định) · tiêu đề khác, gửi vào đây
   c. Vùng chữ: làm mềm hậu cảnh bên trái, vì cảnh chợ không có tường hay sàn trơn (mặc định — cảnh đông) · đổi góc máy để có tường trơn bên trái

## Kịch bản Media
| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | Cảnh chợ đông buổi sáng, mở bài | hero | 16:9 | Đời thường | toàn cảnh | ngang tầm mắt | nắng sớm từ mái chợ | sáng sớm | người bán | 2 chèn chữ sau — 1/3 trái (theo mục c) |

Sửa format theo số dòng, ví dụ "ảnh 3 đổi 4:5, bỏ ảnh 5", hoặc trả "ok".
```

**Lượt 2 ("ok"): pack.** Tiêu đề mặc định rút gọn còn 5 từ ("Buổi sáng ở chợ Bến Thành") để đúng quy tắc tối đa 6 từ.

### Ảnh 1 — Hero (chế độ 2, cách b) · 76 từ
```text
Photo of a morning market stall at a crowded covered market in Saigon, horizontal 16:9 frame. A vendor weighs mango on a brass scale on the right third, sharp, with mango crates in front also sharp. The left third is a softly blurred background of stacked crates and hanging bags, medium-dark and low in detail, shapes still recognisable. Overcast daylight from the open side. Candid, slightly off-center. Unposed, not retouched, not cinematic. No readable text anywhere.
```
**Vùng chữ:** 1/3 trái, khoảng 40% khung · cách tạo: hậu cảnh làm mềm nhẹ (b), chủ thể và tiền cảnh nét · nền tối trung bình → chữ trắng hoặc kem; hậu cảnh rối thì thêm dải màu đặc sau chữ · lề an toàn ~5% · tiêu đề 1–2 dòng · cắt sang 1.91:1 vẫn còn nguyên; khung 2:3 dùng prompt dọc riêng.
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.

---

## Bảng chấm US1 (tiêu chí `tests/acceptance.md`, mục v0.3 — US1)

| # | Kịch bản | Kết quả | Bằng chứng |
|---|---|---|---|
| V3-US1-1 | I | Đạt | Hero: chủ thể "on the right third", vùng chữ "The left third" |
| V3-US1-2 | I | Đạt | Mỗi prompt chế độ 2 có đúng một cách: (a) "nothing in that area" (hero, ảnh 5); (b) chỉ ở K |
| V3-US1-3 | I | Đạt | Tông "mid-grey" (tối trung bình) và "cream" (sáng dịu); "plain", "nothing in that area" |
| V3-US1-4 | I | Đạt | Câu "No readable text anywhere." có ở hero và ảnh 5 |
| V3-US1-5 | I | Đạt | Hero 74 từ, ảnh 5 76 từ; vật gọi tên: hero 5 (cây, ornaments, hộp, sạc, cốc), ảnh 5 5 (dải hoa, ornaments, thiệp, nến, thước dây); không số chẵn; không từ cấm |
| V3-US1-6 | I, K | Đạt | Không "bokeh", không thông số máy ảnh, không buzzword; "16:9" và "1.91:1" chỉ là tỉ lệ khung |
| V3-US1-7 | K | Đạt | Chọn cách (b): "subject and foreground sharp", hậu cảnh bên trái "softly blurred ... shapes still recognisable"; khối ghi rõ (b) |
| V3-US1-8 | I, K | Đạt | Ảnh 2–4 (chế độ 0) có "sharp focus throughout" hoặc nét toàn cảnh, không làm mềm; làm mềm ở K chỉ nằm trong vùng chữ |
| V3-US1-9 | Rà `text-in-image.md` | Đạt | Ví dụ (c) khung 2:3 có vùng chữ dải trên; ví dụ (b) là cảnh chợ đông |
| V3-US1-10 | Rà `text-in-image.md` | Đạt | Ba ví dụ chế độ 2: 64, 77, 67 từ; không có "bokeh" hay "f/" trong khối prompt; ví dụ chế độ 3 cùng cảnh với (a) |
| V3-US1-11 | I, K | Cần người chạy | SC-202 đo trên ảnh thật (5 ảnh), không đo được bằng chạy khô |

**Tổng US1:** 10/10 tiêu chí chạy khô đạt (không có vòng sửa cho US1); 1 mục cần người chạy.

**Ghi chú:** tiêu đề mặc định đầu tiên của K viết "Một buổi sáng ở chợ Bến Thành" (7 từ), vượt quy tắc 6 từ; đây là lỗi của người chạy khi soạn, đã sửa ngay trong lượt chạy xuống 5 từ, không phải lỗi tài liệu.
