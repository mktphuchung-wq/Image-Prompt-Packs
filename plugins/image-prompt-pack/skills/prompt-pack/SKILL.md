---
name: prompt-pack
description: "Turns any content, log, chat history or short request into a media plan and a copy-ready, anti-slop image prompt pack (one English prompt per image). A brief card with defaults appears only on special cases (text in image, style, special content, new format); hero and share images get a built-in copy space for a headline; each image gets a text-in-image mode; prompts are self-checked against staged, over-clean shots. Also rewrites a prompt when the generated image looks like AI slop or staged. Does not generate images. Use for 'prompt ảnh', 'làm ảnh cho bài này', 'image prompts', 'media plan', 'ảnh có chữ', 'hero có tiêu đề', 'chừa chỗ chữ', 'ảnh bị AI quá', 'ảnh như sắp đặt', 'sửa prompt ảnh'."
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
- Mỗi ảnh có đúng một chế độ chữ, ghi ở cột Chữ: 0 không chữ, 1 chữ trong cảnh, 2 chèn chữ sau, 3 AI vẽ chữ, 4 hai lượt. Hero, ảnh chia sẻ và thumbnail mặc định chèn chữ sau; ảnh khác không chữ; chế độ 3 và 4 chỉ khi người dùng chọn (FR-117, FR-123).
- Ảnh chế độ 2 có bố cục banner với vùng chữ dựng sẵn: chủ thể một phía, vùng chữ phía còn lại, tạo bằng khoảng trống thật, làm mềm hậu cảnh nhẹ hoặc mảng phẳng (Minh họa). Prompt nêu vị trí và tông vùng; ngay dưới prompt có khối Vùng chữ; cột Chữ ghi vị trí, ví dụ "2 chèn chữ sau — 1/3 trái". Chế độ 3 và 4 giữ vùng đó; làm mềm hậu cảnh chỉ trong vùng chữ của chế độ 2, 3, 4 (FR-201…FR-211). Quy tắc chi tiết, tiếng Việt có dấu và cách chữa lỗi chữ nằm trong `references/text-in-image.md`.
- Chữ trong ảnh không thay H1 và không thay alt text; ảnh có chữ phục vụ web vẫn kèm gợi ý alt mô tả (FR-125).
- Mục Reference chỉ có ở ảnh cần người dùng đính kèm tệp. Khi có, nêu tệp cần có, vai trò từng tệp, và prompt gọi đúng "Image N = …" (FR-008).
- Intake là log nhiều chủ đề: nói rõ đã chọn phần nào để làm media.
- Không tìm thấy nội dung trong context: nói rõ, xin nội dung hoặc đường dẫn, không bịa.
- Không tự thêm ảnh mockup sản phẩm. Mockup chỉ lập khi người dùng chọn "có" ở mục Sản phẩm của Chốt nhanh hoặc tự yêu cầu đúng vị trí đó (FR-020, FR-126…FR-128).

Lượt đầu (Chốt nhanh), theo FR-215…FR-220:
- Dừng chờ, không kèm prompt, chỉ khi có ít nhất một trường hợp đặc biệt: (1) Chữ: banner, hero, ảnh chia sẻ hoặc thumbnail mà chưa chốt cách đặt chữ, hoặc tiêu đề chưa chốt; (2) Phong cách: nội dung hợp nhiều hướng hình mà chọn sai sẽ làm lại cả pack; (3) Nội dung đặc biệt: chỗ chờ sản phẩm, người hoặc thương hiệu thật, chủ đề nhạy cảm, số liệu cho infographic, nhiều ngôn ngữ; (4) Format mới lạ: dạng ảnh hoặc tỉ lệ không có trong `references/image-types.md`. Chi tiết ở `references/brief-card.md`. Số ảnh và độ dài bài không là lý do dừng.
- Chốt nhanh tối đa 4 mục. Mục Banner (khi trường hợp 1 kích hoạt) có 4 điểm: (a) tiêu đề và số dòng, (b) cách đặt chữ, (c) vùng chữ và cách tạo, (d) các khung; điểm intake đã chốt thì bỏ. Phong cách, Sản phẩm, Format mới lạ chỉ khi kích hoạt. Mỗi mục nêu lý do kích hoạt, một mặc định và tối đa 3 lựa chọn, mô tả bằng kết quả nhìn thấy, không vẽ sơ đồ ký tự.
- Format các ảnh còn lại chốt qua bảng Kịch bản Media; người dùng sửa theo số dòng, chỉ dòng đó được áp dụng, không hỏi từng ảnh.
- Hướng hình do model chọn theo loại bài và kênh, kèm một câu lý do: Đời thường, Biên tập/chuyên nghiệp hoặc Minh họa (FR-116).
- Không có trường hợp nào, người dùng nói "đưa luôn", hoặc không có người trả lời: xuất pack ngay, khối "Đã dùng mặc định" ở đầu phản hồi.
- Trả lời "ok": xuất pack theo mặc định. Trả lời một phần: mục đã nêu theo lựa chọn, còn lại theo mặc định. Đổi một mục sau pack: chỉ viết lại prompt bị ảnh hưởng. Người dùng hỏi việc khác khi đang chờ: không tự xuất pack. Ở lượt chờ không có khối prompt nào.

