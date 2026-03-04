# i-ching-plugins

A collection of Vietnamese I Ching (Kinh Dịch) divination plugins for Claude — covering Lục Hào, Bát Quái, and related metaphysical arts.

## Plugins

### `luc-hao` — Lục Hào Bát Quái (六爻八卦)

Gieo quẻ và luận giải Lục Hào Bát Quái theo phương pháp Mai Hoa Dịch Số — Vietnamese Six-Line I Ching divination with hexagram casting and interpretation.

## Cấu trúc

```
.claude-plugin/
  marketplace.json                  # Marketplace listing (repo-level)
plugins/
  luc-hao/
    .claude-plugin/
      plugin.json                   # Plugin metadata và entry points
    commands/
      gieo-que.md                   # /gieo-que — Gieo quẻ Lục Hào
      luan-giai.md                  # /luan-giai — Luận giải quẻ
    skills/
      gieo-que/
        SKILL.md                    # Tự động khi user muốn gieo quẻ
        references/bang-tra-cuu.md  # Bảng tra cứu Nạp Giáp, Nạp Chi, 64 quẻ...
      luan-giai/
        SKILL.md                    # Tự động khi user muốn giải quẻ
        references/quy-tac-luan-giai.md  # Quy tắc luận giải Dụng Thần, Vượng Suy...
```

## Commands vs Skills

| | Commands (`/gieo-que`, `/luan-giai`) | Skills (auto-invoked) |
|---|---|---|
| **Kích hoạt** | User gõ `/gieo-que` hoặc `/luan-giai` | Claude tự nhận diện từ ngữ cảnh |
| **Khi nào** | User biết lệnh, muốn chạy trực tiếp | User nói tự nhiên ("gieo quẻ cho tôi") |
| **Logic** | Chứa toàn bộ hướng dẫn chi tiết | Nhẹ, trỏ về commands/ để thực hiện |

Skills hoạt động như "bộ nhận diện" — khi user nói tự nhiên, skill kích hoạt và thực hiện theo hướng dẫn chi tiết trong commands.

## Thành phần

### `/gieo-que` (Command) + `gieo-que` (Skill)
- **Chức năng**: Thu thập thông tin, lập Tứ Trụ theo Mai Hoa Dịch Số, gieo quẻ Lục Hào
- **Output**: Bảng quẻ Lục Hào hoàn chỉnh (Nạp Giáp, Lục Thân, Thế/Ứng, Lục Thần)
- **Command**: `/gieo-que Nguyễn Văn A, 15/03/1990, nam, hỏi tài lộc`
- **Skill**: "Tôi muốn gieo quẻ xem tài lộc, tên Nguyễn Văn A, sinh 15/03/1990"

### `/luan-giai` (Command) + `luan-giai` (Skill)
- **Chức năng**: Xác định Dụng Thần, phân tích Vượng/Suy, hào động → kết luận + lời khuyên
- **Command**: `/luan-giai` hoặc `/luan-giai Thiên Phong Cấu, hào 1 động, mệnh Hỏa`
- **Skill**: "Quẻ này có ý nghĩa gì?" hoặc "Giải quẻ giúp tôi"

## Luồng sử dụng

```
Cách 1: Dùng commands
  /gieo-que + thông tin  →  /luan-giai

Cách 2: Nói tự nhiên (skills tự kích hoạt)
  "Gieo quẻ cho tôi..."  →  "Giải quẻ giúp tôi"

Cách 3: Luận giải quẻ có sẵn
  /luan-giai + thông tin quẻ thủ công
```

## Cài đặt

Cài qua Claude marketplace hoặc sao chép thư mục `plugins/luc-hao/` vào `.claude/plugins/`.

## Lưu ý

Nên tắt **thinking mode** (extended thinking) khi dùng plugin này. Tính toán Lục Hào đã được hướng dẫn chi tiết từng bước trong commands — thinking mode không cần thiết và làm chậm phản hồi.
