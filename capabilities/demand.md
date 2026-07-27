---
description: Contains capabilities around the Need that are required to be fulfilled
---

# Need Management

_**Personas Involved in this capability:**_

* **Super Admin:** An actor who sets up and configures the initial parameters of the System, including nAdmin and vAdmin.&#x20;
* _**n**_**Admin**: An actor who owns, decides and manages a set of Needs and nCoordinators.&#x20;
* **nCoordinator**: An actor who publishes the Need, enables the Discovery and Delivery by the Volunteer.&#x20;

_**Actions Performed by Various Personas for Demand Capability:**_

* Super Admin attests the need agency and authorize need Admin.&#x20;
* Anyone can register themselves as nAdmin who registers need actors and assigns need Coordinators. Furthermore, nAdmin defines the Need Entity. The Need Entity can be pulled from the master data/registry or from the need defined by the nAdmin.&#x20;
* nCoordinator onboards the agency and raise the needs from the Need Entity.&#x20;

<figure><img src="https://lh6.googleusercontent.com/u15zqOrpoTmPl9pWpRqZ0aBaAGpiXrvh4sLqO-m_ddM4o0W0d6afTBXmR1Qf3pDLnPqHW5C6jymBMsdAGZ2aQjQeQE2mSd2ORf9IgdW6bojQN7-EZohcMvH0nM3wu7hz7m7RHqYwFFIZy02PfR8Q3GMg6F6xfMa0QDrIFHDjAONraHQLMZe7Sim7" alt=""><figcaption></figcaption></figure>



<table><thead><tr><th width="124.33333333333334">Milestone</th><th width="151">Persona</th><th>Usecase</th><th>Release</th></tr></thead><tbody><tr><td>M1</td><td>nCoordinator</td><td>logs in</td><td>Vriddhi - release-1.0.0.0- Completed</td></tr><tr><td></td><td>nCoordinator</td><td>View Needs</td><td>Vriddhi - release-1.0.0.0- Completed</td></tr><tr><td></td><td>nCoordinator</td><td>View Approved needs</td><td>Vriddhi - release-1.1.0.0- Completed</td></tr><tr><td></td><td>nCoordinator</td><td>View unapproved needs</td><td>Vriddhi - release-1.1.0.0- Completed</td></tr><tr><td></td><td>nCoordinator</td><td>Raise Needs</td><td>Vriddhi - release-1.0.0.0- Completed</td></tr><tr><td></td><td>nCoordinator</td><td>View Need Types</td><td>Vriddhi - release-1.2.0.0- Completed</td></tr><tr><td></td><td>nCoordinator</td><td>Receiving Notification (email)</td><td>Vriddhi - release-2.1.0.0- Completed</td></tr><tr><td>M2</td><td>nCoordinator</td><td>Edit Need details</td><td>Vriddhi - release-3.1.0.0- Completed</td></tr><tr><td></td><td>nAdmin</td><td>logs in</td><td>Vriddhi - release-3.1.0.0- Completed</td></tr><tr><td></td><td>nAdmin</td><td>View Needs</td><td>Vriddhi - release-3.1.0.0- Completed</td></tr><tr><td></td><td>nAdmin</td><td>Approve Needs</td><td>Vriddhi - release-3.2.0.0- </td></tr><tr><td></td><td>nAdmin</td><td>View Entitites</td><td>Vriddhi - release-3.1.0.0- Completed</td></tr><tr><td></td><td>nAdmin</td><td>Add and Register Entity</td><td>Vriddhi - release-3.2.0.0- </td></tr><tr><td></td><td>nAdmin</td><td>Assign nCoordinators</td><td>Vriddhi - release-3.2.0.0- </td></tr><tr><td></td><td>Serve Admin</td><td>Create Need Agency</td><td>Vriddhi - release-3.2.0.0- Completed</td></tr><tr><td></td><td>Serve Admin</td><td>Assign nAdmin to Agency</td><td>Vriddhi - release-3.2.0.0- </td></tr><tr><td></td><td>Serve Admin</td><td>Add Entity and Assign Entity</td><td>Vriddhi - release-3.2.0.0- </td></tr><tr><td></td><td>nCoordinator</td><td>Onboard Entity</td><td>Vriddhi - release-3.2.0.0- </td></tr><tr><td>M3</td><td>Volunteer</td><td>Mark interested needs</td><td></td></tr><tr><td></td><td>nCoordinator</td><td>Raise request for New Need Type</td><td></td></tr><tr><td></td><td>nAdmin</td><td>Create Need Type</td><td></td></tr><tr><td></td><td>System</td><td>Notifications</td><td></td></tr><tr><td></td><td>nAdmin</td><td>Taxonomy</td><td></td></tr><tr><td></td><td>nAdmin</td><td>Need Requirement </td><td></td></tr></tbody></table>

#### Entity Onboarding and Need-Raising Workflow

<figure><img src="../.gitbook/assets/Entity Onboard.png" alt=""><figcaption></figcaption></figure>

Schools and colleges are preloaded in the SERVE registry using the authorised government entity list. From the adopter's website, a prospective coordinator selects **Onboard School/College** and completes a simple activation form.

The user selects their entity and provides basic details such as name, mobile number, email, designation, and minimum infrastructure-readiness information. Submitting the form creates a **pending coordinator request,** it does not immediately grant access to the institution.

&#x20;`nAdmin`  reviews the request. nAdmin may authorise it, request clarification, or reject it when the entity association cannot be verified. On authorisation, the system creates the user as an `nCoordinator`, maps them to the selected entity, and marks the entity as active.

The coordinator then receives an activation message containing two ways to continue:

* **SERVE portal:** The nCoordinator uses a secure password-setup link, logs in, and finds the entity already mapped to their account.
* **WhatsApp:** The coordinator sends “Hi” from the registered mobile number. The system recognises the user and begins with the correct entity context.

In either channel, the nCoordinator can proceed to raise and manage a requirement with assistance from the **Need Agent**. The nCoordinator is therefore not required to understand SERVE roles, entity onboarding, or the underlying platform workflow.
