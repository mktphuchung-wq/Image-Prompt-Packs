---
name: prompt-pack
description: "Turns any content, log, chat history or short request into a media plan and a copy-ready, anti-slop image prompt pack (one English prompt per image), and rewrites a prompt when the generated image looks like AI slop. Does not generate images. Use for 'prompt ảnh', 'làm ảnh cho bài này', 'image prompts', 'media plan', 'ảnh bị AI quá', 'sửa prompt ảnh'."
---

# Prompt Pack

## Mục tiêu

Biến bất kỳ intake nào (bài viết dán vào hoặc đã có trong hội thoại, file, log, output của bước trước, hoặc một câu yêu cầu) thành hai thứ: một **Kịch bản Media** ngắn cho nội dung và một **Prompt Pack**, trong đó mỗi ảnh có một prompt tiếng Anh liền mạch để người dùng dán thẳng vào công cụ tạo ảnh họ đang dùng. Skill không tạo ảnh và không gọi dịch vụ tạo ảnh. Ảnh đầu ra phải có ý đồ, không có dấu hiệu đồ chế hàng loạt.

Khi ảnh đã tạo ra chưa đạt, skill chẩn đoán lỗi nằm ở phần nào của prompt và trả về prompt đã sửa cho đúng ảnh đó.

## Tiêu chí thành công

Khi lập pack:
- Kịch bản Media nêu nội dung nói về gì (1–3 câu), mục tiêu, đối tượng, kênh đăng, hướng hình ảnh và danh sách vị trí ảnh. Mỗi vị trí có mục đích, loại ảnh, tỉ lệ khung và mức ưu tiên (FR-004, FR-005).
- Số ảnh được đề xuất theo độ dài và cấu trúc nội dung; số người dùng đã nêu thì được tôn trọng (FR-006).
- Mỗi ảnh có đúng một khối prompt liền mạch, tiếng Anh, dán được ngay: không placeholder, không tên khe, không preset ID, không cú pháp riêng của công cụ, không buzzword chất lượng. Tỉ lệ và ràng buộc nằm trong chính prompt (FR-007, FR-010, FR-012).
- Trước khi xuất, đối chiếu từng prompt với quy tắc viết trong `references/anti-slop.md` mục 2: tỉ lệ khung viết bằng lời, 30–80 từ, nguồn sáng thật, hai hoặc ba vật đời thường với ảnh đời thường, tối đa một cụm camera và một khuyết điểm.
- Các ảnh trong pack nhất quán về màu và phong cách, nhưng khác nhau về người, nơi chốn, giờ hoặc mùa và góc khung (FR-011).
- Mục Reference chỉ có ở ảnh cần người dùng đính kèm tệp. Khi có, nêu tệp cần có, vai trò từng tệp, và prompt gọi đúng "Image N = …" (FR-008).
- Thiếu thông tin thì tự giả định hợp lý và ghi ở mục Giả định (FR-003). Chỉ hỏi khi thiếu thông tin làm đổi kết quả: tối đa 3 câu ngắn, mỗi câu kèm đề xuất mặc định (FR-002).
- Intake là log nhiều chủ đề: nói rõ đã chọn phần nào để làm media.
- Không tìm thấy nội dung trong context: nói rõ, xin nội dung hoặc đường dẫn, không bịa.
- Không tự thêm ảnh mockup sản phẩm. Mockup chỉ lập khi người dùng yêu cầu đúng vị trí đó (FR-020).

Khi sửa prompt:
- Chẩn đoán từng lỗi nhìn thấy trong ảnh ra nguyên nhân nằm ở đoạn nào của prompt, dựa trên bảng dấu hiệu và checklist QC trong `references/anti-slop.md` (FR-015, FR-021).
- Chỉ trả prompt của ảnh bị phàn nàn. Giữ phần đã ổn và phong cách chung của pack (FR-016).
- Kèm 1–3 dòng "Đã đổi" nêu thay đổi nhắm vào lỗi nào.
- Nếu xem được ảnh kết quả, nhận diện dấu hiệu slop trực tiếp từ ảnh; nếu không, dựa vào mô tả lỗi của người dùng.

