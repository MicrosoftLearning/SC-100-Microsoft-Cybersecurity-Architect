# Security Posture Management and Defender XDR Unifed RBAC

Contoso's security team wants to improve its security posture by using Microsoft Secure Score, a tool that provides recommendations and guidance on how to reduce the attack surface and protect against threats.

The security team reviews and delegates Secure Score recommended actions to its extended team members (security ambassadors) that manage the status and action plan associated with improvement actions. The security team also wants to control access to security posture information and the data sources that feed it. Joni Shermann is one of the security ambassadors and needs access to exposure management.

Recently, there have been reports that uninvited associates were automatically being admitted to Teams calls to which they were not directly invited.  Due to the sensitive and confidential nature of calls, the security team want to control this.

### Design approach

The recommended actions tab in Microsoft Secure Score lists the security recommendations that address possible attack surfaces. Those actions can be shared/delegated.

Security teams need to control access to the organization's security posture information and to the specific data sources that feed it. The Microsoft Defender XDR Unified role-based access control (RBAC) model provides a single permissions management experience that provides one central location for administrators to control user permissions across different security solutions.

To ensure that the security ambassadors have the necessary role permissions you need to create a custom role. For the Microsoft Defender XDR security portal to start enforcing the permissions and assignments configured in your new custom roles or imported roles, you must activate the Microsoft Defender XDR Unified RBAC model for some or all of your workloads.

### Proposed solution

|Requirement|Solution|Action plan|
|----|----|----|
|Control access to security posture information and the data sources that feed it. | Microsoft Defender XDR Unified RBAC | Activate Microsoft Defender XDR Unified RBAC and create a custom role |
|Joni Shermann will manage actions and status associated with Security Score recommendations. |Exposure Management - Secure Score and Defender XDR unified RBAC | Create role to manage security posture and grant access to Joni Shermann. |
|Share Secure Score recommendd action |Secure Score | Share recommended action. |

### Task 1 - Activate Defender XDR unified RBAC by activating workloads

For the Microsoft Defender XDR security portal to start enforcing the permissions and assignments configured in your new custom roles, you must activate the Microsoft Defender XDR Unified RBAC model for some or all of your workloads.

In this task you´ll enable specific workloads.

1. Log into the Client 1 VM (LON-SC1) as the **lon-sc1\admin** account. The password should be provided by your lab hosting provider.
1. Open **Microsoft Edge**, select the address bar, navigate to **`https://security.microsoft.com`** and log into **Microsoft Defender** as MOD Administrator **admin@WWLxZZZZZZ.onmicrosoft.com** (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.
1. On the **Stay signed in?** dialog box, select the **Don’t show this again** checkbox and then select **No**.
1. If you are asked to setup multifactor authentication, follow the instruction.
1. Close the password save dialog from the bottom by selecting **Never**, to not save the default global admins credentials in your browser.
1. On the left navigation pane, expand **System** then select **Settings**.
1. Select **Microsoft Defender XDR**.
1. Under General, select **Permissions and roles**.
1. You may have to wait a few minutes for Microsoft Defender XDR to set up.
1. Under Workloads, set the slider for **Endpoints & Vulnerability Management** to **Active**.  Do the same for **Defender for Office 365**, and for **Defender for Office 365**.

You successfully activated the Microsoft Defender XDR Unified RBAC model for some or all of your workloads.

### Task 2 - Create a custom role to manage security posture for Exposure Management

In this task, you'll set up custom role focused on security posture and more specifically on Exposure Management. As part of the custom role, you'll grant Joni Shermann access to the data source for Exposure Management.

1. You should still be logged into the Microsoft Defender portal.
1. On the left navigation pane, expand **System** then select **Permissions**.
1. On the **Permissions** page, expand **Microsoft Defender XDR** and select **Roles**.
1. Select **Create custom role**.
1. In the Role name field, enter **`SecureScore Manager`** then select **Next**.
1. Select **Security posture**.
1. In the Security posture window:
    - Select **Select custom permissions**
    - Under Posture management select **Select custom permissions**
    - Choose **Exposure Management (manage)**
    - Select **Apply**.
    - Select **Next**.
1. On the **Assign users and data sources** page, select **Add assignment** then populate the fields as follows:
    - Assignment name: **`ExposureManagement`**
    - Assign users and group: Enter **`Joni Sherman`**, then select it.
    - Under **Data sources**, select the down arrow to open the drop-down menu and **uncheck** everything except **Microsoft Security Exposure Management**.
    - Select, **Add**.
    - Select, **Next**.
1. In the Review and finish page review your settings, select **Submit**, then select **Done**.

You successfully set up a custom role for security posture that grants Joni Shermann access to the Exposure Management data source.

### Task 3 - Share a recommended action

Share a Microsoft Secure Score recommended action. In this task you'll post the action on a Teams channel. By posting it on Teams, users on the channel will see a notice but will not have access to the data source to edit the status or manage the action. Only Joni Shermann who is a member of the Teams channel and has role permissions can access the recommended action.

1. You should still be logged into Microsoft Defender XDR portal.
1. On the left navigation pane, expand **Exposure management** then select **Secure Score**.
1. Select the **Recommended actions** tab.
1. Search for **`Only invited users should be automatically admitted to Teams meetings`** and select it.
1. Select **Share**, and in the dropdown menu select **Microsoft Teams**.
1. In field **Team** select **Mark 8 Project Team** and in the **Channel** field select **Channel Research and Development**.
1. Select **Post message to Teams**.

Joni Sherman and her Mark 8 Project Team will be notified about the recommended action in the Teams channel.

### Task 4 - Manage Recommendations

As Joni Sherman you received the teams notification that a specific action to increase the organization's security posture was recommended.  As an extended member of the security team you have the role permissions to manage the recommended action and document the solution.

In this task, you´ll manage recommended action and document your solutions.

1. Open a Microsoft Edge inPrivate window, navigate to **`https://office.com`** and sign in as **JoniS@WWLxZZZZZZ.onmicrosoft.com**.
1. If the landing page appears blurred out, refresh the page.
1. Select the app launcher icon, located to the left of the top banner that says Contoso Electronics, and select **Teams**.
1. On the Welcome to Teams window, select **Get Started**.
1. Open Teams. For the **Mark 8 Project Team** select **See all channels** then select **Research and Development**.
1. Review the message posted from the previous task.
1. Although all the members of the Team channel and see the messags, only you have the role permission to access the link. Select the link in the posted message. You are taken direclty to the recommended action in Microsoft Secure Score.
1. Open another tab in the Microsoft Edge inPrivate window, navigate to **`https://security.microsoft.com`**.
1. On the left navigation pane, expand **Exposure management** and select **Secure Score**.
1. Select **Edit status & action plan**.
1. Check **Resolved through third party**.
1. Add a note **Currently secured** to the **Action plan** field.
1. Select **Save and Close**.

As Joni Shermann, you successfully edited the status for the recommended action.
