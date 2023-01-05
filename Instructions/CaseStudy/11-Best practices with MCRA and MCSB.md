---
casestudy:
    title: 'Case study: Best practices with MCRA and MCSB'
    module: 'Module 11: Recommend security best practices with MCRA and MCSB'
---
This case study exercise is designed to provide experience performing some conceptual design tasks that relate to the subjects learned in this module.

## Case study: Best practices with MCRA and MCSB
 
CONTOSO is a health services company with its main offices in Chicago and London, UK.  
The company provides healthcare services to clients at their facilities around Chicago and London, UK metropolitan area.  Contoso’s facilities are full of hospitals that have physicians, nurses, and other health care professionals. Contoso has initiated a company-wide migration of all critical services to the cloud. This migration includes on premises servers, VMs, and the supporting management and monitoring appliances.

Contoso initiated its cloud migration except for some data and application that needs to be hosted in on premises because of compliance and regulatory requirements. Contoso establishes an Azure Active Directory (Azure AD) tenant. This Azure AD is synchronized with Active Directory Domain Services (AD DS), which is maintained on on-premises domain controllers. As the migration progresses, additional Azure subscriptions will be created on an as-needed basis for each department including SaaS applications. To facilitate their daily work, most employees have access to Microsoft 365 applications.  
 
To support continued connectivity, basic Virtual Desktop Infrastructure (VDI) testing has  
been initiated for most categories of employees, such as account managers, support  
staff, and business, finance, and HR staff. Secure connectivity is supported via a Virtual  
Private Network (VPN) gateway for a limited set of users and devices. Additionally, a  
third-party firewall has been deployed to protect virtual server Virtual Local Area  
Networks (VLANs).  
 
While they are on site with the clients, physicians use mobile devices with locally  
stored tracking and monitoring data. This data is protected using proprietary storage  
encryption, and each health care professional is required to log on to their device using locally stored credentials before accessing the data. 
 
### Requirements

As the cloud migration continues and expands, Contoso plans to move all on-premises  
data and application to the cloud except the out-of-scope applications. 

* Deploy Microsoft 365 Defender and Defender for Cloud to enhance Contoso’s security postures against adversaries 
* Microsoft Compliance policy MCSB needs to be applied to Azure Subscription 
* Contoso wants to proactively hunt for possible threats and actively manage attack surface 
* Contoso wants to centrally manage identities for both external contractors and patients and internal employees 
* All the endpoint devices must be centrally managed and continuously evaluated for compliance. 
* Protected Health Information (PHI) stored on mobile devices used by health care professionals will be moved to the cloud following data residency policy to comply with regional regulations. 
* Access to mobile devices while in the field should be restricted by geolocation and requires bio metric as a multi factor authentication  
* Data sharing between apps on the same device must be controlled.  
* Compliance with the Health Insurance Portability and Accountability Act (HIPAA) and National Health Services (NHS) requirements. 
* Contoso wants to manage privilege administrators following the least privileged principals and enforce just in time access policies. 
* Contoso wants to recover their data from any disaster and also wants to keep those backup data in a secure location. In case of any disaster in their primary region, Contoso wants to failover to the secondary region. 
* Contoso wants to make sure they follow Zero trust approach for validating all incoming access
* As data and processing is moved to Azure, the VPN gateway must be configured to  
support secure P2S connections from devices that run a variety of desktop and mobile  
operating systems, including Windows, macOS, Android, and others.  

### Design tasks

* What Defender plan is needed by Contoso to meet their Business and Security requirements? 
* What could Contoso do to validate all incoming access and follow zero trust at the same time? 
* How could Contoso apply NHS and HIPAA policies into their cloud environment? 
* What should Contoso use to have visibility of all existing threats and vulnerabilities? 
* How should Contoso deploy and maintain security configuration to the end point devices ? 
* How can Contoso have visibility on the used cloud applications and data shared externally? 