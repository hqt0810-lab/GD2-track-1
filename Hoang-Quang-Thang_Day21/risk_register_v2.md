# TrustGuard — Risk Register v2.0 (CRO Analysis)

**Bối cảnh Startup:** Series Seed | 5 nhân sự | $200k Bank ($20k/tháng Burn rate) | **Runway: 10-12 tháng**.

---

## 1. Danh sách TOP 10 RISKS (Consolidated)

Sắp xếp theo thứ tự ưu tiên (Score = Likelihood x Impact). Impact đo bằng số tháng Runway bị mất.

| ID | Tên Risk | Loại | Likelihood | Impact | Score | Trạng thái |
| :--- | :--- | :--- | :---: | :---: | :---: | :--- |
| **R1** | **False Positive Auto-Block** | Customer | 4 | 4 | **16** | 🔴 KILL ZONE |
| **R2** | **Missed PII Leakage (False Neg)** | Customer | 3 | 5 | **15** | 🔴 KILL ZONE |
| **R3** | **Enterprise Legal Review Gridlock** | Bandwidth | 5 | 3 | **15** | 🔴 KILL ZONE |
| **R4** | **Outbound API Cost Explosion** | Vendor | 4 | 3 | **12** | 🟠 HIGH RISK |
| **R5** | **TrustGuard Data Breach** | Regulatory | 2 | 5 | **10** | 🟠 HIGH RISK |
| **R6** | **PII Middleware Failure** | Reputational | 2 | 5 | **10** | 🟠 HIGH RISK |
| **R7** | **Log Vendor API Blackout** | Vendor | 4 | 2 | **8** | 🟡 MEDIUM |
| **R8** | **EU AI Act Compliance** | Regulatory | 2 | 4 | **8** | 🟡 MEDIUM |
| **R9** | **OpenAI ToS Change** | Vendor | 3 | 2 | **6** | 🟡 MEDIUM |
| **R10** | **CTO / Key Person Absence** | Bandwidth | 3 | 1 | **3** | 🟢 LOW |

---

## 2. Deep-dive & Mitigation (Top 5 Risks)

Dưới đây là các phương án giảm thiểu rủi ro cho nhóm Kill Zone và High Risk:

### R1: False Positive Auto-Block (Score 16)
- **Vấn đề:** AI khóa nhầm API core của khách hàng do đánh giá sai rủi ro.
- **Các phương án Mitigation:**
    - A. Manual Approval Only: Chỉ gửi thông báo, chờ CISO duyệt tay.
    - B. Confidence Thresholding: Chỉ khóa khi AI tự tin > 95%.
    - C. **Allowlist/Shadow Mode (Best Pick):** Chạy ẩn 30 ngày để học pattern và lập danh sách an toàn.
- **Quyết định (Best Pick):** Triển khai **Shadow Mode**. Giúp xây dựng lòng tin và tránh gián đoạn kinh doanh của khách trong giai đoạn Pilot.

### R2: Missed PII Leakage (Score 15)
- **Vấn đề:** AI quét sót dữ liệu nhạy cảm khiến khách hàng bị lộ data thật.
- **Các phương án Mitigation:**
    - A. Multi-Model Voting: Dùng 3 model quét chéo.
    - B. **Heuristic Pre-processor (Best Pick):** Kết hợp Microsoft Presidio (Regex) + LLM.
    - C. Sampling & Human Audit: Lấy mẫu 1% log "sạch" để người kiểm tra lại.
- **Quyết định (Best Pick):** **Hybrid Approach (Presidio + LLM)**. Tận dụng tốc độ/độ chính xác của Regex cho format chuẩn và trí tuệ của LLM cho ngữ cảnh phức tạp.

### R3: Enterprise Legal Review Gridlock (Score 15)
- **Vấn đề:** Bị kẹt khâu pháp lý/bảo mật với tập đoàn khiến cạn vốn trước khi chốt deal.
- **Các phương án Mitigation:**
    - A. Standardized Trust Package: Chuẩn bị sẵn bộ hồ sơ trắng SOC2/DPA.
    - B. **Local-First Deployment (Best Pick):** Cho phép cài đặt ngay trong VPC của khách hàng.
    - C. Audit-Only Version: Bán bản thu gọn chỉ quét metadata.
- **Quyết định (Best Pick):** **Local-First Deployment**. Đây là "vũ khí" tối thượng để vượt qua 90% các câu hỏi bảo mật của phòng Pháp chế Enterprise.

### R4: Outbound API Cost Explosion (Score 12)
- **Vấn đề:** Tiền API OpenAI vượt quá doanh thu License khi volume log tăng cao.
- **Các phương án Mitigation:**
    - A. Usage-Based Pricing: Tính phí theo GB log.
    - B. **Smart Filtering (Best Pick):** Chỉ gửi 5% log "nghi vấn nhất" lên LLM.
    - C. Self-Hosted Small Models: Dùng Llama/Mistral tự host trên AWS.
- **Quyết định (Best Pick):** **Smart Filtering**. Giữ được mô hình giá trọn gói (Enterprise buyer thích) trong khi vẫn đảm bảo lợi nhuận.

### R5: TrustGuard Data Breach (Score 10)
- **Vấn đề:** Server TrustGuard bị hack làm lộ bí mật khách hàng.
- **Các phương án Mitigation:**
    - A. **Zero-Retention Policy (Best Pick):** Chấm điểm xong xóa trắng dữ liệu log.
    - B. Customer-Managed Encryption Keys: Khách hàng giữ chìa khóa mã hóa.
    - C. Anonymized Metadata: Chỉ lưu hash vô danh.
- **Quyết định (Best Pick):** **Zero-Retention**. Giải pháp an toàn nhất là không lưu trữ bất cứ thứ gì có giá trị với hacker.

---

## 3. Kết luận của CRO
TrustGuard đang đứng trước cơ hội lớn nhưng rủi ro về **"Lòng tin kỹ thuật"** và **"Bẫy pháp lý"** là rất cao. Ưu tiên hàng đầu trong Sprint tới là hoàn thiện bộ **Shadow Mode** và **Local-First Deployment** để đảm bảo sự sống còn về mặt tài chính và uy tín.
