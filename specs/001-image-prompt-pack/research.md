# Research: Image Prompt Pack Plugin

**Date**: 2026-11-18 | **Spec**: [spec.md](./spec.md) | **Plan**: [plan.md](./plan.md)

Mức kiểm chứng dùng chung: **ĐÃ CHẠY THẬT** · **ĐỌC MẪU** (đối chiếu repo/cấu hình đang chạy trên máy)
· **ĐỌC TÀI LIỆU** · **CHƯA KIỂM CHỨNG**.

## R1. Một skill hay nhiều skill

- **Decision**: Một skill `prompt-pack` lo cả ba việc: lập Kịch bản Media + Prompt Pack (US1, US2),
  sửa prompt khi ảnh lỗi (US3).
- **Rationale**: Ba việc dùng chung một bộ tri thức (chống slop, preset, loại ảnh). Một skill thì một
  mô tả kích hoạt, ít file nhất (Constitution II), model tự nhận biết người dùng đang muốn tạo pack hay
  sửa prompt (Constitution III).
- **Alternatives considered**: Hai skill `prompt-pack` + `fix-prompt` — bị loại vì nhân đôi phần nạp
  tri thức và tăng nguy cơ kích hoạt nhầm; ba skill theo user story — quá vụn.

## R2. Định dạng marketplace và manifest cho Claude Code và Codex

- **Decision**: Theo đúng mẫu repo `studio-director` của team: repo gốc có
  `.claude-plugin/marketplace.json` (Claude) và `.agents/plugins/marketplace.json` (Codex); plugin ở
  `plugins/image-prompt-pack/` với `.claude-plugin/plugin.json` và `.codex-plugin/plugin.json`, cả hai
  trỏ `"skills": "./skills/"`; mỗi skill có `agents/openai.yaml` cho Codex.
- **Rationale**: Cấu trúc này đang được Claude Code (`known_marketplaces.json`, nguồn git) và Codex
  (`[marketplaces.studio-director] source_type = "git"` trong `~/.codex/config.toml`) dùng trên máy
  người dùng. Mức: **ĐỌC MẪU**.
- **Cài đặt**:
  - Claude Code: `/plugin marketplace add mktphuchung-wq/Image-Prompt-Packs` →
    `/plugin install image-prompt-pack@image-prompt-packs`; cập nhật: `/plugin marketplace update
    image-prompt-packs`.
  - Codex: thêm `[marketplaces.image-prompt-packs]` `source_type = "git"`, `source =
    "https://github.com/mktphuchung-wq/Image-Prompt-Packs.git"` và
    `[plugins."image-prompt-pack@image-prompt-packs"] enabled = true` vào `~/.codex/config.toml`
    (hoặc lệnh marketplace của Codex nếu bản đang dùng có). Cập nhật: Codex kéo lại git source.
- **Alternatives considered**: Repo plugin riêng cho mỗi harness — vi phạm Constitution IV.
  Marketplace Codex dạng `source: url "./"` như superpowers — không cần vì có thư mục `plugins/`.
- **Còn mở**: Cài thật trên cả hai harness chưa chạy → ghi **CHƯA KIỂM CHỨNG** trong
  `docs/verification.md` cho tới khi chạy quickstart.

## R3. Đưa plugin vào ChatGPT

- **Decision**: ChatGPT dùng chính thư mục `plugins/image-prompt-pack/skills/prompt-pack/`: nén
  thành zip và tải lên làm Skill nếu tài khoản có tính năng Skills; nếu không, tạo một Project, dán
  phần thân `SKILL.md` vào Project instructions và đính kèm 4 file `references/` làm tài liệu Project.
  Cập nhật = tải lại zip/file từ bản phát hành mới.
- **Rationale**: Giữ một nguồn nội dung (FR-018). ChatGPT chưa có cơ chế marketplace Git đã kiểm chứng,
  nên đây là đường lui như spec Assumptions đã ghi. `SKILL.md` phải tự đứng được khi dán làm
  instructions: không phụ thuộc biến/đường dẫn riêng của Claude/Codex, tham chiếu references bằng tên
  file.
- **Alternatives considered**: Custom GPT riêng — tạo bản nội dung thứ hai, bị loại.
- **Còn mở**: **CHƯA KIỂM CHỨNG**. Ghi vào `docs/verification.md`.

## R4. Đặt tri thức ở đâu và nạp thế nào

- **Decision**: 4 file trong `skills/prompt-pack/references/`; `SKILL.md` nói khi nào cần đọc file nào
  (ví dụ: luôn đọc `anti-slop.md`; đọc `presets.md` khi chọn phong cách; `image-types.md` khi lập Kịch
  bản Media; `example-pack.md` để xem chuẩn đầu ra).
- **Rationale**: Progressive disclosure giữ context nhỏ; references trong thư mục skill thì gói skill
  tự đủ cho ChatGPT (R3).
- **Alternatives considered**: Một `SKILL.md` dài chứa hết (>600 dòng) — nặng context, khó bảo trì;
  thư mục `context/` ở cấp plugin như studio-director — gói ChatGPT sẽ thiếu file.

