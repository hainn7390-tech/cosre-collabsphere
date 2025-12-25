# **04\. DATABASE DETAILED DESIGN**

**Project:** CollabSphere (COSRE)

## **1\. Entity Relationship Diagram (ERD)**

erDiagram  
    USERS ||--o{ CLASS\_MEMBERS : joins  
    USERS ||--o{ TEAM\_MEMBERS : belongs\_to  
    CLASSES ||--o{ PROJECTS : has  
    PROJECTS ||--o{ MILESTONES : defines  
    PROJECTS ||--o{ TEAMS : assigned\_to  
    TEAMS ||--o{ TASKS : manages  
    TEAMS ||--o{ SUBMISSIONS : submit  
    MILESTONES ||--o{ TASKS : associated\_with

## **2\. Schema Specification**

### **Table: users**

| Column | Type | Constraints | Description |
| :---- | :---- | :---- | :---- |
| id | SERIAL | PK |  |
| email | VARCHAR(100) | UNIQUE, NOT NULL |  |
| password\_hash | VARCHAR(255) | NOT NULL |  |
| role | ENUM | ('ADMIN','STAFF','HEAD','LECTURER','STUDENT') |  |
| is\_active | BOOLEAN | DEFAULT TRUE |  |

### **Table: projects**

| Column | Type | Constraints | Description |
| :---- | :---- | :---- | :---- |
| id | SERIAL | PK |  |
| title | VARCHAR(200) | NOT NULL |  |
| syllabus\_id | INT | FK \-\> syllabus.id |  |
| created\_by | INT | FK \-\> users.id | Lecturer tạo |
| status | ENUM | ('DRAFT','PENDING','APPROVED','REJECTED') |  |

### **Table: teams**

| Column | Type | Constraints | Description |
| :---- | :---- | :---- | :---- |
| id | SERIAL | PK |  |
| project\_id | INT | FK \-\> projects.id | Nullable nếu chưa chọn đề tài |
| class\_id | INT | FK \-\> classes.id |  |
| leader\_id | INT | FK \-\> users.id |  |

### **Table: tasks (Kanban)**

| Column | Type | Constraints | Description |
| :---- | :---- | :---- | :---- |
| id | SERIAL | PK |  |
| team\_id | INT | FK \-\> teams.id |  |
| milestone\_id | INT | FK \-\> milestones.id |  |
| status | ENUM | ('TODO','DOING','DONE') |  |
| assignee\_id | INT | FK \-\> users.id |  |

## **3\. Indexing Strategy**

* users(email): Cho login nhanh.  
* team\_members(user\_id, team\_id): Composite index để query "User này thuộc team nào".  
* tasks(team\_id, status): Tối ưu load bảng Kanban.

## **4\. Open Questions**

* \[ \] Xử lý soft delete (xóa mềm) cho Project/Task hay xóa cứng?  
* \[ \] Lưu trữ lịch sử chat trong bảng messages hay dùng NoSQL (MongoDB) nếu scale lớn? (Hiện tại: PostgreSQL Partitioning).