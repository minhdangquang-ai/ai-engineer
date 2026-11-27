# Workflow làm việc & quản lý nghiệp vụ Citybus cho QC/DEV/Quản lý: ghi chép phỏng vấn
Ngày: 2026-11-26 · Mục tiêu: Chốt workflow để QC, DEV và Quản lý nắm đúng nghiệp vụ (chung Citybus, riêng từng dự án, và cụ thể theo từng User Story) trước khi làm chuyên môn; đồng thời chốt cách quản lý tài liệu nghiệp vụ Markdown trên GitHub (chia sẻ, branch, version).
Trạng thái: đang làm

## Bối cảnh đã biết (không hỏi lại)
- Người được phỏng vấn: Minh — vai trò BA trong các dự án Citybus (FUTA), làm việc với QC, DEV và Quản lý.
- Nghiệp vụ chung Citybus đã có file tổng hợp: FUTA_Citybus_Nghiep_vu_Tong_hop.md — TTCC là đơn vị nhà nước quản lý buýt toàn thành phố; GoLab là vendor cung cấp GoPS (app bán vé chính trên POS T10) và GoAFC (hệ thống Admin quản lý buýt); Smartbus là hệ thống nội bộ FUTA; các mốc eLVC 12:00 là 12:00 trưa giờ Việt Nam.
- Các dự án riêng Minh nêu ví dụ: "Smartbus App vs GoPS App", "Smartbus App vs VNPay App", "App điều hành tài xế trên Tablet".
- File phỏng vấn này lưu trong repo ai-engineer (~/workspace/FUTA-TECH/ai-engineer/phong-van/) theo yêu cầu của Minh. Buổi phỏng vấn trước đã được clear theo yêu cầu của Minh ngày 2026-11-26 và bắt đầu lại từ đầu — không kế thừa câu trả lời cũ.
- Không có file CLAUDE.md trong workspace.

