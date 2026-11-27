# Nghiệp vụ chung của dự án — Smartbus App vs GoPS App

Thư mục chứa nghiệp vụ chung cấp dự án (Tầng 2).

## File gốc

- `nghiep-vu-chung-du-an.md` — tài liệu nghiệp vụ của dự án (tích hợp Smartbus App ↔ GoPS App trên máy POS T10: luồng SharedFolder, đồng bộ vé GoPS → GoAFC → Smartbus, eLVC của dự án...). Tên file **cố định, không dùng tiền tố ngày**.

## Quy tắc ghi thay đổi nghiệp vụ (Minh chốt ngày 2026-11-27, áp dụng thống nhất cho mọi dự án)

- Từ nay, **bất kỳ thay đổi nghiệp vụ nào cũng ghi riêng ra một file mới** đặt trong thư mục này — không ghi lẫn vào file gốc.
- Tên file thay đổi có tiền tố ngày theo định dạng **`yyyy-mm-dd`**: `yyyy-mm-dd-thay-doi-<noi-dung-ngan>.md` (vd `2026-11-28-thay-doi-dong-bo-ve.md`).
- Trong file thay đổi phải **chỉ rõ phần đã thay đổi**: mục/đoạn nào trong `nghiep-vu-chung-du-an.md` bị ảnh hưởng, nội dung trước → sau thay đổi, lý do thay đổi và task Jira liên quan (nếu có).

## Lịch sử

| Ngày | Việc |
|---|---|
| 2026-11-27 | Áp dụng logic thư mục của dự án App điều hành tài xế trên Tablet (FTT) cho dự án này: file `nghiep-vu-du-an.md` ở gốc hồ sơ được đổi tên và chuyển vào thư mục này thành `nghiep-vu-chung-du-an.md`; thư mục `us/` cũ được thay bằng `nghiep-vu-theo-us/` gồm `backlog/` và `sprint-1/`. |
