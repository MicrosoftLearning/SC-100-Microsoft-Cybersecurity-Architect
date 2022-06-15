This case study exercise is designed to provide experience performing some conceptual design tasks that relate to the subjects learned in this module.

## Case study: evaluate regulatory compliance

Contoso Pharma is an international pharmaceutical industry with a presence in North America and Europe. Contoso Pharma has workloads on-premises and in Azure. The goal is that in the next two years, all workloads will be fully in Azure and there will be minimum workloads on-premises. Below is a list of their major workloads:

- VMs (Windows and Linux)
- Storage accounts
- Key Vault
- SQL PaaS and SQL on VMs

Contoso Pharma also has a Site-to-Site VPN between the headquarters in Redmond and the main office in London. This VPN is used to allow resources on-premises to communicate.

Contoso Pharma has a legacy environment in Redmond composed by a couple of Windows Server 2012 running a Web Server that is used by the application that queries the database to check for customer's information. Upon investigation it was noted that the communication of the legacy web server with the database is done via HTTP.

### Design requirements

Contoso Pharma has different compliance needs according to their workloads, as shown in the table below:

| **Workload** | **Type of Data** | **Compliance Standard** |
|:---:|:---:|:---:|
| Windows VMs | Credit card holder information | PCI DSS |
| SQL PaaS | Patient health information | HIPAA |
| Storage Accounts | Credit card holder information | PCI DSS accounts |

To be compliant with these standards, Contoso Pharma must be able to:

- Monitor compliance progress over time
- Prohibit workload owners to provision resources that are not compliant with those standards
- Ensure that new subscriptions that are deployed in the environment are using required standards by default
- Ensure resources that are provisioned on each geo-location keep the data in the source region for data sovereignty purposes

### Design tasks

* To ensure that Contoso Pharma can analyze their compliance status over time, which tool should be utilized? Select the most appropriate option.
* Which service in Azure should be used to enforce workload owners to create only resources that are following the required standards?
* Which option should be utilized to ensure that when workload owners create resources, they're keeping the data in the correct geo-location?
* How can Contoso Pharma validate if the VMs that were provisioned are compliant with PCI DSS and if they're not what needs to be done to remediate?
* Data encryption is an imperative component to address your privacy requirements. What are the data stages that you must apply encryption?
* Which Azure service can you use to enforce data encryption across workloads?
