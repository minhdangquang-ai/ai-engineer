# JIRA-Workflows

Thư mục chứa **quy chuẩn làm việc trên Jira** cho team Citybus — song song với `CITYBUS-Workflows/` (kho nghiệp vụ) và `../workflow-quan-ly-nghiep-vu-citybus.md` (workflow quản lý nghiệp vụ tổng thể).

> Nguồn quyết định: buổi phỏng vấn grill-me "JIRA-Workflows" ngày 2026-11-27 (15 câu hỏi, file `../phong-van/2026-11-27-jira-workflows.md`).
> Hai điểm còn **tạm hoãn**: ánh xạ chi tiết loại mã → issue type Jira; DoR/DoD chính thức (xem Mục 9 của tài liệu workflow).

## Mục lục

| File | Nội dung |
|---|---|
| `01-quy-chuan-dat-ten-ma-truy-vet.md` | Quy chuẩn đặt tên & mã truy vết: công thức mã FR/NFR/SCR/US/BR/CM/TC, 7 nhóm ràng buộc, BR vs CM, định dạng tiêu đề ticket, nguyên tắc Self-Contained Story |
| `02-jira-workflow.md` | Cấu trúc Jira (project CITY, Component, board theo dự án), chuỗi trạng thái v2 cho Task/Story, workflow Bug rút gọn, assign theo chặng + quyền override của BA, Change Request bằng label, tên sprint & quản lý backlog |
| `prompts/prompt-ba-agent.md` | Prompt chuẩn cho AI Agent hỗ trợ BA sinh US/BR/CM (khóa cứng quy chuẩn mã) |
| `prompts/prompt-qc-agent-testcase.md` | Prompt chuẩn cho AI Agent hỗ trợ QC sinh Test Case từ US |
| `prompts/prompt-qc-agent-bug-architect.md` | Prompt chuẩn cho AI Agent hỗ trợ QC tạo Bug (kiến trúc 4 bước, đã hiệu chỉnh bảo mật + khớp workflow đã chốt) |

## Tóm tắt nhanh

- **Jira:** 1 project key `CITY`; mỗi dự án con = 1 **Component** + 1 board Scrum riêng; sprint 2 tuần, tên sprint dạng `FTT Sprint 3 (01/12–12/12)`.
- **Trạng thái Story:** `Open → Drafting Specs → Spec Review → Spec Approved → Ready for Dev → In Progress → Ready for Test → In Testing → Done` — **Done = đã qua QC kiểm thử đạt**.
- **Trạng thái Bug (rút gọn):** `Open → In Progress → Ready for Test → In Testing → Done`; cả hai luồng đều có `Reopened / Cancelled / Won't Fix / Verifying on Prod`.
- **Assign:** chốt theo chặng tại Sprint Planning (BA → DEV → QC); **BA có full quyền override** mọi trạng thái.
- **Change Request:** không tạo issue/trạng thái riêng — xử lý theo cơ chế sửa tại chỗ / tạo task mới và gắn label `change-request`.
