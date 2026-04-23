# Day 16 Submission
## Members
- Hoàng Quang Thắng
---
## 1. Idea reframed
Original idea:
> Product này giúp sinh viên upload tài liệu (PDF/slide) và tự động biến nó thành tóm tắt trọng tâm, bộ câu hỏi ôn tập và lộ trình học cá nhân hóa. Thay vì đọc lại tài liệu một cách thụ động, sinh viên được hướng dẫn học như có “gia sư AI”, giúp ôn thi nhanh và hiệu quả hơn.
Reframed as a product opportunity:  
> Sinh viên hiện học từ PDF/slide nhưng thiếu cấu trúc, dẫn đến học thụ động và kém hiệu quả — đây là một observed gap rõ ràng giữa “có tài liệu” và “biết cách học”. Các công cụ hiện tại chỉ hỗ trợ ghi chú hoặc flashcard rời rạc, không tạo được trải nghiệm học có định hướng.
> Founding belief: nếu AI có thể chuyển tài liệu thành lộ trình học + bài tập + kiểm tra liên tục, thì hiệu quả học sẽ tăng đáng kể. Đây là cơ hội để xây dựng một “AI tutor layer” nằm trên tài liệu học.
---
## 2. Customer / Segment Card
- **Segment name:** Sinh viên đại học đang chuẩn bị cho bài kiểm tra
- **Operational context:** Học từ PDF/slide, deadline dồn, thi cuối kỳ
- **Recurring workflow:** Đọc tài liệu → highlight → cố nhớ → làm đề (nếu có)
- **Pain moment:** Không biết phần nào quan trọng, ôn lan man trước kỳ thi
- **Why now:** AI đủ mạnh để hiểu tài liệu + generate bài tập + cá nhân hóa
- **Access path:** Campus, bạn bè, cộng đồng sinh viên, TikTok/FB học tập
One-sentence description:
> Sinh viên ôn thi bằng PDF/slide nhưng không có hệ thống học hiệu quả và không biết bắt đầu từ đâu
---
## 3. Need Map (2–3 needs)
### Need #1 (priority)
- **Statement (JTBD):** When I prepare for exams from PDF/slide, I want a structured study plan with practice questions, so I can study efficiently and know what matters.
- **Current workaround:** Đọc lại, highlight, hỏi bạn, tìm đề trên mạng
- **Pain signal:** Học nhiều nhưng vẫn không nhớ, tốn thời gian highlight, tìm kiếm đề trên mạng
- **Evidence / proxy evidence:** Thói quen dùng highlight + hỏi “phần nào thi?” rất phổ biến
- **Why underserved:** Công cụ hiện tại không kết nối tài liệu → luyện tập → lộ trình

### Need #2
- **Statement (JTBD):** When I study, I want to test myself continuously, so I can measure progress.
- **Current workaround:** Làm đề cũ (nếu có)
- **Pain signal:** Đến sát thi nhưng vẫn chưa hiểu
- **Evidence / proxy evidence:** Sinh viên phụ thuộc heavily vào đề cũ
- **Why underserved:** hông có tool nào auto generate exam từ tài liệu cá nhân

---
## 4. Strategy Statement
For [sinh viên đại học]
who struggle with [bài kiểm tra không có trọng tâm],
our product helps them [biến mọi file pdf thành 1 file học tập có trọng tâm]
through [summaries, quizzes và study plans do AI-generated],
unlike [notepad hay flashcard],
because we can leverage [Chuyển đổi nguyên liệu thô thành quy trình học tập có thể áp dụng thực tiễn.].
---
## 5. Moat Hypothesis
**Moat mechanism:** [e.g. domain-learning flywheel]
If we deploy at scale in student contexts, the following improve:
1. Hiểu pattern tài liệu (slide, môn học, đề thi) tốt hơn
2. Cải thiện chất lượng câu hỏi và lộ trình học
3. Cá nhân hóa theo hành vi học của user
Why competitors cannot easily replicate this:
> Cần dữ liệu hành vi học thực + vòng lặp cải tiến liên tục, không chỉ là LLM generic
---
## 6. Initial TAM / SAM / SOM view
| Layer | Estimate          | Key assumptions                      | Confidence |
| ----- | ----------------- | ------------------------------------ | ---------- |
| TAM   | $2B–$5B/year      | Global student learning tools        | Medium     |
| SAM   | $200M–$500M       | Students dùng digital learning tools | Low        |
| SOM   | $1M–$5M (12–24mo) | Campus adoption + viral loop         | Low        |
**Top 3 unknowns requiring further research:**
1. Sinh viên có trả tiền không hay chỉ dùng free
2. Retention sau kỳ thi có đủ cao không
3. Chất lượng AI có đủ để tạo trust không

**Judgment:**
- [V] Worth pursuing now
- [ ] Worth pursuing but not now (need to validate [...] first)
- [ ] Not worth pursuing as currently framed
---
## 7. Positioning Note (2 sentences)
**What we are:**
> AI biến tài liệu học thành hệ thống ôn thi hoàn chỉnh (plan + practice + test)
**What we are not / not yet:**
> Không phải chatbot chung chung hay app ghi chú đơn thuần
---
## 8. Self-assessment before Day 17
Trong 6 mắt xích (Idea Customer Need Strategy Moat Market Size), mắt xích nà
> Moat (chưa rõ đủ mạnh để chống copy)
Open questions chúng tôi muốn khám phá thêm ở Day 17:
1. Làm sao tạo retention sau khi user thi xong
2. Làm sao đảm bảo chất lượng câu hỏi đủ “giống đề thật”
3. Có nên focus 1 môn (vd: IT, kinh tế) trước không