# Cross-tenant Synchronization

Contoso recently acquired Tailwind Traders and it has been difficult to determine which guests are customers or partners, and which are employees of the acquired company. Your task is to provide an initial common address list from Tailwind Traders to Contoso. Additionally, your tenant must only allow known domain names to be added as guest users to Entra ID. You want to limit who can invite guests to the organization to internal users only. You will restrict external access to only one domain. You will also create a B2B collaboration and cross-tenant synchronization from Tailwind Traders to Contoso.

As a Cybersecurity Architect, you must ensure that all requirements are met and implement the necessary changes to Entra ID to apply Zero Trust principles. In this exercise, you will team up with a lab partner to create a cross-tenant synchronization. 

## Part 1: Design a solution (required)

In this task you will design a concept to address the requirements Contoso Ltd. and Tailwind Traders are facing.

### Design approach

The initial step involves analyzing the requirements based on the described scenario, understanding the objectives and defining the requirements.

Based on the provided use-case, the following requirements can be outlined:

- Synchronize both company's users
- Make external users identifiable as externals
- Restrict invitation rights to internal employees only 
- Restrict external access to company trusted domains

In the second step examine Contoso Ltd.'s existing environment. Microsoft Entra ID offers solutions to enable external collaboration. Investigate which controls exist and which policies are already in place. Use the Entra ID portal to review current configurations and policies and determine what adjustments must be implemented to meet the requirements for the carve in.

The third phase involves crafting the solution's concept. Upon investigation, it is evident that cross-tenant synchronization is the best way to enable collaboration meeting all the requirements.  

### Proposed solution

|Requirement|Solution|Action plan|
|----|----|----|
|Restrict invitation rights to internal employees only|External collaboration settings|Limit invitation rights to members of the tenant and specific admin invitation roles|
|Block invitations from all but the list of trusted domains|External collaboration settings|Create an invitation whitelist including only trusted domains|
|Synchronize both company's users|Entra ID Cross-tenant synchronization|Establish access trust between both Entra ID tenants and create a configuration that synchronizes users to the other tenant|
|Make external users identifiable as externals|Cross-tenant attribute mapping|Edit the displayName attribute of every user synchronized by creating a custom expression using the attribute mapping function of the Cross-tenant synchronization configuration|

## Part 2: Implement the solution (optional)

### Task 1 - Team up and preparations

In this Task you will check the prerequisites of a cross-tenant synchronization and team up with a lab partner.

1. Log into the Client 1 VM (LON-Sc1) as the **lon-sc1\admin** account. The password should be provided by your lab hosting provider.
2. Open **Microsoft Edge**, select the address bar, navigate to **https://entra.microsoft.com** and log into the Entra ID Portal as **MOD Administrator** admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.
3. On the **Stay signed in?** dialog box, select the **Don’t show this again** checkbox and then select **No**.
4. Close the password save dialog from the bottom by selecting Never, to not save the default global admins credentials in your browser.
5. On the left navigation pane, navigate to **Identity** > **Overview**.
6. Note down the **Tenant ID** and the **Primary domain** that are presented under the **Overview** tab.
7. Exchange your **Tenant ID** and **Primary domain** with your lab partner.

You should have a plan what topology you want to use, what users will be in scope for the first synchronization test and how you want to map them to Contoso's Entra ID tenant.

### Task 2 - Configure cross-tenant access

Since you now have prepared the information you need for the implementation of the cross-tenant sync, you will now perform the steps necessary for your tenant to access your partners' tenant and vice versa.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com**.
2. On the left navigation pane, navigate to **Identity** > **External Identities** > **Cross-tenant access settings**.
3. Select the ** Organizational settings** tab and select **Add organization**.
4. Fill out the **Tenant ID or domain name** field with the tenant ID provided by your lab partner and select **Add**.
5. Under **Inbound access** for Contoso, select **Inherited from default** to access the cross-tenant sync settings for that specific tenant.
6. Under the **Trust settings** enable **Automatically redeem invitations with the tenant Contoso**.
7. Select **Save**.
8. Under **cross-tenant sync** enable **Allow users sync into this tenant**.
9. Select **Save** and close out of the dialog by using the **X** in the top right corner.
10. Under **Outbound access** for Contoso, select **Inherited from default** to access the cross-tenant sync settings for that specific tenant.
11. Under **Trust settings** enable **Automatically redeem invitations with the tenant Contoso**.
12.  Select **Save** and close out of the dialog by using the **X** in the top right corner.

You have enabled your tenant to synchronize both ways with your partner's tenant without the need for users to redeem their invitations manually. 

### Task 3 - Restrict external access

In this Task you will restrict the ability to invite new guest users to your organization by controlling the scope of users with permission to send invitations. You will limit the scope of domains that can be invited as guests to your partner's tenant domain.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com**.
2. On the left navigation pane, navigate to **Identity** > **External Identities** > **External collaboration settings**.
3. In the **Guest invite settings** section, select **Member users and users assigned to specific admin roles can invite guest users including guests with member permissions**.
4. Under **Collaboration restrictions** select **Allow invitations only to the specified domains**.
5. Add your partner's domain **WWLxZZZZZZ.onmicrosoft.com** (where ZZZZZZ is your partner's unique tenant ID provided by your lab hosting provider).
6. Select **Save**.

