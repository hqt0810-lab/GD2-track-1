# Day 20 — Workshop 1: Ma trận RICE

## Dự án

**TrustGuard — AI Governance Control Tower cho Enterprise**

## Giả định

- Quy mô pilot ban đầu: **50 user / quý** (Bao gồm các CISO, Compliance Officer và Dev Lead tại 3-5 tập đoàn).
- Vì một số tính năng AI phân tích log phức tạp chưa chạy thực tế nhiều, chỉ số **Confidence** được giữ ở mức **50%**. Các tính năng rõ ràng về mặt kỹ thuật sẽ ở mức **80%**.
- Effort tính theo person-month (đã bao gồm buffer cho QA, Security review do đây là sản phẩm Enterprise).

---

## 1. Bảng RICE

| # | Tính năng | Reach / quý | Impact | Confidence | Effort | RICE Score | Quyết định |
|---|---|---:|---:|---:|---:|---:|---|
| 1 | Quét Log & Phát hiện Shadow AI | 50 | 3.0 | 0.8 | 1.5 | 80.0 | Quick Win / NOW |
| 2 | Chấm điểm rủi ro tự động (Trust Score) | 50 | 3.0 | 0.5 | 2.5 | 30.0 | NOW |
| 3 | Luồng phê duyệt tự động (Fast-track GO/NO-GO) | 40 | 3.0 | 0.5 | 3.0 | 20.0 | Strategic Bet / NEXT |
| 4 | Dashboard báo cáo rủi ro cho CISO | 10 | 2.0 | 0.8 | 1.0 | 16.0 | NOW |
| 5 | Phân quyền RBAC phức tạp đa tầng | 50 | 0.5 | 0.8 | 4.0 | 5.0 | Non-starter cho MVP |

---

## 2. Giải thích cách chấm

### 2.1. Quét Log & Phát hiện Shadow AI

- **Reach:** 50 user / quý (Ảnh hưởng tới toàn bộ Dev Lead và CISO)
- **Impact:** 3.0 — Tác động rất lớn (Giải quyết ngay nỗi đau "mù tịt" của CISO)
- **Confidence:** 0.8 — Technical feasible, dễ dàng kết nối qua API với LangSmith/Datadog.
- **Effort:** 1.5 person-month
- **RICE Score:** 80.0

**Lý do:**
Đây là tính năng "Aha moment" của TrustGuard. Mở app lên và thấy ngay 7 cái Shadow AI đang chạy ngầm trong công ty sẽ thuyết phục CISO mua giải pháp ngay lập tức.
**Kết luận:** Làm đầu tiên (Quick Win).

---

### 2.2. Chấm điểm rủi ro tự động (Trust Score)

- **Reach:** 50 user / quý
- **Impact:** 3.0 — Tác động rất lớn
- **Confidence:** 0.5 — Việc quét PII và độ chính xác của score cần được validate thực tế tại Enterprise.
- **Effort:** 2.5 person-month
- **RICE Score:** 30.0

**Lý do:**
Đây là core engine của sản phẩm. Không có điểm rủi ro thì không thể phân loại dự án nào an toàn, dự án nào nguy hiểm.
**Kết luận:** Đưa vào MVP, làm ngay sau phần dò tìm log.

---

### 2.3. Luồng phê duyệt tự động (Fast-track GO/NO-GO)

- **Reach:** 40 user / quý (Chủ yếu là Dev Lead submit và Compliance duyệt)
- **Impact:** 3.0 — Tác động rất lớn (Giảm 80% thời gian duyệt)
- **Confidence:** 0.5 — Cần thời gian để thay đổi thói quen và thuyết phục CISO tin vào quyết định auto của máy.
- **Effort:** 3.0 person-month
- **RICE Score:** 20.0

**Lý do:**
Đây chính là "Workflow Integration Moat" giúp TrustGuard đánh bật các tool Dashboard thông thường. Tuy nhiên, nó tốn effort khá lớn để xử lý logic rule engine cho từng công ty.
**Kết luận:** Strategic Bet, có thể làm bản rule base đơn giản trước, bản tự động hoàn toàn đưa vào NEXT.

---

