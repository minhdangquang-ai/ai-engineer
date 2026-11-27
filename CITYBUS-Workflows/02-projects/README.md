# 02-projects — Hồ sơ từng dự án (Tầng 2 + Tầng 3)

Mỗi dự án 1 thư mục, đặt tên theo quy ước: `<YYYY>-q<quý>-<tên ngắn>` — kebab-case, không dấu.
Ví dụ: `2026-q4-smartbus-vs-gops/`, `2026-q4-app-dieu-hanh-tai-xe/`.

## Cấu trúc bên trong 1 thư mục dự án

Cấu trúc chuẩn này được chốt từ dự án App điều hành tài xế trên Tablet (FTT) ngày 2026-11-27 và áp dụng thống nhất cho mọi dự án.

```text
<YYYY>-q<quý>-<tên dự án>/
├── README.md                  # Mục lục của dự án (tạo từ 99-templates/template-du-an.md)
├── nghiep-vu-chung-du-an/     # Tầng 2 — Nghiệp vụ chung của dự án
│   ├── README.md              # Quy tắc ghi thay đổi + lịch sử thay đổi của dự án
│   ├── nghiep-vu-chung-du-an.md   # File nghiệp vụ gốc — tên cố định, KHÔNG tiền tố ngày
│   └── yyyy-mm-dd-thay-doi-<noi-dung>.md   # Mỗi thay đổi nghiệp vụ = 1 file riêng, chỉ rõ phần đã thay đổi
├── api-integration.md         # Tích hợp API riêng của dự án
├── nghiep-vu-theo-us/         # Tầng 3 — Nghiệp vụ riêng theo từng US
│   ├── backlog/               # US chưa được xếp vào sprint nào
│   └── sprint-1/              # US thuộc Sprint 1 (giai đoạn hiện tại); các sprint sau thêm sprint-2/, sprint-3/...
└── bien-ban-hop/              # Biên bản họp của dự án, nhóm theo tháng
    └── YYYY-MM/YYYY-MM-DD.md
```

## Quy tắc nghiệp vụ trong hồ sơ dự án

- File nghiệp vụ gốc của dự án luôn là `nghiep-vu-chung-du-an/nghiep-vu-chung-du-an.md` — tên cố định để mọi link tham chiếu ổn định.
- **Thay đổi nghiệp vụ:** ghi riêng ra file mới trong `nghiep-vu-chung-du-an/`, tên có tiền tố ngày định dạng `yyyy-mm-dd`, trong file chỉ rõ phần đã thay đổi (mục bị ảnh hưởng, nội dung trước → sau, lý do, task Jira liên quan). Không ghi lẫn thay đổi vào file gốc.
- US chưa vào sprint nằm ở `nghiep-vu-theo-us/backlog/`; khi Sprint Planning chốt vào sprint nào thì move file sang thư mục sprint đó.

## Quy định theo loại dự án

- **Dự án mới:** áp dụng cấu trúc chuẩn ngay từ đầu.
- **Dự án đang làm — tính năng mới:** file US link về Tầng 1/Tầng 2, chỉ ghi phần mới.
- **Dự án đang làm — sửa tính năng cũ:** file US bắt buộc có "Hiện trạng đang chạy" + "Thay đổi yêu cầu" (dùng `99-templates/template-hien-trang-thay-doi.md`).
