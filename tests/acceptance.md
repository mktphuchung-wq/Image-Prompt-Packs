# Tiêu chí nghiệm thu: prompt-pack v0.1.0

Mỗi dòng ánh xạ tới FR hoặc SC trong `specs/001-image-prompt-pack/spec.md`. Cột **Đạt/Không** để người chạy điền. Kết quả chạy khô nằm trong `tests/runs/2026-11-18-codex/` (us1.md, us2.md, us3.md) và đã được ghi lại ở đó.

## US1: Fixture 01 và lượt đổi thành mockup

Chạy theo `quickstart.md` mục 3, dòng 1, 1b và 5.

| # | Kịch bản | Tiêu chí | FR/SC | Đạt/Không |
|---|---|---|---|---|
| US1-1 | Dòng 1 | Kịch bản Media đủ trường: nội dung 1–3 câu, mục tiêu, đối tượng, kênh, hướng hình ảnh, danh sách vị trí ảnh | FR-004, FR-005 | |
| US1-2 | Dòng 1 | Có 3–8 ảnh | FR-006 | |
| US1-3 | Dòng 1 | Mỗi ảnh một khối prompt copy được; không placeholder `[...]`; không cú pháp riêng của công cụ; không buzzword chất lượng | FR-007, FR-010, FR-012, SC-005 | |
| US1-4 | Dòng 1 | Không có mục Reference ở ảnh không cần tệp đính kèm | FR-008 | |
| US1-5 | Dòng 1 | Không tự thêm ảnh mockup dù bài có nhắc sản phẩm | FR-020, US1-AS5 | |
| US1-6 | Dòng 1 | Đầu ra chỉ là văn bản; không tạo ảnh | FR-013 | |
| US1-7 | Dòng 1 | Các ảnh khác nhau về người, nơi chốn, giờ | FR-011 | |
| US1-8 | Dòng 1b | Lượt sau "làm prompt ảnh cho bài vừa rồi" tự lấy bài từ lịch sử, không bắt dán lại | FR-002, US1-AS3 | Chưa kiểm: cần hội thoại thật |
| US1-9 | Dòng 5 | Ảnh 2 thành mockup: có Reference là ảnh sản phẩm thật; prompt không vẽ lại thiết kế hay logo; có ghi chú ghép thiết kế thật và giữ metadata AI | FR-020 | |

## US2: Fixture 02, fixture 03 và intake rỗng

Chạy theo `quickstart.md` mục 3, dòng 2 và 3; thêm trường hợp intake rỗng.

| # | Kịch bản | Tiêu chí | FR/SC | Đạt/Không |
|---|---|---|---|---|
| US2-1 | Dòng 2 | Có mục Giả định nêu rõ các giả định đã dùng | FR-003, US2-AS1 | |
| US2-2 | Dòng 2 | Đúng 3 ảnh theo số người dùng nêu | Edge Case 3, FR-006 | |
| US2-3 | Dòng 2 | Không tự thêm mockup dù yêu cầu có chữ "bán" | FR-020 | |
| US2-4 | Dòng 2 | Nếu có hỏi thì tối đa 3 câu, mỗi câu có đề xuất mặc định | US2-AS3 | |
| US2-5 | Dòng 2 | Pack đủ cấu trúc theo `contracts/prompt-pack-output.md` mục 1 | FR-007, FR-008 | |
| US2-6 | Dòng 3 | Nói rõ đã chọn phần "5 thói quen buổi sáng…" của log | US2-AS2, FR-002 | |
| US2-7 | Dòng 3 | Pack đủ cấu trúc theo contract; không lẫn nội dung của hai chủ đề còn lại | FR-007, US2-AS2 | |
| US2-8 | Intake rỗng | Khi "làm ảnh cho bài này" mà không có bài nào trong context: báo không tìm thấy nội dung, xin nội dung hoặc đường dẫn, không bịa | Edge Case 1, FR-002 | |

## US3: Fixture 04 (sửa prompt)

