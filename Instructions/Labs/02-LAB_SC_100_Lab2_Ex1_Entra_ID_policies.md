# Configure Entra ID

## Lab scenario

Following the acquisition of Tailwind Traders, Contoso Ltd. needs to strengthen Entra ID security policies. You will restrict third-party application consent, enable admin consent workflows, and create a hardened authentication strength policy to eliminate SMS-based authentication methods.

In this lab, you will:
- Configure user consent settings to limit third-party app permissions
- Set up admin consent request workflows
- Create a custom authentication strength policy excluding SMS and voice methods

**Estimated time: 15-20 minutes**

## Lab tasks

**Note:** These lab steps must be executed on the M365 Lab Profile.

### Task 1 - Restrict use of third-party apps to Microsoft verified services

In this task you will restrict the level of access a user can grant to applications. You will also add the functionality for users to request access they are not able to permit themselves. 

1. Log into the Client 1 VM (LON-Sc1) as the **lon-sc1\admin** account. The password should be provided by your lab hosting provider.
1. Open **Microsoft Edge**, select the address bar, navigate to **`https://entra.microsoft.com`** and log into the Entra ID Portal as **MOD Administrator** admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). The admin password should be provided by your lab hosting provider.
1. If you're asked to setup multifactor authentication, follow the instructions.
1. On the **Stay signed in?** dialog box, select the **Don’t show this again** checkbox and then select **No**.
1. Close the password save dialog box by selecting **Not now**, to not save the default global admin's credentials in your browser.
1. On the left navigation pane, navigate to **Entra ID> Enterprise apps > Consent and permissions** (listed under security).
1. Navigate to **Permission classifications**.
1. Entra will suggest the most used permissions for **low risk** permissions.
1. Check all these permissions and select **Yes, add selected permissions** to classify them as **low risk** in your Entra ID tenant.
1. Navigate to **User consent settings**.
1. Select the option **Allow user consent for apps from verified publishers, for selected permissions**. This enables users to consent for permissions classified as "low impact" (that you previously selected), for apps from verified publishers.
1. Select **Save**.
1. Navigate to **Admin consent settings** and enable Admin consent requests by selecting **Yes**, to allows users to request admin consent to aps they are unable to content to.
1. Select **+ Add users** to add **`Lidia Holloway`** and **`MOD Administrator`** as users that can review admin consent requests.
1. Select **Save** on the **Admin consent settings** window.
1. Keep this browser tab open for the next task.

You have now configured the application consent settings limiting the access every user can grant to applications. Users can still request permission consent to applications and the application admin team can approve of them after evaluating the need and risk for the specific application.

### Task 2 - Create an Authentication strength

In this Task you will use the Entra ID portal to create an own Authentication strength to restrict the use of SMS OTP within your organization. 

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com**.
2. On the left navigation pane, expand **Entra ID** then navigate to **Authentication methods** > **Authentication strengths**.
3. Select **+ New authentication strength**.
4. Enter the name **Hardened MFA**.
5. Check **Phishing-resistant MFA**, **Passwordless MFA** and **Multifactor authentication**.
6. Under Multifactor authentication uncheck the following:
   - **Temporary Access Pass (Multi-use)**
   - **Password + SMS**
   - **Password + Voice**
   - **Federated Single factor + SMS**
   - **Federated Single factor + Voice**.
7. Select **Next**.
8. Review and check, that none of the above factors are left in the authentication strength.
9.  Select **Create**.

You have now created an authentication strength that restricts the use of SMS OTP as an authentication factor.
