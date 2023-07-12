---
casestudy:
    title: 'Case study: Design solutions that align with the Cloud Adoption Framework (CAF)'
    module: 'Module 02: Design solutions that align with CAF and WAF'
---
This case study exercise is designed to provide experience performing some conceptual design tasks that relate to the subjects learned in this module.

## Case study: Design solutions that align with the Cloud Adoption Framework (CAF)

- Contoso Banking is a subsidiary of Contoso Group, that is being carved out into an independent business entity. Contoso Banking will be a separate company with its own infrastructure and IT organization. 
- The Contoso Banking infrastructure will be based entirely in the Microsoft Azure cloud. To build a secure cloud platform from the beginning of the company, you need to design a secure Azure Landing Zone.
- The terms of the agreement dictate that the transition needs to take maximum of 6 months
- Contoso Banking plans to build the next-generation FinTech solution using cloud-native solutions. MVP 1 release needs to be done in 6 weeks.

### Requirements

Contoso Group does not use any cloud services, the infrastructure is entirely hosted in their own data center. The environment that will be part of Contoso Banking includes:

- Environment 1: Core banking systems: 20 apps. Security is essential.
- Environment 2: Next-gen / Fintech app, built on Azure Kubernetes Service and Azure Data Lake. 100 releases per month

#### Planned Changes

Environment 1: Contoso Banking plans to move all the core banking infrastructure to the cloud. The approach needs to include the following:

- Deploy a landing zone with where the core applications are hosted.
- The users need to access the core applications from secure cloud-based workstations. The users need to have consistent user experience to access the applications.
- The solution needs to ensure best practices on identity and access management , governance, security, network and logging are followed.

Environment 2 (Fintech app) needs to meet the following requirements:

- Release 100x / month
- Continuously be audit-ready
- Comply with PCI-DSS

### Design tasks

- What are the components needed to be deployed into the landing zone?
- How will the choice of workloads affect the implementation time and complexity?
- How would you implement the secure access to core apps?
- Which Azure Landing Zone should you recommend Contoso Banking to implement for Environment 1?
- Which Azure Landing Zone should you recommend Contoso Banking to implement for Environment 2?
