# xteams-cli backup

Bản export đầy đủ của **xteams-cli** (boazy v0.3.0) đang chạy trên server của sếp Huy — để restore nhanh khi đổi máy/VM mới.

## Nội dung

- `xteams` — binary Linux x86-64 (10MB)
- `teams` — wrapper script gọi `xteams`
- `xteams.sha256` — hash SHA-256 của binary, để verify sau khi tải về

> ⚠️ **KHÔNG bao gồm** `~/.local/state/xteams/token-cache.json` — file này chứa access/refresh token đăng nhập Teams của sếp, tuyệt đối không đưa lên git. Sau khi restore, login lại bằng device-code (xem bên dưới).

## Restore trên máy mới

```bash
# 1. Tải binary + wrapper về
cp xteams ~/workspace/bin/xteams
cp teams ~/workspace/bin/teams
chmod +x ~/workspace/bin/xteams ~/workspace/bin/teams

# 2. Verify (tùy chọn)
sha256sum ~/workspace/bin/xteams
# so với nội dung file xteams.sha256

# 3. Đăng nhập Teams (device-code)
~/workspace/bin/xteams login
# → mở link hiện trên màn hình, nhập mã, login bằng logan.h@bincorporation.com
```

## Cú pháp cơ bản

```bash
~/workspace/bin/teams chat list -n 30                          # danh sách hội thoại
~/workspace/bin/teams message list "<conversation-id>" -n 5    # đọc tin nhắn
~/workspace/bin/teams message send "<conversation-id>" "..."   # gửi tin nhắn
```

## Ghi chú

- Token cache nằm ở `~/.local/state/xteams/token-cache.json`, refresh token tự gia hạn ~90 ngày.
- Quy tắc dùng của team: Teams và Zalo CHỈ dùng agent CLI, không dùng browser.
- Export ngày: 2026-10-20. Người giữ: Trợ lý Caca.
