# Technical Design Details

## **Overview**

The Volunteer Management service facilitates the registration, profile management and scheduling of volunteers to fulfill identified needs. The Agency Management service handles agency registration, profile management and reporting to ensure effective coordination of volunteering efforts. The User Management service manages various users like nAdmin, nCoordinator, vAdmin and vCoordinator, while the Credentialing service manages the verification and expiration of volunteer credentials. Together, these microservices form a cohesive system that enables seamless volunteer engagement, agency coordination, and user management within the larger volunteering software system.

### Services

#### 1) Volunteer Management Service

Provides an endpoint for users to register as volunteers, capturing their personal information such as name, contact details, and skills. Also, allows volunteers to update their profile information, add or remove skills, and specify their availability.

#### 2) Agency Management Service

Allows agencies or organizations to register within the system, providing their details such as name, contact information, and areas of expertise.  Provides functionality for agencies to update their profile information and specify their service offerings.

#### 3) User Management Service

Responsible for managing various users like nAdmin, nCoordinator, vAdmin and vCoordinator and their roles.&#x20;

## Technical Design Details for the Volunteering Microservice

<figure><img src="../../../.gitbook/assets/Volunteering MS.drawio.png" alt=""><figcaption></figcaption></figure>

**Microservice Architecture**:&#x20;

The Volunteering microservice follows a microservices architecture, ensuring loose coupling and independent scalability. It is built using a lightweight framework or technology stack suitable for microservice development - Spring Boot.

This microservice integrates with Sunbird RC for registration of Volunteers, Agency and other Users.&#x20;

**API**

The Volunteering Microservice exposes a RESTful API that follows REST principles. It provides endpoints for creating, retrieving, updating, and deleting volunteers, agencies, and users. For example, endpoints like `/volunteers`, `/agencies`, and `/users` handle creating new resources, while endpoints like `/volunteers/{id}`, `/agencies/{id}`, and `/users/{id}` retrieve, update, or delete specific resources. The API uses standard HTTP verbs such as GET, POST, PUT/PATCH, and DELETE to perform CRUD operations on these resources, with request payloads and response data represented in formats like JSON or XML.

**Authentication and Authorization**

The Volunteering microservice incorporates authentication and authorization mechanisms to ensure secure access and protect sensitive data. It integrates with Keycloak, an open-source identity and access management solution, for authentication and authorization. Keycloak handles user authentication, supports various authentication mechanisms, and issues access tokens. The microservice enforces access control based on roles and permissions defined in Keycloak, allowing only authorized users to interact with the Volunteering functionality, such as managing volunteers, agencies, and user accounts. Token management, including validation, expiration, and revocation, is implemented to enhance secure communication between the microservice and Keycloak. By integrating Keycloak, the Volunteering microservice ensures secure access control, protects sensitive data, and enforces fine-grained authorization policies for managing volunteering-related operations.

**RC Instance**

* Database: The Registry instance has its own dedicated database to store data related to volunteers, agencies, users and any other relevant information.
* API Layer: Exposes a set of APIs specifically designed to interact with the Volunteering Microservice. These APIs handle database operations, such as CRUD (Create, Read, Update, Delete) operations, data retrieval, and modification.
* Data Persistence: The Registry instance ensures the durability and reliability of the data by implementing appropriate database technologies and data backup strategies.
* Database Schema Design: Defines the database schema to efficiently store and retrieve data, considering factors such as data relationships, indexing, and query optimization.

**Database Integration**

The microservice integrates with a dedicated database or a portion of the larger database system. It utilizes a database management system, such as MongoDB, to store and retrieve need-related data efficiently. The schema design is optimized to support the specific requirements of need types, plans, deliverables, and associated metadata.

All the transactional data will be saved in the serve db.&#x20;

**Monitoring and Logging**

The microservice implements comprehensive monitoring and logging mechanisms to track its performance and detect anomalies.
