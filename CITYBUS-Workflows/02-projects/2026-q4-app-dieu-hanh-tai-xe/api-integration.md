# Tích hợp API — Dự án App điều hành tài xế trên Tablet (FTT)

> Trạng thái: **khung ban đầu** (ngày 2026-11-27), tổng hợp từ 2 file nghiệp vụ ban đầu của dự án. Chi tiết endpoint/cấu trúc dữ liệu sẽ chốt dần theo từng FR và cập nhật vào file này.

## 1. Các hệ thống tích hợp

| Hệ thống | Vai trò trong dự án | Dữ liệu chính | FR liên quan |
|---|---|---|---|
| **GoAFC** (GoLab) | Nguồn gốc định danh & danh mục chuẩn nhà nước | Tài khoản lái xe (SĐT/mật khẩu), danh mục tuyến, giờ xuất bến, dữ liệu bán vé gốc từ GoPS, tọa độ các xe cùng tuyến | FR-001, FR-002, FR-004, FR-006 |
| **FUTA Smartbus** | Nguồn gốc nhân sự & phân công nội bộ | Hồ sơ nhân sự, trạng thái `ACTIVE/INACTIVE`, lịch phân công ca/xe, Lệnh vận chuyển trong ngày, log vi phạm tốc độ | FR-001, FR-002, FR-005 |
| **Máy POS T10** (trên xe) | Thiết bị đồng hành — khởi tạo chuyến & bán vé | Trạng thái chuyến, trạng thái kết nối của T10, số liệu vé/lượt khách trong chuyến | FR-003, FR-004, FR-010 |
| **Phần cứng trên xe** | Nguồn dữ liệu thời gian thực tại chỗ | GPS động (tọa độ, vận tốc), mức pin SOC, Camera (luồng RTSP/Stream), Loa/Micro | FR-003 → FR-010 |
| **Trung tâm OCC** | Điều hành trực tuyến | Kênh Socket/Push 2 chiều, lệnh điều độ, đàm thoại khẩn cấp (ưu tiên âm thanh cao nhất) | FR-007 |

## 2. Nguyên tắc tích hợp xuyên suốt

- **Thứ tự xác thực (FR-001):** gọi GoAFC trước → hợp lệ mới gọi Smartbus đối chiếu trạng thái `ACTIVE`.
- **Offline-First:** mất mạng quá 5 giây hiện banner cảnh báo (`FTT-CM-EXC-001`); API timeout quá 10 giây hoặc lỗi `500/502/503` hiển thị thông báo chuẩn kèm mã lỗi, không treo app (`FTT-CM-EXC-002`) — chi tiết tại `nghiep-vu-chung-du-an/nghiep-vu-chung-du-an.md` Mục 4.3.
- **Dữ liệu cục bộ:** bản đồ tuyến đã cache, file âm thanh trạm và phiên đăng nhập (Encrypted Local Storage) phải hoạt động khi mất kết nối.

## 3. Điểm chưa chốt (theo phụ lục backlog)

- Cấu trúc API Lệnh vận chuyển từ Smartbus (FR-002).
- Nhà cung cấp bản đồ và độ trễ GPS cho phép (FR-004).
- Công thức tính giãn cách và nguồn đếm khách (FR-006).
- Giao thức đàm thoại OCC: VoIP hay Push-to-Talk (FR-007).
- Cơ chế giao tiếp giữa Tablet và máy POS T10 (FR-010).
