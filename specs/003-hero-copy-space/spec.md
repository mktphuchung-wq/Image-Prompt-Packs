# Feature Specification: Vùng chữ dựng sẵn cho hero ở chế độ "chèn chữ sau"

**Feature Branch**: `mktphuchung-wq/Feature`

**Created**: 2026-11-19

**Status**: Draft

**Input**: User description: "Hero banner chế độ \"chèn chữ sau\" (chế độ 2) phải tạo được layout sẵn để chèn chữ: prompt mặc định dựng bố cục có vùng chữ rõ ràng — hoặc nền xóa phông nhẹ (làm mềm hậu cảnh ở vùng chữ), hoặc khoảng trống/negative space — và plugin (AI) tự xác định, nêu rõ vị trí vùng chữ cho người dùng để chèn tiêu đề sau. Hiện tại prompt chế độ 2 chỉ ghi \"clean empty space for a headline added later\", ảnh hero ra không có chỗ chữ rõ ràng/người dùng tưởng thiếu chữ."

## Bối cảnh

Nâng cấp nhỏ trên plugin v0.2.1 (`specs/002-prompt-pack-optimize`). Theo Clarification Q2 của 002, hero,
ảnh chia sẻ (OG) và thumbnail mặc định dùng **chế độ 2 — chèn chữ sau**. Khi dùng thật, người dùng tạo
ảnh hero và thấy **không có chữ, cũng không có chỗ rõ ràng để đặt chữ**, nên tưởng plugin bị lỗi.

Nguyên nhân nằm ở cách viết prompt chế độ 2 hiện tại: chỉ một cụm chung chung kiểu "clean empty space
for a headline added later" (xem ví dụ cuối `references/text-in-image.md`). Prompt không:

- quyết định chủ thể nằm ở đâu để chừa chỗ;
- chọn bề mặt cụ thể làm vùng chữ, hay cách làm vùng chữ "yên" (ít chi tiết);
- nói vùng đó sáng hay tối để chữ đọc được;
- và pack không nói cho người dùng biết vùng chữ ở đâu, cỡ bao nhiêu, nên đặt chữ màu gì.

Spec này **giữ nguyên mặc định chế độ 2** và biến nó thành một bố cục banner có chủ đích. Chế độ 3
(AI vẽ chữ) và 4 (hai lượt) không đổi, ngoài việc dùng chung vùng chữ ở đây.

Sau phiên làm rõ 2026-11-19, phạm vi thêm **khâu khởi tạo**: lượt đầu chỉ dừng hỏi khi quét intake thấy
trường hợp đặc biệt (chữ, phong cách, nội dung đặc biệt, format mới lạ), hỏi banner theo 4 điểm, và chốt
format các ảnh còn lại qua bảng Kịch bản Media (User Story 4, FR-215…FR-220).

## Clarifications

### Session 2026-11-19

- Q: Lượt đầu có luôn dừng hỏi về banner và format trước khi viết prompt không? → A: Không luôn luôn. Chỉ
  dừng hỏi khi gặp trường hợp đặc biệt: về chữ (có banner/hero/ảnh chia sẻ cần quyết cách đặt chữ, hoặc
  có tiêu đề/chữ người dùng chưa chốt), về phong cách (nội dung hợp nhiều hướng hình khác nhau), khi quét
  bài thấy nội dung đặc biệt, hoặc phát hiện dạng format mới lạ. Không có trường hợp nào thì xuất luôn
  với mặc định. Thay điều kiện dừng theo số ảnh/độ dài bài của 002 (FR-110, FR-114).
- Q: Khi dừng hỏi về banner/hero, hỏi những gì? → A: Bốn điểm, mỗi điểm có mặc định: tiêu đề chính xác và
  số dòng; cách đặt chữ; vùng chữ phía nào và tạo bằng khoảng trống thật hay làm mềm hậu cảnh; các khung
  cần. Màu thương hiệu lấy từ brand guideline nếu có, không hỏi.
- Q: Các ảnh còn lại chốt format thế nào khi lượt đầu dừng hỏi? → A: Bảng Kịch bản Media hiện format từng
  ảnh (loại, tỉ lệ, hướng, chữ); người dùng sửa theo số dòng hoặc trả "ok"; chỉ hỏi riêng ảnh có format
  mới lạ.
