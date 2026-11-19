---
description: "Task list for v0.3.0 — vùng chữ dựng sẵn + khâu khởi tạo"
---

# Tasks: Vùng chữ dựng sẵn cho hero + khâu khởi tạo theo trường hợp đặc biệt (v0.3.0)

**Input**: `specs/003-hero-copy-space/` (spec.md có Clarifications 2026-11-19, plan.md, research.md,
data-model.md, contracts/copy-space.md, contracts/first-turn.md, quickstart.md)

**Tests**: Không code test. Kiểm bằng fixture + `tests/acceptance.md` phần v0.3 + chạy thử khô + manifest.

## Đọc trước (bắt buộc)

- `CLAUDE.md`, `.specify/memory/constitution.md` (II: không script; III: không quy trình đánh số bước).
- Toàn bộ `specs/003-hero-copy-space/`. Spec 002 để hiểu nền: `specs/002-prompt-pack-optimize/spec.md`.
- Hiện trạng v0.2.1: `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` (138 dòng) và 6 file
  `references/`, `tests/acceptance.md`, `tests/fixtures/05-christmas-article.md`, `CHANGELOG.md`.
- Nguồn nghiên cứu chỉ đọc: [R03] `D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\03-plugin-test-staged-look-and-text-in-image.md`
  (bài học tương phản chữ), [R02] `...\02-prompt-strategy-preset-library.md`.

## Quy ước chung

- Repo root `C:\Users\user\orca\workspaces\Image-Prompt-Packs\Feature`. Tiếng Việt có dấu; prompt tiếng Anh;
  UTF-8 không BOM.
- Prompt mẫu đạt tự kiểm 002: 30–80 từ (ghi số từ), ≤ 5 vật gọi tên, không số chẵn/đối xứng, không từ cấm,
  câu chặn chữ tự thêm; ảnh hướng Đời thường có vật lạc đề + dấu vết người.
- Mô tả vùng chữ bằng lời. KHÔNG dùng: "bokeh", thông số máy ảnh (f/1.8, aperture), `--ar`, `--no`, `::`,
  buzzword, tên công cụ tạo ảnh/thiết kế, sơ đồ bố cục bằng ký tự.
- `SKILL.md` ≤ ~150 dòng (hiện 138): phần mới chỉ là tiêu chí ngắn; được phép rút gọn câu cũ trùng lặp; chi
  tiết đặt ở references. Mỗi reference ≤ ~300 dòng.
- Không sửa `specs/001-*`, `specs/002-*`, và spec/plan/research/data-model/contracts/quickstart của 003.
- Không `git push`. Xong task nào đánh `[X]`.

---

## Phase 1: Setup

- [X] T001 Nâng `version` lên `0.3.0` trong `plugins/image-prompt-pack/.claude-plugin/plugin.json` và `plugins/image-prompt-pack/.codex-plugin/plugin.json`; tạo thư mục `tests/runs/2026-11-19-v0.3/`
  - FR-214. Xong khi: JSON hợp lệ, hai version bằng nhau.
- [X] T002 [P] Thêm `## [0.3.0] - 2026-11-19` lên đầu `CHANGELOG.md`: Added — vùng chữ dựng sẵn cho ảnh chế độ 2 (ba cách: khoảng trống thật, làm mềm hậu cảnh nhẹ, mảng phẳng), khối "Vùng chữ" dưới prompt, cột Chữ có vị trí vùng, chế độ 3/4 dùng lại vùng; lượt đầu dừng hỏi theo 4 trường hợp đặc biệt (chữ, phong cách, nội dung đặc biệt, format mới lạ), mục Banner 4 điểm, chốt format qua bảng sửa theo số dòng; 3 fixture mới (07, 08, 09). Changed — bỏ điều kiện dừng theo số ảnh/độ dài bài (thay FR-110, FR-114 của 002); ngoại lệ có giới hạn cho tell bokeh
  - Xong khi: manifest check (quickstart 001 §1) in `OK 0.3.0` sau T001.

---

## Phase 2: Foundational

