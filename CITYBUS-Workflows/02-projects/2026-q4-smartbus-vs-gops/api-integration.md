# Tích hợp của dự án Smartbus App vs GoPS App

| # | Điểm tích hợp | Chiều dữ liệu | Nội dung |
|---|---|---|---|
| 1 | **SharedFolder** (trên máy T10) | Smartbus App → GoPS | Dữ liệu chuyến khi Start: giờ tài, loại vé, mệnh giá, số xe, tài xế, tiếp viên |
| 2 | **GoPS → GoAFC** | GoPS đẩy lên GoAFC | Mã vé, giá tiền, loại vé — ngay khi bán |
| 3 | **GoAFC → Smartbus Admin** | GoAFC đồng bộ về Smartbus | Mã vé vào module Lịch sử mua vé; phục vụ Báo cáo tuyến và eLVC |

Tổng quan các nhóm API toàn hệ thống: xem `01-core-wiki/04-api-integration/`.
