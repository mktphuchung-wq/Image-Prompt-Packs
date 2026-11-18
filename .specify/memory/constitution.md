<!--
Sync Impact Report
- Version change: (template, chưa ratify) → 1.0.0
- Principles (mới, thay toàn bộ placeholder):
  - [PRINCIPLE_1_NAME] → I. Bám mục tiêu cốt lõi
  - [PRINCIPLE_2_NAME] → II. Đơn giản trước, kỹ thuật sau
  - [PRINCIPLE_3_NAME] → III. Dựa vào năng lực model & harness, không viết procedure
  - [PRINCIPLE_4_NAME] → IV. Chạy được trên nhiều harness
  - [PRINCIPLE_5_NAME] → V. Cài đặt & cập nhật qua marketplace Git repo
- Added sections: Ràng buộc bổ sung; Quy trình phát triển & cổng chất lượng
- Removed sections: không có
- Templates: plan/spec/tasks templates đọc constitution lúc chạy — không cần sửa
- Follow-up TODOs: không có
-->

# Image Prompt Packs Constitution

## Core Principles

### I. Bám mục tiêu cốt lõi

Mục tiêu duy nhất của dự án: từ bất kỳ intake nào của người dùng, tạo ra một Prompt Pack tạo ảnh
dùng được ngay, cho ra ảnh chân thật, không "slop". Plugin KHÔNG tự tạo ảnh.

- Mọi tính năng, file, template, preset PHẢI trả lời được: "Nó giúp prompt pack tốt hơn hoặc
  người dùng đỡ tốn thời gian hơn như thế nào?" Không trả lời được thì không thêm.
- Không mở rộng phạm vi sang việc gọi API tạo ảnh, chỉnh ảnh, lưu trữ ảnh hay quản lý asset.

**Lý do**: Phạm vi hẹp giữ chất lượng đầu ra cao và plugin dễ bảo trì.

### II. Đơn giản trước, kỹ thuật sau

- Ưu tiên nội dung văn bản thuần (Markdown, YAML/JSON khi thật cần) mà model đọc trực tiếp được.
- KHÔNG có build step, runtime, server, database hay dependency bên ngoài cho chức năng lõi.
- Chỉ thêm script/code khi model không thể làm việc đó đáng tin cậy bằng ngôn ngữ tự nhiên, và
  phải ghi lý do trong plan (mục Complexity Tracking).
- Ít file hơn, ngắn hơn được ưu tiên; xoá thứ không dùng (YAGNI).

**Lý do**: Plugin là tri thức + hướng dẫn cho model; mỗi lớp kỹ thuật thêm vào là thêm chỗ hỏng.

### III. Dựa vào năng lực model & harness, không viết procedure

- Hướng dẫn mô tả **mục tiêu, tiêu chuẩn chất lượng, ví dụ và hợp đồng đầu ra** — không mô tả
  từng bước máy móc mà model tự làm tốt được (đọc file, tóm tắt, phân tích nội dung, suy luận).
- Tận dụng context có sẵn trong phiên (lịch sử hội thoại, file, log, output trước) và công cụ
  của harness (đọc file, tìm kiếm, hỏi lại người dùng) thay vì tự xây cơ chế tương đương.
- Template và preset là **điểm tựa chất lượng** (tham chiếu, cấu hình gợi ý), không phải
  biểu mẫu bắt buộc điền cứng.

**Lý do**: Model hiện đại suy luận tốt hơn procedure cứng; procedure chi tiết làm đầu ra rập khuôn
và lỗi thời nhanh.

### IV. Chạy được trên nhiều harness

- Nội dung lõi PHẢI dùng được trên Claude (Claude Code/Claude.ai), Codex và ChatGPT.
- Phần riêng cho từng harness (manifest, cấu trúc thư mục, cách khai báo skill) chỉ là lớp vỏ
  mỏng bọc cùng một nguồn nội dung; không nhân bản nội dung theo harness.
- Không phụ thuộc vào tính năng chỉ một harness có cho chức năng lõi; tính năng riêng chỉ được
  dùng như phần tăng cường, có đường lui khi thiếu.

**Lý do**: Người dùng làm việc trên nhiều công cụ; một nguồn sự thật tránh lệch phiên bản.

### V. Cài đặt & cập nhật qua marketplace Git repo

- Cách cài đặt và cập nhật chính thức là thêm link marketplace từ Git repo vào harness.
- Mỗi bản phát hành PHẢI có số phiên bản (semver) và ghi chú thay đổi ngắn.
- Không yêu cầu người dùng copy file thủ công, chạy script cài đặt hay cấu hình môi trường.

**Lý do**: Một đường phân phối duy nhất, cập nhật một lệnh, không lệch bản giữa người dùng.

## Ràng buộc bổ sung

- Đầu ra cho người dùng là văn bản (kịch bản media + prompt pack) có thể copy dùng ngay ở công cụ
  tạo ảnh bất kỳ; không khoá vào một model tạo ảnh cụ thể.
- Không gửi nội dung người dùng ra dịch vụ bên ngoài ngoài harness đang dùng.
- Ngôn ngữ giao tiếp mặc định theo ngôn ngữ người dùng; prompt tạo ảnh có thể ở tiếng Anh nếu
  điều đó cho chất lượng ảnh tốt hơn.

## Quy trình phát triển & cổng chất lượng

- Mỗi thay đổi được kiểm bằng cách chạy plugin với vài intake mẫu đại diện (bài viết, log/lịch sử,
  yêu cầu ngắn) và đánh giá đầu ra theo tiêu chuẩn chống slop, không bằng test code phức tạp.
- Review PHẢI kiểm: có bám mục tiêu cốt lõi không (I), có thêm phức tạp không cần thiết không (II),
  có biến thành procedure cứng không (III), có chạy trên các harness mục tiêu không (IV).

## Governance

- Constitution này ưu tiên cao hơn mọi quy ước khác trong dự án.
- Sửa đổi: đề xuất bằng PR, nêu nguyên tắc bị ảnh hưởng và lý do; cập nhật Sync Impact Report.
- Versioning: MAJOR khi bỏ/định nghĩa lại nguyên tắc; MINOR khi thêm nguyên tắc/mục; PATCH khi
  làm rõ câu chữ.
- Mọi plan (`/speckit-plan`) PHẢI qua Constitution Check; vi phạm phải được biện minh trong
  Complexity Tracking hoặc loại bỏ.

**Version**: 1.0.0 | **Ratified**: 2026-11-18 | **Last Amended**: 2026-11-18
