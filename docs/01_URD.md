# **01\. USER REQUIREMENTS DOCUMENT (URD)**

Project: CollabSphere (COSRE)  
Version: 1.0  
Date: 2025-05-20

## **1\. Giới thiệu (Introduction)**

### **1.1. Bối cảnh (Context)**

Hiện tại, việc học theo dự án (Project-Based Learning \- PBL) tại trường đang gặp khó khăn do sự phân mảnh công cụ: sinh viên dùng Messenger/Zalo để chat, Google Drive để lưu file, và Zoom để họp. Giảng viên khó theo dõi tiến độ thực tế và đánh giá đóng góp của từng sinh viên.

### **1.2. Mục tiêu (Goals)**

Xây dựng hệ thống **"All-in-one"** hỗ trợ toàn diện quy trình PBL:

* **Centralized:** Tập trung mọi hoạt động (quản lý, giao tiếp, làm việc) trên 1 nền tảng.  
* **Transparency:** Minh bạch hóa tiến độ và đóng góp của thành viên.  
* **Intelligence:** Tích hợp AI để hỗ trợ gợi ý và giảm tải công việc thủ công.

## **2\. Danh sách các bên liên quan (Stakeholders)**

| Stakeholder | Vai trò & Trách nhiệm chính | Mong muốn cốt lõi |
| :---- | :---- | :---- |
| **Admin** | Quản trị hệ thống, bảo mật. | Hệ thống ổn định, dễ quản lý user, log đầy đủ. |
| **Staff** (Giáo vụ) | Quản lý dữ liệu học vụ (Môn, Lớp). | Import dữ liệu nhanh (Excel), ít lỗi. |
| **Head** (Trưởng bộ môn) | Phê duyệt đề tài, giám sát chất lượng. | Quy trình duyệt nhanh, nhìn được tổng quan các lớp. |
| **Lecturer** (Giảng viên) | Tạo đề tài, hướng dẫn, đánh giá. | Công cụ chấm điểm tiện lợi, theo dõi được ai làm gì. |
| **Student** (Sinh viên) | Thực hiện dự án, báo cáo. | Có không gian làm việc nhóm (chat, whiteboard) hiệu quả. |

## **3\. User Needs (Nhu cầu người dùng)**

* **UN-01:** Tôi cần một nơi để xem tất cả thông tin đồ án thay vì tìm kiếm trong email.  
* **UN-02:** Tôi muốn họp nhóm online và vẽ ý tưởng ngay trên web mà không cần cài phần mềm.  
* **UN-03:** Giảng viên cần biết chính xác sinh viên nào "gánh team", sinh viên nào không làm gì.  
* **UN-04:** Hệ thống cần gợi ý các mốc thời gian (milestones) để sinh viên đỡ bỡ ngỡ khi bắt đầu.

## **4\. Open Questions**

* \[ \] Quy trình xử lý khi sinh viên muốn đổi nhóm giữa chừng? (Hiện tại: Cần Lecturer approve).  
* \[ \] Dung lượng lưu trữ tối đa cho mỗi nhóm là bao nhiêu? (Giả định: 5GB/nhóm).