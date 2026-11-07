# Razer Tray, bản tiếng Việt cho Razer Blade 15 Advanced 2020

Bản tùy chỉnh của razer-ctl cho **Razer Blade 15 Advanced 2020 (RZ09-03305, USB PID 0x0253)** chạy Windows 11. Bản sao lưu ngày **07/11/2026** gồm chương trình chạy và mã nguồn Rust tương ứng.

## Tải và chạy

- [razer-tray-vietnamese.exe](./razer-tray-vietnamese.exe) là bản chạy trực tiếp trên Windows x64. Đặt tệp ở thư mục muốn dùng lâu dài, chạy tệp rồi nhấp chuột phải vào biểu tượng Razer Tray trong khay hệ thống.
- [ma-nguon-razer-tray.zip](./ma-nguon-razer-tray.zip) chứa mã nguồn, tài liệu chỉnh curve GPU và giấy phép MIT.
- [HUONG-DAN-BACKUP.md](./HUONG-DAN-BACKUP.md) ghi mã SHA-256 của bản chạy và gói mã nguồn.

## Điều khiển laptop

- **Hiệu năng và quạt.** Chọn chế độ hiệu năng hoặc đặt quạt tự động/thủ công. Mức quạt dùng chung giữa các profile và được áp dụng lại sau khi chuyển profile. Dòng **Tốc độ quạt** gần nút **Thoát** hiển thị RPM thực tế của hai quạt. RPM thực tế có thể khác giá trị đặt do firmware.
- **Đèn bàn phím.** Chọn **Cố định** để dùng một màu, hoặc **Chọn màu...** để mở bảng màu. Bật **Để ứng dụng khác điều khiển màu bàn phím** nếu dùng OpenRGB. Razer Tray vẫn quản lý độ sáng theo profile.
- **Phím tắt.** `Win + F4` bật/tắt quyền micro, `Win + F5` bật/tắt quyền camera, `Win + F6` bật/tắt touchpad. Cả ba thao tác đều có trong menu.
- Menu còn có tần số quét, đèn logo và giới hạn sạc tùy tính năng firmware hỗ trợ.

## Chỉnh curve GPU NVIDIA

Trong menu tray, mở **Chỉnh curve GPU NVIDIA...**. Trình chỉnh hiện hỗ trợ **RTX 2080 Super Max-Q trên PCI bus 1** và kiểm tra bảng 128 điểm của driver. Đồ thị hiển thị từ 0,3 đến 1,0 V. Vùng xám là vùng driver không cung cấp điểm chỉnh. Các điểm trên 1,0 V vẫn được giữ trong tệp.

1. Chọn điện áp, rồi kéo điểm trên đồ thị hoặc nhập xung theo bước 15 MHz.
2. **Làm phẳng từ điểm này** đặt phần bên phải về xung mục tiêu. **Undervolt** lấy chênh lệch MHz tại điểm chọn so với curve gốc, dịch các điểm bên trái theo mức đó và làm phẳng từ điểm chọn trở đi. Bấm lại tính từ gốc.
3. **Lưu curve** lưu bản nháp. **Áp dụng** ghi lên GPU với quyền quản trị và đọc lại để xác nhận. **Khôi phục trước lần áp dụng** nạp bảng offset trước lần ghi gần nhất. **Đưa offset về mặc định** đưa offset từng điểm về 0.

## Tự áp dụng khi đăng nhập Windows

Lưu curve rồi bật **Tự áp dụng curve đã lưu khi đăng nhập Windows** trong cửa sổ curve. Xác nhận quyền quản trị khi Windows hỏi. Tùy chọn này dùng chung một mục Task Scheduler với **Khởi động cùng Windows** của Razer Tray.

Khi đăng nhập, app đợi driver sẵn sàng rồi nạp curve đã lưu. Nếu điểm nào cần offset vượt **+150 MHz** so với curve gốc hiện tại của driver, app hạ điểm đó xuống trong giới hạn và giữ đường cong không giảm. Tệp đã lưu được giữ nguyên. Khi tùy chọn bật, một lần **Áp dụng** thủ công thành công cũng cập nhật bản lưu dùng cho lần đăng nhập tiếp theo.

Bỏ chọn **Tự áp dụng curve đã lưu khi đăng nhập Windows** để chỉ chạy tray. Dùng **Khởi động cùng Windows** trong menu tray để quản lý việc chạy ứng dụng lúc đăng nhập. Sau khi di chuyển EXE, bật lại mục khởi động từ vị trí mới để cập nhật đường dẫn.

## Cấu hình và nhật ký

- Cấu hình tray nằm ở `%APPDATA%\razer-tray\config\default-config.toml`.
- Curve đã lưu và kết quả lần tự áp dụng nằm trong `%LOCALAPPDATA%\razer-tray\gpu-curve`, lần lượt là `saved.toml` và `startup-result.toml`.
- Nhật ký tray nằm ở `%LOCALAPPDATA%\razer-tray\razer-tray.log`.

Bản sao lưu GitHub gồm chương trình và mã nguồn. Cấu hình cá nhân, curve đã lưu và nhật ký nằm trên máy.

## Biên dịch

Giải nén gói mã nguồn. Cài Rust stable cho `x86_64-pc-windows-msvc` và Visual Studio Build Tools có bộ công cụ C++ cùng Windows SDK. Mở **x64 Native Tools Command Prompt** tại thư mục chứa `Cargo.toml` rồi chạy:

```powershell
cargo test --workspace --locked
cargo build --release --locked -p razer-tray
```

File chạy nằm ở `target\release\razer-tray.exe`.

Mã nguồn dựa trên razer-ctl tại commit `158ba283f4c7d2a5367b3b6cac95c0deaaee9642` và giữ giấy phép MIT. [Dự án gốc](https://github.com/sqmagellan/razer-ctl/tree/158ba283f4c7d2a5367b3b6cac95c0deaaee9642)
