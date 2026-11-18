# Feature Specification: Prompt Pack v0.2 — chống ảnh dàn dựng, chế độ chữ, Chốt nhanh

**Feature Branch**: `mktphuchung-wq/Feature`

**Created**: 2026-11-18

**Status**: Draft

**Input**: User description: "Tối ưu plugin image-prompt-pack v0.1 → v0.2 dựa trên lượt chạy thật và báo cáo D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\03-plugin-test-staged-look-and-text-in-image.md. Vấn đề: (1) ảnh ra đơn điệu, quá clean, như dàn dựng — prompt dài 120–170 từ, liệt kê vật như danh mục, số lượng chẵn, mọi vật thuần chủ đề, không người/dấu vết dùng, ánh vàng đồng đều, khung giống nhau; plugin có quy tắc nhưng không tự ép. (2) Hero cần chữ nhưng chính sách chữ chỉ có "tránh/chừa trống". (3) Quyết định lớn (hướng hình, chữ, mockup, số ảnh) bị giả định thầm lặng, người dùng biết muộn. (4) Ranh giới mockup mơ hồ (pack tự thêm mục Bonus mockup khi bài có placeholder sản phẩm). Hướng: thẻ Chốt nhanh có mặc định ở đầu phản hồi (tối đa 4 mục, trả lời ok là xong, dừng chờ khi bài dài/≥4 ảnh); chế độ chữ trong ảnh (không chữ, chữ trong cảnh, chèn chữ sau, AI vẽ chữ, hai lượt) + QC chữ; tiêu chí tự kiểm trước khi xuất (≤80 từ, ≤5 vật gọi tên, tránh số chẵn/đối xứng, ≥1 vật lạc đề, 1 dấu vết con người, cấm từ trừu tượng đứng một mình, chặn chữ model tự thêm); bảng đa dạng cấp pack (loại khung, độ cao máy, nhiệt độ ánh sáng, thời tiết/giờ, có người); 4 tell mới; mockup chỉ hỏi xác nhận khi bài nhắc sản phẩm/placeholder, mặc định không; fixture Giáng sinh + acceptance mới."

## Bối cảnh

Đây là bản nâng cấp của feature `specs/001-image-prompt-pack` (plugin v0.1.0 đã phát hành). Mọi yêu cầu
của 001 vẫn giữ nguyên trừ những điểm spec này **thay thế** (ghi rõ "thay FR-xxx của 001"). Bằng
chứng gốc: lượt chạy thật của người dùng với bài "Indoor Christmas Decorations" (9 prompt, 3 ảnh đã
tạo) và báo cáo nghiên cứu 03 (gọi tắt **[R03]**).

Bốn lỗi quan sát được:

1. **Ảnh dàn dựng, đơn điệu.** Prompt dài 120–170 từ (quy định là 30–80), viết như danh mục vật, nêu
   số lượng chẵn ("two wreaths", "four stockings"), mọi vật thuần chủ đề, 6/8 ảnh không có người,
   cùng ánh vàng ấm, cùng khung 3:2 ngang tầm mắt. Plugin có quy tắc đúng nhưng không tự ép.
2. **Hero cần chữ nhưng plugin chỉ biết "tránh hoặc chừa trống".**
3. **Quyết định lớn bị giả định thầm lặng.** Hướng hình, chữ, mockup, số ảnh nằm ở mục Giả định;
   người dùng chỉ biết sau khi đã nhận cả pack và tạo ảnh.
4. **Ranh giới mockup mơ hồ.** Bài có chỗ chờ sản phẩm, pack tự thêm mục "Bonus — Product-locked
   prompts".

## Clarifications

### Session 2026-11-18

- Q: Mặc định hướng hình của cả pack là gì? → A: Model tự chọn theo loại bài/kênh và nêu rõ trong Chốt
  nhanh, vì có lúc ảnh cần chuyên nghiệp, chỉn chu, thời trang (fashionista) chứ không chỉ đời thường.
