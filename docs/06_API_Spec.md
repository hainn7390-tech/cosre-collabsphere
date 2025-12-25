# **06\. API SPECIFICATION**

**Project:** CollabSphere (COSRE)

## **1\. General Conventions**

* **Base URL:** https://api.collabsphere.com/api/v1  
* **Auth Header:** Authorization: Bearer \<token\>  
* **Response Format:**  
  {  
    "data": { ... },  
    "meta": { "page": 1, "total": 100 },  
    "error": null  
  }

## **2\. Endpoint Details & Requirement Mapping**

### **Auth (FR-SEC-02)**

* POST /auth/login  
  * Req: {email, password}  
  * Res: {access\_token, refresh\_token, user\_info}  
* POST /auth/refresh

### **Projects (FR-PRO-01, FR-PRO-02)**

* GET /projects: List projects (Query params: class\_id, status).  
* POST /projects: Create project.  
* POST /projects/{id}/generate-milestones: **AI Feature**.  
  * Req: { "prompt\_context": "..." }  
  * Res: { "suggested\_milestones": \[...\] }

### **Teams (FR-TEAM-01)**

* POST /teams: Create team.  
* POST /teams/{id}/join: Join via code.  
* GET /teams/{id}/members.

### **Tasks (FR-WRK-01)**

* GET /teams/{id}/tasks.  
* PUT /tasks/{id}/move: Update status (Drag & Drop).  
  * Req: { "new\_status": "DONE", "index": 2 }

### **Evaluation (FR-EVA-01)**

* POST /evaluations: Submit grading.  
  * Req: { "target\_id": 10, "type": "PEER", "scores": {...} }

## **3\. Error Codes**

* 400: Bad Request (Validation failed).  
* 401: Unauthorized (Token expired/missing).  
* 403: Forbidden (Role not allowed).  
* 404: Not Found.  
* 429: Too Many Requests (Rate Limit).

## **4\. Open Questions**

* \[ \] API Documents sẽ dùng Swagger (OpenAPI) hay ReDoc?  
* \[ \] Giới hạn Rate Limit cho API AI là bao nhiêu request/phút?