# TrustGuard — Rules, Rails, Rituals (R3 Framework)

**Risk lớn nhất của startup:** Nhân viên hoặc hệ thống TrustGuard vô tình gửi nguyên bản log dữ liệu của khách hàng Enterprise (chứa thông tin PII như tên, email, số thẻ tín dụng) sang các Public LLM API (OpenAI, Anthropic) để phân tích, dẫn đến vi phạm nghiêm trọng thỏa thuận bảo mật dữ liệu (Data Breach) và giết chết startup ngay lập tức.

---

### R1 — RULES (Quy định)
1. **Cấm cụ thể:** NGHIÊM CẤM gửi nguyên bản (raw data) bất kỳ log/payload nào của khách hàng sang các public API (OpenAI, Anthropic, Gemini, v.v.). Mọi API call liên quan đến data khách hàng không được phép bypass qua middleware bảo mật.
2. **Allowed alternative:** BẮT BUỘC sử dụng công cụ Internal PII Masking (được dựng sẵn trên server nội bộ) để mã hóa toàn bộ dữ liệu nhạy cảm trước khi gọi API ngoài. Đối với dữ liệu phân loại tuyệt mật (Tier 1), chỉ được dùng mô hình Open-source tự host (Llama 3, Cost: ~$150/tháng tiền GPU).
3. **Hậu quả vi phạm:** Vi phạm lần 1 -> Thu hồi quyền truy cập Database + Founder nói chuyện trực tiếp cảnh cáo. Vi phạm lần 2 (hoặc cố tình bypass) -> Buộc thôi việc (Let go) ngay lập tức và chịu trách nhiệm pháp lý.
4. **Update mechanism:** Quy trình code, danh sách các Public API được phép sử dụng và bộ từ điển PII luôn được cập nhật tại trang `[Engineering / Data Privacy Policy]` trên Notion nội bộ của công ty.

---

### R2 — RAILS (Công cụ tự động chặn)
1. **Công cụ 1: Microsoft Presidio (Middleware PII Anonymizer)**
   - **Tác dụng:** Chạy dưới dạng một chốt chặn độc lập (middleware) trước cổng outbound API. Mọi request gửi từ server TrustGuard ra OpenAI đều đi qua đây. Nếu phát hiện text chứa email/phone/credit card, nó tự động thay bằng chuỗi `[MASKED]` rồi mới cho đi tiếp.
   - **Cost:** $0 (Open-source) + $40/tháng chi phí server AWS ECS để chạy độc lập.
2. **Công cụ 2: GitGuardian (CI/CD Scanner)**
   - **Tác dụng:** Tích hợp trực tiếp vào GitHub. Nếu phát hiện bất kỳ dòng code nào (Pull Request) cố tình gọi thẳng API của OpenAI mà không import cái thư viện PII Masking nội bộ, hệ thống CI/CD sẽ báo đỏ (Fail) và block không cho merge code vào nhánh chính.
   - **Cost:** ~$50/user/tháng -> Tổng $250/tháng (cho team 5 devs).

---

### R3 — RITUAL (Thói quen vận hành)
- **Ritual hàng tuần:** Trong buổi Weekly Sync 15 phút sáng thứ Hai, Tech Lead sẽ mở Dashboard log của cổng outbound (hoặc bảng báo cáo của GitGuardian) để review *"Top các request chứa PII bị chặn lại"* của tuần trước, xem có mẫu dữ liệu nào mới lọt lưới hoặc bị đánh dấu nhầm (false positive) không.
- **Câu hỏi của Founder (dành cho Dev Lead):** *"Tuần vừa rồi hệ thống Rails của chúng ta đã tự động chặn được bao nhiêu request chứa dữ liệu nhạy cảm suýt bị gửi ra ngoài, và nguyên nhân gốc rễ là do đâu?"*

---

### Self-check 
- **Tổng cost Rails:** $40 + $250 = **$290/tháng** (Pass yêu cầu < $500/tháng).
- **Ritual implement:** Phân quyền GitGuardian và họp 15p đầu tuần hoàn toàn triển khai được ngay lập tức trong 1 tuần (Pass).
