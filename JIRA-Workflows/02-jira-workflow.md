# Jira Workflow — Quy trình làm việc trên Jira cho team Citybus

> Nguồn quyết định: buổi phỏng vấn grill-me "JIRA-Workflows" ngày 2026-11-27 (file `phong-van/2026-11-27-jira-workflows.md`), gồm 15 câu hỏi; các điểm **tạm hoãn** được ghi rõ ở Mục 9.
> Tài liệu liên quan: `01-quy-chuan-dat-ten-ma-truy-vet.md` (quy chuẩn mã), `../workflow-quan-ly-nghiep-vu-citybus.md` (workflow quản lý nghiệp vụ tổng thể), kho nghiệp vụ `../CITYBUS-Workflows/`.

## 1. Bối cảnh vận hành

- Dự án chạy theo **Scrum**, sprint **2 tuần**.
- Team mỗi dự án: **1 BA, 1 QC, 1–2 DEV, 1 Designer**.
- BA là người chịu trách nhiệm chính về tính đúng của nghiệp vụ và là **người duy nhất sắp xếp thứ tự ưu tiên backlog** của dự án.

## 2. Cấu trúc Jira

- **Một project duy nhất:** key `CITY` trên `vatoteam.atlassian.net` (vd `CITY-2848`).
- **Mỗi dự án con = 1 Component** trong CITY (vd Component `FTT` — App điều hành tài xế trên Tablet; `SMB` — Smartbus; `HRA` — HR/Admin).
- **Mỗi dự án con có board Scrum riêng**, lọc theo Component của dự án đó.
- Mã dự án con hiển thị trên **tiêu đề (Summary)** của ticket theo quy chuẩn mã truy vết (xem tài liệu `01-...`).

## 3. Workflow trạng thái — Task/Story (chuỗi v2)

Tên trạng thái chuẩn hóa **tiếng Anh toàn bộ**.

**Luồng chính:**

```
Open → Drafting Specs → Spec Review → Spec Approved → Ready for Dev
     → In Progress → Ready for Test → In Testing → Done
```

| Trạng thái | Ý nghĩa |
|---|---|
| `Open` | Task vừa được tạo, chưa bắt đầu soạn nghiệp vụ |
| `Drafting Specs` | BA đang soạn US/nghiệp vụ |
| `Spec Review` | Đang review nghiệp vụ (theo phân tầng rủi ro: US thường BA tự review + ký xác nhận; US chạm tiền/trợ giá/thanh toán/đối soát bắt buộc peer review) |
| `Spec Approved` | Nghiệp vụ đã chốt — mốc khóa: thay đổi sau mốc này là Change Request (Mục 6) |
| `Ready for Dev` | Sẵn sàng để DEV bắt đầu |
| `In Progress` | DEV đang thực hiện |
| `Ready for Test` | DEV đã làm/fix xong, bàn giao cho QC |
| `In Testing` | QC đang kiểm thử |
| `Done` | **Đã qua QC kiểm thử đạt.** Đây là định nghĩa cứng — DEV làm xong chỉ tới `Ready for Test`, không bao giờ là Done |

**Trạng thái rẽ nhánh:**

| Trạng thái | Quy tắc |
|---|---|
| `Reopened` | QC test phát hiện lỗi → task quay lại `In Progress` để DEV xử lý |
| `Cancelled` | Hủy task/bug — vào được từ **mọi trạng thái**, **bắt buộc comment lý do** |
| `Won't Fix` | Chỉ áp dụng cho **Bug**; **DEV quyết định** và **bắt buộc comment lý do**; BA/QC không đồng ý thì chuyển `Reopened` |
| `Verifying on Prod` | Task/bug **không reproduce được trên môi trường DEV** → theo dõi/kiểm thử trên Prod, sau đó về `Done` hoặc `Reopened` |

## 4. Workflow trạng thái — Bug (rút gọn)

Bug dùng một workflow riêng rút gọn (không có các trạng thái soạn/chốt nghiệp vụ):

```
Open → In Progress → Ready for Test → In Testing → Done
```

