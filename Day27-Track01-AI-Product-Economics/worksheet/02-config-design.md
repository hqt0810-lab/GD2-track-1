# 02 · Configuration Design — Đặt tên + Chốt knobs cho ≥3 Configs

> **Mục tiêu**: Biến phác thảo ở `01-base-flow.md` thành ≥3 configurations chi tiết, mỗi config có tên + 3 knobs đã chốt + lý do chọn.
>
> **Thời gian**: 15 phút (đầu phần Main, trước khi tính cost)

---

## Tại sao đặt tên + viết lý do?

Khi present, nhóm sẽ nói "Config 1, Config 2, Config 3" → người nghe sẽ chán ngay. Đặt tên gợi mở (Budget Bot, Premium Concierge, Smart Mix...) giúp memorable + cho thấy nhóm hiểu rõ tradeoff. Viết lý do giúp nhóm tự kiểm tra: "Mình chọn config này vì lý do gì? Có justify được không?"

---

## Cách điền

Với mỗi config: đặt tên + chốt 3 knobs + viết 2–3 câu lý do chọn. Mỗi câu lý do phải gắn với 1 tình huống thực tế (volume thấp / khách hỏi visa nhiều / budget bị siết...).

Tham khảo bảng pricing chi tiết tại `cost-reference-card.md` mục **3. Decision Points**.

---

## Config 1

**Tên config** (gợi mở: "Budget Bot", "Bare Minimum", "Lean Mode", "Night Mode" — đặt tên có cá tính):

```text
Backpacker Budget
```

### 3 Knobs

**① Model tier**:

```text
Response model: Gemini 2.5 Flash-Lite → giá $0.10 / $0.40  per 1M tokens (input/output)
Classifier model: Keyword/Regex → giá $0 / $0  per 1M tokens (hoặc keyword = $0)
```

**② Web search**:

```text
☑ OFF
□ ON selective — bật cho intent: __________________
□ ON broad
```

**③ History management**:

```text
☑ Last 3
□ Last 5
□ Full
□ Summarize every ___ turns
```

### Lý do nhóm chọn config này

Trước khi viết, tự hỏi:

- Config này phục vụ tình huống nào tốt nhất? (mùa thấp điểm? night-time? volume cao đột biến?)
- Trade-off chính là gì? (Rẻ nhưng kém chất lượng? Đắt nhưng chính xác?)
- Khách hàng nào sẽ hài lòng nhất với config này? Khách nào sẽ thất vọng?

```text
Phục vụ tình huống cần tối ưu chi phí tuyệt đối mùa khách Tây balo đông, những người chỉ hỏi nhanh đáp gọn. Chỉ trả lời dựa trên RAG với chi phí rẻ như cho.
Đánh đổi chất lượng bằng việc dễ quên yêu cầu nếu chat quá dài và có thể báo sai thông tin mới.
```

### Rủi ro lớn nhất của config này

```text
Thông tin Visa có thể outdated do tắt Web Search dẫn đến khách nhập cảnh thất bại.
```

---

## Config 2

**Tên config**:

```text
First-Class Concierge
```

### 3 Knobs

**① Model tier**:

```text
Response model: Claude Sonnet 4.6 → giá $3.00 / $15.00  per 1M tokens
Classifier model: Claude Sonnet 4.6 → giá $3.00 / $15.00  per 1M tokens (hoặc keyword)
```

**② Web search**:

```text
□ OFF
□ ON selective — bật cho intent: __________________
☑ ON broad
```

**③ History management**:

```text
□ Last 3
□ Last 5
☑ Full
□ Summarize every ___ turns
```

### Lý do nhóm chọn config này

```text
Thiết kế dành cho mùa cao điểm toàn khách VIP, ưu tiên trải nghiệm khách hàng lên hàng đầu bất chấp chi phí. Cung cấp câu trả lời cực kỳ mượt mà, sâu sắc và luôn kiểm chứng internet.
```

### Rủi ro lớn nhất của config này

```text
Cost spike lên cực kì cao nếu volume quá lớn và khách hàng cố tình nói nhảm độ dài 10-15 turns.
```

---

## Config 3

**Tên config**:

```text
Smart Navigator
```

### 3 Knobs

**① Model tier**:

```text
Response model: Mix (Sonnet 4.6 cho Visa/Weather, Flash-Lite cho Guide)
Classifier model: Claude Sonnet 4.6 → giá $3.00 / $15.00  per 1M tokens (hoặc keyword)
```

**② Web search**:

```text
□ OFF
☑ ON selective — bật cho intent: Visa, Weather
□ ON broad
```

**③ History management**:

```text
□ Last 3
☑ Last 5
□ Full
□ Summarize every ___ turns
```

### Lý do nhóm chọn config này

```text
Giải quyết bài toán ROI tối ưu nhất. Chỉ "chi tiền" xài AI xịn và Web cho những tác vụ mang tính rủi ro sai sót thông tin (Visa/Thời tiết) và tối giản chi phí cho RAG thông thường (Guide). Cân bằng hoàn hảo giữa hiệu quả và ngân sách.
```

### Rủi ro lớn nhất của config này

```text
Classifier model nhận diện sai intent sẽ dẫn đến việc chọn nhầm model (ví dụ: dùng Flash-Lite cho Visa) dẫn đến hậu quả nghiêm trọng.
```

---

## Bảng kiểm trước khi tính cost

- [x] ≥3 configs đã đặt tên (không chỉ "Config 1/2/3")
- [x] Mỗi config đã chốt rõ 3 knobs (không còn ô trống)
- [x] Mỗi config có ≥2 câu lý do
- [x] 3 configs đủ khác biệt — không phải chỉ đổi mỗi 1 knob nhỏ
- [x] Nhóm đồng thuận đây là 3 configs đáng so sánh

Xong → mở `03-cost-calculation.md` để bắt đầu tính cost.
