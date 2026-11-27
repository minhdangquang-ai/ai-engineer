# NGHIỆP VỤ CORE CHUNG — CITYBUS

> **Mục đích của file này:** đây là file nghiệp vụ **dùng chung cho toàn bộ hệ thống Citybus**, viết dạng tự chứa (đủ ngữ cảnh, có giải thích thuật ngữ) để **bất kỳ QC/DEV nào cũng có thể nạp file này làm ngữ cảnh (context) cho AI** khi phân tích, viết test case hoặc phát triển tính năng cho bất kỳ dự án Citybus nào.
>
> **Quy tắc:** file này chỉ chứa nghiệp vụ chung — không chứa nghiệp vụ riêng của dự án. Nội dung phải ổn định; mọi thay đổi do BA chốt và merge vào `main` theo quy trình chung. Cập nhật đến: 27/11/2026.

---

## 1. Các bên và hệ thống trong hệ sinh thái Citybus

| Thành phần | Vai trò |
|---|---|
| **TTCC** (Trung tâm Công cộng) | Đơn vị **nhà nước** quản lý hệ thống buýt **toàn thành phố** của tất cả công ty vận tải (FUTA chỉ là 1 công ty). TTCC căn cứ eLVC để tất toán **trợ giá** và chuyển tiền cho các công ty vận tải |
| **GoLab** | Đơn vị (vendor) **cung cấp giải pháp cho TTCC** — không phải đơn vị nhà nước. GoLab cung cấp 2 sản phẩm: GoPS và GoAFC |
| **GoPS** | Ứng dụng **bán vé chính trên xe buýt**, chạy trên máy POS T10, do GoLab cung cấp cho TTCC |
| **GoAFC** | Hệ thống Admin quản lý buýt do GoLab cung cấp cho TTCC: quản lý buýt toàn thành phố (nhiều công ty), tiếp nhận vé từ GoPS, phục vụ đối soát và trợ giá |
| **Smartbus** | Hệ thống **nội bộ của FUTA**: Smartbus Admin (quản trị) + App Smartbus trên T10 |
| **Máy POS T10** | Thiết bị bán vé đặt trên xe buýt |
| **Giờ tài** | Ca/phiên làm việc của 1 xe + tài xế trong ngày; là đơn vị quản lý chuyến và xác thực vé |
| **eLVC** (Lệnh vận chuyển điện tử) | Chứng từ điện tử chốt sản lượng của **1 tuyến trong 1 ngày** (1 eLVC gồm nhiều chuyến); là căn cứ để TTCC tất toán trợ giá |

## 2. Chính sách miễn phí vé từ 01/10/2026

Từ ngày **01/10/2026**, toàn bộ người dân được **miễn phí vé** xe buýt, nhưng bắt buộc **xác thực công dân hợp pháp** trước khi lên xe bằng 1 trong 3 cách:

- Quét mã QR **Căn cước mẫu mới** (CCCD)
- Quét mã QR **Thẻ giao thông công cộng** (đã định danh với CCCD gốc)
- Quét mã QR từ **App VNeID**

Quy tắc bắt buộc:

- **Không xác thực lại** cùng một mã QR trong **cùng 1 giờ tài**.
- Máy T10 **không còn hiển thị** hình thức bán tiền mặt hoặc vé miễn thủ công.
- Toàn bộ sản lượng vé được nghiệm thu giữa công ty vận tải và TTCC (qua GoAFC) để nhà nước chuyển tiền trợ giá — vì vậy **mọi lượt đi đều phải có vé/giao dịch ghi nhận trên hệ thống**.

## 3. Quy trình eLVC và các mốc giờ ngày T+1

eLVC của ngày vận doanh **T** phải hoàn thành trong ngày **T+1** theo các mốc sau (giờ Việt Nam):

| Mốc giờ | Việc bắt buộc |
|---|---|
| Trước **08:00** ngày T+1 | Điều hành bấm **"Kiểm tra sản lượng vé"** — đồng bộ chủ động sản lượng từ GoAFC về hệ thống của công ty để hạn chế thiếu sót |
| Trước **11:00** ngày T+1 | Chốt đầy đủ dữ liệu chuyến và sản lượng |
| Trước **12:00 trưa** ngày T+1 | Điều hành ký xác nhận và bấm **"Hoàn thành eLVC"** — đây là **hạn chót cứng**, eLVC được đẩy sang GoAFC/TTCC |

Sau khi nhận eLVC, TTCC tất toán trợ giá và chuyển tiền cho công ty vận tải.

## 4. Nguyên tắc trợ giá và đối soát (áp dụng cho mọi dự án)

- Vé chỉ được tính trợ giá khi **đã có trên GoAFC** tại thời điểm chốt eLVC.
- **Đồng bộ trễ sau khi đã đẩy eLVC** (ví dụ vé bán ngày T nhưng đến T+2 mới đồng bộ về) khiến vé đó **không được TTCC trợ giá** → công ty vận tải bị thiệt. Đây là rủi ro nghiệp vụ nghiêm trọng nhất của hệ thống.
- **Giao dịch qua ngày:** vé bán trong ngày T nhưng đồng bộ về sau mốc chốt T+1 vẫn phải được ghi nhận đúng **ngày vận doanh bán vé** (kể cả chuyến bị DXMC).
- Khi hệ thống GoAFC/GoPS bị lỗi: chỉ được mở lại hình thức vé miễn/vé tập (cùi giấy) khi có **xác nhận lỗi hệ thống từ GoLab**; dữ liệu fallback phải được **đánh dấu rõ nguồn gốc** để đối soát về sau.

## 5. Chuyển đổi vé học sinh — sinh viên (HSSV)

- GoAFC đối chiếu các giao dịch thanh toán bằng CCCD với dữ liệu của **Sở Giáo dục**.
- Nếu đúng đối tượng HSSV, giao dịch tự động chuyển từ **vé lượt** sang **vé CCCD HS-SV**.
- Hệ quả cần nhớ khi làm bất kỳ báo cáo/eLVC nào: **sản lượng vé lượt và vé HSSV có thể thay đổi sau thời điểm đối chiếu**.

---

*File này được tách ra từ tài liệu tổng hợp nghiệp vụ Citybus (cập nhật 26/11/2026) — chỉ giữ phần dùng chung toàn hệ thống. Nghiệp vụ riêng của từng dự án nằm trong `02-projects/<dự án>/`.*
