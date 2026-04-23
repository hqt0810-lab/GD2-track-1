# Day 16 Submission
## Members
- Hoàng Quang Thắng
---
## 1. Idea reframed

> Sinh viên hiện có rất nhiều tài liệu (PDF, slide) nhưng thiếu khả năng chuyển chúng thành kế hoạch học và luyện tập hiệu quả, tạo ra một khoảng trống rõ ràng giữa “access to content” và “learning outcomes”. Các công cụ hiện tại (note-taking, flashcard) chỉ giải quyết từng phần nhỏ và vẫn yêu cầu người dùng tự thiết kế cách học.
> Observed gap: Không có lớp “orchestration layer” biến tài liệu thô thành trải nghiệm học có cấu trúc và đo lường được.
> Founding belief: Nếu AI có thể tự động hóa việc hiểu tài liệu → tạo bài tập → xây lộ trình → đánh giá tiến độ, thì nó có thể thay thế phần lớn vai trò của gia sư cơ bản. → Đây là cơ hội xây dựng một AI-native learning workflow, không chỉ là feature AI.
---
## 2. Customer / Segment Card
- **Segment name:** Sinh viên đại học đang chạy deadline
- **Operational context:** Học theo kỳ, áp lực thi, tài liệu rời rạc (PDF/slide)
- **Recurring workflow:** Thu thập tài liệu → đọc lướt → highlight → học dồn trước kỳ thi
- **Pain moment:** Không biết phần nào quan trọng, không có feedback về mức độ hiểu
- **Why now:**
    - LLM đủ mạnh để hiểu nội dung học thuật
    - Sinh viên quen với AI tools
    - Áp lực tối ưu thời gian học ngày càng lớn
- **Access path:** Campus communities, study groups, TikTok/FB, referral giữa sinh viên

**One-sentence description:**
> Sinh viên học từ tài liệu số nhưng thiếu hệ thống để biến chúng thành quá trình ôn thi hiệu quả và có kiểm chứng
---
## 3. Need Map
### Need #1 (priority)
- **Statement (JTBD):** When I prepare for exams from scattered materials, I want a structured study system generated automatically, so I can focus on high-impact content and save time.
- **Current workaround:** Học nhiều nhưng không vào, cảm giác “học sai trọng tâm”
- **Pain signal:** Học nhiều nhưng vẫn không nhớ, tốn thời gian highlight, tìm kiếm đề trên mạng
- **Evidence / proxy evidence:** Hành vi phụ thuộc vào đề cũ rất phổ biến, sinh viên thường hỏi nhau “có đề không”
- **Why underserved:** Không có tool nào transform input (PDF) → output (plan + practice + evaluation) end-to-end

### Need #2
- **Statement (JTBD):** When I study, I want continuous testing and feedback, so I can accurately gauge my readiness before exams.
- **Current workaround:** Làm đề cũ (nếu có)
- **Pain signal:** Overconfidence, sốc khi vào phòng thi
- **Evidence / proxy evidence:** Đề cũ được share rất nhiều → chứng tỏ nhu cầu cao
- **Why underserved:** Không có hệ thống auto-generate exam phù hợp với từng tài liệu cá nhân

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
1. Tích lũy dataset về cấu trúc tài liệu học, pattern câu hỏi thix2
2. Cải thiện chất lượng với câu hỏi gần đề hơn và lộ trình học phù hợp workload thực tế
3. Cá nhân hóa theo tốc độ học và performance từng user 
Why competitors cannot easily replicate this:
> Không chỉ cần model tốt, mà cần behavioral learning data + feedback loop + domain tuning, thứ chỉ có khi có distribution thực
---
## 6. Initial TAM / SAM / SOM view
| Layer | Estimate          | Key assumptions                           | Confidence |
| ----- | ----------------- | ----------------------------------------- | ---------- |
| TAM   | $2B–$5B/year      | Global digital learning + AI tools        | Medium     |
| SAM   | $200M–$500M       | Students actively using study tools       | Low        |
| SOM   | $1M–$5M (12–24mo) | Campus-first growth + freemium conversion | Low        |

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