## Tóm tắt các quyết định
- Câu 1: **Không** lấy GitHub Markdown làm nguồn nghiệp vụ duy nhất. Cách làm chính là truyền thống: **BA ghi nghiệp vụ trực tiếp vào phần Mô tả (Description) của từng Task trên Jira**. Minh sẽ **bổ sung thêm 1 file Markdown tóm tắt nghiệp vụ của task đó** đi kèm.
- Câu 2: File Markdown tóm tắt **đính kèm (attachment) trực tiếp vào chính Task Jira** — chọn phương án (a), không lưu ở GitHub. File Markdown ban đầu là **cơ sở lưu vết nghiệp vụ** trên hệ thống của công ty (Jira), tránh rủi ro repo cá nhân bị xóa khi BA nghỉ việc. **Mọi thay đổi nghiệp vụ sau đó sẽ comment trực tiếp trong Jira** (lưu vết theo comment), không dựa vào việc sửa repo.
- Cấu trúc lưu nghiệp vụ gồm **3 phần/tầng**: (1) nghiệp vụ **chung** cho Citybus, (2) nghiệp vụ **riêng** cho từng dự án, (3) nghiệp vụ qua **User Story trên Task Jira**.
- Câu 3: Tầng 1 và Tầng 2 **neo ngay trong Jira** theo phương án (a) — mỗi tầng là 1 Epic/Task "tài liệu" riêng, Mô tả chứa nội dung chính + đính kèm file Markdown, các US link về đó.
- Phân loại dự án (Minh bổ sung): dự án có **2 loại** — (1) **dự án mới**: dễ control; (2) **dự án đang làm**: làm tính năng mới hoặc sửa tính năng cũ. Nhận xét của Peter (đã ghi, chưa phải quyết định): loại 2 khó hơn vì nghiệp vụ hiện trạng có thể chưa có tài liệu hoặc đã lệch thực tế, có rủi ro regression khi sửa tính năng cũ — cần chốt cách xử lý ở Câu 4.
- Câu 4: **Bắt buộc tài liệu hiện trạng + thay đổi khi sửa tính năng cũ** (Minh đồng ý với đề xuất): file Markdown gồm "Hiện trạng đang chạy" + "Thay đổi yêu cầu", QC dùng hiện trạng để test regression; tính năng mới trong dự án đang làm chỉ cần link Tầng 1/Tầng 2 + ghi phần mới.
- Câu 5 (điều chỉnh từ Minh): **BA là người chịu trách nhiệm chính về nghiệp vụ đúng** — BA là người chốt và ra file Markdown gửi cho team. Đề xuất "3 vai trò cùng xác nhận mới được Ready" của Peter **không được chốt theo hướng đó**; trách nhiệm đúng/sai nghiệp vụ dồn về BA.
- Băn khoăn mới của Minh (gốc rễ cần giải quyết): BA nhiều khi **dùng AI hỗ trợ tạo US nhưng không review lại US đó, mà xuất hẳn thành file Markdown** gửi team — rủi ro file chính thức chứa nội dung AI bịa/chưa kiểm chứng mà không ai phát hiện.
- Câu 6: **Kiểm soát US do AI hỗ trợ theo phân tầng rủi ro** (Minh đồng ý): US thường — BA tự review theo checklist + comment ký xác nhận trên Jira; US đụng tiền/trợ giá/thanh toán/đối soát — bắt buộc peer review bởi người thứ hai. Bản AI tạo chỉ là Draft; đầu file bắt buộc có mục Nguồn đối chiếu/Người review/Ngày review; thiếu thì QC/DEV có quyền trả task về.
- Câu 7 (thay đổi hướng, thay thế một phần Câu 1/Câu 2): BA quá nhiều việc, **không thể nhớ và quay lại cập nhật từng Task Jira cũ**. BA sẽ có **cơ chế quản lý nghiệp vụ riêng, luôn giữ bản đầy đủ nhất**, và quy trình phải có **1 chỗ tập trung** để QC/DEV clone về toàn bộ nghiệp vụ chung (Tầng 1) + nghiệp vụ từng dự án (Tầng 2). Cách đánh version vX.Y trên attachment Jira chưa chốt — chờ mô hình kho tập trung ở Câu 8.
- Câu 8: **Mô hình 2 lớp đã chốt** (Minh "ok"): Lớp kho chính thuộc **sở hữu công ty** (BA là maintainer, bàn giao khi nghỉ việc) là nơi QC/DEV clone bản đầy đủ/mới nhất; Lớp lưu vết trên Jira giữ Mô tả + snapshot Markdown lúc chốt + comment thay đổi, BA không phải quay lại cập nhật từng task cũ.
- Câu 9: **Branch + tag đã chốt**: tách branch theo phương án (a) — `main` là bản chốt duy nhất cho QC/DEV clone, BA làm trên `draft/<mã task>` và merge sau review. **Tag đánh theo ngày + mã Task Jira** (tạm chốt, Minh sẽ review lại sau).
- Câu 10: **Cấu trúc thư mục kho chính đã chốt** (Minh "ok"): `README.md` cổng vào, `01-nghiep-vu-chung-citybus/`, `02-du-an/<slug>/` (có `us/` và README mục lục), `99-templates/`.
- Câu 11: **Phân quyền kho chính đã chốt**: chỉ BA (maintainer) + 1 người dự phòng được merge vào `main`; QC/DEV chỉ đọc/clone, góp ý qua comment. (Bổ sung bởi Câu 19: thực tế hiện chỉ có 1 BA, chưa có người dự phòng.)
- Câu 12: **Chuỗi trạng thái workflow Jira tạm chốt** (Minh sẽ review lại sau): Open -> Đang soạn nghiệp vụ -> Review nghiệp vụ -> Đã chốt nghiệp vụ -> Ready for Dev -> In Progress -> In Testing -> Done. Chưa đối chiếu với board hiện tại của team.
- Câu 13: **Thay đổi sau chốt xử lý theo mức độ (c)**: chưa Done thì sửa tại chỗ trên task cũ (branch mới, tag mới, snapshot mới, comment diff, QC test lại phần ảnh hưởng + regression); đã Done thì tạo task mới link "relates to", không mở lại task cũ.
- Câu 15: **Bản tham khảo QC chỉ để tham khảo — cấu trúc cuối tối ưu cho vai trò BA** (Minh chỉ đạo): không gộp phạm vi QC/nhiều người commit vào kho này, Câu 11 giữ nguyên (chỉ BA merge `main`); Tầng 3 thiết kế riêng cho workflow BA; **quy tắc bảo mật đã chốt**: không ghi mật khẩu thật vào git, chỉ ghi URL + tên tài khoản + nơi lấy mật khẩu.
- Câu 16: **Cấu trúc kho tối ưu cho BA đã chốt** (Minh "ok", thay thế Câu 10): thêm `00-inbox/` (sổ tiếp nhận của BA), `01-core-wiki/` chia theo miền, `02-projects/<YYYY-qN-ten>/` có `us/`, `03-resources/` cho BA đối chiếu, `99-templates/`. Bảng đối chiếu khác/giống với bản QC đã log tại `phong-van/doi-chieu-cau-truc-BA-vs-QC-tham-khao.md` theo yêu cầu của Minh.
- Câu 14: **Template US + checklist review AI đã chốt** (Minh chốt ngày 2026-11-27): khung phần đầu (mã task/dự án/link Tầng 1-2/nguồn đối chiếu/người review/ngày review/trạng thái/tag) + phần thân (Mục tiêu, Phạm vi, Actor, Luồng chính/ngoại lệ, BR-, AC- Given/When/Then, Dữ liệu/API, Hiện trạng+Thay đổi khi sửa cũ, Câu hỏi còn mở); mục không áp dụng ghi "Không áp dụng". Minh sẽ cập nhật thay đổi sau khi triển khai thực tế.
- Câu 17: **Pilot ở 1 dự án mới** (Minh chọn (a) ngày 2026-11-27): áp dụng thử toàn bộ workflow/kho/template đầu tiên tại 1 dự án mới sắp bắt đầu, phạm vi hẹp, tổng kết sau pilot trước khi nhân rộng; tên dự án cụ thể xác định khi khởi động.
- Câu 18: **Thông báo bản mới bằng (b)**: comment trong Task Jira (kèm tag + tóm tắt thay đổi) + nhắn vào group chat chung của dự án để team pull bản mới ngay.
- Câu 19: **Chưa có người dự phòng merge — chấp nhận rủi ro tạm thời** (Minh nêu ngày 2026-11-27): team thường chỉ có 1 BA, công ty chưa có người backup; khi BA vắng thì đóng băng merge vào `main`, cả team làm task dự án khác hoặc chờ BA quay lại merge. Phần "1 người dự phòng" của Câu 11 ghi nhận là chưa khả thi hiện tại.