- [X] T003 [P] Sửa `plugins/image-prompt-pack/skills/prompt-pack/references/anti-slop.md`: ngay dưới bảng tell (hoặc trong ô Đối phó của dòng "Bokeh nền mờ mọi cảnh") thêm **ngoại lệ có giới hạn** (FR-205): chỉ ảnh chế độ chữ 2/3/4 được làm mềm hậu cảnh, chỉ ở phần hậu cảnh của vùng chữ, ở mức nhẹ (vật vẫn nhận ra được), chủ thể và tiền cảnh nét; ảnh chế độ 0/1 giữ "deep focus"; trỏ `references/text-in-image.md` mục "Dựng vùng chữ". Sửa mục QC "Nền không bokeh vô cớ" thêm "(trừ vùng chữ chế độ 2/3/4 theo ngoại lệ trên)"
  - Xong khi: không câu nào trong file mâu thuẫn ngoại lệ.
- [X] T004 [P] Sửa `plugins/image-prompt-pack/skills/prompt-pack/references/image-types.md`: (1) cột Chữ mặc định của Hero/OG/Thumbnail ghi thêm vị trí vùng điển hình ("2 chèn chữ sau — 1/3 trái hoặc phải"; khung dọc "dải trên/dưới"); (2) ghi chú dưới bảng: khung ngang → vùng chữ một phần ba hoặc nửa bên; khung dọc (2:3, 4:5, 9:16) → dải trên hoặc dưới; hero 16:9 cắt sang 1.91:1 thường còn vùng, sang 2:3/9:16 thì cần prompt khung dọc riêng (FR-209); (3) thêm câu định nghĩa: **format mới lạ** = loại ảnh không có trong bảng này (ví dụ carousel, before/after, chuỗi ảnh kể chuyện, ảnh so sánh, ảnh in ấn) hoặc tỉ lệ/kênh không có ở cột Tỉ lệ (FR-215 mục 4)
  - Xong khi: định nghĩa format mới lạ có mặt; mọi preset ID còn hợp lệ.

---

## Phase 3: User Story 1 — Hero ra ảnh có sẵn vùng đặt tiêu đề (P1) 🎯 MVP

**Independent Test**: quickstart 003 kịch bản I và K; acceptance v0.3-US1.

- [X] T005 [US1] Sửa `plugins/image-prompt-pack/skills/prompt-pack/references/text-in-image.md`
  - Sửa dòng chế độ 2 trong bảng "Năm chế độ": cách viết = dựng bố cục banner: vị trí chủ thể + vị trí vùng chữ + một cách tạo vùng + tông vùng + câu chặn chữ; trỏ mục mới.
  - Thêm mục **"## Dựng vùng chữ (chế độ 2, dùng lại ở 3 và 4)"** (FR-201…FR-205) theo `specs/003-hero-copy-space/research.md` R1–R3 và `contracts/copy-space.md`: (a) khoảng trống thật — gọi tên bề mặt (wall, sky, floor, tabletop, plain fabric), tông, "nothing in that area"; (b) làm mềm hậu cảnh nhẹ — "subject and foreground sharp; the background behind the left side softly blurred, low detail, shapes still recognisable" (không "bokeh", không thông số máy ảnh); (c) mảng phẳng cho hướng Minh họa. Cách chọn: (a) khi cảnh có bề mặt trơn tự nhiên; (b) khi cảnh đông hoặc hướng Biên tập; (c) hướng Minh họa. Vị trí: khung ngang một phần ba/nửa bên, khung dọc dải trên/dưới. Cỡ 35–50% khung (tiêu đề dài/tiếng Việt nhiều dòng 45–50%). Tông nền → màu chữ gợi ý (nền tối trung bình → trắng/kem; nền sáng dịu → gần đen; màu thương hiệu nếu đủ tương phản, không thì dải màu đặc) — nêu bài học [R03]: chữ trắng trên tường sáng yếu khi thu nhỏ.
  - Thay **"Ví dụ: hero chế độ 2 cùng cảnh"** bằng prompt mới theo `contracts/copy-space.md` (cách a, tường xám đậm 1/3 trái), ghi số từ (30–80) và số vật; thêm **ví dụ cách (b)** cho cảnh chợ đông (khớp fixture 07) và **ví dụ khung dọc 2:3** (vùng chữ dải trên). Mỗi ví dụ kèm khối Vùng chữ (T008 định nghĩa mẫu; có thể viết luôn ở đây theo `contracts/copy-space.md`).
  - Sửa ví dụ chế độ 3 hiện có: giữ cùng bố cục/vùng chữ với ví dụ chế độ 2 mới (FR-211) — để dùng cho US3.
  - Xong khi: mục mới có đủ a/b/c, cách chọn, vị trí ngang/dọc, cỡ, tông→màu chữ; 3 ví dụ chế độ 2 đều 30–80 từ, không chứa "bokeh"/"f/".
