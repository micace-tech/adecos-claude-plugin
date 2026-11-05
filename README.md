# Plugin adecos cho Claude

Bộ skill giúp Claude làm việc cùng adecos: lấy số báo cáo affiliate hằng ngày, sửa flow báo cáo, đánh giá chương trình affiliate và độ lãi, tạo và tối ưu chiến dịch Google Ads Search đúng chính sách, tổng hợp hiệu suất team.

Một plugin dùng cho mọi vai trò. Quyền xem/sửa vẫn do server adecos quyết định theo tài khoản của bạn.

## Cài đặt

### claude.ai (web) và Claude Desktop

1. **Customize → Plugins → Add → Add marketplace**, nhập `micace-tech/adecos-claude-plugin`.
2. Cài plugin **adecos**.
3. Mở tab **Connectors** của plugin → bấm **Connect** ở `adecos` → đăng nhập bằng tài khoản adecos. Không làm bước này thì skill vẫn chạy nhưng Claude không đọc được số liệu.

Không thêm được marketplace? Tải `adecos-<version>.zip` ở mục [Releases](https://github.com/micace-tech/adecos-claude-plugin/releases) rồi chọn **Add → Upload plugin**.

### Claude Code

```
/plugin install adecos --marketplace micace-tech/adecos-claude-plugin
```

Bản Claude Code cũ hơn 2.1.275:

```
/plugin marketplace add micace-tech/adecos-claude-plugin
/plugin install adecos@adecos
```

Lần đầu gọi tool adecos, Claude Code sẽ mở trình duyệt để đăng nhập.

### Điều khiển trình duyệt (lấy số tự động)

Hai skill `collecting-daily-reports` và `fixing-report-flows` cần thêm server `adecos-local` chạy trong **app desktop adecos** trên máy bạn: mở app → bấm **Kết nối Claude** → làm theo hướng dẫn cho Claude Desktop hoặc Claude Code. Không dùng được trên claude.ai web.

## Cập nhật

- claude.ai / Desktop: plugin từ marketplace tự cập nhật; bản upload zip thì tải bản mới và upload lại.
- Claude Code: `/plugin marketplace update adecos`.

Chi tiết skill: [plugins/adecos/README.md](plugins/adecos/README.md).
