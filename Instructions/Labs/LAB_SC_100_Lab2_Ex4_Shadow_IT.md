---
    lab: 3
    title: 'Exercise 4 - Shadow-IT'
---


# Lab 2 - Exercise 4 - Shadow-IT

Contoso's IT infrastructure has evolved over the past decades, providing various server instances, applications, and services. The company has recently prioritized securing its environment, with the implementation of Device Management, data governance, and Identity and Application Protection over the last two years. However, the process of restricting users to only specific applications deployed by the company has not yet been established, allowing users to install applications from various sources. As the organisation's cyber security architect, you aim to have a complete overview of all applications used by employees. Your protection measure is to block insecure applications in your environment.

## Part 1: Design a solution (required)

In this task you will design a concept to adress the challenges Contoso Ltd. is facing.

### Design Approach

In the given scenario, your initial action is to analyze and uncover all applications currently in use by employees. Unauthorized applications installed by users can pose security risks to the company, highlighting the need to identify Shadow IT. The subsequent step involves remedying the risks posed by these unsafe applications.

Defender for Cloud Apps is a security solution designed to address Shadow IT risks within cloud environments. It aids organizations in discovering and monitoring unauthorized cloud applications utilized by employees, evaluating their security posture, and enforcing policies to ensure compliance and safeguard data. By offering visibility and control over Shadow IT, Defender for Cloud Apps assists organizations in mitigating security risks associated with unauthorized cloud usage, thereby enhancing the security of their cloud environment.

### Proposed Solution

|Requirement|Solution|Action plan|
|----|----|----|
|Discover Shadow IT|Microsoft Defender for Cloud Apps|Investigate all applications in the Contoso environment|
|Block all unsafe applications|Microsoft Defender for Cloud Apps|Mark unsafe applications as unsanctioned|

## Part 2: Implement the solution (optional)

### Task 1: Integrate Microsoft Defender for Endpoint with Defender for Cloud Apps

In order to control the use of application on users company owned devices you must integrate Defender for Endpoint with Defender for Cloud Apps.

1. Sign-in to the Microsoft Defender portal **https://security.microsoft.com/** as Allan Deyoung using his administrator account **MOD Administrator**.
2. In the Microsoft Defender portal, expand **Hunting** and select **Advanced Hunting**. Wait for the completion of the new spaces preparation.
3. In the Microsoft Defender portal, in the left navigation page select **Settings**.
4. On the **Settings** page select **Endpoints**.
5. On the **Endpoints** page, under **General** select **Advanced features**.
6. Enable **Microsoft Defender for Cloud Apps**.
7. Select **Save preferences** at the bottom.

You have successfully enabled Microsoft Defender for Cloud Apps for Endpoints. With this set-up all signals coming from Microsoft Defender for Endpoints are forwared to Defender for Cloud Apps giving you the ability to block unsecure applications. All applications tagged as **Unsanctoned** will now be blocked.

### Task 2: Investigate the Shadow-IT of Contoso Ltd.

In this task, you will analyse all the applications currently used in your company. You will take a closer look at various applications and their respective risk assessment as well as their assessment structure.

1. You should still be logged into the Microsoft Defender portal **https://security.microsoft.com/**.
2. In the Microsoft Defender portal, in the left navigation page expand **Cloud apps** and select **Cloud discovery**.
3. On the **Cloud Discovery** page select **Discovered apps**.
4. The **Discovered apps** blade displays all applications currently utilized within your organization. Explore multiple applications and their associated risk scores by selecting each respective application.

> [!NOTE] Defender for Cloud Apps assesses risks by evaluating regulatory certification, industry standards, and best practices. The score reflects the maturity of the app's suitability for enterprise use. It calculates a total score for each app by averaging weighted subscores across various risk categories that include considerations for reliability.

You have successfully reviewed several applications that are currently used at Contoso.

### Task 3: Block unsecure applications

Once you have successfully gained an overview of the use of applications in your environment, your first remediation action is to block unsafe applications.

1. You should still be logged into the Microsoft Defender portal **https://security.microsoft.com/**.
2. In the Microsoft Defender portal, in the left navigation page expand **Cloud apps** and select **Cloud discovery**.
3. On the **Cloud Discovery** page select **Discovered apps**.
4. Set the filter for **Risk score** to 0 - 4.
5. Select **Bulk selection** then select **All**.
6. Select the three dots for **More actions**.
7. Select **Tag as unsanctioned**.
8. Select **Save**.
   
You have successfully blocked vulnerable applications from being used by users.

### Task 4: Block unsecure applicatons automatically

In order to automatically block unsafe applications in the future, you will create a custom app discovery policy. This policy will tag unsafe applications as **Unsanctioned**. As you have integrated Defender for Endpoint with Defender for Cloud Apps, these applications will be blocked automatically.

1. You should still be logged into the Microsoft Defender portal **https://security.microsoft.com/**.
2. In the Microsoft Defender portal, in the left navigation page expand **Cloud apps** and select **Cloud discovery**.
3. On the **Discovered apps** page select **+ New policy from search**.
4. Enter the following information:
    - **Policy Name**: Tag unsafe apps as unsanctioned
    - **Policy severity**: Medium
    - **Description for users**: Applications with a risk score of 4 or lower will be unsanctioned and blocked automatically.
5. Under **Apps matching all of the following** add a filter and set it to **Risk score equals 0-4**.
6. Under **Alerts** select **Create an alert for each matching event with the policy's severity** and set the value for **Daily alert limit per policy** to 5.
7. Under **Governance actions** select **Tag app as unsanctioned**.
8. Select **Create**.

You have successfully created a policy to tag applications with a risk score of 5 or lower as unsanctioned.