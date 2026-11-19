# Mức kiểm chứng: Image Prompt Pack (từ v0.1.0; dòng v0.2 và v0.3 ở dưới)

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
| **v0.2** — Manifest 0.2.0 (quickstart 001 §1) | ĐÃ CHẠY THẬT | 2026-11-18 | PowerShell từ thư mục gốc: `OK 0.2.0`; bốn file JSON đọc được; CHANGELOG có mục `[0.2.0]` |
| **v0.2** — Chạy khô US1 (fixture 05 sau "ok", fixture 06) | ĐÃ CHẠY THẬT (chạy khô) | 2026-11-18 | `tests/runs/2026-11-18-v0.2/us1.md`: 12 trên 12 tiêu chí đạt sau một vòng sửa (làm rõ cách đếm trang phục trong `anti-slop.md` §2; bỏ "lamp" ở một prompt) |
| **v0.2** — Chạy khô US2 (A, B, trả lời một phần, F, G, hỏi việc khác khi đang chờ) | ĐÃ CHẠY THẬT (chạy khô) | 2026-11-18 | `us2.md`: V2-US2-1…9 đạt; V2-US2-7 chỉ kiểm mức bảng và trạng thái mặc định; V2-US2-10 là mô phỏng |
| **v0.2** — Chạy khô US3 (chế độ 2, chế độ 3, tiếng Việt có dấu, chế độ 4) | ĐÃ CHẠY THẬT (chạy khô) | 2026-11-18 | `us3.md`: V2-US3-1…7 đạt ở mức văn bản; QC chữ kiểm trên văn bản prompt; SC-106 cần người chạy |
| **v0.2** — Chạy khô US4 (B, D, fixture 01, fixture 03) | ĐÃ CHẠY THẬT (chạy khô) | 2026-11-18 | `us4.md`: V2-US4-1…5 đạt; "Reference ảnh sản phẩm thật" là yêu cầu trong pack, chưa có ảnh để kiểm |
| **v0.2** — Dừng chờ Chốt nhanh và "ok" trên Claude Code, Codex, ChatGPT (SC-104) | CHƯA KIỂM CHỨNG | | Chưa chạy trên harness thật; cần người chạy `quickstart.md` mục 3 (kịch bản A, B, F, G) trên từng harness |
| **v0.2** — Mockup có xác nhận trên harness thật (SC-105) | CHƯA KIỂM CHỨNG | | Chưa chạy; cần người chạy kịch bản B và D |
| **v0.2** — Blind test so với 3 ảnh cũ (SC-103) | CHƯA KIỂM CHỨNG | | Giao thức ở `docs/blind-test.md`; cần 5 người và ảnh thật |
| **v0.2** — Hero có chữ qua 7 mục QC (SC-106) | CHƯA KIỂM CHỨNG | | Cần 5 lần tạo ảnh thật; giao thức ở `docs/blind-test.md` |
| **v0.2** — Số lần sửa prompt trên mỗi pack giảm so với v0.1 (SC-107) | CHƯA KIỂM CHỨNG | | Cần đo trên cùng bài với công cụ thật |
| **v0.2** — Tỉ lệ "ok" nguyên khối ≥ 60% (SC-108) | CHƯA KIỂM CHỨNG | | Cần đo khi dùng thật; dưới 60% thì xem lại mặc định |
| **v0.2** — Rà skill theo Constitution II–IV và chuỗi cấm (T028) | ĐÃ CHẠY THẬT | 2026-11-18 | Xem bảng "Rà skill v0.2" cuối file |
| **v0.3** — Manifest 0.3.0 (quickstart 001 §1) | ĐÃ CHẠY THẬT | 2026-11-19 | PowerShell từ thư mục gốc: `OK 0.3.0`; bốn file JSON đọc được; CHANGELOG có mục `[0.3.0]`. Chạy lại sau commit ở T023 |
| **v0.3** — Chạy khô H–N (I, K, N; H, J, L, M) | ĐÃ CHẠY THẬT (chạy khô) | 2026-11-19 | `tests/runs/2026-11-19-v0.3/us1.md` đến `us4.md`: US1 10/10 đạt (1 mục cần người chạy); US2 7/7; US3 5/5; US4 11/11 (1 mục cần người chạy). Số vòng sửa: 1 (mục Banner-b thiếu "ảnh cố ý không có chữ"; quy tắc chế độ 3 chưa nói giữ dưới 80 từ). Cùng một worker vừa đóng vai model vừa viết skill, nên chỉ bắt được lỗi rõ |
| **v0.3** — Số từ prompt chế độ 2 trong chạy khô | ĐÃ CHẠY THẬT (chạy khô) | 2026-11-19 | Đếm bằng PowerShell: hero 74, ảnh chia sẻ 76, hero cách (b) 76, hero chế độ 3 sau sửa 74 (bản nháp 94, trượt). Ví dụ trong `text-in-image.md`: 78 (chế độ 3), 64, 77, 67 (chế độ 2) |
| **v0.3** — Hero có vùng chữ, 5 ảnh thật (SC-202) | CHƯA KIỂM CHỨNG | | Cần 5 ảnh thật; giao thức ở `docs/blind-test.md` |
| **v0.3** — Dừng chờ theo trường hợp đặc biệt và "ok" trên Claude Code, Codex, ChatGPT (SC-206) | CHƯA KIỂM CHỨNG | | Chạy khô đã kiểm văn bản H, L, M. Chưa chạy trên harness thật; cần người chạy kịch bản H, J, L, M trên từng harness |
| **v0.3** — Ảnh chế độ 0 không tăng bokeh vô cớ so với v0.2.1 (SC-204) | CHƯA KIỂM CHỨNG | | Chạy khô chỉ kiểm văn bản; cần so ảnh thật theo checklist QC |
| **v0.3** — Người dùng không báo "hero thiếu chữ" (SC-203) | CHƯA KIỂM CHỨNG | | Cần lượt thử với người dùng thật |
| **v0.3** — Chốt trong một câu trả lời ở ≥ 80% lần dùng thật (SC-207) | CHƯA KIỂM CHỨNG | | Đo khi dùng thật |
| **v0.3** — Rà skill theo Constitution II–IV và chuỗi cấm (T022) | ĐÃ CHẠY THẬT | 2026-11-19 | Xem bảng "Rà skill v0.3" cuối file |

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

