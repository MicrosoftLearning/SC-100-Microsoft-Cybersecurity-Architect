# Compliance assessment

## Lab scenario

Contoso Ltd. requires ISO-27001 certification to meet customer IT security demands. As the cyber security architect, you need to assess the company's compliance posture and assign remediation tasks to technical staff.

In this lab, you will:
- Create an ISO-27001 compliance assessment using Microsoft Purview Compliance Manager
- Assign improvement actions to a technical engineer
- Grant appropriate access for the engineer to view and work on assigned tasks

**Estimated Time**: 25 minutes

## Lab tasks

### Task 1: Conduct an ISO-27001 assessment

Your first step is to analyse the company's current environment. You carry out a compliance assessment to analyze the extent to which Contoso's environment complies with the ISO-27001 regulations.

1. Sign-in to the Microsoft Purview portal **`https://purview.microsoft.com/`** as Allan Deyoung using his administrator account **MOD Administrator**.
1. If you're asked to setup multifactor authentication, follow the instructions.
1. You're taken to the new Microsoft Purview portal landing page. Select **Get started**.
1. From the left navigation panel, select **Solutions** then select **Compliance Manager**. Alternatively, from the main window you can select the **View all solutions** tile, then select the **Compliance Manager** tile listed under Risk & Compliance.
1. From the **Compliance Manager** panel on the left, select **Assessments**.
1. From the **Assessments** window, select **+ Add assessment**.
1. From the **Base your assessment on a regulation** window, select **Select regulation**.
1. In the search text box enter **`ISO/IEC 27001:2022`**, then select the regulation then select **Save** and then select **Next**.
1. On the **Add name and group** page, in the text box **Assessment name**, enter **`ISO-27001 Audit assessment`**. Leave the **Assessment group** setting to **Use existing group** with the **Default group**, then select **Next**.
1. On the **Select services** page, the **Microsoft 365** service should already be listed.  If not, select **Select services** and select **Microsoft 365** and select **Add**. Select **Next**.
1. On the **Review and finish** page, select **Create the assessment**. It will take a few seconds to create the assessment, then select **Done** .
1. You should now be on the newly created **ISO-27001 Audit assessment** page.
1. Leave this browser tab open for the next task.

You have successfully created an assessment based on ISO-27001.

### Task 2: Assign tasks to a technical engineer

The results of the assessment shows you different areas and actions that are essential to comply with ISO-27011 regulations. You will investigate improvement actions and assign a task to a technical engineer.

1. You should still be on the page for the assessment you just created, **ISO-27001 Audit assessment**.  If not, navigate to the Microsoft Purview portal **`https://purview.microsoft.com/`** and from there select **Solutions** > **Compliance Manager** > **Assessments** > **ISO-27001 Audit assessment**
1. From the **ISO-27001 Audit assessment** page, select **Your improvement actions**.
1. Set the filter for **Control family** to **Physical controls** and select **Apply**.
1. Select the box next to **Improvement action** to select all shown improvement actions, then select **Assign to user** (listed above the filters options).
1. In the new **Assign improvement actions** window, in the search text box enter **`Nestor`** and press enter.
1. Select the user and select **Assign**.
1. Keep this browser tab open for the next task.

You have successfully viewed and assigned an improvement action to a technical engineer

### Task 3: Provide access to a technical engineer for the improvement actions

Users need access to view the tasks assigned to them. You will grant Nestor Wilke access to the assessment.

1. You should still be on the **Your improvement actions** tab for **ISO-27001 Audit assessment** page.  If not, navigate to the Microsoft Purview portal **`https://purview.microsoft.com/`** and from there select **Solutions** > **Compliance Manager** > **Assessments** > **ISO-27001 Audit assessment** > **Your improvement actions**.
1. From the upper right corner of the **ISO/IEC 27001:Assessment** page, select **Manage user access**.
1. From the new **Manage user access** window, select the **Assessor** tab and select **Add assessors**.
1. In the **Search for users** text box, enter **`Nestor`** and press enter.
1. Select the user and then select **Apply**, then select **Save**.
1. You have successfully granted Nestor Wilke the Assessor role for this assessment.
1. You can now exit out of the Microsoft Purview portal by closing the browser tab.

You have successfully granted Nestor Wilke the Assessor role for this assessment.
