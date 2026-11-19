# Chạy thử khô US2 — khối Vùng chữ và cột Chữ (v0.3.0)

**Nguồn đầu ra:** các khối Vùng chữ và cột Chữ lấy từ `us1.md` (kịch bản I, K) và `us4.md` (kịch bản H). Cách chạy và giới hạn như `us1.md`.

## Đầu ra liên quan

**Cột Chữ (kịch bản I, bảng Kịch bản Media):**

| # | Ảnh | Chữ |
|---|---|---|
| 1 | Hero | 2 chèn chữ sau — 1/3 trái |
| 2 | Minh họa phòng khách | 0 không chữ |
| 3 | Lối vào | 0 không chữ |
| 4 | Phòng ngủ | 0 không chữ |
| 5 | Ảnh chia sẻ | 2 chèn chữ sau — 1/3 trái |

**Khối Vùng chữ** (đầy đủ ở `us1.md`):
- Hero (I): 1/3 trái, khoảng 40% khung · tường xám trung bình (a) · nền tối trung bình → chữ trắng hoặc kem · lề ~5% · tiêu đề 1 dòng · cắt sang 1.91:1 còn nguyên; 2:3 cần prompt dọc riêng · câu cố định.
- Ảnh chia sẻ (I): 1/3 trái, khoảng 35% khung · tường kem nhạt (a) · nền sáng dịu → chữ gần đen · lề ~5% · tiêu đề 1 dòng · cắt sang 16:9 còn nguyên; 2:3 cần prompt dọc riêng · câu cố định.
- Hero (K): 1/3 trái, khoảng 40% khung · hậu cảnh làm mềm nhẹ (b) · nền tối trung bình → chữ trắng hoặc kem; hậu cảnh rối thì thêm dải màu đặc · lề ~5% · tiêu đề 1–2 dòng · cắt sang 1.91:1 còn nguyên; 2:3 cần prompt dọc riêng · câu cố định.

**Mục Banner, điểm b (kịch bản H, bản sau sửa):** "chừa vùng, ảnh cố ý không có chữ, tự thêm tiêu đề bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề · hai lượt".

---

## Bảng chấm US2 (tiêu chí `tests/acceptance.md`, mục v0.3 — US2)

| # | Kịch bản | Kết quả | Bằng chứng |
|---|---|---|---|
| V3-US2-1 | I, K | Đạt | Cả ba khối có đủ tám trường (vị trí, cỡ, cách tạo, tông, màu chữ, lề, số dòng, câu cố định) cộng khối "khi cắt khung" |
| V3-US2-2 | I | Đạt | Cột Chữ: "2 chèn chữ sau — 1/3 trái" cho hero và ảnh chia sẻ; ảnh chế độ 0 ghi "0 không chữ" |
| V3-US2-3 | I | Đạt | Khối hero và khối ảnh chia sẻ đều nói khung 2:3 mất vùng và cần prompt dọc riêng |
| V3-US2-4 | H, K | Đạt sau vòng sửa 1 (H). K: không áp dụng | Bản đầu của điểm b không nói "ảnh cố ý không có chữ" (trượt FR-210); đã sửa ở `SKILL.md`, `brief-card.md`, `example-pack.md`, chạy lại H đạt. K: điểm b đã có trong intake ("tiêu đề sẽ thêm sau", tức chèn chữ sau) nên bị bỏ theo quy tắc điểm đã chốt thì bỏ; tiêu chí được kiểm ở H |
| V3-US2-5 | I, K | Đạt | Không có sơ đồ ký tự; không có tên công cụ thiết kế; vị trí mô tả bằng lời |
| V3-US2-6 | K | Đạt | Khối ghi (b); tông "nền tối trung bình" khớp với "medium-dark" trong prompt |
| V3-US2-7 | I | Đạt | Cỡ 40% (hero) và 35% (ảnh chia sẻ) nằm trong 35–50%; tiêu đề ngắn ("Indoor Christmas Decorations") nên không cần 45–50% |

**Tổng US2:** 7/7 đạt (một mục, V3-US2-4, đạt sau vòng sửa 1; một điểm K không áp dụng, có lý do ghi trên).
