# Retention policies

The German government recently modified specific laws governing retention periods for companies. One significant change is that all financial documents must now be retained for 11 years, instead of the previous requirement of 10 years. Another change is that commercial or business correspondence, including copies of dispatched commercial or business correspondence, can now be retained for 5 years instead of 7. Currently, your company adheres to a retention policy that maintains all documents for a duration of 7 years. However, Contoso Ltd. has encountered challenges in recent years due to the accumulation of a large volume of data in its environment. This has led to increased maintenance costs and significant storage space consumption. Your assignment is to optimize the retention policy in your company to comply with legal regulations while minimizing data storage requirements. The company policy dictates that all data must be retained for at least five years after creation, in strict adherence to all applicable laws governing data retention.

## Part 1: Design a solution (required)

In this task you will design a concept to address the challenges Contoso Ltd. is facing.

### Design Approach

The initial step involves analyzing the requirements based on the described issue and understanding the objectives

Based on the provided use-case, the following requirements can be outlined:

- Retain all financial data for 11 years
- Retain all business correspondence for 5 years
- Minimization of data storage overhead

In the second step examinine Contoso Ltd.'s existing environment. Contoso has several solutions in place to retain it´s data for a specific time. Your task is to analyse current setup and decide whether they meet the legal requirements. 

The third phase involves crafting the solution concept. After thorough investigation, it becomes clear that none of the existing policies fulfill the specified criteria. Therefore, a new set of policies is essential.

Based on above scenario, Microsoft Purview Data Lifecycle Management can be used to retain the data adequately.

### Proposed Solution

|Requirement|Solution|Action plan|
|----|----|----|
|Retain all financial data for 11 years| Microsoft Purview Data Lifecycle Management|Create and auto-apply a retention label|
|Retain all business correspondence for 5 years| Microsoft Purview Data Lifecycle Management|Deploy a retention policy|


## Part 2: Implement the solution (optional)

### Task 1: Analyze the current structure of the retention policy

In this task, you will familiarize yourself with your company's existing retention policy. You will have a look into different retention policies, labels and label policies. You will use the Security & Compliance PowerShell module and view the existing policies. You will investigate the current set-up and decide whether the existing retention policies are enough for Contoso Ltd. to meet the legal requirements.

>[!NOTE] You should have already installed the Exchange Online PowerShell module. If the module is missing follow the instructions for installing the module.

1. Open an elevated Windows PowerShell window by selecting the Windows button with the right mouse button and then select **Terminal (Admin)**.
1. Confirm the **User Account Control** window with **Yes**.
1. Enter the following cmdlet to install the latest Exchange Online PowerShell module version:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirm the untrusted repository security dialog with **Y** for Yes and press **Enter**.  This process may take some time to complete.
1. Enter the following cmdlet to connect to Security & Compliance PowerShell then when prompted, login with your MOD administrator credentials:

    ```powershell
    Connect-IPPSSession
    ```

1. Enter the following cmdlet to view existing retention policies and settings:

    ```powershell
     Get-ComplianceTag | Format-Table -Auto Name,Priority,RetentionAction,RetentionDuration,Workload
    ```

1. Take some time to assess the resulting table.

    >[!NOTE] You can also access the Microsoft Purview Compliance portal to view retention policies but you have to look into each policy one by one instead of getting an overview over all your policies at a glance.

You successfully viewed the existing labels and settings to decide whether they meet the legal requirements.

### Task 2: Create a retention policy

You have effectively assessed Contoso Ltd.'s retention policies, uncovering an outdated setup that fails to meet legal standards. Your investigation revealed five retention policies sharing identical settings, with only one retention label applied, none of which adequately address legal requirements.

Your plan involves implementing a new company-wide retention policy with a five-year retention period. Following this timeframe, data may be retained but is not mandatory for deletion. This adjustment satisfies the legal requirements for minimum retention periods and reduces data overhead.

