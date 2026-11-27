# JIRA-Workflows cho dự án Citybus (Scrum): ghi chép phỏng vấn
Ngày: 2026-11-27 · Mục tiêu: Chốt cách tổ chức và vận hành Jira cho các dự án Citybus theo mô hình Scrum — cấu trúc project/board/sprint, quy chuẩn đặt tên & mã truy vết, workflow trạng thái và luồng assign task — làm cơ sở xây dựng thư mục `JIRA-Workflows/` trong repo ai-engineer.
Trạng thái: đang phỏng vấn (grill-me, từng câu một)

## Bối cảnh Minh cung cấp khi bắt đầu (chưa phải quyết định chốt qua phỏng vấn)
- Đa phần dự án theo mô hình **SCRUM**. Ví dụ: dự án "App điều hành tài xế trên Tablet" — thư mục `2026-q4-app-dieu-hanh-tai-xe`, **mã dự án: FTT**.
- **1 Sprint thường kéo dài 2 tuần.**
- **Thành phần team:** 1 BA, 1 QC, 1–2 DEV, 1 Designer.
- Minh gửi kèm **Quy chuẩn đặt tên & đánh mã truy vết** để tham khảo (đã lưu tại `phong-van/tham-khao-2026-11-27-quy-chuan-dat-ten-ma-truy-vet.md`): công thức `[MÃ_DỰ_ÁN]-[LOẠI]-[MÃ_CHA].[SỐ]`; các loại FR/NFR/SCR/US/BR/CM/TC/BUG; 7 nhóm ràng buộc VAL/SEC/WFL/CAL/INT/EXC/FMT; 3 nguyên tắc vận hành Jira & AI (Rovo).
- Minh đặt vấn đề cần chốt: **luồng cấu hình Jira workflow assign task chuẩn**.
- Liên quan buổi phỏng vấn trước (đã chốt 26–27/11/2026, file `2026-11-26-workflow-quan-ly-nghiep-vu-citybus.md`): workflow nghiệp vụ 8 trạng thái cho 1 task (tạm chốt), mô hình kho CITYBUS-Workflows 3 tầng, template US với BR-/AC- đánh số đơn giản — buổi này sẽ đối chiếu/đồng bộ với chuẩn Jira mới.

## Tóm tắt các quyết định
- Câu 1: **Áp dụng quy chuẩn đặt tên & mã truy vết** làm chuẩn của JIRA-Workflows, kèm 3 làm rõ của Minh: (i) Jira chỉ có **1 project key `CITY`** (vatoteam.atlassian.net, vd CITY-2848) — `FTT` là mã dự án con hiển thị trên **title** ticket, mã truy vết ghi trên title; (ii) ví dụ chuẩn phân biệt BR (riêng 1 US: `FTT-BR-001.01-VAL-01`) với CM (dùng chung toàn dự án: `FTT-CM-VAL-002`) qua yêu cầu bắt buộc/độ dài mật khẩu; (iii) **TC của QC quản lý riêng ngoài Jira** — QC đọc task Jira tự xây bộ test case, chỉ tạo **bug trên Jira** gắn với task của BA khi phát hiện lỗi.
- Câu 2: **Tách dự án con bằng Component** (Minh chọn (a)): mỗi dự án con là 1 Component trong project CITY (vd `FTT`), mỗi dự án có board Scrum riêng lọc theo Component.
- Câu 4 (qua góp ý Câu 3): **Chuỗi trạng thái workflow v2 đã chốt** — chuẩn hóa tiếng Anh: `Open → Drafting Specs → Spec Review → Spec Approved → Ready for Dev → In Progress → Ready for Test → In Testing → Done` (Done = đã qua QC kiểm thử đạt; Ready for Test = Dev xong, bàn giao QC), rẽ nhánh: `Reopened` (test lỗi trả về), `Cancelled` (hủy, bắt buộc comment), `Won't Fix` (chỉ bug, DEV quyết + bắt buộc comment lý do), `Verifying on Prod` (không reproduce được ở DEV thì theo dõi/test trên Prod).
- Câu 5: **Assign theo cơ chế lai (c)**: Sprint Planning chốt assignee theo chặng BA → DEV → QC, assignee tự chuyển trạng thái chặng mình; **BA có full quyền override** — thay đổi bất kỳ trạng thái nào của mọi task/bug.
- Câu 7: **Change Request không tạo khái niệm riêng** (Minh chọn (c)): xử lý theo cơ chế Câu 13 buổi trước + gắn label `change-request` cho thay đổi sau Spec Approved.
- Câu 9: **Ceremony chưa chuẩn hóa** (Minh chọn (c)): họp theo phát sinh, không đặt lịch ceremony Scrum cố định.
- Câu 10: **Chưa ước lượng chính thức** (Minh chọn (c)): chỉ chia nhỏ US cho vừa 1 sprint, không dùng story point/giờ công.
- Câu 11: **Bug dùng workflow v2 rút gọn** (Minh chọn (b)): `Open → In Progress → Ready for Test → In Testing → Done` + Reopened/Won't Fix/Verifying on Prod/Cancelled.
- Câu 12: **Đồng bộ template US sang quy chuẩn mã mới** (Minh chọn (a)): BR/CM dùng mã chuẩn (`FTT-BR-001.01-VAL-01`, `FTT-CM-VAL-002`), AC giữ `AC-01`; việc sửa file template để sau phỏng vấn.
- Câu 13: **Tên sprint + backlog** (Minh chọn (a)): tên sprint mẫu `FTT Sprint 3 (01/12–12/12)`; BA là người duy nhất sắp xếp thứ tự ưu tiên backlog.
- Câu 14: **Bộ 3 prompt AI chuẩn** lưu trong `JIRA-Workflows/`: BA Agent (sinh US/BR/CM), QC Agent Test Case (sinh TC), QC Agent Bug Architect (kiến trúc 4 bước Minh gửi + 5 điểm hiệu chỉnh: không nhúng mật khẩu thật, key CITY + Component, assignee bug = DEV phụ trách US gốc, thêm Priority Critical cho mảng tiền/vé/eLVC, bug khởi tạo Open theo workflow rút gọn).

