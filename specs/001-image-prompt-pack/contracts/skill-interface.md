# Contract: Giao diện skill `prompt-pack`

## Frontmatter `SKILL.md`

```yaml
---
name: prompt-pack
description: <một câu tiếng Anh nêu khi nào dùng + vài cụm kích hoạt tiếng Việt/Anh>
---
```

- `name` = tên thư mục skill = `prompt-pack`.
- `description` phải kích hoạt khi người dùng: xin prompt tạo ảnh cho bài viết/nội dung/landing/social;
  hỏi "bài này cần ảnh gì"; xin sửa prompt vì ảnh ra trông AI/lỗi. Ví dụ cụm: "prompt ảnh", "làm ảnh
  cho bài này", "image prompts", "media plan", "ảnh bị AI quá", "sửa prompt ảnh".
- `description` phải nói rõ skill **không tạo ảnh** để harness không chọn nó cho yêu cầu "tạo ảnh ngay".

## Thân `SKILL.md` (thứ tự mục)

1. **Mục tiêu** — một đoạn.
2. **Tiêu chí thành công** — gạch đầu dòng kiểm được, ánh xạ FR-002…FR-016, FR-020, FR-021.
3. **Đầu ra** — tóm tắt [prompt-pack-output.md](./prompt-pack-output.md), kèm mẫu ngắn.
4. **Tri thức** — khi nào đọc file nào trong `references/` (đường dẫn tương đối `references/<file>`).
5. **Ranh giới** — không tạo ảnh; không adapter công cụ; mockup chỉ khi được yêu cầu; không giả mạo
   người thật; nội dung nhạy cảm chọn hướng hình an toàn; không gửi nội dung ra ngoài.

Không có: bước thủ tục đánh số kiểu "Bước 1: đọc file… Bước 2: …", tên tool riêng của một harness,
biến đường dẫn riêng (`${CLAUDE_PLUGIN_ROOT}`…). Dài ≤ ~150 dòng.

## `agents/openai.yaml` (Codex)

```yaml
interface:
  display_name: "Prompt Pack"
  short_description: "<≤ 80 ký tự>"
  default_prompt: "Use $prompt-pack to plan the images for this article and give me copy-ready prompts."
policy:
  allow_implicit_invocation: true
```

Không có `dependencies` (plugin không cần MCP).

## Cách gọi trên từng harness

| Harness | Gọi rõ | Gọi ngầm |
|---|---|---|
| Claude Code | `/image-prompt-pack:prompt-pack` | theo `description` |
| Codex | `$prompt-pack` | `allow_implicit_invocation: true` |
| ChatGPT | nhắc tên skill / Project đã nạp | theo instructions của Project |
