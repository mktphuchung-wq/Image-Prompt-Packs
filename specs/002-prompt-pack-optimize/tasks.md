---
description: "Task list for Prompt Pack v0.2"
---

# Tasks: Prompt Pack v0.2 — chống ảnh dàn dựng, chế độ chữ, Chốt nhanh

**Input**: `specs/002-prompt-pack-optimize/` (spec.md, plan.md, research.md, data-model.md, contracts/, quickstart.md)

**Tests**: Không viết code test (Constitution II). Kiểm bằng fixture + `tests/acceptance.md` phần v0.2 +
chạy thử khô + lệnh kiểm manifest.

## Đọc trước khi làm bất kỳ task nào (bắt buộc)

- `CLAUDE.md` (repo root) và `.specify/memory/constitution.md`. Quan trọng nhất: **II** (chỉ
  Markdown/JSON/YAML, không script) và **III** (`SKILL.md` viết mục tiêu, tiêu chí, hợp đồng đầu ra, tri
  thức — KHÔNG thủ tục "Bước 1, Bước 2…").
- `specs/002-prompt-pack-optimize/spec.md` (mục Clarifications: hướng hình do model chọn; hero mặc định
  chèn chữ sau), `plan.md`, `research.md`, `data-model.md`, `contracts/*.md`, `quickstart.md`.
- Hiện trạng v0.1.0: toàn bộ `plugins/image-prompt-pack/skills/prompt-pack/` (SKILL.md + 4 references),
  `tests/acceptance.md`, `docs/verification.md`, `docs/blind-test.md`, `CHANGELOG.md`.
- Nguồn nghiên cứu (chỉ đọc, không sửa):
  - **[R03]** `D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\03-plugin-test-staged-look-and-text-in-image.md` — nguồn chính của v0.2.
  - **[R01]** `D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\01-landscape-tells-anti-slop.md`
  - **[R02]** `D:\SEO Konic\Researcher\ai-image-gen-anti-slop\outputs\02-prompt-strategy-preset-library.md`
- Bài thật của lượt test (chỉ đọc): `C:\Users\user\Downloads\PYW_How To.md`.

## Quy ước chung

- Repo root: `C:\Users\user\orca\workspaces\Image-Prompt-Packs\Feature`. Mọi đường dẫn tính từ đây.
- Văn bản tiếng Việt có dấu đầy đủ; prompt mẫu tiếng Anh. UTF-8 không BOM, LF.
- Prompt mẫu trong tri thức tuân **tiêu chí tự kiểm v0.2**: 30–80 từ; ≤ 5 vật gọi tên; không số lượng
  chẵn hay bố trí đối xứng; ảnh đời thường có 1 vật lạc đề + 1 dấu vết người; không từ cấm đứng một mình
  (cozy, welcoming, lived-in, natural, authentic, realistic, imperfect, charming, "slightly imperfect",
  "subtle imperfections"); ảnh không chữ có câu chặn chữ tự thêm; không `--ar`, `--no`, `::`, không
  buzzword (8K, masterpiece, ultra-detailed, stunning, flawless, hyperrealistic).
- Không nêu tên công cụ tạo ảnh hay công cụ thiết kế cụ thể trong plugin; chỉ nói "công cụ bạn đang dùng"
  / "công cụ thiết kế".
- `SKILL.md` ≤ ~150 dòng; mỗi reference ≤ ~300 dòng.
- Không sửa `specs/001-image-prompt-pack/**` và các file spec/plan/research/data-model/contracts của 002.
- Không `git push`, không đổi remote. Commit cục bộ ở task cuối.
- Xong task nào đánh `[X]` task đó trong file này.

---

## Phase 1: Setup

- [X] T001 Nâng version lên `0.2.0` trong `plugins/image-prompt-pack/.claude-plugin/plugin.json` và `plugins/image-prompt-pack/.codex-plugin/plugin.json` (chỉ đổi trường `version`), tạo thư mục `tests/runs/2026-11-18-v0.2/`
  - FR-130. Xong khi: hai file JSON hợp lệ, cùng `"version": "0.2.0"`.
- [X] T002 [P] Thêm mục `## [0.2.0] - 2026-11-18` lên đầu `CHANGELOG.md` (trên mục 0.1.0), nhóm Added/Changed: Chốt nhanh (`references/brief-card.md`); chế độ chữ + QC chữ (`references/text-in-image.md`); tiêu chí tự kiểm prompt; bảng đa dạng cấp pack; 4 tell mới (15 tell); nhóm preset E (4); mockup chỉ hỏi xác nhận khi bài nhắc sản phẩm; fixture 05, 06. Mục "Thay đổi so với 0.1.0": cách hỏi (thay FR-002/003 của 001), đa dạng (FR-011), điều kiện mockup (FR-020), chính sách chữ; mục Giả định ở cuối pack được thay bằng khối "Đã dùng mặc định" ở đầu
  - FR-130. Xong khi: lệnh kiểm manifest (quickstart 001 §1) in `OK 0.2.0` sau T001.