- [X] T006 [P] [US1] Tạo `tests/fixtures/07-crowded-hero-request.md`: HTML comment mục đích (FR-202 b, FR-203, FR-215 mục 1, SC-201) + yêu cầu tiếng Việt: "Cần ảnh hero 16:9 cho bài 'Một buổi sáng ở chợ Bến Thành' (blog du lịch), tiêu đề sẽ thêm sau. Cảnh chợ đông, nhiều sạp." — kèm 3–4 câu tóm tắt bài
- [X] T007 [US1] Thêm phần **"## v0.3 — US1: vùng chữ trong prompt"** vào `tests/acceptance.md`: kịch bản I (fixture 05 sau "ok"): prompt hero nêu vị trí chủ thể, vị trí vùng chữ, đúng một cách tạo (a/b/c), tông vùng, câu chặn chữ; 30–80 từ; ≤ 5 vật; không "bokeh"/thông số máy ảnh (FR-201…FR-206, SC-201); kịch bản K (fixture 07): chọn cách (b), chủ thể và tiền cảnh nét, hậu cảnh vùng chữ mềm nhẹ (FR-203, FR-205); ảnh trong bài (chế độ 0) vẫn "deep focus"/không làm mềm (SC-204); SC-202 ghi "đo khi tạo ảnh thật: 5 ảnh, ≥ 4/5 đặt được tiêu đề ~40% không che chủ thể, đọc được ở ~360 px"

---

## Phase 4: User Story 2 — Pack nói rõ vùng chữ (P2)

**Independent Test**: quickstart 003 kịch bản I; acceptance v0.3-US2.

- [X] T008 [US2] Bổ sung `plugins/image-prompt-pack/skills/prompt-pack/references/text-in-image.md` (sau T005) mục **mẫu khối Vùng chữ** (FR-207) đúng `contracts/copy-space.md` và `data-model.md`: Vị trí · Cỡ (% khung) · Cách tạo (a/b/c) · Tông nền → màu chữ gợi ý (mã hex nếu màu thương hiệu) · Lề an toàn ~5% · Số dòng tiêu đề dự kiến · Khi cắt khung khác ("còn nguyên ở 1.91:1" / "mất ở 2:3 → dùng prompt khung dọc") · câu cố định "Ảnh cố ý không có chữ; thêm tiêu đề bằng công cụ thiết kế."; quy tắc cột Chữ "<chế độ> — <vị trí vùng>" (FR-208)
- [X] T009 [US2] Sửa `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` (≤ ~150 dòng sau sửa): (1) tiêu chí chế độ chữ: ảnh chế độ 2 có bố cục banner với vùng chữ dựng sẵn (một trong ba cách, trỏ `references/text-in-image.md` mục Dựng vùng chữ), có khối Vùng chữ ngay dưới prompt, cột Chữ ghi vị trí vùng; làm mềm hậu cảnh chỉ trong vùng chữ chế độ 2/3/4 (FR-201…FR-208); (2) mẫu Đầu ra: thêm dòng `**Vùng chữ:** <vị trí · cỡ · cách tạo · tông → màu chữ · lề · số dòng · khi cắt khung>` và câu "Ảnh cố ý không có chữ…" dưới prompt hero chế độ 2; sửa ô Chữ ví dụ trong bảng thành "2 chèn chữ sau — 1/3 trái"
  - Xong khi: `wc -l` ≤ 150; không bước đánh số.
