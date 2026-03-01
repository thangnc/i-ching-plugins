# Lục Hào Plugin (六爻)

Hệ thống gieo quẻ và luận giải Lục Hào theo Kinh Dịch, Ngũ Hành, Bát Quái.

## Cấu trúc

```
luc-hao-plugin/
├── .claude-plugin/
│   └── plugin.json              # Plugin metadata
├── commands/                    # Slash commands (user-initiated)
│   ├── gieo-que.md              # /gieo-que — Gieo quẻ Lục Hào
│   └── luan-giai.md             # /luan-giai — Luận giải quẻ
├── skills/                      # Auto-invoked skills
│   ├── gieo-que/
│   │   └── SKILL.md             # Tự động khi user muốn gieo quẻ
│   └── luan-giai/
│       └── SKILL.md             # Tự động khi user muốn giải quẻ
└── README.md
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
- **Chức năng**: Thu thập thông tin, lập Tứ Trụ, gieo quẻ Lục Hào
- **Output**: Bảng quẻ Lục Hào hoàn chỉnh
- **Command**: `/gieo-que Nguyễn Văn A, 15/03/1990, nam, hỏi tài lộc`
- **Skill**: "Tôi muốn gieo quẻ xem tài lộc, tên Nguyễn Văn A, sinh 15/03/1990"

### `/luan-giai` (Command) + `luan-giai` (Skill)
- **Chức năng**: Phân tích Dụng thần, vượng suy, hào động → kết luận + lời khuyên
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

Sao chép thư mục plugin vào `.claude/plugins/` hoặc cài qua marketplace.
