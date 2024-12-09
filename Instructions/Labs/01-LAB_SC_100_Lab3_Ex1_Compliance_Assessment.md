# Compliance assessment

## Lab scenario introduction

You are Allan Deyoung, a member of the IT department at Contoso Ltd. You have recently been transferred to the IT Security division. Your new role is to evaluate Contoso's Zero Trust readiness and develop an action plan to establish a Zero Trust initiative, following the Zero Trust pillars. Contoso is a large multinational corporation with a global presence in multiple industries. The company has a large cloud footprint and a hybrid infrastructure. Contoso's security operations center (SOC) is responsible for monitoring and responding to security incidents across the enterprise. The SOC is staffed with security analysts, security engineers, and network engineers. The SOC uses Microsoft Sentinel as its security information and event management (SIEM) solution. The SOC has a log analytics workspace that is used to collect and analyze security logs from across the enterprise.

Contoso Ltd. is expanding into Europe to increase sales, but is having trouble satisfying customer IT security demands. Customers want Contoso to maintain a secure environment to facilitate safe collaboration and minimize the risk of data leaks and compromised company assets. Many customers require evidence of well-established IT business processes and a robust security framework, which is often in the form of an ISO-27001 certification. To address this, Contoso has decided to hire an external audit firm to conduct the ISO-27001 Audit and obtain the certification. It is necessary to assess the current organizational stance and develop an action plan to meet the ISO-27001 requirements. As the company's cyber security architect, you are tasked with identifying the existing gaps and assigning specific tasks to people within the organization to resolve them.

## Part 1: Design a solution (required)

In this task you will design a concept to address the challenges Contoso Ltd. is facing.

### Design Approach

To address the described issue effectively, it's crucial to grasp ISO 27001 thoroughly. Assessing Contoso's setup against ISO 27001 standards is essential, highlighting any inconsistencies for analysis. This process can be time-consuming due to the complexity of both the M365 environment and the 27001 regulations. However, the Microsoft Compliance Manager assessment streamlines this analysis.

Compliance Manager assessments from Microsoft are groupings of controls from specific regulations, standards, or policies. They help you ensure that your organization meets the requirements of various standards, regulations, or laws. For instance, completing all actions within an assessment may align your Microsoft 365 settings with ISO 27001 requirements. Assessments encompass several components and provide templates for over 360 regulations, offering the necessary controls and steps to assess your compliance effectively. 

### Proposed Solution

|Requirement|Solution|Action plan|
|----|----|----|
|Comparison of the M365 environment with the ISO 27001 regulations|Microsoft Purview Compliance Manager|Create an assessment|
|Create an action plan|Microsoft Purview Compliance Manager|Assign tasks to a technical engineer|

## Part 2: Implement the solution (optional)

### Task 1: Conduct an ISO-27001 assessment

Your first step is to analyse the company's current environment. You carry out a compliance assessment to analyse the extent to which Contoso's environment complies with the ISO-27001 regulations.

1. Sign-in to the Microsoft Purview Compliance portal **`https://purview.microsoft.com/`** as Allan Deyoung using his administrator account **MOD Administrator**.
1. If you're asked to setup multifactor authentication, follow the instructions.
1. You're taken to the new Microsoft Purview portal landing page. Select the box next to the statement, **I agree to the terms of data flow disclosure and Privacy Statements**, then select **Get started**.
1. From the left navigation panel, select **Solutions** then select **Compliance Manager**. Alternatively, from the main window you can select the **View all solutions** tile, then select the **Compliance Manager** tile listed under Risk & Compliance.
1. From the **Compliance Manager** panel on the left, select **Assessments**.
1. From the **Assessments** window, select **+ Add assessment**.
1. From the **Base your assessment on a regulation** window, select **Select regulation**.
1. In the search text box enter **`ISO/IEC 27001:2022`**, then select the regulation then select **Save** and then select **Next**.
1. On the **Add name and group** page, in the text box **Assessment name** , enter **`ISO-27001 Audit assessment`**. Leave the **Assessment group** setting to **Use existing group** with the **Default group**, then select **Next**.
1. On the **Select services** page, the **Microsoft 365** service should already be listed.  If not, select **Select services** and select **Microsoft 365** and select **Add**. Select **Next**.
1. On the **Review and finish** page, select **Create the assessment**. It will take a few seconds to create the assessment, then select **Done** .
1. You should now be on the newly created **ISO-27001 Audit assessment** page.
1. Leave this browser tab open for the next task.

You have successfully created an assessment based on ISO-27001.

### Task 2: Assign tasks to a technical engineer

The results of the assessment shows you different areas and actions that are essential to comply with ISO-27011 regulations. You will investigate improvement actions and assign a task to a technical engineer.

1. You should still be on the page for the assessment you just created, **ISO-27001 Audit assessment**.  If not, navigate to the Microsoft Purview portal **`https://purview.microsoft.com/`** and from there select **Solutions** > **Compliance Manager** > **Assessments** > **ISO-27001 Audit assessment**
1. From the **ISO-27001 Audit assessment** page, select **Your improvement actions**.
1. Set the filter for **Control family** to **Physical controls**.
1. Select the box next to **Improvement action** to select all shown improvement actions, then select **Assign to user** (listed above the filters options).
1. In the new **Assign improvement actions** window, in the search text box enter **`Nestor Wilke`**.
1. Select the user and select **Assign**.
1. Keep this browser tab open for the next task.

You have successfully viewed and assigned an improvement action to a technical engineer

### Task 3: Provide access to a technical engineer for the improvement actions

Users need access to view the tasks assigned to them. You will grant Nestor Wilke access to the assessment.

1. You should still be on the **Your improvement actions** tab for **ISO-27001 Audit assessment** page.  If not, navigate to the Microsoft Purview portal **`https://purview.microsoft.com/`** and from there select **Solutions** > **Compliance Manager** > **Assessments** > **ISO-27001 Audit assessment** > **Your improvement actions**.
1. From the upper right corner of the **ISO/IEC 27001:Assessment** page, select **Manage user access**.
1. From the new **Manage user access** window, select the **Assessor** tab and select **Add assessors**.
1. In the **Search for users** text box, enter **`Nestor Wilke`**.
1. Select the user and then select **Apply**, then select **Save**.
1. You have successfully granted Nestor Wilke the Assessor role for this assessment.
1. You can now exit out of the Microsoft Purview portal by closing the browser tab.

You have successfully granted Nestor Wilke the Assessor role for this assessment.
