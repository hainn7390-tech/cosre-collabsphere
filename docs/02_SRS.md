# **02\. SOFTWARE REQUIREMENTS SPECIFICATION (SRS)**

**Project:** CollabSphere (COSRE)

## **1\. Yêu cầu chức năng (Functional Requirements \- FR)**

### **Module 1: Academic & Account Management**

* **FR-ACC-01:** Admin có thể khóa tài khoản vi phạm.  
* **FR-ACA-01:** Staff import danh sách Lớp (Class) và Sinh viên (Student) từ file CSV/Excel.  
* **FR-ACA-02:** Staff gán Giảng viên (Lecturer) phụ trách lớp.

### **Module 2: Project Management**

* **FR-PRO-01:** Lecturer tạo Project với các thông tin: Tên, Mô tả, Syllabus áp dụng.  
* **FR-PRO-02 (AI):** Hệ thống tích hợp AWS Bedrock để tự động gợi ý 4-6 Milestones dựa trên mô tả Project.  
* **FR-PRO-03:** Head Department phê duyệt (Approve) hoặc từ chối (Deny) Project.

### **Module 3: Team & Workspace**

* **FR-TEAM-01:** Sinh viên tự tạo nhóm hoặc tham gia nhóm theo Link mời/Mã lớp.  
* **FR-WRK-01:** Task Board (Kanban) cho phép kéo thả task (Todo \-\> Doing \-\> Done).  
* **FR-WRK-02:** Leader xác nhận hoàn thành Milestone (Submit checkpoint).

### **Module 4: Communication & Collaboration**

* **FR-COM-01:** Chat nhóm Realtime (Text, Image).  
* **FR-COM-02:** Video Meeting tích hợp (WebRTC), hỗ trợ Screen Share.  
* **FR-COL-01:** Whiteboard Realtime: Vẽ hình, note ý tưởng, đồng bộ tức thì.

### **Module 5: Evaluation**

* **FR-EVA-01:** Lecturer chấm điểm theo Rubric (định nghĩa trong Syllabus).  
* **FR-EVA-02:** Sinh viên thực hiện đánh giá chéo (Peer Review) ẩn danh.

## **2\. Yêu cầu phi chức năng (Non-Functional Requirements \- NFR)**

### **Performance**

* **NFR-PER-01:** Thời gian phản hồi API trung bình \< 300ms.  
* **NFR-PER-02:** Độ trễ (Latency) của Whiteboard/Chat \< 200ms.  
* **NFR-PER-03:** Hỗ trợ 500 CCU (Concurrent Users) mà không crash.

### **Security**

* **NFR-SEC-01:** Mật khẩu lưu trữ dạng Hash (Bcrypt/Argon2).  
* **NFR-SEC-02:** Authentication dùng JWT (Access Token 30p, Refresh Token 7 ngày).  
* **NFR-SEC-03:** Mọi API thay đổi dữ liệu phải check RBAC (Role-Based Access Control).

### **Reliability**

* **NFR-REL-01:** Hệ thống Backend (Azure) đảm bảo Uptime 99%.

## **3\. Use Case Descriptions (Sample)**

**UC-02: Create Project with AI**

* **Actor:** Lecturer  
* **Pre-condition:** Đã login, được gán vào lớp.  
* **Main Flow:**  
  1. Lecturer chọn "Create Project".  
  2. Nhập "Tên đề tài" và "Mô tả sơ bộ".  
  3. Nhấn nút "Generate Milestones with AI".  
  4. Hệ thống gọi AWS Bedrock, trả về danh sách Milestone gợi ý.  
  5. Lecturer chỉnh sửa và nhấn "Save".  
* **Post-condition:** Project ở trạng thái "Pending Approval".

## **4\. Open Questions**

* \[ \] Cơ chế Retry khi gọi AI thất bại (Timeout/Rate limit)?  
* \[ \] Giới hạn số lượng Project mà một Lecturer được tạo trong 1 kỳ?