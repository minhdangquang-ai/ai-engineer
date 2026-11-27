# Tài liệu tham khảo Minh gửi ngày 2026-11-27 (trong buổi grill-me workflow Citybus)
Nguồn: Minh dán trực tiếp vào chat, yêu cầu Peter tham khảo/review đối chiếu với cấu trúc kho chính đã chốt ở Câu 10.
Trạng thái: tài liệu tham khảo — chưa phải bản chốt; các điểm hợp nhất/xung đột được ghi ở Câu 15 trong file phỏng vấn chính.

---

# FUTA CITYBUS — Hệ thống Quản trị Tri thức & Quy trình QC Đa Dự Án

> Kho lưu trữ chuẩn hóa nghiệp vụ, nhật ký kiểm thử hàng ngày và hồ sơ từng dự án thuộc **FUTA CITYBUS** (tối ưu cho Obsidian / VS Code / GitHub).

## 1. Cấu trúc thư mục

```text
futa-citybus/
├── README.md                          # Tổng quan kiến trúc & quy trình vận hành
├── .gitignore
├── 00-inbox/                          # Trung tâm điều phối theo NGÀY (Z -> A)
│   ├── daily-log-template.md          # Mẫu nhật ký 4 phần hàng ngày
│   └── 2026-11/
│       └── 2026-11-26.md
├── 01-core-wiki/                      # Tầng 1: Từ điển nghiệp vụ chuẩn (Source of Truth)
│   ├── 01-web-admin.md                # Web Admin & Website Citybus
│   ├── 02-onbus-hardware.md           # Thiết bị on-bus (POS, T10, NFC/QR, offline)
│   ├── 03-mobile-app-driver.md        # Mobile App Tài xế / Tiếp viên & Điều hành trực tuyến
│   ├── 04-api-integration.md          # API Hub tổng quan (2 chiều Outbound/Inbound)
│   └── 04-api-integration/
│       ├── 01-api-noi-bo-futa.md          # SSO, Hệ sinh thái FUTA, Công ty con
│       ├── 02-api-thanh-toan.md           # VNPay, MoMo, ZaloPay...
│       ├── 03-api-thiet-bi-gps.md         # Bình Anh, TongDa (GPS, camera, tốc độ...)
│       └── 04-api-doi-tac-van-hanh.md     # GoAFC (Trung tâm công cộng), GoPS/GOLAB...
├── 02-projects/                       # Tầng 2: Hồ sơ từng dự án độc lập (5 khối chuẩn + API riêng)
│   ├── _template-du-an.md
│   ├── 2026-q4-smartbus-vs-gops/      # README.md + api-integration.md
│   ├── 2026-q4-smartbus-vs-vnpay/     # README.md + api-integration.md
│   └── 2026-q4-app-dieu-hanh-tai-xe/  # README.md + api-integration.md
└── 03-resources/                      # Tài nguyên & môi trường kiểm thử
    ├── test-devices.md                # Thiết bị test vật lý (T10, POS, Mobile...)
    └── test-environments.md           # URL Dev/Staging/UAT & tài khoản test phân quyền
```

## 2. Luồng vận hành & Cổng "Nghiệp vụ Đúng" (tóm tắt từ bản gốc)
- Tiếp nhận thông tin hàng ngày (Email lỗi, Chat BA, Task Jira) -> ghi vào `00-inbox/YYYY-MM/YYYY-MM-DD.md`.
- Trao đổi BA trên chat (chưa có Jira): trạng thái "⏳ Chờ BA lên Jira".
- BA đã tạo Task Jira chính thức: qua Cổng kiểm soát "Nghiệp vụ Đúng" — đổi trạng thái "✅ Đã chốt [Link Jira]", rồi mới cập nhật `02-projects/<du-an>/` và đồng bộ rule chuẩn vào `01-core-wiki/`.
- Email lỗi/sự cố phức tạp: tóm tắt & review với QC Lead/PO, chờ xác nhận "OK" trước khi ghi vào `02-projects/`.
- Tiến độ test & task Done: cập nhật Khối 4 trong `02-projects/`.
- 17h00: tổng hợp báo cáo cuối ngày gửi QC Lead Bình.

## 3. Nguyên tắc vàng (bản gốc)
1. Cổng "Nghiệp vụ Đúng": thông tin trên chat chỉ lưu ở `00-inbox/` dạng chờ; chỉ khi BA tạo Task Jira chính thức mới là nghiệp vụ chuẩn.
2. Không trùng lặp dữ liệu với Jira/TestRail: Markdown chỉ lưu link Jira Filter/Dashboard/Ticket + bảng tóm tắt tiến độ.
3. Review trước khi ghi sự cố: tóm tắt Phạm vi ảnh hưởng, Timeline, Nguyên nhân gốc rễ, Action items và xác nhận trước.
4. Nhật ký `00-inbox/` sắp xếp Z -> A theo tháng `YYYY-MM/YYYY-MM-DD.md`.
5. Đầu mối báo cáo cuối ngày: QC Lead Bình.

## 4. Quy tắc đặt tên, Commit & Người Commit (bản gốc)
- Git Author: mỗi thành viên cấu hình đúng danh tính cá nhân (`git config user.name`, `user.email`). Bản gốc ghi cấu hình hiện tại là `dangquangminh-vn <dangquangminh.vn@gmail.com>` — lưu ý: khác với cấu hình trên máy của Peter (`minhdangquang-ai <minhdangquang.ai@gmail.com>`), cần Minh xác nhận khi hợp nhất.
- Tên thư mục/file: kebab-case không dấu; thư mục dự án theo `YYYY-q<1-4>-<ten-ngan>/`; nhật ký ngày theo `YYYY-MM/YYYY-MM-DD.md`.
- Commit message: `<type>(<scope>): <mô tả ngắn> [Mã Jira nếu có]` — type gồm `log`, `docs`, `feat`, `chore`.
