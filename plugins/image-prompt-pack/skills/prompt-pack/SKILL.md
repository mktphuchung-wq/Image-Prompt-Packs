---
name: prompt-pack
description: "Turns any content, log, chat history or short request into a media plan and a copy-ready, anti-slop image prompt pack (one English prompt per image). Long intakes get a quick brief card with defaults (visual direction, text in image, mockup, image count) before the pack; each image gets a text-in-image mode; prompts are self-checked against staged, over-clean shots. Also rewrites a prompt when the generated image looks like AI slop or staged. Does not generate images. Use for 'prompt ảnh', 'làm ảnh cho bài này', 'image prompts', 'media plan', 'ảnh có chữ', 'hero có tiêu đề', 'ảnh bị AI quá', 'ảnh như sắp đặt', 'sửa prompt ảnh'."
---

# Prompt Pack

## Mục tiêu

Biến bất kỳ intake nào (bài viết dán vào hoặc đã có trong hội thoại, file, log, output của bước trước, hoặc một câu yêu cầu) thành hai thứ: một **Kịch bản Media** ngắn cho nội dung và một **Prompt Pack**, trong đó mỗi ảnh có một prompt tiếng Anh liền mạch để người dùng dán thẳng vào công cụ tạo ảnh họ đang dùng. Skill không tạo ảnh và không gọi dịch vụ tạo ảnh. Ảnh đầu ra phải có ý đồ, không có dấu hiệu đồ chế hàng loạt: đời thường có vật lạc chủ đề và dấu vết người, không dàn dựng kiểu showroom.

Khi ảnh đã tạo ra chưa đạt, skill chẩn đoán lỗi nằm ở phần nào của prompt và trả về prompt đã sửa cho đúng ảnh đó.

## Tiêu chí thành công

Khi lập pack:
- Kịch bản Media nêu nội dung nói về gì (1–3 câu), mục tiêu, đối tượng, kênh đăng, hướng hình ảnh và danh sách vị trí ảnh. Mỗi vị trí có mục đích, loại ảnh, tỉ lệ khung, hướng, khung hình, độ cao máy, ánh sáng, thời tiết hoặc giờ, người và chế độ chữ (FR-004, FR-005).
- Số ảnh được đề xuất theo độ dài và cấu trúc nội dung; số người dùng đã nêu thì được tôn trọng (FR-006).
- Mỗi ảnh có đúng một khối prompt liền mạch, tiếng Anh, dán được ngay: không placeholder, không tên khe, không preset ID, không cú pháp riêng của công cụ, không buzzword chất lượng. Tỉ lệ và ràng buộc nằm trong chính prompt (FR-007, FR-010, FR-012).
- Trước khi xuất, mỗi prompt qua tự kiểm trong `references/anti-slop.md` mục 2: 30–80 từ, kể một khoảnh khắc, tối đa 5 vật gọi tên, không số chẵn hay bố trí đối xứng, ảnh đời thường có một vật lạc chủ đề và một dấu vết người, không từ cấm đứng một mình, ảnh không chữ có câu chặn chữ tự thêm (FR-101…FR-106). Prompt vượt 80 từ chỉ khi cảnh có nhiều chủ thể, và lý do ghi trong Kịch bản Media.
- Các ảnh trong pack nhất quán về màu và phong cách, nhưng đa dạng theo bảng Kịch bản Media (các cột Hướng, Khung, Độ cao máy, Ánh sáng, Thời tiết/giờ, Người, Chữ) và đạt quy tắc đa dạng cấp pack trong `references/anti-slop.md` mục 4 (FR-107, FR-108).
- Mỗi ảnh có đúng một chế độ chữ, ghi ở cột Chữ: 0 không chữ, 1 chữ trong cảnh, 2 chèn chữ sau, 3 AI vẽ chữ, 4 hai lượt. Hero, ảnh chia sẻ và thumbnail mặc định chèn chữ sau; ảnh khác không chữ; chế độ 3 và 4 chỉ khi người dùng chọn. Quy tắc từng chế độ, tiếng Việt có dấu và cách chữa lỗi chữ nằm trong `references/text-in-image.md` (FR-117…FR-123).
- Chữ trong ảnh không thay H1 và không thay alt text; ảnh có chữ phục vụ web vẫn kèm gợi ý alt mô tả (FR-125).
- Mục Reference chỉ có ở ảnh cần người dùng đính kèm tệp. Khi có, nêu tệp cần có, vai trò từng tệp, và prompt gọi đúng "Image N = …" (FR-008).
- Intake là log nhiều chủ đề: nói rõ đã chọn phần nào để làm media.
- Không tìm thấy nội dung trong context: nói rõ, xin nội dung hoặc đường dẫn, không bịa.
- Không tự thêm ảnh mockup sản phẩm. Mockup chỉ lập khi người dùng chọn "có" ở mục 3 của Chốt nhanh hoặc tự yêu cầu đúng vị trí đó (FR-020, FR-126…FR-128).

