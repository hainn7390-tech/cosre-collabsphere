# **03\. SYSTEM ARCHITECTURE**

**Project:** CollabSphere (COSRE)

## **1\. High-Level Architecture (C4 Container)**

graph TD  
    User((User Browser))  
      
    subgraph "Frontend Cloud (AWS)"  
        CDN\[CloudFront CDN\]  
        S3\[S3 Bucket \- React App\]  
    end  
      
    subgraph "Backend Cloud (Azure)"  
        AppService\[Azure App Service \- Linux\]  
        FastAPI\[FastAPI Container\]  
        SocketIO\[Socket.IO Manager\]  
    end  
      
    subgraph "Data & Services"  
        Postgres\[(Azure Database for PostgreSQL)\]  
        Redis\[(Upstash Redis \- Pub/Sub)\]  
        Cloudinary\[Cloudinary Media Store\]  
        Bedrock\[AWS Bedrock AI\]  
    end

    User \--\>|HTTPS/443| CDN  
    CDN \--\> S3  
    User \--\>|REST API & WSS| AppService  
    AppService \--\> FastAPI  
    AppService \--\> SocketIO  
      
    FastAPI \--\>|Query/Write| Postgres  
    FastAPI \--\>|Cache/Queue| Redis  
    FastAPI \--\>|GenAI| Bedrock  
    SocketIO \--\>|Adapter| Redis  
      
    User \--\>|Direct Upload| Cloudinary

## **2\. Technology Stack Selection**

| Layer | Technology | Rationale |
| :---- | :---- | :---- |
| **Frontend** | ReactJS \+ Vite \+ TailwindCSS | Hiệu năng cao, dev experience tốt, ecosystem lớn. |
| **Backend** | Python (FastAPI) | Async native (tốt cho I/O), dễ tích hợp AI/Data libs. |
| **Database** | PostgreSQL | Quan hệ chặt chẽ, hỗ trợ JSONB (cho Syllabus content). |
| **Realtime** | Socket.IO \+ Upstash Redis | Socket.IO xử lý fallback tốt; Redis làm Adapter để scale ngang. |
| **Video Call** | WebRTC (Mesh/PeerJS) | Miễn phí, peer-to-peer giảm tải cho server. |
| **AI** | AWS Bedrock | Truy cập các model mạnh (Claude/Titan) qua API chuẩn. |
| **Deploy** | Azure (BE) \+ AWS (FE) | Tận dụng gói Student Credits đa nền tảng. |

## **3\. Deployment Diagram**

* **Frontend:** Static build \-\> S3 \-\> Phân phối qua CloudFront (Global Edge).  
* **Backend:** Docker Image \-\> Azure Container Registry \-\> Azure Web App.  
* **Config:** Biến môi trường inject qua App Settings (Azure) và .env (Build time AWS).

## **4\. Open Questions**

* \[ \] Chiến lược backup DB: Dùng tính năng có sẵn của Azure hay cronjob dump ra S3?  
* \[ \] Cấu hình CORS chặt chẽ giữa tên miền AWS FE và Azure BE.