1. Sign-in to the Microsoft Purview Compliance portal **`https://purview.microsoft.com/`** as Allan Deyoung using his administrator account **MOD Administrator**.
1. If you're asked to setup multifactor authentication, follow the instructions.
1. You're taken to the new Microsoft Purview portal landing page. Select the box next to the statement, **I agree to the terms of data flow disclosure and Privacy Statements**, then select **Get started**.
1. From the left navigation panel, select **Solutions** then select **Data Lifecycle Management**. Alternatively, from the main window you can select the **View all solutions** tile, then select the ***Data Lifecycle Management** tile listed under Data Governance.

1. On the **Data lifecycle management** pane, expand **Policies** and select **Retention policies**.
1. On the **Retention policies** page select **+ New retention policy**.
1. On the **Name your retention policy** page enter the following information:
    - **Name**: **`General retention policy`**
    - **Description**: **`This policy is the default retention policy for the entire organization. All data must be retained for at least 5 years.`**
1. Select **Next**.
1. On the **Policy Scope** page select **Next**.
1. On the **Choose the type of retention policy to create** page select **Static** and select **Next**.
1. On the **Choose where to apply this policy** page enable following locations:

    - Exchange mailboxes
    - SharePoint classic and communication sites
    - OneDrive accounts
    - Microsoft 365 Group mailboxes & sites

1. Select **Next**.
1. On the **Decide if you want to retain content, delete it or both** page enter the following settings:

    - Retain items for a specific period: **5 years**
    - Start the retention period based on: **When items were cerated**
    - At the end of the retention period: **Do nothing**

1. Select **Next**.
1. On the **Review and finish** page select **Submit**, then select **Done**.

You have successfully created a retention policy. You can now delete all remaining retention policies as they do not meet the company's requirements.

### Task 3: Create a retention label

To adhere to german regulations you will now create a retention label with a retention period of 10 years and auto-apply it to all documents that contain german financial data.

1. You should still be logged into the **Data Lifecycle Management** solution in the Microsoft Purview portal.  If not, navigate to **`https://purview.microsoft.com/`** > **Solutions** > **Data Lifecycle Management**.
1. On the **Data lifecycle management** pane, select **Retention labels**.
1. On the **Labels** page, select **+ Create a label**.
1. On the **Name your retention label** page enter the following information:

    - Name: **`German financial data`**
    - Description for users: **`This label retains all German financial data for 10 years.`**
    - Description for admins: **`The label retains all financial data for 10 years and it is automatically applied.`**

1. Select **Next**.
1. On the **Define label settings** page select **Enforce actions after a specific period** and select **Next**.
1. On the **Define the period** page enter the following information:

    - How long is the period?: **10 years**
    - When should the period begin?: **When items were created**

1. Select **Next**.
1. On the **Choose what happens after the period** page select **Delete items automatically**. Click **Next**.
1. On the **Review and finish** page select **Create label**.
1. On the **Your retention label is created** page select **Auto-apply this label to a specific type of content** and select **Done**.
1. On the **Let´s get started** page enter the following information:

    - Name: **`Automatically retain all German financial data for 10 years`**
    - Descriptions: **`This policy auto-applies the label German financial data.`**

1. Select **Next**.
1. On the **Choose the type of content you want to apply this label to** page select **Apply label to content that contains sensitive info** and select **Next**.
1. On the **Content that contains sensitive info** page set the filter to **Germany** and select **Financial** and then **Germany Financial Data** then select **Next**.
1. On the **Define content that contains sensitive info** page, leave all existing settings (no change) and select **Next**.
1. On the **Policy scope** page select **Next**.
1. On the **Choose the type of retention policy to create**, page select **Static**.
1. On the **Choose where to automatically apply the label** page enable following locations:

    - Exchange mailboxes
    - SharePoint classic and communication sites
    - OneDrive accounts
    - Microsoft 365 Group mailboxes & sites

1. Select **Next**.
1. On the **Choose a label to auto-apply** page make sure that the  **German Financial Data** label is already present. Otherwise add it using the **+ Add label** button. Select **Next**.
1. On the **Decide whether to test or run your policy** page select **Turn on policy** then select **Next**.
1. On the **Review and finish** page select **Submit** then select **Done**.

You have successfully created and auto-applied a retention label.
