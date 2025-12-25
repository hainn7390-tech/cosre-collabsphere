# **07\. REALTIME COLLABORATION SPECIFICATION**

**Project:** CollabSphere (COSRE)

## **1\. Architecture: Socket.IO \+ Redis**

* **Server:** FastAPI mount python-socketio.  
* **Message Broker:** Redis (Upstash) dùng để Pub/Sub events giữa các instances backend (khi scale nhiều node).  
* **Client:** socket.io-client (React).

## **2\. Namespaces & Rooms**

* **Namespace:** /workspace  
* **Rooms:** team\_{teamId} (VD: team\_101).  
* **Flow:**  
  1. User vào Workspace \-\> Emit join\_room({ room: 'team\_101' }).  
  2. Server add socketID vào room.  
  3. User thoát \-\> Emit leave\_room.

## **3\. Events Catalogue (FR-COL-01, FR-COM-01)**

| Event Name | Direction | Payload | Description |
| :---- | :---- | :---- | :---- |
| chat:send | C \-\> S | {msg, type} | Gửi tin nhắn. |
| chat:receive | S \-\> C | {msg, sender, time} | Broadcast tin nhắn cho room. |
| wb:draw | C \-\> S | {x0, y0, x1, y1, color} | Gửi nét vẽ (vector). |
| wb:sync | S \-\> C | {x0, y0, ...} | Broadcast nét vẽ cho người khác. |
| signal:offer | C \-\> S | {sdp, target} | WebRTC Signaling (Video call). |
| signal:answer | C \-\> S | {sdp, target} | WebRTC Signaling. |
| task:update | S \-\> C | {taskId, status} | Noti khi có ai kéo task. |

## **4\. Conflict Resolution (Whiteboard)**

* **Strategy:** Last Write Wins (LWW) đơn giản cho MVP.  
* **Future:** CRDT (Conflict-free Replicated Data Types) cho phiên bản nâng cao (Yjs).

## **5\. Open Questions**

* \[ \] Lưu lại trạng thái Whiteboard (snapshot) vào DB bao lâu một lần? (Hiện tại: Khi user rời phòng hoặc mỗi 5 phút).  
* \[ \] Giới hạn số người trong 1 phòng Video Call (Mesh topology tốn băng thông client)? (Khuyến nghị: Max 6-8 pax).