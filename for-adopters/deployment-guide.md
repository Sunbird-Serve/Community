# Deployment Guide

### **1. Prerequisites**

Before deploying, ensure the following are set up:

* **Infrastructure**: Cloud (AWS, GCP, Azure) or On-Premises
* **Operating System**: Ubuntu 20.04+ or any Linux-based OS
* **Database**: PostgreSQL 12+
* **Java**: OpenJDK 17
* **Node.js**: v16+ (for UI service)
* **Nginx**: For reverse proxy and SSL termination
* **Docker & Kubernetes** (Optional but recommended for scaling)

***

### **2. Deployment Options**

#### **A. Single-Server Setup (For Testing & Pilots)**

✅ Best for small-scale pilots or sandbox environments.\
All services (backend, UI, database, and proxy) run on a **single EC2/VM instance**.

**Step 1: Install Dependencies**

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y openjdk-17-jdk postgresql nginx git curl
```

**Step 2: Setup PostgreSQL Database**

```bash
sudo -i -u postgres
psql
CREATE DATABASE serve_db;
CREATE USER serve_user WITH ENCRYPTED PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE serve_db TO serve_user;
\q
exit
```

**Step 3: Clone Sunbird Serve Repositories**

```bash
git clone https://github.com/Sunbird-Serve/sunbird-serve-need.git
git clone https://github.com/Sunbird-Serve/sunbird-serve-fulfill.git
git clone https://github.com/Sunbird-Serve/sunbird-serve-volunteering.git
git clone https://github.com/Sunbird-Serve/sunbird-serve-ui.git
```

**Step 4: Configure Backend (Spring Boot Services)**

*   Modify `application.properties` to set database details:

    ```properties
    propertiesCopyEditspring.datasource.url=jdbc:postgresql://localhost:5432/serve_db
    spring.datasource.username=serve_user
    spring.datasource.password=your_password
    ```
*   Build and run:

    ```bash
    bashCopyEditcd serve-backend
    ./mvnw clean install
    java -jar target/serve-backend.jar
    ```

**Step 5: Deploy Frontend (React UI)**

```bash
cd sunbird-serve-ui/src/main/frontend
npm install
npm start
```

*   Configure Nginx to serve the UI:

    ```bash
    sudo nano /etc/nginx/sites-available/serve
    ```

    Add the following:

    ```
    nginxCopyEditserver {
        listen 80;
        server_name yourdomain.com;

        root /path/to/serve-ui/build;
        index index.html;

        location / {
            try_files $uri /index.html;
        }

        location /api/ {
            proxy_pass http://localhost:8080/;
        }
    }
    ```

```bash
sudo ln -s /etc/nginx/sites-available/serve /etc/nginx/sites-enabled/
sudo systemctl restart nginx
```

***

#### **B. Multi-Server Deployment (For Scaling & Production)**

✅ Best for handling real-world traffic with **dedicated servers for backend, frontend, and database**.

**Step 1: Set Up Infrastructure**

* **Backend Server** (EC2/VM with Java & Spring Boot)
* **Frontend Server** (EC2/VM with Node.js & Nginx)
* **Database Server** (EC2/RDS with PostgreSQL)
* **Optional Load Balancer** (AWS ALB/Nginx for API traffic routing)

**Step 2: Configure PostgreSQL on Dedicated DB Server**

* Create a new PostgreSQL instance
*   Update `application.properties` on backend server:

    ```properties
    propertiesCopyEditspring.datasource.url=jdbc:postgresql://db-server-ip:5432/serve_db
    spring.datasource.username=serve_user
    spring.datasource.password=your_password
    ```

**Step 3: Deploy Backend on Dedicated Server**

```bash
scp serve-backend.jar user@backend-server-ip:/home/user/
ssh user@backend-server-ip
java -jar serve-backend.jar
```

**Step 4: Deploy Frontend on UI Server**

* Build UI on a separate instance
* Configure Nginx to serve frontend and route API calls

***

### **3. Deploying with Docker & Kubernetes (Recommended for Scaling)**

✅ Best for **scalable, containerized deployments** on **AWS ECS, GKE, AKS, or On-Prem Kubernetes**.

**Step 1: Create Docker Compose File**

```yaml
yamlCopyEditversion: '3.8'
services:
  postgres:
    image: postgres:12
    environment:
      POSTGRES_DB: serve_db
      POSTGRES_USER: serve_user
      POSTGRES_PASSWORD: your_password
    ports:
      - "5432:5432"

  backend:
    image: sunbird-serve/backend
    build: ./serve-backend
    environment:
      SPRING_DATASOURCE_URL: jdbc:postgresql://postgres:5432/serve_db
      SPRING_DATASOURCE_USERNAME: serve_user
      SPRING_DATASOURCE_PASSWORD: your_password
    ports:
      - "8080:8080"
    depends_on:
      - postgres

  frontend:
    image: sunbird-serve/frontend
    build: ./serve-ui
    ports:
      - "80:80"
```

```bash
bashCopyEditdocker-compose up -d
```

**Step 2: Deploy on Kubernetes**

Create a `deployment.yaml` file:

```yaml
yamlCopyEditapiVersion: apps/v1
kind: Deployment
metadata:
  name: serve-backend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: serve-backend
  template:
    metadata:
      labels:
        app: serve-backend
    spec:
      containers:
      - name: serve-backend
        image: sunbird-serve/backend
        ports:
        - containerPort: 8080
```

Apply deployment:

```bash
bashCopyEditkubectl apply -f deployment.yaml
```

***

### **4. Security & Monitoring Best Practices**

* **Enable HTTPS** using Certbot (Let's Encrypt)
* **Use Reverse Proxy (Nginx) to Secure APIs**
* **Enable Logging & Monitoring** with Prometheus + Grafana
* **Set Up Auto-Scaling** if using Kubernetes or cloud environments

***

### **5. Post-Deployment Steps**

✅ **Testing API & UI**

* Test UI: Open browser and access `http://yourdomain.com`

✅ **Monitor Performance**

* Use tools like **htop, Prometheus, or AWS CloudWatch**

✅ **Backup Strategy**

* Schedule **PostgreSQL backups**
* Implement **file & database replication**

***

### **6. Summary**

| Deployment Type | Recommended For | Complexity | Infra Required    |
| --------------- | --------------- | ---------- | ----------------- |
| Single Server   | Pilots, Testing | Low        | 1 VM              |
| Multi-Server    | Production      | Medium     | 3+ VMs            |
| Docker + K8s    | Large Scale     | High       | Cloud/K8s Cluster |

***
