# Feature Specification: Image Prompt Pack Plugin

**Feature Branch**: `mktphuchung-wq/Feature`

**Created**: 2026-11-18

**Status**: Draft

**Input**: User description: "Tạo một Plugin chuyên tạo Prompt Pack tạo ảnh cho người dùng dựa vào bất kỳ intake nào của họ. Lý do: Người dùng thường mất nhiều thời gian, phân tích content, chỗ nào cần làm hình ảnh, ảnh dạng gì, trông như thế nào, sau đó tạo ảnh phải xử lý sao cho chân thật, không bị Slop. Vấn đề: Mất thời gian, phải nghĩ prompt, phải sửa output ảnh cho prompt chưa tốt. Giải pháp mong muốn: Plugin đọc log, lịch sử, output trước đó hoặc yêu cầu của user, tạo kịch bản media cho content (Bài viết này là gì, cần làm media kiểu gì, tạo bao nhiêu hình, format gì, chất lượng thế nào) và đưa lại prompt cho người dùng (không tự tạo ảnh) trong prompt có các trường như reference tham chiếu, các template, preset cấu hình trước trong plugin để tạo ảnh chất lượng hơn."

## Clarifications

### Session 2026-11-18

- Q: Với mỗi ảnh, prompt trả về cho người dùng nên trình bày dạng nào? → A: Mỗi ảnh là một prompt
  liền mạch, copy dùng ngay. Model tự đọc plugin (khung, preset, quy tắc chống slop) và tự chủ áp
  dụng bên trong prompt, không bắt buộc hiển thị khe/trường cấu trúc. Chỉ ghi rõ Reference khi ảnh
  cần tệp đính kèm.
- Q: Plugin có viết prompt riêng/kèm ghi chú theo từng công cụ tạo ảnh không? → A: Không phân biệt
  công cụ. Mặc định một prompt chung chạy tốt trên mọi công cụ tạo ảnh phổ biến; plugin không kèm
  adapter hay ghi chú theo công cụ.
- Q: Bản đầu tiên kèm những nhóm preset nào? → A: Cả ba nhóm từ thư viện nghiên cứu: R (12 preset
  ảnh thật đời sống), S (8 phong cách thủ công cho minh họa), C (4 cách giữ nhân vật nhất quán);
  ghi nhãn v0.1 chưa test.
- Q: Với ảnh có sản phẩm/thiết kế/logo thật, có bắt buộc quy tắc trung thực sản phẩm không? → A: Có
  (Reference ảnh sản phẩm thật + AI chỉ tạo bối cảnh/người/ánh sáng + ghi chú ghép thiết kế thật và
  giữ metadata AI), nhưng plugin chỉ tạo prompt ảnh mockup sản phẩm khi người dùng báo vị trí đó cần
  mockup; không tự đề xuất.
- Q: Bản đầu tiên được coi là đạt chuẩn chống slop khi qua phép kiểm nào? → A: Cả hai: blind test
  nội bộ (5 người, preset đạt khi ≥4/5 "dùng được" và "không thấy đồ chế hàng loạt") và mỗi ảnh mẫu
  qua đủ checklist QC đạt/không đạt.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Từ nội dung có sẵn ra Prompt Pack dùng ngay (Priority: P1)

Người làm content (writer, SEO, marketer) vừa có một bài viết/nội dung — dán trực tiếp, trỏ tới
file, hoặc nó đã nằm sẵn trong lịch sử hội thoại/output trước đó. Họ gọi plugin. Plugin tự hiểu
nội dung là gì, quyết định cần những ảnh nào, rồi trả về một **Kịch bản Media** ngắn và một
**Prompt Pack** gồm prompt cho từng ảnh, đã áp sẵn template/preset chống slop. Người dùng copy
prompt sang công cụ tạo ảnh họ đang dùng.

**Why this priority**: Đây là toàn bộ giá trị cốt lõi — bỏ khâu phân tích content và nghĩ prompt.
Chỉ riêng story này đã là một MVP hoàn chỉnh.

**Independent Test**: Đưa vào một bài blog ~1.500 từ, không kèm hướng dẫn gì thêm. Kiểm tra đầu ra
có Kịch bản Media (tóm tắt nội dung, danh sách vị trí cần ảnh, số lượng, loại, định dạng, mức chất
lượng) và mỗi vị trí có một prompt đầy đủ trường, dán thẳng vào công cụ tạo ảnh được.

**Acceptance Scenarios**:

1. **Given** người dùng dán một bài viết hoàn chỉnh, **When** họ yêu cầu tạo prompt pack, **Then**
   plugin trả về Kịch bản Media nêu rõ bài viết nói về gì, mục tiêu, đối tượng, và danh sách vị trí
   đặt ảnh kèm lý do, loại ảnh, tỉ lệ khung hình, mức chất lượng.
2. **Given** Kịch bản Media đã có, **When** plugin xuất Prompt Pack, **Then** mỗi ảnh có một prompt
   liền mạch dán thẳng vào công cụ tạo ảnh là dùng được, không cần sửa hay ghép thêm; mục Reference
   chỉ xuất hiện ở ảnh cần tệp đính kèm.
3. **Given** nội dung đã có sẵn trong lịch sử hội thoại hoặc là output của bước trước,
   **When** người dùng chỉ nói "làm prompt ảnh cho bài này", **Then** plugin tự lấy đúng nội dung
   đó từ context mà không bắt người dùng dán lại.
4. **Given** bất kỳ đầu vào nào, **When** plugin hoàn tất, **Then** plugin KHÔNG tự tạo ảnh, chỉ
   trả về văn bản.
5. **Given** bài viết có nhắc tới sản phẩm nhưng người dùng không yêu cầu mockup, **When** plugin
   lập Kịch bản Media, **Then** plugin không tự thêm vị trí ảnh mockup sản phẩm.

---

### User Story 2 - Yêu cầu ngắn hoặc intake lộn xộn (Priority: P2)

