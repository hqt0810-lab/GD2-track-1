# 03 · Cost Calculation — Tính chi phí từng Config × 2 Scenarios

> **Mục tiêu**: Với mỗi config đã thiết kế ở `02-config-design.md`, tính cost/turn → cost/conversation → monthly cho cả 2 scenarios (low season + high season).
>
> **Thời gian**: 55 phút (phần lớn của Main phase) — checkpoint 11:00 và 11:20

---

## Cách làm

**Đừng tính tay từng turn — đó là cách thừa thời gian.** Dùng AI để tính. Dán prompt template từ `prompts/01-cost-calc.md` vào ChatGPT/Claude/Gemini, thay parameters theo config của nhóm, AI sẽ tính cho.

Tuy nhiên nhóm phải **hiểu** kết quả AI trả về, không phải copy-paste mù. Mỗi lần AI trả số, nhóm phải tự kiểm 1 lần: con số này có hợp lý không? Có vẻ quá đắt hay quá rẻ?

---

## Trước khi gọi AI — Setup chung

**Các tham số cố định cho tất cả configs** (tham khảo `cost-reference-card.md` mục 4):

```text
System prompt:              500 tokens
User message:                80 tokens
Assistant response:         180 tokens (output)
1 prior turn (history):     260 tokens (80 user + 180 assistant)
RAG top-5 chunks:         1,250 tokens (cố định)
Web search results:         800 tokens (khi bật)
Web search API call:       $0.008 / call (Tavily)
LLM classifier:            ~170 tokens (150 in + 20 out) — nếu dùng
```

**Scenario A — mùa thấp điểm**:

```text
Volume:            300 conversations / ngày
Turns/conv:        avg 4 lượt
Intent mix:        Guide 50%, Visa 25%, Weather 10%, Booking 10%, Complaint 5%
AI-served ratio:   85% (15% là Booking + Complaint = handoff)
```

**Scenario B — mùa cao điểm**:

```text
Volume:           1,200 conversations / ngày (×4)
Turns/conv:        avg 7 lượt
Intent mix:        Guide 30%, Visa 15%, Weather 10%, Booking 35%, Complaint 10%
AI-served ratio:   55% (45% là handoff)
```

**Human baseline để so sánh**: $0.50 / conversation cố định.

---

## Quy trình tính cho 1 config (lặp lại cho từng config)
*(Đã sử dụng AI để mô phỏng và tính toán)*

---

## Điền số cho từng config

Dùng AI tính xong, copy số vào đây. Đừng quên kiểm 1 lần xem số có hợp lý không.

### Config 1 — Backpacker Budget

| Item | Scenario A (4 turns) | Scenario B (7 turns) |
|---|---|---|
| Cost / conversation (avg) | $0.00084 | $0.00184 |
| Monthly cost | $7.56 | $66.24 |
| Human baseline | $4,500 | $18,000 |
| **Rẻ hơn human ___×** | 595× | 271× |
| **Savings %** | 99.8% | 99.6% |

**Sanity check** (trả lời cho nhóm trước khi đi tiếp):

- Cost/conv có nằm trong $0.005–$0.10 không? Nếu quá thấp → có thể quên component (RAG? web? classifier?). Nếu quá cao → có thể tính sai history.
- Monthly có hợp lý không? (cheap config thường $100–$300, premium config có thể đến $3,000+)

```text
Có vẻ hoàn toàn hợp lý, chi phí cực thấp chưa tới $100/tháng cho cả mùa cao điểm do dùng model rẻ Flash-Lite và cắt bỏ hoàn toàn web search API đắt đỏ.
```

---

### Config 2 — First-Class Concierge

| Item | Scenario A | Scenario B |
|---|---|---|
| Cost / conversation (avg) | $0.0477 | $0.0920 |
| Monthly cost | $429.30 | $3,312.00 |
| **Rẻ hơn human ___×** | 10.4× | 5.4× |
| **Savings %** | 90.4% | 81.6% |

**Sanity check**:

```text
Scenario B tốn hơn 3 nghìn đô vì model Sonnet đắt gấp 30 lần Flash-Lite, cộng thêm Web search gọi liên tục và token từ lịch sử hội thoại 7 turns. Dù vậy vẫn tiết kiệm >80% so với nhân sự thực.
```

---

### Config 3 — Smart Navigator

| Item | Scenario A | Scenario B |
|---|---|---|
| Cost / conversation (avg) | $0.0192 | $0.0408 |
| Monthly cost | $172.80 | $1,468.80 |
| **Rẻ hơn human ___×** | 26× | 12.2× |
| **Savings %** | 96.1% | 91.8% |

**Sanity check**:

```text
Mix model giúp chi phí giảm phân nửa so với First-Class, mức giá < $1500 cho mùa cao điểm 36,000 lượt chat là cực kỳ lý tưởng về bài toán ROI mà vẫn đáp ứng được nhu cầu thực chiến khó nhất.
```

---

## Quality + Speed estimate (qualitative)

Mỗi config — estimate Low / Medium / High. Không có công cụ đo chính xác trong lab, ước tính dựa trên model tier + web search + history.

| Config | Quality (Low/Med/High) | Speed (Low/Med/High) | Lý do |
|---|---|---|---|
| 1: Budget | Low | High | Phản hồi siêu tốc nhưng nguy cơ sai thông tin rất lớn do không kết nối web. |
| 2: Premium | High | Low | Câu trả lời hoàn hảo, nhưng tốc độ chậm đi 1-2s do độ trễ model lớn và phải cào dữ liệu web liên tục. |
| 3: Smart Mix | High | Med | Cân bằng tuyệt vời vì chỉ gọi web vài case cần thiết, chất lượng mấu chốt vẫn đảm bảo ở mức cao. |

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Tất cả ≥3 configs đã có cost/conv + monthly cho cả 2 scenarios
- [x] Đã so sánh từng config với human baseline ($0.50/conv)
- [x] Có quality + speed estimate cho mỗi config
- [x] Đã sanity check — không có số "quá lạ" (cost <$0.001 hoặc >$1/conv)

Xong → mở `04-comparison-table.md`.