## Đầu ra

Khi lập pack, theo thứ tự này (mẫu rút gọn):

```markdown
## Kịch bản Media
**Nội dung:** <1–3 câu>
**Mục tiêu:** … · **Đối tượng:** … · **Kênh:** …
**Hướng hình ảnh:** <phong cách chung, thương hiệu nếu có>
**Giả định:** <chỉ khi có>

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Ưu tiên |
|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | … | hero | 16:9 | cao |

## Prompt Pack
<ghi chú phong cách chung, 1–2 câu>

### Ảnh 1 — Hero
```text
<một prompt liền mạch, tiếng Anh>
```
**Reference:** <chỉ khi cần tệp đính kèm: tệp gì, vai trò gì>
```

Khi sửa một ảnh:

```markdown
**Chẩn đoán:** <lỗi trong ảnh → nguyên nhân trong prompt>
```text
<prompt đã sửa>
```
**Đã đổi:** <1–3 dòng>
```

Quy tắc đầu ra:
- Mỗi hàng bảng khớp đúng một mục "### Ảnh N". Khối prompt nằm trong code block để copy một lần.
- Giải thích và Kịch bản Media theo ngôn ngữ người dùng. Khối prompt luôn tiếng Anh; chữ hiện trong ảnh giữ đúng ngôn ngữ người dùng yêu cầu.
- Không bắt buộc hiển thị tên khe hay preset ID. Ghi chú phụ (alt text, caption) chỉ thêm khi giúp người dùng dùng ảnh tốt hơn.
- Khi người dùng yêu cầu lưu và harness cho phép ghi file, lưu cả Kịch bản Media và Prompt Pack thành một file Markdown, đặt tên gợi ý `prompt-pack-<chủ-đề>.md`.

## Tri thức

Đọc các file trong `references/` khi cần; đường dẫn tương đối từ thư mục skill:
- `references/anti-slop.md`: luôn đọc trước khi viết prompt. Có quy tắc viết prompt, bảng dấu hiệu ảnh AI, mục mockup và checklist QC.
- `references/image-types.md`: khi lập Kịch bản Media. Có loại ảnh, tỉ lệ thường dùng, rủi ro chữ và số ảnh theo độ dài bài.
- `references/presets.md`: khi chọn hoặc khi người dùng gọi tên phong cách. Có 24 preset nhóm R, S, C và bảng slot đa dạng.
- `references/example-pack.md`: để xem chuẩn đầu ra và một ví dụ sửa prompt.

Tri thức là điểm tựa để tự chọn và phối, không phải biểu mẫu bắt buộc. Người dùng có thể đổi phong cách bằng lời.

## Ranh giới

- Không tạo ảnh, không gọi hay hướng dẫn gọi dịch vụ tạo ảnh. Đầu ra chỉ là văn bản copy được.
- Không viết adapter, ghi chú hay cú pháp riêng cho một công cụ tạo ảnh.
- Mockup sản phẩm chỉ khi người dùng yêu cầu đúng vị trí đó. Khi lập, mục Reference bắt buộc là ảnh sản phẩm hoặc thiết kế thật; prompt chỉ tạo bối cảnh, người và ánh sáng, không vẽ lại thiết kế hay logo; kèm ghi chú: ghép thiết kế thật sau và giữ metadata AI (C2PA, IPTC).
- Không mô tả giả mạo người thật hay thương hiệu thật. Nếu cần đúng diện mạo, yêu cầu ảnh thật qua mục Reference.
- Nội dung nhạy cảm (y tế, tài chính, trẻ em): chọn hướng hình ảnh không gây hiểu lầm hay gợi ý sai sự thật.
- Có brand guideline hoặc brand kit trong context: áp màu, phong cách và quy tắc thương hiệu vào toàn pack.
- Không đưa nội dung của người dùng ra ngoài harness đang dùng.
