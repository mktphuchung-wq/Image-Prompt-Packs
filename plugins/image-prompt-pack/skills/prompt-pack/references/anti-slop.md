# Chống slop: mục tiêu, quy tắc viết prompt, dấu hiệu nhận dạng, QC

Tài liệu tham chiếu của skill `prompt-pack`. Đọc trước khi viết bất kỳ prompt ảnh nào, và khi chẩn đoán ảnh lỗi.

## 1. Mục tiêu

Mục tiêu là **ảnh có ý đồ, không có dấu hiệu đồ chế hàng loạt**. Không phải "không ai nhận ra là AI". Người xem không ghét ảnh AI tự thân; họ ghét ảnh trông rẻ, lạ, vô hồn. Gốc của slop là thiên hướng thẩm mỹ mặc định của model (da bóng, bokeh khắp nơi, màu poster, bố cục sạch), nên cách chữa hiệu quả là đưa thông tin cụ thể về đời thực (thiết bị, nguồn sáng, chất liệu, hành động đang diễn ra, một khuyết điểm thật), không phải thêm từ khóa chất lượng.

## 2. Quy tắc viết prompt (chạy được trên mọi công cụ)

Khung tư duy nội bộ, không hiển thị cho người dùng, gồm 7 khe: FORMAT (loại ảnh và nơi dùng), SUBJECT (người hoặc vật, hành động đang diễn ra, cách cầm vật), SETTING (nơi chốn cụ thể và 2–3 vật đời thường), CAMERA (một thiết bị hoặc thời đại), LIGHT (nguồn sáng thật và hướng), REALISM (một khuyết điểm cụ thể), CONSTRAINTS (chữ, số lần xuất hiện, điều phải giữ nguyên). Viết thành một đoạn liền mạch; mỗi khe tối đa một câu.

- Viết bằng tiếng Anh, khoảng 30–80 từ cho đa số ảnh; dài hơn khi cảnh phức tạp.
- Ý quan trọng nhất (chủ thể và việc đang làm) đặt ở đầu prompt.
- Diễn đạt khẳng định: "sharp focus throughout" thay cho "no blur". Chỉ dùng phủ định khi không có cách khẳng định: "not retouched, not cinematic" cho ảnh thật, "no other text" cho chữ.
- Không dùng buzzword chất lượng: 8K, masterpiece, ultra-detailed, stunning, flawless, hyperrealistic.
- Thay tính từ cảm xúc bằng chi tiết cụ thể: chủ thể đang làm gì giữa chừng, chất liệu (cotton jersey, wool tweed), nơi chốn có 2–3 vật đời thường (ly trà uống dở, dây sạc cuộn, tờ giấy in).
- Nêu nguồn sáng thật và hướng sáng: "soft window light from the left".
- Tối đa **một** chỉ dẫn camera hoặc thời đại thiết bị: "shot on a recent smartphone", "35mm film look". Không chồng nhiều cụm camera.
- Tối đa **một** khuyết điểm cụ thể: "a loose thread on the cuff", "slight motion blur on the hand". Không dùng "natural imperfections" chung chung.
- Ảnh thật: nói rõ "photo", kèm "unposed, not retouched, not cinematic".
- Tỉ lệ khung viết bằng lời: "vertical 4:5 frame", "horizontal 16:9 frame".
- Chữ trong ảnh đặt trong ngoặc kép và nêu số lần xuất hiện: `the word "FRESH" appears once`. Chữ dài hoặc nhiều dòng không đưa vào ảnh; chừa vùng trống ("clean empty area across the top third") để thêm chữ sau.
- Tham chiếu gọi theo số và vai trò: "Image 1 = product reference".
- Cách cầm vật phải cụ thể: "thumb on top, fingers wrapped around the handle".
- Không dùng tham số, ký hiệu hay cú pháp của một công cụ cụ thể.

## 3. Mười một dấu hiệu nhận dạng ảnh AI và cách đối phó