- [X] T010 [US2] Thêm phần **"## v0.3 — US2: khối Vùng chữ"** vào `tests/acceptance.md`: kịch bản I: mỗi ảnh chế độ 2 có khối Vùng chữ đủ 8 trường (FR-207, SC-201); cột Chữ có vị trí (FR-208); khối nói tình trạng khi cắt khung, khung dọc mất vùng thì có prompt riêng hoặc đề xuất (FR-209); khối "Đã dùng mặc định"/Chốt nhanh mô tả mặc định chữ là "chừa vùng, ảnh cố ý không có chữ" (FR-210); SC-203 ghi "đo khi dùng thật"

---

## Phase 5: User Story 4 — Lượt đầu chỉ hỏi khi có trường hợp đặc biệt (P2)

**Independent Test**: quickstart 003 kịch bản H, J, L, M; acceptance v0.3-US4.

- [X] T011 [US4] Sửa `plugins/image-prompt-pack/skills/prompt-pack/references/brief-card.md` theo `specs/003-hero-copy-space/contracts/first-turn.md` (FR-215…FR-220):
  - Thay bảng "Khi nào dừng chờ, khi nào xuất luôn" và đoạn ngưỡng 800 từ bằng bảng 3 tình huống của contract; liệt kê **4 trường hợp kích hoạt** với ví dụ cụ thể: (1) Chữ — có hero/banner/OG/thumbnail mà intake chưa chốt cách đặt chữ hoặc tiêu đề; (2) Phong cách — nội dung hợp ≥ 2 hướng, sai sẽ làm lại cả pack, không có brand guideline; (3) Nội dung đặc biệt — chỗ chờ sản phẩm, người/thương hiệu thật, chủ đề nhạy cảm, số liệu cho infographic, nhiều ngôn ngữ; (4) Format mới lạ — theo định nghĩa ở `image-types.md`. Câu rõ: số ảnh hay độ dài bài một mình không là lý do dừng.
  - Đổi bảng "Bốn mục": mục 2 thành **Banner** (chỉ khi trường hợp 1 do banner/hero/OG kích hoạt) với 4 điểm a–d và mặc định đúng FR-218 (a tiêu đề bài ≤ 6 từ, 1 dòng; b chèn chữ sau; c model đề xuất phía + cách tạo kèm lý do; d khung theo kênh); màu chữ lấy từ brand guideline, không hỏi màu/kiểu chữ/CTA/logo; mô tả bằng lời, không sơ đồ ký tự. Mục 1 hướng hình chỉ xuất hiện khi trường hợp 2 kích hoạt; mục Sản phẩm khi trường hợp 3 (chỗ chờ sản phẩm); thêm mục **Format mới lạ** khi trường hợp 4. Giữ ≤ 4 mục; Banner = 1 mục; mỗi loại 2–4 tối đa một mục (FR-220). Mục số ảnh-tỉ lệ-kênh cũ được thay bằng chốt qua bảng (dưới).
  - Mỗi mục in kèm **lý do kích hoạt** (trường hợp nào, thấy ở đâu trong bài) (FR-217).
  - Thêm quy tắc **chốt format qua bảng** (FR-219): dưới bảng Kịch bản Media có dòng "Sửa format theo số dòng, ví dụ 'ảnh 3 đổi 4:5, bỏ ảnh 5', hoặc trả 'ok'"; áp đúng dòng được sửa, giữ dòng khác.
  - Sửa mẫu "Đã dùng mặc định": dòng Chữ = "hero chừa vùng chèn tiêu đề ở <vị trí>; ảnh cố ý không có chữ" (FR-216, FR-210).
  - Sửa ví dụ điền sẵn bài Giáng sinh theo mẫu contract (mục Banner 4 điểm + mục Sản phẩm, mỗi mục có lý do).
  - Xong khi: không còn chữ "800 từ" hay "từ 4 ảnh" làm điều kiện dừng; không "Bước 1".
