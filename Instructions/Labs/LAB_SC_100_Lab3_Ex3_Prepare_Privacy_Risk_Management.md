---
    lab: 3
    title: 'Exercise 3 - Prepare Privacy Risk Management'
---


# Lab 3 - Exercise 3 - Prepare Privacy Risk Management

Contoso Ltd. wants to improve their compliance posture as part of the expansion to Europe. As the Cybersecurity Architect Expert you have been tasked with improving the Priva Privacy Risk Management Score in particular. Use Compliance Manager to look at improvement actions and delegate their implementation for an improvement of the privacy risk management compliance score. As part of that you will also add a new policy for the regions U.S. and EU.

## Part 1: Design a solution (required)

In this task you will design a concept to address the requirements Contoso Ltd. is facing.

### Design approach

The initial step involves analyzing the requirements based on the described scenario, understanding the objectives and defining the requirements.

Based on the provided use-case, the following requirements can be outlined:

- Admins and other users with access to reports should not see user's names
- Privacy risks need to be managed by a designated team
- Guidelines need to exists for privacy risks

In the second step examine Contoso Ltd.'s existing environment. Microsoft Priva offers solutions to manage privacy risks. Investigate which controls exist and which policies are already in place. Use the Microsoft Purview Compliance portal to review current configurations and determine what adjustments must be implemented to meet the requirements for the region they are expanding to.

The third phase involves crafting the solution's concept. Upon investigation, it is evident that creating policies to monitor potential risks is the best way to meet the requirements.  

### Proposed solution

|Requirement|Solution|Action plan|
|----|----|----|
|Admins and other users with access to reports should not see user's names|Compliance improvement action|Assign and implement the improvement action **Anonymize user names to users in certain roles**|
|Privacy risks need to be managed by a designated team|Microsoft Purview roles|Create a role group with permissions to handle privacy risks and assign the designated employees|
|Guidelines need to exists for privacy risks|Privacy Risk Management Policy|Create a privacy risk management policy to alert the privacy risk management team of potential risks|

## Part 2: Implement the solution (optional)

## Task 1 – Look at possible Compliance Manager improvement actions for Privacy Risk Management and assign them owners

In this task you will get an overview of possible Privacy Risk Management improvement actions and delegate them.

1. **Sign-in** to the **Microsoft Purview Compliance portal** **https://compliance.microsoft.com/**.
2. On the left pane select **Privacy Risk Management Overview**.
3. Scroll down to the **Stay on track with regulations and improve your privacy posture** card.
4. Select the **View improvement actions** button.
5. Look at the possible improvement actions. Think about which improvement actions can be configured preliminary by yourself and which can be delegated to the security team.
6. Select the **Enable privacy operations admins to create and support subject rights request fulfillment** improvement action.
7. Read the details of the improvement.
8. Assign **Megan Bowen** as Owner of the improvement action using the drop-down menu.
9. Select **Edit details** at the top of the page.
10. Set the **Implementation status** to **Implemented**. Because you assigned **Megan Bowen** the subject rights requests administrator and privacy risk management administrator role groups in the last exercise.
11. Select **Save and close** at the top of the page.

You have succesfully assigned an improvement action to a security employee.

## Task 2 - Assign and implement the improvement action **Anonymize user names to users in certain roles**

You have to make sure that users are anonymized in all the Priva components for the improvement action.

*Skip to 5. if you are still on the **improvement actions overview.***
1. **Sign-in** to the **Microsoft Purview Compliance portal** **https://compliance.microsoft.com/**.
1. Select **Compliance Manager** > **Improvement actions**.
1. Select the **Anonymize user names to users in certain roles** improvement action.
1. Assign yourself **MOD Administrator** as the Owner for this improvement action using the drop-down menu.
1. Under **Details** select the **Launch Now** Link at the end of the **How to Implement** description.
1. Check if the **Show anonymized versions of user names** setting is selected, if not, select it and select **Save**.
1. Close the browser tab.
1. Select **Edit details** at the top of the improvement action **Show anonymized versions of user names**.
1. Set the **Implementation status** to **Implemented** and select **Save**.
1. Select **Save and close** at the top of the page.

You have successfully assigned and implemented an improvement action.

## Task 3 – Create a privacy risk management policy

This last task is about creating the custom privacy risk management policy for the EU and U.S. regions.

1. Go to the **Microsoft Purview Compliance portal** **https://compliance.microsoft.com/**
2. On the left pane select **Privacy risk management** > **Policies**.
3. Select **Create a policy** in the top right.
4. Select **Create** in the **Custom** card.
5. Select the **Data minimization** policy template.
6. Enter the policy name:**Data minimization USA and EU**.
7. Enter the description:**This policy is intended to minimize saved privacy risk relevant data according to U.S. and EU regulations.**
8. Select **Next**.
9. Select **Add classification groups**.
10. Select:
    - GDPR Enhanced
    - U.S. Gramm-Leach-Bliley Act (GLBA) Enhanced
    - U.S. Health Insurance Act (HIPAA) Enhanced
    - U.S. Patriot Act Enhanced
    - U.S. Personally identifiably Information (PII) Data Enhanced
    - U.S. State Breach Notification Laws Enhanced
11. Select **Add** and **Next**.
12. Select all users and groups and select **Next**.
13. Select all locations and select **Next**.
14. Set the **Item hasn't been modified in the previous (days)** setting to 120.
15. For **Choose frequency of notifications**, select **Monthly, every 1**.
16. For the **Link to privacy training** enter: https://learn.microsoft.com/en-us/privacy/"
17. Select **Next**.
18. Set **Create alerts** to **On**.
19. Set **High volume of personal data** to 20 instances.
20. Select **Next**.
21. Select **Next**.
22. Review your settings and select **Submit**.

You have successfully created a privacy risk management policy for U.S. and EU data protection laws.

You have successfully finished setting up and delegating some improvement actions, pricacy risk management policies and user permissions. You can proceed with the next exercise.
