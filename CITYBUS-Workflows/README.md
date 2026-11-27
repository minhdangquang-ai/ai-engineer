# CITYBUS-Workflows — Kho nghiệp vụ Citybus (tối ưu cho vai trò BA)

Đây là **kho nghiệp vụ chính** của các dự án Citybus: nơi chứa bản nghiệp vụ **đầy đủ và mới nhất** để BA phát hành và QC/DEV clone về làm việc. Quy trình vận hành đầy đủ nằm trong tài liệu [Workflow quản lý nghiệp vụ Citybus](../workflow-quan-ly-nghiep-vu-citybus.md).

## Cấu trúc thư mục

| Thư mục | Nội dung |
|---|---|
| `00-inbox/` | Sổ tiếp nhận thông tin thô của BA theo ngày — trạng thái "Chờ lên Jira" / "Đã lên Jira [link]" |
| `01-core-wiki/` | **Tầng 1** — Nghiệp vụ chung Citybus. File chính: `00-nghiep-vu-core-citybus.md` — **file Core duy nhất, dùng để nạp ngữ cảnh cho AI**; các file còn lại chia theo miền |
| `02-projects/` | **Tầng 2 + Tầng 3** — Hồ sơ từng dự án (`<YYYY>-q<quý>-<tên dự án>/`), bên trong có `nghiep-vu-chung-du-an/` (nghiệp vụ chung của dự án + file thay đổi theo ngày `yyyy-mm-dd`), `nghiep-vu-theo-us/` (US theo Task Jira, chia `backlog/` và `sprint-<n>/`) và `bien-ban-hop/` (biên bản họp theo ngày, nhóm theo tháng) |
| `03-resources/` | Tài nguyên phục vụ BA đối chiếu (môi trường, thiết bị, đối tác) |
| `04-bao-cao-ngay/` | Báo cáo hằng ngày của BA gửi cấp trên **trước 16:00**, nhóm theo tháng |
| `99-templates/` | Template dự án, template US, template Hiện trạng + Thay đổi, template biên bản họp, template báo cáo ngày, checklist review AI |

## Quy tắc bắt buộc

- Chỉ **BA (maintainer)** được merge vào `main`. QC/DEV chỉ đọc/clone, góp ý qua comment trên Task Jira.
- Mọi soạn thảo làm trên branch `draft/<mã task>`, qua cổng review mới merge vào `main`.
- Tag theo ngày + mã Task Jira: `YYYY-MM-DD_<Mã task>` (tạm chốt, sẽ rà soát sau pilot).
- **Không ghi mật khẩu thật vào git** — file môi trường chỉ ghi URL, tên tài khoản và nơi lấy mật khẩu.
- Commit message theo quy ước ở mục dưới.

## Quy ước commit (để dễ truy vết)

Định dạng: `<type>(<scope>): <mô tả ngắn> [Mã Jira]`

- **type**: `docs` (tài liệu nghiệp vụ), `feat` (nghiệp vụ/tính năng mới), `log` (ghi inbox/nhật ký), `chore` (việc lặt vặt, cấu trúc kho)
- **scope**: khu vực bị tác động, ví dụ `inbox`, `core-wiki`, `us`, `templates`, tên dự án
- **mô tả**: ngắn gọn, nói rõ làm gì — người đọc log phải hiểu được mà không cần mở file
- **[Mã Jira]**: đặt cuối message khi commit gắn với 1 Task; commit cấp kho (không gắn Task nào) thì bỏ qua

Ví dụ:
- `docs(us): chốt US bán vé qua VNPay [CITY-1234]`
- `log(inbox): ghi nhận yêu cầu từ vận hành ngày 2026-11-27`
- `chore(templates): cập nhật checklist review AI sau pilot`