- Q: Hero mặc định dùng chế độ chữ nào? → A: Chèn chữ sau bằng công cụ thiết kế (đỡ phải sửa ảnh); AI vẽ
  chữ và hai lượt chỉ khi người dùng chọn.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Pack không còn ra ảnh dàn dựng (Priority: P1)

Người dùng đưa một bài viết theo mùa/chủ đề (ví dụ trang trí Giáng sinh trong nhà). Plugin trả về các
prompt ngắn, kể một khoảnh khắc thay vì liệt kê đồ, có dấu vết người đang dùng, có vật đời thường
lạc đề, và cả pack khác nhau rõ về khung, ánh sáng, có người hay không. Ảnh tạo ra trông như chụp
trong nhà thật, không như showroom.

**Why this priority**: Đây là than phiền chính sau lượt chạy thật và là mục tiêu cốt lõi của plugin
(ảnh không có dấu hiệu đồ chế hàng loạt).

**Independent Test**: Chạy fixture Giáng sinh (bài gốc của lượt test) và đối chiếu từng prompt với
tiêu chí tự kiểm; đối chiếu bảng đa dạng cấp pack. Không cần thẻ Chốt nhanh hay chế độ chữ để kiểm.

**Acceptance Scenarios**:

1. **Given** bài Giáng sinh của lượt test, **When** plugin xuất pack, **Then** mỗi prompt dài 30–80
   từ (trừ cảnh nhiều chủ thể, có ghi lý do), gọi tên tối đa 5 vật, không nêu số lượng chẵn hay bố trí
   đối xứng, có ít nhất một vật đời thường lạc chủ đề và một dấu vết con người cụ thể.
2. **Given** cùng bài, **When** plugin xuất pack, **Then** không prompt nào dùng từ trừu tượng đứng
   một mình (cozy, welcoming, lived-in, natural, authentic, realistic, imperfect, charming) mà không
   kèm chi tiết cụ thể thay thế.
3. **Given** pack từ 4 ảnh trở lên, **When** xem bảng Kịch bản Media, **Then** có các cột loại khung,
   độ cao máy, nhiệt độ ánh sáng, thời tiết/giờ, có người hay không; không hai ảnh liền nhau trùng cả
   loại khung, độ cao máy và nhiệt độ ánh sáng; có ít nhất một ảnh ánh lạnh hoặc u ám; có ít nhất hai
   ảnh có tay hoặc người; không loại khung nào chiếm quá nửa số ảnh.
4. **Given** một ảnh không cần chữ, **When** plugin viết prompt, **Then** prompt có câu khẳng định
   chặn chữ model tự thêm (ví dụ bao bì trơn, không có chữ đọc được).
5. **Given** ba ảnh cũ của lượt test cùng mô tả lỗi "đơn điệu, quá clean, như sắp đặt", **When**
   người dùng nhờ sửa prompt, **Then** chẩn đoán chỉ ra đúng các nguyên nhân ở [R03] mục A (danh mục
   vật, số chẵn, thuần chủ đề, không dấu vết dùng, ánh đồng đều, khung giống nhau) và prompt sửa xử lý
   từng nguyên nhân.

---

### User Story 2 - Chốt nhanh trước khi viết cả pack (Priority: P2)

Với bài dài hoặc pack từ 4 ảnh trở lên, phản hồi đầu tiên của plugin là Kịch bản Media kèm khối
**Chốt nhanh** đặt ngay đầu: tối đa 4 mục (hướng hình, chữ trong ảnh, sản phẩm/mockup, số ảnh-tỉ lệ-
kênh), mỗi mục có mặc định. Người dùng trả lời "ok" là plugin viết pack theo mặc định; sửa một mục thì
pack theo lựa chọn đó.

**Why this priority**: Chặn việc tạo hàng loạt ảnh sai hướng (tốn credit, thời gian), giải quyết lỗi
"giả định thầm lặng". Đặt sau P1 vì không có P1 thì dù chốt đúng hướng ảnh vẫn dàn dựng.