Chạy theo `quickstart.md` mục 3, dòng 4.

| # | Kịch bản | Tiêu chí | FR/SC | Đạt/Không |
|---|---|---|---|---|
| US3-1 | Dòng 4 | Chẩn đoán trỏ đúng ba lỗi: tay cầm vật sai, chữ méo, ánh sáng studio sai bối cảnh | FR-015, FR-021 | |
| US3-2 | Dòng 4 | Chỉ trả prompt của ảnh 2; ảnh 1 và 3 không xuất hiện lại | FR-016, US3-AS3 | |
| US3-3 | Dòng 4 | Prompt đã sửa mô tả cách cầm cốc cụ thể | `anti-slop.md` mục 3 | |
| US3-4 | Dòng 4 | Chữ trên cốc đặt trong ngoặc kép kèm "appears once", hoặc bỏ hẳn chữ | `anti-slop.md` mục 2 | |
| US3-5 | Dòng 4 | Nguồn sáng là thật và hợp bối cảnh bếp nhà (cửa sổ, đèn bếp), không có ánh đèn studio | FR-010, FR-021 | |
| US3-6 | Dòng 4 | Có 1–3 dòng "Đã đổi" nêu thay đổi và lỗi mỗi thay đổi nhắm tới | US3-AS1, contract mục 2 | |
| US3-7 | Dòng 4 | Tỉ lệ thành công sau tối đa một lần sửa (SC-004) | SC-004 | Chưa kiểm: đo khi chạy với ảnh thật |

## Ghi chú chung

- Dòng 1b, US3-7 và SC-003 (blind test) cần người hoặc hội thoại thật; không kiểm được bằng chạy khô.
- Cột Đạt/Không để người chạy điền. Kết quả chạy khô, lần sửa và bằng chứng nằm trong `tests/runs/2026-11-18-codex/us1.md`, `us2.md`, `us3.md`.

## v0.2 — US1: chống dàn dựng

Chạy theo `specs/002-prompt-pack-optimize/quickstart.md` mục 3, kịch bản B (fixture `05-christmas-article.md` và trả lời "ok") và kịch bản E (fixture `06-staged-images-feedback.md`). Cột **Đạt/Không** để người chạy điền. Kết quả chạy khô, số từ từng prompt và số vòng sửa nằm trong `tests/runs/2026-11-18-v0.2/us1.md`.

| # | Kịch bản | Tiêu chí | FR/SC | Đạt/Không |
|---|---|---|---|---|
| V2-US1-1 | B | Mỗi prompt dài 30–80 từ (ghi số từ của từng prompt) | FR-101, SC-101 | |
| V2-US1-2 | B | Mỗi prompt gọi tên tối đa 5 vật, đếm theo quy ước ở `anti-slop.md` mục 2 (không đếm người, bộ phận cơ thể, nguồn sáng, nơi chốn, bề mặt nền) | FR-102, SC-101 | |
| V2-US1-3 | B | Không có số lượng chẵn ("two", "four", "a pair of") và không có bố trí đối xứng hoặc cách đều trong prompt | FR-102, SC-101 | |
| V2-US1-4 | B | Mỗi ảnh Đời thường có ít nhất một vật lạc chủ đề và một dấu vết người cụ thể; vật lạc chủ đề không lặp giữa các ảnh | FR-103, US1-AS1 | |
| V2-US1-5 | B | Không dùng đứng một mình các từ cấm: cozy, welcoming, lived-in, natural, authentic, realistic, imperfect, charming, "slightly imperfect", "subtle imperfections" | FR-104, US1-AS2, SC-101 | |
| V2-US1-6 | B | Ảnh không chữ có câu chặn chữ tự thêm và nêu vật nền cụ thể | FR-105 | |
| V2-US1-7 | B | Bảng Kịch bản Media có đủ cột Hướng, Khung, Độ cao máy, Ánh sáng, Thời tiết/giờ, Người, Chữ | FR-107 | |
| V2-US1-8 | B | Pack từ 4 ảnh đạt bốn quy tắc: không hai ảnh liền nhau trùng cả Khung, Độ cao máy và Ánh sáng; có ít nhất một ảnh ánh lạnh hoặc u ám; có ít nhất hai ảnh có tay hoặc người; không loại Khung nào chiếm quá nửa số ảnh | FR-108, US1-AS3, SC-102 | |
| V2-US1-9 | B | Prompt vượt 80 từ (nếu có) được ghi lý do trong Kịch bản Media | FR-101 | |
| V2-US1-10 | E | Chẩn đoán nêu ít nhất 5 nguyên nhân trong bảng dấu hiệu ở `anti-slop.md` mục 3: danh mục vật, số chẵn, thuần chủ đề, không dấu vết, ánh đồng đều, khung giống nhau, model tự thêm vật hoặc chữ | FR-109, US1-AS5 | |
| V2-US1-11 | E | Prompt sửa cho từng ảnh đạt mọi tiêu chí tự kiểm (V2-US1-1 đến V2-US1-6), và chỉ trả prompt của ảnh bị phàn nàn | FR-106, FR-016 | |
| V2-US1-12 | E | Mỗi ảnh sửa có 1–3 dòng "Đã đổi" nêu thay đổi nhắm vào lỗi cụ thể | FR-015, US1-AS5 | |

