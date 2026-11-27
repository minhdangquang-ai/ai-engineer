# Nghiệp vụ riêng theo US — Dự án Smartbus App vs GoPS App (Tầng 3)

Thư mục chứa nghiệp vụ chi tiết theo từng User Story, tổ chức theo trạng thái xếp sprint:

| Thư mục con | Ý nghĩa |
|---|---|
| `backlog/` | US chưa được xếp vào sprint nào |
| `sprint-1/` | US thuộc Sprint 1 — giai đoạn hiện tại |

Quy tắc chung:

- Mỗi User Story 1 file, đặt tên: `<Mã task>-<tên ngắn>.md` (kebab-case, không dấu).
- Tạo file mới từ `99-templates/template-us.md`.
- Dự án này là dự án đang làm: nếu US sửa tính năng cũ, bắt buộc dùng thêm `99-templates/template-hien-trang-thay-doi.md`.
- Nghiệp vụ gốc để phân rã US: xem `../nghiep-vu-chung-du-an/nghiep-vu-chung-du-an.md`.
- File US là bản BA dùng để up lên Jira (Mô tả + file đính kèm snapshot khi chốt).
- Khi US được xếp vào sprint: move file từ `backlog/` sang thư mục sprint tương ứng (vd `sprint-1/`).
