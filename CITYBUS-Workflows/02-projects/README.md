# 02-projects — Hồ sơ từng dự án (Tầng 2 + Tầng 3)

Mỗi dự án 1 thư mục, đặt tên theo quy ước: `<YYYY>-q<quý>-<tên ngắn>` — kebab-case, không dấu.
Ví dụ: `2026-q4-smartbus-vs-gops/`, `2026-q4-app-dieu-hanh-tai-xe/`.

## Cấu trúc bên trong 1 thư mục dự án

```text
<YYYY>-q<quý>-<tên dự án>/
├── README.md              # Mục lục của dự án (tạo từ 99-templates/template-du-an.md)
├── nghiep-vu-du-an.md     # Tầng 2 — Nghiệp vụ riêng của dự án
├── api-integration.md     # Tích hợp API riêng của dự án
└── us/                    # Tầng 3 — File US theo Task Jira
    └── <Mã task>-<tên ngắn>.md
```

## Quy định theo loại dự án

- **Dự án mới:** áp dụng cấu trúc chuẩn ngay từ đầu.
- **Dự án đang làm — tính năng mới:** file US link về Tầng 1/Tầng 2, chỉ ghi phần mới.
- **Dự án đang làm — sửa tính năng cũ:** file US bắt buộc có "Hiện trạng đang chạy" + "Thay đổi yêu cầu" (dùng `99-templates/template-hien-trang-thay-doi.md`).