**Independent Test**: Đưa bài Giáng sinh, kiểm phản hồi đầu chỉ có Kịch bản Media + Chốt nhanh và
dừng chờ; trả "ok" thì nhận pack đúng mặc định; trả lời sửa mục 2 thì hero đổi chế độ chữ.

**Acceptance Scenarios**:

1. **Given** bài dài hoặc pack dự kiến từ 4 ảnh, **When** người dùng gọi plugin, **Then** phản hồi đầu
   có Kịch bản Media và khối Chốt nhanh ở đầu phản hồi, không có prompt nào, và dừng chờ một câu trả lời.
2. **Given** khối Chốt nhanh, **When** người dùng trả lời "ok", **Then** plugin xuất pack theo đúng các
   mặc định đã nêu, không hỏi thêm.
3. **Given** yêu cầu ngắn 1–3 ảnh, hoặc người dùng nói "đưa luôn", hoặc không có người để hỏi
   (chạy tự động), **When** plugin xử lý, **Then** plugin xuất pack ngay và đặt khối mặc định đã dùng ở
   đầu phản hồi.
4. **Given** intake đã nêu phong cách, chữ, sản phẩm hay số ảnh, **When** plugin lập Chốt nhanh,
   **Then** mục đã rõ không xuất hiện trong khối; mọi mục đều rõ thì không có khối Chốt nhanh.
5. **Given** pack đã xuất, **When** người dùng đổi một mục (ví dụ hướng hình), **Then** plugin chỉ viết
   lại các prompt bị ảnh hưởng.
6. **Given** bất kỳ khối Chốt nhanh nào, **When** đọc nó, **Then** không có tên/ID preset, tên công cụ
   tạo ảnh hay tham số kỹ thuật; các lựa chọn mô tả bằng kết quả nhìn thấy.

---

### User Story 3 - Hero và ảnh chia sẻ có chữ khi cần (Priority: P3)

Mỗi vị trí ảnh có một **chế độ chữ**. Hero/OG/Pinterest có thể có tiêu đề do AI vẽ luôn, hoặc chừa
vùng để chèn chữ sau, hoặc tạo hai lượt (cảnh trước, thêm chữ sau). Prompt có chữ tuân bộ quy tắc
riêng để chữ đúng chính tả, đọc được khi thu nhỏ.

**Why this priority**: Phục vụ trực tiếp than phiền "hero cần chữ". Phụ thuộc Chốt nhanh mục 2 để
người dùng chọn, nhưng kiểm độc lập được khi người dùng nêu thẳng chế độ.

**Independent Test**: Yêu cầu "hero có tiêu đề 'Indoor Christmas Decorations' do AI vẽ"; kiểm prompt
hero theo quy tắc chế độ AI vẽ chữ; tạo ảnh và kiểm theo QC chữ.

**Acceptance Scenarios**:

1. **Given** bảng Kịch bản Media, **When** xem từng ảnh, **Then** có cột Chữ ghi một trong các chế độ:
   không chữ, chữ trong cảnh, chèn chữ sau, AI vẽ chữ, hai lượt.
2. **Given** hero ở chế độ AI vẽ chữ, **When** plugin viết prompt, **Then** prompt có chuỗi chữ chính
   xác trong ngoặc kép (tối đa khoảng 6 từ, 1–2 dòng), kiểu chữ hoa/thường, kiểu chữ mô tả bằng đặc
   điểm (không tên font), màu, vị trí, cỡ tương đối, bề mặt nền tương phản phía sau chữ, lề an toàn
   khoảng 5% mỗi cạnh, và câu "xuất hiện một lần, không có chữ nào khác".
3. **Given** chế độ chèn chữ sau, **When** plugin viết prompt, **Then** prompt chừa một vùng trống có
   vị trí và độ tương phản rõ, không có chữ trong ảnh, và pack ghi người dùng thêm chữ bằng công cụ
   thiết kế.