- [X] T012 [US4] Sửa `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` (sau T009; vẫn ≤ ~150 dòng): thay các gạch đầu dòng "Cách hỏi trước khi viết pack" bằng tiêu chí FR-215…FR-220 ngắn gọn (dừng khi và chỉ khi có trường hợp đặc biệt; 4 trường hợp nêu tên, chi tiết trỏ `references/brief-card.md`; mục Banner 4 điểm; mỗi mục có lý do + mặc định; format ảnh khác chốt qua bảng, sửa theo số dòng; "đưa luôn"/không người trả lời → xuất luôn); sửa mẫu Đầu ra lượt chờ: mục 1 Banner a–d, dòng hướng dẫn sửa theo số dòng dưới bảng
  - Xong khi: grep không thấy "800 từ", "từ 4 ảnh" như điều kiện dừng; `wc -l` ≤ 150.
- [X] T013 [P] [US4] Tạo `tests/fixtures/08-carousel-request.md`: HTML comment mục đích (FR-215 mục 4, SC-206) + yêu cầu: "Làm carousel 5 slide Instagram cho bài '5 thói quen buổi sáng cho người làm việc tại nhà', mỗi slide một thói quen, phong cách đời thường, không chữ trong ảnh."
- [X] T014 [P] [US4] Tạo `tests/fixtures/09-clear-request.md`: HTML comment mục đích (FR-216, SC-206: không có trường hợp đặc biệt → xuất luôn) + yêu cầu: "3 ảnh minh họa trong bài về thói quen buổi sáng, tỉ lệ 3:2, phong cách đời thường chụp điện thoại, không chữ, không sản phẩm." kèm 3 ý chính của bài
- [X] T015 [US4] Thêm phần **"## v0.3 — US4: lượt đầu"** vào `tests/acceptance.md`: H (fixture 05): dừng; mục Banner 4 điểm có mặc định; mục Sản phẩm (2 chỗ chờ); mỗi mục có lý do kích hoạt; không prompt; dòng sửa theo số dòng (FR-215, FR-217, FR-218, FR-219, FR-220); J ("ảnh 3 đổi 4:5, bỏ ảnh 5, còn lại ok"): chỉ áp 2 thay đổi; L (fixture 08): dừng với mục Format mới lạ có lý do; M (fixture 09): không dừng, "Đã dùng mặc định" ở đầu (FR-216); SC-206 tổng hợp H/L/M; SC-207 ghi "đo khi dùng thật"

---

## Phase 6: User Story 3 — Chế độ 3/4 dùng lại vùng chữ (P3)

**Independent Test**: quickstart 003 kịch bản N; acceptance v0.3-US3.

- [X] T016 [US3] Sửa `plugins/image-prompt-pack/skills/prompt-pack/references/text-in-image.md` mục "Chế độ 4: hai lượt" và quy tắc chế độ 3: thêm câu — đổi từ chế độ 2 sang 3/4 giữ nguyên câu bố cục và vùng chữ; tiêu đề đặt **trong** vùng đã xác định; lượt 1 của chế độ 4 = prompt chế độ 2 nguyên văn (FR-211); một dòng tiêu chí tương ứng trong `SKILL.md` nếu còn chỗ (không vượt ~150 dòng)
- [X] T017 [US3] Thêm phần **"## v0.3 — US3: dùng lại vùng chữ"** vào `tests/acceptance.md`: N (sau I, "hero cho AI vẽ luôn tiêu đề"): bố cục, chủ thể, vùng chữ giữ nguyên; tiêu đề nằm trong vùng; theo quy tắc chế độ 3 (FR-211, SC-205); chế độ 4: lượt 1 trùng prompt chế độ 2

---

## Phase 7: Example, chạy thử, polish

