# 🚀 Enterprise DevOps CI/CD Pipeline for Cloud-Based Node.js Application 

## 📖 Project Overview
To design and implement a secure, automated, and scalable DevOps CI/CD pipeline for deploying a Node.js application on AWS EC2, using Jenkins for CI/CD, NGINX as a reverse proxy, PM2 for process management, DuckDNS for domain mapping, and Linux monitoring tools to ensure application reliability and observability.

# The implementation covers:

CI/CD automation using Jenkins

Secure Jenkins access using Matrix-based security

Application deployment using NGINX reverse proxy

Process management with PM2

Domain mapping using DuckDNS

System and application monitoring

# 🧰 Tech Stack

Cloud: AWS EC2 (Ubuntu)

Language: Node.js

CI/CD: Jenkins

Web Server: NGINX

Process Manager: PM2

Domain: DuckDNS

Version Control: Git & GitHub

Monitoring: top, htop, sysstat

OS: Linux (Ubuntu)

# 🏗️ Application Architecture

Client
  ↓
DuckDNS Domain
  ↓
NGINX (Port 80)
  ↓
Node.js Application (Port 3000 via PM2)


# ✅ Task-wise Implementation
🔹 Task 1: Application Setup

Cloned Node.js repository from GitHub

Installed dependencies using npm install

Verified application execution using example server

🔹 Task 2: CI/CD Pipeline using Jenkins

Installed Jenkins on Linux EC2

Created CI/CD pipeline using Jenkinsfile

Integrated GitHub repository

Automated build and deployment process
<img width="1327" height="1935" alt="image" src="https://github.com/user-attachments/assets/901ecab0-ac99-41e4-8ac9-c68b9c1fe3e2" />


🔹 Task 3: Jenkins Security

Enabled Matrix-based security

Created admin and developer users

Assigned role-based permissions

Restricted anonymous access

🔹 Task 4: Deployment using NGINX & DuckDNS

Node.js application managed using PM2

NGINX configured as reverse proxy

DuckDNS domain mapped to EC2 public IP

Application accessible via:

http://devlogin-dj.duckdns.org

# 📄 NGINX Configuration
server {
    listen 80;
    server_name devlogin-dj.duckdns.org;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
    }
}

🔹 Task 5: Monitoring

CPU & memory monitoring using top / htop

Application monitoring using PM2

Disk monitoring using df -h

Verified Jenkins and NGINX service health

# 📂 Scripts (Task 6 Requirement)

All scripts are stored in the scripts/ directory.

## 📄 scripts/install-jenkins.sh
#!/bin/bash
sudo apt update
sudo apt install -y openjdk-17-jdk
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install -y jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins

## 📄 scripts/install-node-pm2.sh
#!/bin/bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
sudo npm install -g pm2

## 📄 scripts/install-nginx.sh
#!/bin/bash
sudo apt update
sudo apt install -y nginx
sudo systemctl start nginx
sudo systemctl enable nginx

## 📄 scripts/duckdns.sh
#!/bin/bash
curl "https://www.duckdns.org/update?domains=devlogin-dj&token=YOUR_TOKEN&ip="

## 📄 scripts/monitoring.sh
#!/bin/bash
echo "CPU & Memory Usage"
top -bn1 | head -20

echo "Disk Usage"
df -h

echo "PM2 Status"
pm2 status

# 📁 Configuration Files

Jenkinsfile – Jenkins CI/CD pipeline

NGINX reverse proxy configuration

PM2 process configuration

## 📸 Screenshots

The screenshots/ directory contains:

# Instance 
<img width="1618" height="495" alt="image" src="https://github.com/user-attachments/assets/d228e472-6e9b-406c-a538-ca1c2f780ce4" />
<img width="1618" height="712" alt="image" src="https://github.com/user-attachments/assets/1fae9013-8638-4bff-b937-2a9fb95148ad" />

# Terminal 
<img width="1142" height="730" alt="image" src="https://github.com/user-attachments/assets/d1cb28b5-6bdf-4ae3-a396-552982b10906" />
<img width="1901" height="703" alt="image" src="https://github.com/user-attachments/assets/47db683f-d1d7-4d2f-803f-b6992577313c" />
<img width="1440" height="677" alt="image" src="https://github.com/user-attachments/assets/7a8ed93e-0a59-45ee-8dbb-818749f819dd" />
<img width="1580" height="548" alt="image" src="https://github.com/user-attachments/assets/6f37af00-3009-426d-af3c-b6ee4acc1497" />
<img width="1825" height="680" alt="image" src="https://github.com/user-attachments/assets/96cd3ab2-fb6b-48d2-95a0-69af05be6242" />
<img width="1132" height="688" alt="image" src="https://github.com/user-attachments/assets/d8efc14e-9184-4352-9da2-85cb2b3c4c23" />

# Jenkins pipeline success
<img width="1911" height="872" alt="image" src="https://github.com/user-attachments/assets/9e390e92-76dd-4dcf-8335-1ab0f19da651" />
<img width="1918" height="875" alt="image" src="https://github.com/user-attachments/assets/66c91677-59a5-4fb7-a69c-6c08ec1d8e88" />
<img width="652" height="1156" alt="image" src="https://github.com/user-attachments/assets/e6406b8d-1cd8-4916-aa7f-e12f90247044" />
<img width="1418" height="24627" alt="image" src="https://github.com/user-attachments/assets/af313eab-d158-4bdb-851c-ff40d533c940" />

# Jenkins user configuration
<img width="1920" height="878" alt="image" src="https://github.com/user-attachments/assets/082c2bf6-e357-4980-bd98-acf487c08cde" />
<img width="1918" height="3753" alt="image" src="https://github.com/user-attachments/assets/0eb3747a-81ba-4890-9411-1afbb2305882" />
<img width="1903" height="1465" alt="image" src="https://github.com/user-attachments/assets/d1af0ed1-c2fc-4fce-8555-d4f0879fed18" />


# Application running via DuckDNS domain
<img width="895" height="1392" alt="image" src="https://github.com/user-attachments/assets/0add9df2-fe9d-412d-9dd3-22beb00f7dfd" />
<img width="1920" height="937" alt="image" src="https://github.com/user-attachments/assets/79f3be24-8875-4944-a9de-9e31b38224d8" />


# Monitoring outputs (top, pm2 status, df -h)
<img width="1835" height="596" alt="image" src="https://github.com/user-attachments/assets/47b03da7-e3da-46c4-8f49-5de4b76fd333" />
<img width="996" height="597" alt="image" src="https://github.com/user-attachments/assets/ae25876b-8028-4f6a-9240-aa6479ec5ac3" />
<img width="1105" height="623" alt="image" src="https://github.com/user-attachments/assets/a74fae34-3402-4e62-a991-939f5c143257" />


## 🔗 Application Access
http://devlogin-dj.duckdns.org
<img width="1920" height="937" alt="image" src="https://github.com/user-attachments/assets/af05d0c8-4d8d-48e7-b324-568ae033f9a6" />


# 🎯 Key DevOps Concepts Demonstrated

CI/CD Automation

Role-Based Access Control (RBAC)

Reverse Proxy Architecture

Process Management with PM2

Cloud Deployment (AWS EC2)

Domain Management (DuckDNS)

System & Application Monitoring

## 🏁 Conclusion

This project demonstrates a production-style DevOps workflow including automation, security, deployment, domain configuration, and monitoring.
