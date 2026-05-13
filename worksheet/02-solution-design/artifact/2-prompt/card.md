---
artifact: 2 — Lớp chỉ dẫn AI
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp chỉ dẫn AI

**Tình huống xử lý**: T-01 (Lọt lưới nhồi máu cơ tim do AI hùa theo người bệnh)
Xem `../../1-map-and-format-final.md` Phần A.

---

## 1. Giải pháp là gì?

Nhóm sẽ nâng cấp System Prompt bằng cách bổ sung "Red-Flag Triage Protocol" (Giao thức Cấp cứu Đỏ). 
Cụ thể, AI sẽ bị ràng buộc bởi các luật cứng: tuyệt đối cấm đồng thuận (sycophancy) với các chẩn đoán chủ quan tâm lý (ví dụ: "do mệt", "do stress") của bệnh nhân khi có xuất hiện các triệu chứng báo động đỏ như tức ngực, khó thở, tê tay. Nếu có rủi ro, AI buộc phải kết luận bằng lời khuyên đi cấp cứu.

---

## 2. Vì sao sửa ở lớp chỉ dẫn AI?

- AI đang chiều theo giả định sai của người dùng (bị "neo" tâm lý).
- AI cần luật rõ: khi nào trả lời, khi nào từ chối (từ chối việc hẹn khám ngày mai hoặc theo dõi tại nhà).
- Có thể sửa nhanh bằng prompt trước khi thay đổi hệ thống lớn hơn (như viết Rule-based NLP ở lớp kiến trúc).

**Hành động phòng vệ chính**:

- [x] Ngăn câu trả lời sai ngay từ đầu (Ngăn AI đồng ý với user)
- [ ] Bắt buộc nêu nguồn khi nói về thông tin quan trọng
- [x] Từ chối trả lời khi thiếu căn cứ (Từ chối việc trì hoãn cấp cứu)
- [x] Chuyển người thật khi vượt phạm vi (Gọi 115)

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo cần có:

- Luật chính cho AI (Red-Flag Protocol)
- Mẫu câu khi đối mặt với rủi ro đỏ
- Mẫu câu khi cần từ chối
- 3 ví dụ hỏi đáp để kiểm tra luật
- Kết quả thử lại với vài tình huống từ Bài 1

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

AI có thể trở nên quá cứng nhắc, "nhìn đâu cũng thấy bệnh nặng", khiến người dùng hoang mang với cả những bệnh lý thông thường. Trải nghiệm chat có thể bị giảm do AI từ chối giải thích thêm mà chỉ nằng nặc khuyên đi viện.

**Nhóm giảm vấn đề đó bằng cách nào?**

Chỉ kích hoạt luật cấm đồng thuận cứng ngắc với nhóm từ khoá (keywords) cảnh báo đỏ cụ thể (tim mạch, đột quỵ, nhi khoa nguy kịch). Ở trong System Prompt sẽ dặn AI vẫn phải giữ thái độ lịch sự, chuyên nghiệp, không cần hoảng loạn nhưng phải kiên quyết.

---

## 5. Checklist trước khi nộp

- [x] Luật viết đủ cụ thể để AI làm theo.
- [x] Có mẫu câu khi AI không có đủ thông tin.
- [x] Có ví dụ cho tình huống dễ sai.
- [x] Có thử lại bằng tình huống trong Bài 1.
- [x] Không dùng prompt như cách duy nhất nếu lỗi nằm ở dữ liệu hoặc quy trình (Nhóm đã phối hợp với lớp 1-uiux và 3-architecture).

**Người phụ trách**: Đặng Tuấn Anh

