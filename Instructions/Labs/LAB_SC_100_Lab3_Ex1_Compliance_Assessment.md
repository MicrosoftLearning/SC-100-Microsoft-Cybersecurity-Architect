---
    lab: 3
    title: 'Exercise 1 - Compliance assessment'
---

# Lab 3 - Exercise 1 - Compliance assessment

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

1. Sign-in to the Microsoft Purview Compliance portal **https://compliance.microsoft.com/** as Allan Deyoung using his administrator account **MOD Administrator**.
2. You will be asked to setup multifactor authentication, follow the instruction.
3. In the Microsoft Purview Compliance portal, in the left navigation page, select **Compliance Manager**.
4. On the **Compliance Manager** page, select **Assessment**.
5. On the **Compliance Manager \| Assessments** page, select **+ Add assessment**.
6. On the **Base your assessment on a regulation** page, select **Select regulation**.
7. In the search text box enter **ISO-27001:2022**, then select the regulation then select **Save** and then select **Next**.
8. On the **Add name and group** page, in the text box **Assessment name** , enter **ISO-27001 Audit assessment** and then select **Next**.
9. On the **Select services** page, select **Select serivices** and select **Microsoft 365** and select **Add** then select **Next**
10. Finish the configuration and create the assessment.

You have successfully created an assessment based on ISO-27001.

### Task 2: Assign tasks to a technical engineer

The results of the assessment shows you different areas and actions that are essential to comply with ISO-27011 regulations. You will investigate improvement actions and assign a task to a technical engineer.

1. You should still be logged into the Microsoft Purview Compliance portal **https://compliance.microsoft.com/**.
2. In the Microsoft Purview Compliance portal, in the left navigation page, select **Compliance Manager**.
3. On the **Compliance Manager** page, select the assessment **ISO-27001 Audit assessment** you created.
4. On the assessment page, select **Your improvement actions** blade.
5. Set the filter for **Control family** to **Physical controls**.
6. Select all shown improvement actions, then select **Assign to user**.
7. In the new **Assign improvement actions** page, in the search text box enter **Nestor Wilke**.
8. Select the user and select **Assign**.

You have successfully viewed and assigned an improvement action to a technical engineer

### Task 3: Provide access to a technical engineer for the improvement actions.

Users need access to view the tasks assigned to them. You will grant Nestor Wilke access to the assessment.

1. You should still be logged into the Microsoft Purview Compliance portal **https://compliance.microsoft.com/**.
2. In the Microsoft Purview Compliance portal, in the left navigation pane, select **Compliance Manager**.
3. In the **Compliance Manager** page, select **Assessment** pane then select the **ISO-27001 Audit assessment** assessment.
4. In the **ISO/IEC 27001:Assessment** page, select **Manage user access**.
5. In the new **Manage user access** page, select **Assessor** and select **Add assessors**.
6. In the **Search for users** text box, enter **Nestor Wilke**.
7. Select the user and then select **Save**.

You have successfully grant Nestor Wilke access to the assessment.
