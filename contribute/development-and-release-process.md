# Development & Release Process

## Overview

This document acts as a guide for new contributors, providing them with an overview of the project, its goals, and the development process. It helps them understand how to get started, contribute effectively, and adhere to the project's guidelines and standards.

Kindly go through [Sunbird Community Contribution Practice Ver1.0](https://docs.google.com/document/d/1ulBgZW-UthdK75BssIfKCUNk3tyv5NeSRUxRO7hZ-qY/edit) document for detailed contribution guidelines and practice.&#x20;

## Development Process

### **Step 1**: **Design, Estimate and Plan the development process**

Design artifacts play a crucial role in visualizing the system architecture, defining service contracts and APIs, and designing database schemas. Functional design involves creating use case diagrams, sequence diagrams, and domain models to outline the interactions, behavior, and data structures of microservices. Technical artifacts include individual code repositories, API gateway configurations, deployment scripts, message formats, service discovery mechanisms, containerization files, and infrastructure requirements. These artifacts serve as documentation and references for development teams, ensuring consistency, facilitating collaboration, and guiding the implementation of microservices. Kindly check the [Product & Developer Guide](../explore/product-and-developer-guide/) to access all the required artifacts.&#x20;

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### **Step 2: Code, Merge and Test Process**

**Code Development:**&#x20;

* Identify the task or feature to be implemented or the bug to be fixed.&#x20;
* Create a new branch from the main development branch (e.g., "develop").&#x20;
* Write code to implement the desired functionality or fix the bug following coding best practices and coding standards - [Click here](https://docs.google.com/document/d/1aoj6cSgQ5uziLqsvG4oGzh3bhNHh5khe4pk\_lGh10BU/edit).&#x20;
* Test the code locally to ensure it functions as expected. e. Commit changes to the local branch with descriptive commit messages.

**Code Review:**&#x20;

* Raise a pull request to initiate the code review and merge process.
* Reviewers examine the code changes for correctness, adherence to coding standards, potential bugs, and overall quality.&#x20;
* Address any feedback or suggested improvements by making necessary modifications to the code.&#x20;
* Iterate the review process if needed until the code meets the required standards and receives approval.

**Code Merge:**&#x20;

* Ensure the code branch is up-to-date with the latest changes from the main development branch.&#x20;
* Resolve any conflicts that may arise due to overlapping changes.&#x20;
* Once the code review process is complete and approved, merge the branch into the release-version branch.&#x20;
* Run local tests on the merged code to ensure its stability and compatibility with the existing codebase.&#x20;

**Continuous Integration and Deployment:**&#x20;

* Integrate the code changes into the main development branch using a continuous integration (CI) system.&#x20;
* The CI system automatically builds and tests the code to ensure it remains stable and compatible with the existing codebase.&#x20;
* If all tests pass successfully, the CI system can trigger the deployment process to move the code changes to staging environments.

**Documentation and Reporting:**&#x20;

* Update relevant documentation, such as user guides or API documentation, to reflect any changes or new features introduced.&#x20;
* Generate reports summarizing the code changes, test results, and any issues or fixes made during the process.&#x20;
* Share the reports with the development team, stakeholders, or clients for visibility and transparency.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### **Step 3: Defects Identified during the release testing**

When a defect is identified during the release testing, the QA community will mark the status as "Failed Validation". The issue is then reviewed, and the status is changed to "In Development". The development team will repeat Step 2, which involves analyzing the defect and assigning it to a developer for resolution. This iterative process allows for thorough defect investigation and ensures that appropriate actions are taken to address the identified issues.

\


<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>



## Release Process

Kindly go through [Sunbird Community Contribution Practice Ver1.0](https://docs.google.com/document/d/1ulBgZW-UthdK75BssIfKCUNk3tyv5NeSRUxRO7hZ-qY/edit) document's Release Practice section for detailed release process followed.&#x20;

#### Release Naming Convention&#x20;

Sunbird Serve building block follows a 4 digit release naming convention i.e. A.B.C.D

A -> number denoting the major release

B -> number denoting the stable release on the major release

C -> number denoting the intermediate release on the stable release

D -> number denoting the hotfix on the intermediate release

A release number 4.10.1.2 denotes, 4th Major Release, 10th Stable release,1st intermediate release on 10th Stable release and 2nd hotfix release on the intermediate release.

#### Release Activities

Below diagram will give a overview of the different release activities and their sequence\


<figure><img src="https://lh4.googleusercontent.com/l_4b84PRB0e-etVMGRY5eLc9GRPfDL9xhmRZtBb3DGtNYi8tDn-jq0vh25mYZQhFzAhGp8eSUQRO5YiB88HRQy7ChuWsrXwnOfjbBWVdr1V8E5S8n_h90b7iQN7vSnSDStQgts1eGZ4_QmQgX_EW84I" alt=""><figcaption></figcaption></figure>

Intermediate Release Activities :-

\


<figure><img src="https://lh3.googleusercontent.com/cbz-4WHvZ9Ew3Wu0H4eFxsES8pAi-qERw0kRACx9B40PP4bOifJSOuZLIYR3ZIB0S0_2EinwK1joAgj0xjfK_sRDRTqT_kGR1FOBGd_FaJ8Xh6om-Snyj0slZxhdwuuncaPw1qd2YlT_I3d5juVstBo" alt=""><figcaption></figcaption></figure>

\


Stable Release Activities :-

\


<figure><img src="https://lh6.googleusercontent.com/YcBvxATARyzOCqHJIxetqLi69-av9nYt-mUsNrXvlQf6Rif-C7KXNmdHoaF-__HiPuWPpBNO0pYATsA0wxlpW5N9zGcS_pk1MLE0Y9ovHSzEpVIfsrdhLMyq7IG8khZ2PNedYaVfrP95Ny96QteE54E" alt=""><figcaption></figcaption></figure>

\