## Các câu hỏi
### Câu 1 · Nguồn nghiệp vụ chính thức duy nhất (Single Source of Truth)
- Hỏi: Có chốt repo Markdown trên GitHub là nguồn nghiệp vụ chính thức duy nhất không — Jira (User Story) chỉ chứa mô tả ngắn + link tới đúng file/đúng version trong repo, QC/DEV/Quản lý không nhận nghiệp vụ qua chat hay file rời nữa?
- Đã chốt: Không đồng ý với đề xuất SSOT GitHub. Minh nói nguyên văn: "tôi muốn BA sẽ ghi nghiệp vụ theo cách truyền thống vào Mô tả trong từng Task Jira, tôi sẽ bổ sung thêm 1 file markdown tóm tắt nghiệp vụ của task đó". Tức là: Mô tả Task Jira = nơi ghi nghiệp vụ chính; file Markdown = tài liệu tóm tắt bổ sung theo từng task.
- Đề xuất, chưa chốt: (đề xuất SSOT GitHub của Peter đã bị bác, không còn hiệu lực)
- Còn bỏ ngỏ: File Markdown tóm tắt được lưu ở đâu và khi nội dung giữa Mô tả Jira và file Markdown lệch nhau thì lấy bên nào làm chuẩn? -> Minh trả lời (Câu 2)

### Câu 2 · Nơi lưu file Markdown tóm tắt và thứ tự ưu tiên khi lệch nhau
- Hỏi: File Markdown tóm tắt nghiệp vụ của mỗi task sẽ lưu ở đâu — (a) đính kèm (attachment) trực tiếp vào chính Task Jira đó; (b) lưu trong repo GitHub và dán link vào Task Jira; hay (c) cả hai? Và nếu Mô tả Jira với file Markdown khác nhau, bên nào là chuẩn để QC/DEV làm theo?
- Đã chốt: Minh chọn **(a)**. Nguyên văn: "theo tôi, file markdown ban đầu làm cơ sở để lưu vết nghiệp vụ (tránh tình trạng BA nghỉ việc thì sẽ xóa toàn bộ Repo?) — Thay đổi gì sẽ comment trong Jira luôn — thường thì cấu trúc lưu nghiệp vụ nên cơ cấu thành 3 phần: nghiệp vụ chung cho Citybus, nghiệp vụ riêng cho từng dự án, và nghiệp vụ qua US trên task Jira". Hiểu đã chốt: file Markdown ban đầu đính kèm Task Jira làm bản lưu vết gốc; thay đổi về sau ghi bằng comment trong Jira; cấu trúc nghiệp vụ 3 tầng như ở phần Tóm tắt.
- Đề xuất, chưa chốt: (đề xuất lưu GitHub của Peter đã bị bác, không còn hiệu lực)
- Còn bỏ ngỏ: Tầng 1 (chung Citybus) và Tầng 2 (riêng từng dự án) được lưu ở đâu và dưới dạng nào, vì Tầng 3 đã chốt là Task Jira + attachment? -> Minh trả lời (Câu 3)