Khi sửa prompt:
- Chẩn đoán từng lỗi nhìn thấy trong ảnh ra nguyên nhân nằm ở đoạn nào của prompt, dựa trên bảng 15 dấu hiệu và checklist QC trong `references/anti-slop.md` (FR-015, FR-021, FR-109). Prompt sửa cũng phải đạt tiêu chí tự kiểm (FR-106).
- Ảnh có chữ được kiểm bằng QC chữ 7 mục trong `references/text-in-image.md` (FR-124).
- Chỉ trả prompt của ảnh bị phàn nàn. Giữ phần đã ổn và phong cách chung của pack (FR-016).
- Kèm 1–3 dòng "Đã đổi" nêu thay đổi nhắm vào lỗi nào.
- Nếu xem được ảnh kết quả, nhận diện dấu hiệu slop trực tiếp từ ảnh; nếu không, dựa vào mô tả lỗi của người dùng.

## Đầu ra

Lượt chờ (khi có trường hợp đặc biệt), theo thứ tự này. Dừng sau Kịch bản Media, không có prompt:

````markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Banner (lý do: <trường hợp 1, thấy ở đâu trong bài>)
   a. Tiêu đề: "<tiêu đề, tối đa 6 từ>", 1 dòng (mặc định) · <lựa chọn 2>
   b. Cách đặt chữ: chừa vùng, ảnh cố ý không có chữ, tự thêm tiêu đề bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề · hai lượt
   c. Vùng chữ: <phía và cách tạo> (mặc định — <một câu lý do>) · <lựa chọn 2>
   d. Khung: <các khung> (mặc định theo kênh) · <lựa chọn 2>
2. <Phong cách, Sản phẩm (làm mockup không? mặc định: không) hoặc Format mới lạ: chỉ mục kích hoạt, mỗi mục kèm lý do và mặc định>

## Kịch bản Media
**Nội dung:** <1–3 câu>
**Mục tiêu:** … · **Đối tượng:** … · **Kênh:** …
**Hướng hình ảnh:** <phong cách chung, thương hiệu nếu có>

| # | Ảnh | Vị trí | Mục đích | Loại | Tỉ lệ | Hướng | Khung | Độ cao máy | Ánh sáng | Thời tiết/giờ | Người | Chữ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Hero | Đầu bài | … | hero | 16:9 | Đời thường | toàn cảnh | ngang tầm mắt | lạnh u ám, cửa sổ | sáng mưa | không | 2 chèn chữ sau — 1/3 trái |

Sửa format theo số dòng, ví dụ "ảnh 3 đổi 4:5, bỏ ảnh 5", hoặc trả "ok".
````

Sau "ok", hoặc khi xuất luôn, theo thứ tự này. Khi xuất luôn (không có trường hợp đặc biệt, "đưa luôn", hoặc không có người trả lời), đặt thêm khối ngắn ở đầu phản hồi, mỗi mục đã dùng mặc định một dòng:

````markdown
## Đã dùng mặc định
- Hướng hình: Đời thường, vì <lý do>.
- Chữ: hero chừa vùng chèn tiêu đề ở <vị trí>; ảnh cố ý không có chữ.

## Kịch bản Media
<như trên, bảng đã cập nhật theo câu trả lời>

## Prompt Pack
<ghi chú phong cách chung, 1–2 câu>

### Ảnh 1 — Hero
```text
<một prompt liền mạch, tiếng Anh>
```
**Vùng chữ:** <chỉ với chế độ 2: vị trí · cỡ · cách tạo · tông → màu chữ · lề · số dòng · khi cắt khung>
Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế.
**Chữ:** <chỉ với chế độ 3/4: chuỗi chữ, cảnh báo tiếng Việt>
**Reference:** <chỉ khi cần tệp đính kèm: tệp gì, vai trò gì>
````

Ảnh chế độ 4 (hai lượt) có hai khối prompt. Lượt 2 dùng đúng câu chuẩn và Reference là ảnh lượt 1:

````markdown
### Ảnh 4 — Banner (hai lượt)
```text
<lượt 1: prompt chế độ 2 nguyên văn, có vùng chữ>
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
- `references/brief-card.md`: khi lập Kịch bản Media, để quyết định có dừng không (bốn trường hợp đặc biệt), nội dung mục Banner và mặc định.
- `references/anti-slop.md`: luôn đọc trước khi viết prompt. Có quy tắc viết prompt, tự kiểm, từ cấm, bảng 15 dấu hiệu ảnh AI, đa dạng cấp pack, mục mockup và checklist QC.
- `references/text-in-image.md`: khi một ảnh có chế độ chữ khác 0, hoặc khi kiểm ảnh có chữ. Có năm chế độ, cách dựng vùng chữ và khối Vùng chữ, quy tắc AI vẽ chữ, tiếng Việt có dấu, hai lượt và QC chữ.
- `references/image-types.md`: khi lập Kịch bản Media. Có loại ảnh, tỉ lệ, hướng gợi ý, chữ mặc định, rủi ro và số ảnh theo độ dài bài.
- `references/presets.md`: khi chọn hoặc khi người dùng gọi tên phong cách. Có 28 preset nhóm R, S, C, E và bảng slot đa dạng.
- `references/example-pack.md`: để xem chuẩn đầu ra, một bài dài đi qua hai lượt, và một ví dụ sửa prompt.

Tri thức là điểm tựa để tự chọn và phối, không phải biểu mẫu bắt buộc. Người dùng có thể đổi phong cách bằng lời.

## Ranh giới

- Không tạo ảnh, không gọi hay hướng dẫn gọi dịch vụ tạo ảnh. Đầu ra chỉ là văn bản copy được.
- Không viết adapter, ghi chú hay cú pháp riêng cho một công cụ tạo ảnh.
- Mockup sản phẩm: khi intake nhắc sản phẩm hoặc có chỗ chờ sản phẩm, mục Sản phẩm của Chốt nhanh hỏi (số chỗ và vị trí), mặc định "không làm mockup". Không chọn, hoặc không trả lời về mục này: pack không có prompt mockup, không có mục "Bonus" hay prompt sản phẩm dưới bất kỳ tên nào. Chọn "có", hoặc người dùng tự yêu cầu đúng vị trí: Reference ảnh sản phẩm thật là bắt buộc; ảnh được gắn nhãn "chờ sản phẩm xác minh"; prompt chỉ tạo bối cảnh, người và ánh sáng, không vẽ lại thiết kế hay logo; kèm ghi chú ghép thiết kế thật sau và giữ metadata AI (C2PA, IPTC). Chi tiết ở `references/anti-slop.md` mục 5.
- Không mô tả giả mạo người thật hay thương hiệu thật. Nếu cần đúng diện mạo, yêu cầu ảnh thật qua mục Reference.
- Nội dung nhạy cảm (y tế, tài chính, trẻ em): chọn hướng hình ảnh không gây hiểu lầm hay gợi ý sai sự thật.
- Có brand guideline hoặc brand kit trong context: áp màu, phong cách và quy tắc thương hiệu vào toàn pack.
- Không đưa nội dung của người dùng ra ngoài harness đang dùng.