## Các câu hỏi

### Câu 1 · Áp dụng quy chuẩn đặt tên & mã truy vết làm chuẩn chính thức?
- Hỏi: Quy chuẩn đặt tên Minh gửi kèm có được chốt làm chuẩn chính thức của JIRA-Workflows không — (a) áp dụng nguyên vẹn; (b) áp dụng với điều chỉnh; hay (c) chỉ tham khảo, thiết kế lại?
- Đã chốt: Minh không trả lời trực tiếp (a)/(b)/(c) mà trả lời đầy đủ 3 điểm kỹ thuật Peter nêu — theo hướng **áp dụng quy chuẩn**, kèm 3 làm rõ quan trọng sau:
  1. **Jira thực tế chỉ có 1 project key là `CITY`** (site `vatoteam.atlassian.net`, ví dụ ticket `https://vatoteam.atlassian.net/browse/CITY-2848`). `FTT` **không phải Jira project key riêng** — FTT là tên/mã dự án con, dùng làm **quy tắc hiển thị trên title (Summary) của ticket**. Tức là: key hệ thống = `CITY-xxxx`; mã truy vết (`FTT-US-001.01`...) ghi trên title ticket. Điểm này **làm rõ/thay thế** cách ghi trong bản tham khảo ("mã dự án trùng khớp 100% với Project Key trên Jira").
  2. **Ví dụ chuẩn BR vs CM** (yêu cầu: "Trường Số điện thoại và Mật khẩu là bắt buộc. Mật khẩu dài 6–32 ký tự, không cho phép nhập khoảng trắng"): nếu ràng buộc chỉ riêng màn hình Đăng nhập → **BR**: `FTT-BR-001.01-VAL-01 | Kiểm tra trường bắt buộc và định dạng mật khẩu khi đăng nhập`; nếu dùng chung toàn dự án (sau này thêm màn hình Đổi mật khẩu/Tạo tài khoản dùng chung quy tắc) → **CM**: `FTT-CM-VAL-002 | Kiểm tra trường bắt buộc và độ dài mật khẩu tiêu chuẩn (6–32 ký tự)`.
  3. **Mã TC của QC KHÔNG sống trên Jira:** QC đọc task từ Jira rồi tự phân tích thành **bộ test case riêng** (quản lý ngoài Jira); **chỉ khi có bug**, QC mới tạo bug trên Jira tương ứng với task của BA.
- Đề xuất, chưa chốt: (đề xuất áp dụng quy chuẩn của Peter được Minh tiếp nhận kèm 3 làm rõ trên)
- Còn bỏ ngỏ: Với 1 Jira project CITY chứa nhiều dự án con -> phân tách board/sprint theo dự án con bằng cơ chế nào? -> Minh trả lời (Câu 2). Đồng bộ template US của CITYBUS-Workflows (BR-/AC-) với quy chuẩn mã mới -> hỏi ở câu sau.

### Câu 2 · Một Jira project CITY chứa nhiều dự án con: tách board/sprint thế nào?
- Hỏi: Khi mọi dự án con (FTT, SMB...) cùng nằm trong 1 project Jira `CITY`, mỗi dự án con vận hành Scrum (board + sprint riêng) bằng cơ chế nào — (a) mỗi dự án con là 1 **Component** trong CITY, board Scrum riêng lọc theo Component; (b) dùng **Label** thay cho Component; hay (c) không tách, 1 board chung cho tất cả, chỉ phân biệt bằng tiền tố trên title?
- Đã chốt: Minh chọn **(a)** — mỗi dự án con là 1 **Component** trong project CITY (ví dụ Component = `FTT`), và mỗi dự án con có **board Scrum riêng lọc theo Component** của mình.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Bộ trạng thái workflow trên Jira cho Story/Task trong Scrum — quan hệ với chuỗi 8 trạng thái nghiệp vụ đã chốt ở buổi phỏng vấn trước -> Minh trả lời (Câu 3)

