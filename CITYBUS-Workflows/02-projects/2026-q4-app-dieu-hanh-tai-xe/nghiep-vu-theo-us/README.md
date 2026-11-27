# Nghiệp vụ riêng theo US — Dự án App điều hành tài xế trên Tablet, FTT (Tầng 3)

Thư mục chứa nghiệp vụ chi tiết theo từng User Story, tổ chức theo trạng thái xếp sprint:

| Thư mục con | Ý nghĩa |
|---|---|
| `backlog/` | US chưa được xếp vào sprint nào |
| `sprint-1/` | US thuộc Sprint 1 — giai đoạn hiện tại |

Quy tắc chung:

- Mỗi User Story 1 file, đặt tên: `<Mã task>-<tên ngắn>.md` (kebab-case, không dấu).
- Tạo file mới từ `99-templates/template-us.md`.
- Mã US/BR/CM theo quy chuẩn đặt tên & mã truy vết: `JIRA-Workflows/01-quy-chuan-dat-ten-ma-truy-vet.md` (vd `FTT-US-001.01`, `FTT-BR-001.01-VAL-01`).
- Nghiệp vụ gốc để phân rã US: xem `../nghiep-vu-chung-du-an/nghiep-vu-chung-du-an.md` (nghiệp vụ chung của dự án).
- File US là bản BA dùng để up lên Jira (Mô tả + file đính kèm snapshot khi chốt).
- Khi US được xếp vào sprint: move file từ `backlog/` sang thư mục sprint tương ứng (vd `sprint-1/`).