---

## Phase 2: Foundational (tri thức dùng chung)

- [X] T003 Sửa `plugins/image-prompt-pack/skills/prompt-pack/references/anti-slop.md` (giữ ≤ ~300 dòng)
  - **§2 Quy tắc viết prompt** — thêm tiểu mục **"Tự kiểm trước khi xuất"** (FR-101…FR-106) dạng danh sách kiểm được, không đánh số bước: 30–80 từ (vượt chỉ khi nhiều chủ thể, lý do ghi trong Kịch bản Media); kể một khoảnh khắc, không viết thành danh mục vật; ≤ 5 vật gọi tên; tránh số chẵn và bố trí cách đều/đối xứng, chỉ nêu số khi có ý nghĩa; ảnh hướng Đời thường: ≥ 1 vật lạc chủ đề chọn theo ngữ cảnh bài (không lặp cùng một vật cho mọi ảnh) + 1 dấu vết con người cụ thể (cốc uống dở, việc đang làm dở); ảnh không chữ: nói cụ thể vật nền + câu kiểu "plain unlabeled jars and boxes, no readable text anywhere". Danh sách **từ cấm khi đứng một mình**: cozy, welcoming, lived-in, natural, authentic, realistic, imperfect, charming, "slightly imperfect", "subtle imperfections" — mỗi từ kèm cách thay bằng chi tiết cụ thể (ví dụ "lived-in" → "a jumper thrown over the armrest"). Sửa câu về chữ dài ở §2 thành trỏ `references/text-in-image.md`. Thêm một câu: hướng Biên tập/chuyên nghiệp không bắt buộc vật lạc đề và dấu vết dùng nhưng giữ mọi tiêu chí còn lại (FR-116).
  - **§3** — đổi tiêu đề thành "Mười lăm dấu hiệu…", thêm 4 dòng theo [R03] mục A và P4 (FR-109), mỗi dòng có cột Vì sao + Đối phó trong prompt: (1) đối xứng, đồ thành cặp — "two wreaths, two mugs" khiến model kiểm kê và xếp đều → bỏ số chẵn, đặt lệch, cho một món khác biệt; (2) thuần chủ đề, không vật lạc đề → một vật đời thường không thuộc chủ đề; (3) không dấu vết sử dụng → một dấu vết cụ thể; (4) model tự thêm chữ hoặc vật (tuyết ngoài cửa, nến, bảng "Hot Cocoa") → nói cụ thể vật nền + câu chặn chữ. Ghi chú dưới bảng: 4 dòng mới là suy luận từ một lượt test, chưa đo.
  - **§4 Đa dạng** — viết lại thành "Đa dạng cấp pack" (FR-107, FR-108): các cột bắt buộc trong bảng Kịch bản Media (Hướng, Khung, Độ cao máy, Ánh sáng, Thời tiết/giờ, Người, Chữ — giá trị theo `specs/002-prompt-pack-optimize/data-model.md`); quy tắc pack ≥ 4 ảnh: không hai ảnh liền nhau trùng cả Khung + Độ cao máy + Ánh sáng; ≥ 1 ảnh ánh lạnh hoặc u ám; ≥ 2 ảnh có tay hoặc người; không loại khung nào chiếm quá nửa; pack 1–3 ảnh áp theo khả năng. Giữ câu cảnh báo "khuyết điểm cố ý cũng thành slop mới".
  - **§5 Mockup** — đổi điều kiện (FR-126…FR-128): khi intake nhắc sản phẩm hoặc có chỗ chờ sản phẩm, hỏi xác nhận ở mục 3 Chốt nhanh, mặc định "không"; giữ "không" → pack không có prompt mockup, không mục "Bonus" hay prompt sản phẩm dưới bất kỳ tên nào; chọn "có" hoặc người dùng tự yêu cầu → Reference ảnh sản phẩm thật bắt buộc, nhãn "chờ sản phẩm xác minh", giữ quy tắc trung thực cũ (AI chỉ tạo bối cảnh/người/ánh sáng, ghép thiết kế thật sau, giữ metadata AI).
  - **§6 QC** — thêm một dòng: ảnh có chữ kiểm thêm QC chữ ở `references/text-in-image.md`.
  - Xong khi: bảng §3 có đúng 15 dòng dữ liệu; §2 có danh sách từ cấm; §4 có đủ 4 quy tắc FR-108; không còn câu "Mockup chỉ khi người dùng yêu cầu" mâu thuẫn §5 mới.