### Câu 3 · Bộ trạng thái workflow Jira cho Story/Task: dùng chuỗi nghiệp vụ đã chốt hay tách 2 giai đoạn?
- Hỏi: Chuỗi 8 trạng thái nghiệp vụ đã tạm chốt ở buổi trước (Open → Đang soạn nghiệp vụ → Review nghiệp vụ → Đã chốt nghiệp vụ → Ready for Dev → In Progress → In Testing → Done) sẽ áp vào Jira thế nào — (a) dùng nguyên chuỗi đó làm workflow Jira cho Story/Task và board Scrum hiển thị tất cả các cột; (b) tách 2 giai đoạn: các trạng thái nghiệp vụ (soạn/review/chốt) diễn ra ở backlog **trước sprint**, board sprint chỉ hiển thị từ "Đã chốt nghiệp vụ" (= Ready) → In Progress → In Testing → Done; hay (c) bỏ chuỗi nghiệp vụ, dùng workflow Scrum chuẩn (To Do → In Progress → In Review → Done) và theo dõi nghiệp vụ bên ngoài Jira?
- Đã chốt: Minh không chọn (a)/(b)/(c) mà góp ý chi tiết để **sửa chính chuỗi trạng thái** (nguyên văn các ý): (1) thiếu trạng thái "Dev đã fix xong" để QC biết mà test; (2) thiếu trạng thái xử lý khi In Testing phát hiện lỗi; (3) task/bug còn có thể bị **hủy** hoặc **Won't fix bởi DEV — bắt buộc DEV phải comment**; (4) có task/bug **không reproduce được trên môi trường DEV**, phải theo dõi/test trên **Prod**; (5) trạng thái **Done gây nhầm lẫn** — không biết là Dev done hay QC done (Minh gợi ý hướng "Done by Dev and QC?"); (6) nên có/đổi thành trạng thái **Ready for Test** cho điểm bàn giao Dev → QC; (7) **các trạng thái nên chuẩn hóa một ngôn ngữ** — tiếng Anh hết hoặc tiếng Việt hết.
- Đề xuất, chưa chốt: (phương án tách 2 giai đoạn của Peter được gác lại; Peter soạn chuỗi trạng thái v2 theo 7 góp ý trên để Minh chốt ở Câu 4)
- Còn bỏ ngỏ: Chuỗi trạng thái v2 (chuẩn hóa tiếng Anh, có Ready for Test, Reopened, Cancelled, Won't Fix, trạng thái theo dõi trên Prod, định nghĩa lại Done) -> Minh xác nhận (Câu 4)

### Câu 4 · Chuỗi trạng thái workflow v2 (đã sửa theo góp ý của Minh)
- Hỏi: Có chốt chuỗi trạng thái v2 do Peter soạn theo 7 góp ý ở Câu 3 không — chuẩn hóa **tiếng Anh toàn bộ**; luồng chính: `Open → Drafting Specs → Spec Review → Spec Approved → Ready for Dev → In Progress → Ready for Test → In Testing → Done`; trong đó `Ready for Test` = Dev đã làm/fix xong, bàn giao QC; `Done` được định nghĩa cứng là **đã qua QC kiểm thử đạt** (Dev xong chỉ tới Ready for Test nên không còn nhầm lẫn); các trạng thái rẽ nhánh: `Reopened` (QC test lỗi → trả về, từ In Testing quay lại In Progress), `Cancelled` (hủy task, vào được từ mọi trạng thái, bắt buộc comment lý do), `Won't Fix` (chỉ cho bug, DEV quyết định, **bắt buộc comment lý do**, BA/QC không đồng ý thì Reopened lại), `Verifying on Prod` (không reproduce được ở DEV → theo dõi/test trên Prod, sau đó về Done hoặc Reopened)?
- Đã chốt: Minh trả lời "ok" — **chốt chuỗi trạng thái workflow v2** như đề xuất: luồng chính 9 trạng thái tiếng Anh `Open → Drafting Specs → Spec Review → Spec Approved → Ready for Dev → In Progress → Ready for Test → In Testing → Done` (Done = đã qua QC đạt), kèm 4 trạng thái rẽ nhánh `Reopened`, `Cancelled`, `Won't Fix`, `Verifying on Prod` với các quy tắc bắt buộc comment như đã nêu.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Luồng assign task: ai là assignee ở từng giai đoạn và cơ chế gán (đẩy/pull) -> Minh trả lời (Câu 5)

### Câu 5 · Luồng assign task: ai giữ assignee ở từng giai đoạn?
- Hỏi: Assignee của 1 Story/Task được gán theo cơ chế nào — (a) **Pull (Scrum chuẩn):** task ở trạng thái chờ thì để trống/chung, DEV tự nhận (self-assign) khi kéo vào In Progress, QC tự nhận khi kéo vào In Testing; (b) **Push:** BA chốt người phụ trách cụ thể ngay từ Sprint Planning cho cả vòng đời task; hay (c) **Lai:** Sprint Planning chốt trước người phụ trách chính cho từng chặng (BA giữ assignee ở giai đoạn soạn/chốt nghiệp vụ; sang Ready for Dev thì assignee là DEV đã được chốt ở Planning; Ready for Test thì chuyển assignee sang QC của dự án), và chính người giữ assignee là người chuyển trạng thái chặng của mình?
- Đã chốt: Minh chọn **(c)** — cơ chế lai: assignee được chốt theo chặng tại Sprint Planning (BA → DEV → QC), người giữ assignee tự chuyển trạng thái chặng của mình. **Bổ sung quan trọng của Minh: BA có full quyền thay đổi bất kỳ trạng thái nào của mọi task/bug** (quyền override để xử lý khi người phụ trách vắng/kẹt — nhất quán với thực tế team chỉ có 1 BA); việc override là ngoại lệ, luồng thường vẫn do assignee tự chuyển.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận, kèm bổ sung quyền override của BA)
- Còn bỏ ngỏ: Ánh xạ các loại mã (FR/NFR/SCR/US/BR/CM/Bug) sang issue type của Jira -> Minh trả lời (Câu 6)