Người dùng không có bài viết hoàn chỉnh — chỉ có một câu yêu cầu ("cần 3 ảnh cho landing page
bán áo hoodie"), một đoạn log làm việc, ghi chú rời rạc, hoặc một brief. Plugin vẫn dựng được Kịch
bản Media hợp lý, nêu rõ giả định đã dùng, và chỉ hỏi lại khi thiếu thông tin thật sự làm đổi kết
quả.

**Why this priority**: Mở rộng "bất kỳ intake nào" — thực tế phần lớn yêu cầu không đến từ bài viết
sạch sẽ. Phụ thuộc vào khả năng của Story 1 nhưng test độc lập được.

**Independent Test**: Đưa vào một câu yêu cầu một dòng và, riêng biệt, một đoạn log hội thoại dài
lẫn nhiều chủ đề. Kiểm tra cả hai đều ra Kịch bản Media + Prompt Pack hợp lý, có mục giả định.

**Acceptance Scenarios**:

1. **Given** yêu cầu chỉ một câu, **When** plugin xử lý, **Then** plugin đưa ra Kịch bản Media với
   các giả định được ghi rõ (đối tượng, kênh đăng, phong cách) và Prompt Pack đầy đủ.
2. **Given** intake là log/lịch sử dài có nhiều chủ đề, **When** plugin xử lý, **Then** plugin xác
   định đúng nội dung cần làm media và nói rõ nó đã chọn phần nào.
3. **Given** thiếu một thông tin làm đổi hẳn kết quả (ví dụ không rõ ảnh cho sản phẩm thật hay minh
   họa ý tưởng), **When** plugin xử lý, **Then** plugin hỏi tối đa vài câu ngắn, có đề xuất mặc định,
   thay vì đoán sai hoặc hỏi dồn dập.

---

### User Story 3 - Sửa prompt khi ảnh ra chưa đạt (Priority: P3)

Người dùng đã tạo ảnh từ prompt và kết quả bị lỗi (trông "AI", da nhựa, tay sai, chữ vỡ, bố cục
chung chung, sai sản phẩm…). Họ mô tả lỗi hoặc đưa ảnh kết quả lại. Plugin chẩn đoán nguyên nhân từ
phía prompt và trả về prompt đã sửa cho đúng ảnh đó, giữ nguyên các phần đã ổn.

**Why this priority**: Giải quyết nỗi đau "phải sửa output ảnh cho prompt chưa tốt". Có giá trị
riêng ngay cả với prompt không do plugin tạo ra.

**Independent Test**: Đưa một prompt kèm mô tả lỗi "ảnh trông như stock AI, da quá mịn". Kiểm tra
plugin trả về prompt mới có thay đổi nhắm đúng lỗi và giải thích ngắn đã đổi gì.

**Acceptance Scenarios**:

1. **Given** một prompt và mô tả lỗi của ảnh, **When** người dùng yêu cầu sửa, **Then** plugin trả
   về prompt đã chỉnh, kèm 1–3 dòng giải thích thay đổi nhắm vào lỗi nào.
2. **Given** người dùng gửi kèm ảnh kết quả và harness có khả năng xem ảnh, **When** yêu cầu sửa,
   **Then** plugin tự nhận diện các dấu hiệu slop trong ảnh và sửa prompt tương ứng.
3. **Given** một Prompt Pack nhiều ảnh, **When** người dùng chỉ phàn nàn về ảnh số 2, **Then** plugin
   chỉ sửa prompt ảnh số 2 và giữ phong cách thống nhất với các ảnh còn lại.

---

### User Story 4 - Cài đặt và cập nhật qua marketplace (Priority: P4)

Người dùng thêm link marketplace (Git repo) vào harness đang dùng, cài plugin, và sau này cập nhật
lên bản mới bằng thao tác cập nhật chuẩn của harness — không copy file thủ công.

**Why this priority**: Điều kiện để phân phối cho team; không tạo ra giá trị nội dung nhưng bắt buộc
trước khi dùng rộng.

**Independent Test**: Trên một máy sạch, thêm link marketplace, cài plugin, gọi plugin với một intake
mẫu; sau đó phát hành bản mới và kiểm tra người dùng cập nhật được bằng một thao tác.

**Acceptance Scenarios**:

1. **Given** máy chưa có plugin, **When** người dùng thêm link marketplace và cài, **Then** plugin
   sẵn sàng dùng mà không cần cấu hình thêm.
2. **Given** có bản mới được phát hành, **When** người dùng chạy thao tác cập nhật của harness,
   **Then** plugin lên đúng phiên bản mới và người dùng xem được thay đổi chính.

---

### Edge Cases

- Intake quá ngắn hoặc mơ hồ (chỉ "làm ảnh cho bài này" khi không có bài nào trong context):
  plugin nói rõ không tìm thấy nội dung và xin nội dung/đường dẫn, không bịa nội dung.
- Nội dung rất dài (nhiều nghìn từ, nhiều phần): plugin đề xuất số lượng ảnh hợp lý theo cấu trúc,
  không sinh ảnh cho mọi đoạn; người dùng có thể yêu cầu tăng/giảm.
- Người dùng đã nêu số ảnh hoặc tỉ lệ: plugin tôn trọng các ràng buộc đó thay vì mặc định của
  mình. Người dùng nêu tên công cụ tạo ảnh: prompt vẫn ở dạng chung (FR-012).
- Ảnh cần chữ trong ảnh (infographic, thumbnail có tiêu đề): plugin cảnh báo rủi ro chữ vỡ và đề
  xuất cách an toàn (chữ ngắn, hoặc để trống vùng chữ để thêm sau).
- Nội dung liên quan người thật hoặc thương hiệu thật: plugin tránh prompt mô tả giả mạo người
  thật; nếu cần đúng diện mạo thì yêu cầu ảnh thật qua mục Reference.
- Người dùng báo một vị trí cần mockup sản phẩm: áp quy tắc trung thực sản phẩm (FR-020).
- Nội dung nhạy cảm (y tế, tài chính, trẻ em): plugin chọn hướng hình ảnh phù hợp, tránh hình gây
  hiểu lầm hoặc gợi ý sai sự thật.
- Có sẵn brand guideline/brand kit trong context: plugin áp màu, phong cách, quy tắc thương hiệu vào
  toàn bộ pack.
- Intake ở ngôn ngữ khác tiếng Việt: Kịch bản Media theo ngôn ngữ người dùng; prompt ảnh vẫn bằng
  tiếng Anh; chữ cần hiện trong ảnh giữ đúng ngôn ngữ người dùng yêu cầu.

## Requirements *(mandatory)*

### Functional Requirements

**Đọc intake**

- **FR-001**: Plugin MUST nhận intake dưới mọi dạng văn bản người dùng có: nội dung dán trực tiếp,
  file/đường dẫn mà harness đọc được, lịch sử hội thoại, log, output của bước trước, hoặc yêu cầu
  ngắn.
- **FR-002**: Plugin MUST tự xác định nội dung cần làm media từ context hiện có trước khi hỏi người
  dùng; chỉ hỏi lại khi không tìm thấy nội dung hoặc thiếu thông tin làm đổi hẳn kết quả.
- **FR-003**: Plugin MUST ghi rõ các giả định đã dùng khi intake thiếu thông tin.

**Kịch bản Media**

- **FR-004**: Plugin MUST tạo Kịch bản Media gồm: nội dung nói về gì (1–3 câu), mục tiêu, đối tượng,
  kênh đăng dự kiến, hướng hình ảnh tổng thể, và danh sách vị trí cần ảnh.
- **FR-005**: Với mỗi vị trí ảnh, Kịch bản Media MUST nêu: vị trí trong nội dung, mục đích của ảnh,
  loại ảnh (ví dụ ảnh hero, minh họa trong bài, ảnh sản phẩm, infographic, ảnh chia sẻ mạng xã hội),
  tỉ lệ/định dạng, mức chất lượng/độ ưu tiên.
- **FR-006**: Plugin MUST đề xuất số lượng ảnh dựa trên độ dài, cấu trúc và mục tiêu của nội dung,
  và tôn trọng số lượng người dùng chỉ định nếu có.

**Prompt Pack**

- **FR-007**: Với mỗi ảnh, Prompt Pack MUST có tên ảnh (khớp Vị trí ảnh trong Kịch bản Media) và
  **một prompt liền mạch copy dùng ngay**. Tỉ lệ, phong cách và các ràng buộc cần thiết nằm sẵn
  trong prompt. Model tự quyết định cách áp khung, preset và quy tắc chống slop vào prompt; plugin
  KHÔNG bắt buộc hiển thị khe cấu trúc, trường phụ hay preset ID. Ghi chú phụ (alt text, caption,
  điều cần tránh tách riêng…) chỉ thêm khi model thấy nó giúp người dùng dùng ảnh tốt hơn.
- **FR-008**: Mục Reference MUST xuất hiện **chỉ khi** ảnh cần người dùng đính kèm tệp (ví dụ ảnh
  sản phẩm thật, ảnh nhân vật, ảnh phong cách). Khi có, nó MUST nêu cần tệp gì, vai trò từng tệp,
  và prompt MUST gọi đúng các tệp đó theo vai trò. Ảnh không cần tệp đính kèm thì không có mục này.
- **FR-009**: Plugin MUST đi kèm bộ template theo loại ảnh và bộ preset phong cách/chất lượng dựng
  sẵn làm tri thức cho model; model tự chọn và phối hợp chúng cho từng ảnh. Người dùng có thể yêu
  cầu đổi phong cách bằng lời hoặc theo tên preset. Bộ preset bản đầu MUST gồm ba nhóm: **R** — ảnh
  thật đời sống (12), **S** — phong cách thủ công cho minh họa (8), **C** — giữ nhân vật nhất quán
  qua nhiều ảnh (4); toàn bộ ghi nhãn v0.1 chưa test.
- **FR-010**: Mục tiêu chống slop là "ảnh có ý đồ, không có dấu hiệu đồ chế hàng loạt", không phải
  "không ai nhận ra là AI". Mọi prompt MUST: không dùng buzzword chất lượng (8K, masterpiece,
  ultra-detailed, stunning, flawless…); thay tính từ cảm xúc bằng chi tiết cụ thể (chủ thể đang làm
  gì, chất liệu, nơi chốn có 2–3 vật đời thường); nêu nguồn sáng thật và hướng sáng; dùng tối đa
  **một** chỉ dẫn camera/thời đại thiết bị và **một** khuyết điểm cụ thể (không chồng qualifiers mơ
  hồ); với ảnh thật thì nói rõ "photo", "unposed, not retouched, not cinematic"; chữ trong ảnh đặt
  trong ngoặc kép, nêu số lần xuất hiện. Plugin MUST chứa bảng dấu hiệu nhận dạng ảnh AI (da sáp,
  bokeh mọi nơi, màu cam-teal/ngả vàng, bố cục quá sạch, ánh sáng studio sai bối cảnh, tay cầm vật
  sai, chữ méo, chất liệu vô nghĩa, ánh sáng nền lệch chủ thể, quá nét/bão hòa, khuôn mặt AI lặp
  lại) kèm cách đối phó, làm tri thức cho model.
- **FR-011**: Các ảnh trong cùng một pack MUST nhất quán về phong cách, màu sắc và thương hiệu, trừ
  khi người dùng yêu cầu khác; đồng thời MUST đa dạng hóa người, nơi chốn, giờ/mùa, góc khung giữa
  các ảnh để tránh "cùng một khuôn mặt, cùng một phòng".
- **FR-012**: Mọi prompt MUST viết theo cách chạy tốt trên mọi công cụ tạo ảnh phổ biến mà không
  cần chỉnh: ý quan trọng nhất ở đầu, diễn đạt dạng khẳng định ("sharp focus throughout" thay vì
  "no blur"), không phụ thuộc negative prompt hay tham số riêng của một công cụ. Plugin KHÔNG chứa
  adapter hay ghi chú riêng theo công cụ.
- **FR-013**: Plugin MUST KHÔNG tự tạo ảnh hay gọi dịch vụ tạo ảnh; đầu ra chỉ là văn bản copy được.
- **FR-014**: Đầu ra MUST hiển thị được ngay trong hội thoại; khi harness hỗ trợ ghi file, người dùng
  có thể yêu cầu lưu Kịch bản Media + Prompt Pack thành một file văn bản.
- **FR-020**: Plugin MUST chỉ tạo prompt ảnh mockup sản phẩm (sản phẩm, thiết kế in, logo thật) khi
  người dùng báo vị trí đó cần mockup; không tự đề xuất. Khi tạo, plugin MUST: (a) có mục Reference
  yêu cầu ảnh sản phẩm/thiết kế thật; (b) viết prompt để AI chỉ tạo bối cảnh, người và ánh sáng,
  không vẽ lại thiết kế/logo; (c) kèm ghi chú ngắn: ghép thiết kế thật sau và giữ nguyên metadata AI
  (C2PA/IPTC) khi xuất file.

**Sửa prompt**

- **FR-015**: Plugin MUST nhận một prompt cùng mô tả lỗi hoặc ảnh kết quả, chẩn đoán nguyên nhân phía
  prompt, và trả về prompt đã sửa kèm giải thích ngắn.
- **FR-016**: Khi sửa một ảnh trong pack, plugin MUST giữ nguyên các ảnh khác và giữ sự nhất quán
  phong cách của pack.
- **FR-021**: Plugin MUST chứa checklist QC đạt/không đạt (không chấm điểm) và dùng nó khi chẩn đoán
  ảnh lỗi: da có texture; tay cầm vật đúng; chữ đúng, không méo; một nguồn sáng hợp lý, bóng khớp;
  nền không bokeh vô cớ, có vật đời thường; màu không ngả cam-teal/vàng mặc định; không lặp khuôn
  mặt đã dùng trong pack; với ảnh mockup thêm: sản phẩm/thiết kế đúng thật, metadata còn nguyên.
  Checklist không bắt buộc xuất kèm mỗi pack; người dùng có thể yêu cầu.

**Phân phối**

- **FR-017**: Plugin MUST cài đặt và cập nhật được qua link marketplace trỏ tới Git repo, trên các
  harness hỗ trợ marketplace (Claude, Codex).
- **FR-018**: Cùng một nguồn nội dung (hướng dẫn, template, preset) MUST dùng được trên Claude,
  Codex và ChatGPT; không duy trì bản nội dung riêng cho từng harness.
- **FR-019**: Mỗi bản phát hành MUST có số phiên bản và ghi chú thay đổi ngắn.

### Key Entities

- **Intake**: Mọi thứ người dùng đưa vào hoặc đã có trong context — nội dung, log, lịch sử, output
  trước, yêu cầu. Thuộc tính: loại, nguồn, phần nội dung được chọn để làm media.
- **Kịch bản Media (Media Brief)**: Bản phân tích nội dung và kế hoạch hình ảnh. Gồm tóm tắt, mục
  tiêu, đối tượng, kênh, hướng hình ảnh, giả định, và danh sách Vị trí ảnh.
- **Vị trí ảnh (Image Slot)**: Một ảnh cần làm. Gồm vị trí, mục đích, loại ảnh, tỉ lệ/định dạng,
  mức chất lượng. Mỗi Vị trí ảnh ứng với đúng một Prompt.
- **Prompt Pack**: Tập Prompt cho toàn bộ Kịch bản Media, kèm ghi chú phong cách chung của pack.
- **Prompt**: Đầu ra cho một ảnh — tên ảnh và một prompt liền mạch copy dùng ngay; có Reference
  chỉ khi cần tệp đính kèm; ghi chú phụ tùy model quyết định.
- **Template**: Khung prompt theo loại ảnh (hero, minh họa, sản phẩm, infographic, mạng xã hội…),
  nêu những yếu tố một prompt loại đó cần có.
- **Preset**: Khung prompt phong cách dựng sẵn có ID và tên để người dùng gọi lại, thuộc một trong
  ba nhóm: R (ảnh thật đời sống: snapshot điện thoại, phóng sự, phim 35mm, UGC cầm sản phẩm, product
  trung thực…), S (phong cách thủ công: risograph, cắt dán giấy, linocut, màu nước…), C (nhân vật
  nhất quán: character sheet, đưa vào cảnh mới, đổi trang phục, kiểm tra trôi).
- **Reference**: Ảnh tham chiếu người dùng có hoặc nên chuẩn bị, kèm vai trò (sản phẩm, phong cách,
  nhân vật, bố cục).

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Từ lúc đưa intake đến lúc có Prompt Pack hoàn chỉnh cho một bài viết ~1.500 từ mất
  dưới 3 phút, so với 30+ phút khi người dùng tự phân tích và viết prompt.
- **SC-002**: Ít nhất 80% prompt trong pack được người dùng dùng ngay lần đầu mà không phải sửa tay.
- **SC-003**: Blind test nội bộ: 5 người xem ảnh tạo từ prompt của plugin, trộn lẫn với ảnh chụp
  thật, không biết nguồn, trả lời "Có dùng ảnh này cho bài/listing không?" và "Có thấy đồ chế hàng
  loạt không?". Một preset đạt khi ít nhất 4/5 người dùng được và không thấy đồ chế; preset không đạt
  phải sửa hoặc bỏ trước khi gỡ nhãn v0.1.
- **SC-004**: Khi ảnh lỗi, ít nhất 80% trường hợp đạt yêu cầu sau tối đa 1 lần sửa prompt bằng plugin.
- **SC-005**: 100% prompt trong pack dán thẳng vào công cụ tạo ảnh là chạy được, không cần người
  dùng ghép trường hay xoá chú thích; 100% ảnh cần tệp đính kèm có mục Reference; không có ảnh nào
  bị tự tạo.
- **SC-006**: Người dùng mới cài xong plugin và chạy được pack đầu tiên trong dưới 5 phút chỉ với
  link marketplace; cập nhật phiên bản bằng một thao tác.
- **SC-007**: Cùng một intake mẫu cho ra Kịch bản Media và Prompt Pack tương đương về cấu trúc và
  chất lượng trên Claude, Codex và ChatGPT.
- **SC-008**: 100% ảnh mẫu dùng để nghiệm thu bản phát hành qua đủ các mục checklist QC áp dụng cho
  loại ảnh đó (FR-021).

## Assumptions

- Người dùng chính là người làm content/SEO/marketing viết bài blog, landing page, bài mạng xã hội
  và trang sản phẩm; đây là các loại nội dung được ưu tiên cho template mặc định.
- Người dùng tự tạo ảnh bằng công cụ họ đã có; plugin không chọn hay tích hợp công cụ tạo ảnh.
- Prompt mặc định viết bằng tiếng Anh (cho chất lượng ảnh tốt nhất trên đa số công cụ), phần giải
  thích và Kịch bản Media theo ngôn ngữ người dùng.
- Tri thức chống slop và thư viện preset lấy từ nghiên cứu nội bộ ngày 2026-11-18
  (`D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\01-landscape-tells-anti-slop.md` và
  `02-prompt-strategy-preset-library.md`); hiệu quả là giả thuyết cho tới khi qua SC-003.
- Số ảnh mặc định do plugin đề xuất theo nội dung (thường 3–8 ảnh cho một bài viết dài); người dùng
  có thể ghi đè.
- Claude và Codex cài/cập nhật qua link marketplace Git repo; với ChatGPT (nếu chưa hỗ trợ
  marketplace Git), cùng gói nội dung được đưa vào qua cơ chế skill/project của ChatGPT — đây là
  đường lui, không phải đường phân phối chính.
- Khả năng xem ảnh để chẩn đoán lỗi (Story 3, kịch bản 2) phụ thuộc harness; khi không có, plugin
  dựa vào mô tả lỗi của người dùng.
- Plugin không lưu lịch sử hay dữ liệu người dùng ngoài những gì harness đã giữ trong phiên.
- Bộ template theo loại ảnh ban đầu nhỏ (khoảng 5–8 loại ảnh). Bộ preset lấy từ thư viện nghiên cứu
  v0.1 (24 preset, nhóm R/S/C), chưa test trên model thật; preset bị từ chối nhiều trong blind test
  sẽ được sửa hoặc bỏ.
