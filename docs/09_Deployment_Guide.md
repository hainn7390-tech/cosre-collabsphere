# **09\. DEPLOYMENT GUIDE**

**Project:** CollabSphere (COSRE)

## **1\. Infrastructure Overview**

* **Backend:** Azure App Service (Docker Container).  
* **Frontend:** AWS S3 (Hosting) \+ CloudFront (CDN/SSL).  
* **Database:** Azure Database for PostgreSQL.  
* **Cache:** Upstash Redis (Serverless).  
* **Media:** Cloudinary (SaaS).

## **2\. Environment Variables (.env)**

### **Backend**

DATABASE\_URL=postgresql://user:pass@host:5432/db  
SECRET\_KEY=your\_jwt\_secret  
ALGORITHM=HS256  
AWS\_ACCESS\_KEY\_ID=xxx (For Bedrock)  
AWS\_SECRET\_ACCESS\_KEY=yyy  
AWS\_REGION=us-east-1  
CLOUDINARY\_URL=cloudinary://key:secret@cloud  
REDIS\_URL=redis://default:pass@upstash-url:6379

### **Frontend**

VITE\_API\_URL=\[https://cosre-api.azurewebsites.net\](https://cosre-api.azurewebsites.net)  
VITE\_SOCKET\_URL=\[https://cosre-api.azurewebsites.net\](https://cosre-api.azurewebsites.net)

## **3\. Deployment Steps**

### **Backend (Azure)**

1. Build Docker Image: docker build \-t cosre-be .  
2. Push to ACR: docker push myregistry.azurecr.io/cosre-be  
3. Config App Service: Set DOCKER\_REGISTRY\_SERVER\_URL, etc.  
4. Restart App Service.

### **Frontend (AWS)**

1. Build Static: npm run build \-\> Output folder dist/.  
2. Sync S3: aws s3 sync ./dist s3://my-cosre-bucket \--delete  
3. Invalidate CloudFront: aws cloudfront create-invalidation ...

## **4\. CI/CD Pipeline (GitHub Actions)**

* **On Push Main:**  
  * Run Lint & Unit Tests.  
  * Nếu Pass \-\> Build Docker \-\> Push ACR.  
  * Trigger Webhook deploy Azure.  
  * Build React \-\> Sync S3.

## **5\. Open Questions**

* \[ \] Cấu hình Domain custom (VD: www.cosre.edu.vn) và SSL Certificate.  
* \[ \] Chi phí dự kiến hàng tháng? (Azure Student Tier \+ AWS Free Tier).