# Razer Tray — bản sao lưu tiếng Việt

Bản tùy chỉnh của [razer-ctl](https://github.com/sqmagellan/razer-ctl), dùng trên Razer Blade 15 Advanced 2020 RZ09-03305 (USB PID `0x0253`).

## Tệp trong bản sao lưu

- `razer-tray-vietnamese.exe`: bản tray đang dùng trên máy tại thời điểm sao lưu.
- `ma-nguon-razer-tray.zip`: mã nguồn tương ứng để tự biên dịch.
- `HUONG-DAN-BACKUP.md`: nguồn gốc và mã SHA-256 của tệp thực thi.

## Tính năng

Menu tiếng Việt; điều khiển profile, quạt, đèn và các cài đặt được máy hỗ trợ; chọn màu bàn phím hoặc để OpenRGB điều khiển màu. Quạt dùng một cài đặt chung khi chuyển profile; dòng gần nút Thoát hiển thị số vòng thực tế của hai quạt. Có tùy chọn khởi động cùng Windows trong menu.

Mức quạt đặt là giá trị yêu cầu, tốc độ thực tế có thể khác tùy firmware và profile. Tính năng được thử trên máy RZ09-03305, không bảo đảm hoạt động trên mọi model.

## Sử dụng và biên dịch

Chạy `razer-tray-vietnamese.exe` trên Windows, sau đó mở menu từ biểu tượng tray. Cấu hình cá nhân được lưu tại `%APPDATA%\razer-tray\config\default-config.toml` và không nằm trong kho sao lưu.

Giải nén mã nguồn, cài Rust và Visual Studio Build Tools với công cụ C++/Windows SDK, rồi chạy:

```powershell
cargo test --workspace --locked
cargo build --release --locked -p razer-tray
```

Chương trình biên dịch nằm tại `target\release\razer-tray.exe`. File EXE sao lưu trùng mã SHA-256 với bản đã biên dịch và đang chạy tại thời điểm tạo bản sao lưu; không khẳng định bản tự biên dịch lại sẽ trùng từng byte.

## Nguồn gốc

Dự án gốc: [sqmagellan/razer-ctl](https://github.com/sqmagellan/razer-ctl), commit `158ba283f4c7d2a5367b3b6cac95c0deaaee9642`. Mã nguồn giữ giấy phép MIT.