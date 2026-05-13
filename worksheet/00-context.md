---
title: 00 — Bối cảnh sản phẩm của nhóm
section: Day 25 — dùng lại cho mọi cuộc trò chuyện với AI
format: Nhóm
time: Điền 5 phút đầu buổi
---

# 00-context.md — Bối cảnh sản phẩm của nhóm

Điền file này một lần ở đầu buổi. Sau đó, mỗi lần dùng AI, hãy đưa toàn bộ nội dung file này vào đầu cuộc trò chuyện.

Lý do: AI không tự nhớ bối cảnh giữa các cuộc trò chuyện. Nếu mỗi lần đưa bối cảnh khác nhau, câu trả lời cũng sẽ lệch.

---

## 1. Sản phẩm

- **Tên sản phẩm / bot**: Trợ lý AI sàng lọc triệu chứng (Track 03)
- **Sản phẩm giúp ai làm gì**: Giúp người dùng (bệnh nhân hoặc người nhà) mô tả tình trạng sức khỏe/triệu chứng trước khi đặt lịch khám, hỗ trợ chọn loại lịch hẹn chuyên khoa phù hợp và tìm hướng dẫn tiếp theo.
- **Người dùng gặp sản phẩm ở đâu**: Website phòng khám, App đặt lịch khám, Trang "Mô tả triệu chứng", Trang "Tôi nên đặt lịch khám chuyên khoa nào?", và qua Chat trước khi gặp điều phối viên.
- **Giai đoạn hiện tại**: Đang thiết kế / thử nghiệm

---

## 2. Phạm vi

**AI được làm gì**

- Giúp người dùng mô tả triệu chứng rõ ràng hơn.
- Đặt câu hỏi phụ để làm rõ bối cảnh (ví dụ: khi người nhà khai báo thay).
- Gợi ý chuyên khoa phù hợp hoặc điều phối lịch khám.
- Đưa ra hướng dẫn tiếp theo (ví dụ: chờ, đặt lịch, tìm hỗ trợ khẩn cấp).

**AI không được làm gì**

- KHÔNG thay thế bác sĩ (không đưa ra chẩn đoán y tế).
- KHÔNG kê đơn thuốc hay chỉ định phương pháp điều trị.
- KHÔNG tự ý đưa ra kết luận về sự nguy hiểm tính mạng mà không có disclaimer hoặc hướng dẫn cấp cứu.

**Vì sao có giới hạn này**

An toàn tính mạng của bệnh nhân là rủi ro lớn nhất. AI có thể đưa ra kết luận sai, và AI không có chứng chỉ hay chuyên môn hành nghề y tế. Tuân thủ pháp lý y tế và bảo vệ tính mạng người dùng.

---

## 3. Người dùng

- **Là ai**: Bệnh nhân đa dạng độ tuổi, hoặc người nhà khai báo thông tin thay. Có thể không có kiến thức y khoa chuyên môn.
- **Họ hỏi AI khi nào**: Khi cần đặt lịch khám, khi gặp vấn đề sức khỏe ban đêm (Flow B) chưa biết có nên đi viện ngay hay không, hoặc phân vân chọn chuyên khoa.
- **Họ cần quyết định gì sau khi hỏi AI**: Nên chờ theo dõi thêm, đặt lịch khám bình thường, hay phải đi cấp cứu/tìm hỗ trợ khẩn cấp ngay.
- **Khi nào họ dễ bị tổn thương / dễ hiểu sai**: Khi đang lo lắng tột độ, đau đớn, hoặc khi sử dụng AI vào ban đêm không có người tư vấn. Dễ lầm tưởng phản hồi của AI là lời khuyên chuẩn xác của bác sĩ.
- **Họ thường tin AI đến mức nào**: Có thể tin ngay vì đang trong tâm trạng hoảng loạn hoặc mặc định "AI của phòng khám là đại diện cho bác sĩ".

---

## 4. Bối cảnh ngành

- **Sự cố tương tự đã từng xảy ra**: Chatbot y tế đưa ra lời khuyên sai khiến bệnh nhân không đi cấp cứu kịp thời (đánh giá sai mức độ nghiêm trọng của triệu chứng), hoặc AI đưa ra chẩn đoán gây hoang mang.
- **Quy định hoặc ràng buộc liên quan**: Ràng buộc bảo mật dữ liệu y tế (tuân thủ luật bảo vệ dữ liệu cá nhân sức khỏe), không vi phạm luật khám chữa bệnh (chỉ người có chứng chỉ mới được chẩn đoán).
- **Nguồn chính thức nên ưu tiên**: Hướng dẫn của bác sĩ điều phối, hotline cấp cứu của phòng khám/bệnh viện.

---

## 5. Ghi chú thêm

- Đặc biệt chú ý đến luồng **Escalation** (Leo thang): Cần ưu tiên an toàn, luôn có bước chuyển sang kênh hỗ trợ khẩn cấp nếu nhận diện các từ khóa/triệu chứng nguy hiểm.
- Khi người dùng cung cấp thông tin thiếu sót, AI cần biết hỏi thêm để hiểu ngữ cảnh.

---

## Cách dùng

```text
1. Mở công cụ AI phù hợp với bước đang làm.
2. Đưa toàn bộ nội dung file này vào đầu cuộc trò chuyện.
3. Chọn prompt tham khảo từ thư mục ../prompts/ và chỉnh lại nếu cần.
4. Đọc lại bản nháp AI tạo ra.
5. Sửa lại cho đúng bối cảnh nhóm.
6. Lưu kết quả vào đúng file trong worksheet/.
```

Ghi chú: nội dung trong `[...]` là chỗ cần điền. Sau khi điền xong, xóa dấu ngoặc nếu không cần giữ.
