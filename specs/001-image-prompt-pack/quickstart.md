# Quickstart: Kiểm chứng Image Prompt Pack Plugin

Hướng dẫn chạy để chứng minh plugin hoạt động đầu-cuối. Chi tiết hợp đồng: [contracts/](./contracts/);
tiêu chí đạt từng fixture: `tests/acceptance.md` (tạo trong implement).

## 0. Điều kiện

- Repo đã đẩy lên `https://github.com/mktphuchung-wq/Image-Prompt-Packs` (nhánh mặc định chứa
  `plugins/image-prompt-pack/`). Trước khi đẩy, kiểm local bằng đường dẫn thư mục thay cho URL.
- Có ít nhất một trong: Claude Code, Codex, ChatGPT.

## 1. Kiểm manifest (máy, ~5 giây)

Từ repo root, PowerShell:

```powershell
$f = '.claude-plugin/marketplace.json','.agents/plugins/marketplace.json','plugins/image-prompt-pack/.claude-plugin/plugin.json','plugins/image-prompt-pack/.codex-plugin/plugin.json'
$j = $f | ForEach-Object { Get-Content $_ -Raw | ConvertFrom-Json }   # lỗi ở đây = JSON hỏng
$v = $j[2].version; if ($j[3].version -ne $v) { "VERSION MISMATCH" } elseif (-not (Select-String -Path CHANGELOG.md -Pattern "\[$v\]" -Quiet)) { "CHANGELOG thiếu $v" } else { "OK $v" }
```

Kỳ vọng: `OK 0.1.0`.

## 2. Cài và cập nhật

**Claude Code**

```text
/plugin marketplace add mktphuchung-wq/Image-Prompt-Packs
/plugin install image-prompt-pack@image-prompt-packs
```

Kỳ vọng: skill `image-prompt-pack:prompt-pack` xuất hiện. Cập nhật: `/plugin marketplace update image-prompt-packs`.

**Codex** — thêm vào `~/.codex/config.toml`, giữ nguyên mục cũ:

```toml
[marketplaces.image-prompt-packs]
source_type = "git"
source = "https://github.com/mktphuchung-wq/Image-Prompt-Packs.git"

[plugins."image-prompt-pack@image-prompt-packs"]
enabled = true
```

Kỳ vọng: mở Codex mới, `$prompt-pack` có trong danh sách skill.

**ChatGPT** — nén `plugins/image-prompt-pack/skills/prompt-pack/` thành zip, tải lên làm Skill; nếu
không có Skills: tạo Project, dán thân `SKILL.md` vào instructions, đính kèm 4 file `references/`.

Ghi kết quả từng harness vào `docs/verification.md` (SC-006).

## 3. Chạy 4 kịch bản

| # | Fixture | Câu gọi | Đạt khi (tóm tắt — đầy đủ ở `tests/acceptance.md`) |
|---|---|---|---|
| 1 | `tests/fixtures/01-blog-article.md` | "Làm prompt ảnh cho bài này" + dán bài | Có Kịch bản Media đủ trường; 3–8 ảnh; mỗi ảnh một khối prompt copy được; không Reference thừa; không mockup tự thêm |
| 1b | (cùng hội thoại) | "làm prompt ảnh cho bài vừa rồi" ở lượt sau | Tự lấy bài từ lịch sử, không bắt dán lại |
| 2 | `tests/fixtures/02-one-line-request.md` | dán câu yêu cầu | Có mục Giả định; pack đầy đủ; hỏi tối đa 3 câu nếu hỏi |
| 3 | `tests/fixtures/03-messy-log.md` | "làm media cho phần đang bàn" | Nói rõ đã chọn phần nào của log |
| 4 | `tests/fixtures/04-failed-image-feedback.md` | dán prompt + mô tả lỗi | Có Chẩn đoán, prompt đã sửa, 1–3 dòng Đã đổi; chỉ sửa ảnh bị phàn nàn |
| 5 | (sau 1) | "ảnh 2 cần mockup áo hoodie của shop" | Ảnh 2 có Reference ảnh sản phẩm thật, prompt không vẽ lại thiết kế, có ghi chú ghép + giữ metadata |

Chạy cả 5 trên mỗi harness đã cài để kiểm SC-007 (cấu trúc tương đương).

## 4. Kiểm chất lượng ảnh

1. Dán 3 prompt bất kỳ từ kịch bản 1 vào một công cụ tạo ảnh đang dùng (không đổi chữ nào) → ảnh ra
   được, không lỗi cú pháp (SC-005).
2. Đối chiếu từng ảnh với checklist QC trong `references/anti-slop.md` (SC-008).
3. Blind test preset theo `docs/blind-test.md` (SC-003) — làm trước khi lên 1.0.0.
