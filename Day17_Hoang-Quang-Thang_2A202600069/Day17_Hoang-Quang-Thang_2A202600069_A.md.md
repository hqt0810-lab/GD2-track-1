# Day 17 Submission
**Student:** Hoàng Quang Thắng  
**Date:** 24/04/2026
**Product idea:** AI web app cho phép sinh viên upload PDF/slide và tự động tạo tóm tắt + bộ câu hỏi ôn thi để học nhanh và chủ động hơn.
---

# 1. MVP Boundary Sheet

## Riskiest Assumption
> Sinh viên sẽ quay lại dùng nhiều lần nếu AI giúp họ biến PDF thành bài tập ôn thi tốt hơn cách tự học hiện tại.

## In-Scope
- [ ] Upload PDF + parse text  
  - Test giả định: user sẵn sàng dùng tài liệu thật của họ

- [ ] Generate Quiz (10 câu)  
  - Test giả định: câu hỏi tạo ra đủ hữu ích để học

- [ ] Basic Summary  
  - Test giả định: user cần hiểu nhanh trọng tâm trước khi làm quiz

## Out-of-Scope
- Login / account system  
  - Lý do bỏ: không cần để test value

- Study plan nhiều ngày  
  - Lý do bỏ: chưa phải pain đầu tiên

- Mobile app native  
  - Lý do bỏ: web là đủ test demand

## Non-Goals
- Không build chatbot general như ChatGPT
- Không support mọi loại file ngoài PDF text-based

---

# 2. PRD Skeleton

## Problem Statement
> Sinh viên đại học học bằng PDF/slide nhưng không có cách biến nội dung đó thành bài tập luyện thi, dẫn đến học thụ động và hiệu quả thấp.

## Target User
> Sinh viên đại học năm 1–4, ôn thi giữa kỳ/cuối kỳ, dùng PDF làm nguồn học chính.

## User Stories

### Story 1
> As a student, I want to upload my lecture PDF and receive practice questions, so that I can test my understanding quickly.

### Story 2
> As a student, I want a summary of key concepts, so that I know what to focus on before exams.

## AI-Specific

### Model Selection
- **Model:** GPT-4-class API
- **Lý do chọn:** mạnh về reasoning + generation + speed to market
- **Trade-offs chấp nhận:** chi phí cao hơn
- **Trade-offs không chấp nhận:** hallucination không kiểm soát

### Data Requirements
- **Nguồn:** PDF user upload
- **Owner:** user + platform xử lý tạm thời
- **Update frequency:** realtime mỗi upload

### Fallback UX
- **Chiến lược:** Expectation Management
- **Trigger:** PDF parse lỗi / output quá generic
- **Hành động:** báo lỗi + gợi ý upload file rõ hơn
- **User options:** retry / chọn summary only

### Success Metrics
- **Primary metric:** % user upload PDF và làm quiz
- **Ngưỡng thành công:** >50%
- **Timeframe:** 30 ngày đầu

### Dependencies & Constraints
- PDF text extraction quality
- API cost
- Latency < 20s

---

# 3. Hypothesis Table

## Hypothesis 1
> Chúng tôi tin rằng quiz tạo từ PDF sẽ giúp sinh viên học chủ động hơn.  
> Chúng tôi sẽ biết mình đúng khi thấy quiz completion rate đạt 50% trong 30 ngày.

- **Riskiest assumption:** Quiz đủ chất lượng
- **Cách test cheapest:** manual review + 20 users beta

## Hypothesis 2
> Chúng tôi tin rằng summary giúp tăng conversion vào quiz.  
> Đúng khi summary viewers có quiz start rate cao hơn 20%.

---

# 4. PMF Scorecard

## Aha Moment
> User upload PDF thứ hai trong vòng 7 ngày mà không cần nhắc.

## Actionable Metric
> % users tạo quiz lần 2 trong 7 ngày

## PMF Method
- Retention Curve + Aha tracking
- **Ngưỡng:** 25% repeat in 7 days

## Vanity Metrics tôi sẽ không dùng
- Signups
- Website visits
- Downloads

---

# 5. AI Critique Log

1. Scope hơi rộng  
   - **Action:** Accept  
   - Giảm còn PDF + quiz + summary

2. Thiếu retention metric  
   - **Action:** Accept  
   - Thêm repeat usage

3. Chưa có fallback UX  
   - **Action:** Accept  
   - Thêm retry flow


---

# 6. Self-assessment

## Yếu nhất
> PMF / retention

## Open questions
1. User có quay lại ngoài mùa thi không?
2. Quiz quality đủ trust không?

---

