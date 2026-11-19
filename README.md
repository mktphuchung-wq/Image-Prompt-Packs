# Image Prompt Packs

Plugin cho Claude Code và Codex, cùng một nguồn nội dung dùng được trên ChatGPT. Từ bất kỳ đầu vào nào (bài viết, log, lịch sử hội thoại, output của bước trước, hoặc một câu yêu cầu), plugin lập **Kịch bản Media** và **Prompt Pack**: mỗi ảnh có một prompt tiếng Anh copy dùng ngay, đã áp quy tắc chống slop.

**Plugin không tạo ảnh.** Bạn dán prompt vào công cụ tạo ảnh đang dùng.

## Cách gọi

- "Làm prompt ảnh cho bài này" (kèm bài viết, hoặc bài đã có sẵn trong hội thoại).
- "Bài này cần những ảnh gì? Đưa prompt luôn."
- "Ảnh ra trông AI quá, sửa prompt giúp tôi." (kèm prompt và mô tả lỗi của ảnh).
- "Ảnh 2 cần mockup áo hoodie của shop." Chỉ dùng khi bạn thật sự cần mockup sản phẩm; khi đó cần đính kèm ảnh sản phẩm thật.

Plugin chỉ dừng hỏi khi có trường hợp đặc biệt: chữ trong ảnh (banner, hero, ảnh chia sẻ chưa chốt cách đặt chữ), phong cách, nội dung đặc biệt (chỗ chờ sản phẩm, người hoặc thương hiệu thật, số liệu cho infographic, nhiều ngôn ngữ) hoặc format mới lạ (carousel, before/after, ảnh so sánh...). Khi dừng, plugin trả khối **Chốt nhanh** kèm lý do và mặc định (tối đa 4 mục; banner gồm bốn điểm: tiêu đề, cách đặt chữ, vùng chữ, khung). Trả lời "ok" để nhận pack theo mặc định, hoặc sửa theo số dòng trong bảng Kịch bản Media. Không có trường hợp đặc biệt, hoặc bạn nói "đưa luôn", thì pack xuất ngay. Số ảnh và độ dài bài không phải lý do dừng.

Hero và ảnh chia sẻ chế độ chèn chữ sau có vùng chữ dựng sẵn: prompt nêu vị trí và cách tạo vùng, còn mỗi ảnh có khối **Vùng chữ** (vị trí, cỡ, tông nền, màu chữ gợi ý, lề an toàn) để bạn thêm tiêu đề bằng công cụ thiết kế.

## Cài và cập nhật

### Claude Code

```text
/plugin marketplace add mktphuchung-wq/Image-Prompt-Packs
/plugin install image-prompt-pack@image-prompt-packs
```

Kỳ vọng: skill `image-prompt-pack:prompt-pack` xuất hiện. Cập nhật bằng `/plugin marketplace update image-prompt-packs`.

### Codex

Thêm vào `~/.codex/config.toml`, giữ nguyên các mục cũ:

```toml
[marketplaces.image-prompt-packs]
source_type = "git"
source = "https://github.com/mktphuchung-wq/Image-Prompt-Packs.git"

[plugins."image-prompt-pack@image-prompt-packs"]
enabled = true
```

Mở phiên Codex mới để thấy `$prompt-pack` trong danh sách skill. Cập nhật: Codex kéo lại git source.

### ChatGPT (đường lui)

ChatGPT chưa có cơ chế marketplace Git đã kiểm chứng, nên dùng cùng thư mục skill:

- Nén `plugins/image-prompt-pack/skills/prompt-pack/` thành zip và tải lên làm Skill, nếu tài khoản có tính năng Skills.
- Nếu không có Skills: tạo một Project, dán phần thân `SKILL.md` vào Project instructions, và đính kèm bốn file trong `references/`.
- Cập nhật: tải lại từ bản phát hành mới.

## Trạng thái phiên bản

Phiên bản hiện tại là 0.3.0. Bản 0.3.0 thêm vùng chữ dựng sẵn cho hero (chế độ 2, dùng lại ở chế độ 3 và 4), khối Vùng chữ dưới prompt, và lượt đầu chỉ dừng khi có trường hợp đặc biệt; bản 0.2.1 chỉ đồng bộ metadata. 28 preset phong cách (R 12, S 8, C 4, E 4) đang ở nhãn **v0.1 chưa test** trên model thật. Bản 0.2.0 thêm Chốt nhanh, chế độ chữ trong ảnh, tự kiểm trước khi xuất và bảng đa dạng cấp pack; chi tiết ở `CHANGELOG.md`. Kết quả blind test ghi theo `docs/blind-test.md`. Mức kiểm chứng từng hạng mục xem ở `docs/verification.md`.

## Cấu trúc repo

- `.claude-plugin/marketplace.json`: marketplace Claude Code.
- `.agents/plugins/marketplace.json`: marketplace Codex.
- `plugins/image-prompt-pack/`: plugin, với manifest cho Claude và Codex, cùng một skill `prompt-pack`.
- `plugins/image-prompt-pack/skills/prompt-pack/`: `SKILL.md`, `agents/openai.yaml` và `references/` (anti-slop, presets, image-types, example-pack).
- `tests/`: fixture, `acceptance.md` và `runs/` (bằng chứng chạy khô).
- `docs/`: `verification.md` (mức kiểm chứng) và `blind-test.md`.
- `specs/` và `.specify/`: đặc tả và quy trình theo Spec Kit.
- `CHANGELOG.md`: ghi chú thay đổi theo phiên bản.

## Nguồn tri thức (chỉ đọc)

- [R01] `D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\01-landscape-tells-anti-slop.md`
- [R02] `D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\02-prompt-strategy-preset-library.md`

## Phát hành bản mới

1. Tăng `version` ở cả hai file `plugin.json` (`.claude-plugin` và `.codex-plugin`) cùng một số.
2. Thêm mục `## [x.y.z]` vào `CHANGELOG.md`, kèm ghi chú thay đổi ngắn.
3. Chạy kiểm manifest trong `specs/001-image-prompt-pack/quickstart.md` mục 1. Kết quả phải là `OK x.y.z`.
4. Commit và đẩy lên nhánh mặc định.