- Q: Có vẽ sơ đồ bố cục bằng ký tự cho banner ở lượt đầu không? → A: Không; chỉ mô tả vùng chữ bằng lời.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Hero ra ảnh có sẵn vùng đặt tiêu đề (Priority: P1)

Người dùng nhận prompt hero ở chế độ 2, dán vào công cụ tạo ảnh. Ảnh ra có chủ thể dồn về một phía và
một vùng rộng, yên, ít chi tiết ở phía còn lại. Vùng đó hoặc là một bề mặt trơn có thật trong cảnh
(tường, trời, sàn, mặt bàn), hoặc là hậu cảnh được làm mềm nhẹ. Người dùng đặt được tiêu đề lên vùng đó
mà không che chủ thể và chữ vẫn đọc rõ.

**Why this priority**: Đây đúng là lỗi người dùng gặp; thiếu nó thì mặc định chế độ 2 không dùng được.

**Independent Test**: Lấy prompt hero chế độ 2 của fixture Giáng sinh, tạo 5 ảnh, đặt thử một tiêu đề
rộng khoảng 40% bề ngang lên vùng chữ đã nêu; đếm số ảnh mà tiêu đề không che chủ thể và đọc được.

**Acceptance Scenarios**:

1. **Given** hero ở chế độ 2, **When** plugin viết prompt, **Then** prompt nêu rõ: chủ thể nằm ở phía
   nào (ví dụ một phần ba bên phải), vùng chữ ở phía nào, vùng chữ là gì (bề mặt cụ thể hoặc hậu cảnh
   làm mềm), tông của vùng chữ (sáng hay tối, ít chi tiết), và câu chặn chữ tự thêm.
2. **Given** cùng prompt, **When** đếm, **Then** prompt vẫn đạt tiêu chí tự kiểm của 002 (30–80 từ,
   ≤ 5 vật gọi tên, không số chẵn, không từ cấm), trừ ngoại lệ làm mềm hậu cảnh ở FR-205.
3. **Given** ảnh tạo ra từ prompt, **When** đặt tiêu đề rộng khoảng 40% bề ngang vào vùng chữ, **Then**
   tiêu đề không chồng lên chủ thể và đọc được khi thu nhỏ còn khoảng 360 px bề rộng.

---

### User Story 2 - Pack nói rõ vùng chữ ở đâu và đặt chữ thế nào (Priority: P2)

Ngay dưới prompt hero, pack có một khối **Vùng chữ** ngắn: vùng nằm ở đâu, chiếm khoảng bao nhiêu khung,
tông nền, màu chữ nên dùng, lề an toàn, và vùng còn nguyên khi cắt sang khung khác (OG, Pinterest) hay
không. Bảng Kịch bản Media ghi vị trí vùng chữ ngay trong cột Chữ. Người dùng biết ngay ảnh **cố ý không
có chữ** và biết chèn chữ vào đâu.

**Why this priority**: Giải phần "người dùng tưởng thiếu chữ"; cần P1 để vùng chữ thật sự tồn tại.

**Independent Test**: Đọc pack của fixture Giáng sinh; kiểm khối Vùng chữ có đủ trường và cột Chữ ghi
vị trí; người không biết plugin đọc pack và nói đúng "chữ sẽ thêm sau, ở vùng nào".

**Acceptance Scenarios**:

1. **Given** một ảnh chế độ 2, **When** pack xuất, **Then** ngay dưới khối prompt có khối "Vùng chữ" với:
   vị trí, cỡ tương đối, tông nền, màu chữ gợi ý, lề an toàn khoảng 5%, và câu "ảnh cố ý không có chữ;
   thêm tiêu đề bằng công cụ thiết kế".
2. **Given** bảng Kịch bản Media, **When** xem cột Chữ của ảnh chế độ 2, **Then** ô ghi cả chế độ và vị
   trí vùng, ví dụ "2 chèn chữ sau — 1/3 trái".
3. **Given** hero dùng lại cho khung khác (OG 1.91:1, Pinterest 2:3, story 9:16), **When** pack xuất,
   **Then** khối Vùng chữ nói vùng còn nguyên hay cần dời khi cắt, hoặc đề xuất prompt khung riêng.
4. **Given** khối Chốt nhanh mục 2, **When** mặc định là chèn chữ sau, **Then** câu mô tả nói rõ "ảnh
   chừa vùng để chèn tiêu đề, không có chữ trong ảnh" để người dùng không bất ngờ.

