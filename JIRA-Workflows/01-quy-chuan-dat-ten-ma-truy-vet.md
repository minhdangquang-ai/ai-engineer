# Quy chuẩn đặt tên & mã truy vết (Naming & Traceability Standard)

> Nguồn quyết định: buổi phỏng vấn grill-me "JIRA-Workflows" ngày 2026-11-27 (file `phong-van/2026-11-27-jira-workflows.md`) và tài liệu quy chuẩn gốc Minh cung cấp cùng ngày.
> Áp dụng cho: mọi dự án con trong project Jira **CITY** (vatoteam.atlassian.net) và kho nghiệp vụ `CITYBUS-Workflows/`.

## 1. Nguyên tắc nền tảng

1. **Một project Jira duy nhất:** toàn bộ dự án con dùng chung project key `CITY`. Mỗi dự án con là **1 Component** trong CITY (vd Component `FTT`) và có **board Scrum riêng** lọc theo Component đó.
2. **Mã dự án con không phải project key:** mã như `FTT` dùng làm **quy tắc hiển thị trên tiêu đề (Summary)** của ticket và trong mọi mã truy vết — để nhìn tiêu đề là biết ticket thuộc dự án nào mà không cần mở ra xem.
3. **Mã TC không sống trên Jira:** QC đọc task từ Jira rồi tự phân tích thành bộ test case riêng của QC (ngoài Jira). Chỉ khi phát hiện lỗi, QC mới tạo **Bug trên Jira** gắn với task của BA.

## 2. Công thức mã tổng quát

```
[MÃ_DỰ_ÁN]-[LOẠI_TÀI_LIỆU]-[MÃ_CHA].[SỐ_THỨ_TỰ]
```

Quy tắc bất biến: **cấp con luôn dùng dấu chấm phân cấp** (vd `.01`), không bao giờ đánh số thứ tự chạy dài ở cấp con — để AI (Rovo) và con người đều truy vết được cây cha–con.

## 3. Các loại tài liệu / thực thể

| Loại | Định dạng mã | Ý nghĩa |
|---|---|---|
| **FR** — Functional Requirement | `[PRJ]-FR-[001..999]` | Tính năng chính. Được phép chia dải số theo phân hệ (vd 1xx = Auth, 2xx = Vận hành, 3xx = Báo cáo) |
| **NFR** — Non-Functional Requirement | `[PRJ]-NFR-[001..999]` | Yêu cầu phi chức năng: hiệu năng, bảo mật, offline, chịu tải, Kiosk mode... |
| **SCR** — Screen | `[PRJ]-SCR-[Mã FR].[01..99]` | Màn hình/giao diện, gắn với FR chứa nó |
| **US** — User Story | `[PRJ]-US-[Mã FR].[01..99]` | Câu chuyện người dùng — đặc tả chi tiết dưới FR |
| **BR** — Business Rule | `[PRJ]-BR-[Mã FR].[Mã US]-[NHÓM]-[01..99]` | Ràng buộc **đặc thù, chỉ tồn tại trong đúng 1 US** |
| **CM** — Common Rule | `[PRJ]-CM-[NHÓM]-[001..999]` | Ràng buộc **dùng chung toàn dự án**, nhiều US cùng tham chiếu |
| **TC** — Test Case | `[PRJ]-TC-[Mã FR].[Mã US]-[01..99]` | Kịch bản kiểm thử của QC — quản lý ngoài Jira |
| **BUG** | Theo định dạng tiêu đề ở Mục 6 | Báo cáo lỗi — tạo trên Jira, gắn với task của BA |

**AC (Acceptance Criteria)** giữ định dạng ngắn `AC-01`, `AC-02`... trong nội bộ từng US (đã chốt 2026-11-27): AC chỉ sống trong 1 US nên không cần tiền tố phân cấp.

## 4. BR hay CM? — Quy tắc phân biệt

| Tiêu chí | BR | CM |
|---|---|---|
| Phạm vi áp dụng | Chỉ 1 màn hình / 1 US cụ thể | Toàn dự án, nhiều màn hình/US dùng lại |
| Ví dụ | `FTT-BR-001.01-VAL-01` — Kiểm tra trường bắt buộc và định dạng mật khẩu **khi đăng nhập** | `FTT-CM-VAL-002` — Quy tắc trường bắt buộc và mật khẩu 6–32 ký tự, dùng lại cho màn Đổi mật khẩu / Tạo tài khoản |

**Ví dụ tình huống:** yêu cầu "SĐT và mật khẩu là bắt buộc; mật khẩu 6–32 ký tự, không chứa khoảng trắng" — phần kiểm tra gắn riêng với màn Đăng nhập là **BR**; quy tắc mật khẩu chuẩn dùng chung cho nhiều màn là **CM**.

## 5. Bảy nhóm ràng buộc kỹ thuật

Điền vào vị trí `[NHÓM]` trong mã BR/CM:

| Nhóm | Tên đầy đủ | Ý nghĩa |
|---|---|---|
| `VAL` | Validation | Kiểm tra hợp lệ dữ liệu đầu vào (bắt buộc, độ dài, định dạng) |
| `SEC` | Security & Auth | Bảo mật, xác thực, phân quyền |
| `WFL` | Workflow & State | Luồng xử lý, chuyển đổi trạng thái |
| `CAL` | Calculation & Logic | Tính toán, ngưỡng cảnh báo |
| `INT` | Integration & Sync | Tích hợp API, đồng bộ giữa các hệ thống |
| `EXC` | Exception & Error | Xử lý ngoại lệ, thông báo lỗi |
| `FMT` | Format & Display | Định dạng hiển thị |

## 6. Định dạng tiêu đề (Summary) trên Jira

**Ticket nghiệp vụ (FR/US...):** bắt đầu bằng mã truy vết, tiếp theo là tên ngắn gọn.

```
FTT-US-001.01 Đăng nhập bằng SĐT và mật khẩu
```

**Bug:** `[Đối tượng] [Bug] [Module] Mô tả lỗi ngắn gọn`

```
[Dev-BE] [Bug] [Tour] Lỗi get số tour từ EZ
```

Trong đó `[Đối tượng]` gồm môi trường + phía xử lý, vd `[Dev-BE]`, `[Dev-App]`, `[Prod-BE]` (chi tiết ở prompt Bug Architect: `prompts/prompt-qc-agent-bug-architect.md`).

## 7. Nguyên tắc Self-Contained Story (cho AI/Rovo đọc đúng)

Khi một US tham chiếu tới 1 CM, **bắt buộc dán tóm tắt 1–2 dòng nội dung của CM đó vào Description của US** — không để AI phải tự đi tìm CM ở nơi khác (AI rất dễ bỏ sót context khi phải nhảy nhiều tầng link).

## 8. Áp dụng cho AI Agent

Bảng quy tắc đặt mã trong tài liệu này được **khóa cứng (hard-lock)** vào prompt của các AI Agent — xem thư mục `prompts/`:

- `prompt-ba-agent.md` — Agent cho BA: sinh US/BR/CM.
- `prompt-qc-agent-testcase.md` — Agent cho QC: sinh TC.
- `prompt-qc-agent-bug-architect.md` — Agent cho QC: tạo Bug chuẩn cấu trúc.

AI **không được tự bịa mã** ngoài quy chuẩn này; thiếu thông tin để cấp mã thì phải hỏi lại người dùng.
