---
    lab: 3
    title: 'Exercise 2 - Delegate Subject Rights Requests'
---


# Lab 3 - Exercise 2 - Delegate Subject rights requests

Contoso Ltd. is preparing for ISO-27001 certification. As part of this preparation, they need to implement a process for GDPR subject rights requests. The company will use the Microsoft Priva subject rights requests feature and integrate the new workflow into their internal compliance audit process. 

As the Cybersecurity Architect Expert, you will delegate the handling of European DSRs and set up read permissions for the audit. To ensure that employees handling DSR cases do not also handle the Privacy Risk Management feature, you will create a custom view-only role group. The built-in role groups grant too many permissions for the audit. 

You will assign the chosen employees the necessary roles for handling subject rights requests or auditing, following the principle of least privilege. To complete the POC, you will use the Microsoft Priva trial and ensure that audit logs are activated in your tenant. Since the compliance audit occurs bi-monthly, you will increase the subject rights request retention duration to eliminate any blind spots between the audits. 

## Part 1: Design a solution (required)

In this task you will design a concept to address the requirements Contoso Ltd. is facing with their expansion into Europe.

### Design approach

The initial step involves analyzing the requirements based on the described scenario, understanding the objectives and defining the requirements.

Based on the provided use-case, the following requirements can be outlined:

- Enable your environment to handle data subject requests
- A designated team needs to handle DSRs
- Rentention limits of DSRs need to be modified to comply with the audit schedule

In the second step examine Contoso Ltd.'s existing environment. Microsoft Priva offers solutions to manage data subject requests. Investigate which controls exist and which policies are already in place. Use the Microsoft Purview Compliance portal to review current configurations and determine what adjustments must be implemented to meet the requirements for the region they are expanding to.

The third phase involves crafting the solution's concept. Upon investigation, it is evident that enabling specific employees to manage DSRs is the best way to meet all the requirements.  

### Proposed solution

|Requirement|Solution|Action plan|
|----|----|----|
|Enable your environment to handle data subject requests|Microsoft Purview and Admin Center|Assign Priva licenses and verify that the unified audit log is enabled|
|A designated team needs to handle DSRs|Microsoft Purview roles|Create a role group with permissions to handle DSRs and assign the designated employees|
|Rentention limits of DSRs need to be modified to comply with the audit schedule|Microsoft Purview Privacy Risk Management|Use an improvement action to set a retention limit of 90 days for DSRs|

## Part 2: Implement the solution (optional)

## Task 1 – Activate the Microsoft Priva trial license

In the first two tasks you will check the necessary preconditions for using the Microsoft Priva features. You have to activate the Microsoft Priva trial license and make sure that audit logs are enabled in your tenant.

1. Login to the **VM** with your admin credentials.
2. Open **Microsoft Edge**, select the address bar, navigate to **https://compliance.microsoft.com** and log into the Microsoft Purview Compliance portal as **MOD Administrator** admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Admin**s password should be provided by your lab hosting provider.
3. When asked if you want to stay signed in select **No**.
4. On the left pane select either **Privacy Risk Management - Overview** or **Subject rights requests**.
5. If the trial is not active select **activate trial** on the top of the page.

If the trial is already active in your lab you still have to check the exact amount of subject rights requests cases contained in your license in the admin center.

6. **Sign-in** to the **Microsoft 365 Admin Center** **https://admin.microsoft.com/**.
7. On the left pane, select **Billing** and **Your products**.
8. Look for the **Priva Privacy Risk Management** license.
9. Look for the **Privacy Management - subject rights request** license and how many cases are included.

You have successfully checked, if your M365 Tenant has active Microsoft Priva Licenses.

## Task 2 – Check if audit logs are enabled

For the privacy risk management features to function, audit logging must be active in your tenant.

1. Open an elevated **PowerShell** window by selecting the start menu with the right mouse button and then select **Windows PowerShell** and **run as administrator**.
2. Enter the following cmdlet to install the latest Exchange Online module version:
    ```powershell
    Install-Module -Name ExchangeOnlineManagement
    ```