---

### User Story 3 - Chế độ 3 và 4 dùng chung vùng chữ (Priority: P3)

Khi người dùng đổi hero sang AI vẽ chữ hoặc hai lượt, plugin dùng lại đúng vùng chữ đã xác định: tiêu đề
nằm trong vùng đó, nền vùng đó bảo đảm tương phản.

**Why this priority**: Giữ nhất quán; thay đổi nhỏ.

**Independent Test**: Sau pack mặc định, yêu cầu "hero cho AI vẽ luôn tiêu đề …"; kiểm prompt mới giữ
nguyên bố cục và đặt tiêu đề vào vùng đã nêu.

**Acceptance Scenarios**:

1. **Given** hero chế độ 2 đã có vùng chữ, **When** đổi sang chế độ 3, **Then** prompt giữ bố cục, chủ
   thể và vùng chữ; tiêu đề đặt trong vùng đó theo quy tắc chế độ 3 của 002.
2. **Given** chế độ 4, **When** pack xuất, **Then** lượt 1 chính là prompt chế độ 2 có vùng chữ; lượt 2
   đặt tiêu đề vào đúng vùng đó.

---

### User Story 4 - Lượt đầu chỉ hỏi khi có trường hợp đặc biệt (Priority: P2)

Plugin quét intake trước khi viết prompt. Nếu thấy trường hợp đặc biệt về chữ, phong cách, nội dung hoặc
format, lượt đầu dừng với khối Chốt nhanh chỉ hỏi đúng các điểm đó, mỗi câu nói vì sao hỏi. Không có gì
đặc biệt thì xuất pack ngay với mặc định ghi rõ ở đầu.

**Why this priority**: Khâu khởi tạo quyết định chất lượng cả pack; hỏi đúng chỗ tránh làm lại, không hỏi
thừa.

**Independent Test**: Chạy fixture Giáng sinh (có hero + chỗ chờ sản phẩm → phải dừng), một yêu cầu
"3 ảnh minh họa cho bài về thói quen buổi sáng, không chữ, phong cách đời thường" (không có gì đặc biệt →
xuất luôn), và một yêu cầu carousel 5 slide (format mới lạ → phải dừng).

**Acceptance Scenarios**:

1. **Given** intake có hero/banner mà chưa chốt cách đặt chữ, **When** plugin xử lý, **Then** lượt đầu là
   Chốt nhanh có mục Banner gồm 4 điểm (tiêu đề và số dòng, cách đặt chữ, vùng chữ, các khung), mỗi điểm
   có mặc định, không có prompt.
2. **Given** intake đã chốt chữ, phong cách, format và không có nội dung đặc biệt, **When** plugin xử lý,
   **Then** pack xuất ngay, khối "Đã dùng mặc định" ở đầu.
3. **Given** intake yêu cầu một format không có trong bảng loại ảnh, **When** plugin xử lý, **Then** Chốt
   nhanh hỏi về format đó, nêu lý do "format mới lạ".
4. **Given** bất kỳ câu hỏi nào trong khối, **When** đọc, **Then** câu đó nêu lý do kích hoạt và có mặc định.
5. **Given** lượt đầu đã dừng, **When** người dùng trả "ảnh 3 đổi 4:5, bỏ ảnh 5, còn lại ok", **Then** pack
   áp đúng hai thay đổi đó, các ảnh khác theo bảng ban đầu.

---

### Edge Cases

- Cảnh vốn đông, không có bề mặt trơn (chợ, phố đông, phòng chật): plugin chọn làm mềm hậu cảnh ở vùng
  chữ, hoặc đổi góc máy để có trời/tường/sàn làm vùng chữ; nói rõ đã chọn cách nào.
- Khung dọc (2:3, 4:5, 9:16): vùng chữ là dải trên hoặc dưới, không phải một phần ba bên hông.
- Một hero dùng cho nhiều khung: chủ thể và vùng chữ phải nằm trong phần an toàn khi cắt; nếu không thể,
  đề xuất một prompt riêng cho khung đó.
- Tiêu đề dài hoặc tiếng Việt có dấu nhiều dòng: vùng chữ cần lớn hơn (khoảng 40–50% khung) và khối Vùng
  chữ ghi số dòng dự kiến.
