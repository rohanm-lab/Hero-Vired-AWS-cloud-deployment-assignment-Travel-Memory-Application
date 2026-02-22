# Hero-Vired-AWS-cloud-deployment-assignment-Travel-Memory-Application
Created this repo for submission of Travel Memory Application Deployment using AWS Cloud

**Region:** ap-south-1 (Mumbai)  
**Deployed Using:** EC2 · Nginx · PM2 · ALB · ASG · Cloudflare · MongoDB Atlas  

---

## Overview  
This project is a full MERN-stack deployment of the **TravelMemory** application using AWS Cloud services.  
The architecture includes:

- Separate **frontend** and **backend** EC2 tiers  
- **Nginx** reverse proxy for both frontend (React) & backend (Node.js/Express)  
- **PM2** for backend Node.js process management  
- **Application Load Balancer (ALB)**  
- **Auto Scaling Groups (ASG)** with Launch Templates  
- **Path-based routing**  
  - `/` → Frontend  
  - `/trip*` → Backend API  
- **Cloudflare DNS** with a custom domain  
- **MongoDB Atlas** as the managed database  

---

## Final Deployed URLs  
| Component | URL |
|----------|-----|
| Frontend via ALB + Cloudflare | **http://app.rohanmangate.online/** |
| Backend API via ALB | **http://app.rohanmangate.online/trip** |
| Direct Frontend EC2 Instance | **http://frontend.rohanmangate.online/** |

---

## Architecture Summary  
- **Cloudflare** manages DNS  
  - CNAME: `app` → ALB DNS  
  - A Record: `frontend` → Single frontend EC2  
- **ALB (Application Load Balancer)**  
  - Listener: HTTP:80  
  - Rules:  
    - `/` → `tg-frontend`  
    - `/trip*` → `tg-backend`
- **Target Groups**  
  - `tg-frontend` (health check `/`)  
  - `tg-backend` (health check `/trip`)
- **Auto Scaling Groups**  
  - `asg-frontend` (Launch Template: `lt-frontend v2`)  
  - `asg-backend` (Launch Template: `lt-backend v1`)
- **EC2 Instances**  
  - Frontend: Nginx serving React build  
  - Backend: Nginx proxy → Node.js (PM2) on port 3001  
- **MongoDB Atlas** stores trip experiences  

**Full architecture diagram included in the PDF submission.**

---

##  Repository Contents  
- `README.md` — You are reading it  
- `TravelMemory_Submission_Captioned+Diagram_v2.pdf` — (All screenshots and documentation are provided in this documentation) 
- `Deployment architecture diagram.drawio.png` — Architecture diagram (PNG)  
- `architecture.drawio` — Raw draw.io file

---
I deployed the TravelMemory MERN application on AWS using an enterprise-grade architecture:
• Created separate EC2 instances for frontend (React + Nginx) and backend (Node.js + Express + PM2).
• Configured Nginx reverse proxy for both tiers.
• Connected MongoDB Atlas using MONGO_URI.
• Set up an Application Load Balancer (ALB) with path-based routing:
– “/” → tg-frontend
– “/trip*” → tg-backend
• Created Launch Templates for both frontend and backend.
• Configured Auto Scaling Groups (ASG) with desired/min/max = 2/2/4 for high availability.
• Locked down Security Groups using best practices (alb-sg → frontend-sg → backend-sg).
• Purchased a domain (rohanmangate.online) from Hostinger and integrated Cloudflare DNS:
– CNAME (app) → ALB DNS
– A record (frontend) → Frontend EC2
• Verified final URLs:
– http://app.rohanmangate.online/ (Frontend UI via ALB)
– http://app.rohanmangate.online/trip (Backend API via ALB)
– http://frontend.rohanmangate.online/ (Direct frontend EC2)
• Successfully validated health checks, scaling, routing, and Cloudflare propagation.
• Attached documentation PDF and architecture diagram as required.
This submission includes the complete deployment report, screenshots, architecture diagram, and verification checks.
