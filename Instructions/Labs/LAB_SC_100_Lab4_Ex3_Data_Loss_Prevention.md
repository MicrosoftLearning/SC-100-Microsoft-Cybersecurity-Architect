---
    lab: 4
    title: 'Exercise 3 - Data Loss Prevention'
---

# Lab 4 - Exercise 3 - Data Loss Prevention

Contoso Ltd. is currently integrating Tailwind Traders into their projects. Although the merger is still in progress, both companies operate within separate tenants. Tailwind Traders employees are considered external users and are invited as guests to Contoso's tenant to facilitate sharing of SharePoint sites and files. In certain projects, selected Tailwind Traders employees receive Windows 11 clients managed by Contoso Ltd. to ensure full access to internal resources while maintaining security oversight. Access to M365 desktop applications is blocked for unmanaged devices, and these users can only access the environment via web applications. The managed devices are secured through various policies in Endpoint Manager. Contoso Ltd. has implemented Microsoft Purview Information Protection to encrypt sensitive documents based on the type of information they contain. 

As a cybersecurity architect, you recently examined various activities in the Defender for Cloud Apps activity log and discovered that some documents marked as confidential are being copied to external USB drives. You also discovered that users are free to store any company data they have access to on their unmanaged, personal devices. This poses a major problem that needs to be addressed. As a solution, you will design a security policy to restrict the storage of company data on unmanaged, personal devices. This will help to minimize the risk of sensitive data being compromised.

## Part 1: Design a solution (required)

In this task you will design a concept to address the risks Contoso Ltd. is facing.

### Design Approach

The initial step involves analyzing the requirements based on the described issue, understanding the objectives, and defining the requirements.

Based on the provided use-case, the following requirements can be outlined:

- Preventing data transfer to USB drives
- Limiting access to sensitive data from unmanaged devices
- Blocking the download of sensitive data from unmanaged devices

In the second step examine Contoso Ltd.'s existing environment. Microsoft Purview and Microsoft Defender offer various solutions for managing data flow, encompassing Microsoft Purview Information Protection, Data Loss Prevention, Conditional Access, and Retention Policies. Investigate which controls are already in place. Access various portals to review current configurations and policies, determining if adjustments are necessary or if new settings/policies need implementation.

The third phase involves crafting the solution concept. Upon investigation, it is evident that none of the current policies meet the defined requirements. Therefore, a new set of policies is essential.

### Proposed Solution

Design a security policy to restrict the storage of company data on unmanaged, personal devices. This will help to minimize the risk of sensitive data being compromised. The policy should outline the types of data that are considered sensitive and the acceptable devices on which they can be stored. Additionally, the policy should provide guidelines for the secure transfer of data to external devices. Employees should be required to sign an agreement acknowledging their understanding of the policy and their commitment to adhering to it. The policy should be communicated to all employees and enforced through regular audits and disciplinary action for non-compliance. Regular training sessions should also be conducted to ensure that employees are aware of the risks associated with storing company data on personal devices and the importance of following the policy. Finally, the policy should be reviewed and updated regularly to ensure that it remains effective and relevant. 

|Requirement|Solution|Action plan|
|----|----|----|
|Block move of data to USB drives|Endpoint Data Loss Prevention|Block all data with a sensitive label from being copied to a USB drive|
|Restrict access to sensitive data from unmanaged devices|Defender for Cloud Apps|Block copy/cut/paste of data for unmanaged devices|
|Block download of sensitive data from unmanaged devices|Defender for Cloud Apps|Block download of data from unmanaged devices|

## Part 2: Implement the solution (optional)

### Task 1: Deploy a data loss prevention policy

The first step of the solution design involves creating of a Data Loss Prevention rule for Endpoints. You will deploy a DLP rule to block copy of data to USB drives. 

1. Sign-in to the Microsoft Purview Compliance portal **https://compliance.microsoft.com** as Allan Deyoung using his administrator account **MOD Administrator**.
2. In the Microsoft Purview portal, in the left navigation pane, expand **Data loss prevention** then select **Policies**.
3. On the **Policies** page select **+ Create policy**.
4. On the **Start with a template or create a custom policy** page select **Custom**, **Custom policy** then select **Next**.
5. On the **Name your DLP policy** page enter a Name and Description and select **Next**.
6. On the **Assign admin units** page select **Next**.
7. On the **Choose where to apply the policy** page select only **Devices** and select **Next**.
8. On the **Define policy settings** page select **Next**.
9. On the **Customize advanced DLP rules** page select **+ Create rule**.
10. Enter a name and a decription for the rule. 
11. Under **Conditions** select **+ Add condition** and select **Content contains**.
12. Specify the following conditions:

    - **Content contains**: Sensitivity labels
      - Select **Add**, then select **Sensitivity labels** and select the labels **Trusted People**, **Project - Falcon**, **Confidential**, **Highly Confidential**, **Confidential - Finance**