- [X] T004 [P] Tạo `plugins/image-prompt-pack/skills/prompt-pack/references/text-in-image.md` (≤ ~200 dòng) từ [R03] mục B-P1, mục C và Kết luận 3–4
  - Mở đầu 2 câu: mỗi ảnh có đúng một chế độ chữ, ghi ở cột Chữ của Kịch bản Media (FR-117); **mặc định: hero, ảnh chia sẻ (OG) và thumbnail = chế độ 2 chèn chữ sau; ảnh khác = chế độ 0 không chữ** (FR-123); chế độ 3 và 4 chỉ khi người dùng chọn.
  - Bảng 5 chế độ `Chế độ | Khi dùng | Cách viết prompt` theo [R03] P1: 0 không chữ (FR-105); 1 chữ trong cảnh — tối đa 3 từ, ngoặc kép, "appears once", viết tay hay in, nằm trên vật gì (FR-118); 2 chèn chữ sau — chủ thể ở một phần, vùng trống có vị trí rõ, tương phản trung bình hoặc tối, không chữ trong ảnh, ghi chú "thêm tiêu đề bằng công cụ thiết kế" (FR-119); 3 AI vẽ chữ (FR-120); 4 hai lượt — lượt 2 dùng đúng câu `Image 1 = approved scene. Add the headline only; keep everything else unchanged.`, Reference của lượt 2 là ảnh lượt 1 (FR-121).
  - Mục **Quy tắc chế độ 3** (FR-120): tiêu đề ≤ ~6 từ, 1–2 dòng, dòng phụ chỉ khi cần; chép đúng chuỗi trong ngoặc kép; kiểu hoa/thường; kiểu chữ mô tả bằng đặc điểm ("bold condensed sans-serif"), không tên font; màu (mã hex nếu là màu thương hiệu); vị trí + canh lề; cỡ tương đối (ví dụ "about 40% of the frame width"); **bề mặt nền tương phản phía sau chữ** (tường trung tính tối hoặc dải màu đặc) — bài học: chữ trắng trên tường sáng yếu khi thu nhỏ; lề an toàn ~5% mỗi cạnh; luôn kèm "the headline appears once; no other text anywhere".
  - Mục **Tiếng Việt có dấu** (FR-122): ở chế độ 3/4, pack cảnh báo thử một ảnh mẫu trên công cụ đang dùng; sai một dấu → chuyển sang chế độ 2.
  - Mục **SEO** (FR-125): chữ trong ảnh không thay H1 và alt; ảnh có chữ phục vụ web vẫn có gợi ý alt mô tả.
  - Mục **QC chữ đạt/không đạt** (FR-124), đúng 7 mục: đúng chính tả từng ký tự; đúng dấu tiếng Việt; xuất hiện một lần; đọc được khi thu nhỏ còn khoảng 360 px bề rộng; đủ tương phản; không có chữ lạ trên biển/sách/bao bì; nằm trong lề an toàn.
  - Một ví dụ prompt chế độ 3 cho hero "Indoor Christmas Decorations" dựa trên [R03] mục C **đã áp các chỉnh sửa [R03] gợi ý** ("plain mid-grey wall" thay "plain pale wall", "lights spilling out of the box in loops" thay "tangled lights"), ≤ 80 từ nếu được (ghi số từ). Một ví dụ chế độ 2 cùng cảnh (không chữ, vùng trống bên trái).
  - Xong khi: đủ 5 chế độ, 7 mục QC, 2 ví dụ; không tên công cụ cụ thể.
- [X] T005 [P] Tạo `plugins/image-prompt-pack/skills/prompt-pack/references/brief-card.md` (≤ ~150 dòng) theo `specs/002-prompt-pack-optimize/contracts/brief-card.md` và [R03] mục D
  - **Khi nào có khối, khi nào dừng** (FR-110, FR-114): bảng 3 tình huống y như contract; ngưỡng "bài dài" ≈ ≥ 800 từ hoặc ≥ 4 mục lớn; ≥ 4 ảnh dự kiến → dừng chờ, lượt đầu không có prompt; 1–3 ảnh / "đưa luôn" / không người trả lời → xuất luôn, khối "Đã dùng mặc định" ở đầu (thay mục Giả định cuối).
  - **4 mục** (FR-111): bảng `Mục | Vì sao hỏi | Mặc định | Bỏ qua khi` theo [R03] mục D, với các điều chỉnh đã chốt: mục 1 Hướng hình — **model chọn mặc định theo loại bài và kênh, ghi 1 câu lý do** (FR-116); 3 hướng chuẩn: Đời thường (chụp điện thoại, dấu vết dùng) · Biên tập/chuyên nghiệp (tạp chí, thời trang, sản phẩm chỉn chu — preset nhóm E) · Minh họa thủ công (nhóm S); có thể phối theo ảnh; gợi ý ánh xạ: how-to/đời sống → Đời thường; thời trang, mỹ phẩm, thương hiệu cao cấp, landing bán hàng → Biên tập; khái niệm trừu tượng → Minh họa. Mục 2 Chữ — mặc định hero/OG/thumbnail chèn chữ sau, ảnh khác không chữ (FR-123). Mục 3 Sản phẩm — chỉ khi intake nhắc sản phẩm hoặc có chỗ chờ, nêu số chỗ + vị trí, mặc định "không" (FR-126). Mục 4 Số ảnh-tỉ lệ-kênh — theo `image-types.md`.
  - **Quy tắc** (FR-112, FR-113, FR-115): chỉ in mục chưa quyết, đánh số lại liên tục; mỗi mục 1 mặc định + ≤ 3 lựa chọn mô tả bằng kết quả nhìn thấy; không preset ID, tên công cụ, tham số; "ok" → pack theo mặc định không hỏi thêm; trả lời một phần → mục không nhắc theo mặc định; người dùng hỏi việc khác khi đang chờ → không tự xuất pack; đổi một mục sau khi có pack → chỉ viết lại prompt bị ảnh hưởng.
  - **Mẫu khối** đúng contract, và một ví dụ điền sẵn cho bài Giáng sinh (4 mục; mục 3 nêu 2 chỗ chờ sản phẩm: sofa, phòng ngủ). Một mẫu "Đã dùng mặc định" ngắn.
  - Xong khi: không có câu dạng "Bước 1/Step 1"; đủ 4 mục và 3 tình huống.
