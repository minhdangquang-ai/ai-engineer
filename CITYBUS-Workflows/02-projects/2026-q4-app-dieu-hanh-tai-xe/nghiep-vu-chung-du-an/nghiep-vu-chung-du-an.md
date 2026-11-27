# NGHIỆP VỤ TỔNG QUAN DỰ ÁN: APP ĐIỀU HÀNH TÀI XẾ TRÊN TABLET

> **Quản trị tài liệu**
> - **Nguồn đối chiếu:** file "NGHIEP VU TONG QUAN DU AN APP DIEU HANH TAI XE TREN TABLET" do Minh gửi ngày 2026-11-27 — nghiệp vụ ban đầu của dự án.
> - **Người review:** Minh (BA) — chờ xác nhận
> - **Ngày review:** —
> - **Trạng thái:** Draft (nghiệp vụ ban đầu)
> - **Hiệu chỉnh khi lưu vào kho (2026-11-27, đã báo Minh):** (1) sửa vai trò GoAFC — GoAFC là hệ thống của **GoLab**, không phải "hệ thống của Nhà nước/TTCC"; (2) đổi nhãn "Mã dự án (Project Key)" thành "Mã dự án con (Component)" theo quy chuẩn Jira đã chốt (project key chung là `CITY`).
> - **Lưu vết (2026-11-27):** file đặt tại thư mục `nghiep-vu-chung-du-an/` (Nghiệp vụ chung của dự án), tên chuẩn `nghiep-vu-chung-du-an.md` — **không dùng tiền tố ngày cho file gốc**. Mọi thay đổi nghiệp vụ về sau ghi riêng thành file mới đặt trong cùng thư mục, tên có tiền tố ngày theo định dạng `yyyy-mm-dd` (vd `2026-11-28-thay-doi-<noi-dung>.md`) và chỉ rõ phần đã thay đổi — theo quy tắc Minh chốt ngày 2026-11-27 (thay cho ý định tiền tố `dd.mm.yyyy` trước đó).

* **Mã dự án con (Component trên Jira `CITY`):** `FTT` (Futa Tech Tablet)
* **Tên định danh kho lưu trữ:** `2026-q4-app-dieu-hanh-tai-xe`
* **Phạm vi tài liệu:** Tài liệu Nghiệp vụ cấp Dự án (Project-Level Domain) — quy định ranh giới hệ thống, luồng tích hợp và các nguyên tắc vận hành xuyên suốt toàn bộ ứng dụng.
* **Tài liệu liên quan:** nghiệp vụ chung Citybus — xem `../../../01-core-wiki/00-nghiep-vu-core-citybus.md`. (File danh mục nghiệp vụ theo từng chức năng chính từng lưu kèm file này đã được xóa ngày 2026-11-27 theo yêu cầu của Minh.)

---

## 1. Ranh giới Hệ thống & Phân vai Thiết bị (System Boundaries)

Trong hệ sinh thái vận hành xe buýt điện **CITYBUS**, trên mỗi phương tiện bố trí 2 thiết bị vận hành độc lập. Dự án `FTT` xác định rõ ranh giới trách nhiệm như sau:

| Thiết bị / Hệ thống | Vai trò chính | Phạm vi nghiệp vụ |
| :--- | :--- | :--- |
| **Máy POS T10** *(Hệ thống hiện hữu: App Smartbus & App GoPS)* | **Khởi tạo chuyến & Bán vé** | Thực hiện thao tác Start chuyến (Smartbus) và bán vé hành khách (GoPS). Dữ liệu bán vé đẩy về **GoAFC** (hệ thống của GoLab), sau đó đồng bộ ngược về **FUTA Smartbus**. |
| **Tablet Điều hành (`FTT`)** *(Dự án phát triển mới)* | **Bảng điều khiển trung tâm cho Lái xe** | **Không thực hiện nghiệp vụ bán vé.** Chỉ đọc và đồng bộ dữ liệu (Read/Sync) từ GoAFC, Smartbus và phần cứng trên xe (GPS động, Camera, Loa, T10) để hỗ trợ tài xế điều hành chuyến, giám sát an toàn và liên lạc trực tuyến với OCC. |

---

## 2. Nguyên tắc "Nguồn chân lý duy nhất" (Single Source of Truth)

Để tránh xung đột dữ liệu giữa các hệ thống tích hợp, dự án `FTT` tuân thủ phân cấp nguồn dữ liệu gốc như sau:

1. **Hệ thống GoAFC (của GoLab — nền tảng quản lý buýt phục vụ TTCC):**
   * Nguồn dữ liệu gốc cho: Tài khoản định danh lái xe (SĐT & mật khẩu), danh mục tuyến, tài, giờ xuất bến theo quy chuẩn nhà nước và dữ liệu bán vé gốc từ GoPS.