## v0.2 — US2: Chốt nhanh

Chạy theo `specs/002-prompt-pack-optimize/quickstart.md` mục 3, kịch bản A, B, F, G và trả lời một phần. Kịch bản A dùng fixture `05-christmas-article.md`; F dùng `02-one-line-request.md`. Cột **Đạt/Không** để người chạy điền. Kết quả chạy khô nằm trong `tests/runs/2026-11-18-v0.2/us2.md`.

| # | Kịch bản | Tiêu chí | FR/SC | Đạt/Không |
|---|---|---|---|---|
| V2-US2-1 | A | Phản hồi đầu có khối "Chốt nhanh" ở trên cùng, rồi Kịch bản Media; không có khối prompt nào; dừng chờ một câu trả lời | FR-110, US2-AS1, SC-104 | |
| V2-US2-2 | A | Khối có tối đa 4 mục; mỗi mục có một mặc định và tối đa 3 lựa chọn | FR-111 | |
| V2-US2-3 | A | Mục 1 (hướng hình) nêu hướng mặc định và một câu lý do; có thể là Đời thường, Biên tập hoặc Minh họa | FR-116 | |
| V2-US2-4 | A | Mục 3 (sản phẩm) nêu đúng 2 chỗ chờ (chăn trên sofa và chăn trên giường phòng ngủ), mặc định "không" | FR-126, FR-111 | |
| V2-US2-5 | A | Khối không có tên hay ID preset, tên công cụ tạo ảnh, tham số kỹ thuật; lựa chọn mô tả bằng kết quả nhìn thấy | FR-111, US2-AS6 | |
| V2-US2-6 | B | Trả lời "ok": xuất pack theo đúng các mặc định đã nêu, không hỏi thêm | FR-113, US2-AS2, SC-104 | |
| V2-US2-7 | B | Trả lời một phần "hướng B, còn lại ok": mục B áp dụng, các mục còn lại theo mặc định | FR-113, Edge case | |
| V2-US2-8 | F | Xuất luôn (3 ảnh); khối "Đã dùng mặc định" ở đầu phản hồi, mỗi mục một dòng; không có mục Giả định ở cuối | FR-114, US2-AS3 | |
| V2-US2-9 | G | Sau khi có pack, "đổi sang hướng biên tập chuyên nghiệp": chỉ prompt bị ảnh hưởng được viết lại; prompt mới vẫn đạt tự kiểm, trừ FR-103 | FR-115, FR-116, US2-AS5 | |
| V2-US2-10 | A (biến thể) | Người dùng hỏi việc khác khi đang chờ: không tự xuất pack; khi quay lại, khối Chốt nhanh đã đưa vẫn giữ nguyên | Edge case "không trả lời" | |