### Câu 3 · Nơi lưu Tầng 1 (chung Citybus) và Tầng 2 (riêng từng dự án)
- Hỏi: Tầng 1 và Tầng 2 sẽ "neo" ở đâu trong Jira — (a) mỗi tầng là 1 Epic/Task "tài liệu" riêng trong Jira, Mô tả chứa nội dung chính + đính kèm file Markdown, các Task US link về đó; (b) để ở Confluence/Drive của công ty và chỉ dán link vào Jira; hay (c) cách khác?
- Đã chốt: Minh chọn **(a)** và bổ sung nguyên văn: "dự án thường sẽ có 2 loại — 1: dự án mới (này thì dễ control) — 2: dự án đang làm -> Làm tính năng mới hoặc sửa tính năng cũ".
- Đề xuất, chưa chốt: (đề xuất (a) của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Với dự án đang làm (loại 2), trước khi làm tính năng mới/sửa tính năng cũ có bắt buộc dựng lại tài liệu nghiệp vụ hiện trạng không? -> Minh trả lời (Câu 4)

### Câu 4 · Dự án đang làm: có bắt buộc tài liệu "hiện trạng" trước khi thay đổi không?
- Hỏi: Với dự án đang làm, khi sửa tính năng cũ (hoặc làm tính năng mới dựa trên tính năng cũ), có bắt buộc BA phải có 1 phần "nghiệp vụ hiện trạng" (tính năng đang chạy như thế nào) được xác nhận trước, rồi mới ghi phần thay đổi (delta) không? Hay chỉ cần ghi phần thay đổi?
- Đã chốt: Minh trả lời "đồng ý" — chấp nhận toàn bộ đề xuất: sửa tính năng cũ bắt buộc file Markdown có 2 phần "Hiện trạng đang chạy" + "Thay đổi yêu cầu", QC dùng phần hiện trạng để test regression; tính năng mới trong dự án đang làm chỉ cần link Tầng 1/Tầng 2 + ghi phần mới.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Ai xác nhận phần "hiện trạng" là đúng trước khi DEV sửa, và xác nhận bằng cách nào? -> gộp vào Câu 5 (cổng xác nhận trong workflow)

### Câu 5 · Cổng xác nhận "đã hiểu đúng nghiệp vụ" trong workflow Jira
- Hỏi: Trước khi DEV/QC bắt đầu làm chuyên môn, task phải qua cổng xác nhận nào — có bắt buộc buổi walkthrough do BA trình bày, và QC lead, DEV lead, Quản lý phải comment xác nhận "đã review, đã hiểu, câu hỏi đã được giải đáp" trên chính task Jira thì task mới được chuyển sang trạng thái Ready/In Progress không?
- Đã chốt: Minh điều chỉnh lại hướng: nguyên văn "tôi nghĩ BA là người chịu trách nhiệm chính cho nghiệp vụ đúng thì chốt ra file markdown gửi cho team". Tức là trách nhiệm chốt nghiệp vụ thuộc về BA, BA ra file Markdown chính thức gửi team — không chốt cơ chế 3 vai trò cùng ký xác nhận như đề xuất. Đồng thời Minh nêu băn khoăn thật: "BA nhiều khi cũng dùng AI hỗ trợ tạo US và cũng không review US đó mà xuất hẳn thành file markdown" — vấn đề nằm ở khâu BA tự kiểm chứng nội dung trước khi chốt.
- Đề xuất, chưa chốt: (đề xuất cổng 3 xác nhận của Peter bị thay thế bởi hướng BA chịu trách nhiệm chính; cơ chế kiểm soát chất lượng đầu ra của BA chuyển sang Câu 6)
- Còn bỏ ngỏ: Cơ chế nào ngăn BA xuất thẳng US do AI tạo mà chưa review? -> Minh trả lời (Câu 6)

### Câu 6 · Cổng kiểm soát US do AI hỗ trợ tạo
- Hỏi: Mức kiểm soát nào áp cho US/file Markdown có dùng AI hỗ trợ — (a) BA tự review theo checklist và comment ký xác nhận trên Jira "đã review, chịu trách nhiệm nội dung"; (b) mọi US đều phải có người thứ hai (Quản lý hoặc BA khác) peer review mới được chốt; hay (c) phân tầng theo rủi ro: US thường thì (a), US đụng tới tiền/trợ giá/thanh toán/đối soát (vé, eLVC, VNPay...) thì bắt buộc (b)?
- Đã chốt: Minh trả lời "đồng ý" — chấp nhận phương án (c) phân tầng rủi ro và quy định cứng kèm theo: US thường do BA tự review theo checklist + ký xác nhận trên Jira; US đụng tiền/trợ giá/thanh toán/đối soát (vé, eLVC, VNPay...) bắt buộc peer review bởi người thứ hai; bản AI tạo chỉ là Draft; đầu file Markdown bắt buộc có "Nguồn đối chiếu / Người review / Ngày review"; thiếu thì QC/DEV có quyền trả task về.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Cách đánh version cho file Markdown đính kèm Jira khi có thay đổi -> Minh trả lời (Câu 7)

### Câu 7 · Đánh version cho file Markdown đính kèm Jira
- Hỏi: Khi nghiệp vụ của 1 task thay đổi và phải ra file Markdown mới, cách đánh version nào sẽ dùng — (a) version trong tên file dạng vX.Y kèm bảng lịch sử trong file; (b) version theo ngày (YYYYMMDD); hay (c) không đánh version, chỉ dựa vào lịch sử attachment/comment của Jira?
- Đã chốt: Minh không chọn (a)/(b)/(c), mà nêu ràng buộc thực tế thay đổi hướng giải quyết. Nguyên văn: "số lượng công việc của BA rất nhiều, khó là BA không nhớ task cũ nào để vào đúng mà cập nhật vào Jira — BA sẽ có cơ chế quản lý nghiệp vụ riêng để đảm bảo luôn là bản đầy đủ nhất — Quy trình là nên có 1 chỗ để QC, Dev luôn biết lên để clone về toàn bộ quy trình chung và quy trình cho từng dự án". Hiểu đã chốt: (i) việc cập nhật ngược vào từng Task Jira cũ là không khả thi ở quy mô công việc của BA; (ii) BA duy trì một cơ chế quản lý nghiệp vụ riêng, luôn giữ bản đầy đủ nhất; (iii) quy trình phải có **1 chỗ tập trung duy nhất** để QC/DEV vào clone về toàn bộ nghiệp vụ chung + nghiệp vụ từng dự án.
- Đề xuất, chưa chốt: (đề xuất version vX.Y trên attachment Jira bị gác lại — version sẽ do cơ chế quản lý của BA/kho tập trung đảm nhiệm, chi tiết chờ Câu 8)
- Còn bỏ ngỏ: Kho tập trung đó là gì, thuộc sở hữu ai, và quan hệ của nó với bản đính kèm Jira ở Câu 2 ra sao (vì Câu 2 từng lo repo bị xóa khi BA nghỉ việc)? -> Minh trả lời (Câu 8). Ghi chú theo quy tắc phỏng vấn: câu trả lời này **bổ sung/thay đổi một phần Câu 1 và Câu 2** — kho tập trung quay lại trong mô hình; phần cũ vẫn giữ nguyên ở trên để đối chiếu.

### Câu 8 · Kho tập trung để clone: sở hữu và quan hệ với Jira
- Hỏi: Kho tập trung cho QC/DEV clone có phải là mô hình 2 lớp không — Lớp 1 "kho chính" do BA quản lý (bản đầy đủ nhất, có version/branch) và Lớp 2 "lưu vết" là bản snapshot đính kèm Task Jira khi chốt US? Và kho chính phải thuộc sở hữu công ty (GitHub Organization/GitLab của công ty, BA là maintainer) chứ không phải repo cá nhân, để xử lý đúng lo ngại "BA nghỉ việc thì repo bị xóa" ở Câu 2?
- Đã chốt: (chờ trả lời)
- Đã chốt: Minh trả lời "ok" — chấp nhận mô hình 2 lớp và kho chính thuộc sở hữu công ty như đề xuất.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Cách tách branch và đánh version/tag trong kho chính -> Minh trả lời (Câu 9)

### Câu 9 · Tách branch và version trong kho chính
- Hỏi: Kho chính có tách branch không — (a) có: `main` là bản đã chốt duy nhất mà QC/DEV clone, BA soạn/thay đổi trên branch riêng theo task (vd `draft/CITY-1234`) rồi mới merge vào `main` khi đã chốt và qua cổng review ở Câu 6; (b) không tách: mọi người sửa thẳng trên `main`; hay (c) tách branch dài hạn theo từng dự án?
- Đã chốt: (chờ trả lời)
- Đã chốt: Minh chọn **(a)** — `main` là bản đã chốt duy nhất để QC/DEV clone, BA soạn trên branch riêng theo task (`draft/<mã task>`) rồi merge vào `main` sau khi qua cổng review Câu 6. Về tag: Minh chốt **đánh tag theo ngày và mã Task Jira** (không dùng tag `v2026.11` như Peter đề xuất) — định dạng tạm hiểu là `<YYYY-MM-DD>_<Mã task>` tại thời điểm merge/chốt, vd `2026-11-26_CITY-1234`. Minh ghi chú rõ phần tag này là **tạm chốt, sẽ review lại sau** — ghi vào Việc còn bỏ ngỏ để không coi là quy ước cuối cùng.
- Đề xuất, chưa chốt: (phần branch (a) của Peter đã được chấp nhận; phần tag theo mốc của Peter đã bị thay bằng tag ngày + mã task)
- Còn bỏ ngỏ: Cấu trúc thư mục bên trong kho chính -> Minh trả lời (Câu 10). Quy ước tag (ngày + mã task) cần Minh review lại sau.

### Câu 10 · Cấu trúc thư mục bên trong kho chính
- Hỏi: Cấu trúc thư mục của kho chính có theo mẫu 3 tầng đã chốt không — thư mục gốc gồm: `README.md` (cổng vào: hướng dẫn clone, bản đồ tài liệu, quy trình), `01-nghiep-vu-chung-citybus/`, `02-du-an/<ten-du-an>/` (mỗi dự án có file nghiệp vụ riêng + thư mục `us/` chứa các file Markdown theo task), và `99-templates/` (template US, template hiện trạng+thay đổi, checklist review AI)?
- Đã chốt: Minh trả lời "ok" — chấp nhận cấu trúc thư mục như đề xuất, gồm README cổng vào, `01-nghiep-vu-chung-citybus/`, `02-du-an/<slug-du-an>/` (kèm `us/` và README mục lục từng dự án), `99-templates/`.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Phân quyền trên kho chính: ai được merge vào `main`? -> Minh trả lời (Câu 11)

### Câu 11 · Phân quyền trên kho chính: ai được merge vào `main`?
- Hỏi: Quyền ghi trên kho chính phân thế nào — (a) chỉ BA (maintainer) mới được merge vào `main`, QC/DEV chỉ có quyền đọc/clone và góp ý qua comment Jira hoặc comment trên pull/merge request; (b) DEV/QC lead cũng được merge; hay (c) ai trong team cũng sửa được?
- Đã chốt: Minh chọn **(a)** — chỉ BA (maintainer) merge vào `main`, kèm 1 người dự phòng giữ quyền maintainer; QC/DEV chỉ đọc/clone và góp ý qua comment, không tự sửa nội dung nghiệp vụ trong kho.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Chuỗi trạng thái workflow Jira đầy đủ từ tạo task đến Done -> Minh trả lời (Câu 12)

### Câu 12 · Chuỗi trạng thái workflow Jira cho 1 task
- Hỏi: Workflow Jira cho 1 task có theo chuỗi trạng thái Peter đề xuất không, hay team đã có bộ trạng thái chuẩn sẵn phải bám theo? Chuỗi đề xuất: `Open (BA tạo task + Mô tả)` -> `Đang soạn nghiệp vụ (BA làm trên branch draft)` -> `Review nghiệp vụ (self-review/peer review theo Câu 6)` -> `Đã chốt nghiệp vụ (snapshot đính kèm Jira + merge main + tag ngày_mã task + comment link)` -> `Ready for Dev` -> `In Progress (DEV)` -> `In Testing (QC)` -> `Done`.
- Đã chốt: Minh trả lời "ok cứ vậy trước đi, mình sẽ review lại nữa" — **tạm chốt** chuỗi trạng thái như đề xuất (Open -> Đang soạn nghiệp vụ -> Review nghiệp vụ -> Đã chốt nghiệp vụ -> Ready for Dev -> In Progress -> In Testing -> Done), chưa đối chiếu với workflow/board hiện tại của team; Minh sẽ review lại sau, ghi vào Việc còn bỏ ngỏ.
- Đề xuất, chưa chốt: (khung trạng thái của Peter được tạm chấp nhận; lưu ý "chỉ thêm tối đa 2 trạng thái mới" và việc đối chiếu board hiện tại vẫn còn bỏ ngỏ)
- Còn bỏ ngỏ: Xử lý thay đổi nghiệp vụ sau khi đã chốt (đang Dev/QC hoặc đã Done) -> Minh trả lời (Câu 13). Đối chiếu chuỗi trạng thái với board Jira hiện tại của team -> Minh cung cấp/review sau.

### Câu 13 · Thay đổi nghiệp vụ sau khi đã chốt
- Hỏi: Khi nghiệp vụ thay đổi sau trạng thái "Đã chốt nghiệp vụ" (task đang Dev, đang QC, hoặc đã Done), luồng xử lý nào sẽ dùng — (a) quay task về `Review nghiệp vụ`, BA sửa trên branch draft mới, merge + tag mới, đính kèm snapshot mới và comment diff, DEV/QC làm lại phần ảnh hưởng; (b) tạo task mới hoàn toàn cho phần thay đổi; hay (c) tùy mức độ: thay đổi nhỏ thì (a) ngay trên task cũ, thay đổi lớn/đã Done thì (b)?
- Đã chốt: Minh chọn **(c)** — task chưa Done: xử lý tại chỗ trên task cũ theo (a), comment rõ đổi gì so với tag nào, QC test lại phần ảnh hưởng + regression; task đã Done: tạo task mới link "relates to" task cũ, không mở lại task cũ. Mọi thay đổi đều sinh tag mới, không sửa đè tag/snapshot cũ.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Nội dung bắt buộc của template file US Markdown và checklist review AI trong `99-templates/` -> Minh trả lời (Câu 14)

### Câu 14 · Template file US Markdown và checklist review AI
- Hỏi: Template file US trong `99-templates/` có chốt theo khung Peter đề xuất không — Phần đầu: mã task, dự án, link Tầng 1/Tầng 2 liên quan, nguồn đối chiếu, người review, ngày review, trạng thái Draft/Đã chốt, tag; Phần thân: Mục tiêu, Phạm vi (làm/không làm), Actor, Luồng chính, Luồng ngoại lệ, Business Rules đánh số BR-, Acceptance Criteria dạng Given/When/Then đánh số AC-, Dữ liệu/API liên quan, mục Hiện trạng + Thay đổi (chỉ khi sửa tính năng cũ), Câu hỏi còn mở? Và checklist review AI là 1 file riêng gồm các mục: đối chiếu mọi con số/mốc giờ/tên hệ thống với nguồn, không có rule nào không có nguồn, thuật ngữ đúng chuẩn (TTCC/GoLab/GoAFC/GoPS...), AC nào cũng test được, đã xét trường hợp ngoại lệ?
- Đã chốt: Minh trả lời "chốt" ngày 2026-11-27 — chấp nhận khung template US + checklist review AI như đề xuất, gồm nguyên tắc mục không áp dụng thì ghi "Không áp dụng". Minh ghi chú rõ: "sau khi triển khai thực tế mình sẽ cập nhật thay đổi sau" — tức template là bản chốt để bắt đầu triển khai, các thay đổi phát sinh từ thực tế sẽ được cập nhật vào template sau (ghi vào Việc còn bỏ ngỏ, không coi template là bất biến).
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Cập nhật template sau triển khai thực tế -> Minh báo thay đổi khi có. Dự án áp dụng thử (pilot) đầu tiên -> Minh trả lời (Câu 17)

### Câu 15 · Hợp nhất cấu trúc tham khảo QC với cấu trúc kho chính đã chốt (Câu 10)
- Bối cảnh: Ngày 2026-11-27 Minh gửi tài liệu tham khảo "FUTA CITYBUS — Hệ thống Quản trị Tri thức & Quy trình QC Đa Dự Án" (đã lưu tại `phong-van/tham-khao-2026-11-27-cau-truc-futa-citybus-qc.md`) gồm: `00-inbox/` nhật ký điều phối theo ngày + Cổng "Nghiệp vụ Đúng" (chat = ⏳ Chờ BA lên Jira, chỉ Task Jira chính thức mới là chuẩn), `01-core-wiki/` Tầng 1 chia theo miền (web-admin, onbus-hardware, mobile-app-driver, api-integration tách 4 nhóm: nội bộ FUTA / thanh toán / thiết bị-GPS / đối tác vận hành), `02-projects/` Tầng 2 đặt tên `YYYY-qN-<ten>/` có `_template-du-an.md` + `api-integration.md` riêng từng dự án, `03-resources/` thiết bị & môi trường test, báo cáo cuối ngày 17h cho QC Lead Bình, quy ước commit `<type>(<scope>): <mô tả> [Mã Jira]`, git author theo từng cá nhân.
- Review của Peter (đã ghi): Cấu trúc tham khảo mạnh hơn bản Câu 10 ở 4 điểm nên tiếp thu — (1) `00-inbox/` giải quyết khâu tiếp nhận thông tin từ chat/email trước khi có Jira, khớp Cổng "Nghiệp vụ Đúng" đã chốt ở Câu 2/5/12; (2) Tầng 1 chia theo miền + API tách 4 nhóm đúng thực tế Citybus; (3) tên dự án có tiền tố thời gian `YYYY-qN-` giúp sắp xếp/vòng đời; (4) `03-resources/` và quy ước commit message + git author cá nhân giúp truy vết. Có 3 xung đột phải chốt: (i) phạm vi — bản tham khảo là kho tri thức của **QC** (có nhật ký test hằng ngày, tài nguyên test, biên bản sự cố, nhiều người commit hằng ngày) trong khi Câu 8/11 chốt kho nghiệp vụ do **BA** quản lý, chỉ BA merge `main` — gộp chung 1 repo sẽ xung đột phân quyền; (ii) bản tham khảo chưa có thư mục US theo task (Tầng 3) và `templates/` cho US/checklist AI (Câu 14); (iii) `test-environments.md` chứa tài khoản test — không được lưu mật khẩu thật vào git. Ngoài ra git author trong bản tham khảo (`dangquangminh-vn`) khác cấu hình máy Peter (`minhdangquang-ai`) — cần thống nhất khi áp dụng.
- Hỏi: Phạm vi kho cuối cùng chọn hướng nào — (a) 1 repo chung BA+QC theo cấu trúc tham khảo đã bổ sung (phân quyền theo khu vực: `01-core-wiki/` chỉ BA merge; `00-inbox/`, phần tiến độ test trong `02-projects/`, `03-resources/` QC được commit theo quy trình riêng); (b) giữ 2 repo riêng: kho nghiệp vụ của BA (Câu 8-13) và kho QC theo cấu trúc tham khảo, hai bên link lẫn nhau; hay (c) 1 repo nhưng chỉ lấy phần nghiệp vụ của bản tham khảo (inbox + core-wiki + projects), phần nhật ký/tài nguyên test của QC để riêng?
- Đã chốt: Minh không chọn nguyên (a)/(b)/(c), mà chỉ đạo nguyên tắc xử lý cả 3 xung đột. Nguyên văn: "Phân quyền: bản tham khảo là kho của QC — nhiều người commit hằng ngày — đụng thẳng quy tắc Câu 11 => thông tin trên là tham khảo, bạn hãy tối ưu cho vai trò BA nha. Thiếu Tầng 3 => Tối ưu riêng cho vai trò BA. Bảo mật: test-environments.md không được ghi mật khẩu thật vào git — chỉ ghi URL, tên tài khoản và nơi lấy mật khẩu => đồng ý". Hiểu đã chốt: (i) tài liệu QC chỉ là **tham khảo** — không gộp phạm vi/nhân sự QC vào kho này, cấu trúc cuối phải **tối ưu cho vai trò BA**, và quy tắc Câu 11 (chỉ BA maintainer merge `main`) **giữ nguyên**; (ii) Tầng 3 (file US theo task + template US/checklist AI) phải được thiết kế **riêng cho workflow của BA**; (iii) **quy tắc bảo mật được chấp nhận**: không lưu mật khẩu thật vào git, chỉ ghi URL + tên tài khoản + nơi lấy mật khẩu.
- Đề xuất, chưa chốt: (phương án phân quyền theo khu vực của Peter bị thay bằng nguyên tắc tối ưu cho BA ở trên; bản cấu trúc tối ưu cho BA do Peter soạn ở Câu 16 chờ Minh xác nhận)
- Còn bỏ ngỏ: Cấu trúc kho tối ưu cho BA (bản thay thế Câu 10) -> Minh xác nhận (Câu 16). Template US + checklist review AI cho BA -> quay lại Câu 14 sau Câu 16.

### Câu 16 · Cấu trúc kho tối ưu cho vai trò BA (bản thay thế Câu 10)
- Hỏi: Có chốt cấu trúc kho do Peter tối ưu cho BA (giữ khung Câu 10, tiếp thu có chọn lọc từ bản tham khảo QC) không — `README.md` cổng vào; `00-inbox/` là sổ tiếp nhận thông tin thô của **BA** theo ngày (chat/email/yêu cầu từ vận hành/đối tác, trạng thái "Chờ lên Jira" / "Đã lên Jira [link]"), không phải nhật ký test của QC và không có báo cáo 17h cho QC Lead; `01-core-wiki/` là Tầng 1 chia theo miền như bản tham khảo (web-admin, onbus-hardware, mobile-app-driver, api-integration tách 4 nhóm); `02-projects/<YYYY-qN-ten-du-an>/` là Tầng 2 gồm `README.md` mục lục, file nghiệp vụ dự án, `api-integration.md`, và thư mục `us/` chứa Tầng 3 (file Markdown theo mã Task Jira); `03-resources/` phục vụ BA đối chiếu (môi trường: chỉ URL + tên tài khoản + nơi lấy mật khẩu; danh mục thiết bị/đối tác liên quan nghiệp vụ); `99-templates/` gồm template dự án, template US, template Hiện trạng+Thay đổi, checklist review AI. Phân quyền giữ nguyên Câu 11; quy ước commit `<type>(<scope>): <mô tả> [Mã Jira]` và git author cá nhân được tiếp thu từ bản tham khảo.
- Đã chốt: Minh trả lời "ok" — chấp nhận cấu trúc kho tối ưu cho BA như đề xuất, thay thế cấu trúc Câu 10. Đồng thời Minh yêu cầu **log thêm bảng đối chiếu các điểm khác nhau so với bản cấu trúc QC tham khảo** để đối chiếu về sau, và trích rõ 2 ý: (1) `00-inbox` của BA khác bản QC (sổ tiếp nhận của BA, không phải nhật ký test, không có báo cáo 17h cho QC Lead); (2) quy ước commit `<type>(<scope>): mô tả [Mã Jira]` + git author cá nhân là điểm **tiếp thu nguyên vẹn** từ bản QC vì phục vụ truy vết cho BA. Bảng đối chiếu đầy đủ (12 điểm khác + các điểm giống/tiếp thu) đã lập tại file riêng: `phong-van/doi-chieu-cau-truc-BA-vs-QC-tham-khao.md`.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Template US + checklist review AI cho BA -> quay lại Câu 14

### Câu 17 · Dự án áp dụng thử (pilot) đầu tiên
- Hỏi: Toàn bộ workflow/kho/template đã chốt sẽ áp dụng thử đầu tiên ở đâu — (a) 1 dự án mới sắp bắt đầu (dễ control, đúng phân loại ở Câu 3); (b) 1 dự án đang làm có US sắp tới; hay (c) áp dụng ngay cho tất cả dự án?
- Đã chốt: Minh chọn **(a)** — pilot đầu tiên ở **1 dự án mới sắp bắt đầu** (dễ control), kèm phạm vi hẹp theo đề xuất: dựng khung kho + templates, chạy trọn vòng đời vài US từ inbox -> Jira -> review -> merge/tag -> Dev/QC, sau đó tổng kết để xử lý các mục tạm chốt trước khi nhân rộng.
- Đề xuất, chưa chốt: (phạm vi hẹp của đề xuất được áp dụng cùng lựa chọn (a); tên dự án cụ thể chưa xác định)
- Còn bỏ ngỏ: Tên dự án mới cụ thể dùng làm pilot -> Minh xác định khi dự án khởi động. Cách thông báo cho team khi có bản nghiệp vụ mới được merge/tag -> Minh trả lời (Câu 18)

### Câu 18 · Thông báo cho team khi có bản nghiệp vụ mới
- Hỏi: Khi BA merge/tag 1 bản nghiệp vụ mới vào `main`, QC/DEV/Quản lý được biết bằng cách nào — (a) chỉ cần comment trong Task Jira (team tự theo dõi task của mình); (b) comment Jira + nhắn thêm vào group chat chung của dự án; hay (c) có thêm kênh thông báo cố định (ví dụ mục "Bản mới" cập nhật trong README kho / thông báo định kỳ)?
- Đã chốt: Minh chọn **(b)** — mỗi lần merge/tag bản nghiệp vụ mới: **comment trong Task Jira** (lưu vết chính thức, kèm tag và tóm tắt thay đổi) **+ nhắn vào group chat chung của dự án** để team biết ngay và pull bản mới.
- Đề xuất, chưa chốt: (đề xuất của Peter đã được Minh chấp nhận)
- Còn bỏ ngỏ: Vai trò của người dự phòng merge `main` -> Minh trả lời (Câu 19)

### Câu 19 · Người dự phòng merge vào `main` là ai (theo vai trò)?
- Hỏi: Câu 11 đã chốt có 1 người dự phòng nhưng chưa chốt vai trò — người dự phòng merge `main` khi BA vắng/nghỉ là (a) Quản lý của BA; (b) BA thứ hai trong team; hay (c) để trống, xác định khi pilot bắt đầu (ghi tên cụ thể vào README kho lúc đó)?
- Đã chốt: Minh cho biết thực tế (nguyên văn): "thường thì chỉ có 1 BA (cty chưa có người backup đây cũng là 1 rủi ro, nhưng phải chấp nhận tạm thời). Cả team làm task dự án khác hoặc chờ BA vào làm lại rồi merge". Hiểu đã chốt: **hiện không có người dự phòng** — phần "1 người dự phòng" trong Câu 11 được **ghi nhận lại là chưa khả thi ở thời điểm này** (không phải bị bác về nguyên tắc). Quy tắc vận hành khi BA vắng: **đóng băng merge vào `main`**, team chuyển sang làm task của dự án khác hoặc chờ BA quay lại merge. Rủi ro điểm nghẽn 1 người (bus factor = 1) được Minh ý thức rõ và **chấp nhận tạm thời**; giảm thiểu một phần đã có sẵn trong mô hình: kho thuộc sở hữu công ty + bản nghiệp vụ đầy đủ nhất nằm trong kho (Câu 8) nên nếu BA nghỉ hẳn vẫn bàn giao được, chỉ chậm khi BA vắng ngắn hạn.
- Đề xuất, chưa chốt: (đề xuất (b)/(c) của Peter không áp dụng được vì thực tế chưa có BA thứ hai — chờ khi công ty có thêm BA sẽ bổ sung người dự phòng)
- Còn bỏ ngỏ: Bổ sung người dự phòng merge -> xem xét lại khi công ty có thêm BA. Câu hỏi kết thúc phỏng vấn -> Minh trả lời (Câu 20)

### Câu 20 · Câu hỏi kết thúc: còn điều gì chưa được hỏi tới?
- Hỏi: Còn điều gì về workflow làm việc và quản lý nghiệp vụ Citybus mà Peter chưa hỏi tới, hoặc có quyết định nào ở các câu trước bạn muốn sửa/bổ sung không?
- Đã chốt: Minh trả lời "không" — không còn điều gì bổ sung, không sửa quyết định nào. **Buổi phỏng vấn kết thúc tại đây (ngày 2026-11-27)** với 20 câu hỏi; toàn bộ quyết định nằm ở mục "Tóm tắt các quyết định", các mục tạm chốt/chờ thực tế nằm ở "Việc còn bỏ ngỏ".
- Đề xuất, chưa chốt: (không có — câu hỏi mở để Minh bổ sung)
- Còn bỏ ngỏ: (chưa)

## Việc còn bỏ ngỏ
- Quy ước tag theo ngày + mã Task Jira — Minh sẽ review lại sau (tạm chốt ngày 2026-11-26)
- Chuỗi trạng thái workflow Jira — Minh sẽ review lại sau, gồm đối chiếu với board hiện tại của team (tạm chốt ngày 2026-11-27)
- Cập nhật template US + checklist review AI sau khi triển khai thực tế — Minh sẽ báo thay đổi khi phát sinh (ghi chú ngày 2026-11-27)
- Tên dự án mới cụ thể dùng làm pilot -> Minh xác định khi dự án khởi động (Câu 17 đã chốt pilot ở 1 dự án mới)
- Rủi ro chỉ có 1 BA, không có người backup merge — Minh đã chấp nhận tạm thời (Câu 19); xem xét lại khi công ty có thêm BA