2. **Hệ thống FUTA Smartbus (Quản trị Nội bộ Doanh nghiệp):**
   * Nguồn dữ liệu gốc cho: Hồ sơ nhân sự, trạng thái làm việc (`ACTIVE` / `INACTIVE`), lịch phân công ca/xe và Lệnh vận chuyển trong ngày.
3. **Phần cứng trực tiếp trên xe buýt điện:**
   * Nguồn dữ liệu gốc cho: Tọa độ GPS động, vận tốc tức thời, trạng thái mức pin xe điện (SOC), luồng hình ảnh Camera giám sát và trạng thái kết nối các thiết bị ngoại vi.

---

## 3. Vòng đời Vận hành Chuẩn của 1 Ca làm việc (End-to-End Lifecycle)

Toàn bộ ứng dụng vận hành theo một chu trình khép kín, ràng buộc chặt chẽ theo trạng thái ca làm việc:

```text
[1. Đăng nhập chéo 2 hệ thống (FTT-FR-001)]
      |
      v
[2. Nhận thông tin tài xế & Lệnh vận chuyển (FTT-FR-002)]
      |
      v
[3. Kiểm tra tình trạng an toàn xe đầu ca (FTT-FR-003)]
      |
      v
[4. Vận hành chuyến & Giám sát thời gian thực (FTT-FR-004 -> FTT-FR-010)]
      |
      v
[5. Xác nhận kiểm tra & chốt xe cuối ca (FTT-FR-003)]
      |
      v
[6. Đăng xuất & Bàn giao thiết bị (FTT-FR-001)]
```

---

## 4. Các Quy tắc Vận hành Xuyên suốt Toàn Dự án (Cross-Cutting Rules)

Mọi tính năng (`FTT-FR-001` đến `FTT-FR-010`) đều phải tuân thủ 4 nhóm nguyên tắc nền tảng sau:

### 4.1. Nguyên tắc An toàn Giao thông (Safety-First)
* Mọi thao tác làm gián đoạn màn hình điều khiển hoặc thay đổi phiên đăng nhập (Đăng xuất thủ công, Force Logout khi bị khóa tài khoản trên Smartbus, hết hạn phiên 18 tiếng) **chỉ được phép thực thi khi xe đã dừng hẳn (`Speed == 0 km/h`)**.
* Giao diện thiết kế tối giản thao tác chạm (Large Touch Targets), ưu tiên hiển thị trực quan và cảnh báo âm thanh để tài xế không bị xao nhãng khi đang lái xe.

### 4.2. Chế độ Kiosk & Tự phục hồi Phiên làm việc
* Ứng dụng chạy ở chế độ **Kiosk Mode** (khóa cứng trên Tablet, ngăn tài xế thoát ra ngoài hệ điều hành hoặc cài đặt ứng dụng ngoài).
* Khi Tablet bị tắt nguồn đột ngột hoặc khởi động lại trong thời hạn phiên còn hiệu lực (tối đa 18 tiếng), ứng dụng phải tự khởi động và khôi phục lại đúng màn hình vận hành trước đó từ bộ nhớ mã hóa cục bộ (Encrypted Local Storage) mà không yêu cầu đăng nhập lại.

### 4.3. Cơ chế Offline-First & Xử lý Lỗi mạng (`FTT-CM-EXC`)
* **Mất kết nối Internet (`FTT-CM-EXC-001`):** Khi thiết bị mất sóng 4G/Wi-Fi quá 5 giây, hiển thị banner cảnh báo đỏ ở góc trên màn hình (*"Mất kết nối mạng. Đang thử kết nối lại..."*). Các tính năng cốt lõi như bản đồ tuyến đã cache, cảnh báo tốc độ theo GPS và phát thanh trạm dừng cục bộ vẫn phải duy trì hoạt động ổn định.
* **Lỗi API / Timeout (`FTT-CM-EXC-002`):** Khi API từ GoAFC hoặc Smartbus phản hồi quá 10 giây hoặc trả mã lỗi `500/502/503`, hệ thống không được treo (freeze) mà phải hiển thị thông báo chuẩn kèm mã lỗi kỹ thuật.

### 4.4. Quy tắc Ưu tiên Âm thanh trên Xe (Audio Priority)
Khi nhiều nguồn phát âm thanh cùng được kích hoạt tại một thời điểm, hệ thống áp dụng thứ tự ưu tiên ngắt (Interrupt) từ cao xuống thấp:
1. **Ưu tiên 1 (Cao nhất):** Cuộc gọi thoại / Lệnh cảnh báo khẩn cấp từ Trung tâm Điều hành OCC (`FTT-FR-007`).
2. **Ưu tiên 2:** Cảnh báo vi phạm tốc độ và an toàn lái xe (`FTT-FR-005`).
3. **Ưu tiên 3:** Phát thanh tự động đọc tên trạm dừng hoặc thông báo hành khách (`FTT-FR-008`).
