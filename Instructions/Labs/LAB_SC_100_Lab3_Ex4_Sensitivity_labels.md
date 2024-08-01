---
    lab: 3
    title: 'Exercise 4 - Sensitivity Labels'
---

# Lab 3 - Exercise 4 - Sensitivity Labels

Contoso Ltd. is in the process of acquiring Tailwind Traders. Management has decided to treat all documents in this process as strictly confidential to minimize the risk of a data leak.

You have been given the following safety requirements for the label:

- Content may only be shared with internal employees of Contoso Ltd.
- Content must be encrypted.
- Files and e-mails may not be forwarded.
- Access to content from non-corporate devices is prohibited.
- The scope of this label is management.

## Part 1: Design a solution (required)

In this task you will design a concept to address the issues Contoso Ltd. is facing.

### Design Approach

Contoso has several solutions in place to protect it´s data. Your initial approach would be to analyse current setup and decide whether they meet the current requirements. 

Based on above scenario, Microsoft Purview Information Protection can be used to fulfill the requirements and protect the data adequately. Microsoft Purview Information Protection's sensitivity labels empower you to classify and safeguard your organization's data, all while ensuring seamless user productivity and collaborative capabilities remain unimpeded. 

### Proposed Solution

|Requirement|Solution|Action plan|
|----|----|----|
|Encrypt documents and mails|Microsoft Purview Information Protection|Deploy a sensitivty label|
|Restrict access to data from unmanaged deviecs|Microsoft Purview Information Protection|Deploy a sensitivity label|
|Restrict access to internal users only|Microsoft Purview Information Protection|Deploy a sensitivity label

## Part 2: Implement the solution (optional)

### Task 1: Investigate existing sensitivity labels

In this task you will investigate existing sesnitivity labels and decide whether a new label needs to be created.

>[!NOTE] You should have already installed the Exchange Online PowerShell module. If the module is missing follow the instructions for installing the module.

1. Open an elevated PowerShell window by selecting the Windows button with the right mouse button and then select **Windows PowerShell (Admin)**.
1. Confirm the **User Account Control** window with **Yes**.
1. Enter the following cmdlet to install the latest Exchange Online PowerShell module version:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirm the untrusted repository security dialog with **Y** for Yes and press **Enter**.  This process may take some time to complete.
1. Enter the following cmdlet to connect to Security & Compliance PowerShell:

    ```powershell
    Connect-IPPSSession
    ```
1.When the **Sign in** window is displayed, sign in as admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider) and use the administrative password for your tenant.
1. Enter the following cmdlet to get a list of all deployes sensitivity labels

    ```powershell
    Get-Label | Format-Table -wrap ParentLabelDisplay,DisplayName,LabelActions
    ```
This cmdlet shows you all deployed sensitivity label and the corresponding actions. Examine the labels. Decide whether the existing labels meet the business requirements or whether new labeling is required. When you have finished, continue with the next task.

### Task 2: Enable sensitivity label support for groups & sites

In a previous task you reviewed the existing labels and came to the conclusion that current existing labels don´t meet the business requirement of the company. In order to apply sensitivity labels to groups & sites, you need to enable sensitivity label support in PowerShell.

1. Open an elevated PowerShell window by selecting the start menu with the right mouse button and then select Windows PowerShell and run as administrator.
1. Confirm the User Account Control window with Yes and press Enter.
1. First we need to install Microsoft Graph PowerShell SDK. Since it comes in two modules, Microsoft.Graph and Microsoft.Graph.Beta, we need to install both. Enter the following cmdlet to install the latest Microsoft.Graph:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```
1. Confirm the Nuget security dialog and the Untrusted repository security dialog with Y for Yes and press Enter. This may take a while to complete processing.
1. Enter the following cmdlet to install Microsoft.Graph.Beta:

```powershell
Install-Module Microsoft.Graph.Beta -Scope CurrentUser
```
1. Confirm the User Account Control window with Yes and press Enter.
1. Connect to the tenant:

```powershell
Connect-MgGraph -Scopes "Directory.ReadWrite.All"
```

1. In the Sign into your account form, sign in as admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). The password should be provided by your lab hosting provider.
1. On the **permissions requested** window select **Consent on behalf of your oganization** and select **Accept**. After signin, elect the PowerShell window.
1. Enter following cmdlet to enable Sensitivity labels:

```powershell
$params = @{
     Values = @(
 	    @{
 		    Name = "EnableMIPLabels"
 		    Value = "True"
 	    }
     )
}