- [X] T006 [P] Sửa `plugins/image-prompt-pack/skills/prompt-pack/references/presets.md`
  - Thêm **Nhóm E: biên tập/chuyên nghiệp (4)** (research R3), cùng định dạng bảng `ID | Tên | Dùng khi | Khung`, khung tiếng Anh 30–80 từ, [biến] trong ngoặc vuông, ≤ 5 vật, nguồn sáng thật, một cue camera, không buzzword, không từ cấm: E01 fashion editorial ngoài trời ánh tự nhiên (người mặc trang phục cụ thể chất liệu, đang bước/xoay, ánh chiều nghiêng); E02 interior editorial kiểu tạp chí nhà cửa (một góc phòng, ánh cửa sổ, một vật cá nhân để lại); E03 product/still-life editorial bóng cứng (sản phẩm không nhãn trên bề mặt chất liệu cụ thể, nắng gắt tạo bóng rõ — mockup thật vẫn theo anti-slop §5); E04 chân dung chuyên nghiệp/doanh nghiệp (môi trường làm việc thật, ánh cửa sổ, tư thế đang nói/nghe). Ghi trạng thái `v0.1 chưa test`.
  - Bảng slot đa dạng: thêm hàng **Nhiệt độ ánh sáng** (ấm tungsten tối, trung tính ban ngày, lạnh u ám, huỳnh quang xanh nhạt, đèn đường natri) và **Loại khung** (toàn cảnh, trung cảnh, cận chi tiết, qua vai, đang làm dở); đổi tham chiếu FR-011 thành "đa dạng cấp pack (anti-slop §4)".
  - Mục "Phối preset": thêm dòng hướng Biên tập → E01–E04; hướng Đời thường → nhóm R; Minh họa → nhóm S.
  - Rà lại 24 khung cũ: khung nào chứa từ cấm đứng một mình hoặc số chẵn thì sửa tối thiểu (ghi danh sách preset đã sửa ở cuối file kết quả T019).
  - Xong khi: đủ 28 ID duy nhất (regex `^\| [RSCE]\d\d `); 4 khung E đếm từ ≤ 80.
- [X] T007 [P] Sửa `plugins/image-prompt-pack/skills/prompt-pack/references/image-types.md`
  - Thêm cột **Chữ mặc định** vào bảng loại ảnh: Hero = 2 chèn chữ sau; OG = 2; Thumbnail/banner = 2; Minh họa, Lifestyle, Mockup = 0; Infographic = 2 (tiêu đề) hoặc 1 (số ngắn trong cảnh).
  - Thêm cột **Hướng gợi ý** (Đời thường / Biên tập / Minh họa) và thêm preset E vào cột Preset hợp khi phù hợp (Hero của thương hiệu/thời trang: E01, E02; Mockup: R06 hoặc E03).
  - Sửa cột Rủi ro: bỏ các câu "không nhúng tiêu đề"/"để trống" mâu thuẫn; thay bằng trỏ chế độ chữ.
  - Thay mục "## Ảnh có chữ" bằng 2–3 dòng trỏ `references/text-in-image.md`.
  - Dòng Mockup: "chỉ khi người dùng xác nhận ở Chốt nhanh mục 3 hoặc tự yêu cầu".
  - Mục "Đề xuất số ảnh": thêm câu ≥ 4 ảnh → Chốt nhanh dừng chờ (trỏ `brief-card.md`).
  - Xong khi: mọi preset ID được trỏ tồn tại trong `presets.md` sau T006.

**Checkpoint**: Tri thức v0.2 đủ; không file nào mâu thuẫn Clarifications của spec 002.

---

## Phase 3: User Story 1 — Pack không còn ra ảnh dàn dựng (P1) 🎯 MVP

**Goal**: Prompt ngắn, kể khoảnh khắc, có vật lạc đề + dấu vết người, bảng đa dạng đủ cột.

**Independent Test**: Quickstart 002 kịch bản B và E; đạt `tests/acceptance.md` phần v0.2-US1.

