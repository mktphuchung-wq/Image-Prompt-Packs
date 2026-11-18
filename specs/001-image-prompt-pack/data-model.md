# Data Model: Image Prompt Pack Plugin

Plugin không lưu dữ liệu. Các "entity" dưới đây là **hình dạng nội dung** — của đầu ra cho người dùng
(Kịch bản Media, Prompt Pack) và của tri thức trong plugin (Preset, Loại ảnh, Tell, Mục QC). Không có
schema máy; model đọc và viết bằng Markdown.

## Đầu ra cho người dùng

### Intake (đầu vào, không lưu)

| Trường | Mô tả | Quy tắc |
|---|---|---|
| nguồn | dán trực tiếp / file / lịch sử hội thoại / log / output trước / yêu cầu ngắn | FR-001 |
| phần được chọn | đoạn nội dung model chọn để làm media | Phải nói rõ khi intake lẫn nhiều chủ đề (US2-AS2) |
| giả định | các điều model tự giả định khi thiếu | Bắt buộc liệt kê khi có (FR-003) |

Không tìm thấy nội dung → hỏi xin nội dung, không bịa (Edge Case 1).

### Kịch bản Media

| Trường | Bắt buộc | Quy tắc |
|---|---|---|
| tóm tắt | có | 1–3 câu: nội dung nói về gì (FR-004) |
| mục tiêu | có | |
| đối tượng | có | |
| kênh đăng | có | blog, landing, social, trang sản phẩm… |
| hướng hình ảnh | có | phong cách chung cả pack; áp brand guideline nếu có trong context |
| giả định | khi có | FR-003 |
| danh sách Vị trí ảnh | có, ≥1 | số lượng theo FR-006; tôn trọng số người dùng nêu |

### Vị trí ảnh

| Trường | Bắt buộc | Quy tắc |
|---|---|---|
| tên | có | duy nhất trong pack, ví dụ "Ảnh 1 — Hero" |
| vị trí | có | nằm ở đâu trong nội dung |
| mục đích | có | |
| loại ảnh | có | một trong các loại ở `image-types.md` |
| tỉ lệ/định dạng | có | |
| mức ưu tiên/chất lượng | có | |

Quan hệ: 1 Vị trí ảnh ↔ đúng 1 Prompt. Loại "mockup sản phẩm" chỉ xuất hiện khi người dùng yêu cầu
(FR-020).

### Prompt Pack

| Trường | Bắt buộc | Quy tắc |
|---|---|---|
| ghi chú phong cách chung | có | 1–2 câu, giữ nhất quán (FR-011) |
| danh sách Prompt | có | cùng thứ tự với Vị trí ảnh |

### Prompt

| Trường | Bắt buộc | Quy tắc |
|---|---|---|
| tên ảnh | có | khớp Vị trí ảnh |
| prompt | có | một khối liền mạch tiếng Anh, copy dùng ngay; tỉ lệ và ràng buộc nằm trong prompt; theo quy tắc FR-010, FR-012 |
| Reference | **chỉ khi** cần tệp đính kèm | liệt kê tệp + vai trò; prompt gọi đúng "Image N = <vai trò>" (FR-008) |
| ghi chú mockup | chỉ với mockup | ghép thiết kế thật sau, giữ metadata AI (FR-020c) |
| ghi chú phụ | tùy model | alt text, caption… chỉ khi giúp ích (FR-007) |

Không được có: khe cấu trúc bắt buộc, preset ID bắt buộc, cú pháp riêng một công cụ (`--ar`, `--no`,
trọng số `::`), buzzword chất lượng.

### Sửa prompt (US3)

| Trường | Bắt buộc | Quy tắc |
|---|---|---|
| chẩn đoán | có | lỗi nào trong ảnh ↔ nguyên nhân nào trong prompt; dựa bảng tell + checklist QC (FR-021) |
| prompt đã sửa | có | một khối copy dùng ngay; giữ phần đã ổn |
| thay đổi | có | 1–3 dòng: đổi gì, nhắm lỗi nào (US3-AS1) |

Sửa một ảnh trong pack: chỉ trả prompt của ảnh đó, giữ phong cách pack (FR-016).

## Tri thức trong plugin

### Preset (`references/presets.md`)

| Trường | Quy tắc |
|---|---|
| ID | `R01`–`R12`, `S01`–`S08`, `C01`–`C04`; duy nhất |
| nhóm | R ảnh thật đời sống / S phong cách thủ công / C nhân vật nhất quán |
| mục đích | dùng khi nào |
| khung | câu mẫu tiếng Anh, chỗ `[...]` là biến |
| trạng thái | `v0.1 chưa test` → `đạt blind test` / `đã sửa` / `bỏ` (theo `docs/blind-test.md`) |

Kèm bảng slot biến thiên: người, nơi, mùa/giờ, khung, thiết bị (FR-011).

### Loại ảnh (`references/image-types.md`)

| Trường | Quy tắc |
|---|---|
| tên loại | 7 loại theo research R7 |
| mục đích & kênh | |
| tỉ lệ thường dùng | |
| preset hợp | trỏ ID preset |
| rủi ro & cách tránh | ví dụ chữ vỡ → chữ ngắn hoặc chừa vùng trống |

### Tell (`references/anti-slop.md`)

| Trường | Quy tắc |
|---|---|
| tên tell | 11 dòng theo research 01 |
| vì sao xảy ra | 1 câu |
| đối phó trong prompt | câu/cụm tiếng Anh dùng được ngay |

### Mục QC (`references/anti-slop.md`)

Danh sách đạt/không đạt, không chấm điểm (FR-021). 7 mục chung + 2 mục chỉ cho mockup.

## Trạng thái

Chỉ preset có vòng đời: `v0.1 chưa test` → (blind test) → `đạt` | `sửa` → lại blind test | `bỏ`.
Plugin lên `1.0.0` khi mọi preset còn giữ đều ở trạng thái `đạt` (research R9).
