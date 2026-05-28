# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> tôi thấy rõ là temperature càng thấp thì model càng cứng, trả lời gần như y chang nhau, rất chuẩn nhưng hơi khô. Khi tăng lên 0.5 và 1.0, câu trả lời bắt đầu linh hoạt hơn, diễn đạt đa dạng và tự nhiên hơn. Còn ở 1.5 thì model trở nên sáng tạo, đôi khi kể những chi tiết thú vị bất ngờ, nhưng cũng dễ lạc đề hoặc hơi sai sự thật.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> tôi sẽ để khoảng **0.2–0.3**. Chatbot hỗ trợ khách hàng cần sự chính xác và nhất quán cao, khách hỏi gì cũng nên trả lời rõ ràng, không bịa thêm thông tin. Temperature thấp giúp model bám sát thông tin đã có, tránh tình trạng “sáng tạo” dẫn đến trả lời sai gây hiểu lầm cho khách.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Tổng token mỗi ngày: 10.000 × 3 × 350 = 10.500.000 token (giả sử chia đều input/output: ~175.000 input + ~175.000 output mỗi lần gọi, tức ~5.25M input + 5.25M output token/ngày).

GPT-4o: (5.25 × $5.00 + 5.25 × $20.00) / 1 = $131.25/ngày
GPT-4o-mini: (5.25 × $0.15 + 5.25 × $0.60) / 1 = $3.94/ngày

GPT-4o đắt hơn GPT-4o-mini khoảng 33 lần với cùng workload này.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> GPT-4o xứng đáng với chi phí cao hơn khi ứng dụng yêu cầu lý luận phức tạp, ví dụ như phân tích hợp đồng pháp lý hoặc tư vấn y tế — nơi mà độ chính xác và khả năng suy luận sâu trực tiếp ảnh hưởng đến quyết định quan trọng. Ngược lại, GPT-4o-mini là lựa chọn tốt hơn cho các tác vụ đơn giản như phân loại email, trả lời FAQ, hay tóm tắt văn bản ngắn — những việc không đòi hỏi năng lực cao nhưng cần xử lý khối lượng lớn với chi phí tối ưu.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming rất quan trọng khi người dùng đang chờ phản hồi trực tiếp, đặc biệt với câu trả lời dài như viết bài, giải thích chi tiết hay trò chuyện. Việc hiện từng chữ một sẽ làm người dùng cảm thấy nhanh hơn, không bị “treo” màn hình khó chịu. Ngược lại, non-streaming phù hợp hơn khi cần xử lý xong toàn bộ mới trả kết quả, ví dụ: trả về JSON để hệ thống khác đọc, phân tích dữ liệu batch, hay các tác vụ chạy ngầm không có người dùng chờ trực tiếp.


## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