## Rà skill v0.2 (T028): ĐÃ RÀ, 2026-11-18

Số dòng đếm bằng `wc -l` trên file hiện tại (phiên bản 0.2.0):

| File | Số dòng | Giới hạn | Kết quả |
|---|---|---|---|
| `skills/prompt-pack/SKILL.md` | 138 | ≤ ~150 | Đạt |
| `references/anti-slop.md` | 107 | ≤ ~300 | Đạt |
| `references/brief-card.md` | 75 | ≤ ~150 | Đạt |
| `references/text-in-image.md` | 71 | ≤ ~200 | Đạt |
| `references/presets.md` | 77 | ≤ ~300 | Đạt |
| `references/image-types.md` | 27 | ≤ ~200 | Đạt |
| `references/example-pack.md` | 101 | ≤ ~300 | Đạt |

Kiểm theo chuỗi, cấu trúc và mã hóa:

| Mục kiểm | Kết quả |
|---|---|
| Thủ tục đánh số ("Bước n", "Step n") | Không có. Các danh sách đánh số là lựa chọn của Chốt nhanh và mục của đầu ra, không phải bước làm việc |
| Tên tool hoặc harness, biến đường dẫn riêng (`${CLAUDE_PLUGIN_ROOT}`, `mcp__`, `Read(`, `Bash(`, `WebFetch`, Claude, Codex, ChatGPT) | Không có trong SKILL và references |
| Tên công cụ tạo ảnh hoặc thiết kế (Midjourney, DALL·E, GPT, Gemini, Canva, Figma, Photoshop, và các tên tương tự) | Không có. Một khớp nhầm với chuỗi "buckling" đã được loại trừ |
| Đường dẫn cá nhân (ổ đĩa, `/Users/`, `/home/`) | Không có |
| Chuỗi cấm (`--ar`, `--no`, `::`, 8K, masterpiece, ultra-detailed, stunning, flawless, hyperrealistic) | Chỉ xuất hiện trong danh sách cấm (`anti-slop.md` §2), trong bảng dấu hiệu nêu tên từ làm ví dụ (§3), và trong Ví dụ B là prompt sai có ghi rõ |
| Từ cấm đứng một mình (cozy, welcoming, lived-in, natural, authentic, realistic, imperfect, charming, "slightly imperfect", "subtle imperfections") trong prompt mẫu | Không có trong prompt mẫu. Chỉ xuất hiện trong danh sách cấm và trong Ví dụ B là prompt sai |
| Preset ID trỏ từ skill | 28 ID đều tồn tại trong `presets.md`; không có ID trỏ sai |
| Prompt mẫu đạt tự kiểm (ghi số từ) | Ví dụ A (pack): 78, 69, 60, 78, 68 từ; Ví dụ B (sửa): 77 từ; `text-in-image.md`: 80 (chế độ 3), 63 (chế độ 2); khung nhóm E: 62–66 từ |
| Tiếng Việt có dấu | Kiểm theo byte: các khớp không dấu đều là từ không dấu đúng chính tả (ví dụ "nội dung", "chân dung", "cung cấp") |
| Mã hóa và xuống dòng | UTF-8 không BOM, LF (kiểm bằng byte) |
| Quy tắc v0.1 đã thay ("tối đa 3 câu hỏi") | Không còn trong bất kỳ file nào của skill |