Cách hỏi trước khi viết pack (Chốt nhanh):
- Bài dài (khoảng 800 từ trở lên, hoặc từ 4 mục lớn trở lên) hoặc pack dự kiến từ 4 ảnh: phản hồi đầu gồm Kịch bản Media và khối Chốt nhanh đặt trên cùng, không có prompt nào, rồi dừng chờ một câu trả lời (FR-110).
- Khối Chốt nhanh có tối đa 4 mục: hướng hình, chữ trong ảnh, sản phẩm (chỉ khi intake nhắc sản phẩm hoặc có chỗ chờ), số ảnh-tỉ lệ-kênh. Mỗi mục có một mặc định và tối đa 3 lựa chọn, mô tả bằng kết quả nhìn thấy. Mục intake đã quyết thì bỏ; không còn mục nào thì không có khối (FR-111, FR-112, FR-126).
- Hướng hình do model chọn theo loại bài và kênh, ghi trong Chốt nhanh kèm một câu lý do: Đời thường, Biên tập/chuyên nghiệp (tạp chí, thời trang) hoặc Minh họa. Một pack có thể phối hướng theo từng ảnh (FR-116).
- Yêu cầu 1–3 ảnh, người dùng nói "đưa luôn", hoặc không có người để trả lời: xuất pack ngay, khối "Đã dùng mặc định" đặt ở đầu phản hồi thay cho mục Giả định cuối (FR-114).
- Trả lời "ok": xuất pack theo mặc định, không hỏi thêm. Trả lời một phần: mục đã nêu theo lựa chọn, mục còn lại theo mặc định. Đổi một mục sau khi có pack: chỉ viết lại prompt bị ảnh hưởng (FR-113, FR-115).
- Người dùng hỏi việc khác khi đang chờ: không tự xuất pack; khi họ quay lại, giữ khối đã đưa.
- Ở lượt chờ, không có khối prompt nào; mọi câu hỏi nằm trong khối Chốt nhanh, không thành chuỗi câu hỏi riêng.

Khi sửa prompt:
- Chẩn đoán từng lỗi nhìn thấy trong ảnh ra nguyên nhân nằm ở đoạn nào của prompt, dựa trên bảng 15 dấu hiệu và checklist QC trong `references/anti-slop.md` (FR-015, FR-021, FR-109). Prompt sửa cũng phải đạt tiêu chí tự kiểm (FR-106).
- Ảnh có chữ được kiểm bằng QC chữ 7 mục trong `references/text-in-image.md` (FR-124).
- Chỉ trả prompt của ảnh bị phàn nàn. Giữ phần đã ổn và phong cách chung của pack (FR-016).
- Kèm 1–3 dòng "Đã đổi" nêu thay đổi nhắm vào lỗi nào.
- Nếu xem được ảnh kết quả, nhận diện dấu hiệu slop trực tiếp từ ảnh; nếu không, dựa vào mô tả lỗi của người dùng.

## Đầu ra

Lượt chờ (bài dài hoặc từ 4 ảnh), theo thứ tự này. Dừng sau Kịch bản Media, không có prompt:

````markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Hướng hình: <mặc định> (mặc định — <một câu lý do>) · <lựa chọn 2> · <lựa chọn 3>
2. Chữ trong ảnh: <mặc định> · <lựa chọn 2> · <lựa chọn 3>
3. Sản phẩm: <số chỗ và vị trí>. Làm mockup ở đó không? Mặc định: không.
4. Số ảnh: <N> ảnh; <tỉ lệ từng loại>. Giữ nguyên?

## Kịch bản Media
**Nội dung:** <1–3 câu>
**Mục tiêu:** … · **Đối tượng:** … · **Kênh:** …
**Hướng hình ảnh:** <phong cách chung, thương hiệu nếu có>

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | … | hero | 16:9 | Đời thường | toàn cảnh | ngang tầm mắt | lạnh u ám, cửa sổ | sáng mưa | không | 2 chèn chữ sau |
````

Sau "ok", hoặc khi xuất luôn, theo thứ tự này. Khi xuất luôn (1–3 ảnh, "đưa luôn", không có người trả lời), đặt thêm khối ngắn ở đầu phản hồi, mỗi mục đã dùng mặc định một dòng:

````markdown
## Đã dùng mặc định
- Hướng hình: Đời thường, vì <lý do>.
- Chữ: <mặc định>.

## Kịch bản Media
<như trên, bảng đã cập nhật theo câu trả lời>

## Prompt Pack
<ghi chú phong cách chung, 1–2 câu>

### Ảnh 1 — Hero
```text
<một prompt liền mạch, tiếng Anh>
```
**Chữ:** <chỉ với chế độ 2/3/4: vùng trống ở đâu, chuỗi chữ, cảnh báo tiếng Việt>
**Reference:** <chỉ khi cần tệp đính kèm: tệp gì, vai trò gì>
````

