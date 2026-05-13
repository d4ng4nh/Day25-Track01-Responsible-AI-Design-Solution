---
artifact: 3 — Lớp kiến trúc dữ liệu
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp kiến trúc dữ liệu

**Tình huống xử lý**: T-01  
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Thêm một lớp **Red-Flag Safety Router** trước khi chatbot đi vào luồng AI trả lời hoặc đặt lịch. Router này kiểm tra input của người dùng để phát hiện cụm triệu chứng nguy hiểm như “tức ngực”, “khó thở”, “tê tay”, đặc biệt khi user tự giảm nhẹ là “do mệt” hoặc muốn đặt lịch ngày mai.

Nếu phát hiện red flag, hệ thống không cho tiếp tục luồng đặt lịch thông thường. Thay vào đó, hệ thống trả về mẫu hướng dẫn an toàn đã chuẩn bị trước: khuyến nghị gọi cấp cứu, đến cơ sở y tế gần nhất, hoặc liên hệ nhân viên y tế trực.

---

## 2. Vì sao sửa ở lớp kiến trúc dữ liệu?

Rủi ro T-01 xảy ra vì hệ thống có thể phụ thuộc quá nhiều vào LLM để tự phân loại mức độ nguy hiểm. LLM có thể bị “neo” theo lời tự chẩn đoán của user như “chắc do chạy deadline mệt”, rồi tiếp tục hỗ trợ đặt lịch thay vì cảnh báo khẩn cấp.

Sửa ở lớp kiến trúc giúp tạo một lớp chặn độc lập với LLM. Trước khi AI sinh câu trả lời, hệ thống đã kiểm tra cụm triệu chứng nguy hiểm và quyết định có cần chuyển sang luồng khẩn cấp hay không.

**Hành động phòng vệ chính**:

- [x] Ngăn lỗi bằng bước kiểm tra red-flag trước khi AI trả lời
- [x] Phát hiện khi input có cụm triệu chứng rủi ro cao
- [x] Khắc phục bằng cách chuyển sang kênh y tế / người thật khi cần
- [x] Ghi lại lỗi để cải thiện sau

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo cần có:

- Sơ đồ cách dữ liệu đi qua hệ thống
- Bước kiểm tra trước khi AI trả lời
- Cách xử lý khi phát hiện red flag
- Cách xử lý khi không phát hiện red flag rõ ràng
- Cách ghi lại hoặc theo dõi lỗi

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

| Tác dụng phụ | Vì sao có thể xảy ra | Cách giảm |
|---|---|---|
| Báo động nhầm | User nhắc đến từ khóa như “khó thở” nhưng không ở tình huống cấp tính | Chỉ kích hoạt mạnh khi có cụm nhiều triệu chứng cùng lúc hoặc có dấu hiệu thời gian như “đang”, “từ tối qua”, “vừa bị” |
| Bỏ sót red flag | User dùng từ đời thường hoặc viết sai chính tả như “nặng ngực”, “ngộp thở”, “tay trái lạ lạ” | Mở rộng danh sách từ đồng nghĩa từ test set và log lỗi |
| User khó chịu vì không đặt lịch được ngay | Hệ thống ưu tiên an toàn nên chặn luồng đặt lịch thường | Câu cảnh báo phải ngắn, rõ lý do, và đưa lựa chọn hành động tiếp theo |
| Không có nhân viên trực | User dùng ngoài giờ hành chính | Luôn có fallback: gọi cấp cứu hoặc đến cơ sở y tế gần nhất |

**Nhóm giảm vấn đề đó bằng cách nào?**

Nhóm chỉ áp dụng router này cho nhóm triệu chứng rủi ro cao. Các câu hỏi thông thường vẫn đi qua luồng chatbot bình thường. Với các case bị router chặn, hệ thống ghi log để nhóm review và điều chỉnh rule sau.

---

## 5. Checklist trước khi nộp

- [x] Sơ đồ cho thấy dữ liệu đi từ đâu đến đâu.
- [x] Có bước kiểm tra nguồn/rủi ro trước khi AI trả lời.
- [x] Có cách xử lý khi không đủ an toàn để AI tự trả lời.
- [x] Có cách chuyển sang người thật với tình huống rủi ro cao.
- [x] Có cách biết lỗi này có đang lặp lại không.

**Người phụ trách**: Dương Khoa Điềm