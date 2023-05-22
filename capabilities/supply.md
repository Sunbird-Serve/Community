---
description: Contains capabilities around Volunteers as Serve entities to be managed
---

# Volunteer Management

_**Personas Involved in this capability:**_

* **System Admin:** An actor who sets up and configures the initial parameters of the System, including nAdmin and vAdmin.&#x20;
* **Volunteer:** An actor who participates to volunteer by nominating and fulfilling the demand.&#x20;
* **vAdmin**: An actor who owns, decides and manages a set of Volunteers and vCoordinators.&#x20;
* **vCoordinator**: An actor who manages the Volunteer’s life cycle.&#x20;

_**Actions Performed by Various Personas for Supply Capability:**_

* vAdmin attests the volunteer agency and authorize vAdmin.&#x20;
* Volunteer Registers self via vRC component.&#x20;
* vAdmin registers the Volunteer Agency and assigns vCoordinators.&#x20;
* vCoordinators registers self and attest Volunteers.&#x20;

<figure><img src="https://lh4.googleusercontent.com/lv3OI0dzyCaq8u5fgpmNul0DnCH0wvh2SFb9DYKFz-S4SlwLP9gY8QRv5YvVVN3YbbcDZSCxTpw-SPhDxt0ZkS2BtmZ0uS3e_nOjuyn44Q-L9yZgTt0emMzZVzr4AkiKsJKrSyjLLGM5UwJp7UarWpDLyq8ImlrWsDanlZrunoakVHms9b3jD0nu" alt=""><figcaption></figcaption></figure>



| Milestone  | Persona      | Usecase                     |
| ---------- | ------------ | --------------------------- |
| M1         | vCoordinator | Login                       |
|            | vCoordinator | view registered volunteers  |
|            | Volunteer    | Login                       |
|            | Volunteer    | Register                    |
| M2         | vCoordinator | Check onboard status        |
|            | vCoordinator | Complete onboarding process |
|            | vCoordinator | Update the status           |
|            | vCoordinator | Onboard Refresh             |
|            | vCoordinator | Receiving Notification      |
| M1         | System       | Notification                |
