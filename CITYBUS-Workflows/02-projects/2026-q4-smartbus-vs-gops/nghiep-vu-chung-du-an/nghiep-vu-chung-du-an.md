# NGHIỆP VỤ DỰ ÁN — Smartbus App vs GoPS App (Tầng 2)

> File này chỉ chứa nghiệp vụ **riêng của dự án tích hợp Smartbus App ↔ GoPS App**. Nghiệp vụ chung Citybus (vai trò TTCC/GoLab, chính sách miễn phí vé, khung eLVC, nguyên tắc trợ giá) nằm ở file Core: `01-core-wiki/00-nghiep-vu-core-citybus.md` — đọc Core trước khi đọc file này.
> Nguồn: tài liệu tổng hợp nghiệp vụ Citybus, cập nhật 26/11/2026.
> **Lưu vết (2026-11-27):** áp dụng logic thư mục của dự án App điều hành tài xế trên Tablet (FTT) cho dự án này theo yêu cầu của Minh — file đổi tên từ `nghiep-vu-du-an.md` thành `nghiep-vu-chung-du-an.md` và chuyển vào thư mục `nghiep-vu-chung-du-an/`. Mọi thay đổi nghiệp vụ về sau ghi riêng thành file mới trong cùng thư mục, tên có tiền tố ngày `yyyy-mm-dd` và chỉ rõ phần đã thay đổi (xem `README.md` cùng thư mục).

---

## 1. Tổng quan tích hợp

Trên mỗi máy POS T10 chạy song song 2 ứng dụng:

- **App Smartbus** (FUTA): đăng nhập, chọn chuyến theo giờ tài, Start/Kết thúc chuyến.
- **App GoPS** (GoLab): bán vé chính trên xe.

Điểm nối giữa 2 app là thư mục **SharedFolder** trên thiết bị.

## 2. Luồng Start chuyến

1. Nhân viên đăng nhập App Smartbus.
2. Chọn chuyến được phân công theo giờ tài.
3. Start chuyến thành công → dữ liệu chuyến (giờ tài, loại vé, mệnh giá, số xe, tên tài xế, tên tiếp viên) được ghi vào **SharedFolder**.
4. Mở App GoPS → GoPS **đọc SharedFolder** để lấy thông tin và start chuyến bán vé.

**Điểm rủi ro:** SharedFolder bị lỗi / đầy / quyền ghi bị chặn sẽ khiến GoPS không start được chuyến — cần test kỹ các trường hợp này.

## 3. Luồng bán vé & đồng bộ

- GoPS bán vé → đẩy mã vé, giá tiền, loại vé sang **GoAFC trước**.
- GoAFC đồng bộ mã vé về **Smartbus Admin**, module **Lịch sử mua vé**.
- Lịch sử mua vé là nguồn đối chiếu chính với eLVC và Báo cáo tuyến.

## 4. Kết thúc chuyến & ghi nhận eLVC

- App Smartbus kết thúc chuyến + Điều hành xác nhận xe đã về bến → chuyến được ghi nhận vào eLVC của tuyến ngày đó.
- **Hủy trạng thái "Kết thúc chuyến":** chỉ Admin được phân quyền mới được hủy; sau khi hủy được phép Start lại và bán bù vé.

## 5. Báo cáo tuyến (CITY-2813)

- Đồng bộ thủ công: chỉ **Super Admin**, chọn tối đa **3 ngày** bằng DateRangePicker.
- Đồng bộ tự động: job chạy lúc **09:00** và **00:00** ngày T+1 cho dữ liệu ngày T.
- Nếu phát hiện vé đồng bộ trễ → đánh dấu ngày cần re-sync, tự động chạy lại lúc **10:00** mỗi ngày.

## 6. Báo cáo "Giao dịch đồng bộ trễ"

- Giao diện tương tự Lịch sử mua vé, bổ sung cột: **Thời gian đồng bộ**, **Mã lệnh tổng**, **Mã lệnh chi tiết**.
- 3 loại filter: (1) **Giao dịch qua ngày** — đã có; (2) Giao dịch đồng bộ sau đẩy lệnh — đang cập nhật; (3) Giao dịch không nằm trong lệnh — đang cập nhật.
- Đây là công cụ chính để phát hiện vé bị trễ **sau khi eLVC đã đẩy** (rủi ro mất trợ giá — xem file Core, mục 4).

## 7. Sự cố & quy định vận hành riêng của dự án

### 7.1. Sự cố cập nhật ứng dụng giữa chuyến (17/11/2026)

- Smartbus cập nhật phiên bản mới qua MDM → ứng dụng không phản hồi.
- GoPS tự kết thúc chuyến trong khi còn khách trên xe → khách tap out bị từ chối.

**Quy định rút ra:**
- Chỉ cập nhật ứng dụng **ngoài giờ xe chạy: sau 22:00 hoặc trước 05:00**.
- Cải tiến GoPS: **không tự kết thúc chuyến** khi Smartbus mất kết nối tạm thời.

### 7.2. Đối soát phía Smartbus

- Trước 11:00 ngày T+1 phải chốt đầy đủ dữ liệu chuyến và sản lượng trên Smartbus.
- Các trường hợp đồng bộ trễ xử lý sau thông qua báo cáo Giao dịch đồng bộ trễ.
- Khi có chuyển đổi vé HSSV sau đối chiếu (cơ chế ở file Core, mục 5), cần kiểm tra lại sản lượng trên các báo cáo và eLVC của dự án.
