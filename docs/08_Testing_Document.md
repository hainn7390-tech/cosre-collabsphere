# **08\. TESTING DOCUMENT**

**Project:** CollabSphere (COSRE)

## **1\. Test Strategy**

* **Unit Testing (Backend):** Dùng pytest. Tập trung vào Services, Util functions, Data Models. Coverage target: 80%.  
* **Integration Testing:** Test API endpoints với DB test riêng. Check Auth flow, Data integrity.  
* **Frontend Testing:** Dùng Jest \+ React Testing Library. Test các component render đúng, event handler hoạt động.  
* **E2E Testing:** Dùng Cypress hoặc Playwright. Test các luồng người dùng chính (Critical Paths).

## **2\. Test Cases Mapping (Sample)**

| TC ID | Requirement | Description | Expected Result | Priority |
| :---- | :---- | :---- | :---- | :---- |
| **TC-AUTH-01** | FR-SEC-02 | Login với email/pass đúng. | Trả về 200 OK \+ JWT Token. | High |
| **TC-PROJ-01** | FR-PRO-02 | Gọi API AI generate milestones. | Trả về list milestones không rỗng, đúng format JSON. | Medium |
| **TC-REAL-01** | FR-COL-01 | User A vẽ, User B cùng phòng. | User B thấy nét vẽ của A sau \< 200ms. | High |
| **TC-REAL-02** | FR-COM-02 | 2 User join video room. | Kết nối WebRTC thành công, stream video hiển thị. | High |

## **3\. Bug Reporting Process**

1. Phát hiện lỗi \-\> Log lên Jira (Issue Type: Bug).  
2. Gán Priority (Critical/Major/Minor).  
3. Dev fix \-\> Commit \-\> QA verify trên môi trường Staging.  
4. Close ticket.

## **4\. Open Questions**

* \[ \] Làm sao để automate test WebRTC (fake media stream)?  
* \[ \] Load testing cho Socket.IO server dùng tool gì? (Gợi ý: Artillery hoặc Locust).