## v0.2 — US3: chế độ chữ

Chạy theo `specs/002-prompt-pack-optimize/quickstart.md` mục 3, kịch bản B (cột Chữ), C (hero AI vẽ chữ), và hai biến thể: chế độ 3 với tiêu đề tiếng Việt có dấu, chế độ 4 (hai lượt). Cột **Đạt/Không** để người chạy điền. Kết quả chạy khô nằm trong `tests/runs/2026-11-18-v0.2/us3.md`.

| # | Kịch bản | Tiêu chí | FR/SC | Đạt/Không |
|---|---|---|---|---|
| V2-US3-1 | B | Bảng Kịch bản Media có cột Chữ; mỗi ảnh ghi đúng một chế độ (0 đến 4) | FR-117 | |
| V2-US3-2 | B | Hero và ảnh chia sẻ ghi chế độ 2 (chèn chữ sau); các ảnh khác ghi chế độ 0 | FR-123, SC-101 | |
| V2-US3-3 | B | Prompt hero ở chế độ 2 chừa vùng trống có vị trí và độ tương phản rõ, không có chữ trong ảnh, và pack ghi người dùng thêm chữ bằng công cụ thiết kế | FR-119, FR-123 | |
| V2-US3-4 | C | "Hero cho AI vẽ luôn tiêu đề Indoor Christmas Decorations": chỉ prompt hero đổi; chuỗi nằm trong ngoặc kép, nêu kiểu hoa/thường, kiểu chữ theo đặc điểm (không tên font), màu, vị trí, cỡ tương đối, bề mặt nền tương phản, lề khoảng 5%, và câu "appears once; no other text anywhere" | FR-120, US3-AS2 | |
| V2-US3-5 | C (biến thể) | Tiêu đề tiếng Việt có dấu "Trang trí Giáng sinh trong nhà" ở chế độ 3: pack cảnh báo thử một ảnh mẫu trên công cụ đang dùng, và sai một dấu thì chuyển sang chèn chữ sau | FR-122, US3-AS5 | |
| V2-US3-6 | C (biến thể) | Chế độ 4 (hai lượt): ảnh có hai khối prompt; lượt 2 dùng đúng câu "Image 1 = approved scene. Add the headline only; keep everything else unchanged."; mục Reference của lượt 2 là ảnh lượt 1 | FR-121, US3-AS4 | |
| V2-US3-7 | Mọi ảnh có chữ | Ảnh có chữ có gợi ý alt mô tả; chữ không được dùng thay H1 hoặc alt | FR-125 | |
| V2-US3-8 | Kiểm ảnh | Khi người dùng xin kiểm ảnh có chữ, dùng đủ 7 mục QC chữ (đúng chính tả từng ký tự, đúng dấu tiếng Việt, xuất hiện một lần, đọc được ở khoảng 360 px, đủ tương phản, không có chữ lạ, trong lề an toàn) | FR-124, US3-AS6 | |
| SC-106 | Ảnh thật | Hero có chữ (AI vẽ chữ hoặc hai lượt) qua đủ 7 mục QC chữ ở ít nhất 4 trên 5 lần tạo, với tiêu đề tiếng Anh. Mục này chỉ đo được khi tạo ảnh thật: **cần người chạy** | SC-106 | Cần người chạy |

## v0.2 — US4: mockup

Chạy theo `specs/002-prompt-pack-optimize/quickstart.md` mục 3, kịch bản B (giữ mặc định), D (chọn "có" ở mục 3), và hai fixture không có chỗ chờ sản phẩm: `01-blog-article.md` (có nhắc hoodie) và `03-messy-log.md` (không nhắc sản phẩm). Cột **Đạt/Không** để người chạy điền. Kết quả chạy khô nằm trong `tests/runs/2026-11-18-v0.2/us4.md`.