You have now restricted who is able to invite and who can be invited to your tenant. 

### Task 4 - Create a configuration

In this Task you will create a basic configuration and test the connection to the other tenant.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com**.
2. On the left navigation pane, navigate to **Identity** > **External Identities** > **Cross-tenant synchronization** > **Configurations**.
3. Create a **New configuration**.
4. Enter the name **Contoso cross-tenant synchronization** and select **Create**.
5. Under **Provisioning** change the **Provisioning Mode** to Automatic.
6. In the **Tenant Id** box, enter your partner's tenant ID you noted in Task 1.
7. Select **Test Connection**.
8. Select **Save**.

If you have configured the access settings correctly, you should see a message that the supplied credentials are authorized to enable provisioning. If the test connection fails, check if your partner has entered the correct domain in Task 3 and configured cross tenant sync as described in Task 2.

### Task 5 - Define user scope

In this Task you will define who is in scope for the first synchronization. 

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com** in the Provisioning settings of your just created configuration. If not follow these 3 steps to get back there:
   1. On the left navigation pane, navigate to **Identity** > **External Identities** > **Cross-tenant synchronization** > **Configurations**.
   2. Select **Contoso cross-tenant synchronization**
   3. Navigate to **Provisioning**.
2. Expand the **Settings** section.
3. Verify that the Scope dropdown is set to **Sync only assigned users and groups**.
4. If you had to change this setting, select **Save**.
5. In the navigation pane, select **Users and groups**.
6. Select **Add user/group**.
7. On the **Add Assignment** page select **None Selected**.
8. Search for **Legal** and highlight the **Legal Team** by using the check box, then select **Select**.
9. Select **Assign** to add the team consisting of two users to the synchronization scope.

You have now defined your first scope of users for synchronization to your partner's tenant.

### Task 6 - Review attribute mappings

In this Task you will review the attribute mappings and make sure that the synchronized users will show up in Contoso's global address list.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com** in the **Users and groups** settings of your cross-tenant synchronization configuration. If not follow these 2 steps to get back to the configuration page:
   1. On the left navigation pane, navigate to **Identity** > **External Identities** > **Cross-tenant synchronization** > **Configurations**.
   2. Select **Contoso cross-tenant synchronization**.
2. Navigate to **Provisioning** and expand the **Mappings** section.
3. Select **Provision Microsoft Entra ID Users**.
4. Under the **showInAddressList** attribute select Edit.
5. Make sure its Mapping type is set to **Constant** and its value is set to **true**.
6. Select **Ok**.
7. Under the **displayName** attribute select **Edit**.
8. Change the Mapping type to **Expression**.
9. Remove the preexisting expression.
10. Select **Use the expression builder**.
11. Select the function **Append**.
12. Select the **[displayName]** attribute.
13. Enter **' (Contoso)'** including the space in front of the bracket but without the quotation marks.
14. Select **Add expression**.
    -  Your expression on the right should look like `Append([displayName], " (Contoso)")`
15. You can test your expression by selecting a user.
16. Select **Apply expression** and select **Ok** to leave the edit dialog.
17. Select **Save**.
18. Close the Attribute Mapping page by selecting the **X** in the top right corner.

You have now made sure, that all synchronized users will show up in the other tenant's global address list. You also have added a (Contoso) expression to the display name of every synchronized user within the other tenant.

### Task 7 - Enable provisioning and test with your lab partner

In this task you will enable the provisioning and test if your users show up in the other tenant the way you need them to. Since the automatic provisioning may take some time we will trigger a manual provisioning.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com** in the Provisioning settings of your cross-tenant synchronization configuration. If not follow these 2 steps to get back to the configuration page:
   1. On the left navigation pane, navigate to **Identity** > **External Identities** > **Cross-tenant synchronization** > **Configurations**.
   2. Select **Contoso cross-tenant synchronization**
2. Navigate to **Provision on demand**.
3. Search for **Grady Archie** as a member of the scoped **Legal team**.
4. Select **Provision**.
    - You will get a confirmation once the provisioning is done.
5. Close the Perform action page by selecting the **X** in the top right corner.

You have just provisioned your first user manually and when you check your partner tenant's user list, you will see the user Grady Archie (Contoso).

### Task 8 - Rollout the full synchronization

Since the first user provisioning was successfully testet you will now provision the rest of your user list to the other tenant.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com** in the **Provision on demand** page of your cross-tenant synchronization configuration. If not follow these 2 steps to get back to the configuration page:
   1. On the left navigation pane, navigate to **Identity** > **External Identities** > **Cross-tenant synchronization** > **Configurations**.
   2. Select **Contoso cross-tenant synchronization**
2. Select **Users and groups**.
3. Select **Add user/group**.
4. On the **Add Assignment** page select **None Selected**.
5. Select the **All employees** group as it is the group containing **all Contoso employees**.
6. Confirm your selection.
7. Select **Assign**.

You have now successfully created a cross-tenant synchronization between your tenant and another tenant. You should be able to adapt everything you have done in your demo tenant to Tailwind Traders' productive system and help them integrate into Contoso.