- [X] T018 Sửa `plugins/image-prompt-pack/skills/prompt-pack/references/example-pack.md` Ví dụ A theo v0.3: lượt 1 Chốt nhanh có mục Banner a–d (có lý do) + bảng có cột Chữ kèm vị trí + dòng sửa theo số dòng; lượt 2 hero chế độ 2 có prompt vùng chữ + khối Vùng chữ đủ trường; một câu minh họa trả lời sửa theo số dòng. Giữ Ví dụ B
- [X] T019 Chạy thử khô: worker đóng vai model, đọc `SKILL.md` + mọi reference, chạy quickstart 003 kịch bản H, I, J, K, L, M, N; lưu đầu ra + bảng chấm theo acceptance v0.3 vào `tests/runs/2026-11-19-v0.3/us1.md`, `us2.md`, `us3.md`, `us4.md` (ghi số từ từng prompt chế độ 2); trượt thì sửa references/SKILL.md (không sửa tiêu chí), chạy lại, ghi số vòng sửa
  - Xong khi: mọi tiêu chí văn bản của v0.3 đạt.
- [X] T020 [P] Cập nhật metadata: `.claude-plugin/marketplace.json` (mô tả plugin), hai `plugin.json` (`description`), `.codex-plugin/plugin.json` `interface.longDescription`, `.agents/plugins/marketplace.json` (`interface.shortDescription` của marketplace và plugin), `plugins/image-prompt-pack/skills/prompt-pack/agents/openai.yaml` (`short_description`), frontmatter `description` của `SKILL.md` — nêu: chỉ hỏi khi có trường hợp đặc biệt (chữ, phong cách, nội dung, format), hero có vùng chữ dựng sẵn. Giữ cấu trúc JSON/YAML hiện có; tiếng Anh cho description, tiếng Việt cho longDescription
- [X] T021 [P] Cập nhật `README.md` (root; phiên bản 0.3.0, cách dùng: lượt đầu chỉ hỏi khi có trường hợp đặc biệt; hero có khối Vùng chữ), `plugins/image-prompt-pack/README.md`, `CLAUDE.md` (Output contract trỏ thêm `specs/003-hero-copy-space/contracts/`; lượt đầu dừng theo trường hợp đặc biệt, không theo số ảnh), `docs/verification.md` (dòng v0.3: manifest, chạy thử khô H–N, SC-202 ảnh thật, hành vi dừng trên 3 harness — mức trung thực), `docs/blind-test.md` (mục SC-202: 5 ảnh hero, đặt tiêu đề ~40%)
- [X] T022 Rà `plugins/image-prompt-pack/skills/prompt-pack/` theo Constitution II–IV và quy ước chung (không "bokeh"/thông số máy ảnh trong prompt mẫu, không bước đánh số, không tên công cụ, `SKILL.md` ≤ ~150, reference ≤ ~300, prompt mẫu đạt tự kiểm); thêm bảng "Rà skill v0.3" (số dòng từng file) vào cuối `docs/verification.md`; thêm bảng truy vết v0.3 (FR-201…FR-220, SC-201…SC-207 → file/dòng acceptance → trạng thái) vào cuối `tests/acceptance.md`
- [X] T023 Chạy manifest check → `OK 0.3.0`; `git add -A`; commit cục bộ `feat: prompt-pack v0.3.0 (hero copy space, special-case first turn, banner brief)` với dòng cuối `Co-Authored-By: Claude Haiku 5.5 <noreply@anthropic.com>`; KHÔNG push
  - Xong khi: `git status` sạch.

---

## Dependencies & Execution Order

- T001 → T002. T003 ∥ T004 (sau T001).
- US1: T005 → T007; T006 song song.
- US2: T008 sau T005 (cùng file); T009; T010 sau T007 (cùng acceptance).
- US4: T011 sau T004; T012 sau T009 (cùng SKILL.md); T013 ∥ T014; T015 sau T010.
- US3: T016 sau T008; T017 sau T015.
- Polish: T018 sau T011, T016; T019 sau T018; T020 ∥ T021 sau T019; T022 sau đó; T023 cuối.

### Parallel Opportunities

- T003 ∥ T004 · T006 ∥ T005 · T013 ∥ T014 · T020 ∥ T021

## Implementation Strategy

1. Setup + Foundational. 2. US1 (MVP: hero có vùng chữ thật). 3. US2 (khối Vùng chữ). 4. US4 (lượt đầu).
5. US3. 6. Example, chạy thử, metadata/docs, rà, commit.

## Notes

- Spec 003 thắng khi mâu thuẫn; ghi mâu thuẫn vào báo cáo cuối.
