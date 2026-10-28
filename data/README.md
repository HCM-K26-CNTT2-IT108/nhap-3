# Hệ thống giám sát trạm cảm biến nông trại (SmartFarm Monitor)

Hệ thống lọc log máy chủ tự động và quản lý thiết bị trạm cảm biến của SmartFarm.

## Hướng dẫn chạy script

```powershell
cd smartfarm-system\scripts
.\auto_report.ps1
```

Nếu bị chặn bởi ExecutionPolicy:

```powershell
powershell -ExecutionPolicy Bypass -File .\auto_report.ps1
```

Kết quả được ghi vào `backup/bao-cao-su-co.txt`.

## Checklist kiểm tra thiết bị

- [x] Tạo xong cây thư mục và file `.env`
- [x] Chạy `auto_report.ps1` không lỗi
- [ ] Kiểm tra nguồn điện các trạm cảm biến
- [ ] Kiểm tra kết nối mạng sensor-03

## Bảng thông số phần cứng

| Tên thiết bị | Đơn giá (VNĐ) | Loại storage |
|--------------|---------------|--------------|
| (thiết bị 1 lấy từ sheet danh-muc-linh-kien) | ... | SSD |
| (thiết bị 2) | ... | HDD |
| (thiết bị 3) | ... | SSD |

## Phân tích hệ thống

### Mô hình IPO của chức năng lọc log

- **Input:** file `log-he-thong.log`
- **Process:** `Get-Content | Select-String` lọc dòng CRITICAL/ERROR và đếm số dòng
- **Output:** file `bao-cao-su-co.txt`

### Phân loại DIKW

| Phát biểu | Tầng |
|-----------|------|
| (a) Quyết định thay modem trạm sensor-03 trước thứ Sáu | Wisdom |
| (b) 2026-10-12 08:15:01 [ERROR] sensor-03 Connection TIMEOUT after 30s | Data |
| (c) Hôm nay ghi nhận 8 sự cố, 4 sự cố từ sensor-03 | Information |
| (d) Sensor-03 hay mất kết nối buổi chiều do sóng yếu, cần lắp thêm anten | Knowledge |

## Bẫy phần cứng

Tải file log 500 MB qua mạng 100 Mbps:

- Quy đổi: 100 Mbps ÷ 8 = 12,5 MB/s
- Thời gian: 500 MB ÷ 12,5 MB/s = **40 giây**