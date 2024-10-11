# Lab 4 - Exercise 1 - Security Posture Management

Contoso wants to improve its security posture by using Microsoft Secure Score, a tool that provides recommendations and guidance on how to reduce the attack surface and protect against threats. Contoso has a dedicated security team that manages the Secure Score dashboard and assigns actions to different product teams based on their roles and responsibilities. One of the product teams, the Mark 8 Project Team, is responsible for the mobile device management and needs to ensure that devices lock after a period of inactivity to prevent unauthorized access.

## Part 1: Design a solution (required)

### Design approach

The initial step involves analyzing the requirements based on the described scenario, understanding the objectives and defining the requirements.

Based on the provided use-case, the following requirements can be outlined:

- Get more recommendation to increase security posture
- Grant limited access to recommendation 
- Inform responsible team

Microsoft Secure Score evaluates an organization’s security posture across all Microsoft 365 workloads. It provides centralized visibility, threat-prioritized insights and comprehensive controls to enhance protection against cyberattacks and optimize cybersecurity.

### Proposed solution

|Requirement|Solution|Action plan|
|----|----|----|
|Add more recommendations to increase security posture | Additional data sources | Enable additional 'non-workload' sources |
|Grant limited access to recommendation |Defender XDR Permission and roles |Grant specific access to Joni Shermann |
|Inform responsible team |Secure Score |Inform the Mark 8 Project Team |

### Design tradeoffs and alternative solutions

## Part 2: Implement the solution (optional)

### Task 1 - Setup additional data source in Secure Score

In this Task you´ll enable additional data sources for Secure Score, to get more recommendation on your attack surface.

1. Log into the Client 1 VM (LON-SC1) as the **lon-sc1\admin** account. The password should be provided by your lab hosting provider.
2. Open **Microsoft Edge**, select the address bar, navigate to <https://security.microsoft.com> and log into the Microsoft 365 admin center  as **MOD Administrator** <admin@WWLxZZZZZZ.onmicrosoft.com> (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.
3. On the **Stay signed in?** dialog box, select the **Don’t show this again** checkbox and then select **No**.
4. You will be asked to setup multifactor authentication, follow the instruction.
5. Close the password save dialog from the bottom by selecting **Never**, to not save the default global admins credentials in your browser.
6. On the left navigation pane, select **Settings**.
7. Select **Microsoft Defender XDR**.
8. Under General, select **Permissions and roles**.
9. You may have to wait a few minutes for Microsoft Defender XDR to set up.
10. Enable **Additional data sources**.
11. Go back to the Secure Score dashboard.

You successfully enabled Additional data sources, to set up role based access to specfic product recommendations.

### Task 2 - Setup RBAC for Secure Score

In this task, you´ll make sure that only selected people can access this information. You enable RBAC for Secure Score and base it on the concept of least privilege access.

1. You should still be logged into Microsoft Defender XDR portal.
2. On the left navigation pane, select **Settings**.
3. Select **Microsoft Defender XDR**.
4. Select **Permissions and roles**.
5. Select **Go to Permissions and roles**.
6. Select **Create custom role**.
7. Role name: SecureScore Apps
8. Select **Next**.
9. Click on **Security posture**, select **Select custom permissions** and select **Select custom permissions**.
10. Choose **Secure Score (manage)**.
11. Select **Apply**.
12. Select **Next**.
13. Select **Add assignment**.
14. Assignment name: SecureScore Manager
15. Assign it to **Joni Sherman**. 
16. Under **Data sources**, **uncheck** everything except **Microsoft Secure Score - Additional data sources**.
17. Select, **Add**.
18. Select, **Next**.
19. Select, **Submit**.

You successfully implemented RBAC for accessing the additional data source recommendations for Joni Sherman in the Secure Score.

### Task 3 - Delegate an action

The Mark 8 Project Team of Contoso is responsible for the further development of the mobile device management, therefore you will inform the project team about your security recommendation.

1. You should still be logged into Microsoft Defender XDR portal.
2. On the left navigation pane, select **Secure Score**.
3. On the tab, select **Recommended actions**.
4. Search for **Ensure devices lock after a period of inactivity to prevent unauthorized access** and select it.
5. Select **Share**, and in the dropdown menu select **Microsoft Teams**.
6. In field **Team** select **Mark 8 Project Team** and in the **Channel** field select **Channel Research and Development**.
7. Select **Post message to Teams**.

Joni Sherman and her Mark 8 Project Team will be notified about the recommended action in their teams channel.

### Task 4 - Manage Recommendations

As Joni Sherman you received the teams notification that a specific action to increase your security posture was recommended and are going to manage the recommended action and document the solution.

In this task, you´ll manage recommended action and document your solutions.

1. Open a Microsoft Edge inPrivate window, navigate to <https://office.com> and sign in as <JoniS@WWLxZZZZZZ.onmicrosoft.com>.
2. Open Teams and open the Channel **Research and Development** in **Mark 8 Project Team**.
3. Review the message posted from the Secure Score action.
4. Open another tab in the Microsoft Edge inPrivate window, navigate to <https://security.microsoft.com>.
5. On the left navigation pane, select **Secure Score**.
6. Select the **Recommended actions** tab to see all the actions you have access to.
7. Search for **Ensure devices lock after a period of inactivity to prevent unauthorized access** and select it.
8. Select **Edit status & action plan**.
9. Check **Resolved through third party**.
10. Add a note **Currently secured with JAMF** to the **Action plan** field.
11. Select **Save and Close**.

You successfully setup additional workloads for Secure Score, assigned permission based on least privilege access and managed and delegated recommended actions to identity team of Contoso Ltd.