4. **Given** chế độ hai lượt, **When** plugin xuất, **Then** ảnh đó có hai prompt: lượt 1 tạo cảnh có
   vùng trống; lượt 2 chỉnh ảnh, gọi ảnh lượt 1 là ảnh tham chiếu đã duyệt, chỉ thêm tiêu đề, giữ nguyên
   mọi thứ khác.
5. **Given** tiêu đề tiếng Việt có dấu được chọn cho chế độ AI vẽ chữ, **When** plugin xuất, **Then**
   pack cảnh báo cần thử một ảnh mẫu trên công cụ đang dùng và nói rõ sai một dấu thì chuyển sang chèn
   chữ sau.
6. **Given** ảnh có chữ đã tạo, **When** người dùng xin kiểm, **Then** plugin dùng QC chữ đạt/không đạt:
   đúng chính tả từng ký tự, đúng dấu tiếng Việt, xuất hiện một lần, đọc được khi thu nhỏ còn khoảng
   360 px bề rộng, đủ tương phản, không có chữ lạ trên biển/sách/bao bì, nằm trong lề an toàn.

---

### User Story 4 - Mockup có xác nhận rõ ràng (Priority: P4)

Khi bài có nhắc sản phẩm hoặc có chỗ chờ sản phẩm, plugin hỏi một câu xác nhận trong Chốt nhanh, mặc
định "không làm mockup". Người dùng chọn "có" thì mới có prompt mockup; chọn "không" thì pack không có
bất kỳ mục mockup hay "Bonus" nào.

**Why this priority**: Đóng vùng xám đã gặp; phạm vi nhỏ.

**Independent Test**: Bài Giáng sinh có 2 chỗ chờ sản phẩm; trả "ok" thì pack không có mockup; chọn
"có" thì ảnh tương ứng có Reference bắt buộc và nhãn chờ sản phẩm xác minh.

**Acceptance Scenarios**:

1. **Given** bài nhắc sản phẩm hoặc có chỗ chờ sản phẩm, **When** plugin lập Chốt nhanh, **Then** có mục
   sản phẩm nêu số chỗ và vị trí, mặc định "không".
2. **Given** người dùng giữ mặc định, **When** pack xuất, **Then** không có prompt mockup, không có mục
   "Bonus" hay prompt sản phẩm nào.
3. **Given** người dùng chọn "có", **When** pack xuất, **Then** ảnh mockup có Reference ảnh sản phẩm thật
   bắt buộc, nhãn "chờ sản phẩm xác minh", và vẫn theo quy tắc trung thực sản phẩm của 001.
4. **Given** bài không nhắc sản phẩm, **When** plugin lập Chốt nhanh, **Then** không có mục sản phẩm.

---

### Edge Cases

- Người dùng không trả lời khối Chốt nhanh mà hỏi chuyện khác: plugin không tự xuất pack; khi người
  dùng quay lại thì giữ khối đã đưa.
- Người dùng trả lời một phần ("hướng B, còn lại ok"): áp mục đã đổi, mục còn lại theo mặc định.
- Harness hoặc pipeline không có người trả lời: xuất luôn, ghi rõ ở đầu là đã dùng mặc định.
- Bài theo mùa cần giá trị "cảm hứng", hoặc nội dung thời trang/thương hiệu cần ảnh chuyên nghiệp: hướng
  "biên tập/chuyên nghiệp" được phép gọn đẹp, không bắt vật lạc đề hay dấu vết dùng, nhưng vẫn giữ độ dài,
  số vật, không số chẵn, không từ trừu tượng, và bảng đa dạng (FR-116).
- Cảnh nhiều chủ thể thật sự (nhóm người, so sánh nhiều sản phẩm): cho phép vượt 80 từ, prompt ghi lý
  do ngắn trong Kịch bản Media (không trong khối prompt).
