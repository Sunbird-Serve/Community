# Data Security and Privacy

#### Data Encryption and Key Management​

* Password Encryption –  Passwords are salted and the strengthened password is hashed using SHA 256 algorithm. ​
* Secure HTTP – Server is configured for SSL/TLS offload and the server instance is added to a security group that allows inbound HTTPS traffic.

#### Data Access Control – Role Based Access Control​

* Access Resource and Perform Actions –  Implements a Role-Based Access Control (RBAC) model, ensuring that users are granted access to resources and actions based on their assigned roles.ach of those permissions is associated with one or more roles/personas.  Each role is associated with specific permissions, meticulously crafted to govern data access and actions performed within the platform.
* Data Visibility  - Dashboards or audit report generation are restricted based on the permission associated for each role.

#### Data Protection

* Data on Move - Amazon RDS creates an SSL/TLS certificate and installs the certificate on the DB instance when Amazon RDS provisions the instance. Amazon RDS for MySQL supports Transport Layer Security.   ​
* Data in Use and Rest – Environment files and .json secret files are used to protect and store database password, host name and secret keys. ​

#### Data Backup

Through Amazon RDS service automated backups of the DB instance is created and saved during the back up window. A storage volume snapshot of the DB instance is backed up and saved on Amazon S3 bucket. DB instance is automated on a daily basis. ​

#### Session Management

Django session framework is used by enabling the session middleware class. Django session framework stores and retrieves data on a per-site-visitor basis. Django abstracts the process of sending and receiving cookies, by placing a session ID cookie on the client side, and storing all the related data on the server side. Django sessions framework is cookie-based, session IDs are not put in the URLs. ​

#### Data Governance and Compliance

Users have appropriate access, control and visibility to their personal data.​

Protection of Children: Not collecting or saving data of children against identity tracing, tracking, labelling and discrimination.​

&#x20;A Non Disclosure Agreement is signed with the Volunteer that certain information will remain confidential, how we save the data and what rights volunteer have over the data.
