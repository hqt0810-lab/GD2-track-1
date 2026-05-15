# 05 · Recommendation + Justification — Kết luận & Chuẩn bị Present

> **Mục tiêu**: Chọn 1 config (hoặc combo) nhóm recommend deploy, viết justification ngắn gọn, và chuẩn bị 5 phút present.
>
> **Thời gian**: 10 phút (cuối phần Final) — Pens down lúc 12:00

---

## Bảng số ai cũng tính được. PM giỏi phải **recommend** và **justify**.

Đây là phần quan trọng nhất — phần phân biệt nhóm chỉ làm xong với nhóm thực sự hiểu sản phẩm.

---

## 4 câu hỏi nhóm phải trả lời

Mỗi câu trả lời 2–4 câu. Không lan man, không clichés. Mỗi câu phải justify được bằng số trong bảng so sánh.

### Câu 1 — Recommend config nào?

Trước khi viết, thảo luận 1 phút:

- Recommend 1 config duy nhất chạy quanh năm? Hay 2 configs khác nhau cho mùa thấp / mùa cao?
- Có nên recommend "Smart Mix model theo intent" thay vì pick 1 config cố định không?
- Nếu sếp nói "chỉ deploy 1 config thôi" — chọn cái nào?

```text
Nhóm recommend triển khai mô hình "Smart Navigator" cho toàn bộ 2 kịch bản quanh năm. Nó tối giản sự lãng phí tài nguyên của First-Class nhưng vẫn lấp đầy những lỗ hổng chết người của Budget Bot bằng logic mix-routing khôn ngoan.
```

### Câu 2 — So với human baseline $0.50/conv → tiết kiệm bao nhiêu? Có đắt hơn human ở chỗ nào không?

```text
So với human, Smart Navigator tiết kiệm quỹ lương lên tới 96.1% (Scenario A) và 91.8% (Scenario B), tương đương việc giữ lại hơn $16,500/tháng mùa cao điểm. Hoàn toàn không đắt hơn người thật, AI còn cung cấp thặng dư 24/7 và thông thạo đa ngôn ngữ mà không cần training.
```

### Câu 3 — Khi nào nên upgrade / downgrade config?

Trước khi viết, tự hỏi:

- Volume bao nhiêu thì cost AI scale lớn hơn benefit?
- Quality complaint rate bao nhiêu thì biết Budget Bot không đủ?
- Có signal nào báo nên chuyển sang Premium? (mùa cao điểm bắt đầu? customer feedback?)

```text
Chỉ nâng cấp lên First-Class nếu khách hàng phàn nàn RAG nội bộ không đủ thông tin (cần cào web cho cả Guide) hoặc doanh thu đủ lớn để lấp đầy biên lợi nhuận bị bào mòn. Chỉ downgrade xuống Budget khi công ty đói vốn và muốn cắt giảm vận hành đến mức tối thiểu ở siêu thấp điểm.
```

### Câu 4 — Rủi ro lớn nhất của config được chọn?

Trước khi viết, tự hỏi:

- Rủi ro về quality? (visa info outdated? language mismatch?)
- Rủi ro về cost? (provider tăng giá? volume spike?)
- Rủi ro về business? (khách bị bot trả lời sai → bad review → mất khách?)
- Có mitigation plan không?

```text
Rủi ro chí mạng của Smart Mix là Classifier phân loại sai Intent. Ví dụ phân nhầm câu hỏi Visa thành điểm đến, dẫn đến việc tắt bỏ kết nối Web search và đẩy cho mô hình rẻ trả lời sai luật pháp. Mitigation: Bắt buộc dùng LLM Strong để làm Classifier thay vì Regex.
```

---

## Final answer — Recommendation in 1 paragraph

Tổng hợp 4 câu trên thành 1 paragraph 5–7 câu — đây là phần nhóm sẽ đọc / chiếu khi present.

```text
Nhóm đề xuất triển khai mô hình "Smart Navigator" làm giải pháp cốt lõi cho mọi mùa du lịch vì nó cân bằng hoàn hảo giữa hiệu suất và chi phí ROI. Mức tiết kiệm đạt mốc 90% ngân sách so với thuê nhân viên thật, đồng thời vượt trội hoàn toàn về mặt rủi ro kinh doanh so với mẫu Budget nhờ khả năng cập nhật thời gian thực các chính sách Visa/Thời tiết nhạy cảm. Tuy đội ngũ kỹ sư phải vất vả cấu hình logic phân luồng phức tạp ban đầu, giá trị mà doanh nghiệp thu lại là chất lượng phục vụ tương đương một Chatbot First-Class nhưng với giá duy trì hệ thống chỉ bằng một nửa, tạo ra lợi thế cạnh tranh về biên lợi nhuận tuyệt đối trong mùa cao điểm.
```

---

## Chuẩn bị Present (5 phút)

Chia 5 phút thành 5 nhịp. 1 người trong nhóm chính phụ trách 1 nhịp. Người còn lại trả lời Q&A.

### Nhịp 0:00 – 0:30 — Base flow + 3 knobs đã chọn

Ai trình bày: Thành viên 1

Nói gì:

