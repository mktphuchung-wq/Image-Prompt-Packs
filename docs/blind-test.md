# Blind test preset (SC-003)

Bài kiểm này trả lời một câu hỏi: preset có tạo ảnh mà người xem dùng được và không thấy là đồ chế hàng loạt không. Nó là điều kiện để gỡ nhãn v0.1 của preset. Nguồn: `specs/001-image-prompt-pack/spec.md` (SC-003, Clarification Q5) và research R9 và 02 mục F.

## Mục đích và phạm vi

- Mỗi preset được kiểm riêng. Kết quả quyết định preset giữ, sửa hay bỏ.
- Lần đầu chạy 12 preset của thí nghiệm nhỏ nhất (R01, R02, R03, R05, R06, R08, R10, S01, S03, S05, C02, R12). Trước khi lên 1.0.0 phải kiểm đủ 28 preset (R 12, S 8, C 4, E 4). Nhóm E (biên tập/chuyên nghiệp, thêm ở v0.2) kiểm sau nhóm R, S, C.

## Chuẩn bị

1. Chọn hai model: một model của hãng lớn và một model team đang dùng.
2. Với mỗi preset và mỗi model, tạo 4 biến thể bằng cách đổi giá trị slot (người, nơi, giờ, khung, thiết bị) theo `references/presets.md`. Không đổi khung.
3. Chọn thêm một số ảnh chụp thật cùng chủ đề để trộn vào. Số lượng do người chuẩn bị quyết định và ghi lại.
4. Trộn toàn bộ ảnh, xóa nhãn nguồn và đánh lại số. Người chuẩn bị không tham gia chấm.

## Người xem và câu hỏi

- 5 người trong team, nhìn mù: không biết model, không biết ảnh là AI hay ảnh thật.
- Với mỗi ảnh, hai câu hỏi:
  1. "Bạn có dùng ảnh này cho bài hoặc listing không?"
  2. "Có thấy đồ chế hàng loạt không?"
- Ghi số người trả lời theo từng câu. Không quy thành điểm tổng hợp (research 02 mục F).

## Tiêu chí đạt

- Preset đạt khi ít nhất 4 trên 5 người trả lời "có dùng" ở câu 1 và ít nhất 4 trên 5 người trả lời "không thấy" ở câu 2. Đây là cách đọc của nhóm về SC-003 ("≥ 4/5 dùng được và không thấy đồ chế"); cần xác nhận lại với người duy trì nếu có thắc mắc.
- Preset không đạt: sửa khung hoặc bỏ trước khi gỡ nhãn v0.1.
- Ảnh chụp thật bị chê nhiều hơn ảnh AI của cùng preset: ghi lại, vì câu hỏi không đo được là đúng hay sai, chỉ đo được cảm nhận.

## Bảng ghi kết quả

Trạng thái theo vòng đời trong `data-model.md`: `v0.1 chưa test` → `đạt` | `sửa` (rồi kiểm lại) | `bỏ`.

| ID | Công cụ | Số người "dùng được" (/5) | Số người "thấy đồ chế" (/5) | Trạng thái | Ghi chú |
|---|---|---|---|---|---|
| R01 | | | | v0.1 chưa test | |
| R02 | | | | v0.1 chưa test | |
| R03 | | | | v0.1 chưa test | |
| R04 | | | | v0.1 chưa test | |
| R05 | | | | v0.1 chưa test | Chỉ dùng khi sản phẩm không có thiết kế thật |
| R06 | | | | v0.1 chưa test | Mockup: chỉ khi người dùng yêu cầu |
| R07 | | | | v0.1 chưa test | |
| R08 | | | | v0.1 chưa test | |
| R09 | | | | v0.1 chưa test | |
| R10 | | | | v0.1 chưa test | |
| R11 | | | | v0.1 chưa test | |
| R12 | | | | v0.1 chưa test | |
| S01 | | | | v0.1 chưa test | |
| S02 | | | | v0.1 chưa test | |
| S03 | | | | v0.1 chưa test | |
| S04 | | | | v0.1 chưa test | |
| S05 | | | | v0.1 chưa test | Chữ tiếng Việt dài: thêm bằng thiết kế |
| S06 | | | | v0.1 chưa test | |
| S07 | | | | v0.1 chưa test | |
| S08 | | | | v0.1 chưa test | |
| C01 | | | | v0.1 chưa test | |
| C02 | | | | v0.1 chưa test | |
| C03 | | | | v0.1 chưa test | |
| C04 | | | | v0.1 chưa test | Không có khung sinh ảnh; kiểm trôi nhân vật |
| E01 | | | | v0.1 chưa test | Nhóm E (v0.2): biên tập thời trang ngoài trời |
| E02 | | | | v0.1 chưa test | Nhóm E (v0.2): biên tập nội thất kiểu tạp chí |
| E03 | | | | v0.1 chưa test | Nhóm E (v0.2): sản phẩm không nhãn; mockup thật theo anti-slop mục 5 |
| E04 | | | | v0.1 chưa test | Nhóm E (v0.2): chân dung chuyên nghiệp |

