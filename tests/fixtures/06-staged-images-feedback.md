<!--
Fixture 06: ba ảnh lỗi của lượt test v0.1, mô tả bằng chữ vì không lưu ảnh (xem Assumptions của spec 002).
Dùng cho US1-AS5 (FR-109, FR-106) và kịch bản E: chẩn đoán phải nêu nguyên nhân theo bảng dấu hiệu ở anti-slop mục 3, và prompt sửa phải đạt tự kiểm.
Phần "Prompt cũ (trích)" là các cụm mà [R03] ghi là gây lỗi, cùng ba prompt dựng lại ngắn để đại diện cho ba ảnh. Đây không phải nguyên văn pack v0.1.
-->

# Ba ảnh lỗi của lượt test

## Lời người dùng

> Ảnh đơn điệu, quá clean, như được sắp đặt. Sửa prompt giúp tôi.

## Ba ảnh (mô tả bằng chữ)

1. Ảnh 1: sofa và chăn caro.
2. Ảnh 2: hành lang và cầu thang.
3. Ảnh 3: bếp.

## Sự thật chung cho cả ba ảnh (theo [R03], mục Sự thật)

- Ánh vàng ấm đồng đều; cùng một khung ngang tầm mắt.
- Đối xứng: hai vòng hoa y hệt trên hai cửa tủ, ba nơ đỏ cách đều trên lan can, hai cốc giống nhau.
- Không có người, không có dấu vết đang dùng.
- Mọi vật thuộc chủ đề Giáng sinh hoặc đồ bếp được styling; không có vật lạc chủ đề.
- Model tự thêm thứ prompt không yêu cầu: tuyết ngoài cửa sổ, nến, chậu quả mọng, chữ "Hot Cocoa" trên bảng đen.

## Prompt cũ (trích)

Các cụm mà [R03] ghi là gây lỗi:

- "Two small evergreen wreaths"
- "two ceramic holiday mugs"
- "two brushed brass candleholders"
- "Four knitted Christmas stockings"
- "soft winter daylight"
- "slightly imperfect"
- "genuinely lived-in"
- "subtle household imperfections"

Ba prompt dựng lại, mỗi prompt đại diện một ảnh và giữ các cụm trên:

### Ảnh 1: sofa và chăn caro

```text
Cozy living room sofa with a red-and-green plaid blanket over one arm. Two small evergreen wreaths on the wall above it, soft winter daylight from the window, a slightly imperfect cushion, genuinely lived-in feel, subtle household imperfections. Shot on a phone, 3:2 frame.
```

### Ảnh 2: hành lang và cầu thang

```text
Entryway staircase with evergreen garland along the railing, three red bows spaced evenly on it. Four knitted Christmas stockings hang in a row from the banister, soft winter daylight, slightly imperfect paint, genuinely lived-in, subtle household imperfections. 3:2 frame at eye level.
```

### Ảnh 3: bếp

```text
Kitchen counter with two ceramic holiday mugs side by side, two brushed brass candleholders beside them, a small wreath on each cabinet door, soft winter daylight through the window, slightly imperfect tiles, subtle household imperfections. 3:2 frame at eye level.
```