- [X] T008 [US1] Sửa `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` — phần US1 (toàn file sau T008, T012, T015, T017 vẫn ≤ ~150 dòng)
  - Mục **Tiêu chí thành công > Khi lập pack**: thay gạch đầu dòng "đối chiếu từng prompt với anti-slop mục 2" bằng tiêu chí tự kiểm cụ thể (FR-101…FR-106): mỗi prompt 30–80 từ, kể một khoảnh khắc; ≤ 5 vật gọi tên; không số chẵn/đối xứng; ảnh Đời thường có 1 vật lạc đề theo ngữ cảnh + 1 dấu vết người; không từ cấm đứng một mình (trỏ danh sách ở `references/anti-slop.md` §2); ảnh không chữ có câu chặn chữ tự thêm. Thay gạch đầu dòng đa dạng (FR-011) bằng: bảng Kịch bản Media có các cột Hướng, Khung, Độ cao máy, Ánh sáng, Thời tiết/giờ, Người, Chữ và đạt quy tắc đa dạng ở anti-slop §4 (FR-107, FR-108).
  - Mục **Khi sửa prompt**: thêm "dùng cả 15 dấu hiệu, gồm 4 dấu hiệu dàn dựng; prompt sửa cũng phải đạt tiêu chí tự kiểm" (FR-109, FR-106).
  - Mục **Đầu ra**: cập nhật mẫu bảng theo `specs/002-prompt-pack-optimize/contracts/prompt-pack-output.md` (cột mới); thêm câu "prompt nào vượt 80 từ thì ghi lý do dưới bảng".
  - Xong khi: grep không thấy `Bước 1`/`Step 1`; các FR-101…FR-109 đều có tiêu chí tương ứng.
- [X] T009 [P] [US1] Tạo fixture `tests/fixtures/05-christmas-article.md`: HTML comment đầu file nêu mục đích (bài thật của lượt test v0.1; ≥ 4 ảnh → Chốt nhanh dừng chờ; có 2 chỗ chờ sản phẩm → mục 3; dùng cho FR-101…FR-129, SC-101…SC-105) + nội dung chép nguyên văn từ `C:\Users\user\Downloads\PYW_How To.md`
  - Xong khi: số từ phần nội dung khớp file nguồn (±1%); vẫn tìm thấy 2 chỗ chờ sản phẩm (ghi vị trí của chúng trong comment đầu file).
- [X] T010 [P] [US1] Tạo fixture `tests/fixtures/06-staged-images-feedback.md` theo research R8: HTML comment mục đích (US1-AS5, FR-109, FR-106); phần "Prompt cũ (trích)" liệt kê các cụm gây lỗi mà [R03] ghi ("Two small evergreen wreaths", "two ceramic holiday mugs", "two brushed brass candleholders", "Four knitted Christmas stockings", "soft winter daylight", "slightly imperfect", "genuinely lived-in", "subtle household imperfections") và dựng lại 3 prompt ngắn gọn đại diện cho 3 ảnh (sofa/chăn caro, hành lang/cầu thang, bếp) có các lỗi đó; phần "Mô tả 3 ảnh" theo [R03] "Sự thật" (ánh vàng đồng đều; hai vòng hoa y hệt trên hai cửa tủ; ba nơ đỏ cách đều trên lan can; hai cốc giống nhau; không người; mọi vật thuần chủ đề; model tự thêm tuyết, nến, chậu quả mọng, chữ "Hot Cocoa" trên bảng đen); lời người dùng: "Ảnh đơn điệu, quá clean, như được sắp đặt. Sửa prompt giúp tôi."
- [X] T011 [US1] Thêm phần **"## v0.2 — US1: chống dàn dựng"** vào cuối `tests/acceptance.md` (trước mục Truy vết nếu có, hoặc thêm mục truy vết v0.2 riêng): bảng `Kịch bản | Tiêu chí | FR/SC | Đạt/Không`
  - Kịch bản B (fixture 05 + "ok"): từng prompt 30–80 từ (ghi số từ từng prompt); ≤ 5 vật; không số chẵn/đối xứng; ảnh Đời thường có vật lạc đề + dấu vết người, vật lạc đề không lặp giữa các ảnh; không từ cấm; ảnh không chữ có câu chặn chữ (FR-101…FR-105, SC-101); bảng đủ cột và đạt 4 quy tắc FR-108 (SC-102).
  - Kịch bản E (fixture 06): chẩn đoán nêu ≥ 5 nguyên nhân ở [R03] bảng A (danh mục vật, số chẵn, thuần chủ đề, không dấu vết, ánh đồng đều, khung giống nhau, model tự thêm vật/chữ); prompt sửa đạt tự kiểm; 1–3 dòng Đã đổi mỗi ảnh (US1-AS5, FR-109).
- [X] T012 [US1] Sửa `plugins/image-prompt-pack/skills/prompt-pack/references/example-pack.md` — **Ví dụ B** thay bằng ca sửa ảnh dàn dựng: một prompt kiểu danh mục ~120 từ có số chẵn + từ cấm (lấy từ fixture 06, ảnh bếp) → Chẩn đoán trỏ đúng các tell (gồm 4 tell mới) → prompt sửa ≤ 80 từ đạt tự kiểm → Đã đổi 1–3 dòng. Giữ Ví dụ A cho T016.
  - Xong khi: prompt sửa có ghi số từ; đạt mọi tiêu chí tự kiểm.
