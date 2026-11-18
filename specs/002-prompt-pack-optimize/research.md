# Research: Prompt Pack v0.2

**Date**: 2026-11-18 | **Nguồn chính**: [R03]
`D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\03-plugin-test-staged-look-and-text-in-image.md`
(kèm [R01] `01-landscape-tells-anti-slop.md`, [R02] `02-prompt-strategy-preset-library.md`).

## R1. Đặt chi tiết ở đâu để `SKILL.md` vẫn ngắn

- **Decision**: `SKILL.md` chỉ giữ tiêu chí ngắn + thứ tự đầu ra; chi tiết Chốt nhanh vào
  `references/brief-card.md`, chi tiết chữ vào `references/text-in-image.md`; quy tắc tự kiểm chi tiết
  và từ cấm vào `references/anti-slop.md` §2.
- **Rationale**: FR-131; [R03] bảng "Cần sửa ở đâu" đề xuất đúng hai file này. Giữ `SKILL.md` ≤ ~150 dòng.
- **Alternatives**: Gộp hết vào `SKILL.md` — vượt giới hạn, nặng context ở mọi lượt.

## R2. Làm sao để model thật sự tự ép quy tắc

- **Decision**: (a) Tiêu chí tự kiểm trong `SKILL.md` viết dạng kiểm được trên văn bản ("mỗi prompt
  30–80 từ", "≤ 5 vật gọi tên", "không số chẵn"); (b) đặt chúng ngay cạnh mục Đầu ra, không ở cuối;
  (c) ví dụ đúng/sai cụ thể trong `example-pack.md` (Ví dụ B: prompt dàn dựng → prompt sửa);
  (d) bảng Kịch bản Media có cột đa dạng, buộc model quyết định khung/ánh sáng/người trước khi viết.
- **Rationale**: [R03] Kết luận 2 — quy tắc đã có nhưng không được ép vì nằm sâu trong reference và viết
  như lời khuyên. Cột bảng là cách "ép" không cần quy trình đánh số (Constitution III).
- **Alternatives**: Script đếm từ — vi phạm Constitution II; quy trình kiểm từng bước — vi phạm III.

## R3. Hướng hình do model chọn (Clarification Q1)

- **Decision**: 3 hướng chuẩn: **Đời thường** (chụp điện thoại, dấu vết dùng), **Biên tập/chuyên nghiệp**
  (tạp chí, thời trang, sản phẩm chỉn chu), **Minh họa thủ công**. Model chọn theo loại bài/kênh, ghi
  trong Chốt nhanh với một câu lý do, có thể phối theo ảnh. Gợi ý ánh xạ: blog how-to/đời sống → đời
  thường; thời trang, mỹ phẩm, thương hiệu cao cấp, landing bán hàng → biên tập; khái niệm trừu tượng →
  minh họa.
- **Nhóm preset E mới (4, v0.1 chưa test)**: E01 fashion editorial ngoài trời ánh tự nhiên; E02
  interior editorial (kiểu tạp chí nhà cửa); E03 product/still-life editorial có bóng cứng; E04 chân
  dung chuyên nghiệp/doanh nghiệp. Khung viết theo quy tắc FR-101…FR-105 (≤ 80 từ, ≤ 5 vật, nguồn sáng
  thật, một cue camera), không buzzword. Tính chân thật lấy từ ánh sáng, chất liệu, tư thế, bối cảnh.
- **Rationale**: Nhóm R thiên đời thường, S là minh họa; chưa có preset cho hướng chuyên nghiệp mà người
  dùng yêu cầu.
- **Alternatives**: Không thêm preset, để model tự viết — mất điểm tựa chất lượng cho hướng mới.

## R4. Ngưỡng dừng chờ của Chốt nhanh

- **Decision**: Dừng chờ khi số ảnh dự kiến ≥ 4 **hoặc** bài ≥ ~800 từ / ≥ 4 mục lớn; xuất luôn khi 1–3
  ảnh, người dùng nói "đưa luôn"/"không cần hỏi", hoặc không có người trả lời (pipeline). Khi xuất luôn,
  khối "Đã dùng mặc định" đặt ở đầu, thay mục Giả định ở cuối.
- **Rationale**: Spec Assumptions; [R03] mục D.
- **Alternatives**: Luôn dừng — chậm với yêu cầu nhỏ; không bao giờ dừng — lặp lại lỗi giả định thầm lặng.

## R5. Chế độ chữ và mặc định (Clarification Q2)

- **Decision**: 5 chế độ theo [R03] P1. Mặc định: hero, OG, thumbnail = chèn chữ sau; ảnh khác = không
  chữ. Quy tắc chế độ AI vẽ chữ và QC chữ chép từ [R03] P1 (tối đa ~6 từ, 1–2 dòng, mô tả kiểu chữ bằng
  đặc điểm, nền tương phản, lề 5%, "appears once; no other text anywhere"). Chế độ hai lượt: lượt 2 dùng
  "Image 1 = approved scene. Add the headline only; keep everything else unchanged."
- **Bài học từ ảnh thử**: chữ trắng trên tường sáng → tương phản yếu khi thu nhỏ → quy tắc bắt buộc mô tả
  bề mặt nền trung bình/tối hoặc dải màu đặc sau chữ.
- **Rationale**: Docs OpenAI/Google/BFL ([R02]) + một lượt thử ([R03] Kết luận 4).

## R6. Đa dạng cấp pack

- **Decision**: Cột mới trong bảng Kịch bản Media: Hướng, Khung, Độ cao máy, Ánh sáng (nhiệt độ + nguồn),
  Thời tiết/giờ, Người, Chữ. Quy tắc FR-108. Bảng slot trong `presets.md` thêm hàng "Nhiệt độ ánh sáng"
  (ấm tungsten, trung tính ban ngày, lạnh u ám, huỳnh quang xanh, đèn đường natri) và "Loại khung"
  (toàn, trung, cận chi tiết, qua vai, đang làm dở).
- **Rationale**: [R03] P3, bảng A.

## R7. Bốn tell mới

- **Decision**: Thêm vào bảng `anti-slop.md` §3 (thành 15 dòng), nhãn "suy luận từ một lượt test, chưa
  đo": đối xứng/đồ thành cặp → tránh số chẵn, đặt lệch, một món khác biệt; thuần chủ đề → một vật lạc đề
  theo ngữ cảnh; không dấu vết dùng → một dấu vết cụ thể; model tự thêm chữ/vật → nói rõ vật nền + câu
  "plain unlabeled …, no readable text anywhere".
- **Rationale**: [R03] P4, bảng A.

## R8. Fixture bài thật

- **Decision**: `tests/fixtures/05-christmas-article.md` = bài `C:\Users\user\Downloads\PYW_How To.md`
  (2.889 từ, có 2 chỗ chờ sản phẩm) chép nguyên văn, thêm HTML comment mục đích ở đầu. Repo private nên
  giữ nguyên văn để test sát thật. `06-staged-images-feedback.md` = mô tả 3 ảnh lỗi theo [R03] "Sự thật"
  (sofa/chăn caro, hành lang/cầu thang, bếp) + trích các cụm prompt gây lỗi được [R03] nêu ("Two small
  evergreen wreaths", "two ceramic holiday mugs", "Four knitted Christmas stockings", "soft winter
  daylight", "slightly imperfect", "genuinely lived-in") + lời người dùng "đơn điệu, quá clean, như được
  sắp đặt".
- **Rationale**: FR-129; bản pack gốc 9 prompt không có trong repo, chỉ dùng phần [R03] đã ghi.

## R9. Phiên bản và tương thích

- **Decision**: 0.2.0 (MINOR — thêm hành vi, đổi thứ tự đầu ra). CHANGELOG nêu rõ các điểm thay 001:
  FR-002/003 (cách hỏi), FR-011 (đa dạng), FR-020 (điều kiện mockup), edge case chữ. Spec 001 giữ nguyên.
