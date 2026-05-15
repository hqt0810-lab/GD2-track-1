# Prompt 01 — Tính Cost cho 1 Conversation Chatbot

> **Dùng khi**: Bước 1 của `worksheet/03-cost-calculation.md` — sau khi đã chốt config (3 knobs + intent classifier), nhóm cần tính cost/turn → cost/conv → monthly. Dùng prompt này để AI tính giúp thay vì tính tay từng số.
>
> **Công cụ gợi ý**: ChatGPT, Claude, Gemini — bất kỳ AI nào hỗ trợ markdown table tốt.

---

## Trước khi dán prompt — 5 câu nhóm tự trả lời

Dán prompt mù không cho kết quả tốt. Trước khi gọi AI, nhóm tự trả lời:

1. Config nào nhóm đang tính (đã có ở `02-config-design.md`)?
2. Generation model nào + giá $/M tokens (xem `cost-reference-card.md` mục 3)?
3. Web search bật cho intent nào (không bật nghĩa là tắt hoàn toàn)?
4. History strategy là gì (Last 3 / Last 5 / Full / Summarize)?
5. Classifier dùng keyword ($0) hay LLM (~170 tokens × cheap model)?

Nếu chưa rõ câu nào → quay lại `02-config-design.md` chốt trước.

---

## Câu lệnh đã điền — 3 configs từ `02-config-design.md`

> Dưới đây là prompt đã điền sẵn cho 3 config. Copy paste vào ChatGPT/Claude/Gemini. Mỗi config cần chạy 6–7 lần (thay intent × scenario) — xem bảng ở mục "Lặp lại cho từng intent".

### Config 1: Backpacker Budget — Scenario A (Guide × 4 turns)

````text
Tôi đang thiết kế chatbot AI cho travel agency Việt Nam phục vụ khách quốc tế.
Giúp tôi tính chi phí cho 1 conversation theo config sau:

## Config

- Tên config: Backpacker Budget
- Generation model: Gemini 2.5 Flash-Lite — giá $0.10/M input, $0.40/M output
- Classifier: keyword/regex = $0
- Web search: OFF
- History: Last 3

## Tham số cố định (giống cho mọi config)

- System prompt: 500 tokens
- User message: 80 tokens
- Assistant response: 180 tokens output
- 1 prior turn history: 260 tokens (80 user + 180 assistant)
- RAG top-5 chunks: 1,250 tokens
- Web search results: 800 tokens (khi bật)
- Web search API: $0.008/query
- LLM classifier (nếu dùng): ~170 tokens (150 in + 20 out)

## Conversation scenario tôi cần tính

Tính cost cho 1 conversation với:

- Số turn: 4 (Scenario A — mùa thấp điểm)
- Intent của conversation: Guide/Destination
- Web search được trigger ở turns nào: không bật (OFF toàn bộ)

## Yêu cầu output

1. **Bảng cost per turn** — mỗi turn 1 hàng, cột: History tokens, Input total, Output tokens, Cost model, Cost web API, Cost classifier, Total/turn.
2. **Tổng cost/conversation** — sum của tất cả turns.
3. **Show công thức từng bước** — không chỉ ra số, ghi rõ "input = 500 + 780 + 1,250 + 80 = 2,610" để tôi check.
4. **So sánh với human baseline** ($0.50/conv) — AI rẻ hơn bao nhiêu lần?
````

### Config 2: First-Class Concierge — Scenario B (Visa × 7 turns)

````text
Tôi đang thiết kế chatbot AI cho travel agency Việt Nam phục vụ khách quốc tế.
Giúp tôi tính chi phí cho 1 conversation theo config sau:

## Config

- Tên config: First-Class Concierge
- Generation model: Claude Sonnet 4.6 — giá $3.00/M input, $15.00/M output
- Classifier: LLM model: Claude Sonnet 4.6 — $3.00/M input, $15.00/M output (~170 tokens/call)
- Web search: ON broad (bật cho tất cả intent)
- History: Full

## Tham số cố định (giống cho mọi config)

- System prompt: 500 tokens
- User message: 80 tokens
- Assistant response: 180 tokens output
- 1 prior turn history: 260 tokens (80 user + 180 assistant)
- RAG top-5 chunks: 1,250 tokens
- Web search results: 800 tokens (khi bật)
- Web search API: $0.008/query
- LLM classifier (nếu dùng): ~170 tokens (150 in + 20 out)

## Conversation scenario tôi cần tính

Tính cost cho 1 conversation với:

- Số turn: 7 (Scenario B — mùa cao điểm)
- Intent của conversation: Visa/Policy
- Web search được trigger ở turns nào: Turn 1, 2, 3, 4, 5, 6, 7 (ON broad — mọi turn đều bật)

## Yêu cầu output

1. **Bảng cost per turn** — mỗi turn 1 hàng, cột: History tokens, Input total, Output tokens, Cost model, Cost web API, Cost classifier, Total/turn.
2. **Tổng cost/conversation** — sum của tất cả turns.
3. **Show công thức từng bước** — không chỉ ra số, ghi rõ "input = 500 + 1,560 + 1,250 + 800 + 80 = 4,190" để tôi check.
4. **So sánh với human baseline** ($0.50/conv) — AI rẻ hơn bao nhiêu lần?
````