- [X] T013 [US1] Chạy thử khô US1: worker tự đóng vai model, đọc `SKILL.md` + toàn bộ `references/`, xử lý fixture 05 rồi trả "ok" (kịch bản A→B), và fixture 06 (kịch bản E); lưu đầu ra + bảng chấm theo acceptance v0.2-US1 vào `tests/runs/2026-11-18-v0.2/us1.md`, kèm số từ từng prompt
  - Trượt tiêu chí nào thì sửa `SKILL.md`/references (không sửa tiêu chí), chạy lại; ghi số vòng sửa.
  - Xong khi: mọi tiêu chí v0.2-US1 đạt.

**Checkpoint**: US1 dùng được độc lập (MVP v0.2).

---

## Phase 4: User Story 2 — Chốt nhanh (P2)

**Goal**: Lượt đầu = Chốt nhanh + Kịch bản Media, dừng chờ khi ≥ 4 ảnh; "ok" ra pack.

**Independent Test**: Quickstart 002 kịch bản A, B, F, G; đạt acceptance v0.2-US2.

- [X] T014 [US2] Sửa `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` — phần US2 (sau T008)
  - **Tiêu chí**: thay gạch đầu dòng "Thiếu thông tin thì tự giả định… tối đa 3 câu" bằng tiêu chí Chốt nhanh (FR-110…FR-116): pack dự kiến ≥ 4 ảnh hoặc bài dài → phản hồi đầu chỉ có khối Chốt nhanh ở đầu + Kịch bản Media, không prompt, rồi dừng chờ; 1–3 ảnh / "đưa luôn" / không người trả lời → xuất luôn với khối "Đã dùng mặc định" ở đầu; chỉ hỏi mục chưa quyết, ≤ 4 mục, có mặc định; hướng hình do model chọn theo loại bài và ghi lý do, có thể là Đời thường, Biên tập/chuyên nghiệp (thời trang, tạp chí) hoặc Minh họa; "ok" → không hỏi thêm; đổi một mục → chỉ viết lại prompt bị ảnh hưởng.
  - **Đầu ra**: mẫu bắt đầu bằng `## Chốt nhanh (trả lời "ok" để dùng mặc định)` đặt trên `## Kịch bản Media`; bỏ dòng `**Giả định:**` ở mẫu cũ.
  - **Tri thức**: thêm dòng `references/brief-card.md`: khi lập Kịch bản Media, để quyết định có hỏi không, hỏi gì, mặc định gì.
  - Xong khi: không còn tiêu chí cũ "tối đa 3 câu hỏi" mâu thuẫn; file ≤ ~150 dòng.
- [X] T015 [US2] Thêm phần **"## v0.2 — US2: Chốt nhanh"** vào `tests/acceptance.md`: A (fixture 05): khối Chốt nhanh ở đầu, ≤ 4 mục, mỗi mục có mặc định, mục 1 nêu hướng + lý do, mục 3 nêu 2 chỗ chờ sản phẩm mặc định không, không preset ID/tên công cụ, **không có khối prompt**, dừng chờ (FR-110…FR-112, FR-116, SC-104); B: "ok" → pack theo mặc định, không hỏi thêm (FR-113); F (fixture 02): xuất luôn, khối "Đã dùng mặc định" ở đầu, không mục Giả định ở cuối (FR-114); G: "đổi sang hướng biên tập chuyên nghiệp" → chỉ prompt bị ảnh hưởng đổi, vẫn đạt tự kiểm trừ FR-103 (FR-115, FR-116); thêm dòng: trả lời một phần "hướng B, còn lại ok" (FR-113)
- [X] T016 [US2] Sửa **Ví dụ A** trong `plugins/image-prompt-pack/skills/prompt-pack/references/example-pack.md` theo đầu ra v0.2: lượt 1 (Chốt nhanh + Kịch bản Media đủ cột, không prompt) → lượt 2 sau "ok" (pack 4–5 ảnh, có ít nhất 1 ảnh hướng Biên tập để minh họa phối hướng; hero chế độ 2 chèn chữ sau; mọi prompt ghi số từ và đạt tự kiểm; bảng đạt FR-108)
  - Xong khi: tự kiểm từng prompt đạt; file ≤ ~300 dòng.
- [X] T017 [US2] Chạy thử khô US2 (kịch bản A, B, F, G + trả lời một phần) như T013; lưu `tests/runs/2026-11-18-v0.2/us2.md`; sửa nếu trượt
  - Xong khi: mọi tiêu chí v0.2-US2 đạt.

**Checkpoint**: US1 + US2 chạy được.

---

## Phase 5: User Story 3 — Chế độ chữ (P3)

