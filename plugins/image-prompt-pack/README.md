# Image Prompt Pack (plugin)

Lập Kịch bản Media và Prompt Pack từ bất kỳ đầu vào nào. Mỗi ảnh có một prompt tiếng Anh copy dùng ngay, đã áp quy tắc chống slop. Plugin không tạo ảnh.

## Cài đặt

Claude Code:

```text
/plugin marketplace add mktphuchung-wq/Image-Prompt-Packs
/plugin install image-prompt-pack@image-prompt-packs
```

Codex: thêm marketplace Git theo hướng dẫn ở `README.md` của repo gốc, rồi bật `image-prompt-pack@image-prompt-packs`.

## Tên skill theo từng harness

| Harness | Gọi rõ | Gọi ngầm |
|---|---|---|
| Claude Code | `/image-prompt-pack:prompt-pack` | theo mô tả của skill |
| Codex | `$prompt-pack` | có (`allow_implicit_invocation: true`) |
| ChatGPT | nhắc tên skill, hoặc dùng Project đã nạp | theo instructions của Project |

## Cấu trúc skill `prompt-pack`

- `SKILL.md`: mục tiêu, tiêu chí thành công, đầu ra, cách dùng tri thức và ranh giới.
- `agents/openai.yaml`: metadata hiển thị cho Codex.
- `references/anti-slop.md`: quy tắc viết prompt, bảng 11 dấu hiệu nhận dạng ảnh AI và cách đối phó, mục mockup, checklist QC đạt/không đạt.
- `references/presets.md`: 24 preset R (12), S (8), C (4), nhãn v0.1 chưa test; bảng slot đa dạng hóa ảnh trong pack.
- `references/image-types.md`: 7 loại ảnh, tỉ lệ thường dùng, preset hợp, rủi ro chữ; đề xuất số ảnh theo độ dài bài.
- `references/example-pack.md`: một pack hoàn chỉnh và một lượt sửa prompt làm mẫu đầu ra.
