# AI-Assisted LMS & Grading Portal

Hệ thống quản lý học tập và hỗ trợ chấm bài bằng AI, cho phép quản lý khóa học/bài tập, nộp bài, phát hiện đạo văn ngữ nghĩa, gợi ý chấm điểm theo rubric và công bố kết quả.

## Tính năng chính

- **Xác thực & phân quyền theo ngữ cảnh khóa học (RBAC):** Vai trò `INSTRUCTOR`, `TA`, `STUDENT` trên từng khóa học (JWT Access Token + HttpOnly Refresh Token).
- **Quản lý khóa học & bài tập:** Tạo khóa học, giao bài với deadline, cấu hình rubric (tiêu chí, trọng số, điểm tối đa) và quy tắc trừ điểm nộp muộn.
- **Nộp bài:** Hỗ trợ tệp bài làm (PDF/DOCX/mã nguồn), kiểm tra định dạng/dung lượng, ghi nhận thời gian nộp, đánh dấu nộp muộn và lưu lịch sử phiên bản.
- **AI phát hiện đạo văn ngữ nghĩa:** Bóc tách nội dung, tạo embedding và tính độ tương đồng Cosine giữa các bài nộp; cảnh báo khi mức tương đồng cao (ngưỡng thiết kế > 80%).
- **AI gợi ý chấm bài (AI Copilot):** Đối chiếu bài làm với rubric để đề xuất điểm nháp và nhận xét chi tiết cho trợ giảng/giảng viên.
- **Chấm chéo ẩn danh (Blind Grading):** Phân công chấm độc lập, phát hiện lệch điểm (ngưỡng thiết kế > 20%) để giảng viên rà soát trước khi chốt.
- **Thống kê & xuất bảng điểm:** Phân phối điểm (mean/median/std dev) và xuất kết quả (CSV/XLSX).

## Thiết kế hệ thống (tóm tắt)

- **Kiến trúc:** React Portal, Core API (Node.js), AI Service (FastAPI), PostgreSQL; pipeline xử lý AI bất đồng bộ sau khi nộp bài.
- **Vòng đời bài nộp:** `Draft → Submitted/LateSubmitted → AIAnalyzed → Grading (BlindReview/ConflictCheck/Escalated/Approved) → Published`.
- **Mô hình dữ liệu chính:** Users, Courses, Enrollments, Assignments, Rubric Criteria, Submissions, Grades, Grade Details.

## Tài liệu tham khảo

- Đặc tả chi tiết: `Dự án mở rộng 1 - SRS, Product Backlog & System Design - AI LMS & Grading Portal.pdf` (SRS, Product Backlog, UML, ERD, ADR, API Contracts).
- Tác giả đặc tả: Mai Quang Vũ — Phiên bản 1.0.0 (Baseline Approved).
