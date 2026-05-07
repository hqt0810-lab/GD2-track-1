# TrustGuard — Incident Playbook (Quy trình xử lý sự cố khẩn cấp)

**Tình huống (Đã điều chỉnh cho TrustGuard):** *9h30 sáng. CISO của một tập đoàn Pilot tweet screenshot: AI TrustGuard vừa "nhìn nhầm" toàn bộ source code dự án bán hàng lõi của họ thành dữ liệu chứa PII (False Positive) và TỰ ĐỘNG KHÓA (Auto-block) sạch API, làm sập toàn bộ hệ thống bán hàng của tập đoàn. Bài đăng có 200 retweets từ giới tech C-level trong 30 phút, đang viral.*

---

## Bước 1: Verify (Xác minh sự cố - 3 phút)

**Hành động ngay lập tức (Không hoảng loạn):**
1. **Check log ở đâu?** 
   - Không check OpenAI dashboard vì quá nhiều nhiễu. Mở ngay **LangSmith** (hoặc Datadog) bằng tài khoản Admin. 
   - Lọc tag `customer_id` và `action = auto-block` trong khung giờ 9h00 - 9h30 sáng nay.
   - **Lý do chọn:** OpenAI dashboard chỉ chứa log token thô, không có ngữ cảnh nghiệp vụ. LangSmith/Datadog lưu giữ toàn bộ context (ai gọi, input/output chính xác là gì) giúp khoanh vùng lỗi hệ thống chỉ trong vài giây.
2. **Cách verify nhanh AI thật hay Photoshop?**
   - Nhìn vào màn hình screenshot của khách hàng trên Twitter, tìm mã `Alert_ID` hoặc Timestamp. 
   - Query trực tiếp vào AWS RDS Database (`SELECT * FROM trust_score_history WHERE alert_id = ...`). Nếu prompt và response trong DB khớp 100% với ảnh -> Lỗi do AI TrustGuard thật sự (Hallucination), không phải bịa đặt.
   - **Lý do chọn:** Cung cấp bằng chứng kỹ thuật xác thực 100%, loại bỏ ngay kịch bản bị đối thủ dùng thủ thuật chỉnh ảnh (Photoshop) bôi nhọ, giúp Founder ra quyết định xin lỗi hay đính chính một cách dứt khoát.

---

## Bước 2: Stop the Bleeding (Cầm máu - 5 phút)

**Quyết định:** Chọn **SOFT DOWNGRADE (Chuyển sang chế độ Alert-Only)**.

**Lý do:** 
- Tuyệt đối không chọn *Hard Shutdown* (Tắt sạch TrustGuard) vì CISO vẫn cần nhìn thấy Dashboard để an tâm.
- Không chọn *Tighten* (Chỉnh lại prompt LLM ngay lúc đó) vì sửa vội LLM lúc đang hoảng loạn dễ gây ra lỗi dây chuyền khác.
- Việc gạt công tắc tắt tính năng "Auto-block" (chỉ gửi cảnh báo qua Slack, không khóa API) giúp hệ thống bán hàng của khách hàng lập tức thông luồng trở lại, giảm thiểu thiệt hại kinh doanh tính bằng phút, cho ta thời gian thở để điều tra.

---

## Bước 3: Customer Communication (Liên lạc trực tiếp - 5 phút)

**Gửi Direct Message (DM) / Tin nhắn Zalo trực tiếp cho CISO:**

> "Hi anh [Tên khách hàng], em Thắng - Founder TrustGuard đây ạ. 
> Em vừa xác nhận hệ thống AI bên em đã nhận diện nhầm PII và tự động khóa nhầm API dự án bên anh sáng nay. Em thành thật xin lỗi vì sự cố nghiêm trọng này. 
> 
> Bọn em vừa gạt công tắc chuyển toàn bộ hệ thống sang chế độ "Chỉ cảnh báo" (Alert-Only), luồng API của bên anh đã được mở lại bình thường cách đây 1 phút. 
> 
> "Để đền bù thiệt hại gián đoạn, TrustGuard sẽ hoàn 100% phí license tháng này cho bên anh. Đồng thời, từ giờ em sẽ hard-code thêm một lớp "Whitelist" để các dự án lõi của bên anh không bao giờ bị auto-block nữa. Em sẽ gửi post-mortem chi tiết nguyên nhân kỹ thuật cho anh trong 2 tiếng tới. Một lần nữa em rất xin lỗi anh và team."

**Lý do chọn cách Comm này:**
- **Founder personal voice:** Đích thân Founder nhắn tin nhận lỗi thể hiện sự tôn trọng tuyệt đối với C-level, thay vì đẩy trách nhiệm giải quyết cho bộ phận CS (Customer Support).
- **Tập trung vào giải pháp & Specific compensation:** Việc hoàn tiền ngay lập tức và hứa bổ sung tính năng "Whitelist" (đúng pain point) ở tin nhắn đầu tiên giúp dập tắt sự phẫn nộ tức thời của khách hàng.

## Bước 4: Public Response (Xử lý truyền thông - 2 phút)

**Đăng tải Tweet (Dưới 280 ký tự):**

> "Sáng nay TrustGuard gặp sự cố False Positive, dẫn đến khóa nhầm API của 1 khách hàng Pilot. Chúng tôi đã lập tức tắt tính năng Auto-block trên toàn hệ thống để các luồng dev hoạt động bình thường. Thành thật xin lỗi team bị ảnh hưởng. Post-mortem kỹ thuật sẽ có sau 24h."

**Lý do chọn cách phản hồi này:**
- **Nhận lỗi nhanh - Không bao biện:** Trong 30 phút đầu của đợt viral, công chúng (đặc biệt là giới Tech) rất dị ứng với việc startup vòng vo hay đổ lỗi cho "bên thứ ba" (OpenAI). Việc dũng cảm nhận lỗi, chứng minh hành động "đã tắt Auto-block" cho thấy startup vẫn hoàn toàn làm chủ hệ thống, biến một cuộc khủng hoảng thành cơ hội ghi điểm về sự minh bạch.
