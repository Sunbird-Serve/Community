# Technical Requirements

#### **1. Infrastructure & Software Prerequisites**

| Component                                 | Recommended Specification                                                                        |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Compute (Servers/VMs/Cloud Instances)** | Minimum **4-core CPU, 8GB RAM** for small-scale deployments. Scale up based on concurrent users. |
| **Operating System**                      | Ubuntu 22.04 LTS (Recommended) or any Linux-based OS.                                            |
| **Database**                              | PostgreSQL 14+ (Required for registry and transactional data).                                   |
| **Application Stack**                     | Java (Spring Boot for microservices),                                                            |
| **Frontend**                              | React (for web-based UI)                                                                         |
| **Containerization (Optional)**           | Docker & Kubernetes (Recommended for large-scale deployments).                                   |
| **Reverse Proxy & Load Balancing**        | Nginx (for HTTPS termination & routing).                                                         |
| **Storage Requirements**                  | Minimum **100GB SSD** for logs, media files, and database storage.                               |
| **Message Queuing (Optional)**            | Kafka or RabbitMQ (For event-driven workflows).                                                  |
| **Authentication & Security**             | Firebase/Keycloak for user authentication. TLS encryption for secure communication.              |

***

#### **2. Scalability Considerations**

Sunbird SERVE is designed to scale efficiently based on usage demands. Consider the following when deploying at scale:

**🔹 Compute Scaling**

* **Small Deployments (1,000 users):**
  * A single instance with **4 vCPUs, 8GB RAM** running all services.
  * Postgres DB on the same machine (or separate for better performance).
* **Medium Deployments (10,000 users):**
  * **Separate DB instance** to handle transaction loads.
  * Multiple application instances with **horizontal scaling** using a load balancer.
* **Large Deployments (100,000+ users):**
  * **Microservices on separate servers/containers**.
  * **Auto-scaling groups** for API services using Kubernetes.
  * **CDN (Cloudflare, AWS CloudFront)** for frontend caching.

**🔹 Database Optimization**

* Use **connection pooling** for efficient DB access.
* Implement **read replicas** for high-read traffic.
* Use **partitioning** for large datasets (e.g., school data across states).

**🔹 API Rate Limiting**

* Use **API Gateway (Kong, AWS API Gateway)** to enforce rate limits.

**🔹 High Availability & Disaster Recovery**

* Deploy **across multiple regions/zones** to prevent downtime.
* Maintain **regular backups (daily DB snapshots, file storage backups)**.

***

#### **3. Recommended Deployment Models**

| Deployment Type                   | Best For                                 | Description                                                                 |
| --------------------------------- | ---------------------------------------- | --------------------------------------------------------------------------- |
| **Standalone (Single VM/Server)** | Small pilots, sandbox testing            | All components run on a single instance. Low cost but limited scalability.  |
| **Multi-VM Deployment**           | Medium-scale usage (10,000+ users)       | Separate instances for backend, database, and frontend. Better performance. |
| **Containerized with Kubernetes** | Large-scale deployments (100,000+ users) | Microservices run independently with auto-scaling and load balancing.       |
