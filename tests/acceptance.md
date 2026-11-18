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
