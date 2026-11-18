# Mức kiểm chứng: Image Prompt Pack v0.1.0

Mỗi dòng ghi một việc đã được kiểm đến mức nào, vào ngày nào, và bằng chứng là gì. Bốn mức (theo `specs/001-image-prompt-pack/research.md`):

- **ĐÃ CHẠY THẬT**: đã chạy và có kết quả đo được.
- **ĐỌC MẪU**: đã đối chiếu với repo hoặc cấu hình đang chạy trên máy.
- **ĐỌC TÀI LIỆU**: đã đối chiếu với tài liệu, chưa chạy thử.
- **CHƯA KIỂM CHỨNG**: chưa kiểm; không dùng làm căn cứ cho quyết định.

Hai lưu ý về cách kiểm:

- **Chạy khô** là worker tự đóng vai model, đọc đúng file skill và tự chấm. Người viết skill và người chấm là cùng một worker, nên chỉ bắt được lỗi rõ ràng. Không thay thế blind test hay chạy trên harness thật.
- **Cài thử** dùng thư mục cấu hình tạm (`CODEX_HOME` và `CLAUDE_CONFIG_DIR` trỏ vào thư mục scratchpad). Không sửa `~/.codex/config.toml` hay cấu hình Claude thật. Đã kiểm: `~/.claude/plugins/known_marketplaces.json` thật không có mục nào của `image-prompt-packs`.

## Bảng mức kiểm chứng

| Mục | Mức kiểm chứng | Ngày | Bằng chứng |
|---|---|---|---|
| Cấu trúc marketplace và manifest theo mẫu studio-director | ĐỌC MẪU | 2026-11-18 | Đã đọc `.claude-plugin/marketplace.json`, `.agents/plugins/marketplace.json`, hai `plugin.json` và `skills/concept/agents/openai.yaml` của studio-director (chỉ đọc) |
| Kiểm manifest (quickstart mục 1) | ĐÃ CHẠY THẬT | 2026-11-18 | Chạy lệnh PowerShell từ thư mục gốc repo: kết quả `OK 0.1.0`; bốn file JSON đọc được bằng `ConvertFrom-Json` |
| Claude Code: `claude plugin validate` cho plugin và marketplace | ĐÃ CHẠY THẬT | 2026-11-18 | Claude Code 2.1.322: cả plugin và marketplace đều "Validation passed", exit 0 |
| Claude Code: cài từ marketplace cục bộ | ĐÃ CHẠY THẬT | 2026-11-18 | Trong `CLAUDE_CONFIG_DIR` tạm: `marketplace add` thành công; `plugin install image-prompt-pack@image-prompt-packs` (scope user) thành công; `plugin list` hiện 0.1.0, enabled; `plugin details` liệt kê 1 skill `prompt-pack`, chi phí thường trực khoảng 96 token, khi gọi khoảng 1,3k token |
| Claude Code: cài từ URL Git `mktphuchung-wq/Image-Prompt-Packs` | CHƯA KIỂM CHỨNG | 2026-11-18 | Chưa đẩy lên remote (không push trong lượt này). Cần kiểm sau khi repo có trên GitHub, theo `quickstart.md` mục 2 |
| Claude Code: `claude plugin validate --profile directory` | ĐÃ CHẠY THẬT | 2026-11-18 | Còn hai mục chưa đạt, không chặn cài: thiếu LICENSE (cần quyết định giấy phép) và thiếu icon (cảnh báo). README của plugin đã có dòng cài đặt |
| Codex: cài từ marketplace cục bộ | ĐÃ CHẠY THẬT | 2026-11-18 | codex-cli 0.167.1, `CODEX_HOME` tạm: `codex plugin marketplace add <repo>` rồi `codex plugin add image-prompt-pack@image-prompt-packs`. Trạng thái "installed, enabled", 0.1.0. Cache có `SKILL.md`, `agents/openai.yaml`, bốn file trong `references/`, README và hai manifest |
| Codex: cài từ URL Git theo `quickstart.md` mục 2 | CHƯA KIỂM CHỨNG | 2026-11-18 | Chưa thêm `[marketplaces.image-prompt-packs]` vào cấu hình Codex thật; chưa kiểm đường dẫn git |
| Cập nhật phiên bản (Claude và Codex) | CHƯA KIỂM CHỨNG | 2026-11-18 | Chưa có bản thứ hai để thử cập nhật |
| ChatGPT: Skills hoặc Project | ĐỌC TÀI LIỆU | 2026-11-18 | Đường lui theo `research.md` R3 và Assumptions của spec. Chưa thử trên tài khoản ChatGPT |
| Chạy khô US1 (fixture 01 và lượt đổi ảnh 2 thành mockup) | ĐÃ CHẠY THẬT (chạy khô) | 2026-11-18 | `tests/runs/2026-11-18-codex/us1.md`: 8 trên 9 tiêu chí đạt, 1 chưa kiểm (US1-8, cần hội thoại thật). Trượt ở vòng 1 (US1-3), đạt ở vòng 2 |
| Chạy khô US2 (fixture 02, fixture 03, intake rỗng) | ĐÃ CHẠY THẬT (chạy khô) | 2026-11-18 | `tests/runs/2026-11-18-codex/us2.md`: 8 trên 8 tiêu chí đạt |
| Chạy khô US3 (fixture 04) | ĐÃ CHẠY THẬT (chạy khô) | 2026-11-18 | `tests/runs/2026-11-18-codex/us3.md`: 6 trên 7 tiêu chí đạt, 1 chưa kiểm (SC-004, cần ảnh thật) |
| Số vòng sửa SKILL/references trong lượt chạy khô | ĐÃ CHẠY THẬT | 2026-11-18 | 1 vòng: thêm một dòng tự kiểm về quy tắc prompt vào `SKILL.md`, sau khi bản nháp US1 bị chấm trượt. Cả ba run chạy lại sau sửa này |
| Chạy trên harness thật (fixture 01–04 trên Claude Code, Codex, ChatGPT) | CHƯA KIỂM CHỨNG | | Chưa thực hiện; cần người chạy trên từng harness |
| Blind test preset (SC-003) | CHƯA KIỂM CHỨNG | | Cần 5 người và ảnh AI thật. Quy trình và bảng 24 preset ở `docs/blind-test.md`; chưa có kết quả nào |
| Checklist QC trên ảnh thật (SC-008) | CHƯA KIỂM CHỨNG | | Cần ảnh được tạo từ prompt của plugin |
| SC-007: cùng intake cho cấu trúc tương đương trên ba harness | CHƯA KIỂM CHỨNG | | Cần chạy cùng intake trên Claude Code, Codex và ChatGPT |
| Rà skill theo Constitution II–IV và chuỗi cấm (T029) | ĐÃ CHẠY THẬT | 2026-11-18 | Xem bảng rà bên dưới |
| Đối chiếu FR và SC với file và tiêu chí nghiệm thu (T030) | ĐỌC TÀI LIỆU | 2026-11-18 | Bảng truy vết cuối `tests/acceptance.md` |