### Câu 6 · Ánh xạ loại mã truy vết sang issue type trên Jira
- Hỏi: Mỗi loại trong quy chuẩn đặt tên sẽ tương ứng với cái gì trên Jira — (a) chỉ FR/US/Bug là issue thật (FR = Epic, US = Story, Bug = Bug), còn SCR/NFR/BR/CM chỉ là mã ghi trong Description, không tạo issue riêng; (b) mọi loại đều tạo issue riêng (FR/NFR = Epic, US = Story, SCR = Task, CM = Story); hay (c) FR = Epic, US = Story, Bug = Bug, **SCR = Sub-task của US** (để Designer có việc rõ trên board), **NFR = Story**, **CM = Story nằm trong 1 Epic "Thư viện rule dùng chung"** của dự án, **BR không tạo issue** (là nội dung trong Description của chính US đó)?
- Đã chốt: **Tạm hoãn — Minh chưa chốt Câu 6** (nguyên văn: "Tạm thời tôi chưa chốt câu 6"). Minh yêu cầu khi cần làm rõ thì liệt kê đầy đủ tên viết tắt (đã bổ sung Phụ lục A ở cuối file này). Đồng thời Minh đặt thêm vấn đề: **trạng thái/loại Change Request** xử lý thế nào -> chuyển thành Câu 7.
- Đề xuất, chưa chốt: (phương án (c) của Peter giữ nguyên chờ Minh quay lại chốt)
- Còn bỏ ngỏ: Câu 6 sẽ chốt sau. Change Request trên Jira -> Minh trả lời (Câu 7)

### Câu 7 · Change Request (CR) trên Jira: là trạng thái hay loại issue?
- Hỏi: Khi nghiệp vụ thay đổi sau khi US đã Spec Approved (đang dev/test hoặc đã Done), Change Request được quản lý thế nào — (a) CR là **1 loại issue riêng** trên Jira (title chứa mã CR, link tới US gốc), đi quy trình rút gọn Drafting → Spec Review → Spec Approved rồi mới cập nhật vào US; (b) CR chỉ là **1 trạng thái** thêm vào workflow; hay (c) không tạo khái niệm CR riêng — áp dụng cơ chế đã chốt ở buổi phỏng vấn trước (Câu 13: chưa Done thì sửa tại chỗ trên task cũ + tag/snapshot mới; đã Done thì tạo task mới link "relates to") và chỉ gắn **label `change-request`** cho các thay đổi phát sinh sau Spec Approved để lọc/báo cáo?
- Đã chốt: Minh chọn **(c)** — không tạo loại issue/trạng thái CR riêng; thay đổi sau Spec Approved xử lý theo cơ chế Câu 13 buổi trước (chưa Done: sửa tại chỗ + tag/snapshot mới + comment diff; đã Done: task mới link "relates to"), và gắn **label `change-request`** để truy vết/báo cáo.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Definition of Ready / Definition of Done cho US trong sprint -> Minh trả lời (Câu 8)

