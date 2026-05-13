---
artifact: 1 — FINAL kế hoạch giải pháp
bai-tap: 2 — Thiết kế giải pháp
phase: Chọn rủi ro + chọn tầng + chọn demo + chốt 3 lớp giải pháp
time: 11:00-11:55
input: 00-context.md + 01-test-set-review/3-FINAL-test-set-eval-plan.md
nop-cuoi: Có — file cuối Bài 2
---

# 1 — FINAL: Kế hoạch giải pháp

File này ghi lại quyết định chính của Bài 2:

- Rủi ro nào được chọn.
- Vì sao rủi ro đó quan trọng.
- Nguyên nhân gốc là gì.
- Nhóm sẽ xây 3 lớp giải pháp nào.
- Mỗi lớp dùng demo gì.

Lý do cần 3 lớp: một giải pháp đơn lẻ dễ lọt lỗi. Với rủi ro nặng, nhóm cần nhiều lớp cùng đỡ: lớp này ngăn, lớp kia phát hiện, lớp khác khắc phục hoặc thông báo cho người dùng.

Ba lớp giải pháp nằm trong thư mục `artifact/`:

| Lớp | Thư mục | Vai trò |
|---|---|---|
| Giao diện | `artifact/1-uiux/` | Cảnh báo, dẫn nguồn, nút chuyển sang người thật |
| Chỉ dẫn AI | `artifact/2-prompt/` | Hỏi lại, từ chối, bắt buộc dẫn nguồn |
| Kiến trúc dữ liệu | `artifact/3-architecture/` | Tra cứu nguồn đúng, lưu tạm dữ liệu, xử lý khi thiếu nguồn, giám sát |

Ba lớp này bổ sung cho nhau. Nếu một lớp lọt lỗi, lớp khác vẫn có thể chặn hoặc giảm hại.

## Thông tin nhóm

- **Chủ đề**: Trợ lý AI sàng lọc triệu chứng y tế (Symptom Triage Chatbot)
- **Thành viên**: Đặng Tuấn Anh, Dương Khoa Điềm, Nguyễn Tuấn Khanh
- **Ngày**: 2026-05-13

---

## Phần A — Chọn rủi ro và tầng giải pháp

### Rủi ro chính được chọn

- **ID tình huống**: T-01
- **Mô tả ngắn**: Khi phát hiện dấu hiệu cảnh báo đỏ (tức ngực, khó thở, tê tay), AI có xu hướng bị "neo" theo chẩn đoán chủ quan của bệnh nhân (self-diagnosis là "do mệt mỏi/chạy deadline"), gây trì hoãn cấp cứu cho bệnh nhân có nguy cơ nhồi máu cơ tim.
- **Mức độ**: Nặng
- **Điểm rủi ro**: 25
- **Vì sao chọn tình huống này**: Đây là một trong những lỗi gây hậu quả sinh mạng trực tiếp nhất (tử vong do bỏ sót nhồi máu cơ tim). Bẫy thao túng chẩn đoán cũng là bẫy phổ biến nhất mà các AI y tế sơ khai thường mắc phải.

### Tìm nguyên nhân gốc

Đừng chỉ mô tả lỗi. Hãy trả lời: vì sao lỗi xảy ra?

- [ ] Thiếu nguồn dữ liệu đúng.
- [x] AI đoán khi không biết (bị cuốn theo thông tin của người dùng cung cấp).
- [ ] Giao diện khiến người dùng tin quá mức.
- [x] Quy trình thiếu người duyệt hoặc thiếu bước chuyển sang người thật (Hệ thống phụ thuộc 100% vào LLM để phân loại bệnh thay vì có một hệ thống rule-based quét từ khoá đỏ).
- [ ] Không có theo dõi sau khi ra mắt.
- [ ] Khác: [...]

### Bảng nối nguyên nhân với tầng sửa

