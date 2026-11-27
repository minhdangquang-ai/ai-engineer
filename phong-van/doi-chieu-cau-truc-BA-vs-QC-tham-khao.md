# Đối chiếu: Cấu trúc kho tối ưu cho BA (đã chốt Câu 16) vs Bản cấu trúc QC tham khảo
Ngày lập: 2026-11-27 · Mục đích (theo yêu cầu của Minh): log rõ các điểm KHÁC nhau giữa hai phiên bản để đối chiếu về sau.
Nguồn đối chiếu:
- Bản BA: file phỏng vấn `2026-11-26-workflow-quan-ly-nghiep-vu-citybus.md`, Câu 16 (thay thế Câu 10).
- Bản QC tham khảo: `tham-khao-2026-11-27-cau-truc-futa-citybus-qc.md`.

## A. Các điểm KHÁC nhau

| # | Hạng mục | Bản QC tham khảo | Bản tối ưu cho BA (đã chốt) | Lý do khác |
|---|----------|------------------|------------------------------|------------|
| 1 | Mục đích kho | Quản trị tri thức & quy trình **QC đa dự án**: nghiệp vụ + nhật ký kiểm thử + hồ sơ test | Quản lý **nghiệp vụ của BA**: nơi BA soạn, chốt và phát hành nghiệp vụ đúng cho team | Vai trò chủ kho khác nhau (Câu 15: bản QC chỉ là tham khảo) |
| 2 | Chủ kho / đầu mối | QC Lead **Bình** — nhận báo cáo cuối ngày 17h | **BA** (maintainer) + 1 người dự phòng; không có đầu mối QC Lead | Trách nhiệm nghiệp vụ đúng thuộc BA (Câu 5) |
| 3 | Phân quyền merge `main` | Nhiều thành viên commit hằng ngày (mỗi người 1 git author) | **Chỉ BA merge vào `main`**; QC/DEV chỉ đọc/clone, góp ý qua comment Jira (Câu 11) | Tránh nhiều đầu mối sửa nghiệp vụ làm lệch "bản đầy đủ nhất" |
| 4 | `00-inbox/` — nội dung | **Nhật ký điều phối QC theo ngày**, mẫu 4 phần: tiếp nhận, phân loại, tiến độ test, báo cáo | **Sổ tiếp nhận thông tin thô của BA** theo ngày: chat/email/yêu cầu từ vận hành & đối tác, trạng thái "Chờ lên Jira" / "Đã lên Jira [link]" | BA cần khâu intake trước khi lên Jira, không cần nhật ký test |
| 5 | Báo cáo cuối ngày 17h | **Có** — tổng hợp từ inbox gửi QC Lead Bình | **Không có** — đã loại bỏ | Đây là vận hành của QC, ngoài phạm vi BA |
| 6 | Luồng xử lý sự cố | Email lỗi/sự cố phức tạp: tóm tắt + review với QC Lead/PO, chờ "OK" mới lập biên bản trong `02-projects/` | Sự cố chỉ vào kho BA khi **ảnh hưởng quy tắc nghiệp vụ**; xử lý thay đổi theo Câu 13 (branch/tag/snapshot mới) | BA chỉ quản lý khía cạnh nghiệp vụ của sự cố |
| 7 | Tầng 3 (US theo task) | **Không có** — dự án chỉ có README + `api-integration.md`, tiến độ test ở "Khối 4" | **Có thư mục `us/`** trong từng dự án, chứa file Markdown theo mã Task Jira | Đây là sản phẩm chính hằng ngày của BA (Câu 15: tối ưu riêng cho BA) |
| 8 | Templates | `_template-du-an.md` trong `02-projects/` + `daily-log-template.md` trong inbox | Thư mục riêng **`99-templates/`**: template dự án, **template US, template Hiện trạng+Thay đổi, checklist review AI** | Template của BA phục vụ soạn/chốt US và kiểm soát AI (Câu 6, Câu 14) |
| 9 | `03-resources/` | Tài nguyên **kiểm thử**: thiết bị test vật lý, URL Dev/Staging/UAT & tài khoản test phân quyền cho QC | Tài nguyên **đối chiếu của BA**: môi trường + danh mục thiết bị/đối tác liên quan nghiệp vụ | Cùng tên thư mục, khác đối tượng phục vụ |
| 10 | Quan hệ với Jira | Markdown **không trùng lặp** Jira/TestRail: chỉ lưu link Filter/Dashboard/Ticket + bảng tóm tắt | Markdown trong kho là **bản nghiệp vụ đầy đủ**; Jira giữ Mô tả + **snapshot** lúc chốt + comment (mô hình 2 lớp, Câu 8) | BA cần kho là bản đầy đủ nhất để clone (Câu 7) |
| 11 | Branch & Tag | **Không có** quy định branch/tag — chỉ có quy ước commit | **Có**: branch `draft/<mã task>` -> merge `main` (Câu 9); **tag theo ngày + mã Task Jira** (tạm chốt) | Nhu cầu quản lý version của BA |
| 12 | Cổng kiểm soát | Cổng "Nghiệp vụ Đúng": chat = ⏳ chờ, có Task Jira = ✅ đã chốt | Giữ nguyên ý tưởng cổng, nhưng cụ thể hóa thành **workflow Jira Câu 12** + **cổng review AI phân tầng rủi ro Câu 6** + ký xác nhận của BA | Cổng của BA gắn với trạng thái task và chất lượng file US |