- Có brand guideline: màu chữ gợi ý lấy từ màu thương hiệu nếu đủ tương phản với tông vùng chữ; không đủ
  thì gợi ý thêm dải màu đặc phía sau chữ.
- Hướng Minh họa thủ công: vùng chữ là khoảng giấy trơn hoặc mảng màu phẳng, không dùng làm mềm hậu cảnh.
- Hướng Biên tập/chuyên nghiệp: được dùng khoảng trống lớn, tối giản kiểu tạp chí.
- Làm mềm hậu cảnh không được biến thành bokeh mọi nơi: chỉ ảnh chế độ 2/3/4 dùng, chỉ ở phần hậu cảnh,
  ở mức nhẹ; ảnh trong bài vẫn theo quy tắc nét toàn cảnh của anti-slop.

## Requirements *(mandatory)*

### Functional Requirements

**Bố cục vùng chữ trong prompt (US1)**

- **FR-201**: Mọi prompt ảnh ở chế độ 2 MUST dựng bố cục banner có chủ đích: nêu vị trí chủ thể (ví dụ
  một phần ba bên phải, nửa dưới) và vị trí vùng chữ ở phần còn lại.
- **FR-202**: Prompt MUST chọn đúng một cách tạo vùng chữ và nêu cụ thể:
  (a) **khoảng trống thật trong cảnh** — một bề mặt trơn có thật (tường, trời, sàn, mặt bàn, vải trơn),
  gọi tên bề mặt; hoặc (b) **làm mềm hậu cảnh nhẹ** — chủ thể và tiền cảnh nét, hậu cảnh ở vùng chữ mềm
  và ít chi tiết; hoặc (c) **mảng màu/giấy phẳng** cho hướng Minh họa.
- **FR-203**: Model MUST tự chọn cách (a), (b) hoặc (c) theo cảnh và hướng hình, ưu tiên (a) khi cảnh có
  bề mặt trơn tự nhiên; (b) khi cảnh đông hoặc hướng Biên tập; (c) cho hướng Minh họa.
- **FR-204**: Prompt MUST nêu tông vùng chữ (tối trung bình hoặc sáng dịu), ít chi tiết, không vật nào
  lấn vào vùng đó, và giữ câu chặn chữ tự thêm của 002.
- **FR-205**: Ngoại lệ có giới hạn cho tell "bokeh mọi cảnh": làm mềm hậu cảnh CHỈ dùng cho ảnh chế độ 2,
  3, 4; chỉ ở hậu cảnh vùng chữ; ở mức nhẹ (vật hậu cảnh vẫn nhận ra được); chủ thể và tiền cảnh nét.
  Tri thức chống slop MUST ghi ngoại lệ này cạnh tell bokeh.
- **FR-206**: Prompt chế độ 2 MUST vẫn đạt tiêu chí tự kiểm của 002 (FR-101, FR-102, FR-104, FR-105); FR-103
  áp theo hướng hình như 002.

**Hướng dẫn vùng chữ cho người dùng (US2)**

- **FR-207**: Ngay dưới khối prompt của mỗi ảnh chế độ 2, pack MUST có khối **Vùng chữ** gồm: vị trí; cỡ
  tương đối (phần trăm khung); cách tạo vùng (a/b/c); tông nền; màu chữ gợi ý đủ tương phản (mã màu nếu có
  màu thương hiệu); lề an toàn khoảng 5%; số dòng tiêu đề dự kiến; câu "ảnh cố ý không có chữ; thêm tiêu
  đề bằng công cụ thiết kế".
- **FR-208**: Cột Chữ của bảng Kịch bản Media MUST ghi chế độ và vị trí vùng cho ảnh chế độ 2, 3, 4 (ví dụ
  "2 chèn chữ sau — 1/3 trái").
- **FR-209**: Khi hero được dùng cho khung khác, khối Vùng chữ MUST nói vùng còn nguyên hay phải dời khi
  cắt; nếu vùng mất khi cắt, plugin MUST đề xuất prompt riêng cho khung đó.
- **FR-210**: Mô tả mặc định chế độ 2 trong khối Chốt nhanh và khối "Đã dùng mặc định" MUST nói rõ ảnh
  chừa vùng để chèn tiêu đề và không có chữ trong ảnh.

**Dùng chung vùng chữ (US3)**