Kèm đủ 4 rẽ nhánh: `Reopened`, `Won't Fix`, `Verifying on Prod`, `Cancelled` (quy tắc như Mục 3).

- Bug do QC tạo trong quá trình test: link tới US/task gốc (kiểu link **"blocks"** — bug chặn US đạt Done).
- Bug phát hiện trên Prod hoặc từ vận hành: cũng vào cùng luồng này, tạo ở `Open`, link tới US/dự án liên quan.
- Cấu trúc nội dung bug: theo prompt Bug Architect (`prompts/prompt-qc-agent-bug-architect.md`).

## 5. Assign task — cơ chế lai theo chặng

- **Sprint Planning chốt assignee cho từng chặng** của mỗi task:
  - Giai đoạn soạn/chốt nghiệp vụ (`Open` → `Spec Approved`): assignee = **BA**.
  - Từ `Ready for Dev` / `In Progress`: assignee = **DEV** đã được chốt ở Planning.
  - Từ `Ready for Test` / `In Testing`: assignee = **QC** của dự án.
- **Người giữ assignee tự chuyển trạng thái** trong chặng của mình.
- **BA có full quyền override:** thay đổi được **bất kỳ trạng thái nào của mọi task/bug** (xử lý khi người phụ trách vắng/kẹt). Override là ngoại lệ — luồng thường vẫn do assignee tự chuyển.

## 6. Change Request (thay đổi nghiệp vụ sau Spec Approved)

- **Không** tạo loại issue riêng, **không** tạo trạng thái riêng cho Change Request.
- Xử lý theo cơ chế đã chốt ở workflow nghiệp vụ tổng thể:
  - Task **chưa Done**: sửa tại chỗ trên task cũ — cập nhật file US + snapshot mới + tag mới, comment rõ phần thay đổi; QC test lại phần ảnh hưởng + regression.
  - Task **đã Done**: tạo **task mới** link **"relates to"** task cũ, không mở lại task cũ.
- Mọi thay đổi phát sinh sau `Spec Approved` gắn **label `change-request`** để truy vết và báo cáo tần suất thay đổi.

## 7. Sprint & backlog

- **Tên sprint:** `<Mã dự án> Sprint <số thứ tự> (<ngày bắt đầu>–<ngày kết thúc>)`
  - Ví dụ: `FTT Sprint 3 (01/12–12/12)`
- **Backlog:** BA là người duy nhất sắp xếp thứ tự ưu tiên.
- **Ước lượng:** chưa áp dụng ước lượng chính thức (không story point, không giờ công) — khi lên kế hoạch sprint, chỉ chia nhỏ US sao cho vừa 1 sprint.

## 8. Liên kết Jira ↔ kho nghiệp vụ CITYBUS-Workflows

- File US (Tầng 3) đính kèm/khớp với Task Jira theo mô hình 2 lớp: kho chính thuộc sở hữu công ty là bản nghiệp vụ đầy đủ nhất; Jira là lớp lưu vết (Description + snapshot tại thời điểm chốt + comment thay đổi).
- Thông báo bản nghiệp vụ mới: **comment trên Task Jira** (kèm tag + tóm tắt thay đổi) và **nhắn group chat chung của dự án**.
- Mã BR/CM trong file US tuân thủ quy chuẩn ở tài liệu `01-...`; AC giữ dạng `AC-01`.

## 9. Các điểm tạm hoãn (chưa áp dụng — xem xét lại sau)

| Nội dung | Trạng thái |
|---|---|
| Ánh xạ chi tiết từng loại mã (FR/NFR/SCR/US/BR/CM/Bug) sang issue type của Jira | **Tạm hoãn** — chốt sau khi làm rõ thêm |
| Definition of Ready (DoR) / Definition of Done (DoD) chính thức | **Chưa làm** — xem xét lại sau khi workflow chạy thực tế (riêng định nghĩa cứng của `Done` ở Mục 3 vẫn áp dụng) |
| Chuẩn hóa ceremony Scrum (Planning/Daily/Review/Retro theo lịch cố định) | **Chưa chuẩn hóa** — họp theo phát sinh; mốc chốt assignee đầu sprint vẫn thực hiện theo Mục 5 |