### Câu 8 · Definition of Ready (DoR) và Definition of Done (DoD)
- Hỏi: Có chốt bộ tiêu chuẩn vào/ra sprint cho 1 US không — (a) chốt cả DoR và DoD theo đề xuất của Peter; (b) chỉ chốt DoD, không cần DoR vì đã có cổng Spec Approved; hay (c) không đặt DoR/DoD chính thức? Đề xuất DoR (điều kiện US được kéo vào sprint): đã ở trạng thái Spec Approved; Acceptance Criteria rõ và kiểm thử được; đã link file US trong kho CITYBUS-Workflows + tài liệu Tầng 1/Tầng 2 liên quan; không còn câu hỏi mở chặn (blocking); team đã ước lượng. Đề xuất DoD (điều kiện được chuyển Done): DEV hoàn thành và đã qua Ready for Test; QC kiểm thử đạt ở In Testing; nếu có thay đổi nghiệp vụ trong quá trình làm thì file US/snapshot đã cập nhật; bug phát sinh từ US đã xử lý xong hoặc có quyết định Won't Fix/Cancelled kèm comment.
- Đã chốt: Minh trả lời "chưa cần làm" — **DoR/DoD chưa áp dụng ở thời điểm này**, để bỏ ngỏ và xem xét lại sau khi workflow chạy thực tế.
- Đề xuất, chưa chốt: (đề xuất (a) của Peter chưa được áp dụng; giữ lại trong file để tham khảo khi xem xét lại)
- Còn bỏ ngỏ: DoR/DoD -> xem xét lại sau giai đoạn chạy thử workflow. Các buổi ceremony của sprint (Planning/Daily/Review/Retro/Refinement) -> Minh trả lời (Câu 9)

### Câu 9 · Các buổi ceremony của sprint tổ chức thế nào?
- Hỏi: Trong 1 sprint 2 tuần, team có chuẩn hóa các buổi ceremony không — (a) đầy đủ theo Scrum: **Sprint Planning** (đầu sprint — chốt phạm vi + assignee theo chặng như Câu 5), **Daily** 15 phút, **Sprint Review** (cuối sprint — demo kết quả), **Retrospective**, cộng thêm **buổi Refinement giữa sprint** do BA chủ trì để chuẩn bị/chốt nghiệp vụ US cho sprint kế tiếp; (b) chỉ giữ **Planning + Review**, Daily linh hoạt qua chat nhóm; hay (c) chưa chuẩn hóa ceremony, họp theo phát sinh?
- Đã chốt: Minh chọn **(c)** — **chưa chuẩn hóa ceremony**, họp theo phát sinh. (Sprint Planning vẫn là mốc có thật vì Câu 5 đã chốt việc chốt assignee tại Sprint Planning — hiểu là buổi chốt phạm vi/assign đầu sprint diễn ra theo nhu cầu thực tế, không đặt lịch ceremony cố định.)
- Đề xuất, chưa chốt: (đề xuất (a) của Peter không được chọn; ghi nhận để xem xét lại nếu sau này team cần nhịp Scrum đầy đủ)
- Còn bỏ ngỏ: Cách ước lượng khối lượng US khi lên kế hoạch sprint -> Minh trả lời (Câu 10)

### Câu 10 · Ước lượng (estimation) cho US khi lên kế hoạch sprint
- Hỏi: Khi chốt phạm vi sprint, khối lượng của US được ước lượng bằng cách nào — (a) **Story Point** (dãy Fibonacci 1/2/3/5/8/13), cả team cùng ước lượng để theo dõi velocity qua các sprint; (b) **giờ/ngày công** do DEV trực tiếp đưa ra; hay (c) chưa ước lượng chính thức — chỉ chia nhỏ US sao cho vừa 1 sprint?
- Đã chốt: Minh chọn **(c)** — **chưa ước lượng chính thức**; khi lên kế hoạch sprint chỉ chia nhỏ US sao cho vừa 1 sprint.
- Đề xuất, chưa chốt: (đề xuất story point của Peter không được chọn; xem xét lại nếu sau này cần dự báo velocity)
- Còn bỏ ngỏ: Workflow riêng cho Bug (dùng chung chuỗi v2 hay rút gọn) -> Minh trả lời (Câu 11)