3. Confirm the Nuget security dialog and the Untrusted repository security dialog with Y for Yes and press Enter. This may take a while to complete processing.
4. Enter the following cmdlet to connect to the Exchange Online service:
    ```powershell
    Connect-ExchangeOnline
    ```
5. In the **Sign into your account** form, sign in with your admin credentials.
6. After successfully connecting to Exchange Online PowerShell enter:
    ```powershell
    Get-AdminAuditLogConfig | Format-List UnifiedAuditLogIngestionEnabled
    ```
7. A **True** value for _UnifiedAuditLogIngestionEnabled_ is returned.
8. If a **False** value is returned, enable Audit Log with the command:
    ```powershell
    Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    ```
9. A warning that it can take up to 60 minutes for the change to take effect is returned. Audit Log is now turned on in your tenant. You can check again later with the command mentioned before.

You have successfully confirmed that Audit Logs are enabled in your tenant.

## Task 3 – Create a custom role group and assign the designated employees to it

In this task you will create the custom read-only role group for the Contoso Ltd. Compliance audit and assign the designated employees.

1. Sign-in to the **Microsoft Purview Compliance portal** **https://compliance.microsoft.com/**.
2. Select the **Permissions** tab under the **Roles & Scopes** tab on the left pane.
3. Select **Roles** under the Microsoft Purview solutions item.
4. Create a new role group with the following settings:
    |Setting|Value|
    |----|----|
    |Name|Internal Compliance Audit View-only|
    |Description|This role group contains all roles necessary for the bi-monthly audit of the compliance posture of Contoso Ltd.|
    |Roles|View-Only Audit-Logs, View-Only Case, Priva Management Viewer|
    |Users|Grady Archie|
5. Select **Next** on the **Add roles to the role group** and proceed to the next task without closing the dialogue.

You have successfully created a custom role group with the minimum necessary permissions and assigned the designated employees to it.

## Task 4 – Assign employees and yourself to the built-in role groups

Now you have to assign the remaining permissions for subject rights requests management using the built-in role groups.

*(Skip to 4. if you are still in the Roles & Scopes Menu)*
1. **Sign-in** to the **Microsoft Purview Compliance portal** **https://compliance.microsoft.com/**.
2. Select **Roles & Scopes** > **Permissions** on the left pane.
3. Select **Roles** under the **Microsoft Purview solutions** item.
4. Add **Irvin Sayers** to the **Subject Rights Request Administrators** role group.
5. Add **Alex Wilber** and **Joni Sherman** to the **Subject Rights Request Approvers** role group.
6. Add your admin account **MOD Administrator** and **Megan Bowen** to the **Privacy Management Administrators** and the **Subject Rights Request Administrators** role groups.

You now have assigned all necessary permissions to all employees to handle subject rights requests.

## Task 5 - Configure the maximum data retention limit for subject rights requests

For the bi-monthly compliance audit you have to configure the retention limit for subject rights requests in this task.

[!NOTE] It can take up to 30 minute for your role groups changes to apply, which you need to view the subject rights request feature. If you just granted yourself the permissions in task 4, you may have to wait for the changes to take effect.

1. **Sign-in** to the **Microsoft Purview Compliance portal** **https://compliance.microsoft.com/**.
2. On the left pane select **Compliance Manager** and then select the **Improvement actions** tab.
3. On top of the page select the **Solutions:** filter and check **Priva Privacy Risk Management** and **Priva Subject Rights Requests**.
4. Select **Enable and enforce data retention limits for data involved in subject rights request**
5. Click **Assign to user** > Search for **MOD Administrator** > **Assign**, which assigns MOD Administrator as owner of the improvement action.
6. Read the details of the improvement.
7. Select **Launch Now** at the bottom of the description to directly enter the subject rights request settings.
8.  Select the **Data retention periods** tab.
9.  Set the **Data collected and reports** value to 90 days and select **Save**
10. Close the tab in Edge.
11. Select **Edit details** at the top of the page of the improvement action.
12. Set the **Implementation status** to **Implemented**.
13. Select **Save and close** at the top of the page.

You have successfully increased the subject rights request data retention limit and updated the improvement action.

You have finished the setup of the subject rights requests feature and delegated handling cases accordingly. You can proceed with the next exercise.