| # | Kịch bản | Tiêu chí | FR/SC | Đạt/Không |
|---|---|---|---|---|
| V2-US4-1 | B (giữ mặc định) | Pack không có prompt mockup; không có mục "Bonus", "Product-locked" hay prompt sản phẩm dưới tên khác | FR-127, SC-105 | |
| V2-US4-2 | D ("mục 3 chọn có") | Có đúng 2 prompt mockup, mỗi chỗ một prompt; mỗi prompt có Reference là ảnh sản phẩm thật, nhãn "chờ sản phẩm xác minh", và ghi chú ghép thiết kế thật sau cùng giữ metadata AI | FR-128, FR-020 | |
| V2-US4-3 | 01 (có nhắc hoodie, không có chỗ chờ) | Chốt nhanh có mục 3 (sản phẩm), mặc định "không" | FR-126, US4-AS1 | |
| V2-US4-4 | 03 (log không nhắc sản phẩm) | Không có mục 3 sản phẩm trong khối Chốt nhanh hoặc Đã dùng mặc định | FR-126, US4-AS4 | |
| V2-US4-5 | Rà skill | `SKILL.md` không còn câu cũ "mockup chỉ khi người dùng yêu cầu đúng vị trí đó" đứng một mình mâu thuẫn với điều kiện mới; mục Ranh giới trỏ `anti-slop.md` mục 5 | FR-020 (thay), FR-126 | |

## Truy vết FR và SC (T030)

Trạng thái: **Đạt (chạy khô)** nghĩa là có nội dung trong file và có tiêu chí đạt trong bản chạy khô; **Một phần** nghĩa là còn phần cần môi trường thật; **Cần người chạy** nghĩa là chỉ kiểm được bằng người hoặc ảnh thật.

