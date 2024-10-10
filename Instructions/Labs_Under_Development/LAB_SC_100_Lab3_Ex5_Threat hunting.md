---
    lab: 3
    title: 'Exercise 5 - Threat hunting'
---


# Lab 3 - Exercise 5 - Content Search Microsoft Purview

Your company is facing a serious threat to its integrity and security. A significant number of malicious emails have been detected. Your task is to identify the sender addresses or subject lines of these emails. Once you have identified these malicious emails, you must delete them en masse.

## Part 1: Design a solution (required)

### Design approach

The first step is to identify malicious emails. Therefore, an analysis of the current mail-flow is essential. The Microsoft Defender Portal provides a comprehensive overview of all outgoing and incoming mail flow, along with further capabilities for investigating this traffic. The remediation action involves deleting the malicious emails. 

### Proposed Solution

|Requirement|Solution|Action plan|
|----|----|----|
|Identify malicious e-mails|Microsoft Defender for Office 365|Investigate the mail flow and analyse mail headers|
|Elimination of risks emanating from malicious e-mails|Microsoft Defender for Office 365|Delete malicious mails|

### Task 1: Investigate malicious mails

You will investigate the incoming mails in Microsoft Defender portal and identify which mails are suspicious and contain malicious content.

1. Sign-in to the Microsoft Defender portal **https://security.microsoft.com** as Allan Deyoung using his administrator account **MOD Administrator**.
1. In the Microsoft Security portal expand **Email & collaboration** then select **Explorer**.
1. On the **Explorer** page adjust the time period of the query to view all mail-flow of the last 30 days and select **Refresh**
1. The result shows you all incoming and outgoing mails. Investigate the mail-flow and the subject of the mails.
1. Mails with the subject "You have tasks due today" appear suspicious.
1. Select the subject to do further investigation.
1. On the new appeared **You have tasks due today** pane view provided information and select **View header**.
1. On the **Email message headers** pane select **Copy message header** and select **Microsoft Message Header Analyzer**.
1. A new tab will open in your browser.
1. On the **Message Header Analyzer** page paste the message Header and select **Analyze headers**.
1. Review the outcome.

You have successfully reviewed the mail flow in Microsoft Defender portal.

### Task 2: Perform mass deletion of malicious mails

You´ve come to the conclusion that mails with the subject "You have tasks due today" are phishing attacks. Your remediation action involves a mass deletion of those mails using Powershell.

>[!NOTE] You should have already installed the Exchange Online PowerShell module. If the module is missing follow the instructions for installing the module.

1. Open an elevated PowerShell window by selecting the Windows button with the right mouse button and then select **Windows PowerShell (Admin)**.
1. Confirm the **User Account Control** window with **Yes**.
1. Enter the following cmdlet to install the latest Exchange Online PowerShell module version:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirm the untrusted repository security dialog with **Y** for Yes and press **Enter**.  This process may take some time to complete.
1. Open an elevated PowerShell window by selecting the Windows button with the right mouse button and then select **Windows PowerShell (Admin)**.
1. Confirm the **User Account Control** window with **Yes**.
1. Enter the following cmdlet to connect to Security & Compliance PowerShell:

    ```powershell
    Connect-IPPSSession
    ```

1. When the **Sign in** window is displayed, sign in as sign in as admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider) and use the administrative password for your tenant.
1. Enter the following cmdlet to perform content search and specify the time period in the cmdlet:

    ```powershell
    $Search=New-ComplianceSearch -Name "Purge phishing messages" -ExchangeLocation All -ContentMatchQuery '(Subject:"You have tasks due today")'
    Start-ComplianceSearch -Identity $Search.Identity
    ```
1. Enter the followng cmdlet to hard delete messages:

    ```powershell
    New-ComplianceSearchAction -SearchName "Purge phishing messages" -Purge -PurgeType HardDelete
    ---
You have successfully performed a mass-deletion of malicious mails.