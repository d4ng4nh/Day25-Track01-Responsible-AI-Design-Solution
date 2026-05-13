---
artifact: 1 — Lớp giao diện
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo_final.md
---

# Lớp giao diện

**Tình huống xử lý**: T-01

## Giải pháp

Khi người dùng mô tả cụm triệu chứng có thể là red flag tim mạch như `đau ngực + khó thở + tê tay/lan vai`, giao diện không hiển thị câu trả lời AI như một đoạn chat bình thường nữa. Thay vào đó, màn hình chuyển sang trạng thái cảnh báo khẩn: thẻ đỏ nổi bật, câu khuyến nghị ngắn và dứt khoát, khóa nút `Đặt lịch thường`, và thay bằng hai hành động chính là `Gọi cấp cứu 115` và `Nói chuyện với điều phối viên ngay`.

Giải pháp này nhằm cắt khoảnh khắc người dùng dễ tin luôn câu trả lời của AI và tiếp tục đặt lịch hôm sau. Nếu mô hình vẫn lỡ trả lời chưa đủ mạnh, lớp giao diện vẫn đóng vai trò chặn cuối để không cho luồng booking bình thường tiếp diễn.

## Vì sao sửa ở lớp giao diện

- Người dùng rất dễ tin câu trả lời của AI quá mức vì bot nằm trong website/app chính thức của phòng khám.
- Rủi ro xảy ra đúng ở khoảnh khắc người dùng đọc phản hồi và quyết định `chờ đến mai` hay `đi ngay`.
- Nếu lớp prompt hoặc dữ liệu vẫn sót lỗi, giao diện là lớp chặn cuối để không cho user tiếp tục flow nguy hiểm.

## Hành động phòng vệ chính

- Thông báo rõ giới hạn: AI không thay thế bác sĩ.
- Chuyển người thật khi cần: hiện ngay CTA sang điều phối viên.
- Chặn hành động rủi ro: khóa `Đặt lịch thường` trong trạng thái khẩn cấp.

## Demo

Xem file: [demo_final.md](demo_final.md)

Demo thể hiện 3 trạng thái chính:

- Trạng thái bình thường khi user mới nhập triệu chứng.
- Trạng thái cảnh báo đỏ khi AI nhận diện red flag tim mạch.
- Trạng thái chuyển sang người thật với hotline, callback, và cơ sở y tế gần nhất.

## Tác dụng phụ và cách giảm

Vấn đề có thể phát sinh:

- Người dùng thấy bị chặn quá sớm vì chỉ muốn đặt lịch nhanh.
- Cảnh báo đỏ có thể làm user hoảng sợ nếu kích hoạt quá rộng.
- Khóa nút booking có thể làm giảm conversion của luồng đặt lịch.

Cách giảm:

- Chỉ bật trạng thái đỏ khi có cụm red flag rõ hoặc classifier đánh dấu `khẩn cấp`.
- Dùng câu chữ ngắn, trực tiếp, không dọa nạt và không nhồi thuật ngữ y khoa.
- Vẫn cho user một lối đi rõ ràng: `Gọi 115`, `Nói chuyện với điều phối viên`, hoặc `Tôi không thể gọi, hãy chỉ tôi bước tiếp theo`.
- Với ca chưa đủ chắc, dùng trạng thái vàng thay vì đỏ để tránh over-alert.

**Người phụ trách**: Nguyễn Tuấn Khanh