## So sánh v0.2 với 3 ảnh cũ (SC-103)

Trạng thái: **CHƯA KIỂM CHỨNG**. Chưa có ảnh nào được tạo từ pack v0.2 và chưa có người xem. Mục này ghi giao thức để người chạy thực hiện; không ghi kết quả thay cho người chạy.


1. Bài: `tests/fixtures/05-christmas-article.md`. Ba vị trí so sánh: sofa (ảnh 2 của pack v0.2), hành lang (ảnh 3), bếp (ảnh 4). Ba ảnh cũ tương ứng được mô tả trong `tests/fixtures/06-staged-images-feedback.md`.
2. Tạo ba ảnh v0.2 từ ba prompt của pack, trên công cụ đang dùng, không đổi chữ nào trong prompt.
3. Trộn sáu ảnh (ba v0.2, ba cũ), xóa nhãn nguồn, đánh lại số. Người chuẩn bị không chấm.
4. Năm người xem mù trả lời hai câu cho từng ảnh: "Bạn có dùng ảnh này cho bài không?" và "Có thấy đồ chế hàng loạt không?"; sau đó chọn ảnh nào dùng cho bài khi so cạnh nhau.
5. Đạt khi: ít nhất 4/5 người trả lời "dùng được" và ít nhất 4/5 người trả lời "không thấy đồ chế hàng loạt", **tính riêng cho từng câu**; và đa số người chọn ảnh v0.2 khi so cạnh ảnh cũ. Không quy thành điểm tổng.

## Hero có chữ qua 7 mục QC (SC-106)

1. Tạo hero theo chế độ 3 (AI vẽ chữ, tiêu đề "Indoor Christmas Decorations") hoặc chế độ 4 trên công cụ đang dùng, năm lần.
2. Mỗi lần kiểm bằng 7 mục QC chữ trong `plugins/image-prompt-pack/skills/prompt-pack/references/text-in-image.md`.
3. Đạt khi ít nhất 4/5 lần qua đủ 7 mục.
4. Với tiêu đề tiếng Việt có dấu: thử một ảnh mẫu trước khi tạo cả loạt. Sai một dấu thì chuyển sang chế độ 2 (chèn chữ sau).

### Bảng ghi kết quả v0.2

| Mục | Số người "dùng được" (/5) | Số người "không thấy đồ chế" (/5) | Đa số chọn v0.2 | Trạng thái | Ghi chú |
|---|---|---|---|---|---|
| Pack v0.2 (sofa, hành lang, bếp) | | | | CHƯA KIỂM CHỨNG | Cần người chạy |
| Hero chế độ 3, 5 lần (QC chữ, SC-106) | | | — | CHƯA KIỂM CHỨNG | Cần người chạy; đạt khi ≥ 4/5 lần qua 7 mục |

## Sau khi có kết quả

1. Cập nhật cột Trạng thái và ghi lý do vào Ghi chú.
2. Nếu sửa khung, sửa `references/presets.md` và ghi rõ đã đổi gì. Không đổi ID.
3. Ghi thay đổi vào `CHANGELOG.md` theo phiên bản.
4. Điều kiện lên 1.0.0 (research R9): mọi preset còn giữ đều ở trạng thái `đạt`, và cài thật đã kiểm trên Claude Code và Codex.