Update-MgBetaDirectorySetting -DirectorySettingId $grpUnifiedSetting.Id -BodyParameter $params
```

1. Close the PowerShell window.

You have successfully enabled support for sensitivity labels for groups & sites.

### Task 3: Create and deploy a high security sensitivity label

You will create a new sensitivity label to fulfil the requirements.

1. Sign-in to the Microsoft Purview Compliance portal **https://compliance.microsoft.com/** as Allan Deyoung using his administrator account **MOD Administrator**.
1. In the Microsoft Purview portal, in the left navigation pane, expand **Information Protection** then select **Labels**.
1. On the **Labels** page select **+ Create a label**.
1. On the **Provide basic details for this label** page enter the following information:

    - **Name**: Confidential - Acquisition process
    - **Display name**: Confidential - Acquisiton process
    - **Description for users**: Highly confidential data related to any acquisition process.
    - **Desription for admins**: This label provides protection to any data realated to any acquisitons of Contoso.

1. Select **Next**.
1. On the **Define the scope for this label** page, select **Items** and select **Files**, **Emails** and **Groups & sites**. If any other options on this page are selected, deselect those options.
1. On the **Choose protection settings for labeled items** page, select **Apply or remove encryption**.
1. On the **Encryption** page selet **Configure encryption settings**.
1. Enter the following information into the encryption settings: 
    - **Assign permissions now or let users decide?**: Let users assign permissions when they apply the label.
    - **In Outlook, enforce one of the following restrictions**: Do not Forward.
1. Select **In Word, PowerPoint, and Excel, prompt users to specify permissions** then select **Next**.
1. On the **Auto-labeling for files and emails** page, select **Next**.
1. On the **Define protection settings for groups and sites** page, select **Privacy and external user access** and **External sharing and Conditional Access** then select **Next**.
1. On the **Data privacy and external user access settings** page select **Private** than select **Next**.
1. On the **Define external sharing and conditional access settings** page select **Control external sharing from labeled SharePoint sites** and **Use Microsoft Entra Conditional Access to protect labeled SharePoint sites** and set the configuration as following:
    - **Content can be shared with**: Only people in your organization
    - **Determine whether users can access SharePoint sites from unmanaged devices**: Block access
1. Select **Next**.
1. On the **Aut-labeling for schematized data assets (preview)** page select **Next**.
1. On the **Review your settings and finish** page select **Create label**.
1. On the **Your sensitivity label was created** page, as next steps select **Publish label to users' apps**.
1. Select **Done**.
1. On the **Publish label** page select **Create a new label policy**.
1. On the **Choose sensitivity label to publish** page select the label you just created and select **Next**.
1. On the **Assign admin units** page select **Next**.
1. On the **Publish to users and groups** page select **Users and groups** and select **Edit**.
1. On the **Scope for users and groups** page select **Specific users and groups** and select **+ Include users and groups** then select **Executives** and **Leadership** and select **Done** until user assignment is finished.
1. Select **Next**.
1. On the **Policy settings** page select **Users must provide a justification to remove a label or lower its classification** and **Require users to apply a label to their emails and documents**.
1. Select **Next**.
1. On the **Default settings for documents** page select **Email inherits highest priority label from attachments** and select **Next**.
1. On the **Default settings for meetings and calenar events** page select **Next**.
1. On the **Default settings for sites and groups** page select **Next**.
1. On the **Default settings for Fabric and Power BI content** page select **Next**.
1. On the **Name your policy** page enter the following information:
    - **Name**: Management sensitivity label policy
    - **Description**: This policy is designed for management to protect in connection with the acquisition of companies
1. Select **Next**.
1. On the **Review and finish** page select **Submit**.

You have successfully created and published a sensitivity label.