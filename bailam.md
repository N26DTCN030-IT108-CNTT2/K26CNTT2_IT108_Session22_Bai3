# [D26TXCN02-N]_IT108_[Session 22]_[Bài 3]
**Bài tập: Sử dụng AI an toàn khi xử lý lỗi phần mềm**

**Thông tin sinh viên:**
- **Họ và tên:** Lê Hồ Thanh Thảo
- **Mã sinh viên:** N26DTCN030
- **Lớp:** D26TXCN02-N
- **Môn học:** Nhập môn Công nghệ Thông tin (IT_108) 

---

## 1. Báo cáo phân tích theo mô hình IPO (Input - Process - Output)

### 📥 Input (Dữ liệu đầu vào)
* **Bối cảnh:** Gặp lỗi `"Path not found"` khi cài đặt Python trên máy tính.
* **Câu trả lời của AI:** Đưa ra một lệnh gạch đầu dòng và yêu cầu dán/chạy trực tiếp vào Terminal (Command Line/PowerShell) nhưng lệnh trông lạ và có nguy cơ can thiệp sâu vào hệ thống.

---

### ⚙️ Process (Quy trình kiểm chứng thông tin)
Để tránh nguy cơ **AI Hallucination** (AI ảo giác, đưa ra lệnh không chính xác hoặc nguy hại), ta tiến hành quy trình kiểm chứng qua 3 bước:

1. **Phân tích cú pháp lệnh (Command Deconstruction):**
   * Đọc kỹ từng tham số (flag/options) của lệnh. Cảnh giác với các lệnh xóa hệ thống (`rm -rf`, `Remove-Item -Recurse`), can thiệp registry (`reg delete`), hoặc sửa đổi biến môi trường toàn cục (`PATH`) không rõ ràng.
2. **Tra cứu kiểm chứng bằng toán tử Google Search:**
   * **Tra cứu cộng đồng StackOverflow:**
     ```bash
     "Path not found" Python site:stackoverflow.com
     ```
   * **Tra cứu trang chủ chính thức:**
     ```bash
     "environment variables" site:docs.python.org
     ```
3. **Đối chiếu kết quả:**
   * So sánh lệnh AI đưa ra với các giải pháp chuẩn được bình chọn cao (upvoted) trên StackOverflow và tài liệu hướng dẫn gốc (`docs.python.org`).

---

### 📤 Output (Kết quả xác nhận)
* **Đánh giá độ an toàn:** 
  * ❌ **KHÔNG AN TOÀN / KHÔNG THỰC THI NGAY:** Nếu lệnh chứa các tham số sửa đổi Registry hệ thống, can thiệp quyền Administrator (`sudo`, `Run as Administrator`) mà không giải thích rõ ràng, hoặc không xuất hiện trong tài liệu chính thức.
  * ✅ **AN TOÀN:** Chỉ thực thi sau khi đã kiểm chứng qua nguồn chính thống và hiểu rõ tác động của từng từ khóa trong lệnh.

---

## 2. Thiết kế Prompt "Hỏi ngược lại AI" (Verification Prompt)

Khi AI đưa ra một câu lệnh can thiệp hệ thống, bạn có thể dán Prompt mẫu dưới đây để yêu cầu AI tự giải thích và chứng minh độ an toàn trước khi bấm Enter:

```text
Tôi thấy câu lệnh bạn vừa đưa ra có vẻ can thiệp sâu vào hệ thống/biến môi trường. Trước khi tôi thực thi, hãy giải thích chi tiết giúp tôi:

1. Giải thích ý nghĩa của từng thành phần/tham số (flag) trong câu lệnh trên.
2. Lệnh này áp dụng chính xác cho Hệ điều hành nào (Windows, macOS hay Linux)?
3. Rủi ro hoặc tác dụng phụ (nếu có) đối với hệ thống của tôi khi chạy lệnh này là gì?
4. Đưa ra tài liệu chính thức (từ docs.python.org hoặc Microsoft/Apple Docs) hoặc link StackOverflow xác nhận tính an toàn của giải pháp này.
```