Ảnh chế độ 4 (hai lượt) có hai khối prompt. Lượt 2 dùng đúng câu chuẩn và Reference là ảnh lượt 1:

````markdown
### Ảnh 4 — Banner (hai lượt)
```text
<lượt 1: cảnh có vùng trống, không chữ>
```
```text
Image 1 = approved scene. Add the headline only; keep everything else unchanged. <tiêu đề theo quy tắc chế độ 3>
```
**Reference:** lượt 2 cần ảnh tạo từ lượt 1.
````

Khi sửa một ảnh:

````markdown
**Chẩn đoán:** <lỗi trong ảnh → nguyên nhân trong prompt>
```text
<prompt đã sửa>
```
**Đã đổi:** <1–3 dòng>
````

Quy tắc đầu ra:
- Mỗi hàng bảng khớp đúng một mục "### Ảnh N". Khối prompt nằm trong code block để copy một lần.
- Không có mục Giả định ở cuối pack; mặc định đã dùng nằm ở đầu phản hồi.
- Giải thích và Kịch bản Media theo ngôn ngữ người dùng. Khối prompt luôn tiếng Anh; chữ hiện trong ảnh giữ đúng ngôn ngữ người dùng yêu cầu.
- Không bắt buộc hiển thị tên khe hay preset ID. Ghi chú phụ (alt text, caption) chỉ thêm khi giúp người dùng dùng ảnh tốt hơn.
- Prompt nào vượt 80 từ thì ghi lý do ngắn dưới bảng Kịch bản Media.
- Khi người dùng yêu cầu lưu và harness cho phép ghi file, lưu cả Kịch bản Media và Prompt Pack thành một file Markdown, đặt tên gợi ý `prompt-pack-<chủ-đề>.md`.

## Tri thức

Đọc các file trong `references/` khi cần; đường dẫn tương đối từ thư mục skill:
- `references/brief-card.md`: khi lập Kịch bản Media, để quyết định có hỏi không, hỏi mục nào và mặc định là gì.
- `references/anti-slop.md`: luôn đọc trước khi viết prompt. Có quy tắc viết prompt, tự kiểm, từ cấm, bảng 15 dấu hiệu ảnh AI, đa dạng cấp pack, mục mockup và checklist QC.
- `references/text-in-image.md`: khi một ảnh có chế độ chữ khác 0, hoặc khi kiểm ảnh có chữ. Có năm chế độ, quy tắc AI vẽ chữ, tiếng Việt có dấu, hai lượt và QC chữ.
- `references/image-types.md`: khi lập Kịch bản Media. Có loại ảnh, tỉ lệ, hướng gợi ý, chữ mặc định, rủi ro và số ảnh theo độ dài bài.
- `references/presets.md`: khi chọn hoặc khi người dùng gọi tên phong cách. Có 28 preset nhóm R, S, C, E và bảng slot đa dạng.
- `references/example-pack.md`: để xem chuẩn đầu ra, một bài dài đi qua hai lượt, và một ví dụ sửa prompt.

Tri thức là điểm tựa để tự chọn và phối, không phải biểu mẫu bắt buộc. Người dùng có thể đổi phong cách bằng lời.

## Ranh giới

- Không tạo ảnh, không gọi hay hướng dẫn gọi dịch vụ tạo ảnh. Đầu ra chỉ là văn bản copy được.
- Không viết adapter, ghi chú hay cú pháp riêng cho một công cụ tạo ảnh.
- Mockup sản phẩm: khi intake nhắc sản phẩm hoặc có chỗ chờ sản phẩm, Chốt nhanh hỏi ở mục 3 (số chỗ và vị trí), mặc định "không làm mockup". Không chọn, hoặc không trả lời về mục này: pack không có prompt mockup, không có mục "Bonus" hay prompt sản phẩm dưới bất kỳ tên nào. Chọn "có", hoặc người dùng tự yêu cầu đúng vị trí: Reference ảnh sản phẩm thật là bắt buộc; ảnh được gắn nhãn "chờ sản phẩm xác minh"; prompt chỉ tạo bối cảnh, người và ánh sáng, không vẽ lại thiết kế hay logo; kèm ghi chú ghép thiết kế thật sau và giữ metadata AI (C2PA, IPTC). Chi tiết ở `references/anti-slop.md` mục 5.
- Không mô tả giả mạo người thật hay thương hiệu thật. Nếu cần đúng diện mạo, yêu cầu ảnh thật qua mục Reference.
- Nội dung nhạy cảm (y tế, tài chính, trẻ em): chọn hướng hình ảnh không gây hiểu lầm hay gợi ý sai sự thật.
- Có brand guideline hoặc brand kit trong context: áp màu, phong cách và quy tắc thương hiệu vào toàn pack.
- Không đưa nội dung của người dùng ra ngoài harness đang dùng.