## B. Các điểm GIỐNG / tiếp thu nguyên vẹn từ bản QC (để khỏi nhầm là khác)

| Hạng mục | Nội dung tiếp thu |
|----------|-------------------|
| Khung thư mục gốc | `00-inbox/`, `01-core-wiki/`, `02-projects/`, `03-resources/` giữ nguyên số thứ tự và vị trí |
| Tầng 1 `01-core-wiki/` | Chia theo miền: web-admin, onbus-hardware, mobile-app-driver, api-integration (4 nhóm API: nội bộ FUTA / thanh toán / thiết bị-GPS / đối tác vận hành) |
| Tên dự án | Tiền tố thời gian `YYYY-qN-<ten-ngan>/`, kebab-case không dấu |
| Tên file nhật ký inbox | `YYYY-MM/YYYY-MM-DD.md` |
| Quy ước commit | `<type>(<scope>): <mô tả ngắn> [Mã Jira]` với type `log/docs/feat/chore` — **tiếp thu nguyên vẹn** vì phục vụ truy vết cho BA (đúng như Minh trích dẫn khi yêu cầu log đối chiếu) |
| Git author | Mỗi người cấu hình `user.name`/`user.email` cá nhân — tiếp thu nguyên vẹn. Lưu ý chênh lệch cần thống nhất: bản QC ghi `dangquangminh-vn <dangquangminh.vn@gmail.com>`, máy của Peter đang là `minhdangquang-ai <minhdangquang.ai@gmail.com>` |
| Bảo mật môi trường | Không ghi mật khẩu thật vào git — chỉ URL + tên tài khoản + nơi lấy mật khẩu (Minh đã đồng ý ở Câu 15; bản QC gốc chưa nêu rõ điều này, đây là điểm bản BA bổ sung chặt hơn) |
| Nguyên tắc cổng nghiệp vụ | Thông tin trên chat chưa có Jira thì chưa phải nghiệp vụ chuẩn |

## C. Ghi chú của Minh khi yêu cầu lập bảng đối chiếu này (nguyên văn)
"Điểm khác với bản QC: 00-inbox là sổ tiếp nhận của BA (không phải nhật ký test, không có báo cáo 17h cho QC Lead), và quy ước commit <type>(<scope>): mô tả [Mã Jira] + git author cá nhân thì tiếp thu nguyên vẹn vì nó phục vụ truy vết cho BA."