- Vật lạc đề phải hợp ngữ cảnh bài (ví dụ dây sạc, hóa đơn, cốc uống dở), không chọn rập khuôn cùng
  một vật cho mọi ảnh.
- Pack chỉ 1–3 ảnh: quy tắc tỉ lệ trong bảng đa dạng (ít nhất một ảnh lạnh, hai ảnh có người) áp theo
  khả năng; không ép một ảnh duy nhất phải lạnh.
- Ảnh cần chữ nhưng nền tự nhiên quá sáng/rối: prompt phải đặt dải màu đặc hoặc vùng tường trung tính
  tối phía sau chữ.

## Requirements *(mandatory)*

### Functional Requirements

**Tự kiểm trước khi xuất (US1)**

- **FR-101**: Mỗi prompt MUST dài 30–80 từ. Vượt 80 từ chỉ khi cảnh có nhiều chủ thể, và lý do ghi
  trong Kịch bản Media. Prompt MUST kể một khoảnh khắc, không viết thành danh sách vật.
- **FR-102**: Mỗi prompt MUST gọi tên tối đa 5 vật; MUST tránh số lượng chẵn và bố trí đối xứng/cách
  đều; chỉ nêu số khi số đó có ý nghĩa.
- **FR-103**: Mỗi prompt ảnh đời thường MUST có ít nhất một vật đời thường lạc chủ đề, chọn theo
  ngữ cảnh bài, và MUST có một dấu vết con người cụ thể (cốc uống dở, việc đang làm dở, đồ bỏ dở) thay
  cho tính từ.
