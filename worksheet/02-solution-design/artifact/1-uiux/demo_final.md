---
artifact: 1 — Demo giao diện
format: phác thảo màn hình + trạng thái chính
---

# Demo giao diện

## Màn hình chính

```text
TRẠNG THÁI A — CHAT BÌNH THƯỜNG

+--------------------------------------------------------------+
| Phòng khám An Tâm                           [Chat triệu chứng]|
+--------------------------------------------------------------+
| AI có thể giúp bạn mô tả triệu chứng và chọn hướng tiếp theo.|
| AI không thay thế bác sĩ.                                    |
+--------------------------------------------------------------+
| Bạn: Tôi hơi tức ngực, hơi khó thở với tê tay một chút nhưng |
|      chắc do chạy deadline mệt mỏi. Mai tôi đặt lịch khám    |
|      tim mạch được không?                                    |
|                                                              |
| AI đang phân tích triệu chứng...                             |
+--------------------------------------------------------------+
| [ Tiếp tục mô tả triệu chứng ]                               |
+--------------------------------------------------------------+


TRẠNG THÁI B — CẢNH BÁO ĐỎ

+--------------------------------------------------------------+
| Cảnh báo khẩn cấp                                            |
+--------------------------------------------------------------+
| Các dấu hiệu "tức ngực + khó thở + tê tay/lan vai" có thể là |
| tình huống nguy hiểm. Bạn không nên chờ đến ngày mai để đặt  |
| lịch khám thường.                                            |
|                                                              |
| Đây không phải chẩn đoán. Đây là cảnh báo an toàn để bạn tìm |
| hỗ trợ y tế ngay.                                            |
+--------------------------------------------------------------+
| [ Gọi 115 ngay ]                                             |
| [ Nói chuyện với điều phối viên ]                            |
| [ Tôi không thể gọi, hãy chỉ tôi bước tiếp theo ]            |
+--------------------------------------------------------------+
| Nút "Đặt lịch thường" bị khóa trong trạng thái này.          |
+--------------------------------------------------------------+


TRẠNG THÁI C — CHUYỂN SANG NGƯỜI THẬT

+--------------------------------------------------------------+
| Kết nối điều phối viên                                       |
+--------------------------------------------------------------+
| Chúng tôi đã đánh dấu đây là tình huống cần người thật hỗ    |
| trợ. Bạn có thể:                                             |
|                                                              |
| 1. Gọi ngay số hotline phòng khám                            |
| 2. Yêu cầu nhân viên gọi lại trong 1-2 phút                  |
| 3. Xem hướng dẫn đến cơ sở y tế gần nhất                     |
+--------------------------------------------------------------+
| [ Gọi hotline ] [ Yêu cầu gọi lại ] [ Xem cơ sở gần nhất ]   |
+--------------------------------------------------------------+
```

## Các trạng thái cần minh họa

| Trạng thái | Người dùng thấy gì? | Người dùng làm gì tiếp? |
|---|---|---|
| Bình thường / chưa đủ tín hiệu đỏ | Header giải thích AI chỉ hỗ trợ sàng lọc; khung chat vẫn mở; chưa hiện cảnh báo đỏ. | Tiếp tục mô tả triệu chứng hoặc trả lời câu hỏi làm rõ. |
| Cảnh báo đỏ / AI không nên tự trả lời kiểu booking bình thường | Thẻ đỏ lớn, câu cảnh báo ngắn, khóa nút `Đặt lịch thường`, hiện CTA khẩn cấp. | Bấm `Gọi 115`, `Nói chuyện với điều phối viên`, hoặc yêu cầu bước tiếp theo nếu không thể gọi. |
| Cần chuyển sang người thật | Màn hình xác nhận đã chuyển case sang điều phối viên, có hotline và callback. | Chọn gọi hotline hoặc chờ người thật tiếp nhận. |
| Không đủ chắc để cảnh báo đỏ nhưng có rủi ro | Thẻ vàng nhắc `cần thêm thông tin trước khi đặt lịch`, chưa cho AI chốt hướng khám. | Trả lời thêm câu hỏi sàng lọc hoặc chuyển sang nhân viên nếu người dùng không chắc. |

## Ghi chú thành phần

- **Thẻ cảnh báo đỏ**: nằm ngay dưới bong bóng chat cuối cùng của AI; xuất hiện khi classifier hoặc prompt layer đánh dấu `khẩn cấp`; thay thế câu trả lời dài dòng bằng một câu ngắn, dứt khoát.
- **CTA khẩn cấp**: gồm `Gọi 115`, `Nói chuyện với điều phối viên`, `Tôi không thể gọi, hãy chỉ tôi bước tiếp theo`; đây là các hành động chính thay cho CTA booking.
- **Nút `Đặt lịch thường` bị khóa**: vẫn nhìn thấy nhưng disabled để người dùng hiểu hệ thống đang chủ động chặn flow rủi ro, không phải lỗi giao diện.
- **Nhắc giới hạn AI**: câu ngắn `AI không thay thế bác sĩ` đặt ở đầu khu vực chat và lặp lại trong trạng thái cảnh báo.
- **Trạng thái vàng**: dùng cho ca chưa đủ chắc, giúp tránh over-alert và giảm việc người dùng bị hoảng sợ không cần thiết.
