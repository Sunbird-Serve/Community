# Data Security and Privacy

#### 1) Data Encryption and Key Management​

* Password Encryption –  Passwords are salted and the strengthened password is hashed using SHA 256 algorithm. ​
* Secure HTTP – Server is configured for SSL/TLS offload and the server instance is added to a security group that allows inbound HTTPS traffic.

#### 2) Data Access Control – Role Based Access Control​

Access Resource and Perform Actions –  Implements a Role-Based Access Control (RBAC) model, ensuring that users are granted access to resources and actions based on their assigned roles. Each of those permissions is associated with one or more roles/personas.&#x20;

#### 3) Data Visibility

Data visibility is controlled by associating roles with permissions. This means that dashboards and audit report generation are restricted based on the permissions associated with each role. This meticulous approach guarantees that sensitive data is accessible only to authorized personnel.

**4) Data Encryption in Transit and at Rest:**

**Data in Transit:** Every data exchange is by SSL/TLS encryption, forming a shield against unauthorized access throughout its network journey. To further elevate this encryption, installed SSL/TLS certificate directly on the MySQL server within the dedicated EC2 instance. This guarantees that information remains safeguarded and confidential at every step of its communication process.

**Data at Rest:** For data stored in the MySQL database on the dedicated EC2 instance, sensitive information like database passwords, host names, and secret keys are protected. This is achieved through the use of environment files and JSON secret files. These measures ensure that critical data remains inaccessible and secure.

#### 5) Data Backup

A storage volume snapshot of the DB instance is backed up and saved on Amazon S3 bucket. DB instance is automated on a daily basis. ​

#### 6) Session Management

Django session framework is used by enabling the session middleware class. Django session framework stores and retrieves data on a per-site-visitor basis. Django abstracts the process of sending and receiving cookies, by placing a session ID cookie on the client side, and storing all the related data on the server side. Django sessions framework is cookie-based, session IDs are not put in the URLs. ​

#### 7) Data Governance and Compliance

Users have appropriate access, control and visibility to their personal data.​

Protection of Children: Not collecting or saving data of children against identity tracing, tracking, labelling and discrimination.​

&#x20;A Non Disclosure Agreement is signed with the Volunteer that certain information will remain confidential, how we save the data and what rights volunteer have over the data.
