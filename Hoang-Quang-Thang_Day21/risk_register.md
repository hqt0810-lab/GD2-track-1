# TrustGuard — Risk Register & Kill Zone Analysis

*(Giả định: Startup có $200k trong bank, Burn rate $20k/tháng ➡️ Tổng Runway: 10 tháng)*

---

## Bước 1 & 2: Xác định 3 Risks theo công thức (If - Then - Leading to)

### 1. Vendor Risk (Rủi ro nền tảng)
- **If:** OpenAI bất ngờ cập nhật Điều khoản sử dụng (Terms of Service), cấm hoàn toàn việc dùng API của họ để "quét, giám sát và đánh giá" dữ liệu của các nền tảng AI khác.
- **Then:** Engine cốt lõi dùng để chấm điểm Trust Score của TrustGuard sẽ bị vô hiệu hóa ngay lập tức.
- **Leading to:** Mất **2 tháng runway** (do phải trả lương team dev đập đi xây lại toàn bộ bằng Llama-3 tự host, cộng thêm tiền bồi thường gián đoạn SLA cho khách hàng Pilot).

### 2. Customer-facing AI Risk (Rủi ro AI tương tác khách hàng)
- **If:** Mô hình AI chấm điểm rủi ro bị "ảo giác" (Hallucination): Bỏ sót một chuỗi API Key thật (False Negative) khiến nó lọt ra ngoài, HOẶC đánh dấu nhầm mã code sạch của dự án C-level thành PII rủi ro cao (False Positive) khiến dự án bị chặn tự động.
- **Then:** Sự cố bảo mật thực sự xảy ra hoặc quy trình Fast-track gây phẫn nộ cho ban lãnh đạo tập đoàn.
- **Leading to:** Mất **4 tháng runway** (do toàn bộ 3 tập đoàn Pilot hủy hợp đồng ngay lập tức, tốn chi phí rà soát lại toàn bộ model và sụt giảm doanh thu trầm trọng).

### 3. Founder Bandwidth Risk (Rủi ro quá tải Founder)
- **If:** Founder (người duy nhất nắm quy trình chốt Enterprise Sales và quan hệ CISO) bị ốm nặng 2 tuần hoặc phải lao vào fix critical bug cùng team dev.
- **Then:** Luồng thương thảo hợp đồng $50k với 3 tập đoàn Pilot bị đình trệ và dời sang chu kỳ ngân sách quý sau.
- **Leading to:** Mất **1 tháng runway** (do hụt dòng tiền thanh toán trả trước dự kiến trong tháng đó).

---

## Bước 3: Chấm điểm (Likelihood x Impact)

*Thang điểm 1-5. Impact được đo lường bằng số tháng runway bị mất.*

| Loại Risk | Tên Risk | Likelihood (1-5) | Impact (Tháng runway) | Score (L x I) |
| :--- | :--- | :---: | :---: | :---: |
| Vendor | OpenAI đổi Terms of Service | 2 | 2 | **4** |
| Customer-facing | AI chấm điểm sai (False Pos/Neg) | 4 | 4 | **16** |
| Bandwidth | Founder tắc nghẽn Sales | 3 | 1 | **3** |

---

## Bước 4: Vẽ Ma trận 2x2 & Xác định KILL ZONE

```text
               |
  Cao (4-5)    |                  [Customer-facing AI Risk]
               |                       (Score: 16)
I              |
M              |
P  ------------+------------------------------------------
A              |
C              |      [Vendor Risk]
T Trung/Thấp   |       (Score: 4)
  (1-3)        |
               |      [Founder Bandwidth Risk]
               |             (Score: 3)
               |__________________________________________
                  Thấp/Trung (1-3)            Cao (4-5)
                               LIKELIHOOD
```

### 🔴 Kết luận: KILL ZONE Risk
**Risk nằm trong KILL ZONE (Góc phải trên):** Rủi ro AI chấm điểm sai (False Positive / False Negative). 
Đây là rủi ro có khả năng xảy ra rất cao do bản chất của LLM, và hậu quả là tàn phá trực tiếp lòng tin của doanh nghiệp - thứ duy nhất giữ TrustGuard sống sót. 
👉 **Đưa Risk này làm ưu tiên giải quyết số 1 cho Block 3.**