- **FR-104**: Prompt MUST KHÔNG dùng các từ trừu tượng sau khi đứng một mình: cozy, welcoming, lived-in,
  natural, authentic, realistic, imperfect, charming (và tương đương "slightly imperfect", "subtle
  imperfections"). Danh sách nằm trong tri thức chống slop, giữ ngắn.
- **FR-105**: Prompt ảnh không chữ MUST có một câu khẳng định chặn chữ do model tự thêm (bao bì, biển,
  sách không có chữ đọc được) và nói cụ thể vật nền để model không tự điền vật theo chủ đề.
- **FR-106**: Các tiêu chí FR-101…FR-105 MUST được viết thành tiêu chí tự kiểm trong mô tả kỹ năng
  (không thành quy trình đánh số bước), áp cho mọi pack và cho prompt đã sửa.

**Đa dạng cấp pack (US1) — thay FR-011 của 001 về phần đa dạng**

- **FR-107**: Bảng Kịch bản Media MUST có thêm các cột: loại khung (toàn cảnh, trung cảnh, cận chi tiết,
  qua vai, đang làm dở), độ cao máy, nhiệt độ ánh sáng, thời tiết hoặc giờ, có người hay không.
- **FR-108**: Với pack từ 4 ảnh: không hai ảnh liền nhau trùng cả loại khung, độ cao máy và nhiệt độ ánh
  sáng; ít nhất một ảnh ánh lạnh hoặc u ám; ít nhất hai ảnh có tay hoặc người; không loại khung nào
  chiếm quá nửa số ảnh. Pack 1–3 ảnh áp theo khả năng. Tính nhất quán phong cách/thương hiệu của FR-011
  (001) vẫn giữ.

**Tell mới (US1)**

- **FR-109**: Bảng dấu hiệu nhận dạng MUST thêm 4 tell, ghi rõ là suy luận từ một lượt test, chưa đo:
  đối xứng và đồ thành cặp; thuần chủ đề, không vật lạc đề; không dấu vết sử dụng; model tự thêm chữ
  hoặc vật. Mỗi tell có cách đối phó trong prompt. Chế độ sửa prompt MUST dùng các tell này khi chẩn
  đoán.

**Chốt nhanh (US2) — thay FR-002/FR-003 của 001 về cách hỏi**

- **FR-110**: Khi pack dự kiến từ 4 ảnh hoặc intake là bài dài, phản hồi đầu MUST gồm Kịch bản Media và
  khối **Chốt nhanh** đặt đầu phản hồi, không kèm prompt, rồi dừng chờ một câu trả lời.
- **FR-111**: Khối Chốt nhanh MUST có tối đa 4 mục — (1) hướng hình và mức đời thường, (2) chữ trong
  ảnh, (3) sản phẩm/mockup, (4) số ảnh-tỉ lệ-kênh — mỗi mục có một mặc định đề xuất và tối đa 3 lựa
  chọn, mô tả bằng kết quả nhìn thấy. Không có tên/ID preset, tên công cụ tạo ảnh, tham số kỹ thuật.
- **FR-112**: Mục nào intake đã quyết định thì MUST bỏ khỏi khối; không còn mục nào thì không có khối.
- **FR-113**: Trả lời "ok" MUST xuất pack theo mặc định, không hỏi thêm; trả lời một phần thì mục không
  nhắc theo mặc định.
- **FR-114**: Yêu cầu ngắn 1–3 ảnh, người dùng nói "đưa luôn", hoặc không có người để hỏi: MUST xuất pack
  ngay, đặt các mặc định đã dùng thành khối ngắn ở đầu phản hồi (thay cho mục Giả định nằm cuối).
- **FR-115**: Người dùng đổi một mục sau khi đã có pack: MUST chỉ viết lại các prompt bị ảnh hưởng.
- **FR-116**: Mặc định của mục (1) hướng hình MUST do model chọn theo loại nội dung và kênh, và MUST
  được nêu rõ trong khối Chốt nhanh kèm một câu lý do (không giả định thầm lặng). Các hướng hợp lệ gồm ít
  nhất: đời thường chụp điện thoại có dấu vết sử dụng; biên tập/chuyên nghiệp chỉn chu (kiểu tạp chí,
  thời trang, fashion editorial); minh họa thủ công. Một pack có thể phối hướng theo từng ảnh và ghi ở
  bảng Kịch bản Media. Với hướng chuyên nghiệp/thời trang: FR-103 (vật lạc đề, dấu vết dùng) không bắt
  buộc, nhưng FR-101, FR-102, FR-104, FR-105 và FR-108 vẫn áp; tính chân thật đến từ ánh sáng, chất
  liệu, tư thế và bối cảnh cụ thể thay vì từ sự bừa bộn.

**Chế độ chữ (US3) — thay Edge Case "ảnh có chữ" của 001**

- **FR-117**: Mỗi ảnh MUST có đúng một chế độ chữ, hiển thị ở cột Chữ của Kịch bản Media: (0) không chữ,
  (1) chữ trong cảnh, (2) chèn chữ sau, (3) AI vẽ chữ, (4) hai lượt.
- **FR-118**: Chế độ chữ trong cảnh MUST: tối đa 3 từ, trong ngoặc kép, xuất hiện một lần, nêu viết tay
  hay in và nằm trên vật gì.
- **FR-119**: Chế độ chèn chữ sau MUST: chủ thể ở một phần, vùng trống có vị trí và tương phản rõ ở phần
  còn lại, không có chữ trong ảnh; pack ghi người dùng thêm chữ bằng công cụ thiết kế.
- **FR-120**: Chế độ AI vẽ chữ MUST: chuỗi chính xác trong ngoặc kép (tối đa khoảng 6 từ, 1–2 dòng; dòng
  phụ chỉ khi cần), kiểu hoa/thường, kiểu chữ mô tả bằng đặc điểm, màu (mã màu nếu là màu thương hiệu),
  vị trí, cỡ tương đối, bề mặt nền tương phản phía sau chữ, lề an toàn khoảng 5% mỗi cạnh, câu "xuất
  hiện một lần, không có chữ nào khác".
- **FR-121**: Chế độ hai lượt MUST xuất hai prompt cho cùng ảnh: lượt 1 tạo cảnh có vùng trống; lượt 2
  chỉnh ảnh, gọi ảnh lượt 1 là ảnh tham chiếu đã duyệt, chỉ thêm tiêu đề, nói rõ giữ nguyên mọi thứ khác.
  Mục Reference của lượt 2 nêu tệp là ảnh lượt 1.
- **FR-122**: Tiêu đề tiếng Việt có dấu ở chế độ AI vẽ chữ hoặc hai lượt: pack MUST cảnh báo thử một ảnh
  mẫu trên công cụ đang dùng và sai một dấu thì chuyển sang chèn chữ sau.
- **FR-123**: Mặc định của mục (2) chữ trong ảnh MUST là: hero và ảnh chia sẻ/thumbnail dùng **chèn chữ
  sau** (FR-119); các ảnh khác **không chữ**. AI vẽ chữ và hai lượt chỉ dùng khi người dùng chọn trong
  Chốt nhanh hoặc yêu cầu trực tiếp.
- **FR-124**: Tri thức MUST có QC chữ đạt/không đạt: đúng chính tả từng ký tự; đúng dấu tiếng Việt;
  xuất hiện một lần; đọc được khi thu nhỏ còn khoảng 360 px bề rộng; đủ tương phản; không có chữ lạ
  trên biển/sách/bao bì; nằm trong lề an toàn. Chế độ sửa prompt dùng QC này cho ảnh có chữ.
- **FR-125**: Chữ trong ảnh MUST KHÔNG thay alt text; ảnh có chữ vẫn có gợi ý alt mô tả khi pack phục vụ
  trang web.

**Mockup (US4) — thay FR-020 của 001 về điều kiện kích hoạt**

- **FR-126**: Khi intake nhắc sản phẩm hoặc có chỗ chờ sản phẩm, Chốt nhanh MUST có mục sản phẩm nêu số
  chỗ và vị trí, mặc định "không làm mockup". Intake không nhắc sản phẩm thì không có mục này; mockup
  vẫn có thể lập khi người dùng tự yêu cầu (như 001).
- **FR-127**: Khi mockup không được chọn, pack MUST KHÔNG có prompt mockup, mục "Bonus" hay prompt sản
  phẩm nào dưới bất kỳ tên gọi nào.
- **FR-128**: Khi mockup được chọn, ảnh mockup MUST có Reference ảnh sản phẩm thật bắt buộc, nhãn "chờ
  sản phẩm xác minh", và giữ toàn bộ quy tắc trung thực của FR-020 (001).

**Kiểm thử và phát hành**

- **FR-129**: Bộ fixture MUST thêm bài Giáng sinh của lượt test (có 2 chỗ chờ sản phẩm) và bộ ba ảnh lỗi
  kèm mô tả, với tiêu chí đạt mới: đếm từ, đếm vật, số chẵn, vật lạc đề, dấu vết dùng, bảng đa dạng, chế
  độ chữ hero, Chốt nhanh, không mockup khi giữ mặc định.
- **FR-130**: Bản phát hành MUST là 0.2.0 với ghi chú thay đổi liệt kê các điểm thay thế so với 0.1.0.
- **FR-131**: Mô tả kỹ năng MUST vẫn giữ giới hạn độ dài và nguyên tắc không quy trình đánh số; chi tiết
  chế độ chữ và Chốt nhanh nằm ở tri thức tham chiếu riêng.

### Key Entities

- **Khối Chốt nhanh**: Tối đa 4 mục (hướng hình, chữ, sản phẩm, số ảnh-tỉ lệ-kênh); mỗi mục có mặc định,
  tối đa 3 lựa chọn; có trạng thái "đang chờ" (dừng) hoặc "đã dùng mặc định" (xuất luôn).
- **Kịch bản Media (mở rộng)**: Thêm cột Chữ, loại khung, độ cao máy, nhiệt độ ánh sáng, thời tiết/giờ,
  có người; thêm lý do khi prompt vượt 80 từ.
- **Chế độ chữ**: Một trong 5 giá trị; quyết định cấu trúc prompt và số prompt (1 hoặc 2) cho ảnh đó.
- **Prompt (mở rộng)**: Có thể có prompt lượt 2 (chế độ hai lượt); có câu chặn chữ tự thêm ở ảnh không chữ.
- **Tiêu chí tự kiểm**: Danh sách kiểm được trên văn bản prompt (số từ, số vật, số chẵn, vật lạc đề, dấu
  vết con người, từ cấm, câu chặn chữ).
- **QC chữ**: 7 mục đạt/không đạt cho ảnh có chữ.
- **Tell (mở rộng)**: 15 tell (11 cũ + 4 mới), 4 tell mới có nhãn "suy luận, chưa đo".

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-101**: Với fixture Giáng sinh, 100% prompt trong pack đạt mọi tiêu chí tự kiểm FR-101…FR-105
  (đếm được trên văn bản).
- **SC-102**: Với fixture Giáng sinh, bảng Kịch bản Media đạt 100% quy tắc đa dạng FR-108.
- **SC-103**: Blind test 5 người: bộ ảnh tạo từ pack v0.2 cho cùng bài được ít nhất 4/5 người chọn "dùng
  được" và ít nhất 4/5 người chọn "không thấy đồ chế hàng loạt", và được đa số chọn hơn ba ảnh cũ khi
  so cạnh nhau.
- **SC-104**: Với bài dài, 100% lần chạy có phản hồi đầu chỉ gồm Kịch bản Media + Chốt nhanh và dừng chờ;
  trả "ok" ra pack đúng mặc định trong một lượt.
- **SC-105**: Khi người dùng giữ mặc định mục sản phẩm, 0 prompt mockup hay mục "Bonus" xuất hiện.
- **SC-106**: Ảnh hero có chữ (chế độ AI vẽ chữ hoặc hai lượt) qua đủ 7 mục QC chữ ở ít nhất 4/5 lần tạo
  với tiêu đề tiếng Anh trên công cụ người dùng đang dùng.
- **SC-107**: Số lần phải dùng chế độ sửa prompt trung bình cho mỗi pack giảm so với lượt test v0.1 (đo
  trên cùng bài).
- **SC-108**: Khối Chốt nhanh được trả "ok" nguyên khối ở đa số lần dùng thật (≥ 60%); thấp hơn thì
  xem lại mặc định.

## Assumptions

- Nguồn chứng cứ là một lượt test thật (một bài, 9 prompt, 3 ảnh xem được) và một ảnh thử chữ tiếng
  Anh trên một công cụ; các tell mới và hiệu quả đề xuất là giả thuyết cho tới blind test.
- "Bài dài" là nội dung khoảng từ 800 từ trở lên hoặc có từ 4 mục lớn trở lên; dưới mức đó coi là yêu
  cầu ngắn nếu số ảnh dự kiến ≤ 3.
- Hành vi dừng chờ là chỉ dẫn cho model; harness có thể không bảo đảm tuyệt đối. Cần kiểm trên Claude
  Code, Codex và ChatGPT.
- Prompt vẫn chung cho mọi công cụ (FR-012 của 001): không gợi ý tên model hay công cụ thiết kế cụ thể;
  chỉ nói "công cụ bạn đang dùng".
- Không thêm script; mọi tiêu chí đếm (số từ, số vật) là tiêu chí cho model tự kiểm và cho người kiểm
  khi nghiệm thu.
- Pack đã dán trong lượt test có thể được tạo trên ChatGPT; v0.2 phải được kiểm trên cả ba harness.
- Bài gốc lượt test (`C:\Users\user\Downloads\PYW_How To.md`) được đưa vào fixture dưới dạng đã lược
  thông tin không cần thiết; ba ảnh lỗi được mô tả bằng chữ trong fixture nếu không được phép lưu ảnh.