## Rà skill theo Constitution (T029): ĐÃ RÀ, 2026-11-18

Số dòng, đếm bằng lệnh trên file hiện tại:

| File | Số dòng | Giới hạn | Kết quả |
|---|---|---|---|
| `skills/prompt-pack/SKILL.md` | 93 | ≤ ~150 | Đạt |
| `references/anti-slop.md` | 75 | ≤ ~300 | Đạt |
| `references/presets.md` | 63 | ≤ ~300 | Đạt |
| `references/image-types.md` | 27 | ≤ ~200 | Đạt |
| `references/example-pack.md` | 81 | ≤ ~300 | Đạt |

Kiểm theo chuỗi và cấu trúc:

| Mục kiểm | Kết quả |
|---|---|
| Thủ tục đánh số ("Bước n", "Step n") | Không có. Một cụm "Bước đầu" trong `presets.md` đã đổi thành "Ban đầu" để tránh nhầm khi kiểm tự động |
| Tên tool riêng của harness, biến đường dẫn riêng (`${CLAUDE_PLUGIN_ROOT}`, `mcp__`, `WebFetch`, `Read(`, `Bash(`) | Không có |
| Chuỗi cấm (`--ar`, `--no`, `::`, `8K`, `masterpiece`, `ultra-detailed`, `stunning`, `flawless`, `hyperrealistic`) | Chỉ xuất hiện trong danh sách cấm, trong mô tả dấu hiệu "da sáp", và trong ví dụ prompt xấu có ghi rõ là ví dụ (`example-pack.md`, Ví dụ B) |
| Preset ID được trỏ trong `SKILL.md`, `image-types.md`, `example-pack.md` | 14 ID, đều có trong `presets.md` (24 ID: R01–R12, S01–S08, C01–C04) |
| Tiếng Việt có dấu | Quét các từ không dấu phổ biến (khong, duoc, nhung, cach, muc, bai, nguon, chon, cua, nhat, viet, nguoi, thuong): không có kết quả |
| Mã hóa và xuống dòng | UTF-8 không BOM, LF (kiểm bằng byte) |

Đối chiếu Constitution:

| Nguyên tắc | Kiểm | Kết quả |
|---|---|---|
| I. Bám mục tiêu cốt lõi | Không gọi API tạo ảnh. Mọi file phục vụ việc lập pack hoặc sửa prompt. Mockup chỉ khi người dùng yêu cầu | Đạt |
| II. Đơn giản trước, kỹ thuật sau | Chỉ Markdown, JSON, YAML. Không script, build hay dependency | Đạt |
| III. Dựa vào năng lực model, không viết procedure | `SKILL.md` có mục tiêu, tiêu chí, đầu ra, tri thức và ranh giới. Preset là điểm tựa, không phải biểu mẫu bắt buộc | Đạt |
| IV. Chạy được trên nhiều harness | Một thư mục skill dùng chung; manifest của hai harness là vỏ mỏng; ChatGPT dùng cùng thư mục | Đạt về cấu trúc. ChatGPT: CHƯA KIỂM CHỨNG |
| V. Cài đặt và cập nhật qua marketplace Git | Hai marketplace; `version` 0.1.0 ở hai `plugin.json` và trong `CHANGELOG.md` | Đạt về cấu trúc. URL Git: CHƯA KIỂM CHỨNG |
