# Day 20 — Workshop 4: Dependency Map & Critical Path

Dựa vào các tính năng ưu tiên trong cột **NOW** (Quét Log Shadow AI, Chấm Trust Score, CISO Dashboard), dưới đây là bản đồ phụ thuộc và đường găng của dự án TrustGuard:

---

## 1. Top 3 External Dependencies (Rủi ro có thể giết dự án trong 30 ngày)

### Dependency 1: Quy định pháp lý Enterprise (Legal / Data Privacy)
- **Worst-case scenario:** Bộ phận Pháp chế (Legal) của tập đoàn Pilot từ chối thẳng thừng việc cho phép một công cụ bên thứ ba (TrustGuard) đọc log chứa dữ liệu nhạy cảm của nhân viên.
- **Plan B cụ thể:** Cung cấp ngay một script/SDK mã nguồn mở để khách hàng tự mã hóa (Masking) dữ liệu PII ngay trên server của họ trước khi đẩy (Push) phần log an toàn sang TrustGuard để chấm điểm.
- **Cost của Plan B:** 4 ngày dev để hoàn thiện Data Masking Script + 0$ (dùng mã nguồn mở).

### Dependency 2: Nền tảng Observability (Datadog / LangSmith) thay đổi API
- **Worst-case scenario:** Datadog đổi schema API hoặc áp mức phí quá cao cho việc pull (kéo) lượng lớn log, khiến hệ thống quét rủi ro bị đứt luồng.
- **Plan B cụ thể:** Xây dựng một Standard Log Format đơn giản và cấp Webhook URL để đội ngũ IT của khách hàng tự động đẩy log (Push) sang hệ thống TrustGuard.
- **Cost của Plan B:** 1 tuần dev dựng Webhook endpoint + Tài nguyên Server AWS khoảng $50/tháng để hứng log.

### Dependency 3: Chính sách của OpenAI / LLM API
- **Worst-case scenario:** OpenAI khóa API hoặc cấm dùng LLM của họ với mục đích "giám sát" (monitor) hệ thống AI khác.
- **Plan B cụ thể:** Sử dụng Abstraction Layer (đã viết sẵn) để gạt công tắc chuyển toàn bộ luồng quét PII sang một mô hình mã nguồn mở (như Llama-3-8B) được deploy ngay trên HuggingFace/AWS.
- **Cost của Plan B:** 2 ngày dev để setup server + $200/tháng chi phí thuê GPU Inference (VD: AWS g4dn).

---

## 2. Critical Path (Đường găng cho các task NOW)

**Danh sách 5 task chính cho NOW:**
- [Task 1]: Xin phê duyệt Legal / Privacy Policies từ CISO.
- [Task 2]: Thiết kế UI/UX Dashboard cho CISO.
- [Task 3]: Tích hợp API kết nối với Datadog/LangSmith lấy log.
- [Task 4]: Tích hợp API LLM để quét dữ liệu PII.
- [Task 5]: Xây dựng Rule Engine để chấm Trust Score tổng hợp.

**Sự phụ thuộc (Blocking):**
- [Task 1] là điều kiện tiên quyết, **block** toàn bộ [Task 3] và [Task 4].
- [Task 5] bị **block** bởi [Task 3] và [Task 4] (phải có log và kết quả quét mới chấm được điểm).
- [Task 2] (UI Dashboard) độc lập, có thể làm song song không bị block.

**Đường găng dài nhất (Critical Path):**
> **[Task 1: Legal Approval] ➡️ [Task 3: Kết nối Log] ➡️ [Task 4: Tích hợp LLM quét PII] ➡️ [Task 5: Chấm Trust Score]**

*Lưu ý: Nút thắt sinh tử nằm ở [Task 1]. Nếu Pháp chế không đồng ý, dự án sẽ đóng băng ngay lập tức ở vạch xuất phát.*
