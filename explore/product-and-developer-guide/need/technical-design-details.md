# Technical Design Details

## **Overview**

A microservice that manages Need types, Need, Need plan creation, and Need deliverable management is a small, independent component of a larger software system that is responsible for handling the functionality related to the creation and management of various types of needs. This microservice provides a modular and scalable approach to managing needs, which can be customized to fit the specific needs of the organization. It allows for efficient management of different types of needs, and provides the ability to create and manage a plan to fulfill those needs, including the management of deliverables. By breaking down the functionality into separate microservices, it allows for greater flexibility and agility in the software development process, as changes can be made to individual components without affecting the entire system.



### Services

In a software system that manages the creation, tracking, and delivery of various types of needs, three distinct services are utilized to provide a comprehensive and modular approach to the process.

#### 1) Search & Discovery Service

Responsible for allowing users to search for and discover relevant information about different types of needs. This service enables users to easily navigate and find the specific needs they are looking for.

#### 2) Need Service

Is the core service responsible for managing the different types of needs. This service provides the ability to create and manage needs, need type and need plans to fulfill those needs.&#x20;

#### 3) Need Deliverables Service

Responsible for managing the delivery of the various deliverables associated with the fulfillment of needs. This service provides a streamlined and efficient approach to managing the creation, tracking, and delivery of deliverables



## Technical Design Details for the Need Microservice

<figure><img src="../../../.gitbook/assets/Need_Microservice_Architecture.drawio (1).png" alt=""><figcaption></figcaption></figure>

**Microservice Architecture**:&#x20;

The Need Management microservice follows a microservices architecture, ensuring loose coupling and independent scalability. It is built using a lightweight framework or technology stack suitable for microservice development - Spring Boot.

This microservice also integrates with Sunbird RC for registration of needs and need type which is next gen electronic registry.&#x20;

**RESTful API**

The microservice exposes a RESTful API that allows other components and services to interact with it. The API adheres to REST principles, providing endpoints for creating, retrieving, updating, and deleting needs, as well as managing plans and deliverables associated with those needs.

**Database Integration**

Need Registry, Need Type and Entity Registry are created in the postgres db of RC instance. The microservice also integrates with a dedicated database or a portion of the larger database system. It utilizes a database management system, such as MongoDB. The schema design is optimized to support the specific requirements of need types, plans, deliverables, and associated metadata.

All the transactional data will be saved in the serve db. \


**Authentication and Authorization**

The microservice incorporates Keycloak for authentication and authorization. Keycloak handles user authentication using various mechanisms and issues access tokens upon successful authentication. The microservice enforces access control based on assigned roles and permissions defined in Keycloak. Token management, including validation and expiration, is implemented to ensure secure communication. By integrating Keycloak, the microservice ensures secure access control, protects sensitive data, and enforces authorization policies.

**Event-Driven Architecture**

The Need Management microservice embraces an event-driven architecture to facilitate real-time updates and decoupled communication between components. It utilizes a message broker, such as Apache Kafka, to publish and subscribe to relevant events related to need creation, plan updates, and deliverable management. This allows for efficient distribution of messages and asynchronous processing.

**Monitoring and Logging**

The microservice implements comprehensive monitoring and logging mechanisms to track its performance and detect anomalies through Sunbird Telemetry.&#x20;
