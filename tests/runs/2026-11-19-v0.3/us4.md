# Chạy thử khô US4 — lượt đầu theo trường hợp đặc biệt (v0.3.0)

**Cách chạy:** như `us1.md`. Kịch bản H, J, L, M của `specs/003-hero-copy-space/quickstart.md`.

---

## Kịch bản H — fixture 05 + "làm prompt ảnh cho bài này" (dừng)

Trường hợp kích hoạt: (1) Chữ (hero và ảnh chia sẻ có chỗ đặt chữ, cách đặt chữ chưa chốt); (3) Nội dung đặc biệt (hai chỗ chờ sản phẩm). Không có (2) Phong cách hay (4) Format mới lạ.

```markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Banner (lý do: hero và ảnh chia sẻ có chỗ đặt chữ, nhưng intake chưa chốt cách đặt chữ; thấy ở ảnh 1 và ảnh 5 trong bảng dưới)
   a. Tiêu đề: "Indoor Christmas Decorations", 1 dòng (mặc định) · "Indoor Christmas Decorations: Easy Room-by-Room Ideas", 2 dòng
   b. Cách đặt chữ: chừa vùng, ảnh cố ý không có chữ, tự thêm tiêu đề bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề · hai lượt
   c. Vùng chữ: 1/3 trái trên mảng tường xám trung bình (mặc định — cảnh có tường trơn) · làm mềm hậu cảnh bên trái
   d. Khung: hero 16:9 + ảnh chia sẻ 1.91:1 (mặc định) · thêm Pinterest 2:3
2. Sản phẩm (lý do: bài có hai chỗ chờ sản phẩm, chăn trên sofa ở mục phòng khách và chăn trên giường ở mục phòng ngủ; dòng [Product placement] trong bài)
   Làm mockup ở hai chỗ đó không? Mặc định: không · chỉ chỗ sofa · cả hai chỗ

## Kịch bản Media
| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | Phòng khách có cây thông, mở bài | hero | 16:9 | Đời thường | toàn cảnh | ngang tầm mắt | lạnh u ám, cửa sổ | chiều đông | không | 2 chèn chữ sau — 1/3 trái |
| 2 | Minh họa cây thông | Step 2 | Góc phòng với cây thông nhỏ | minh họa | 4:3 | Đời thường | trung cảnh | ngang tầm mắt | đèn vàng ấm | tối | không | 0 không chữ |
| 3 | Minh họa lối vào | Step 3 | Vòng hoa trên cửa chính | minh họa | 3:2 | Đời thường | cận chi tiết | ngang tầm mắt | xám từ cửa | sáng sớm | tay | 0 không chữ |
| 4 | Minh họa phòng ngủ | Step 5 | Giường có chăn kẻ đỏ xanh | minh họa | 3:2 | Đời thường | trung cảnh | ngang tầm mắt | sáng sớm từ cửa sổ | sáng sớm | không | 0 không chữ |
| 5 | Ảnh chia sẻ | Đầu bài (khi chia sẻ) | Lò sưởi và dải hoa, link preview | OG | 1.91:1 | Đời thường | trung cảnh | ngang tầm mắt | đèn vàng từ bên phải | tối | không | 2 chèn chữ sau — 1/3 trái |

Sửa format theo số dòng, ví dụ "ảnh 3 đổi 4:5, bỏ ảnh 5", hoặc trả "ok".
```

Không có khối prompt nào.

**Bản đầu (trước sửa vòng 1):** điểm b là "chèn chữ sau, tự thêm tiêu đề bằng công cụ thiết kế (mặc định) · …", thiếu "ảnh cố ý không có chữ" nên trượt FR-210 (V3-US2-4). Đã sửa, bản trên là bản chạy lại.

---

## Kịch bản J — H rồi "ảnh 3 đổi 4:5, bỏ ảnh 5, còn lại ok"

Hai thay đổi được áp; các dòng khác giữ nguyên.

| # | Ảnh | Thay đổi |
|---|---|---|
| 3 | Minh họa lối vào | Tỉ lệ 3:2 → 4:5 (đổi khung dọc, các cột khác giữ nguyên) |
| 5 | Ảnh chia sẻ | Bỏ dòng |

Pack sau "ok" có bốn ảnh: 1 (hero, 74 từ), 2 (65 từ), 3 (đổi thành khung dọc, 66 từ), 4 (69 từ). Ảnh 3 đổi thành:

