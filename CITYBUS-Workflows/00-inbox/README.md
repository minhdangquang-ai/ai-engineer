# 00-inbox — Sổ tiếp nhận thông tin thô của BA

Nơi BA ghi lại **mọi thông tin nghiệp vụ nhận được** từ chat, email, yêu cầu của vận hành/đối tác — trước khi chúng trở thành Task Jira chính thức.

## Cách tổ chức

- Mỗi ngày 1 file: `YYYY-MM/YYYY-MM-DD.md` (thư mục con theo tháng).
- Mỗi mục ghi trong file ngày gồm: nguồn thông tin, nội dung tóm tắt, trạng thái.

## Trạng thái của một mục

| Trạng thái | Ý nghĩa |
|---|---|
| ⏳ Chờ lên Jira | Mới là thông tin trao đổi — **chưa phải nghiệp vụ chuẩn** (Cổng "Nghiệp vụ Đúng") |
| ✅ Đã lên Jira [link Task] | Đã có Task Jira chính thức, nghiệp vụ được xử lý tiếp trong Task và kho này |

## Mẫu nội dung 1 file ngày

```markdown
# Inbox 2026-11-27

| # | Nguồn | Nội dung | Trạng thái |
|---|-------|----------|------------|
| 1 | Chat vận hành | Yêu cầu bổ sung báo cáo doanh thu theo tuyến | ⏳ Chờ lên Jira |
| 2 | Email đối tác | Thay đổi API thanh toán | ✅ Đã lên Jira [CITY-xxxx] |
```