**Goal**: Mỗi ảnh có chế độ chữ; hero mặc định chèn chữ sau; AI vẽ chữ/hai lượt khi được chọn.

**Independent Test**: Quickstart 002 kịch bản C; đạt acceptance v0.2-US3.

- [X] T018 [US3] Sửa `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` — phần US3 (sau T014)
  - **Tiêu chí**: mỗi ảnh đúng một chế độ chữ ở cột Chữ; mặc định hero/OG/thumbnail chèn chữ sau, ảnh khác không chữ; chế độ AI vẽ chữ/hai lượt chỉ khi người dùng chọn và theo quy tắc `references/text-in-image.md`; tiêu đề tiếng Việt ở chế độ 3/4 kèm cảnh báo thử mẫu; ảnh có chữ phục vụ web vẫn có gợi ý alt; khi sửa ảnh có chữ dùng QC chữ (FR-117…FR-125).
  - **Đầu ra**: mẫu thêm dòng `**Chữ:**` (chỉ chế độ 2/3/4) và mẫu hai khối prompt cho chế độ 4 theo contract.
  - **Tri thức**: thêm dòng `references/text-in-image.md`: khi một ảnh có chế độ chữ khác 0, hoặc khi kiểm ảnh có chữ.
  - Xong khi: file ≤ ~150 dòng.
- [X] T019 [US3] Thêm phần **"## v0.2 — US3: chế độ chữ"** vào `tests/acceptance.md`: B: bảng có cột Chữ, hero/OG = 2, ảnh khác = 0, prompt hero chế độ 2 chừa vùng trống có vị trí + tương phản, không chữ trong ảnh (FR-117, FR-119, FR-123); C: "hero cho AI vẽ luôn tiêu đề Indoor Christmas Decorations" → chỉ prompt hero đổi; có chuỗi trong ngoặc kép, kiểu hoa/thường, kiểu chữ theo đặc điểm, màu, vị trí, cỡ, nền tương phản, lề ~5%, "appears once; no other text anywhere" (FR-120); thêm dòng: tiêu đề tiếng Việt "Trang trí Giáng sinh trong nhà" ở chế độ 3 → có cảnh báo thử mẫu (FR-122); thêm dòng: chế độ 4 → hai khối prompt, lượt 2 đúng câu chuẩn, Reference là ảnh lượt 1 (FR-121); SC-106 ghi "đo khi tạo ảnh thật"
- [X] T020 [US3] Chạy thử khô US3 (C, tiếng Việt chế độ 3, chế độ 4) như T013; lưu `tests/runs/2026-11-18-v0.2/us3.md`; sửa nếu trượt; ghi cuối file danh sách preset đã sửa ở T006 (nếu có)
  - Xong khi: mọi tiêu chí v0.2-US3 đạt.

---

## Phase 6: User Story 4 — Mockup có xác nhận (P4)

**Goal**: Mockup chỉ khi xác nhận; mặc định không; không còn "Bonus".

**Independent Test**: Quickstart 002 kịch bản B (không mockup) và D (chọn có).

- [X] T021 [US4] Sửa mục **Ranh giới** của `plugins/image-prompt-pack/skills/prompt-pack/SKILL.md` (sau T018): thay gạch đầu dòng mockup cũ bằng điều kiện mới (FR-126…FR-128): bài nhắc sản phẩm hoặc có chỗ chờ → hỏi ở Chốt nhanh mục 3, mặc định không; không chọn → pack không có prompt mockup, mục "Bonus" hay prompt sản phẩm dưới bất kỳ tên nào; chọn có hoặc người dùng tự yêu cầu → Reference ảnh sản phẩm thật bắt buộc, nhãn "chờ sản phẩm xác minh", AI chỉ tạo bối cảnh/người/ánh sáng, ghép thiết kế thật sau, giữ metadata AI (chi tiết trỏ anti-slop §5)
  - Xong khi: không còn câu "Mockup sản phẩm chỉ khi người dùng yêu cầu đúng vị trí đó" kiểu cũ mâu thuẫn; file ≤ ~150 dòng.
- [X] T022 [US4] Thêm phần **"## v0.2 — US4: mockup"** vào `tests/acceptance.md`: B (giữ mặc định): 0 prompt mockup, 0 mục "Bonus"/"Product-locked" (FR-127, SC-105); D ("mục 3 chọn có"): 2 prompt mockup cho 2 chỗ, mỗi cái có Reference ảnh sản phẩm thật + nhãn "chờ sản phẩm xác minh" + ghi chú ghép thiết kế/giữ metadata (FR-128); fixture 01 (bài không chờ sản phẩm nhưng có nhắc hoodie): Chốt nhanh có mục 3 mặc định không (FR-126); fixture 03 (log không nhắc sản phẩm): không có mục 3
- [X] T023 [US4] Chạy thử khô US4 (B, D, fixture 01, fixture 03) như T013; lưu `tests/runs/2026-11-18-v0.2/us4.md`; sửa nếu trượt
  - Xong khi: mọi tiêu chí v0.2-US4 đạt.

---

