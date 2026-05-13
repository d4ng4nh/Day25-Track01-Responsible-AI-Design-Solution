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
- **Mô tả ngắn**: Khi người dùng có các triệu chứng khẩn cấp (tức ngực, khó thở, tê tay) nhưng tự chẩn đoán là bệnh nhẹ (ví dụ: "do chạy deadline mệt mỏi"), AI có xu hướng bị "neo" theo chẩn đoán này và cho phép trì hoãn khám, gây lọt lưới bệnh lý nhồi máu cơ tim nguy hiểm.
- **Mức độ**: Nặng
- **Điểm rủi ro**: 25
- **Vì sao chọn tình huống này**: Đây là một rủi ro liên quan trực tiếp đến tính mạng. Bệnh nhân có xu hướng tự coi nhẹ triệu chứng, nếu AI hùa theo (sycophancy) thì sẽ mất cơ hội vàng để cấp cứu nhồi máu cơ tim.

### Tìm nguyên nhân gốc

- [ ] Thiếu nguồn dữ liệu đúng.
- [x] AI đoán khi không biết / AI bị "neo" theo thông tin sai lệch từ người dùng (Sycophancy).
- [ ] Giao diện khiến người dùng tin quá mức.
- [x] Quy trình thiếu người duyệt hoặc thiếu bước chuyển sang người thật (Thiếu bộ lọc từ khóa nguy hiểm độc lập với LLM).
- [ ] Không có theo dõi sau khi ra mắt.
- [ ] Khác: [...]

### Bảng nối nguyên nhân với tầng sửa

| Nguyên nhân gốc | Tầng ưu tiên sửa | Lớp giải pháp liên quan |
|---|---|---|
| AI bị thao túng tâm lý / hùa theo user | Chỉ dẫn hệ thống / quy tắc từ chối | `2-prompt` là chính |
| Hệ thống phụ thuộc 100% vào LLM để phân loại | Quy trình xử lý / Classifier chặn | `3-architecture` là chính |
| User trì hoãn do không nhận thức độ nguy hiểm | Giao diện cảnh báo khẩn cấp | `1-uiux` là chính |

### Kết luận Phần A

**Nguyên nhân gốc**: Hệ thống giao toàn quyền sàng lọc cho một mô hình LLM chung chung, trong khi LLM dễ bị thiên lệch (bias) bởi các giả định của người bệnh. Không có lớp chốt chặn (hard rule) độc lập để vớt các từ khóa báo động đỏ (red flags).

**Tầng chính cần sửa**: Chỉ dẫn AI (Prompt) và Kiến trúc dữ liệu (Architecture / Rule-based router).

**Vì sao cần 3 lớp giải pháp**:

- **Lớp giao diện**: Cần hiển thị cảnh báo đỏ và nút "Gọi cấp cứu 115" ngay lập tức để giành sự chú ý của user, ngăn user tiếp tục tranh luận.
- **Lớp chỉ dẫn AI**: Cần tiêm "Red-Flag Protocol" vào System Prompt, cấm AI tuyệt đối không đồng tình với các chẩn đoán tâm lý/mệt mỏi khi xuất hiện triệu chứng tim mạch.
- **Lớp kiến trúc dữ liệu**: Xây dựng Classifier/Router quét từ khóa trước khi gọi LLM. Nếu thấy "đau ngực", "tê tay", chặn luồng bình thường và ép AI dùng template trả lời khẩn cấp.

---

## Phần B — Chọn định dạng demo

| Lớp | Thư mục | Định dạng demo chọn | Thời gian dự kiến |
|---|---|---|---|
| Giao diện | `1-uiux` | Bản mockup ASCII UI | 15 phút |
| Chỉ dẫn AI | `2-prompt` | Bản system prompt Markdown + Test case | 15 phút |
| Kiến trúc dữ liệu | `3-architecture` | Sơ đồ Mermaid (Flowchart) | 15 phút |

**Lý do chọn demo**

