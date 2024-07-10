---
    lab: 4
    title: 'Exercise 3 - Data Loss Prevention'
---

# Lab 4 - Exercise 3 - Data Loss Prevention

Following the acquisition of Tailwind Traders, Contoso Ltd. has been progressively integrating the new company into various projects. While the merger is still in progress, both entities operate within separate tenants, with Tailwind Traders employees considered as external users. Collaboration consists of inviting these users as guests to Contoso's tenant, facilitating the sharing of SharePoint sites and files. For projects with heightened security requirements, selected Tailwind Traders employees receive Windows 11 clients managed by Contoso Ltd., ensuring full access to internal resources while maintaining security oversight. Access to M365 desktop applications is blocked for unmanaged devices. These users can only access the environment via web applications. Managed devices are secured through various policies in Endpoint Manager. Additionally, Contoso Ltd. has implemented Microsoft Purview Information Protection to encrypt sensitive documents based on the type of information they contain. As a cybersecurity architect, you have recently examined various activities in the Defender for Cloud Apps activity log. You realised that some documents marked as confidential are being copied to external USB drives and that users are free to store any company data they have access to on their unmanaged, personal devices. This is a major problem that needs to be addressed.

As a cyber security architect, you will design a solution to minimise the risk described above. Decide what type of solution can be used.

## Part 1: Design a solution (required)

In this task you will design a concept to adress the risks Contoso Ltd. is facing.

### Design Approach

The initial step involves analyzing the requirements based on the described issue, understanding the objectives, and defining the requirements.

Based on the provided use-case, the following requirements can be outlined:

- Preventing data transfer to USB drives
- Limiting access to sensitive data from unmanaged devices
- Blocking the download of sensitive data from unmanaged devices

In the second step examinine Contoso Ltd.'s existing environment. Microsoft Purview and Microsoft Defender offer various solutions for managing data flow, encompassing Microsoft Purview Information Protection, Data Loss Prevention, Conditional Access, and Retention Policies. Investiage which controls are already in place. Access various portals to review current configurations and policies, determining if adjustments are necessary or if new settings/policies need implementation.

The third phase involves crafting the solution concept. Upon investigation, it is evident that none of the current policies meet the defined requirements. Therefore, a new set of policies is essential.

### Proposed Solution

|Requirement|Solution|Action plan|
|----|----|----|
|Block move of data to USB drives|Endpoint Data Loss Prevention|Block all data with a sensitive label from being copied to a USB drive|
|Restrict access to sensitive data from unmanaged devices|Defender for Cloud Apps|Block copy/cut/paste of data for unmanaged devices|
|Block download of sensitive data from unmanaged devices|Defender for Cloud Apps|Block download of data from unmanaged devices|

## Part 2: Implement the solution (optional)

### Task 1: Deploy a data loss prevention policy

The first step of the solution design involves creating of a Data Loss Prevention rule for Endpoints. You will deploy a DLP rule to block copy of data to USB drives. 

1. Sign-in to the Microsoft Purview Compliance portal **https://compliance.microsoft.com** as Allan Deyoung using his administrator account **MOD Administrator**.
1. In the Microsoft Purview portal, in the left navigation pane, expand **Data loss prevention** then select **Policies**.
1. On the **Policies** page select **+ Create policy**.
1. On the **Start with a template or create a custom policy** page select **Custom**, **Custom policy** then select **Next**.
1. On the **Name your DLP policy** page enter a Name and Description and select **Next**.
1. On the **Assign admin units** page select **Next**.
1. On the **Choose where to apply the policy** page select only **Devices** and select **Next**.
1. On the **Define policy settings** page select **Next**.
1. On the **Customize advanced DLP rules** page select **+ Create rule**.
1. Enter a name and a decription for the rule. 
2. Under **Conditions** select **+ Add condition** and select **Content contains**.
3. Specify the following conditions:

    - **Content contains**: Sensitivity labels
      - Select **Add**, then select **Sensitivity labels** and select the labels **Trusted People**, **Project - Falcon**, **Confidential**, **Highly Confidential**, **Confidential - Finance**
4. Under **Actions** select **+ Add an action** and select **Audit or restrict activities on devices**.
5. Specify the following actions:
   -    Under **File activities for all apps** select **Apply restrictions to specific activity**.
      - Make sure **Copy to a removable USB device** is selected and select the option **Block** from the dropdown menu for this setting.
      - Leave other settings unchanged.
6. Select **Save** then select **Save**.
7. Select **Next**.
8. On the **Policy mode** page select **Turn the policy on immediately**
9.  On the **Review and finish** page select **Submit**.

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
1. In the Microsoft Entra portal expand **Protection** and select **Conditional Access**.
1. In the **Conditional Access | Overview** page select **Policies** and selecht **+ Create new policy**.
1. Enter a name for the policy.
1. Under **Assignments** select **Users** and include **All users**.
1. Under **Assignments** select **Target resources** and include **All cloud apps**.
1. Under **Access controls** select **Session**.
2. On the **Session** pane select **Use Conditional Access App Control** and select **Use custom policy...**, then close the **Session** pane with the **Select** button.
3. Under **Enable policy** select **On**.
4. If you get a warning to exclude the current user from the policy select **I understand that my account will be impacted by this policy. Proceed anyway.**.
5. Optionally, specify the conditions and grant controls.
6. Select **Create**.

Now sign-in to one of the Microsoft web apps, such at [Outlook](https://outlook.office365.com). The application you sign-in will be automatically onboarded to conditional access app control. Sign-in to Microsoft Defender portal and view the applications under conditional access app control.

You have successfully created a conditional access policy to forward all applications to Defender for Cloud Apps and onboarded apps to conditional access app control.

### Task 3: Create session policies in Defender for Cloud apps

You will create two session policies in Defender for Cloud apps to block downloads of data and restrict permissions for unmanaged devices.

1. Sign-in to the Microsoft Defender portal **https://security.microsoft.com** as Allan Deyoung using his administrator account **MOD Administrator**.
1. In the Microsoft Security portal select **Cloud apps** > **Policies** > **Policy management**.
1. On the **Policies** page create a **Session policy**.
1. On **Create session policy** page select the policy template **Block download based on real-time content inspection**.
1. Enter a policy name.
1. Select a policy severity and a category.
1. Enter a description.
1. Under **Session control type** select **Control file download (with inspection)**.
1. Under **Activity source** in the **Activities matching all of the following** section select the following filter:

    - **Device tag**: Select **Does not equal** and select **Intune compliant**.

1. In the **Files matching all of the following** section select the following filter:

    - **Sensitivity label**: Select **Equals** and select the labels **Confidential**, **Highly Confidential** and **Confidential - Finance**.

1. Under **Inspection method** select **Data Classification Service** then select **Any** then select **Sensitive information type...** and select the appropiate sensitive information type you want to apply this policy to.
1. Under **Actions** select **Block**.
1. Select **Create** to create the policy.
1. Create a second policy as descriped above and select the policy template **Block cut/copy and paste based on real-time content inspection**.
1. Under **Activity source** in the **Activitiies matching all of the following** enter the following information: 

    - **Activity type**: Select **Equals** and select **Cut/Copy item, Paste item**
    - **Device tag**: Select **Does not equal** and select **Intune compliant**

1. Disable **Use content inspection** and select **Create** to create the policy.

You have successfully created two session policies in Defender for Cloud Apps.