```text
Photo of a front door entryway in the morning, vertical 4:5 frame. A hand hangs an evergreen wreath with a red ribbon on the door, the wreath slightly crooked. A key ring and a crumpled paper bag lie on the step beside the door. Grey daylight from the open doorway, shot on a recent smartphone, eye level. Candid, not retouched, not cinematic. No readable text anywhere.
```

Prompt ảnh 1, 2, 4 giữ nguyên như ở `us1.md`. Ảnh chia sẻ không còn trong pack.

---

## Kịch bản L — fixture 08 (carousel 5 slide) (dừng)

```markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Format mới lạ (lý do: carousel 5 slide không có trong bảng loại ảnh; thấy ở yêu cầu "carousel 5 slide")
   Năm ảnh 4:5 đời thường, mỗi ảnh một thói quen, không chữ (mặc định — gần nhất với ảnh minh họa trong bài) · một ảnh 4:5 đại diện cho cả bài · bỏ, không làm ảnh cho carousel

## Kịch bản Media
| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Slide 1 | Carousel | Uống nước trước khi mở máy | minh họa | 4:5 | Đời thường | cận chi tiết | ngang tầm mắt | sáng sớm cạnh cửa sổ | sáng sớm | tay | 0 không chữ |
| 2 | Slide 2 | Carousel | Ra ban công đón nắng | minh họa | 4:5 | Đời thường | toàn cảnh | ngang tầm mắt | nắng sớm | sáng sớm | không | 0 không chữ |
| 3 | Slide 3 | Carousel | Mặc đồ như sắp đi làm | minh họa | 4:5 | Đời thường | trung cảnh | ngang tầm mắt | đèn trần | sáng | người | 0 không chữ |
| 4 | Slide 4 | Carousel | Viết ba việc cần làm | minh họa | 4:5 | Đời thường | cận chi tiết | đứng nhìn xuống | ánh sáng bàn | sáng | tay | 0 không chữ |
| 5 | Slide 5 | Carousel | Tắt thông báo đến chín giờ | minh họa | 4:5 | Đời thường | trung cảnh | ngang tầm mắt | ánh tối buổi tối | tối | không | 0 không chữ |

Sửa format theo số dòng, ví dụ "ảnh 3 đổi 4:5, bỏ ảnh 5", hoặc trả "ok".
```

Không có khối prompt nào.

---

## Kịch bản M — fixture 09 (xuất luôn)

````markdown
## Đã dùng mặc định
- Vị trí và kênh: ba ảnh minh họa trong bài, đặt theo ba ý chính; kênh blog (intake không nêu kênh).
- Chữ: không chữ trong ảnh, có câu chặn chữ tự thêm (intake đã nêu).
- Sản phẩm: không có, không làm mockup (intake không nhắc sản phẩm).

## Kịch bản Media
| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Minh họa ý 1 | Đầu mục 1 | Dậy đúng giờ, mở rèm | minh họa | 3:2 | Đời thường | trung cảnh | ngang tầm mắt | sáng sớm từ cửa sổ | sáng sớm | tay | 0 không chữ |
| 2 | Minh họa ý 2 | Giữa mục 2 | Ly nước trước điện thoại | minh họa | 3:2 | Đời thường | cận chi tiết | ngang tầm mắt | ánh sáng cửa sổ | sáng | không | 0 không chữ |
| 3 | Minh họa ý 3 | Cuối mục 3 | Viết ba việc cần làm | minh họa | 3:2 | Đời thường | trung cảnh | ngang tầm mắt | ánh sáng cửa sổ lạnh | sáng | tay | 0 không chữ |

## Prompt Pack
Phong cách chung: ánh sáng cửa sổ thật, không dựng studio, không chữ. Số từ: ảnh 1 — 60; ảnh 2 — 55; ảnh 3 — 63.

### Ảnh 1 — Minh họa ý 1
```text
Photo of a bedroom at first light, horizontal 3:2 frame. A hand pulls a linen curtain open, and the morning light falls across an unmade bed. A charger cable and a sock lie on the floor. Pale window light from the left, shot on a recent smartphone, eye level, slightly off-center. Unposed, not retouched, not cinematic. No readable text anywhere.
```

### Ảnh 2 — Minh họa ý 2
```text
Photo of a kitchen counter in the morning, horizontal 3:2 frame. A glass of water sits half-drunk beside a phone lying face-up, its screen dark. A folded tea towel hangs over the counter's edge. Soft daylight from the window, shot on a recent smartphone, eye level. Candid, not retouched, not cinematic. No readable text anywhere.
```

