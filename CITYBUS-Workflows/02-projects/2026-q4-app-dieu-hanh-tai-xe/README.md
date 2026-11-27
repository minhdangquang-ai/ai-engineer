# Dự án: App điều hành tài xế trên Tablet (FTT)

## 1. Thông tin chung

| Mục | Nội dung |
|---|---|
| Loại dự án | Mới |
| Thời gian | 2026-Q4 |
| Mã dự án con (Component trên Jira `CITY`) | `FTT` |
| Các bên liên quan | FUTA (Smartbus), GoLab (GoAFC/GoPS), TTCC, Trung tâm Điều hành OCC |
| Link Jira (board theo Component `FTT`) | _(bổ sung sau)_ |

## 2. Mục tiêu & phạm vi

Xây dựng ứng dụng trên **Tablet gắn trên xe buýt điện** làm bảng điều khiển trung tâm cho lái xe: đăng nhập ca, nhận Lệnh vận chuyển, kiểm tra xe đầu/cuối ca, giám sát lộ trình–tốc độ–an toàn theo thời gian thực, liên lạc OCC, phát thanh trạm và giám sát camera/phần cứng trên xe. **Tablet không bán vé** — nghiệp vụ bán vé vẫn thuộc máy POS T10 (Smartbus + GoPS); Tablet chỉ đọc/đồng bộ dữ liệu (Read/Sync).

## 3. Nghiệp vụ chung của dự án (Tầng 2) — thư mục `nghiep-vu-chung-du-an/`

- Tổng quan cấp dự án (ranh giới hệ thống, nguồn dữ liệu gốc, vòng đời ca, quy tắc xuyên suốt): [nghiep-vu-chung-du-an.md](nghiep-vu-chung-du-an/nghiep-vu-chung-du-an.md) — tên file cố định, không tiền tố ngày.
- **Thay đổi nghiệp vụ:** ghi riêng thành file mới trong cùng thư mục, tên có tiền tố ngày `yyyy-mm-dd` và chỉ rõ phần đã thay đổi — xem quy tắc trong [nghiep-vu-chung-du-an/README.md](nghiep-vu-chung-du-an/README.md).
- Nghiệp vụ chung toàn hệ thống: file Core [00-nghiep-vu-core-citybus.md](../../01-core-wiki/00-nghiep-vu-core-citybus.md)

## 4. Tích hợp API

Xem file [api-integration.md](api-integration.md).

## 5. Nghiệp vụ riêng theo US (Tầng 3) — thư mục `nghiep-vu-theo-us/`

| Thư mục con | Ý nghĩa |
|---|---|
| `nghiep-vu-theo-us/backlog/` | US chưa được xếp vào sprint nào |
| `nghiep-vu-theo-us/sprint-1/` | US thuộc Sprint 1 — giai đoạn hiện tại |

| Mã Task | Tên US | Vị trí (Backlog / Sprint) | Trạng thái | Tag |
|---|---|---|---|---|
| | | | | |

_Ghi chú: file danh mục nghiệp vụ theo từng chức năng chính (10 FR) từng lưu trong `nghiep-vu-chung-du-an/` đã được xóa ngày 2026-11-27 theo yêu cầu của Minh._

## 6. Biên bản họp

Biên bản họp của dự án lưu trong thư mục `bien-ban-hop/`, nhóm theo tháng (`YYYY-MM/YYYY-MM-DD.md`).
