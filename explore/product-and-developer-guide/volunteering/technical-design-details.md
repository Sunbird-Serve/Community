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