- **FR-211**: Khi đổi ảnh từ chế độ 2 sang 3 hoặc 4, plugin MUST giữ bố cục, chủ thể và vùng chữ; tiêu đề
  đặt trong vùng đã xác định. Lượt 1 của chế độ 4 MUST là prompt chế độ 2 có vùng chữ.

**Khi nào lượt đầu dừng hỏi (US4) — thay FR-110, FR-114 của 002 về điều kiện dừng**

- **FR-215**: Lượt đầu MUST dừng với khối Chốt nhanh (không kèm prompt) khi và chỉ khi có ít nhất một
  trường hợp đặc biệt sau, và khối chỉ hỏi về chính các trường hợp đó:
  (1) **Chữ**: pack có banner/hero/ảnh chia sẻ/thumbnail mà intake chưa chốt cách đặt chữ, hoặc có tiêu đề
  hay chữ trong ảnh chưa chốt nội dung/ngôn ngữ;
  (2) **Phong cách**: nội dung hợp với hơn một hướng hình mà chọn sai sẽ phải làm lại cả pack (ví dụ thời
  trang, thương hiệu, landing bán hàng);
  (3) **Nội dung đặc biệt** phát hiện khi quét bài: chỗ chờ sản phẩm, người hoặc thương hiệu thật, chủ đề
  nhạy cảm, số liệu cần infographic, nhiều ngôn ngữ;
  (4) **Format mới lạ**: dạng ảnh không có trong bảng loại ảnh của plugin (ví dụ carousel, before/after,
  chuỗi ảnh kể chuyện, ảnh so sánh, ảnh in ấn) hoặc tỉ lệ/kênh lạ.