Đối chiếu Constitution (v0.2):

| Nguyên tắc | Kiểm | Kết quả |
|---|---|---|
| II. Đơn giản trước | Chỉ Markdown; không script, không build | Đạt |
| III. Không viết procedure | Chốt nhanh và tự kiểm viết thành tiêu chí; không "Bước 1…"; mẫu đầu ra là hợp đồng, không phải quy trình | Đạt |
| IV. Chạy trên nhiều harness | Không có tên harness trong skill; có đường lui khi không có người trả lời (xuất luôn, ghi mặc định ở đầu) | Đạt về cấu trúc. Hành vi dừng chờ trên Claude Code, Codex, ChatGPT: CHƯA KIỂM CHỨNG |

## Rà skill v0.3 (T022): ĐÃ RÀ, 2026-11-19

Số dòng đếm bằng PowerShell trên file hiện tại (phiên bản 0.3.0):

| File | Số dòng | Giới hạn | Kết quả |
|---|---|---|---|
| `skills/prompt-pack/SKILL.md` | 144 | ≤ ~150 | Đạt |
| `references/anti-slop.md` | 109 | ≤ ~300 | Đạt |
| `references/brief-card.md` | 103 | ≤ ~300 | Đạt |
| `references/text-in-image.md` | 137 | ≤ ~300 | Đạt |
| `references/presets.md` | 77 | ≤ ~300 | Đạt (không đổi trong v0.3) |
| `references/image-types.md` | 31 | ≤ ~300 | Đạt |
| `references/example-pack.md` | 110 | ≤ ~300 | Đạt |

Kiểm theo chuỗi, cấu trúc và mã hóa:

| Mục kiểm | Kết quả |
|---|---|
| Thủ tục đánh số ("Bước n", "Step n") | Không có. Năm dòng đánh số ngoài khối mã là danh sách điều kiện (bốn trường hợp kích hoạt trong `brief-card.md`) và mẫu khối Chốt nhanh; không phải bước làm việc |
| Tên harness, tên tool và biến đường dẫn (`${CLAUDE_PLUGIN_ROOT}`, `mcp__`, `WebFetch`, `Read(`, `Bash(`, Claude, Codex, ChatGPT) | Không có trong skill và references |
| Tên công cụ tạo ảnh hoặc thiết kế (Midjourney, DALL·E, Gemini, Canva, Figma, Photoshop và tên tương tự) | Không có |
| Chuỗi cấm trong khối prompt (`--ar`, `--no`, `::`, 8K, masterpiece, ultra-detailed, stunning, flawless, hyperrealistic, bokeh, f/) | Không có |
| Thông số máy ảnh trong khối prompt mẫu | Đã bỏ "50mm lens look" ở ảnh 3 của Ví dụ A (`example-pack.md`). Còn lại trong `presets.md` (R03 "50mm", E04 "85mm", R10 "1/60s"): thuộc v0.1/v0.2, nằm ngoài danh sách file được sửa của v0.3 nên không đổi; ghi nhận để xử lý ở bản sau |
| Từ cấm đứng một mình trong khối prompt mẫu (cozy, natural, realistic, ...) | Không có |
| Prompt mẫu đạt tự kiểm (ghi số từ) | Ví dụ A: 75, 69, 55, 77, 67 từ. Ví dụ B: 77 từ (bản sửa). `text-in-image.md`: 78 (chế độ 3), 64, 77, 67 (chế độ 2) |
| Tiếng Việt có dấu | Quét các từ không dấu phổ biến ngoài khối mã: không có kết quả |
| Mã hóa và xuống dòng | UTF-8 không BOM, LF (kiểm bằng byte) cho các file skill |

Đối chiếu Constitution (v0.3):

| Nguyên tắc | Kiểm | Kết quả |
|---|---|---|
| II. Đơn giản trước | Chỉ Markdown; không script, không build | Đạt |
| III. Không viết procedure | Chốt nhanh và tự kiểm viết thành tiêu chí; mẫu đầu ra là hợp đồng; không có "Bước n" | Đạt |
| IV. Chạy trên nhiều harness | Không có tên harness trong skill; lượt đầu có đường lui "đưa luôn" hoặc không có người trả lời | Đạt về cấu trúc. Hành vi dừng trên Claude Code, Codex, ChatGPT: CHƯA KIỂM CHỨNG |