13. Under **Actions** select **+ Add an action** and select **Audit or restrict activities on devices**.
14. Specify the following actions:
   -    Under **File activities for all apps** select **Apply restrictions to specific activity**.
      - Make sure **Copy to a removable USB device** is selected and select the option **Block** from the dropdown menu for this setting.
      - Leave other settings unchanged.
15. Select **Save** then select **Save**.
16. Select **Next**.
17. On the **Policy mode** page select **Turn the policy on immediately**
18.  On the **Review and finish** page select **Submit**.

You have successfully implemented a data loss prevention policy that blocks any copying of data to USB drives.

### Task 2: Onboard applications to Conditional Access App Control

Part of the solution is to create session policies in Defender for Cloud apps. Session policies offer comprehensive insight into cloud applications through real-time monitoring of sessions. These policies enable tailored actions according to the specified policy for each user session. In order to create a session policy, conditional access app control needs to be deployed on your applications. Conditional access app control adds real-time monitoring and control capabilities for your apps. Creating a session policy without onboarding any app into conditional access app control won´t work. The first step is to onboard applications you want to protect to conditional access app control. 

There are 2 ways to onboard applications to conditional access app control:

- Add an application manually in Microsoft Defender Portal (Settings > Cloud apps > Connected apps > Conditional Access App Control apps)
- Configure a conditional access policy to protect apps with Defender for Cloud apps

A conditional access policy forwards all applications specified in the policy to "Defender for cloud apps conditional access app control". The next time a user logs on to the specified applications, the corresponding application is automatically added to the conditional access app control. You can view these applications in the Microsoft Defender portal. 
 
>**Tip:** Before you start this task, you should check the existing conditional access app control apps. You will notice that no applications have been onboarded yet. At this stage, try to create a session policy in Defender for Cloud Apps and check the error messages that occur.

In this task you will deploy conditional access app control on your applications by creating a conditional access policy In Microsoft Entra. 

1. Sign-in to the Microsoft Entra portal **https://entra.microsoft.com** as Allan Deyoung using his administrator account **MOD Administrator**.
2. In the Microsoft Entra portal expand **Protection** and select **Conditional Access**.
3. In the **Conditional Access | Overview** page select **Policies** and selecht **+ Create new policy**.
4. Enter a name for the policy.
5. Under **Assignments** select **Users** and include **All users**.
6. Under **Assignments** select **Target resources** and include **All cloud apps**.
7. Under **Access controls** select **Session**.
8. On the **Session** pane select **Use Conditional Access App Control** and select **Use custom policy...**, then close the **Session** pane with the **Select** button.
9. Under **Enable policy** select **On**.
10. If you get a warning to exclude the current user from the policy select **I understand that my account will be impacted by this policy. Proceed anyway.**.
11. Optionally, specify the conditions and grant controls.
12. Select **Create**.

Now sign-in to one of the Microsoft web apps, such at [Outlook](https://outlook.office365.com). The application you sign-in will be automatically onboarded to conditional access app control. Sign-in to Microsoft Defender portal and view the applications under conditional access app control.

You have successfully created a conditional access policy to forward all applications to Defender for Cloud Apps and onboarded apps to conditional access app control.

### Task 3: Create session policies in Defender for Cloud apps

You will create two session policies in Defender for Cloud apps to block downloads of data and restrict permissions for unmanaged devices.

1. Sign-in to the Microsoft Defender portal **https://security.microsoft.com** as Allan Deyoung using his administrator account **MOD Administrator**.
2. In the Microsoft Security portal select **Cloud apps** > **Policies** > **Policy management**.
3. On the **Policies** page create a **Session policy**.
4. On **Create session policy** page select the policy template **Block download based on real-time content inspection**.
5. Enter a policy name.
6. Select a policy severity and a category.
7. Enter a description.
8. Under **Session control type** select **Control file download (with inspection)**.
9. Under **Activity source** in the **Activities matching all of the following** section select the following filter:

    - **Device tag**: Select **Does not equal** and select **Intune compliant**.

10. In the **Files matching all of the following** section select the following filter:

    - **Sensitivity label**: Select **Equals** and select the labels **Confidential**, **Highly Confidential** and **Confidential - Finance**.

11. Under **Inspection method** select **Data Classification Service** then select **Any** then select **Sensitive information type...** and select the appropiate sensitive information type you want to apply this policy to.
12. Under **Actions** select **Block**.
13. Select **Create** to create the policy.
14. Create a second policy as descriped above and select the policy template **Block cut/copy and paste based on real-time content inspection**.
15. Under **Activity source** in the **Activitiies matching all of the following** enter the following information: 

    - **Activity type**: Select **Equals** and select **Cut/Copy item, Paste item**
    - **Device tag**: Select **Does not equal** and select **Intune compliant**

16. Disable **Use content inspection** and select **Create** to create the policy.

You have successfully created two session policies in Defender for Cloud Apps.