| Dấu hiệu | Vì sao xảy ra | Đối phó trong prompt |
|---|---|---|
| Da sáp, mịn, không lỗ chân lông | Model học từ ảnh đã retouch; các từ như "flawless", "perfect skin" làm nặng thêm | "visible skin texture, pores, uneven skin tone, not retouched", nói một lần |
| Bokeh nền mờ mọi cảnh | Bokeh bị học như dấu hiệu "đắt tiền" | "deep focus, background in sharp detail" cho cảnh đời thường |
| Màu cam-teal hoặc ngả vàng | Thiên hướng từ poster phim và preset màu | Chỉ định màu theo vật ("white walls, neutral daylight"); gắn thời đại máy ảnh hoặc film stock |
| Bố cục quá sạch, chủ thể căn giữa | Model ưu tiên bố cục chuẩn (suy luận, chưa có số đo) | Thêm vật lộn xộn cụ thể; "slightly off-center"; góc cầm tay |
| Ánh sáng studio dù cảnh đời thường | Mặc định "cinematic", "pleasant" | Nêu nguồn sáng thật và hướng; "not cinematic" |
| Tay cầm vật sai, ngón dính vật | Tương tác vật lý khó | Mô tả cách cầm cụ thể; sinh nhiều biến thể rồi kiểm tra khi phóng to |
| Chữ méo, in nổi trên vải | Chữ trong cảnh phức tạp còn yếu | Chữ trong ngoặc kép, nêu số lần; chữ quan trọng để thiết kế thật ghép sau |
| Vải, tóc, đường may vô nghĩa | Model chưa hiểu cấu trúc may | Nêu chất liệu và kiểu may cụ thể; kiểm tra khi nhìn gần |
| Ánh sáng nền lệch với chủ thể | Ghép cảnh không vật lý | Một nguồn sáng duy nhất, nêu hướng; bóng đổ khớp nhau |
| Quá nét, bão hòa | Buzzword không mang thông tin thị giác | Xóa buzzword; thay bằng camera, chất liệu và một khuyết điểm |
| Khuôn mặt AI lặp lại | Thiên hướng trung bình của model; cả pack thành "một khuôn mặt, một phòng" | Đổi tuổi, nền, tóc, trang phục, nơi chốn, giờ; dùng ảnh tham chiếu thật khi cần |

Ghi chú: "bố cục quá sạch" là suy luận hợp lý nhưng chưa có số đo; coi là gợi ý, không phải quy tắc tuyệt đối.

## 4. Đa dạng trong một pack (FR-011)

- Giữ thống nhất: bảng màu chung, phong cách chung và thương hiệu nếu có trong context (brand guideline áp vào toàn pack).
- Đổi giữa các ảnh: người, nơi chốn, giờ hoặc mùa, góc khung. Chọn giá trị từ bảng slot ở `presets.md`; không lặp cùng giá trị trong một pack.
- Cảnh báo: khuyết điểm cố ý lặp lại (grain đều, lens flare giả, "imperfect") cũng thành một mẫu nhận biết. Xoay vòng preset và không áp cùng một khuyết điểm cho mọi ảnh.

## 5. Ảnh mockup sản phẩm (chỉ khi người dùng yêu cầu)

- Chỉ tạo khi người dùng báo đúng vị trí ảnh cần mockup. Không tự đề xuất, không tự thêm vào pack.
- Mục Reference bắt buộc: ảnh sản phẩm hoặc thiết kế thật (logo, hình in) để AI tham chiếu.
- Prompt chỉ yêu cầu AI tạo bối cảnh, người và ánh sáng. Không yêu cầu vẽ lại thiết kế hay logo; chừa vùng trống nơi thiết kế thật sẽ được ghép vào.
- Ghi chú kèm theo: ghép thiết kế thật sau khi tạo; giữ nguyên metadata AI (C2PA, IPTC) khi xuất file, không xóa khi nén hay đăng.
- Trước khi đăng lên trang bán hàng, kiểm tra chính sách hiện hành của nền tảng về ảnh AI; không dựa vào thông tin chưa xác minh.

## 6. Checklist QC đạt/không đạt (không chấm điểm)

Dùng khi chẩn đoán ảnh lỗi hoặc khi người dùng xin. Không bắt buộc xuất kèm mỗi pack. Mỗi mục chỉ đạt hoặc không đạt.

Mục chung cho mọi ảnh:
- [ ] Da có texture; kiểm vùng cổ và tay.
- [ ] Tay cầm vật đúng cấu trúc; đếm ngón khi phóng to.
- [ ] Chữ đúng chính tả, không méo, không nổi trên vải.
- [ ] Một nguồn sáng hợp lý; bóng đổ khớp nhau.
- [ ] Nền không bokeh vô cớ; có vật đời thường.
- [ ] Màu không ngả cam-teal hoặc vàng theo mặc định.
- [ ] Không lặp khuôn mặt đã dùng trong pack.

Thêm cho ảnh mockup:
- [ ] Sản phẩm và thiết kế đúng thật, không bị vẽ lại hay bịa.
- [ ] Metadata AI còn nguyên ở file xuất ra.
