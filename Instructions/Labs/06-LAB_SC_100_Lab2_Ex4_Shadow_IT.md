# Shadow-IT

## Lab scenario

Over the years, Contoso's various departments have independently adopted cloud applications to meet their specific needs—marketing uses design tools, sales relies on CRM platforms, and development teams have their own collaboration apps. With the recent shift to hybrid work, employees have also started using personal productivity apps to stay connected. As a result, IT lacks full visibility into the applications being used across the organization. As the cyber security architect, you need to discover all applications in use (Shadow IT) and block insecure applications using Microsoft Defender for Cloud Apps.

In this lab, you will:
- Integrate Microsoft Defender for Endpoint with Defender for Cloud Apps
- Investigate discovered applications and their risk scores
- Block unsafe applications manually
- Create an automated policy to unsanction risky applications

**Estimated time: 20-30 minutes**

## Lab tasks

### Task 1: Integrate Microsoft Defender for Endpoint with Defender for Cloud Apps

In order to control the use of application on users company owned devices you must integrate Defender for Endpoint with Defender for Cloud Apps.

1. Sign-in to the Microsoft Defender portal **`https://security.microsoft.com`** as Allan Deyoung using his administrator account **MOD Administrator**.
1. In the Microsoft Defender portal, expand **Investigation & response** then expand **Hunting** and select **Advanced Hunting**. Wait for the completion of the new spaces preparation.  This step is only for the purpose of setting up the new spaces, there is no hunting in this step.
1. In the Microsoft Defender portal, in the left navigation page expand **System** then select **Settings**.
1. On the **Settings** page select **Endpoints**. NOTE: It can take anywhere from 10 minutes to 1 hour for this option to appear. If after 10 minutes, you don't see it, continue with another exercise and then come back to this step.
1. Under **Endpoints**, select **Advanced features**. Scroll down until you see Microsoft Defender for Cloud Apps.  Select the slider to set it to **On**.
1. At the bottom of the page, select **Save preferences**.

You have successfully enabled Microsoft Defender for Cloud Apps for Endpoints. With this set-up all signals coming from Microsoft Defender for Endpoints are forwarded to Defender for Cloud Apps giving you the ability to block unsecure applications. All applications tagged as **Unsanctoned** will now be blocked.

### Task 2: Investigate the Shadow-IT of Contoso Ltd

In this task, you will analyze all the applications currently used in your company. You will take a closer look at various applications and their respective risk assessment as well as their assessment structure.

1. You should still be logged into the Microsoft Defender portal **https://security.microsoft.com/**.
1. In the Microsoft Defender portal, in the left navigation page expand **Cloud apps** and select **Cloud discovery**.
1. On the **Cloud Discovery** page select **Discovered apps**.
1. The **Discovered apps** blade displays all applications currently utilized within your organization. Explore multiple applications and their associated risk scores by selecting each respective application.

> [!NOTE] Defender for Cloud Apps assesses risks by evaluating regulatory certification, industry standards, and best practices. The score reflects the maturity of the app's suitability for enterprise use. It calculates a total score for each app by averaging weighted subscores across various risk categories that include considerations for reliability.

You have successfully reviewed several applications that are currently used at Contoso.

### Task 3: Block unsecure applications

Once you have successfully gained an overview of the use of applications in your environment, your first remediation action is to block unsafe applications.

1. You should still be logged into the Microsoft Defender portal **https://security.microsoft.com/**.
1. In the Microsoft Defender portal, in the left navigation page expand **Cloud apps** and select **Cloud discovery**.
1. On the **Cloud Discovery** page select **Discovered apps**.
1. Set the filter for **Risk score** to 0 - 4.
1. Select **Bulk selection** then select **All**.
1. Select the three dots for **More actions**.
1. Select **Tag as unsanctioned**.
1. Select **Save**.

You have successfully blocked vulnerable applications from being used by users.

### Task 4: Block unsecure applications automatically

In order to automatically block unsafe applications in the future, you will create a custom app discovery policy. This policy will tag unsafe applications as **Unsanctioned**. As you have integrated Defender for Endpoint with Defender for Cloud Apps, these applications will be blocked automatically.

1. You should still be logged into the Microsoft Defender portal **https://security.microsoft.com/**.
1. In the Microsoft Defender portal, in the left navigation page expand **Cloud apps** and select **Cloud app catalog**.
1. On the **Cloud app catalog** page select **+ New policy from search**.
1. Enter the following information:
    - **Policy Name**: Tag unsafe apps as unsanctioned
    - **Policy severity**: Medium
    - **Description for users**: Applications with a risk score of 4 or lower will be unsanctioned and blocked automatically.
1. Under **Apps matching all of the following** add a filter and set it to **Risk score equals 0-4**, by moving the slider, then select **Apply**.
1. Under **Alerts** select **Create an alert for each matching event with the policy's severity** and set the value for **Daily alert limit per policy** to 5.
1. Under **Governance actions** select **Tag app as unsanctioned**.
1. Select **Create**.

You have successfully created a policy to tag applications with a risk score of 5 or lower as unsanctioned.