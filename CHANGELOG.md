# Changelog

Ghi chú thay đổi của plugin `image-prompt-pack`. Định dạng theo Keep a Changelog; phiên bản theo SemVer.

## [0.1.0] - 2026-11-18

- Skill `prompt-pack`: từ intake bất kỳ (bài viết, log, lịch sử hội thoại, output trước, yêu cầu ngắn) lập Kịch bản Media và Prompt Pack, mỗi ảnh một prompt tiếng Anh copy dùng ngay; sửa prompt khi ảnh ra chưa đạt.
- 24 preset phong cách R (12), S (8), C (4), nhãn v0.1 chưa test; bảng slot đa dạng hóa ảnh trong cùng pack.
- 7 loại ảnh: hero, minh họa trong bài, infographic, mạng xã hội, thumbnail, lifestyle; mockup sản phẩm chỉ khi người dùng yêu cầu.
- Tri thức chống slop: bảng 11 dấu hiệu nhận dạng ảnh AI kèm cách đối phó, quy tắc viết prompt, checklist QC đạt/không đạt.
- Phân phối: marketplace Claude Code (`.claude-plugin/marketplace.json`) và Codex (`.agents/plugins/marketplace.json`) cùng trỏ tới một thư mục plugin.
