# Day 17 Submission
**Student:** Hoàng Quang Thắng  
**Date:** 24/04/2026
**Product idea:** AI study copilot biến mọi tài liệu học thành quiz sát đề, giải thích đáp án và workflow ôn thi lặp lại, giúp sinh viên tăng điểm với ít thời gian hơn.

---

# 1. MVP Boundary Sheet

## Riskiest Assumption
> Nếu AI tạo ra bộ đề sát nội dung môn học trong <2 phút, sinh viên sẽ biến sản phẩm thành workflow mặc định mỗi mùa thi.

## In-Scope
- [ ] Upload PDF + smart chunking  
  - Test giả định: tài liệu thật xử lý ổn định

- [ ] Adaptive Quiz (10–20 câu + explanation)  
  - Test giả định: practice value cao hơn đọc PDF

- [ ] Repeat Loop (save history + upload next file CTA)  
  - Test giả định: có habit loop

## Out-of-Scope
- Flashcard mode  
  - Lý do bỏ: không core loop

- Multi-user class collaboration  
  - Lý do bỏ: phase sau

- Native mobile app  
  - Lý do bỏ: web responsive đủ

## Non-Goals
- Không thay thế LMS / Coursera
- Không dạy full course content

---

# 2. PRD Skeleton

## Problem Statement
> Sinh viên dùng nhiều PDF rời rạc để ôn thi nhưng thiếu hệ thống luyện tập nhanh, khiến mất thời gian và điểm số thấp hơn tiềm năng.

## Target User
> Sinh viên đại học deadline-driven, học sát kỳ thi, ưu tiên speed và score improvement.

## User Stories

### Story 1
> As a student under exam pressure, I want to turn any lecture PDF into a realistic quiz, so that I can identify weak spots fast.

### Story 2
> As a student, I want explanations for wrong answers, so that I improve instead of guessing.

## AI-Specific

### Model Selection
- **Model:** Hybrid (GPT-4-class + smaller local reranker)
- **Lý do chọn:** chất lượng output cao + tối ưu cost retrieval
- **Trade-offs chấp nhận:** complexity backend cao hơn
- **Trade-offs không chấp nhận:** output generic, không grounded vào tài liệu

### Data Requirements
- **Nguồn:** user PDFs + anonymous interaction data
- **Owner:** user owns content, platform owns aggregate analytics
- **Update frequency:** realtime ingestion

### Fallback UX
- **Chiến lược:** Graceful Handover
- **Trigger:** confidence thấp / source mismatch / parse fail
- **Hành động:** show cited excerpts + summary mode only
- **User options:** upload section cụ thể / generate fewer questions / report issue

### Success Metrics
- **Primary metric:** % users upload PDF #2 within 7 days
- **Ngưỡng thành công:** >30%
- **Timeframe:** 60 ngày

### Dependencies & Constraints
- Retrieval quality
- Explainability
- CAC campus channels thấp

---

# 3. Hypothesis Table

## Hypothesis 1
> Chúng tôi tin rằng grounded quizzes từ tài liệu thật sẽ giúp sinh viên quay lại học với tài liệu tiếp theo.  
> Đúng khi PDF #2 upload rate đạt 30% trong 7 ngày.

- **Riskiest assumption:** enough repeat value
- **Cheapest test:** concierge MVP với 30 users

## Hypothesis 2
> Explanation cho câu sai sẽ tăng retention hơn quiz-only.  
> Đúng khi D7 retention cao hơn 15%.

## Hypothesis 3
> “Thi sát đề” positioning convert tốt hơn “AI học tập”.  
> Đúng khi landing CTR cao hơn 25%.

---

# 4. PMF Scorecard

## Aha Moment
> User upload tài liệu mới trước kỳ thi tiếp theo và chia sẻ tool cho bạn cùng lớp.

## Actionable Metric
> Weekly Active Study Sessions / user

## PMF Method
- Sean Ellis
- Cohort Retention
- Aha tracking

## Ngưỡng thành công
- 40% “very disappointed”
- D30 retention >20% mùa thi

## Vanity Metrics
- Tổng signups
- Tổng token generated
- Social likes

---

# 5. AI Critique Log

1. Version A chưa có moat  
   - **Action:** Accept  
   - Thêm interaction data loop

2. Chưa rõ repeat loop  
   - **Action:** Accept  
   - Thêm history + CTA PDF #2

3. Positioning quá generic  
   - **Action:** Accept  
   - Đổi sang “thi sát đề”

## Thay đổi lớn nhất giữa Version A và Version B
> Từ tool tạo quiz một lần thành product có habit loop + retention thesis + sharper positioning.

---

# 6. Self-assessment

## Yếu nhất
> Go-to-market + seasonality risk

## Open questions
1. Làm sao giữ user ngoài mùa thi?
2. Môn nào nên dominate đầu tiên?
3. Giá bao nhiêu sinh viên chịu trả?