### Câu 11 · Bug đi theo workflow nào?
- Hỏi: Bug do QC tạo trên Jira (gắn với task của BA) sẽ chạy theo bộ trạng thái nào — (a) dùng **nguyên chuỗi v2** như Story, kể cả các trạng thái soạn/chốt nghiệp vụ; (b) dùng **chuỗi v2 rút gọn**: `Open → In Progress → Ready for Test → In Testing → Done`, kèm các rẽ nhánh `Reopened / Won't Fix / Verifying on Prod / Cancelled` (bỏ qua Drafting Specs → Spec Review → Spec Approved → Ready for Dev vì bug không cần soạn nghiệp vụ); hay (c) bug không có workflow riêng, chỉ tạo dạng sub-task phụ thuộc vào US gốc?
- Đã chốt: Minh chọn **(b)** — Bug dùng **chuỗi v2 rút gọn** `Open → In Progress → Ready for Test → In Testing → Done` + 4 rẽ nhánh (Reopened / Won't Fix / Verifying on Prod / Cancelled); bug từ Prod/vận hành cũng vào cùng luồng này.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Đồng bộ template US trong CITYBUS-Workflows với quy chuẩn mã truy vết mới -> Minh trả lời (Câu 12)

### Câu 12 · Đồng bộ template US (CITYBUS-Workflows) với quy chuẩn mã mới
- Hỏi: Template US hiện tại trong `99-templates/` đang đánh số đơn giản `BR-01`, `AC-01`. Có đồng bộ sang quy chuẩn mã truy vết vừa chốt không — (a) đồng bộ ngay: BR/CM trong template dùng mã chuẩn mới (vd `FTT-BR-001.01-VAL-01`, `FTT-CM-VAL-002`), riêng **AC giữ dạng `AC-01`** vì quy chuẩn không định nghĩa mã AC và AC chỉ sống nội bộ trong 1 US; (b) bổ sung luôn mã AC vào quy chuẩn theo cùng logic phân cấp (`[PRJ]-AC-[FR].[US]-[số]`) rồi đồng bộ tất cả; hay (c) chưa đồng bộ, chờ Câu 6 (ánh xạ issue type) chốt xong?
- Đã chốt: Minh chọn **(a)** — đồng bộ ngay: template US dùng mã BR/CM theo chuẩn mới; AC giữ dạng `AC-01`. Việc sửa file `99-templates/template-us.md` và `checklist-review-ai.md` trong CITYBUS-Workflows theo quyết định này được ghi vào danh sách việc cần làm sau phỏng vấn (chưa thực hiện trong buổi phỏng vấn).
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Quy ước tên sprint + người quản lý thứ tự ưu tiên backlog -> Minh trả lời (Câu 13)

### Câu 13 · Tên sprint và người quản lý backlog
- Hỏi: Hai quy ước vận hành còn lại của board Scrum — (1) tên sprint đặt thế nào và (2) ai sắp xếp thứ tự ưu tiên backlog: (a) tên sprint theo mẫu `<Mã dự án> Sprint <số thứ tự> (<ngày bắt đầu>–<ngày kết thúc>)`, ví dụ `FTT Sprint 3 (01/12–12/12)`, và **BA là người duy nhất sắp xếp thứ tự ưu tiên backlog** của dự án mình; (b) tên sprint chỉ để mặc định theo board Jira (Sprint 1, Sprint 2...), thứ tự backlog cả team cùng quyết định khi chốt phạm vi sprint; hay (c) chưa quy định cả hai?
- Đã chốt: Minh chọn **(a)** — tên sprint theo mẫu `<Mã dự án> Sprint <số> (<ngày bắt đầu>–<ngày kết thúc>)` (vd `FTT Sprint 3 (01/12–12/12)`); **BA là người duy nhất sắp xếp thứ tự ưu tiên backlog** của dự án.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Áp quy chuẩn mã vào prompt của AI/Rovo Agent cho BA và QC -> Minh trả lời (Câu 14)

### Câu 14 · Khóa quy chuẩn mã vào prompt AI (Rovo Agent)
- Hỏi: Tài liệu quy chuẩn gốc nhấn mạnh việc "hard-lock" bảng quy tắc đặt mã vào prompt của Rovo Agent (Agent BA sinh US/BR/CM, Agent QC sinh TC/Bug) để AI không tự bịa mã. Có áp dụng không — (a) có: Peter soạn sẵn **2 prompt mẫu** (BA Agent + QC Agent) chứa nguyên bảng quy chuẩn mã + nguyên tắc Self-Contained Story, lưu trong thư mục `JIRA-Workflows/` để team dùng khi cấu hình agent; (b) chưa cần — team chưa dùng Rovo Agent chính thức, để sau?
- Diễn biến bổ sung: Minh gửi thêm file kiến trúc **"PROMPT CHUẨN: JIRA BUG ARCHITECT & QA AUTOMATION LEAD"** (file gốc: `~/workspace/user/files/PROMPT_CHU_N__JIRA_BUG_ARCHITECT___QA_AUTOMATION_LEAD.md`; bản tham khảo đã **lược bỏ mật khẩu** lưu ở `phong-van/tham-khao-2026-11-27-prompt-bug-architect-qc.md`) và yêu cầu Peter tham khảo file này để đưa ra **gợi ý giải pháp prompt tối ưu nhất**.
  - Nội dung chính của file kiến trúc: vai trò Senior QA/QC Automation Lead & Jira Workflow Architect; quy trình 4 bước tạo Bug: (0) thu thập context từ ticket dữ liệu test (mặc định HRA-148) + Issue gốc (AC, assignee); (1) tự phân loại kỹ thuật `[Dev][BE]` / `[Dev][App]` + Priority (High nếu chặn nghiệp vụ, Medium nếu lỗi hiển thị nhỏ); (2) Summary theo mẫu `[Môi trường] [Phân loại] [Bug] [Module] Mô tả`; (3) Description 3 phần (Môi trường & thiết bị / Chi tiết lỗi & kịch bản tái hiện kèm Actual vs Expected lấy từ AC gốc / Bằng chứng & dữ liệu kỹ thuật); (4) gán Assignee = Assignee của Issue gốc + link kiểu **"blocks"** tới Issue gốc. Nguyên tắc: không tự bịa AC (thiếu AC thì yêu cầu QC bổ sung), nhất quán Markdown, tự suy luận Module từ mô tả ngắn.
  - **Hiệu chỉnh của Peter khi đưa vào giải pháp chung (chưa chốt):**
    1. **Bảo mật:** Mục 3 của file gốc chứa mật khẩu thật của tài khoản test -> **không đưa mật khẩu vào prompt/repo** (đúng quy tắc bảo mật đã chốt ngày 2026-11-27); prompt chỉ *trỏ tới nguồn dữ liệu* (ticket dữ liệu test trên Jira), kho chỉ ghi nơi lấy mật khẩu.
    2. **Key dự án:** file gốc dùng key `HRA-148` và tên dự án FTWORK -> đổi theo thực tế đã chốt ở Câu 1: 1 project key `CITY`, dự án con là Component; ticket dữ liệu test cũng nằm trong CITY.
    3. **Assignee bug:** file gốc gán cho Assignee hiện tại của Issue gốc — đối chiếu Câu 5 (assign theo chặng), assignee hiện tại có thể đang là QC -> đề xuất gán cho **DEV phụ trách US gốc theo chốt ở Sprint Planning**.
    4. **Priority:** bổ sung mức **Critical** cho bug chạm tiền/vé/eLVC/trợ giá/đối soát (nhất quán phân tầng rủi ro ở buổi phỏng vấn trước), ngoài High/Medium như file gốc.
    5. **Trạng thái khởi tạo:** Bug do agent tạo vào workflow rút gọn (Câu 11) ở trạng thái `Open`, link "blocks" tới US gốc (giữ nguyên ý file gốc — bug chặn US đạt Done).
- Hỏi lại (bản tối ưu sau khi gộp file kiến trúc): Chốt giải pháp prompt gồm **bộ 3 prompt chuẩn** lưu trong `JIRA-Workflows/` — (1) **BA Agent** (sinh US/BR/CM, khóa quy chuẩn mã + Self-Contained Story), (2) **QC Agent — Test Case** (sinh TC theo quy chuẩn mã), (3) **QC Agent — Bug Architect** (theo kiến trúc 4 bước Minh gửi, đã hiệu chỉnh 5 điểm ở trên) — hay giữ phương án cũ chỉ 2 prompt / chưa làm?
- Đã chốt: Minh trả lời "3 prompt" — **chốt giải pháp bộ 3 prompt chuẩn** (BA Agent / QC Agent Test Case / QC Agent Bug Architect kèm 5 điểm hiệu chỉnh của Peter) lưu trong `JIRA-Workflows/`. Việc soạn nội dung 3 prompt là việc làm sau phỏng vấn, chưa thực hiện trong buổi này.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Câu hỏi kết thúc buổi phỏng vấn -> Minh trả lời (Câu 15)

### Câu 15 · Câu hỏi kết thúc: còn điều gì Peter chưa hỏi?
- Hỏi: Nhìn lại toàn bộ buổi — quy chuẩn mã truy vết, Component/board, chuỗi trạng thái v2, assign theo chặng + quyền override của BA, Change Request bằng label, workflow Bug rút gọn, tên sprint/backlog, bộ 3 prompt AI — còn khía cạnh nào của Jira workflow mà Peter chưa hỏi tới nhưng quan trọng với thực tế team của bạn không? (Câu 6 về ánh xạ issue type vẫn đang tạm hoãn theo ý bạn — sẽ quay lại khi bạn sẵn sàng.) Và sau buổi này, bạn có muốn Peter tổng hợp các quyết định đã chốt thành bộ tài liệu trong `JIRA-Workflows/` (quy chuẩn workflow + quy chuẩn đặt mã + 3 prompt mẫu + cập nhật README) như đã làm với buổi phỏng vấn trước không?
- Đã chốt: Minh trả lời "ok hãy lưu hết vào JIRA-Workflows" — **đồng ý tổng hợp toàn bộ quyết định đã chốt thành bộ tài liệu trong `JIRA-Workflows/`**, không bổ sung khía cạnh mới. **Buổi phỏng vấn grill-me về JIRA-Workflows kết thúc tại đây (15 câu)** với 2 điểm vẫn tạm hoãn theo ý Minh: Câu 6 (ánh xạ issue type) và Câu 8 (DoR/DoD — chưa cần làm).
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Câu 6 — ánh xạ issue type (Minh tạm hoãn); Câu 8 — DoR/DoD (xem xét lại sau khi workflow chạy thực tế)

## Kết quả triển khai sau phỏng vấn (ngày 2026-11-27, chỉ ở local — chưa commit/push)
- `JIRA-Workflows/01-quy-chuan-dat-ten-ma-truy-vet.md` — quy chuẩn mã đầy đủ.
- `JIRA-Workflows/02-jira-workflow.md` — cấu trúc project/board, chuỗi trạng thái v2 + workflow Bug rút gọn, assign theo chặng, Change Request, sprint/backlog, các điểm tạm hoãn.
- `JIRA-Workflows/prompts/` — bộ 3 prompt chuẩn: `prompt-ba-agent.md`, `prompt-qc-agent-testcase.md`, `prompt-qc-agent-bug-architect.md`.
- `JIRA-Workflows/README.md` — cập nhật thành mục lục chính thức.
- Đồng bộ theo Câu 12: `CITYBUS-Workflows/99-templates/template-us.md` và `checklist-review-ai.md` dùng mã BR/CM theo quy chuẩn mới.

## Phụ lục A · Bảng viết tắt đầy đủ (theo yêu cầu của Minh, dùng khi cần làm rõ)

**Loại tài liệu / thực thể:**
| Viết tắt | Tên đầy đủ | Ý nghĩa |
|---|---|---|
| `FR` | Functional Requirement | Tính năng chính (cấp Epic) |
| `NFR` | Non-Functional Requirement | Yêu cầu phi chức năng (hiệu năng, bảo mật, offline, chịu tải, Kiosk mode) |
| `SCR` | Screen | Màn hình / giao diện, gắn với FR chứa nó |
| `US` | User Story | Câu chuyện người dùng, đặc tả chi tiết dưới FR |
| `BR` | Business Rule | Ràng buộc đặc thù, chỉ tồn tại trong 1 US |
| `CM` | Common Rule | Ràng buộc dùng chung toàn dự án |
| `TC` | Test Case | Kịch bản kiểm thử của QC (quản lý ngoài Jira) |
| `BUG` | Bug report | Báo cáo lỗi (tạo trên Jira, gắn với task của BA) |

**7 nhóm ràng buộc kỹ thuật (điền vào vị trí [NHÓM] trong mã BR/CM):**
| Viết tắt | Tên đầy đủ | Ý nghĩa |
|---|---|---|
| `VAL` | Validation | Kiểm tra hợp lệ dữ liệu đầu vào |
| `SEC` | Security & Auth | Bảo mật, xác thực, phân quyền |
| `WFL` | Workflow & State | Luồng xử lý, chuyển đổi trạng thái |
| `CAL` | Calculation & Logic | Tính toán, ngưỡng cảnh báo |
| `INT` | Integration & Sync | Tích hợp API, đồng bộ hệ thống |
| `EXC` | Exception & Error | Xử lý ngoại lệ, thông báo lỗi |
| `FMT` | Format & Display | Định dạng hiển thị |

**Mã dự án con (ví dụ đã biết):** `FTT` = App điều hành tài xế trên Tablet (Futa Tech Tablet); `SMB` = Smartbus; `HRA` = HR/Admin. Project key Jira chung: `CITY`.

## Việc còn bỏ ngỏ
- Ánh xạ loại mã (FR/NFR/SCR/US/BR/CM/Bug) sang issue type Jira -> Minh tạm hoãn, chưa chốt (Câu 6)
- Definition of Ready / Definition of Done -> Minh: chưa cần làm, xem xét lại sau khi workflow chạy thực tế (Câu 8)
- Câu hỏi kết thúc buổi phỏng vấn (còn khía cạnh nào chưa hỏi + có tổng hợp tài liệu JIRA-Workflows không) -> Minh trả lời (Câu 15)
- Việc cần làm sau phỏng vấn (khi Minh đồng ý): soạn bộ 3 prompt chuẩn vào `JIRA-Workflows/`
- Việc cần làm sau phỏng vấn: sửa `99-templates/template-us.md` và `checklist-review-ai.md` theo Câu 12 (BR/CM theo quy chuẩn mã mới)
- Đồng bộ template US của CITYBUS-Workflows (BR-/AC-) với quy chuẩn mã mới -> sẽ hỏi
- Luồng cấu hình Jira workflow + assign task chuẩn (vấn đề Minh nêu) -> sẽ hỏi
