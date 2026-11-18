# Image Prompt Pack (plugin)

Lập Kịch bản Media và Prompt Pack từ bất kỳ đầu vào nào. Mỗi ảnh có một prompt tiếng Anh copy dùng ngay, đã áp quy tắc chống slop. Plugin không tạo ảnh.

## Cài đặt

Claude Code:

```text
/plugin marketplace add mktphuchung-wq/Image-Prompt-Packs
/plugin install image-prompt-pack@image-prompt-packs
```

Codex: thêm marketplace Git theo hướng dẫn ở `README.md` của repo gốc, rồi bật `image-prompt-pack@image-prompt-packs`.

## Lượt đầu có thể là Chốt nhanh

Với bài dài (khoảng 800 từ trở lên, hoặc từ 4 mục lớn trở lên) hoặc pack từ 4 ảnh, lượt đầu là Kịch bản Media kèm khối **Chốt nhanh**: tối đa 4 mục, mỗi mục có mặc định. Trả lời "ok" để nhận pack theo mặc định, hoặc sửa một mục. Yêu cầu 1–3 ảnh xuất luôn, với khối "Đã dùng mặc định" ở đầu phản hồi.

## Tên skill theo từng harness

| Harness | Gọi rõ | Gọi ngầm |
|---|---|---|
| Claude Code | `/image-prompt-pack:prompt-pack` | theo mô tả của skill |
| Codex | `$prompt-pack` | có (`allow_implicit_invocation: true`) |
| ChatGPT | nhắc tên skill, hoặc dùng Project đã nạp | theo instructions của Project |

## Cấu trúc skill `prompt-pack`

- `SKILL.md`: mục tiêu, tiêu chí thành công, đầu ra, cách dùng tri thức và ranh giới.
- `agents/openai.yaml`: metadata hiển thị cho Codex.
- `references/anti-slop.md`: quy tắc viết prompt, tự kiểm trước khi xuất, từ cấm đứng một mình, bảng 15 dấu hiệu nhận dạng ảnh AI và cách đối phó, đa dạng cấp pack, mục mockup, checklist QC đạt/không đạt.
- `references/brief-card.md`: khi nào hỏi (Chốt nhanh) và khi nào xuất luôn; bốn mục, mặc định và mẫu khối.
- `references/text-in-image.md`: năm chế độ chữ trong ảnh, quy tắc AI vẽ chữ, tiếng Việt có dấu, hai lượt, QC chữ 7 mục.
- `references/presets.md`: 28 preset R (12), S (8), C (4), E (4, biên tập/chuyên nghiệp), nhãn v0.1 chưa test; bảng slot đa dạng hóa ảnh trong pack.
- `references/image-types.md`: 7 loại ảnh, tỉ lệ, hướng gợi ý, chữ mặc định, preset hợp, rủi ro; đề xuất số ảnh theo độ dài bài.
- `references/example-pack.md`: bài dài đi qua hai lượt (Chốt nhanh, rồi pack) và một lượt sửa ảnh dàn dựng làm mẫu đầu ra.