| Nguyên nhân gốc | Tầng ưu tiên sửa | Lớp giải pháp liên quan |
|---|---|---|
| AI bị thao túng tâm lý / hùa theo user | Chỉ dẫn hệ thống / quy tắc từ chối | `2-prompt` là chính |
| Hệ thống phụ thuộc 100% vào AI sinh tạo | Tách luồng / Chặn bằng Rule-based Classifier | `3-architecture` là chính |
| User trì hoãn do không nhận thức được mức độ | Giao diện cảnh báo khẩn cấp | `1-uiux` là chính |

Nguyên tắc: lỗi ở tầng nào, ưu tiên sửa ở tầng đó. Đừng chỉ thêm cảnh báo giao diện nếu nguyên nhân gốc là thiếu nguồn dữ liệu hoặc AI đoán khi không biết.

### Kết luận Phần A

**Nguyên nhân gốc**: Hệ thống giao toàn quyền phân loại triệu chứng khẩn cấp cho một mô hình LLM chung chung, trong khi LLM dễ bị thiên lệch (bias) bởi các câu tự trấn an của người dùng. Thiếu một luồng xử lý độc lập cho các rủi ro đỏ (Red-flag router).

**Tầng chính cần sửa**: Chỉ dẫn AI (Prompt) và Kiến trúc dữ liệu (Architecture).

**Vì sao cần 3 lớp giải pháp**:

- Lớp giao diện: Cần hiển thị cảnh báo đỏ và nút "Gọi cấp cứu ngay" để gián đoạn luồng chat thông thường, buộc người dùng chú ý.
- Lớp chỉ dẫn AI: Phải có system prompt chỉ thị rõ "Tuyệt đối không đồng tình với chẩn đoán chủ quan của bệnh nhân khi có các keyword: tức ngực, khó thở".
- Lớp kiến trúc dữ liệu: Cần một Classifier (ví dụ Rule-based hoặc NLP nhỏ) quét tin nhắn trước khi gửi vào LLM. Nếu phát hiện keyword khẩn cấp, kích hoạt kịch bản Triage Đỏ thay vì để LLM tự do đối đáp.

---

## Phần B — Chọn định dạng demo

Mỗi lớp cần một bản demo. Demo giúp biến ý tưởng thành thứ trực quan để nhóm khác xem, kiểm tra và phản biện.

| Lớp | Thư mục | Định dạng demo chọn | Thời gian dự kiến |
|---|---|---|---|
| Giao diện | `1-uiux` | Bản nháp ASCII / Mockup text UI | 15 phút |
| Chỉ dẫn AI | `2-prompt` | Bản prompt trong Markdown + ví dụ test case | 15 phút |
| Kiến trúc dữ liệu | `3-architecture` | Sơ đồ Mermaid (Flowchart) | 15 phút |

**Lý do chọn demo**

- Giao diện: Dùng ASCII/Text UI để vẽ nhanh cảnh báo khẩn cấp (Emergency Banner) chèn lên khung chat.
- Chỉ dẫn AI: Việc viết thẳng System Prompt giúp chứng minh rõ các ràng buộc an toàn (Safety constraints) ép AI phải tuân thủ.
- Kiến trúc dữ liệu: Mermaid Flowchart là tốt nhất để biểu diễn luồng đi của dữ liệu từ User -> Keyword Router -> (nếu đỏ) -> Luồng cấp cứu / (nếu bình thường) -> Luồng LLM.

---

## Phần C — Ba lớp giải pháp

Ghi tóm tắt ở đây. Chi tiết nằm trong `card.md` và `demo.*` của từng thư mục.

### Lớp 1 — Giao diện (`artifact/1-uiux/`)

- **Cách tiếp cận**: Bổ sung "Emergency Banner" (Cảnh báo đỏ) và nút bấm "Gọi 115" nổi lên ngay lập tức trên màn hình khi AI nhận diện rủi ro, vô hiệu hóa khung nhập liệu chat để tránh user cố tranh luận thêm.
- **Hành động phòng vệ bao phủ**: Thông báo (cho user biết rủi ro) / Khắc phục (đưa giải pháp gọi 115 ngay).
- **Demo**: ASCII UI Mockup.
- **Trạng thái**: Chờ thực hiện.

