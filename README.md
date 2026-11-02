# Razer Tray — bản sao lưu tiếng Việt

Bản sao lưu ứng dụng điều khiển Razer Blade trên Windows, dựa trên [sqmagellan/razer-ctl](https://github.com/sqmagellan/razer-ctl). Bản này được tùy chỉnh cho Razer Blade 15 Advanced 2020 (RZ09-03305, USB PID `0x0253`).

## Nội dung

- [razer-tray-vietnamese.exe](razer-tray-vietnamese.exe): bản tray tiếng Việt đã sử dụng trên máy.
- [ma-nguon-razer-tray.zip](ma-nguon-razer-tray.zip): mã nguồn được khôi phục sau khi thư mục ban đầu bị xóa.
- [HUONG-DAN-BACKUP.md](HUONG-DAN-BACKUP.md): nguồn gốc và mã kiểm tra của file thực thi.

## Tính năng chính

- Điều khiển chế độ hiệu năng, tốc độ quạt, đèn logo, độ sáng bàn phím và giới hạn sạc khi máy hỗ trợ.
- Chọn màu đèn bàn phím cố định qua **Đèn bàn phím → Chọn màu...**.
- Chọn **Để ứng dụng khác điều khiển màu bàn phím** nếu muốn dùng OpenRGB thay cho tray.
- Lưu cấu hình riêng khi cắm sạc và khi dùng pin; có tùy chọn khởi động cùng Windows.

Các chức năng phụ thuộc vào model và firmware. Độ sáng vẫn do tray điều khiển theo cấu hình nguồn điện, kể cả khi ứng dụng khác điều khiển màu.

## Sử dụng

1. Tải [razer-tray-vietnamese.exe](razer-tray-vietnamese.exe) và chạy trên Windows.
2. Mở menu từ biểu tượng tray để thay đổi cài đặt.
3. Nếu muốn tự chạy khi đăng nhập, bật **Khởi động cùng Windows** trong menu.

Cấu hình cá nhân được lưu tại `%APPDATA%\razer-tray\config\default-config.toml`. Tệp cấu hình không nằm trong kho sao lưu này; hãy lưu riêng nếu bạn muốn giữ các lựa chọn cá nhân.

## Mã nguồn và biên dịch

Giải nén [ma-nguon-razer-tray.zip](ma-nguon-razer-tray.zip), cài Rust cùng Visual Studio Build Tools với công cụ C++ và Windows SDK, rồi chạy trong thư mục đã giải nén:

```powershell
cargo test --workspace --locked
cargo build --release --locked -p razer-tray
```

File biên dịch nằm tại `target\release\razer-tray.exe`. Mã nguồn được dựng lại từ bản gốc và lịch sử thay đổi; các kiểm thử đã đạt, nhưng chưa xác nhận file biên dịch từ mã nguồn này giống từng byte với file EXE được sao lưu.

## Nguồn gốc và giấy phép

Dự án gốc: [sqmagellan/razer-ctl](https://github.com/sqmagellan/razer-ctl), commit `158ba283f4c7d2a5367b3b6cac95c0deaaee9642`. Mã nguồn giữ giấy phép MIT của dự án gốc.