- **Giao diện**: ASCII UI giúp mô phỏng nhanh vị trí của Banner Cảnh Báo Khẩn Cấp đè lên giao diện chat, chứng minh người dùng không thể bỏ qua cảnh báo này.
- **Chỉ dẫn AI**: System Prompt viết bằng Markdown thể hiện rõ logic "If X then Y" giúp AI hiểu giới hạn (boundary) của mình.
- **Kiến trúc dữ liệu**: Sơ đồ Mermaid biểu diễn rõ luồng đi của dữ liệu qua các bộ lọc (Keyword Router -> LLM) giúp hình dung kiến trúc phân luồng (Triage).

---

## Phần C — Ba lớp giải pháp

### Lớp 1 — Giao diện (`artifact/1-uiux/`)

- **Cách tiếp cận**: Bổ sung "Emergency Red Banner" nổi bật trên cùng và nút "Gọi Cấp Cứu 115" ở trung tâm khung chat khi AI phát hiện mức độ rủi ro cao. Khóa (disable) ô nhập liệu để buộc user hành động.
- **Hành động phòng vệ bao phủ**: Thông báo / Khắc phục
- **Demo**: ASCII UI Mockup
- **Trạng thái**: Đã lên kế hoạch (Sẵn sàng triển khai ở bài tập tiếp theo)

Link chi tiết:
- `artifact/1-uiux/card.md`
- `artifact/1-uiux/demo.md` (hoặc `demo.txt`)

### Lớp 2 — Chỉ dẫn AI (`artifact/2-prompt/`)

- **Cách tiếp cận**: Bổ sung "Red-Flag Triage Protocol" vào System Prompt. Yêu cầu AI (1) KHÔNG đồng tình với các giả định nguyên nhân của user, (2) KHÔNG hẹn khám ngày mai với các triệu chứng đỏ, (3) LUÔN kết thúc câu trả lời bằng lời khuyên đến viện ngay.
- **Hành động phòng vệ bao phủ**: Ngăn / Từ chối
- **Demo**: System Prompt v2 + Ví dụ đối thoại
- **Trạng thái**: Đã lên kế hoạch

Link chi tiết:
- `artifact/2-prompt/card.md`
- `artifact/2-prompt/demo.md`

### Lớp 3 — Kiến trúc dữ liệu (`artifact/3-architecture/`)

- **Cách tiếp cận**: Thêm bước `Red-Flag NLP Router` quét regex/keyword tin nhắn đầu vào. Nếu match "tức ngực|khó thở", kích hoạt cờ `is_emergency=True`. Bơm cờ này vào LLM hoặc trả thẳng hard-coded template mà không cần LLM phân tích.
- **Hành động phòng vệ bao phủ**: Ngăn / Phát hiện
- **Demo**: Sơ đồ hộp-mũi tên Mermaid
- **Trạng thái**: Đã lên kế hoạch

Link chi tiết:
- `artifact/3-architecture/card.md`
- `artifact/3-architecture/demo.md`

---

## Tổng kiểm tra

| Câu hỏi | Trả lời |
|---|---|
| Rủi ro chính đã chọn là gì? | T-01 (Bỏ sót rủi ro tim mạch do AI hùa theo người dùng) |
| Nguyên nhân gốc là gì? | Phụ thuộc hoàn toàn vào LLM sinh tạo + LLM bị bẫy thao túng chẩn đoán. |
| 3 lớp giải pháp đã đủ chưa? | Giao diện: 1 / Chỉ dẫn AI: 1 / Kiến trúc: 1 |
| 4 hành động đã bao phủ chưa? | Ngăn: Có (Prompt, Arch) / Phát hiện: Có (Arch) / Khắc phục: Có (UI) / Thông báo: Có (UI) |
| Nhóm khác đã góp ý chưa? | Chưa |
| Nhóm đã sửa gì sau phản biện? | Chưa |

## Phản biện chéo: 4 câu phải trả lời

(Sẽ được thực hiện trong quá trình thiết kế chi tiết ở thư mục artifact)

## Gợi ý chia việc

- Đặng Tuấn Anh: Phụ trách `artifact/1-uiux/`
- Dương Khoa Điềm: Phụ trách `artifact/2-prompt/`
- Nguyễn Tuấn Khanh: Phụ trách `artifact/3-architecture/`
