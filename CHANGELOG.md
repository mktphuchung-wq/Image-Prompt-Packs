# Changelog

Ghi chú thay đổi của plugin `image-prompt-pack`. Định dạng theo Keep a Changelog; phiên bản theo SemVer.

## [0.3.0] - 2026-11-19

### Added

- Vùng chữ dựng sẵn cho ảnh chế độ 2 (hero, ảnh chia sẻ, thumbnail mặc định): prompt dựng bố cục banner với chủ thể một phía và vùng chữ ở phía còn lại, tạo bằng một trong ba cách: khoảng trống thật trong cảnh, làm mềm hậu cảnh nhẹ, hoặc mảng phẳng cho hướng Minh họa. Chi tiết ở `references/text-in-image.md` mục "Dựng vùng chữ".
- Khối **Vùng chữ** ngay dưới prompt chế độ 2 (vị trí, cỡ, cách tạo, tông nền và màu chữ gợi ý, lề an toàn, số dòng, tình trạng khi cắt khung); cột Chữ ghi vị trí vùng, ví dụ "2 chèn chữ sau — 1/3 trái". Chế độ 3 và 4 dùng lại vùng chữ đã xác định.
- Lượt đầu dừng hỏi khi có một trong bốn trường hợp đặc biệt: chữ, phong cách, nội dung đặc biệt, format mới lạ. Mỗi câu hỏi nêu lý do kích hoạt và có mặc định. Mục Banner gồm bốn điểm: tiêu đề và số dòng, cách đặt chữ, vùng chữ, các khung.
- Chốt format các ảnh còn lại qua bảng Kịch bản Media: người dùng sửa theo số dòng (ví dụ "ảnh 3 đổi 4:5, bỏ ảnh 5") hoặc trả "ok".
- Định nghĩa "format mới lạ" trong `references/image-types.md`.
- Ba fixture mới: 07 (hero cảnh chợ đông, làm mềm hậu cảnh), 08 (carousel 5 slide, format mới lạ), 09 (ba ảnh minh họa đã chốt, xuất luôn).
- Acceptance v0.3 và bằng chứng chạy thử khô trong `tests/runs/2026-11-19-v0.3/`.

### Changed

- Điều kiện dừng của lượt đầu: bỏ ngưỡng theo số ảnh (từ 4 ảnh) và độ dài bài (khoảng 800 từ), thay FR-110 và FR-114 của 002. Số ảnh hay độ dài bài một mình không còn là lý do dừng.
- Ngoại lệ có giới hạn cho tell "bokeh mọi cảnh" trong `references/anti-slop.md`: chỉ ảnh chế độ 2, 3, 4 được làm mềm hậu cảnh, chỉ ở vùng chữ và ở mức nhẹ; ảnh trong bài vẫn giữ nét toàn cảnh.

## [0.2.1] - 2026-11-19

### Changed

- Đồng bộ metadata với tính năng 0.2.0: mô tả plugin trong marketplace Claude, hai `plugin.json` (Claude, Codex), giao diện Codex (`shortDescription`, `longDescription`, `defaultPrompt`), `agents/openai.yaml` và mô tả kích hoạt của skill `prompt-pack` nay nêu Chốt nhanh, chế độ chữ trong ảnh và tự kiểm chống ảnh dàn dựng. Thêm keywords `brief-card`, `text-in-image`, `editorial`. Không đổi hành vi.

## [0.2.0] - 2026-11-18

### Added

- Chốt nhanh: bài dài hoặc pack từ 4 ảnh trở lên có Kịch bản Media kèm khối Chốt nhanh ở đầu phản hồi (tối đa 4 mục, mỗi mục có mặc định); trả lời "ok" để nhận pack theo mặc định. Chi tiết ở `references/brief-card.md`.
- Chế độ chữ trong ảnh (0 không chữ, 1 chữ trong cảnh, 2 chèn chữ sau, 3 AI vẽ chữ, 4 hai lượt) và QC chữ đạt/không đạt 7 mục ở `references/text-in-image.md`. Mặc định: hero, ảnh chia sẻ và thumbnail chèn chữ sau.
- Tiêu chí tự kiểm trước khi xuất: 30–80 từ, ≤ 5 vật gọi tên, không số chẵn hay bố trí đối xứng, ảnh đời thường có một vật lạc đề và một dấu vết người, danh sách từ cấm đứng một mình, câu chặn chữ cho ảnh không chữ.
- Bảng đa dạng cấp pack trong Kịch bản Media: các cột Hướng, Khung, Độ cao máy, Ánh sáng, Thời tiết/giờ, Người, Chữ, cùng quy tắc đa dạng cho pack từ 4 ảnh.
- Bốn tell mới (15 tell tổng cộng), ghi rõ là suy luận từ một lượt test, chưa đo.
- Nhóm preset E biên tập/chuyên nghiệp (E01–E04), trạng thái v0.1 chưa test; tổng 28 preset.
- Fixture 05 (bài Giáng sinh của lượt test, có 2 chỗ chờ sản phẩm) và fixture 06 (ba ảnh lỗi mô tả bằng chữ); acceptance v0.2 và bằng chứng chạy thử khô trong `tests/runs/2026-11-18-v0.2/`.

### Changed (thay đổi so với 0.1.0)

- Cách hỏi: thay FR-002/FR-003 của 001. Mục Giả định ở cuối pack được thay bằng khối "Đã dùng mặc định" ở đầu phản hồi; bài dài hoặc từ 4 ảnh trở lên dừng chờ sau khối Chốt nhanh.
- Đa dạng: thay FR-011 của 001 bằng bảng đa dạng cấp pack (FR-107, FR-108).
- Mockup: thay FR-020 của 001. Chỉ hỏi xác nhận khi bài nhắc sản phẩm hoặc có chỗ chờ sản phẩm, mặc định không làm; không chọn thì pack không có prompt mockup hay mục "Bonus".
- Chính sách chữ: thay edge case "ảnh có chữ" của 001 bằng năm chế độ chữ có quy tắc riêng và mặc định theo loại ảnh.

## [0.1.0] - 2026-11-18

- Skill `prompt-pack`: từ intake bất kỳ (bài viết, log, lịch sử hội thoại, output trước, yêu cầu ngắn) lập Kịch bản Media và Prompt Pack, mỗi ảnh một prompt tiếng Anh copy dùng ngay; sửa prompt khi ảnh ra chưa đạt.
- 24 preset phong cách R (12), S (8), C (4), nhãn v0.1 chưa test; bảng slot đa dạng hóa ảnh trong cùng pack.
- 7 loại ảnh: hero, minh họa trong bài, infographic, mạng xã hội, thumbnail, lifestyle; mockup sản phẩm chỉ khi người dùng yêu cầu.
- Tri thức chống slop: bảng 11 dấu hiệu nhận dạng ảnh AI kèm cách đối phó, quy tắc viết prompt, checklist QC đạt/không đạt.
- Phân phối: marketplace Claude Code (`.claude-plugin/marketplace.json`) và Codex (`.agents/plugins/marketplace.json`) cùng trỏ tới một thư mục plugin.