### Ảnh 3 — Minh họa ý 3
```text
Photo of a wooden desk by a window in the morning, horizontal 3:2 frame. A hand holds a pen above a blank sheet of lined paper. A cold cup of coffee sits beside it. A dog's leash hangs over the chair. Cool window light from the left, shot on a recent smartphone, eye level. Unposed, not retouched, not cinematic. No readable text anywhere.
```
````

Không có mục Chốt nhanh; khối "Đã dùng mặc định" đứng đầu phản hồi.

---

## Bảng chấm US4 (tiêu chí `tests/acceptance.md`, mục v0.3 — US4)

| # | Kịch bản | Kết quả | Bằng chứng |
|---|---|---|---|
| V3-US4-1 | H | Đạt | Dừng; có Chốt nhanh và Kịch bản Media; không có khối prompt |
| V3-US4-2 | H | Đạt | Banner có a–d, mỗi điểm có mặc định; d có 16:9, 1.91:1 và Pinterest 2:3; không hỏi màu, kiểu chữ, CTA hay logo |
| V3-US4-3 | H | Đạt | Sản phẩm nêu đúng 2 chỗ chờ (sofa, giường phòng ngủ); mặc định "không" |
| V3-US4-4 | H | Đạt | Mỗi mục có lý do; không có mục Phong cách hay Format mới lạ |
| V3-US4-5 | H | Đạt | Cột Chữ ghi "2 chèn chữ sau — 1/3 trái"; có dòng sửa theo số dòng dưới bảng |
| V3-US4-6 | H, L, M | Đạt | Không dựa vào số ảnh hay độ dài; không có "800 từ" hay "từ 4 ảnh" làm lý do; không hỏi từng ảnh |
| V3-US4-7 | J | Đạt | Chỉ ảnh 3 đổi sang 4:5 và ảnh 5 bị bỏ; các dòng khác giữ nguyên |
| V3-US4-8 | L | Đạt | Dừng với mục Format mới lạ có lý do và mặc định; không có prompt |
| V3-US4-9 | M | Đạt | Không dừng; khối "Đã dùng mặc định" ở đầu nêu các mặc định |
| V3-US4-10 | H, L, M | Đạt (chạy khô) | Ba intake đều đúng: H và L dừng với lý do, M xuất luôn |
| V3-US4-11 | H, L | Đạt | H: 2 mục (Banner tính một), mỗi lựa chọn tối đa 3; L: 1 mục, tối đa 3 lựa chọn |
| V3-US4-12 | — | Cần người chạy | SC-207 đo khi dùng thật |

**Tổng US4:** 11/11 tiêu chí chạy khô đạt; 1 mục cần người chạy (SC-207). Vòng sửa của US4: 0 (V3-US2-4 được ghi ở `us2.md`).

---

## Vòng sửa (tổng toàn bộ lượt chạy thử khô)

**Số vòng sửa: 1.** Vòng 1 phát hiện hai lỗi, sửa cùng lúc, rồi chạy lại hai kịch bản bị ảnh hưởng.

| Lỗi (vòng 1) | Kịch bản | Tiêu chí | Sửa (chỉ references/SKILL, không đổi tiêu chí) | Chạy lại |
|---|---|---|---|---|
| Mục Banner-b không nói "ảnh cố ý không có chữ" (FR-210) | H | V3-US2-4 | `SKILL.md` (mục Chốt nhanh, mục b); `references/brief-card.md` (mẫu khi dừng, danh sách các mục, ví dụ điền sẵn); `references/example-pack.md` (lượt 1) | H: đạt |
| Bản nháp chế độ 3 có 94 từ, vượt 80 từ; quy tắc không nói cách rút; ví dụ chế độ 3 thiếu câu ảnh thật | N | V3-US3-4 | `references/text-in-image.md` (mục Quy tắc chế độ 3; ví dụ chế độ 3, 78 từ) | N: 74 từ, đạt |

**Lỗi của người chạy (không phải tài liệu):** tiêu đề mặc định của K nháp là "Một buổi sáng ở chợ Bến Thành" (7 từ), vượt 6 từ; đã rút còn 5 từ ngay khi soạn (xem `us1.md`).

**Kiểm tra độ dài:** `SKILL.md` 144 dòng (giới hạn ~150); `brief-card.md` 103 dòng; `text-in-image.md` 137 dòng; `example-pack.md` 110 dòng; `image-types.md` 31 dòng; `anti-slop.md` 109 dòng. Không reference nào vượt ~300 dòng.