### Config 3: Smart Navigator — Scenario A (Visa × 4 turns, Web Selective)

````text
Tôi đang thiết kế chatbot AI cho travel agency Việt Nam phục vụ khách quốc tế.
Giúp tôi tính chi phí cho 1 conversation theo config sau:

## Config

- Tên config: Smart Navigator
- Generation model: Mix — Claude Sonnet 4.6 ($3.00/$15.00) cho Visa/Weather, Gemini 2.5 Flash-Lite ($0.10/$0.40) cho Guide
- Classifier: LLM model: Claude Sonnet 4.6 — $3.00/M input, $15.00/M output (~170 tokens/call)
- Web search: ON selective — bật cho intent: Visa, Weather
- History: Last 5

## Tham số cố định (giống cho mọi config)

- System prompt: 500 tokens
- User message: 80 tokens
- Assistant response: 180 tokens output
- 1 prior turn history: 260 tokens (80 user + 180 assistant)
- RAG top-5 chunks: 1,250 tokens
- Web search results: 800 tokens (khi bật)
- Web search API: $0.008/query
- LLM classifier (nếu dùng): ~170 tokens (150 in + 20 out)

## Conversation scenario tôi cần tính

Tính cost cho 1 conversation với:

- Số turn: 4 (Scenario A — mùa thấp điểm)
- Intent của conversation: Visa/Policy
- Web search được trigger ở turns nào: Turn 1, 3 (ON selective — bật cho intent Visa)

## Yêu cầu output

1. **Bảng cost per turn** — mỗi turn 1 hàng, cột: History tokens, Input total, Output tokens, Cost model, Cost web API, Cost classifier, Total/turn.
2. **Tổng cost/conversation** — sum của tất cả turns.
3. **Show công thức từng bước** — không chỉ ra số, ghi rõ "input = 500 + 780 + 1,250 + 800 + 80 = 3,410" để tôi check.
4. **So sánh với human baseline** ($0.50/conv) — AI rẻ hơn bao nhiêu lần?
````

---

## Sau khi AI trả về — Sanity check 3 điểm

Trước khi copy số vào worksheet, kiểm 3 điểm:

1. **History tokens có đúng công thức không?**
   - Full: history = (T − 1) × 260. Turn 1 = 0, Turn 7 = 6 × 260 = 1,560.
   - Last 3: history = min(T − 1, 3) × 260. Turn 1 = 0, Turn 7 = 3 × 260 = 780.

2. **Output token có cố định 180/turn không?**
   - Không phụ thuộc input. Mọi turn = 180 output.

3. **Cost web API có chỉ tính khi turn đó bật web không?**
   - Visa intent + web ON selective: $0.005 × (số turn bật) — không phải mỗi turn của conv đều bật nếu nhóm chọn selective.

Nếu AI sai → reply lại "ở Turn X, history tokens bạn tính sai, công thức phải là... — tính lại". AI sẽ correct và retry.

---

## Lặp lại cho từng intent + từng scenario

Conversation cost ≠ same cho mọi intent (vì web search khác nhau). Tính riêng từng combination:

| Combination | Khi nào gọi AI |
|---|---|
| Guide × 4 turns (Scenario A) | Tính 1 lần |
| Visa × 4 turns (Scenario A, web ON) | Tính 1 lần |
| Weather × 4 turns (Scenario A, web ON) | Tính 1 lần |
| Guide × 7 turns (Scenario B) | Tính 1 lần |
| Visa × 7 turns (Scenario B, web ON) | Tính 1 lần |
| Weather × 7 turns (Scenario B, web ON) | Tính 1 lần |
| Booking / Complaint × 1 turn (handoff) | Tính nhanh — chỉ classifier cost nếu LLM |

Tổng: 6–7 lần gọi AI cho 1 config. Nếu nhóm có ≥3 configs → tổng 18–21 lần gọi AI. **Đây là lý do dùng AI thay vì tính tay.**

Mẹo: Gọi AI lần đầu rồi reply "giờ tính lại cho intent Visa với web search ON" — AI sẽ giữ context và chỉ thay vài tham số, nhanh hơn nhiều.

---

## Sau khi có tất cả số

Tính weighted average cost cho cả conversation (theo intent mix):

```text
avg_cost_scenario_A = 50% × cost_guide_4t + 25% × cost_visa_4t + 10% × cost_weather_4t
                    + 10% × cost_1_turn_handoff + 5% × cost_1_turn_handoff

avg_cost_scenario_B = 30% × cost_guide_7t + 15% × cost_visa_7t + 10% × cost_weather_7t
                    + 35% × cost_1_turn_handoff + 10% × cost_1_turn_handoff
```

Monthly:

```text
monthly_A = avg_cost_scenario_A × 300 × 30
monthly_B = avg_cost_scenario_B × 1,200 × 30
```

Điền vào bảng ở `03-cost-calculation.md`.

---

*Prompt 01 · Cost calc. Dùng cùng pattern này cho mọi config trong nhóm.*
