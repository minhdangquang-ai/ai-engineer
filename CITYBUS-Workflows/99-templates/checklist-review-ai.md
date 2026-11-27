# Checklist review US có dùng AI hỗ trợ

Áp dụng cho **mọi file US có dùng AI hỗ trợ soạn thảo**, trước khi chuyển trạng thái "Đã chốt nghiệp vụ".

## Mức review theo rủi ro

| Loại US | Yêu cầu |
|---|---|
| US thông thường | BA tự review theo checklist này + comment ký xác nhận trên Jira |
| US đụng tới **tiền / trợ giá / thanh toán / đối soát** (vé, eLVC, VNPay...) | **Bắt buộc peer review bởi người thứ hai** |

## Checklist

- [ ] Mọi **con số, mốc giờ, tên hệ thống** trong US đã đối chiếu với nguồn gốc (không để số liệu do AI tự suy đoán)
- [ ] **Không có business rule nào không có nguồn** — mỗi BR truy được về tài liệu/yêu cầu gốc
- [ ] Thuật ngữ đúng chuẩn Citybus: **TTCC / GoLab / GoAFC / GoPS / Smartbus** dùng đúng vai trò, không lẫn lộn
- [ ] Mọi **Acceptance Criteria đều kiểm thử được** (QC đọc AC là viết được test case)
- [ ] Đã xét **trường hợp ngoại lệ** và luồng lỗi (mất kết nối, đồng bộ trễ, dữ liệu thiếu...)
- [ ] Phần đầu file đã điền đủ: **Nguồn đối chiếu / Người review / Ngày review**
- [ ] Mục không áp dụng đã ghi "Không áp dụng" thay vì xóa
- [ ] (Nếu sửa tính năng cũ) Đã có đủ 2 phần **Hiện trạng đang chạy** + **Thay đổi yêu cầu**

> Thiếu Nguồn đối chiếu / Người review / Ngày review: **QC/DEV có quyền trả Task về**.
