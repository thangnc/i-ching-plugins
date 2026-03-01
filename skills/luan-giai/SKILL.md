---
name: luan-giai
description: Luận giải quẻ Lục Hào (六爻) - Phân tích và giải nghĩa chi tiết quẻ Kinh Dịch. Tự động kích hoạt khi có quẻ Lục Hào trong ngữ cảnh hội thoại cần luận giải, hoặc khi người dùng hỏi ý nghĩa quẻ, muốn giải quẻ, phân tích quẻ mà chưa dùng lệnh /luan-giai. Trigger khi gặp: luận giải, giải quẻ, phân tích quẻ, ý nghĩa quẻ, đoán quẻ, quẻ này tốt không, quẻ nói gì, hoặc ngay sau khi gieo quẻ xong và người dùng muốn hiểu kết quả.
---

# Luận Giải Quẻ Lục Hào (Auto-invoked)

Skill này được kích hoạt tự động khi Claude nhận diện người dùng muốn luận giải quẻ qua ngữ cảnh hội thoại.

## Hành động

Thực hiện đúng quy trình luận giải như lệnh `/luan-giai`. Tham khảo file `${CLAUDE_PLUGIN_ROOT}/commands/luan-giai.md` để thực hiện đầy đủ các bước:

1. Xác định Dụng Thần theo lĩnh vực hỏi
2. Phân tích Vượng Suy (Nguyệt kiến, Nhật thần)
3. Phân tích Hào Động (hồi đầu sinh/khắc, hợp/xung)
4. Phân tích Thế Ứng
5. Phân tích Lục Thần bổ trợ
6. Tổng hợp kết luận + lời khuyên

## Nguồn dữ liệu quẻ

Theo thứ tự ưu tiên:
1. **Ngữ cảnh hội thoại** — quẻ vừa gieo bằng /gieo-que hoặc skill gieo-que
2. **Người dùng cung cấp** — tên quẻ, hào động, thông tin cá nhân trong tin nhắn

Nếu chỉ có tên quẻ + hào động (chưa đủ bảng), tự lập bảng Lục Hào hoàn chỉnh trước khi luận giải.

Nếu thiếu thông tin, hỏi lại lịch sự.
