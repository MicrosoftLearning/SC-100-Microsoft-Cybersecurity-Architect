---
casestudy:
    title: 'Case study: Design a resiliency strategy for a ransomware attack'
    module: 'Module 04: Design a resiliency strategy for common cyberthreats like ransomware'
---
This case study exercise is designed to provide experience performing some conceptual design tasks that relate to the subjects learned in this module.

## Case study: Design a resiliency strategy for a ransomware attack
 
CONTOSO is a health services company with its main offices in Chicago and London, UK.  
The company provides healthcare services to clients at their facilities around Chicago and London, UK metropolitan area.  Contoso’s facilities are full of hospitals that have physicians, nurses, and other health care professionals. Contoso has initiated a company-wide migration of all critical services to the cloud. This migration includes on premises servers, VMs, and the supporting management and monitoring appliances.

Contoso initiated its cloud migration except for some data and application that needs to be hosted in on premises because of compliance and regulatory requirements. Contoso has an Azure Active Directory (Azure AD) tenant. This Azure AD is synchronized with Active Directory Domain Services (AD DS), which is maintained on on-premises domain controllers. As the migration progresses, additional Azure subscriptions will be created on an as-needed basis for each department including SaaS applications. To facilitate their daily work, most employees have access to Microsoft 365 applications.  
 
There have been multiple recent high-profile ransomware cases involving Contoso's competitors in the health services market. The CEO and CISO are concerned that Contoso does not yet have an plan in place to mitigate the risk from a ransomware attack. The CISO has personally requested that you draft a ransomware response and mitigation plan to be presented to company executives in two weeks. Some of the more senior IT staff have been vocal that the ransomware threat is being exaggerated and that all the company really needs is good backups and solid perimeter security.
 
### Requirements

* The ransomware response and mitigation plan must include not only critical on-premises infrastructure and cloud services, but also company data stored on company laptops and mobile devices used by employees in the field
* The CEO and CISO have taken a hard line approach that they will never negotiate or pay ransomware hackers. They have said that in the event of a ransomware attack their goal is to have critical systems operational again within 12 hours, and full functionality restored within 48 hours.
* Data handling strategies must comply with privacy requirements including HIPAA in the US and any related standards in the UK.
* Your plan must also detail why good backup aren't sufficient to mitigate the threat from ransomware.

### Initial questions

* What departments and personnel need to be involved in creating the ransomware mitigation plan? 
* What services and infrastructure elements need to be addressed by the plan? 
* What are realistic timelines for creating a robust ransomware response plan?
* What are the main measures of success for the implementation of your ransomware protection plan?

### Design tasks

* List the Azure and M365 services will be critical to backing up and securing your data. Explain why each service is an important part of the ransomware response and the tradeoffs for each one.
* Make a note of any special requirements that your company has which are not addressed by existing Azure and M365 solutions.
* List the services and infrastructure elements which need to be addressed by the plan.
* Estimate some realistic timelines for creating a robust ransomware response plan and then executing that plan. 