## Phase 7: Polish & Cross-Cutting

- [X] T024 [P] Cập nhật `docs/blind-test.md`: thêm mục "So sánh v0.2 với 3 ảnh cũ (SC-103)" — cùng bài Giáng sinh, tạo ảnh từ pack v0.2 cho 3 vị trí tương ứng (sofa, hành lang, bếp), trộn với 3 ảnh cũ, 5 người xem mù trả lời 2 câu cũ + chọn ảnh nào dùng cho bài; tiêu chí ≥ 4/5 cho **từng câu riêng** và đa số chọn ảnh v0.2; thêm 4 hàng E01–E04 vào bảng ghi kết quả; thêm mục SC-106 (hero có chữ tạo 5 lần, QC chữ 7 mục)
- [X] T025 [P] Cập nhật `docs/verification.md`: thêm các dòng v0.2 (manifest 0.2.0; chạy thử khô US1–US4 trỏ `tests/runs/2026-11-18-v0.2/`; hành vi dừng chờ trên Claude Code/Codex/ChatGPT; blind test v0.2 vs cũ; hero có chữ) với mức trung thực theo những gì đã thực sự chạy; không xóa dòng cũ
- [X] T026 [P] Cập nhật `plugins/image-prompt-pack/README.md` (thêm `brief-card.md`, `text-in-image.md`, nhóm E, nói lượt đầu có thể là Chốt nhanh) và `README.md` ở root (mục "Cách dùng": bài dài sẽ nhận Chốt nhanh trước, trả "ok"; trạng thái preset 28 v0.1 chưa test)
- [X] T027 [P] Cập nhật `CLAUDE.md`: mục Output contract trỏ `specs/002-prompt-pack-optimize/contracts/` (Chốt nhanh ở đầu, cột mới, chế độ chữ, mockup có xác nhận); danh sách references thêm `brief-card.md`, `text-in-image.md`, presets 28 (R/S/C/E); giữ phần còn lại
- [X] T028 Rà toàn bộ `plugins/image-prompt-pack/skills/prompt-pack/` theo Constitution II–IV + quy ước chung: không bước đánh số; không tên tool riêng harness, không tên công cụ tạo ảnh/thiết kế; không biến đường dẫn riêng; `SKILL.md` ≤ ~150 dòng, mỗi reference ≤ ~300 dòng; không chuỗi cấm ngoài câu liệt kê cấm; mọi preset ID được trỏ tồn tại; mọi prompt mẫu trong references đạt tự kiểm (ghi số từ); ghi bảng kết quả "Rà skill v0.2" vào cuối `docs/verification.md` kèm số dòng từng file
- [X] T029 Thêm bảng truy vết v0.2 (FR-101…FR-131, SC-101…SC-108 → file/dòng acceptance → trạng thái; SC cần người/ảnh thật ghi "cần người chạy") vào cuối `tests/acceptance.md`
- [X] T030 Chạy lệnh kiểm manifest (quickstart 001 §1) → `OK 0.2.0`; `git add` mọi file thay đổi (gồm `specs/002-prompt-pack-optimize/**`); commit cục bộ trên nhánh hiện tại với message `feat: prompt-pack v0.2.0 (brief card, text-in-image modes, anti-staged self-check, pack diversity)` và dòng cuối `Co-Authored-By: Claude Haiku 5.5 <noreply@anthropic.com>`; KHÔNG push
  - Xong khi: `git status` sạch; `git log -1` hiện commit.

---

## Dependencies & Execution Order

- **Setup**: T001 → T002.
- **Foundational**: T003 ∥ T004 ∥ T005 ∥ T006 ∥ T007 (khác file); T007 kiểm preset ID sau T006.
- **US1**: T008 sau Foundational; T009 ∥ T010 bất kỳ lúc nào; T011 sau T009/T010; T012 sau T003; T013 cuối.
- **US2**: T014 sau T008 (cùng `SKILL.md`); T015 sau T011 (cùng acceptance); T016 sau T012 (cùng example-pack); T017 cuối.
- **US3**: T018 sau T014; T019 sau T015; T020 cuối.
- **US4**: T021 sau T018; T022 sau T019; T023 cuối.
- **Polish**: T024–T027 song song sau US4; T028, T029 sau đó; T030 cuối cùng.

### Parallel Opportunities

- T003 ∥ T004 ∥ T005 ∥ T006 ∥ T007
- T009 ∥ T010
- T024 ∥ T025 ∥ T026 ∥ T027

## Implementation Strategy

1. Setup + Foundational → tri thức v0.2 sẵn sàng.
2. US1 → **MVP**: pack hết dàn dựng (giải than phiền chính).
3. US2 → Chốt nhanh. 4. US3 → chế độ chữ. 5. US4 → mockup.
6. Polish → docs, rà, truy vết, commit.

## Notes

- Spec 002 thắng nếu task mâu thuẫn; ghi mâu thuẫn vào báo cáo cuối.
- Không đánh `[X]` task chưa đạt "Xong khi".