```text
Flow của chúng ta bắt đầu bằng LLM phân loại ý định, rẻ thì RAG, đắt thì gọi Web. Chúng ta sẽ "vặn" 3 knobs: Model Quality, Web Search Priority, và Context History để thiết kế 3 cấu hình.
```

### Nhịp 0:30 – 1:00 — Config overview

Ai trình bày: Thành viên 2

Nói gì (đọc nhanh tên + knobs 3 configs):

```text
Có 3 giải pháp: Backpacker Budget (tắt web, cực rẻ), First-Class Concierge (Bật mọi thứ, đắt) và Smart Navigator (Mix khôn khéo để tối ưu tiền).
```

### Nhịp 1:00 – 2:00 — Cost comparison

Ai trình bày: Thành viên 3

Nói gì (chiếu bảng so sánh, highlight rẻ nhất / đắt nhất):

```text
Mùa cao điểm, Budget siêu rẻ chỉ $66/tháng. Tuy nhiên, First-Class lại đốt tới $3,312/tháng. Dù thế nào, AI vẫn tiết kiệm bèo nhất là 5.4 lần so với mức 18.000 đô trả lương nhân sự thật.
```

### Nhịp 2:00 – 3:00 — Key insight

Ai trình bày: Thành viên 4

Nói gì (knob nào ảnh hưởng cost nhiều nhất + tại sao):

```text
Lựa chọn Model là lỗ đen hút chi phí, nhảy vọt 30 lần tiền nếu lên đời Claude. Thứ hai là tỷ lệ khách phàn nàn và chốt đơn, vì lúc đó AI ngừng chạy, chuyển thẳng sang Sales làm chi phí $0.
```

### Nhịp 3:00 – 4:30 — Recommendation + justification

Ai trình bày: Trưởng nhóm

Nói gì (đọc paragraph "Final answer" ở trên):

```text
Nhóm đề xuất triển khai mô hình "Smart Navigator" làm giải pháp cốt lõi cho mọi mùa du lịch vì nó cân bằng hoàn hảo giữa hiệu suất và chi phí ROI. Mức tiết kiệm đạt mốc 90% ngân sách so với thuê nhân viên thật, đồng thời vượt trội hoàn toàn về mặt rủi ro kinh doanh so với mẫu Budget nhờ khả năng cập nhật thời gian thực các chính sách Visa/Thời tiết nhạy cảm. Tuy đội ngũ kỹ sư phải vất vả cấu hình logic phân luồng phức tạp ban đầu, giá trị mà doanh nghiệp thu lại là chất lượng phục vụ tương đương một Chatbot First-Class nhưng với giá duy trì hệ thống chỉ bằng một nửa.
```

### Nhịp 4:30 – 5:00 — Hardest question prep

Ai trình bày: Toàn team

Nhóm dự đoán câu hỏi khó nhất sẽ bị hỏi là gì?

```text
Tại sao Smart Navigator chỉ lưu 5 lịch sử hội thoại? Rất nhiều khách VIP mùa cao điểm chat dài tới 10-15 lượt, họ sẽ nổi điên nếu AI quên thông tin.
```

Câu trả lời sẵn:

```text
Thống kê 85% hội thoại giải quyết xong trong vòng 4-7 lượt. Việc hy sinh rủi ro cho <15% khách hàng ngoại lai là chấp nhận được nhằm giữ cho hóa đơn API không phình to theo cấp số cộng. Nếu họ chat quá dài, thường là có ý định khiếu nại hoặc đặt tour, lúc đó AI đã bàn giao cho nhân viên thật rồi.
```

---

## Q&A — 2 phút sau khi present xong

Sẵn sàng cho 1 câu từ class + 1 câu từ instructor. Không cần lo lắng — nếu chưa biết câu trả lời, nói "đây là điểm nhóm chưa nghĩ đến — sẽ tính lại sau buổi".

**3 câu instructor thường hỏi**:

1. *"Knob nào ảnh hưởng cost nhiều nhất trong config của nhóm? Tại sao?"*
2. *"Nếu provider tăng giá API ×2 → config của nhóm còn sống được không?"*
3. *"So với nhóm X (vừa present trước) — tại sao nhóm bạn chọn khác?"*

Suy nghĩ trước câu trả lời ngắn:

```text
1. Chính là Model Generation Tier. Tăng từ rẻ lên đắt đội chi phí lên tận 30-50 lần mỗi token sinh ra.
2. Với Smart Navigator, chúng tôi xài Mix. Dù API đắt x2, chi phí nhảy từ $1,500 lên $3,000 vẫn ăn đứt mức $18,000 của nhân sự người.
3. Nhóm X chọn First-Class quá lãng phí tài nguyên cho các câu RAG vô thưởng vô phạt. Nhóm chúng tôi bảo toàn túi tiền cho công ty tốt hơn.
```

---

## Bảng kiểm cuối cùng — trước 12:00 Pens Down

- [x] Đã trả lời 4 câu PM (Recommend / Savings / Threshold / Risk)
- [x] Final answer paragraph viết gọn (5–7 câu)
- [x] Phân công 5 nhịp present cho mỗi thành viên
- [x] Có sẵn câu trả lời cho 3 câu Q&A dự đoán
- [x] Comparison table có sẵn để chiếu / chuyền tay khi present
- [x] Repo đã commit + push (sẽ nộp link sau buổi học)
