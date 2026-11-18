# Contract: Khối Chốt nhanh

Nội dung tri thức đầy đủ nằm ở `references/brief-card.md` của skill; file này là hợp đồng kiểm thử.

## Khi nào có khối, khi nào dừng

| Tình huống | Khối | Dừng chờ |
|---|---|---|
| ≥ 4 ảnh dự kiến, hoặc bài ≥ ~800 từ / ≥ 4 mục lớn | "Chốt nhanh" | Có |
| 1–3 ảnh, hoặc người dùng nói "đưa luôn" / "không cần hỏi", hoặc không có người trả lời | "Đã dùng mặc định" (ngắn) | Không |
| Intake đã quyết mọi mục | Không có khối | Không |

## Mẫu (chỉ in mục chưa quyết; đánh số lại liên tục)

```markdown
## Chốt nhanh (trả lời "ok" để dùng mặc định)
1. Hướng hình: <mặc định model chọn> (mặc định — <1 câu lý do>) · <lựa chọn 2> · <lựa chọn 3>
2. Chữ trong ảnh: Hero và ảnh chia sẻ chừa vùng để chèn tiêu đề sau bằng công cụ thiết kế (mặc định) · AI vẽ luôn tiêu đề "<chuỗi>" · Không chữ. Các ảnh khác: không chữ.
3. Sản phẩm: bài có <N> chỗ chờ sản phẩm (<vị trí>). Làm mockup ở đó không? Mặc định: không.
4. Số ảnh: <N> ảnh; hero <tỉ lệ>, ảnh chia sẻ <tỉ lệ>. Giữ nguyên?
```

## Bất biến

- ≤ 4 mục; mỗi mục 1 mặc định + ≤ 3 lựa chọn.
- Lựa chọn mô tả bằng kết quả nhìn thấy; không preset ID, tên công cụ tạo ảnh/thiết kế, tham số kỹ thuật.
- Khối đặt **trên** Kịch bản Media.
- "ok" → pack theo mặc định, không hỏi thêm; trả lời một phần → mục không nhắc theo mặc định.
- Người dùng hỏi việc khác khi đang chờ → không tự xuất pack.
