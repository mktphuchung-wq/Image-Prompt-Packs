---
description: "Task list for Image Prompt Pack Plugin"
---

# Tasks: Image Prompt Pack Plugin

**Input**: Design documents from `specs/001-image-prompt-pack/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: Không viết code test (plan R8). Kiểm bằng fixture + `tests/acceptance.md` + chạy thử khô
và lệnh kiểm manifest trong quickstart.

**Organization**: Theo user story; mỗi story kiểm độc lập được.

## Đọc trước khi làm bất kỳ task nào (bắt buộc với worker)

- `.specify/memory/constitution.md` — 5 nguyên tắc. Quan trọng nhất: **II** (chỉ Markdown/JSON/YAML,
  không script, không build) và **III** (SKILL.md nêu mục tiêu, tiêu chí, hợp đồng đầu ra, tri thức —
  KHÔNG viết thủ tục "Bước 1, Bước 2…").
- `specs/001-image-prompt-pack/spec.md` (đặc biệt mục Clarifications), `plan.md`, `research.md`,
  `data-model.md`, `contracts/*.md`, `quickstart.md`.
- Nguồn nghiên cứu (chỉ đọc, không sửa):
  - **[R01]** `D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\01-landscape-tells-anti-slop.md`
  - **[R02]** `D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\02-prompt-strategy-preset-library.md`
- Mẫu cấu trúc đang chạy (chỉ đọc): `C:\Users\user\.claude\plugins\marketplaces\studio-director\`
  (manifest, `skills/*/SKILL.md`, `skills/*/agents/openai.yaml`, `README.md`, `docs/verification.md`).

## Quy ước chung cho mọi task

- Đường dẫn tính từ repo root `C:\Users\user\orca\workspaces\Image-Prompt-Packs\Feature`.
- Văn bản giải thích viết **tiếng Việt có dấu đầy đủ**; mọi câu/cụm prompt mẫu viết **tiếng Anh**.
- Encoding UTF-8 không BOM, xuống dòng LF.
- Prompt mẫu trong tri thức tuân FR-012: không `--ar`, `--no`, `::`, không buzzword (8K, masterpiece,
  ultra-detailed, stunning, flawless, hyperrealistic), diễn đạt khẳng định.
- Không tạo file ngoài danh sách trong `plan.md` > Project Structure. Không thêm script.
- Không `git push`, không tạo PR, không đổi remote. Commit cục bộ theo nhóm task được phép.
- Xong task nào đánh `[X]` task đó trong file này.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Khung repo + manifest để harness nhận diện plugin.

- [X] T001 Tạo cây thư mục theo plan: `plugins/image-prompt-pack/.claude-plugin/`, `plugins/image-prompt-pack/.codex-plugin/`, `plugins/image-prompt-pack/skills/prompt-pack/agents/`, `plugins/image-prompt-pack/skills/prompt-pack/references/`, `.claude-plugin/`, `.agents/plugins/`, `docs/`, `tests/fixtures/`
  - Xong khi: các thư mục tồn tại (file sẽ tạo ở task sau; không thêm `.gitkeep` trừ khi thư mục rỗng lúc commit).
- [X] T002 [P] Tạo `.claude-plugin/marketplace.json` và `.agents/plugins/marketplace.json` đúng mẫu trong `specs/001-image-prompt-pack/contracts/plugin-manifests.md`
  - Marketplace `name` = `image-prompt-packs`; plugin `name` = `image-prompt-pack`; owner `SEO Konic Team`; description 1 câu tiếng Anh: "Turns any content or request into a copy-ready, anti-slop image prompt pack. Does not generate images."
  - Codex: `source` = `{"source": "local", "path": "./plugins/image-prompt-pack"}`, policy `AVAILABLE`/`ON_INSTALL`, category `Productivity`. Claude: category `productivity`.
  - FR-017, FR-018. Xong khi: `Get-Content <file> -Raw | ConvertFrom-Json` không lỗi cho cả hai.
- [X] T003 [P] Tạo `plugins/image-prompt-pack/.claude-plugin/plugin.json` và `plugins/image-prompt-pack/.codex-plugin/plugin.json` theo `contracts/plugin-manifests.md`
  - `version` = `0.1.0` ở cả hai; `"skills": "./skills/"`; keywords: `image-prompt`, `prompt-pack`, `anti-slop`, `media-plan`, `content`.
  - Codex `interface`: displayName `Image Prompt Pack`; shortDescription ≤ 80 ký tự tiếng Anh; longDescription tiếng Việt 2–3 câu (đọc nội dung/log/yêu cầu → Kịch bản Media + prompt copy dùng ngay, chống slop, không tạo ảnh); developerName `SEO Konic Team`; category `Productivity`; capabilities `["Read", "Write"]`; defaultPrompt 3 câu tiếng Việt: "Làm prompt ảnh cho bài viết này.", "Bài này cần những ảnh gì? Đưa prompt luôn.", "Ảnh ra trông AI quá, sửa prompt giúp tôi.".
  - FR-017, FR-019. Xong khi: JSON hợp lệ; hai `version` bằng nhau.
- [X] T004 [P] Tạo `CHANGELOG.md` ở repo root, định dạng Keep a Changelog, mục đầu `## [0.1.0] - 2026-11-18` liệt kê: skill `prompt-pack`, 24 preset R/S/C v0.1 chưa test, 7 loại ảnh, tri thức chống slop + checklist QC, marketplace Claude + Codex
  - FR-019. Xong khi: chuỗi `[0.1.0]` có trong file.

**Checkpoint**: Lệnh kiểm manifest ở `quickstart.md` mục 1 in `OK 0.1.0`.

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Tri thức dùng chung cho mọi story. Ba file độc lập, làm song song được.

**⚠️ CRITICAL**: US1–US3 đều cần đủ ba file này.

- [X] T005 [P] Viết `plugins/image-prompt-pack/skills/prompt-pack/references/anti-slop.md` (≤ ~300 dòng) từ [R01] mục "Kết luận trước", "Phân tích" §2–§4, "Phản biện" và [R02] mục A, E (phần QC)
  - **Mục 1 Mục tiêu**: "ảnh có ý đồ, không có dấu hiệu đồ chế hàng loạt" — KHÔNG phải "không ai nhận ra là AI" (FR-010). 2–3 câu lý do lấy từ [R01] Kết luận trước 1–3 (không chép số liệu khảo sát).
  - **Mục 2 Quy tắc viết prompt chạy mọi công cụ** (FR-010, FR-012, research R5): tiếng Anh; ý quan trọng nhất ở đầu; 30–80 từ phần lớn trường hợp; diễn đạt khẳng định thay cho phủ định; không buzzword chất lượng; cụ thể hóa thay tính từ cảm xúc (chủ thể đang làm gì giữa chừng, chất liệu, nơi chốn + 2–3 vật đời thường); nguồn sáng thật + hướng; tối đa MỘT chỉ dẫn camera/thời đại thiết bị; MỘT khuyết điểm cụ thể (không chồng qualifiers); ảnh thật nói rõ "photo" + "unposed, not retouched, not cinematic"; tỉ lệ khung viết bằng lời ("vertical 4:5 frame"); chữ trong ảnh trong ngoặc kép + "appears once" + "no other text"; tham chiếu gọi "Image 1 = <role> reference"; cách cầm vật mô tả cụ thể. Khung 7 khe [R02] mục A (FORMAT, SUBJECT, SETTING, CAMERA, LIGHT, REALISM, CONSTRAINTS) ghi là **khung tư duy nội bộ, không hiển thị cho người dùng** (Clarification Q1).
  - **Mục 3 Bảng 11 tell**: cột Tell | Vì sao | Đối phó trong prompt (cụm tiếng Anh dùng ngay). Lấy đủ 11 dòng [R01] §2: da sáp; bokeh mọi cảnh; màu cam-teal/ngả vàng; quá sạch/căn giữa; ánh sáng studio sai bối cảnh; tay cầm vật sai; chữ méo/in nổi trên vải; vải/tóc/đường may vô nghĩa; ánh sáng nền khác chủ thể; quá nét/bão hòa; khuôn mặt AI lặp lại.
  - **Mục 4 Đa dạng trong pack** (FR-011): đổi người/nơi/giờ-mùa/khung giữa các ảnh; trỏ bảng slot ở `presets.md`. Cảnh báo [R01] Phản biện: "khuyết điểm cố ý" và grain đồng đều cũng thành slop mới → xoay vòng preset, kiểm soát cường độ.
  - **Mục 5 Mockup sản phẩm** (FR-020): chỉ khi người dùng báo vị trí cần mockup; Reference ảnh sản phẩm/thiết kế thật; prompt chỉ tạo bối cảnh/người/ánh sáng, không vẽ lại thiết kế/logo; ghi chú: ghép thiết kế thật sau (composite), giữ nguyên metadata AI (C2PA/IPTC) khi xuất file. Nguồn [R01] §4, [R02] mục E bước 4–5.
  - **Mục 6 Checklist QC đạt/không đạt, không chấm điểm** (FR-021): 7 mục chung — da có texture (kiểm cổ, tay); tay cầm vật đúng, đếm ngón khi phóng to; chữ đúng chính tả, không méo, không nổi trên vải; một nguồn sáng hợp lý, bóng khớp; nền không bokeh vô cớ, có vật đời thường; màu không ngả cam-teal/vàng mặc định; không lặp khuôn mặt đã dùng trong pack. 2 mục chỉ cho mockup — sản phẩm/thiết kế đúng thật, không bịa; metadata còn nguyên ở file cuối. Ghi rõ: dùng khi chẩn đoán ảnh lỗi; không bắt buộc xuất kèm mỗi pack, người dùng có thể xin.
  - KHÔNG đưa vào: bảng adapter theo model ([R02] mục D), số liệu khảo sát, quy trình sản xuất POD từng bước, thí nghiệm [R02] mục F (research R6).
  - Xong khi: đủ 6 mục; bảng tell 11 dòng; checklist 7 + 2 mục; không có chuỗi `--ar`, `--no`, `8K`, `masterpiece` ngoài câu nói "không dùng".
- [X] T006 [P] Viết `plugins/image-prompt-pack/skills/prompt-pack/references/presets.md` (≤ ~300 dòng) từ [R02] mục B, C
  - Đầu file: 2 câu — preset là điểm tựa để model tự chọn/phối, không phải biểu mẫu bắt buộc (FR-009, Constitution III); toàn bộ trạng thái `v0.1 chưa test`, kết quả blind test ghi ở `docs/blind-test.md`.
  - **Bảng slot biến thiên** từ [R02] mục B (Người, Nơi, Mùa/giờ, Khung, Thiết bị) — dùng để đa dạng các ảnh trong cùng pack (FR-011). Bỏ câu "ghi lại giá trị đã dùng để tránh lặp" giữa các phiên (plugin không lưu dữ liệu); thay bằng "không lặp trong cùng pack".
  - **Nhóm R (12)** R01–R12, **nhóm S (8)** S01–S08, **nhóm C (4)** C01–C04: mỗi preset một dòng bảng `ID | Tên | Dùng khi | Khung (tiếng Anh, [biến] trong ngoặc vuông)`. Chép khung từ [R02] mục C, chỉ sửa để hợp FR-012 (không cú pháp riêng công cụ). R06 thêm "(mockup: chỉ khi người dùng yêu cầu — xem anti-slop.md mục 5)". C02/C03 giữ cách gọi "Image 1 = character reference".
  - Cuối file: 3–5 dòng "phối preset": ví dụ hero blog dùng R02/R08, minh họa khái niệm dùng S01/S02/S06, nhân vật lặp nhiều ảnh dùng C01→C02.
  - Xong khi: đủ 24 ID duy nhất (đếm được bằng regex `^\| [RSC]\d\d `); mọi khung tiếng Anh; nhãn `v0.1 chưa test` có mặt.
- [X] T007 [P] Viết `plugins/image-prompt-pack/skills/prompt-pack/references/image-types.md` (≤ ~200 dòng) theo research R7 và `data-model.md` > Loại ảnh
  - 7 loại: (1) hero/ảnh bìa bài viết, (2) minh họa trong bài, (3) infographic/sơ đồ có chữ, (4) ảnh chia sẻ mạng xã hội/OG, (5) thumbnail/banner có tiêu đề, (6) lifestyle/UGC, (7) mockup sản phẩm — **chỉ khi người dùng yêu cầu** (FR-020).
  - Mỗi loại: Mục đích & kênh | Tỉ lệ thường dùng (hero 16:9 hoặc 3:2; OG 1.91:1 ≈ 1200×630; Pinterest 2:3; Instagram 4:5; story/reel 9:16; thumbnail 16:9; inline 4:3 hoặc 3:2) | Preset hợp (ID từ T006) | Rủi ro & cách tránh (ví dụ loại 3, 5: chữ vỡ → chữ ≤ 5 từ trong ngoặc kép hoặc chừa vùng trống "clean empty area on the left third for a headline added later").
  - Mục ngắn "Đề xuất số ảnh" (FR-006): bài dài ~1.500 từ thường 3–8 ảnh, 1 hero + minh họa theo các ý chính (H2) + 1 ảnh social; không làm ảnh cho mọi đoạn; người dùng nêu số thì theo số đó.
  - Xong khi: đủ 7 loại, mỗi loại đủ 4 trường; mọi preset ID được trỏ có thật trong `presets.md`.

**Checkpoint**: Ba file tri thức đủ; worker tự đọc lại và xác nhận không trái Clarifications Q1–Q5 trong spec.

---

## Phase 3: User Story 1 - Từ nội dung có sẵn ra Prompt Pack dùng ngay (Priority: P1) 🎯 MVP

**Goal**: Gọi skill với một bài viết (dán hoặc có sẵn trong hội thoại) → Kịch bản Media + Prompt Pack đúng `contracts/prompt-pack-output.md` mục 1.

**Independent Test**: Chạy fixture `tests/fixtures/01-blog-article.md` theo `quickstart.md` mục 3 dòng 1, 1b, 5; đạt hết tiêu chí tương ứng trong `tests/acceptance.md`.

- [X] T008 [US1] Viết `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` phần lõi (≤ ~150 dòng cho toàn file sau cả US2, US3) theo `contracts/skill-interface.md`
  - Frontmatter: `name: prompt-pack`; `description` tiếng Anh 1–2 câu: dùng khi người dùng cần biết nội dung/bài viết/landing/social cần ảnh gì và muốn prompt tạo ảnh copy dùng ngay, hoặc muốn sửa prompt vì ảnh ra trông AI/lỗi; nói rõ "does not generate images"; kèm cụm kích hoạt: "prompt ảnh", "làm ảnh cho bài này", "image prompts", "media plan", "ảnh bị AI quá", "sửa prompt ảnh".
  - Thân theo thứ tự: **Mục tiêu** (1 đoạn) → **Tiêu chí thành công** (gạch đầu dòng kiểm được, ánh xạ FR-002, FR-004–FR-014, FR-020) → **Đầu ra** (tóm tắt + mẫu ngắn khớp `contracts/prompt-pack-output.md` mục 1, 3, 4) → **Tri thức** (khi nào đọc file nào: luôn đọc `references/anti-slop.md`; `references/image-types.md` khi lập Kịch bản Media; `references/presets.md` khi chọn phong cách; `references/example-pack.md` để xem chuẩn đầu ra) → **Ranh giới** (không tạo ảnh/gọi công cụ tạo ảnh; không adapter/cú pháp riêng công cụ; mockup chỉ khi người dùng yêu cầu; không mô tả giả mạo người thật; nội dung nhạy cảm như y tế/tài chính/trẻ em chọn hình không gây hiểu lầm; áp brand guideline nếu có trong context; không gửi nội dung ra ngoài).
  - Quy tắc đầu ra phải nêu: mỗi ảnh = tên + MỘT khối prompt tiếng Anh trong code block, copy dùng ngay, tỉ lệ và ràng buộc nằm trong prompt; không hiển thị khe/preset ID bắt buộc; Reference **chỉ khi** cần tệp đính kèm (nêu tệp + vai trò, prompt gọi "Image N = …"); ghi chú phụ (alt/caption) chỉ khi hữu ích (FR-007, FR-008); tự lấy nội dung từ lịch sử/output trước khi người dùng nói "bài này/bài vừa rồi" (FR-002, US1-AS3); không tự thêm mockup (US1-AS5).
  - KHÔNG: bước đánh số kiểu thủ tục, tên tool riêng một harness, biến `${CLAUDE_PLUGIN_ROOT}`; đường dẫn tri thức dạng tương đối `references/<file>` (để ChatGPT dùng được, research R3).
  - Xong khi: frontmatter hợp lệ YAML; có đủ 5 mục; grep không thấy `Bước 1`/`Step 1`; mọi FR liệt kê ở trên có ít nhất một tiêu chí tương ứng.
- [X] T009 [P] [US1] Viết `plugins/image-prompt-pack/skills/prompt-pack/references/example-pack.md` phần **Ví dụ A — Pack hoàn chỉnh**
  - Intake giả định: tóm tắt 5–6 dòng một bài blog tiếng Việt (chủ đề khác fixture 01, ví dụ "Cách bố trí góc làm việc tại nhà trong căn hộ nhỏ").
  - Đầu ra đúng `contracts/prompt-pack-output.md` mục 1: Kịch bản Media (Nội dung, Mục tiêu, Đối tượng, Kênh, Hướng hình ảnh, Giả định, bảng 4–5 ảnh gồm hero, 2 minh họa, 1 infographic, 1 OG) + Prompt Pack (ghi chú phong cách chung + mỗi ảnh một khối `text`).
  - Mỗi prompt 30–80 từ, tuân đủ quy tắc `anti-slop.md` mục 2; ít nhất một ảnh dùng preset nhóm S để minh họa khái niệm; infographic có chữ ≤ 5 từ trong ngoặc kép hoặc vùng trống; các ảnh khác nhau về người/nơi/giờ (FR-011); KHÔNG có mục Reference (vì không cần tệp).
  - Cuối ví dụ: 3–4 dòng "Vì sao đạt" chỉ ra tell nào đã được chặn.
  - Xong khi: tự kiểm từng prompt với mục 2 + bảng tell của `anti-slop.md`, không vi phạm.
- [X] T010 [P] [US1] Tạo fixture `tests/fixtures/01-blog-article.md`: bài blog tiếng Việt ~1.500 từ (±150), chủ đề "Cách chọn áo hoodie cotton cho mùa đông", có H1, 5–7 H2, nhắc tới sản phẩm hoodie của một shop giả định nhưng **không** yêu cầu ảnh; đầu file một dòng HTML comment mô tả mục đích fixture (US1, FR-001, FR-006, FR-020 negative case)
  - Xong khi: đếm từ trong khoảng 1.350–1.650.
- [X] T011 [US1] Tạo `tests/acceptance.md` với phần **US1** (bảng: Kịch bản | Tiêu chí | FR/SC | Đạt/Không) cho quickstart dòng 1, 1b, 5
  - Dòng 1: Kịch bản Media đủ trường (FR-004, FR-005); 3–8 ảnh (FR-006); mỗi ảnh một khối prompt copy dùng ngay, không placeholder `[...]`, không cú pháp riêng công cụ, không buzzword (FR-007, FR-010, FR-012, SC-005); không mục Reference ở ảnh không cần tệp (FR-008); không tự thêm mockup dù bài nhắc sản phẩm (FR-020, US1-AS5); không tạo ảnh (FR-013); các ảnh khác nhau người/nơi/giờ (FR-011).
  - Dòng 1b: lượt sau nói "làm prompt ảnh cho bài vừa rồi" → tự lấy từ lịch sử (FR-002, US1-AS3).
  - Dòng 5: "ảnh 2 cần mockup áo hoodie của shop" → ảnh 2 có Reference ảnh sản phẩm thật, prompt không vẽ lại thiết kế/logo, ghi chú ghép + giữ metadata (FR-020).
  - Cột Đạt/Không để trống cho người chạy điền.
  - Xong khi: mỗi tiêu chí trỏ ít nhất một FR/SC.
- [X] T012 [US1] Chạy thử khô US1: worker tự đóng vai model, đọc `SKILL.md` + 4 references, xử lý `tests/fixtures/01-blog-article.md`, rồi lượt "ảnh 2 cần mockup áo hoodie của shop"; lưu đầu ra vào `tests/runs/2026-11-18-codex/us1.md` và chấm theo `tests/acceptance.md` phần US1
  - Nếu tiêu chí nào trượt: sửa `SKILL.md` hoặc references (không sửa tiêu chí), chạy lại; ghi số vòng sửa ở cuối file kết quả.
  - Ghi chú: thư mục `tests/runs/` là bằng chứng kiểm, được phép tạo (bổ sung cho plan).
  - Xong khi: mọi tiêu chí US1 (trừ 1b — cần hội thoại thật, ghi "chưa kiểm") đạt.

**Checkpoint**: US1 dùng được độc lập — đây là MVP.

---

## Phase 4: User Story 2 - Yêu cầu ngắn hoặc intake lộn xộn (Priority: P2)

**Goal**: Intake một câu hoặc log lẫn chủ đề vẫn ra pack hợp lý, có Giả định, chỉ hỏi khi thật cần.

**Independent Test**: Chạy fixture 02 và 03 theo `quickstart.md` mục 3 dòng 2, 3; đạt tiêu chí US2 trong `tests/acceptance.md`.

- [X] T013 [US2] Bổ sung `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` (sau T008, cùng file nên tuần tự) phần xử lý intake thiếu/lộn xộn, viết dạng tiêu chí, không thủ tục
  - Nhận mọi dạng intake (FR-001); tìm nội dung trong context trước khi hỏi (FR-002); intake thiếu → tự giả định hợp lý và liệt kê ở mục **Giả định** (FR-003, US2-AS1); log/lịch sử nhiều chủ đề → nói rõ đã chọn phần nào (US2-AS2); chỉ hỏi khi thiếu thông tin làm đổi hẳn kết quả, tối đa 3 câu ngắn, mỗi câu có đề xuất mặc định (US2-AS3, contracts mục 3); không tìm thấy nội dung → nói rõ và xin nội dung/đường dẫn, không bịa (Edge Case 1); người dùng nêu số ảnh/tỉ lệ → theo đúng (Edge Case 3); nội dung rất dài → đề xuất số ảnh theo cấu trúc (Edge Case 2); intake ngôn ngữ khác → giải thích theo ngôn ngữ người dùng, prompt tiếng Anh, chữ trong ảnh giữ ngôn ngữ người dùng yêu cầu.
  - Xong khi: toàn file vẫn ≤ ~150 dòng; mọi điểm trên có trong mục Tiêu chí thành công hoặc Ranh giới.
- [X] T014 [P] [US2] Tạo fixture `tests/fixtures/02-one-line-request.md`: đúng một dòng "Cần 3 ảnh cho landing page bán áo hoodie unisex, đăng Facebook ads." + HTML comment mục đích (US2-AS1, Edge Case 3: số ảnh do người dùng nêu, và có chữ "bán" nhưng KHÔNG nói mockup)
- [X] T015 [P] [US2] Tạo fixture `tests/fixtures/03-messy-log.md`: log hội thoại ~60–100 dòng giữa người dùng và trợ lý, lẫn 3 chủ đề (sửa lỗi plugin WordPress, lên lịch đăng bài, và bản nháp bài "5 thói quen buổi sáng cho người làm việc tại nhà" — chủ đề đang bàn ở cuối log) + HTML comment mục đích (US2-AS2)
- [X] T016 [US2] Bổ sung phần **US2** vào `tests/acceptance.md`
  - Dòng 2 (fixture 02): có mục Giả định (FR-003); đúng 3 ảnh (Edge Case 3); không tự thêm mockup (FR-020); nếu có hỏi thì ≤ 3 câu, mỗi câu có mặc định (US2-AS3).
  - Dòng 3 (fixture 03): nói rõ đã chọn phần "5 thói quen buổi sáng…" (US2-AS2); pack đủ theo contract.
  - Dòng thêm: intake rỗng "làm ảnh cho bài này" khi không có bài → báo không thấy nội dung, không bịa (Edge Case 1).
- [X] T017 [US2] Chạy thử khô US2 như T012 cho fixture 02, 03 và trường hợp intake rỗng; lưu `tests/runs/2026-11-18-codex/us2.md`; sửa `SKILL.md` nếu trượt
  - Xong khi: mọi tiêu chí US2 đạt.

**Checkpoint**: US1 + US2 cùng chạy được.

---

## Phase 5: User Story 3 - Sửa prompt khi ảnh ra chưa đạt (Priority: P3)

**Goal**: Nhận prompt + mô tả lỗi (hoặc ảnh) → Chẩn đoán, prompt đã sửa, 1–3 dòng Đã đổi.

**Independent Test**: Chạy fixture 04 theo `quickstart.md` mục 3 dòng 4; đạt tiêu chí US3 trong `tests/acceptance.md`.

- [X] T018 [US3] Bổ sung `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` (sau T013) chế độ sửa prompt theo `contracts/prompt-pack-output.md` mục 2
  - Tiêu chí: chẩn đoán lỗi ảnh ↔ nguyên nhân trong prompt dựa bảng tell + checklist QC của `references/anti-slop.md` (FR-015, FR-021); trả prompt đã sửa trong một code block + 1–3 dòng "Đã đổi" (US3-AS1); harness xem được ảnh → tự nhận diện tell trong ảnh, không thì dựa mô tả (US3-AS2); sửa một ảnh trong pack → chỉ trả prompt ảnh đó, giữ phong cách pack (FR-016, US3-AS3); áp được cho prompt không do plugin tạo; mỗi lượt ưu tiên thay đổi nhắm đúng lỗi, giữ phần đã ổn.
  - Xong khi: toàn file ≤ ~150 dòng; mục Tri thức nói rõ đọc checklist QC khi sửa.
- [X] T019 [P] [US3] Bổ sung `plugins/image-prompt-pack/skills/prompt-pack/references/example-pack.md` phần **Ví dụ B — Sửa prompt**: một prompt "xấu" có buzzword (ví dụ "stunning portrait of a young woman drinking coffee, 8K, ultra-detailed, cinematic, flawless skin") + mô tả lỗi "da như nhựa, nền mờ, màu cam-xanh" → Chẩn đoán (trỏ đúng 3 tell) → prompt đã sửa → Đã đổi 1–3 dòng
  - Xong khi: prompt đã sửa qua mục 2 `anti-slop.md`; ví dụ đúng contracts mục 2.
- [X] T020 [P] [US3] Tạo fixture `tests/fixtures/04-failed-image-feedback.md`: một Prompt Pack 3 ảnh ngắn (dạng đầu ra plugin) + lời người dùng "Ảnh 2 ra tay cầm cốc bị dính ngón, chữ trên cốc méo, ánh sáng như studio dù cảnh trong bếp" + HTML comment mục đích (US3-AS1, US3-AS3)
- [X] T021 [US3] Bổ sung phần **US3** vào `tests/acceptance.md`: có Chẩn đoán trỏ đúng 3 tell (tay cầm vật, chữ méo, ánh sáng studio sai bối cảnh) (FR-015, FR-021); chỉ trả prompt ảnh 2 (FR-016); prompt đã sửa mô tả cách cầm cụ thể, chữ trong ngoặc kép + "appears once" hoặc bỏ chữ, nguồn sáng thật; 1–3 dòng Đã đổi (US3-AS1); SC-004 ghi chú "đo khi chạy với ảnh thật"
- [X] T022 [US3] Chạy thử khô US3 như T012 với fixture 04; lưu `tests/runs/2026-11-18-codex/us3.md`; sửa nếu trượt
  - Xong khi: mọi tiêu chí US3 đạt.

**Checkpoint**: US1–US3 hoạt động.

---

## Phase 6: User Story 4 - Cài đặt và cập nhật qua marketplace (Priority: P4)

**Goal**: Cài/cập nhật qua link Git trên Claude Code và Codex; ChatGPT có đường lui cùng nguồn.

**Independent Test**: Lệnh kiểm manifest in `OK 0.1.0`; cài local trên Codex (và Claude Code nếu có) thấy skill `prompt-pack`.

- [X] T023 [P] [US4] Tạo `plugins/image-prompt-pack/skills/prompt-pack/agents/openai.yaml` đúng mẫu `contracts/skill-interface.md` (display_name "Prompt Pack"; short_description ≤ 80 ký tự tiếng Anh; default_prompt "Use $prompt-pack to plan the images for this article and give me copy-ready prompts."; `policy.allow_implicit_invocation: true`; không có `dependencies`)
  - Xong khi: YAML hợp lệ (đối chiếu cấu trúc với file cùng tên của studio-director).
- [X] T024 [P] [US4] Viết `README.md` ở repo root (tiếng Việt): plugin làm gì (3–4 câu, nhấn "không tạo ảnh"); ví dụ câu gọi; **Cài & cập nhật** cho Claude Code, Codex, ChatGPT đúng `quickstart.md` mục 2 (marketplace `image-prompt-packs`, plugin `image-prompt-pack`, URL `https://github.com/mktphuchung-wq/Image-Prompt-Packs.git`); cấu trúc repo ngắn; nguồn tri thức (trỏ [R01], [R02] theo đường dẫn); trạng thái preset v0.1 chưa test; cách phát hành bản mới (tăng version ở 2 `plugin.json` + mục CHANGELOG)
  - FR-017, FR-018, FR-019, SC-006.
- [X] T025 [P] [US4] Viết `plugins/image-prompt-pack/README.md` ngắn (≤ 40 dòng): mô tả plugin, tên skill trên từng harness (bảng trong `contracts/skill-interface.md`), danh sách 4 file references và vai trò
- [X] T026 [US4] Tạo `docs/verification.md` theo mẫu `studio-director/docs/verification.md` (4 mức: ĐÃ CHẠY THẬT, ĐỌC MẪU, ĐỌC TÀI LIỆU, CHƯA KIỂM CHỨNG); các dòng: kiểm manifest; cài Claude Code; cài Codex; ChatGPT Skills/Project; chạy thử khô US1/US2/US3 (trỏ `tests/runs/…`); blind test preset; checklist QC trên ảnh thật; SC-007 cross-harness. Điền mức trung thực theo những gì đã thực sự chạy, ngày 2026-11-18
- [X] T027 [US4] Chạy lệnh kiểm manifest ở `quickstart.md` mục 1 từ repo root; nếu Codex CLI có sẵn, thử cài marketplace local (trỏ `source_type = "local"` tới repo root trong một file config tạm hoặc lệnh marketplace của Codex — KHÔNG sửa `~/.codex/config.toml` thật của người dùng nếu không có cách hoàn tác sạch) và xác nhận skill `prompt-pack` được liệt kê; ghi kết quả + bằng chứng vào `docs/verification.md`
  - Xong khi: manifest check in `OK 0.1.0`; dòng cài Codex có mức trung thực (ĐÃ CHẠY THẬT kèm bằng chứng, hoặc CHƯA KIỂM CHỨNG kèm lý do).

**Checkpoint**: Plugin phân phối được.

---

## Phase 7: Polish & Cross-Cutting Concerns

- [X] T028 [P] Viết `docs/blind-test.md` từ [R02] mục F và [R01] "So what": mục đích (SC-003); chuẩn bị (preset × công cụ × 4 biến thể, trộn ảnh chụp thật); 5 người nhìn mù trả lời 2 câu "Bạn có dùng ảnh này cho bài/listing không?" và "Có thấy đồ chế hàng loạt không?"; preset đạt khi ≥ 4/5 dùng được và không thấy đồ chế; bảng ghi kết quả 24 preset (ID | công cụ | số người dùng được | số người thấy đồ chế | trạng thái `v0.1 chưa test`/`đạt`/`sửa`/`bỏ` | ghi chú); cách cập nhật `presets.md` theo kết quả; điều kiện lên 1.0.0 (research R9)
- [X] T029 Rà toàn bộ `plugins/image-prompt-pack/skills/prompt-pack/` theo Constitution II–IV và tạo bảng kết quả ở cuối `docs/verification.md` (dòng "Rà skill theo Constitution"): không bước thủ tục đánh số; không tên tool riêng harness; không biến đường dẫn riêng; `SKILL.md` ≤ ~150 dòng, mỗi reference ≤ ~300 dòng; không chuỗi cấm (`--ar`, `--no `, `::`, `8K`, `masterpiece`, `ultra-detailed`) ngoài câu liệt kê cấm; mọi preset ID được trỏ ở `image-types.md`/`example-pack.md` tồn tại; tiếng Việt có dấu đầy đủ
  - Sửa vi phạm tìm thấy rồi ghi "ĐÃ RÀ" kèm số dòng từng file.
- [X] T030 Đối chiếu từng FR-001…FR-021 và SC-001…SC-008 của `spec.md` với file/tiêu chí đã tạo; ghi bảng truy vết ngắn (FR/SC → file hoặc dòng acceptance → trạng thái) vào cuối `tests/acceptance.md`; mục nào chỉ kiểm được bằng người/ảnh thật (SC-001, SC-002, SC-003, SC-004, SC-006, SC-007, SC-008) ghi rõ "cần người chạy"
- [X] T031 Chạy lại lệnh kiểm manifest; `git add` các file thuộc plan + `tests/runs/` và commit cục bộ trên nhánh hiện tại với message `feat: image-prompt-pack plugin v0.1.0 (prompt-pack skill, R/S/C presets, Claude + Codex marketplace)` kèm dòng `Co-Authored-By` theo quy ước của harness đang chạy; KHÔNG push
  - Xong khi: `git status` sạch; `git log -1` hiện commit.

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (T001–T004)**: T001 trước; T002, T003, T004 song song sau T001.
- **Foundational (T005–T007)**: sau T001; ba task song song. Chặn mọi story.
- **US1 (T008–T012)**: sau Foundational. T008 trước T012; T009, T010 song song với T008; T011 sau T010; T012 cuối.
- **US2 (T013–T017)**: sau T008 (cùng file `SKILL.md`). T014, T015 song song; T016 sau T011 (cùng file acceptance); T017 cuối.
- **US3 (T018–T022)**: T018 sau T013; T019 sau T009 (cùng file example-pack); T020 song song; T021 sau T016; T022 cuối.
- **US4 (T023–T027)**: T023–T025 song song sau Setup; T026 sau T012/T017/T022 để ghi kết quả chạy thử; T027 sau T026.
- **Polish (T028–T031)**: T028 bất kỳ lúc nào sau T006; T029, T030 sau mọi story; T031 cuối cùng.

### User Story Dependencies

- US1: không phụ thuộc story khác — MVP.
- US2, US3: kiểm độc lập được, nhưng sửa cùng `SKILL.md`/`tests/acceptance.md` nên làm tuần tự sau US1.
- US4: manifest độc lập; phần ghi kiểm chứng cần kết quả US1–US3.

### Parallel Opportunities

- T002 ∥ T003 ∥ T004
- T005 ∥ T006 ∥ T007
- T009 ∥ T010 (cùng lúc T008)
- T014 ∥ T015; T019 ∥ T020
- T023 ∥ T024 ∥ T025 ∥ T028

---

## Parallel Example: Foundational + User Story 1

```text
Task: "T005 Viết references/anti-slop.md từ [R01], [R02]"
Task: "T006 Viết references/presets.md từ [R02] mục B, C"
Task: "T007 Viết references/image-types.md theo research R7"
# sau đó
Task: "T008 Viết SKILL.md phần lõi"
Task: "T009 Viết example-pack.md Ví dụ A"
Task: "T010 Tạo fixture 01-blog-article.md"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Phase 1 Setup → Phase 2 Foundational.
2. Phase 3 US1 → chạy thử khô T012.
3. **Dừng và xác nhận**: pack cho fixture 01 đạt `tests/acceptance.md` US1.

### Incremental Delivery

1. Setup + Foundational → tri thức sẵn sàng.
2. US1 → MVP dùng được trên Claude/Codex khi cài local.
3. US2 → chịu được intake thật lộn xộn.
4. US3 → vòng sửa prompt.
5. US4 + Polish → phân phối, kiểm chứng, commit.

---

## Notes

- [P] = khác file, không phụ thuộc task chưa xong.
- Nếu một yêu cầu trong task mâu thuẫn spec/Clarifications: spec thắng; ghi mâu thuẫn vào báo cáo cuối.
- Không đánh dấu `[X]` cho task chưa đạt tiêu chí "Xong khi".