### Lớp 2 — Chỉ dẫn AI (`artifact/2-prompt/`)

- **Cách tiếp cận**: Nâng cấp System Prompt với phần "Red-Flag Protocol". Quy định rõ 3 cấm kỵ: (1) Cấm đồng ý với chẩn đoán của bệnh nhân, (2) Cấm gợi ý theo dõi tại nhà nếu có triệu chứng tim mạch, (3) Cấm kéo dài hội thoại.
- **Hành động phòng vệ bao phủ**: Ngăn (chặn AI hùa theo người dùng) / Từ chối (từ chối cung cấp lịch khám ngày mai).
- **Demo**: Bản Markdown System Prompt v2 + Test case mẫu.
- **Trạng thái**: Chờ thực hiện.

### Lớp 3 — Kiến trúc dữ liệu (`artifact/3-architecture/`)

- **Cách tiếp cận**: Thêm một `Red-Flag Router` (Bộ phân luồng rủi ro đỏ) ngay trước LLM. Dùng Regex hoặc mô hình NLP nhẹ quét từ khoá "tức ngực, khó thở, tê tay". Nếu khớp, router sẽ gọi một Template trả lời cứng (Hard-coded) thay vì để LLM tự sinh chữ.
- **Hành động phòng vệ bao phủ**: Phát hiện (quét tin nhắn ngay từ cửa ngõ) / Ngăn (tránh rủi ro Hallucination của LLM).
- **Demo**: Sơ đồ Mermaid Flowchart.
- **Trạng thái**: Chờ thực hiện.

---

## Tổng kiểm tra

| Câu hỏi | Trả lời |
|---|---|
| Rủi ro chính đã chọn là gì? | T-01 (Bỏ sót rủi ro tim mạch do hùa theo user) |
| Nguyên nhân gốc là gì? | LLM bị thao túng bởi self-diagnosis + Thiếu bộ lọc từ khoá cứng độc lập. |
| 3 lớp giải pháp đã đủ chưa? | Giao diện: 1 / Chỉ dẫn AI: 1 / Kiến trúc: 1 |
| 4 hành động đã bao phủ chưa? | Ngăn: Có (Prompt, Arch) / Phát hiện: Có (Arch) / Khắc phục: Có (UI) / Thông báo: Có (UI) |
| Nhóm khác đã góp ý chưa? | Chưa |
| Nhóm đã sửa gì sau phản biện? | Chưa |

## Phản biện chéo: 4 câu phải trả lời

Khi nhóm khác góp ý, hoặc khi nhóm tự rà lại, dùng 4 câu này:

| Góc phản biện | Câu hỏi |
|---|---|
| Đúng tầng | Giải pháp có sửa đúng nguyên nhân gốc không? |
| Cụ thể | Demo có đủ rõ để hiểu cách vận hành không? |
| Đủ lớp | 3 lớp có bổ sung cho nhau không, hay đang lặp cùng một ý? |
| Tác dụng phụ | Giải pháp có làm chậm, tốn kém, rối giao diện, hoặc gây hiểu nhầm mới không? |

Ghi góp ý cụ thể vào `card.md` hoặc phần tổng kiểm tra. Không ghi chung chung "ổn" hoặc "chưa ổn".

## Gợi ý chia việc

Nhóm 3 người:

- Đặng Tuấn Anh: `artifact/1-uiux/`
- Dương Khoa Điềm: `artifact/2-prompt/`
- Nguyễn Tuấn Khanh: `artifact/3-architecture/`

5 phút cuối: cả nhóm đọc chéo 3 lớp, sửa lại bảng tổng kiểm tra, rồi chuẩn bị phản biện chéo.
