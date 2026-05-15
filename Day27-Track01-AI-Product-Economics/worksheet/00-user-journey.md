# 00 · User Journey Simulation — Đóng vai Tourist

> **Mục tiêu**: Trước khi tính chi phí, nhóm phải hình dung được khách hàng thật sự hỏi gì, hỏi như thế nào, và 1 conversation thực tế trông ra sao.
>
> **Thời gian**: 8 phút (trong 15 phút phần Setup)

---

## Tại sao phải làm bước này?

Nếu nhóm bắt đầu tính cost mà chưa biết tourist hỏi gì → mọi con số chỉ là lý thuyết. Bước này buộc nhóm "chạm" sản phẩm trước khi mở Excel.

---

## Bước 1 — Mỗi người đóng vai 1 tourist (4 phút)

Tưởng tượng mình là 1 khách du lịch nước ngoài đang plan trip Việt Nam. Bạn vừa mở website công ty du lịch, thấy có chatbot ở góc màn hình. Bạn sẽ hỏi gì?

Trước khi viết, tự hỏi:

- Mình từ đâu đến? Mỹ, Anh, Hàn, Nhật, Úc?
- Đi 1 mình hay đi nhóm? Budget khoảng bao nhiêu?
- Đã biết gì về Việt Nam? Lần đầu đến hay đã đến rồi?
- Mình lo lắng điều gì nhất? (visa, an toàn, ngôn ngữ, thời tiết, ẩm thực, lừa đảo...)

Viết **5–7 câu hỏi bằng tiếng Anh** mình sẽ thật sự gửi cho chatbot. Viết câu hỏi tự nhiên, đúng giọng tourist — không phải đặt câu hỏi "nghe có vẻ technical".

→ Mỗi người viết vào ô dưới (chưa có gì sẵn — đừng nhìn người bên cạnh):

### Tourist #1 (Tên thành viên: John - US)

```text
1. I'm from the US and planning a 3-week trip to Vietnam next month. Do I need an e-visa or can I get it on arrival? I heard policies changed.
2. What are the must-visit hidden gems in Hoi An for a 2-day stay, away from the crowded spots?
3. Is it going to be raining heavily in Da Nang next week? Should I pack an umbrella?
4. I want to book the Ha Long Bay 2-day 1-night cruise you have on your site for 2 people. How do I pay?
5. I've been waiting at the airport pickup spot for 30 mins and your driver isn't here. Please help immediately!
```

### Tourist #2 (Tên thành viên: Emma - EU)

```text
1. I'm a solo traveler from the UK. What's the cheapest way to travel from Hanoi to Sapa?
2. Are there any vegetarian street food options in Ho Chi Minh city?
3. I just realized my passport expires in 5 months. Can I still enter Vietnam?
4. Is it safe to walk around the Old Quarter in Hanoi at night?
5. Can you help me change the date of my Ninh Binh tour to tomorrow?
```

### Tourist #3 (Tên thành viên: Alex - AUS)

```text
1. I'm flying from Sydney. Do Australians need a visa for a 14-day trip?
2. What's the best time of year to visit the Mekong Delta?
3. I need to book a 5-star hotel in Da Nang. Any recommendations near the beach?
4. How much should a taxi cost from the airport to District 1 in HCMC?
5. The room I booked through you has a broken AC. Can I get a refund or move rooms?
```

---

## Bước 2 — Gom lại và phân loại (4 phút)

Cả nhóm chụm vào, gom tất cả câu hỏi lại. Trước khi điền bảng, thảo luận 1 phút:

- Có câu hỏi nào lặp lại giữa các tourist không?
- Có chủ đề nào không ai trong nhóm nghĩ tới ban đầu nhưng quan trọng?
- Câu nào chatbot có thể trả lời được? Câu nào cần chuyển sang nhân viên thật?

5 intent có sẵn (tham khảo `cost-reference-card.md` mục 2):

- **Visa/Policy** — chính sách, thủ tục nhập cảnh
- **Điểm đến/Guide** — gợi ý đi đâu, làm gì, ăn gì
- **Thời tiết/Sự kiện** — info real-time
- **Tour/Booking** — đặt vé, đặt tour, đặt phòng → chuyển sales
- **Khiếu nại** — phàn nàn → chuyển manager

Sau khi gom, điền bảng phân loại:

| # | Câu hỏi (1 dòng) | Intent thuộc loại nào | Cần bao nhiêu lượt chat để xong? | Bot trả lời hay chuyển người? |
|---|---|---|---|---|
| 1 | I'm from the US... Do I need an e-visa? | Visa/Policy | 3-4 | ☑ Bot · □ Người |
| 2 | What are the must-visit hidden gems in Hoi An? | Điểm đến/Guide | 4-5 | ☑ Bot · □ Người |
| 3 | Is it going to be raining heavily in Da Nang? | Thời tiết/Sự kiện | 2-3 | ☑ Bot · □ Người |
| 4 | I want to book the Ha Long Bay 2-day cruise... | Tour/Booking | 1 (Handoff) | □ Bot · ☑ Người |
| 5 | I've been waiting... driver isn't here! | Khiếu nại | 1 (Escalate) | □ Bot · ☑ Người |
| 6 | What's the cheapest way to travel Hanoi -> Sapa? | Điểm đến/Guide | 3-4 | ☑ Bot · □ Người |
| 7 | Are there vegetarian street food options in HCMC?| Điểm đến/Guide | 3-4 | ☑ Bot · □ Người |
| 8 | Passport expires in 5 months. Can I still enter?| Visa/Policy | 2-3 | ☑ Bot · □ Người |
| 9 | Can you help me change the date of my tour? | Tour/Booking | 1 (Handoff) | □ Bot · ☑ Người |
| 10 | Room has broken AC. Can I get a refund? | Khiếu nại | 1 (Escalate) | □ Bot · ☑ Người |

---

## Bước 3 — Rút insight cho nhóm (cuối phần Setup)

Trả lời nhanh 4 câu — sẽ dùng lại ở các bước sau:

**Tổng số câu hỏi nhóm gom được**:

```text
15 câu
```

**Phân bố intent thực tế của nhóm** (% mỗi intent):

```text
Guide: 40%
Visa: 20%
Weather: 13.3%
Booking: 13.3%
Khiếu nại: 13.3%
```

**Số lượt chat trung bình để xong 1 chủ đề**:

```text
Khoảng 3-4 lượt cho các câu hỏi thông tin (Guide, Visa). Booking và Khiếu nại tốn 1 lượt để phân loại và chuyển ngay cho người.
```

**Đối chiếu với đề bài** (Scenario A = 4 lượt, Scenario B = 7 lượt):

```text
Hợp lý vì trung bình 1 intent tốn 3-4 lượt. Kịch bản 7 lượt thường là khách có nhiều intent gộp chung (hỏi thời tiết xong hỏi điểm đến rồi đặt tour).
```

**Insight bất ngờ — điều gì nhóm chỉ hiểu sau khi đóng vai?**

```text
Tourist rất hay lồng ghép khiếu nại hoặc đặt tour vào những câu hỏi thông tin cấp bách. Việc nhận diện đúng Intent Booking và Khiếu nại ngay lượt đầu là cực kỳ quan trọng để không làm khách nổi cáu vì phải chat với AI.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Mỗi người trong nhóm đã viết ≥5 câu hỏi tourist
- [x] Đã gom + phân loại intent cho ≥10 câu (bảng trên)
- [x] Đã có phân bố intent % của nhóm (so với đề bài)
- [x] Có ít nhất 1 insight về cách tourist thật sự dùng chatbot

Xong → mở `01-base-flow.md`.