### 2.4. Dashboard báo cáo rủi ro cho CISO

- **Reach:** 10 user / quý (Chỉ dành cho C-level)
- **Impact:** 2.0 — Tác động cao
- **Confidence:** 0.8 — Làm dashboard UI khá cơ bản và nắm chắc kỹ thuật.
- **Effort:** 1.0 person-month
- **RICE Score:** 16.0

**Lý do:**
Dù Reach thấp (chỉ vài ông sếp xem), nhưng đây lại là người ra quyết định mua hàng (Buyer). Họ cần một nơi để xem tổng quan sức khỏe AI của toàn tập đoàn.
**Kết luận:** Đưa vào NOW (bản đơn giản).

---

### 2.5. Phân quyền RBAC phức tạp đa tầng

- **Reach:** 50 user / quý
- **Impact:** 0.5 — Tác động thấp ở giai đoạn MVP
- **Confidence:** 0.8 — Có thể làm được nhưng mất thời gian.
- **Effort:** 4.0 person-month
- **RICE Score:** 5.0

**Lý do:**
Việc xây dựng hệ thống phân quyền phức tạp (Ai được xem project nào, phòng ban nào) là tiêu chuẩn của Enterprise SaaS, nhưng ở giai đoạn Pilot với 3 công ty đầu tiên, mọi người chủ yếu xài chung tài khoản Admin hoặc role cơ bản. 
**Kết luận:** Loại khỏi MVP, để dành khi scale (LATER).

---

## 3. Ma trận 2x2 Value-Effort

| | Effort thấp | Effort cao |
|---|---|---|
| **Value cao** | Quét Log & Phát hiện Shadow AI; Dashboard CISO | Chấm điểm Trust Score; Luồng phê duyệt tự động |
| **Value thấp** | Export file CSV báo cáo cơ bản | Phân quyền RBAC phức tạp đa tầng |

---

## 4. Quick Win

### Quét Log & Phát hiện Shadow AI
**Lý do chọn:**
- Điểm RICE cao nhất (80.0).
- Effort thấp do tái sử dụng được dữ liệu từ các nền tảng Observability có sẵn (LangSmith).
- Tạo ra giá trị ngay lập tức (Aha moment) cho khách hàng khi phơi bày được các Shadow AI lọt lưới.
**Quyết định:** Đưa vào **NOW** và làm ngay sprint đầu.

---

## 5. Strategic Bet

### Luồng phê duyệt tự động (Fast-track GO/NO-GO)
**Lý do chọn:**
- Đây là "hào nước phòng thủ" (Moat) sâu nhất của TrustGuard.
- Nó thay đổi tận gốc quy trình làm việc rườm rà của Enterprise, khiến họ không thể dứt bỏ TrustGuard một khi đã áp dụng.
- Khó thực hiện hơn nhưng giá trị mang lại về dài hạn là cực kỳ lớn.
**Quyết định:** Đưa vào **NEXT**, bắt đầu với các rule đơn giản và nâng cấp dần lên AI-driven approval.

---

## 6. Non-starter

### Phân quyền RBAC phức tạp đa tầng
**Lý do loại khỏi MVP:**
- Điểm RICE quá thấp (5.0).
- Effort khổng lồ (4 person-month) chỉ để làm hạ tầng không mang lại giá trị lõi ở giai đoạn Pilot.
- MVP chỉ cần Role Admin và Role User là đủ.
**Quyết định:** Loại bỏ khỏi MVP, chuyển xuống **LATER**.

---

## 7. Ưu tiên cuối cùng

### NOW (MVP Core)
1. Quét Log & Phát hiện Shadow AI.
2. Chấm điểm rủi ro tự động (Trust Score).
3. Dashboard báo cáo rủi ro cho CISO.

### NEXT (Moat Building)
1. Luồng phê duyệt tự động GO/NO-GO (Bản hoàn chỉnh).
2. Tích hợp cảnh báo Real-time qua Slack/Teams.

### LATER (Scale Enterprise)
1. Phân quyền RBAC phức tạp đa tầng.
2. Tự động ngắt kết nối API (Auto-block) khi rủi ro ở mức nghiêm trọng.
