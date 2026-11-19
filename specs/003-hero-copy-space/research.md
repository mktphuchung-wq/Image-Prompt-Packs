# Research: Vùng chữ + khâu khởi tạo (v0.3.0)

**Date**: 2026-11-19. Nguồn: spec 003 + Clarifications; [R02] `02-prompt-strategy-preset-library.md`
(docs OpenAI/Google/BFL về bố cục và chữ); [R03] `03-plugin-test-staged-look-and-text-in-image.md` (bài học
tương phản: chữ trắng trên tường sáng yếu khi thu nhỏ).

## R1. Cách viết vùng chữ chạy trên mọi công cụ

- **Decision**: Viết bằng lời, khẳng định, vị trí theo phần khung: "subject on the right third; the left
  two-thirds is a plain dark-grey wall with nothing on it". Ba cách:
  - (a) Khoảng trống thật: gọi tên bề mặt (wall, sky, floor, tabletop, plain fabric) + tông + "nothing in
    that area".
  - (b) Làm mềm hậu cảnh nhẹ: "subject and foreground sharp; the background on the left falls into a soft,
    low-detail blur where shapes stay recognisable". Không dùng thông số máy ảnh (f/1.8…), không "bokeh".
  - (c) Mảng phẳng (Minh họa): "a wide flat area of [paper/colour] on the left".
- **Rationale**: Docs các hãng đều khuyên mô tả bố cục bằng vị trí và diễn đạt khẳng định ([R02] mục A);
  FR-012 cấm cú pháp riêng; spec Assumptions cấm thông số máy ảnh.
- **Alternatives**: Từ khóa "copy space", "negative space" đơn lẻ — mơ hồ, chính là lỗi hiện tại; có thể
  dùng kèm nhưng không thay mô tả cụ thể.

## R2. Chọn cách (a)/(b)/(c)

- **Decision**: (a) mặc định khi cảnh có bề mặt trơn tự nhiên; (b) khi cảnh đông hoặc hướng Biên tập cần
  chiều sâu; (c) hướng Minh họa. Khung ngang: vùng chữ một phần ba hoặc nửa trái/phải; khung dọc: dải trên
  hoặc dưới. Cỡ vùng 35–50% khung; tiêu đề dài/tiếng Việt nhiều dòng → 45–50%.
- **Tông và màu chữ gợi ý**: vùng tối trung bình → chữ trắng/kem; vùng sáng dịu → chữ gần đen; màu thương
  hiệu nếu đủ tương phản, không đủ thì gợi ý dải màu đặc sau chữ ([R03] bài học tương phản).

## R3. Ngoại lệ bokeh

- **Decision**: Ghi ngay dưới tell "Bokeh nền mờ mọi cảnh" và cạnh mục QC "Nền không bokeh vô cớ": chỉ ảnh
  chế độ 2/3/4, chỉ hậu cảnh vùng chữ, mức nhẹ (vật vẫn nhận ra), chủ thể + tiền cảnh nét. Ảnh chế độ 0/1
  giữ "deep focus".
- **Rationale**: FR-205; tránh mâu thuẫn tri thức.

## R4. Khối Vùng chữ

- **Decision**: 6–7 dòng ngắn dưới khối prompt: Vị trí · Cỡ · Cách tạo · Tông nền → màu chữ gợi ý · Lề an
  toàn ~5% · Số dòng tiêu đề dự kiến · Khi cắt khung khác · và câu "Ảnh cố ý không có chữ; thêm tiêu đề bằng
  công cụ thiết kế." Cột Chữ: "2 chèn chữ sau — 1/3 trái".
- **Cắt khung**: hero 16:9 → OG 1.91:1 thường còn nguyên nếu vùng ở hai bên; → 2:3/9:16 mất → đề xuất prompt
  khung dọc riêng (FR-209).

## R5. Trường hợp kích hoạt lượt đầu

- **Decision**: Bốn trường hợp FR-215 thay bảng dừng của `brief-card.md`. Lượt đầu luôn quét intake trước:
  - (1) Chữ: có hero/banner/OG/thumbnail và intake chưa nói cách đặt chữ hoặc chưa có tiêu đề chốt.
  - (2) Phong cách: nội dung hợp ≥ 2 hướng mà sai sẽ làm lại cả pack; không có brand guideline.
  - (3) Nội dung đặc biệt: chỗ chờ sản phẩm, người/thương hiệu thật, chủ đề nhạy cảm, số liệu cho infographic,
    nhiều ngôn ngữ.
  - (4) Format mới lạ: loại ảnh không có trong bảng `image-types.md` (carousel, before/after, chuỗi kể chuyện,
    so sánh, in ấn) hoặc tỉ lệ/kênh lạ.
- **Hệ quả**: Bài blog thông thường có hero → thường kích hoạt (1) → dừng; đúng ý người dùng "hỏi banner".
  Yêu cầu đã chốt mọi thứ → xuất luôn.
- **Mục Banner**: tính một mục (giữ ≤ 4 mục của 002), 4 điểm a–d (FR-218); điểm intake đã chốt thì bỏ.
- **Format ảnh khác**: bảng Kịch bản Media + một dòng hướng dẫn sửa theo số dòng (FR-219); không hỏi từng ảnh.

## R6. Phiên bản

- **Decision**: 0.3.0 (MINOR: đổi hành vi lượt đầu và đầu ra chế độ 2). CHANGELOG nêu thay FR-110/FR-114 của 002.