| Mã | Yêu cầu (tóm tắt) | Nơi đáp ứng | Trạng thái |
|---|---|---|---|
| FR-001 | Nhận intake mọi dạng | `SKILL.md` mục Tiêu chí; US2-6, US2-7 | Đạt (chạy khô) |
| FR-002 | Tự xác định nội dung trước khi hỏi | `SKILL.md`; US1-8, US2-6, US2-8 | Một phần: US1-8 cần hội thoại thật |
| FR-003 | Ghi giả định | `SKILL.md`; US2-1 | Đạt (chạy khô) |
| FR-004 | Kịch bản Media đủ trường | `SKILL.md` mục Đầu ra; US1-1 | Đạt (chạy khô) |
| FR-005 | Vị trí ảnh đủ trường | `SKILL.md` mục Đầu ra; US1-1 | Đạt (chạy khô) |
| FR-006 | Đề xuất số ảnh theo cấu trúc | `image-types.md` mục Đề xuất số ảnh; US1-2, US2-2 | Đạt (chạy khô) |
| FR-007 | Tên ảnh và một prompt liền mạch | `SKILL.md`; US1-3 | Đạt (chạy khô) |
| FR-008 | Reference chỉ khi cần tệp | `SKILL.md`; US1-4, US1-9 | Đạt (chạy khô) |
| FR-009 | Template và preset R/S/C | `presets.md`, `image-types.md` | Đạt về cấu trúc. Chất lượng preset: Cần người chạy (SC-003) |
| FR-010 | Quy tắc chống slop và bảng 11 dấu hiệu | `anti-slop.md` mục 2–3; US1-3 | Đạt (chạy khô, sau vòng 2) |
| FR-011 | Nhất quán và đa dạng trong pack | `anti-slop.md` mục 4; `presets.md` bảng slot; US1-7 | Đạt (chạy khô) |
| FR-012 | Chạy trên mọi công cụ, không adapter | `anti-slop.md` mục 2; `SKILL.md` Ranh giới; kiểm chuỗi trong `verification.md` | Đạt (chạy khô) |
| FR-013 | Không tự tạo ảnh | `SKILL.md` Mục tiêu và Ranh giới; US1-6 | Đạt (chạy khô) |
| FR-014 | Hiển thị ngay, ghi file khi được yêu cầu | `SKILL.md` mục Đầu ra | Một phần: chưa kiểm ghi file trên harness |
| FR-015 | Sửa prompt: chẩn đoán, prompt, giải thích | `SKILL.md`; US3-1, US3-6 | Đạt (chạy khô) |
| FR-016 | Giữ các ảnh khác khi sửa một ảnh | `SKILL.md`; US3-2 | Đạt (chạy khô) |
| FR-017 | Cài và cập nhật qua marketplace Git | Hai marketplace; `verification.md` | Một phần: cài cục bộ đã chạy thật trên Claude Code và Codex; URL Git và cập nhật chưa kiểm |
| FR-018 | Cùng một nguồn cho ba harness | `plugins/image-prompt-pack/skills/prompt-pack/` là nguồn duy nhất | Đạt về cấu trúc. ChatGPT: CHƯA KIỂM CHỨNG |
| FR-019 | Số phiên bản và ghi chú thay đổi | `CHANGELOG.md`; `plugin.json` 0.1.0 | Đạt |
| FR-020 | Mockup chỉ khi người dùng yêu cầu | `SKILL.md` Ranh giới; US1-5, US1-9, US2-3 | Đạt (chạy khô) |
| FR-021 | Checklist QC đạt/không đạt | `anti-slop.md` mục 6; US3-1 | Đạt về nội dung. Dùng trên ảnh thật: Cần người chạy (SC-008) |
| SC-001 | Dưới 3 phút cho bài ~1.500 từ | Không đo được trong chạy khô | Cần người chạy |
| SC-002 | Ít nhất 80% prompt dùng ngay | Không đo được trong chạy khô | Cần người chạy |
| SC-003 | Blind test 5 người | `docs/blind-test.md` | Cần người chạy |
| SC-004 | 80% đạt sau tối đa một lần sửa | US3-7 | Cần người chạy (ảnh thật) |
| SC-005 | Prompt dán được; Reference đủ; không tự tạo ảnh | US1-3, US1-4, US1-6 | Đạt (chạy khô). Dán vào công cụ thật: Cần người chạy |
| SC-006 | Cài dưới 5 phút; cập nhật một thao tác | Cài cục bộ trên Claude Code và Codex đã thử; `verification.md` | Một phần: cần người chạy trên máy sạch và kiểm cập nhật |
| SC-007 | Cùng intake, kết quả tương đương trên ba harness | `quickstart.md` mục 3 | CHƯA KIỂM CHỨNG |
| SC-008 | Ảnh mẫu qua đủ mục QC | `anti-slop.md` mục 6 | Cần người chạy (ảnh thật) |

## Truy vết v0.2 (T029)

Trạng thái: **Đạt (chạy khô)** nghĩa là có tiêu chí v0.2 và bản chạy khô đạt trong `tests/runs/2026-11-18-v0.2/`; **Một phần** nghĩa là còn nhánh chưa chạy; **Cần người chạy** nghĩa là chỉ kiểm được bằng người hoặc ảnh thật; **CHƯA KIỂM CHỨNG** nghĩa là chưa có bằng chứng nào.