## R5. Cách viết prompt chạy tốt trên mọi công cụ

- **Decision**: Quy tắc chung rút từ research 02 (phần giao nhau của OpenAI, Google Nano Banana, BFL
  FLUX.2): tiếng Anh; ý quan trọng nhất ở đầu; 30–80 từ cho đa số ảnh (dài hơn khi cảnh phức tạp);
  diễn đạt khẳng định, không dựa negative prompt; một chỉ dẫn camera/thời đại; một khuyết điểm cụ
  thể; nguồn sáng thật; tỉ lệ khung viết bằng lời trong prompt ("vertical 4:5 frame"); chữ trong ảnh
  đặt trong ngoặc kép kèm số lần xuất hiện; tham chiếu gọi theo số + vai trò ("Image 1 = product
  reference"). Khung 7 khe (FORMAT, SUBJECT, SETTING, CAMERA, LIGHT, REALISM, CONSTRAINTS) là khung
  tư duy nội bộ, không hiển thị (Clarification Q1).
- **Rationale**: Clarification Q2 bỏ adapter; phần giao nhau là phần đáng tin nhất theo research 02.
- **Alternatives considered**: Adapter theo công cụ (bảng D research 02) — bị loại theo Q2. Tham số
  `--ar`, `--no` của Midjourney — là cú pháp riêng, bị loại.

## R6. Nguồn tri thức chống slop và phần được giữ/bỏ

- **Decision**: Chuyển từ research 01/02 vào plugin:
  - Giữ: mục tiêu "ảnh có ý đồ, không có dấu hiệu đồ chế hàng loạt"; bảng 11 tell + đối phó;
    10 phương pháp anti-slop; slot biến thiên (người, nơi, mùa/giờ, khung, thiết bị); 24 preset R/S/C;
    checklist QC 9 mục; quy tắc composite + giữ metadata (chỉ cho mockup, FR-020); cảnh báo "khuyết
    điểm cố ý cũng thành slop mới" → xoay vòng preset, kiểm soát cường độ.
  - Bỏ: số liệu khảo sát, bảng adapter theo model (Q2), quy trình sản xuất POD từng bước (thay bằng
    một ghi chú ngắn), thí nghiệm US-04 (chuyển sang `docs/blind-test.md` cho người duy trì).
- **Rationale**: Plugin chỉ chứa thứ giúp model viết prompt tốt hơn (Constitution I); phần chứng cứ ở
  lại kho nghiên cứu, `README` trỏ nguồn.
- **Alternatives considered**: Chép nguyên văn hai file nghiên cứu — quá dài, lẫn phần không dùng.

## R7. Loại ảnh (template) ban đầu

- **Decision**: 7 loại: (1) hero/ảnh bìa bài viết, (2) minh họa trong bài, (3) infographic/sơ đồ
  có chữ, (4) ảnh chia sẻ mạng xã hội/OG, (5) thumbnail/banner có tiêu đề, (6) ảnh lifestyle/UGC,
  (7) mockup sản phẩm (chỉ khi người dùng yêu cầu). Mỗi loại: mục đích, tỉ lệ thường dùng, preset
  hợp, rủi ro (ví dụ chữ vỡ ở loại 3, 5 → giữ chữ ngắn hoặc chừa vùng trống để thêm sau).
- **Rationale**: Khớp nhóm nội dung ưu tiên trong spec Assumptions (blog, landing, social, trang sản
  phẩm), nằm trong khoảng 5–8 loại.
- **Alternatives considered**: Template theo ngành — chưa có nhu cầu, YAGNI.

## R8. Kiểm thử và nghiệm thu

- **Decision**: Không viết code test. Ba lớp kiểm:
  1. Máy: JSON hợp lệ + version hai `plugin.json` khớp nhau và khớp `CHANGELOG.md` (lệnh một dòng
     trong quickstart).
  2. Kịch bản: 4 fixture × 3 harness, đối chiếu `tests/acceptance.md` (FR/SC từng dòng, đạt/không đạt).
  3. Chất lượng ảnh: blind test 5 người (SC-003) và checklist QC (SC-008), ghi vào
     `docs/blind-test.md` và `docs/verification.md`.
- **Rationale**: Constitution II và mục "Quy trình phát triển & cổng chất lượng".
- **Alternatives considered**: Bộ test Python lint skill như studio-director — studio-director có
  script thật nên cần; plugin này chỉ có Markdown nên không đáng.

## R9. Phiên bản

- **Decision**: Bản đầu `0.1.0` (preset v0.1 chưa test). Lên `1.0.0` khi blind test đạt và cài thật
  đã kiểm trên Claude + Codex. Version ghi ở hai `plugin.json` và `CHANGELOG.md`.
- **Rationale**: FR-019, Constitution V.

## R10. Tên gọi

- **Decision**: Marketplace `image-prompt-packs` (khớp repo), plugin `image-prompt-pack`, skill
  `prompt-pack`. Claude gọi `image-prompt-pack:prompt-pack` hoặc kích hoạt tự động theo mô tả; Codex
  gọi `$prompt-pack`.
- **Rationale**: Tên skill ngắn, không lặp tên plugin khi có namespace.
