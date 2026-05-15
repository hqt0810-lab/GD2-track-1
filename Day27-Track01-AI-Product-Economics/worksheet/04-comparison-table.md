# 04 · Comparison Table — Bảng so sánh đầy đủ

> **Mục tiêu**: Tổng hợp tất cả số đã tính ở `03-cost-calculation.md` thành 1 bảng so sánh duy nhất — đây là artifact chính nhóm sẽ present.
>
> **Thời gian**: 10 phút (đầu phần Final)

---

## Vì sao có bảng so sánh?

Khi sếp hỏi "Nên deploy config nào?", bạn cần đặt lên bàn **1 bảng** thay vì đọc 3 báo cáo riêng. Bảng so sánh đầy đủ cho phép so sánh thẳng từng dòng, dễ nhìn ra tradeoff.

---

## Bảng chính

Điền số đã tính. Số nào chưa có → quay lại `03-cost-calculation.md` tính cho xong.

| | Config 1 | Config 2 | Config 3 |
|---|---|---|---|
| **Tên** | Backpacker Budget | First-Class Concierge | Smart Navigator |
| **① Model** | Flash-Lite | Sonnet 4.6 | Mix (Sonnet+Lite) |
| **② Web search** | OFF | ON Broad | ON Selective |
| **③ History** | Last 3 | Full | Last 5 |
| **Intent classifier** | Keyword | LLM | LLM |
| **Cost / conv (Scenario A — 4 turns)** | $0.00084 | $0.0477 | $0.0192 |
| **Cost / conv (Scenario B — 7 turns)** | $0.00184 | $0.0920 | $0.0408 |
| **Monthly A** (300 conv/day × 30) | $7.56 | $429.30 | $172.80 |
| **Monthly B** (1,200 conv/day × 30) | $66.24 | $3,312.00 | $1,468.80 |
| **vs human $4,500/mo (A)** | rẻ 595× | rẻ 10.4× | rẻ 26× |
| **vs human $18,000/mo (B)** | rẻ 271× | rẻ 5.4× | rẻ 12.2× |
| **Savings % (A)** | 99.8% | 90.4% | 96.1% |
| **Savings % (B)** | 99.6% | 81.6% | 91.8% |
| **Quality estimate** | Low | High | High |
| **Speed estimate** | High | Low | Med |
| **Điểm yếu chính** | Sai lệch thông tin thực tế | Ngốn ngân sách khi volume tăng | Rủi ro sai Intent classifier |
| **Best for** (khi nào nên dùng) | Chống cháy mùa thấp điểm | Khách sạn/Hãng bay 5 sao | Hầu hết doanh nghiệp lữ hành |

---

## Quan sát nhanh từ bảng

Trước khi sang file recommendation, trả lời 4 câu — đây là material để present:

### Câu 1 — Config rẻ nhất là gì? Đắt nhất là gì?

```text
Rẻ nhất: Backpacker Budget — monthly B = $66.24
Đắt nhất: First-Class Concierge — monthly B = $3,312.00
Chênh: 50× lần
```

### Câu 2 — Knob nào ảnh hưởng cost nhiều nhất?

So sánh các config khác nhau ở knob nào, chênh bao nhiêu. Thường: model tier > history > web search.

```text
Đổi từ Flash-Lite lên Sonnet 4.6 (Model Knob) làm giá tăng 30 lần, đây là nguyên nhân chính gây phình cost. Knob History Full cũng kéo dãn khoảng cách ở Scenario B.
```

### Câu 3 — Tại sao Scenario B không đắt ×4 lần Scenario A?

Volume Scenario B = ×4 lần Scenario A. Turns dài hơn (7 vs 4 = ×1.75). Mong đợi monthly B ≈ A × 7. Thực tế có thể thấp hơn vì sao?

Trước khi viết, nghĩ: intent mix Scenario B có gì khác? Booking + Complaint = $0 LLM ở scenario B là bao nhiêu %?

```text
Hội thoại tuy dài hơn (7 vs 4 lượt) khiến token context cộng dồn, nhưng Scenario B lại có tỷ lệ Booking + Complaint lên tới 45% (Handoff = $0 LLM) thay vì 15% ở kịch bản A. Lượng handoff khổng lồ này giúp kìm hãm đà tăng phi mã của LLM cost.
```

### Câu 4 — Có config nào AI đắt hơn human không?

So sánh monthly từng config với human baseline ($4,500 cho A, $18,000 cho B). Nếu AI rẻ hơn → savings %. Nếu đắt hơn → cần justify.

```text
Hoàn toàn không. Ngay cả config đắt nhất First-Class vẫn rẻ hơn nhân viên người thật 5-10 lần. AI mang lại sự tiết kiệm khủng khiếp và khả năng phục vụ không giới hạn giờ giấc.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Bảng đầy đủ — không còn ô trống
- [x] Đã có 4 câu trả lời cho 4 quan sát ở trên
- [x] Nhóm đồng thuận về số trong bảng (đã sanity check)

Xong → mở `05-recommendation.md` để viết recommendation cuối + chuẩn bị present.
