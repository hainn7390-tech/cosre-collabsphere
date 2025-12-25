# **05\. FRONTEND SPECIFICATION**

**Project:** CollabSphere (COSRE)

## **1\. Site Map & Routing**

* **/auth**: Login, Forgot Password.  
* **/dashboard**: (Role-based)  
  * **Admin/Staff**: User Management, Class Import.  
  * **Lecturer**: My Classes, Project Creation, Grading Queue.  
  * **Student**: My Projects, Team Workspace.  
* **/workspace/:teamId**:  
  * **/overview**: Project info, Progress.  
  * **/board**: Kanban Board.  
  * **/whiteboard**: Collaborative Canvas.  
  * **/meeting**: Video Call Room.  
  * **/settings**: Team settings.

## **2\. Component Structure (Key Components)**

* AppLayout: Sidebar, Header, Notification Toast.  
* AuthGuard: Kiểm tra JWT, redirect nếu chưa login.  
* KanbanBoard: Dùng react-beautiful-dnd.  
* Whiteboard: Dùng HTML5 Canvas API \+ Socket.IO hooks.  
* VideoRoom: Dùng simple-peer hoặc WebRTC API wrapper.  
* ChatWidget: Floating chat box hoặc dedicated tab.

## **3\. State Management**

* **Global State (Redux Toolkit):**  
  * authSlice: User info, token.  
  * notificationSlice: Realtime noti queue.  
* **Server State (React Query):**  
  * Fetch danh sách Projects, Tasks, Users (Caching, Re-fetch on focus).  
* **Local State (useState/useRef):**  
  * Form inputs, Whiteboard drawing coordinates.

## **4\. UI/UX Standards**

* **Framework:** TailwindCSS.  
* **Theme:** Primary Color (Indigo-600), Error (Red-500).  
* **Responsive:** Mobile-first (ẩn Sidebar trên mobile).  
* **Loading:** Skeleton screens thay vì spinner xoay.

## **5\. Open Questions**

* \[ \] Thư viện nào để render PDF/Docx ngay trên trình duyệt (Resource viewing)?  
* \[ \] Xử lý mất kết nối mạng (Offline mode) cho Whiteboard thế nào?