- **FR-216**: Không có trường hợp đặc biệt nào, hoặc người dùng nói "đưa luôn", hoặc không có người trả
  lời: plugin MUST xuất pack ngay, khối "Đã dùng mặc định" ở đầu nêu rõ các mặc định (gồm "hero chừa vùng
  chèn tiêu đề, ảnh cố ý không có chữ").
- **FR-218**: Khi trường hợp (1) do banner/hero/ảnh chia sẻ kích hoạt, khối MUST có mục **Banner** gồm đúng
  4 điểm, mỗi điểm một mặc định: (a) tiêu đề chính xác và số dòng (mặc định: tiêu đề bài, rút gọn ≤ 6 từ
  nếu cần); (b) cách đặt chữ: chèn chữ sau / AI vẽ chữ / hai lượt (mặc định: chèn chữ sau); (c) vùng chữ:
  phía nào và cách tạo — khoảng trống thật hoặc làm mềm hậu cảnh (mặc định: model đề xuất theo cảnh, nêu
  một câu lý do); (d) các khung cần dùng, ví dụ 16:9 hero, 1.91:1 chia sẻ, 2:3 Pinterest (mặc định theo
  kênh trong bài). Màu chữ lấy từ brand guideline nếu có trong context; không hỏi màu, kiểu chữ, CTA, logo.
  Điểm nào intake đã chốt thì bỏ. Vùng chữ mô tả bằng lời (phía, cỡ tương đối, cách tạo); không vẽ sơ đồ
  bố cục bằng ký tự.
- **FR-219**: Khi lượt đầu dừng, format các ảnh còn lại MUST được chốt qua bảng Kịch bản Media (mỗi dòng có
  loại, tỉ lệ, hướng, chế độ chữ), kèm một dòng hướng dẫn "sửa theo số dòng, ví dụ 'ảnh 3 đổi 4:5, bỏ ảnh 5',
  hoặc trả 'ok'". Không hỏi từng ảnh; chỉ ảnh có format mới lạ (FR-215 mục 4) mới có câu hỏi riêng. Người
  dùng sửa theo số dòng thì plugin áp đúng dòng đó, giữ nguyên dòng khác.
- **FR-220**: Giới hạn tối đa 4 mục của khối Chốt nhanh (002 FR-111) vẫn giữ; mục Banner tính là một mục dù
  có 4 điểm con. Các trường hợp (2)–(4) mỗi loại tối đa một mục.
- **FR-217**: Mỗi câu hỏi trong khối MUST nêu lý do kích hoạt (trường hợp nào, thấy ở đâu trong bài) và
  có mặc định đề xuất; số lượng ảnh hay độ dài bài một mình KHÔNG là lý do dừng.

**Tri thức, ví dụ, kiểm thử, phát hành**

- **FR-212**: Tri thức chữ trong ảnh MUST có mục "Dựng vùng chữ" mô tả ba cách (a/b/c), cách chọn, cách
  nói vị trí theo khung ngang và dọc, mẫu khối Vùng chữ; ví dụ hero chế độ 2 hiện có MUST được viết lại
  theo FR-201…FR-207, kèm một ví dụ dùng cách (b) và một ví dụ khung dọc.
- **FR-213**: Bộ nghiệm thu MUST có tiêu chí mới cho hero/OG/thumbnail chế độ 2 trên fixture Giáng sinh
  và một fixture cảnh đông (không có bề mặt trơn) để kiểm cách (b).
- **FR-214**: Bản phát hành MUST tăng phiên bản minor và ghi thay đổi; metadata (mô tả plugin, giao diện
  Codex) cập nhật nếu nêu chế độ chữ.

### Key Entities

- **Vùng chữ (copy space)**: vị trí (theo khung ngang/dọc), cỡ tương đối, cách tạo (a khoảng trống thật /
  b làm mềm hậu cảnh / c mảng phẳng), tông nền, màu chữ gợi ý, lề an toàn, số dòng dự kiến, tình trạng khi
  cắt sang khung khác. Gắn với một ảnh chế độ 2/3/4; dùng lại khi đổi chế độ.
- **Khối Vùng chữ**: phần hiển thị của Vùng chữ trong pack, đặt dưới khối prompt.
- **Cột Chữ (mở rộng)**: thêm vị trí vùng chữ cho chế độ 2/3/4.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-201**: 100% ảnh chế độ 2 trong pack của fixture Giáng sinh và fixture cảnh đông có prompt nêu đủ:
  vị trí chủ thể, vị trí vùng chữ, cách tạo vùng, tông vùng; và có khối Vùng chữ đủ trường FR-207.
- **SC-202**: Tạo 5 ảnh từ prompt hero chế độ 2: ít nhất 4/5 ảnh có vùng chữ đặt được tiêu đề rộng khoảng
  40% bề ngang mà không che chủ thể và đọc được khi thu nhỏ còn khoảng 360 px.
- **SC-203**: Trong lượt dùng thử với người dùng, 0 lần người dùng báo "hero thiếu chữ" khi đã đọc pack
  (người dùng hiểu ảnh cố ý chừa chỗ).
- **SC-204**: Ảnh trong bài (chế độ 0) không tăng số ảnh bị dấu hiệu "bokeh vô cớ" theo checklist QC so với
  v0.2.1.
- **SC-205**: Đổi hero sang chế độ 3 giữ nguyên vùng chữ trong 100% lần chạy thử khô.
- **SC-206**: Trên bộ intake kiểm (fixture Giáng sinh; yêu cầu 3 ảnh minh họa đã chốt chữ và phong cách;
  yêu cầu carousel 5 slide), lượt đầu dừng hỏi đúng ở intake có trường hợp đặc biệt và xuất luôn ở intake
  không có — 100% đúng; mỗi câu hỏi nêu lý do kích hoạt.
- **SC-207**: Sau lượt đầu dừng, người dùng chốt toàn bộ banner và format các ảnh trong một câu trả lời
  (trả "ok" hoặc sửa theo số dòng) ở ≥ 80% lần dùng thật, không cần lượt hỏi thứ hai.

## Assumptions

- Mặc định hero/OG/thumbnail vẫn là chế độ 2 (Clarification Q2 của 002); spec này không đổi mặc định.
- Người dùng thêm tiêu đề bằng công cụ thiết kế bất kỳ; plugin không nêu tên công cụ (FR-012 của 001).
- "Làm mềm hậu cảnh nhẹ" là mô tả bằng lời trong prompt (ví dụ hậu cảnh hơi mềm, vật vẫn nhận ra); không
  dùng thuật ngữ thông số máy ảnh cụ thể hay cú pháp riêng công cụ.
- Không thêm script; vị trí và cỡ vùng là ước lượng bằng lời (một phần ba, khoảng 40%), kiểm bằng mắt.
- Phạm vi gồm hero, OG, thumbnail/banner và mọi ảnh người dùng tự chọn chế độ 2; không đổi ảnh chế độ 0, 1.
- Việc phát hiện trường hợp đặc biệt (FR-215) là phán đoán của model khi quét intake, dựa trên danh sách
  trường hợp và bảng loại ảnh của plugin; không có bộ lọc tự động.
