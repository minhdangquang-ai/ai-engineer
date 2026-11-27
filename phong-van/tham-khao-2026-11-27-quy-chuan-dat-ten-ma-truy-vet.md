# THAM KHẢO — Quy chuẩn đặt tên & đánh mã truy vết yêu cầu (Naming & Traceability Convention)
Nguồn: Minh gửi trong chat ngày 2026-11-27 khi bắt đầu phỏng vấn grill-me về JIRA-Workflows. Đây là tài liệu tham khảo Minh đưa để xem xét áp dụng — chưa phải quyết định chốt (sẽ chốt qua phỏng vấn).

## 1. Công thức tổng quát (Master Formula)
Cấu trúc phân cấp Cha -> Con -> Chi tiết:
**`[MÃ_DỰ_ÁN]-[LOẠI_TÀI_LIỆU]-[MÃ_CHA].[SỐ_THỨ_TỰ]`**
- `[MÃ_DỰ_ÁN]` (Project Key): 2–4 ký tự viết hoa, trùng khớp 100% với Project Key trên Jira. Ví dụ: `FTT` (Futa Tech Tablet), `HRA` (HR/Admin), `SMB` (Smartbus).

## 2. Quy chuẩn mã hóa theo vòng đời phát triển (SDLC)
| Giai đoạn / Vai trò | Loại thực thể | Ký tự | Cấu trúc | Ví dụ | Ghi chú |
|---|---|---|---|---|---|
| Phạm vi & Kiến trúc (BA/PO) | Tính năng chính (Epic) | `FR` | `[PRJ]-FR-[001..999]` | `FTT-FR-001` | Functional Requirement; có thể phân dải số theo phân hệ (1xx Auth, 2xx Vận hành, 3xx Báo cáo) |
| | Yêu cầu phi chức năng | `NFR` | `[PRJ]-NFR-[001..999]` | `FTT-NFR-001` | Hiệu năng, bảo mật, offline, chịu tải, Kiosk mode |
| | Màn hình / Giao diện | `SCR` | `[PRJ]-SCR-[FR].[01..99]` | `FTT-SCR-001.01` | Gắn với FR chứa màn hình đó |
| Đặc tả chi tiết (BA/PO) | User Story | `US` | `[PRJ]-US-[FR].[01..99]` | `FTT-US-001.01` | Nhúng mã FR cha trước dấu chấm |
| | Ràng buộc đặc thù (riêng 1 US) | `BR` | `[PRJ]-BR-[FR].[US]-[NHÓM]-[01..99]` | `FTT-BR-001.01-WFL-01` | Business Rule chỉ tồn tại trong 1 US |
| | Ràng buộc dùng chung (toàn dự án) | `CM` | `[PRJ]-CM-[NHÓM]-[001..999]` | `FTT-CM-VAL-001` | Common Rule; lưu tại thư viện chung (Confluence/Epic riêng) |
| Kiểm thử & Lỗi (QC/QA) | Kịch bản kiểm thử | `TC` | `[PRJ]-TC-[FR].[US]-[01..99]` | `FTT-TC-001.01-01` | Nhìn mã biết thuộc US/FR nào |
| | Báo cáo lỗi (Bug) | `BUG` | `[Đối tượng] [Bug] [Module] Mô tả` | `[Dev-BE] [Bug] [Tour] Lỗi get số tour từ EZ` | Chuẩn hóa tiêu đề Jira để Lead phân luồng Dev-App/Dev-BE/Dev-Web |

## 3. Bảng mã phân loại ràng buộc kỹ thuật (7 nhóm chuẩn) — điền vào `[NHÓM]` của BR và CM
| Mã | Tên | Bản chất | Khi nào dùng |
|---|---|---|---|
| `VAL` | Validation | Kiểm tra hợp lệ dữ liệu đầu vào | Định dạng SĐT/email/biển số, min/max, bắt buộc, ký tự đặc biệt |
| `SEC` | Security & Auth | Bảo mật, xác thực, phân quyền | Role, Active/Inactive, hết hạn token, mã hóa |
| `WFL` | Workflow & State | Luồng xử lý, chuyển trạng thái | Pre-condition, thứ tự bước, khóa/mở nút theo trạng thái |
| `CAL` | Calculation & Logic | Tính toán, ngưỡng cảnh báo | Công thức tiền/tốc độ/khoảng cách, làm tròn, ngưỡng cảnh báo |
| `INT` | Integration & Sync | Tích hợp API, đồng bộ | Thứ tự gọi API, retry, đồng bộ đa hệ thống/đối tác |
| `EXC` | Exception & Error | Ngoại lệ, thông báo lỗi | Offline, timeout, 5xx, nội dung thông báo lỗi chuẩn |
| `FMT` | Format & Display | Định dạng hiển thị | Ngày giờ DD/MM/YYYY, đơn vị km/h, VNĐ, cắt chữ "..." |

## 4. Nguyên tắc vận hành trên Jira & AI (Rovo)
1. **Không tự đặt số tịnh tiến cho cấp con:** không đặt US-001..US-100 chạy dài; luôn giữ dấu chấm phân cấp (US-001.01, TC-001.01-01).
2. **Đóng gói tự đủ (Self-Contained Story):** US tham chiếu mã dùng chung (CM) phải dán kèm 1–2 dòng tóm tắt quy tắc ngay trong Description để AI (Rovo) đọc hiểu trực tiếp, không sót ngữ cảnh.
3. **Khóa cứng tiền tố trong Prompt AI:** cấu hình Rovo Agent cho BA (sinh US/BR) và QC (sinh TC/Bug) phải nhúng cố định bảng quy tắc đặt tên này vào phần `# QUY TẮC ĐẶT MÃ`.