| Mã | Yêu cầu (tóm tắt) | Nơi đáp ứng | Acceptance / bằng chứng | Trạng thái |
|---|---|---|---|---|
| FR-101 | 30–80 từ; kể một khoảnh khắc | `SKILL.md` Tiêu chí; `anti-slop.md` §2 (tự kiểm) | V2-US1-1; `us1.md` | Đạt (chạy khô) |
| FR-102 | Tối đa 5 vật; không số chẵn hoặc đối xứng | `anti-slop.md` §2 | V2-US1-2, V2-US1-3 | Đạt (chạy khô) |
| FR-103 | Đời thường: vật lạc chủ đề và dấu vết người | `anti-slop.md` §2 | V2-US1-4 | Đạt (chạy khô) |
| FR-104 | Từ cấm không đứng một mình | `anti-slop.md` §2 (bảng thay thế) | V2-US1-5 | Đạt (chạy khô) |
| FR-105 | Ảnh không chữ có câu chặn chữ | `anti-slop.md` §2 | V2-US1-6 | Đạt (chạy khô) |
| FR-106 | Tiêu chí tự kiểm viết thành tiêu chí, không đánh số bước | `SKILL.md` Tiêu chí; `anti-slop.md` §2 | V2-US1-11; rà T028 | Đạt (chạy khô) |
| FR-107 | Cột đa dạng trong Kịch bản Media | `SKILL.md` Đầu ra; `anti-slop.md` §4 | V2-US1-7 | Đạt (chạy khô) |
| FR-108 | Quy tắc đa dạng cho pack từ 4 ảnh | `anti-slop.md` §4 | V2-US1-8; `us1.md` và `us4.md` (kiểm FR-108) | Đạt (chạy khô) |
| FR-109 | Bốn tell mới, nhãn suy luận; dùng khi chẩn đoán | `anti-slop.md` §3; `SKILL.md` Khi sửa prompt | V2-US1-10; `us1.md` (ảnh E) | Đạt (chạy khô); đo hiệu quả: CHƯA KIỂM CHỨNG |
| FR-110 | Dừng chờ khi dự kiến từ 4 ảnh hoặc bài dài | `SKILL.md` Cách hỏi; `brief-card.md` | V2-US2-1; `us2.md` (A) | Đạt (chạy khô); trên harness: CHƯA KIỂM CHỨNG |
| FR-111 | Chốt nhanh tối đa 4 mục, mỗi mục mặc định, tối đa 3 lựa chọn | `SKILL.md`; `brief-card.md` | V2-US2-2, V2-US2-5 | Đạt (chạy khô) |
| FR-112 | Mục intake đã quyết thì bỏ khỏi khối | `SKILL.md` Cách hỏi; `brief-card.md` | V2-US2-8 (fixture 02: số ảnh do người dùng nêu, không xuất hiện trong khối) | Đạt (chạy khô) |
| FR-113 | "ok" xuất pack mặc định; trả lời một phần | `SKILL.md`; `brief-card.md` | V2-US2-6, V2-US2-7 | Đạt (chạy khô; trả lời một phần chỉ mức bảng) |
| FR-114 | 1–3 ảnh, "đưa luôn", hoặc không có người để trả lời: xuất luôn | `SKILL.md`; `brief-card.md` | V2-US2-8 (fixture 02) | Một phần: nhánh "không có người trả lời" chưa chạy |
| FR-115 | Đổi một mục sau pack: chỉ viết lại prompt bị ảnh hưởng | `SKILL.md` Cách hỏi | V2-US2-9; `us2.md` (G) | Đạt (chạy khô) |
| FR-116 | Hướng hình do model chọn, có lý do; Biên tập không bắt vật lạc đề | `SKILL.md`; `brief-card.md`; `anti-slop.md` §2 | V2-US2-3, V2-US2-9 | Đạt (chạy khô) |
| FR-117 | Mỗi ảnh đúng một chế độ chữ, ghi ở cột Chữ | `SKILL.md`; `text-in-image.md` | V2-US3-1 | Đạt (chạy khô) |
| FR-118 | Chế độ 1: tối đa 3 từ, ngoặc kép, một lần, viết tay hoặc in, nằm trên vật gì | `text-in-image.md` (bảng chế độ) | Có trong tri thức; chưa có kịch bản chạy riêng | Một phần |
| FR-119 | Chế độ 2: vùng trống rõ, không chữ trong ảnh, ghi chú thêm chữ bằng công cụ thiết kế | `text-in-image.md` | V2-US3-3; `us3.md` | Đạt (chạy khô) |
| FR-120 | Chế độ 3: chuỗi, kiểu chữ, màu, vị trí, cỡ, nền, lề, câu "appears once" | `text-in-image.md` | V2-US3-4; `us3.md` | Đạt (chạy khô) |
| FR-121 | Chế độ 4: hai lượt, câu chuẩn, Reference là ảnh lượt 1 | `text-in-image.md`; `SKILL.md` Đầu ra | V2-US3-6; `us3.md` | Đạt (chạy khô) |
| FR-122 | Tiếng Việt có dấu: thử ảnh mẫu, sai một dấu thì chuyển chế độ 2 | `text-in-image.md` | V2-US3-5; `us3.md` | Đạt (chạy khô, văn bản); thử trên ảnh thật: Cần người chạy |
| FR-123 | Mặc định hero, OG, thumbnail: chèn chữ sau; ảnh khác không chữ | `SKILL.md`; `brief-card.md`; `image-types.md` | V2-US3-2 | Đạt (chạy khô) |
| FR-124 | QC chữ đạt/không đạt, 7 mục | `text-in-image.md` | V2-US3-8 | Đạt về nội dung; kiểm trên ảnh thật: Cần người chạy |
| FR-125 | Chữ không thay alt; ảnh có chữ vẫn có gợi ý alt | `SKILL.md` Tiêu chí; `text-in-image.md` | V2-US3-7; `us3.md` | Đạt (chạy khô) |
| FR-126 | Mục sản phẩm khi intake nhắc sản phẩm; mặc định không | `SKILL.md`; `brief-card.md` | V2-US4-3, V2-US4-4; `us4.md` | Đạt (chạy khô) |
| FR-127 | Không chọn mockup: không prompt mockup, không "Bonus" | `SKILL.md` Ranh giới; `anti-slop.md` §5 | V2-US4-1; `us4.md` | Đạt (chạy khô) |
| FR-128 | Chọn có: Reference bắt buộc, nhãn "chờ sản phẩm xác minh", giữ trung thực | `SKILL.md` Ranh giới; `anti-slop.md` §5 | V2-US4-2; `us4.md` | Đạt (chạy khô); ảnh thật: Cần người chạy |
| FR-129 | Fixture 05 và 06 cùng tiêu chí đạt mới | `tests/fixtures/05`, `06`; acceptance v0.2 | `us1.md` đến `us4.md` | Đạt (có fixture; chạy khô) |
| FR-130 | Bản phát hành 0.2.0 có ghi chú thay đổi | `plugin.json` ×2; `CHANGELOG.md` mục `[0.2.0]` | `OK 0.2.0` (manifest) | Đạt |
| FR-131 | `SKILL.md` giữ giới hạn độ dài, không đánh số bước; chi tiết trong references | `SKILL.md` 138 dòng; `brief-card.md`; `text-in-image.md` | Rà T028 trong `docs/verification.md` | Đạt |
| SC-101 | Mọi prompt fixture 05 đạt FR-101…FR-105 | `us1.md` | 10 trên 10 prompt (7 pack, 3 sửa) | Đạt (chạy khô) |
| SC-102 | Bảng fixture 05 đạt 100% FR-108 | `us1.md` | V2-US1-8 | Đạt (chạy khô) |
| SC-103 | Blind test 5 người, pack v0.2 so với ba ảnh cũ | `docs/blind-test.md` | Giao thức có sẵn; chưa có kết quả | Cần người chạy |
| SC-104 | Bài dài: 100% lần chạy có Chốt nhanh và dừng chờ; "ok" ra pack mặc định | `us2.md` | V2-US2-1, V2-US2-6 | Đạt (chạy khô); trên harness: Cần người chạy |
| SC-105 | Giữ mặc định mục sản phẩm: 0 prompt mockup hoặc "Bonus" | `us1.md`; `us4.md` | V2-US4-1 | Đạt (chạy khô) |
| SC-106 | Hero có chữ qua 7 mục QC ở ít nhất 4/5 lần tạo | `docs/blind-test.md`; `text-in-image.md` | V2-US3-8 (văn bản) | Cần người chạy |
| SC-107 | Số lần sửa prompt trung bình mỗi pack giảm so với v0.1 | — | Chưa có số đo | Cần người chạy |
| SC-108 | Khối Chốt nhanh được "ok" nguyên khối ở ≥ 60% lần dùng thật | — | Chưa có số đo | Cần người chạy |
