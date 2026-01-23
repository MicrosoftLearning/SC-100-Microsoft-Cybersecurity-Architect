# Cross-tenant Synchronization

## Lab scenario

Contoso recently acquired Tailwind Traders and it has been difficult to determine which guests are customers or partners, and which are employees of the acquired company. You need to establish cross-tenant synchronization to enable collaboration while maintaining Zero Trust principles. You will restrict guest invitation rights, limit external access to trusted domains, and configure bidirectional user synchronization between tenants.

In this lab, you will:
- Configure cross-tenant access settings between two tenants
- Restrict external collaboration to trusted domains only
- Create and configure a cross-tenant synchronization
- Customize attribute mappings to identify synchronized users
- Provision users to the partner tenant

**Estimated time: 45-60 minutes**

## Lab tasks

### Task 1 - Team up and preparations

In this Task you will check the prerequisites of a cross-tenant synchronization and team up with a lab partner.

1. Log into the Client 1 VM (LON-Sc1) as the **lon-sc1\admin** account. The password should be provided by your lab hosting provider.
1. Open **Microsoft Edge**, select the address bar, navigate to **`https://entra.microsoft.com`** and log into the Entra ID Portal as **MOD Administrator** admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.
1. If you're asked to setup multifactor authentication, follow the instructions.
1. On the **Stay signed in?** dialog box, select the **Don’t show this again** checkbox and then select **No**.
1. Close the password save dialog box by selecting **Not now**, to not save the default global admin's credentials in your browser.
1. On the left navigation pane, expand **Entra ID** and navigate to **Overview**.
1. Note down the **Tenant ID** and the **Primary domain** that are presented under the **Overview** tab.
1. Exchange your **Tenant ID** and **Primary domain** with your lab partner.

You should have a plan what topology you want to use, what users will be in scope for the first synchronization test and how you want to map them to Contoso's Entra ID tenant.

### Task 2 - Configure cross-tenant access

Since you now have prepared the information you need for the implementation of the cross-tenant sync, you will now perform the steps necessary for your tenant to access your partners' tenant and vice versa.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com**.
1. On the left navigation pane, expand **Entra ID** then navigate to **External Identities** > **Cross-tenant access settings**.
1. Select the **Organizational settings** tab and select **Add organization**.
1. Fill out the **Tenant ID or domain name** field with the tenant ID provided by your lab partner and select **Add**.
1. Under **Inbound access** for Contoso, select **Inherited from default** to access the cross-tenant sync settings for that specific tenant.
1. Under the **Trust settings** enable **Automatically redeem invitations with the tenant Contoso**.
1. Select **Save**.
1. Under **cross-tenant sync** enable **Allow users sync into this tenant**.
1. Select **Save** and close out of the dialog by using the **X** in the top right corner.
1. Under **Outbound access** for Contoso, select **Inherited from default** to access the cross-tenant sync settings for that specific tenant.
1. Under **Trust settings** enable **Automatically redeem invitations with the tenant Contoso**.
1. Select **Save** and close out of the dialog by using the **X** in the top right corner.

You have enabled your tenant to synchronize both ways with your partner's tenant without the need for users to redeem their invitations manually.

### Task 3 - Restrict external access

In this Task you will restrict the ability to invite new guest users to your organization by controlling the scope of users with permission to send invitations. You will limit the scope of domains that can be invited as guests to your partner's tenant domain.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com**.
1. On the left navigation pane, expand **Entra ID** then navigate to **External Identities** > **External collaboration settings**.
1. In the **Guest invite settings** section, select **Member users and users assigned to specific admin roles can invite guest users including guests with member permissions**.
1. Under **Collaboration restrictions** select **Allow invitations only to the specified domains**.
1. Add your lab partner's domain **WWLxZZZZZZ.onmicrosoft.com** (where ZZZZZZ is your lab partner's unique tenant ID provided by your lab hosting provider).
1. Select **Save**.

You have now restricted who is able to invite and who can be invited to your tenant.    

### Task 4 - Create a configuration

In this Task you will create a basic configuration and test the connection to the other tenant.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com**.
1. On the left navigation pane, expand **Entra ID** then navigate to **External Identities** > **Cross-tenant synchronization** > **Configurations**.
1. Create a **New configuration**.
1. Enter the name **Contoso cross-tenant synchronization** and select **Create**.
1. Under **Provisioning** change the **Provisioning Mode** to **Automatic**.
1. In the **Tenant Id** box, enter your partner's tenant ID you noted in Task 1.
1. Select **Test Connection**.
1. Select **Save**.

If you have configured the access settings correctly, you should see a message that the supplied credentials are authorized to enable provisioning. If the test connection fails, check if your partner has entered the correct domain in Task 3 and configured cross tenant sync as described in Task 2.

### Task 5 - Define user scope

In this Task you will define who is in scope for the first synchronization.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com** in the Provisioning settings of your just created configuration. If not follow these 3 steps to get back there:
   1. On the left navigation pane, navigate to **Identity** > **External Identities** > **Cross-tenant synchronization** > **Configurations**.
   1. Select **Contoso cross-tenant synchronization**
   1. Navigate to **Provisioning**.
1. Expand the **Settings** section.
1. Verify that the Scope dropdown is set to **Sync only assigned users and groups**.
1. If you had to change this setting, select **Save**.
1. In the navigation pane, select **Users and groups**.
1. Select **Add user/group**.
1. On the **Add Assignment** page select **None Selected**.
1. Search for **Legal** and highlight the **Legal Team** by using the check box, then select **Select**.
1. Select **Assign** to add the team consisting of two users to the synchronization scope.

You have now defined your first scope of users for synchronization to your partner's tenant.

### Task 6 - Review attribute mappings

In this Task you will review the attribute mappings and make sure that the synchronized users will show up in Contoso's global address list.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com** in the **Users and groups** settings of your cross-tenant synchronization configuration. If not follow these 2 steps to get back to the configuration page:
   1. On the left navigation pane, expand **Entra ID** then navigate to **External Identities** > **Cross-tenant synchronization** > **Configurations**.
   1. Select **Contoso cross-tenant synchronization**.
1. Navigate to **Provisioning** and expand the **Mappings** section.
1. Select **Provision Microsoft Entra ID Users**.
1. Under the **showInAddressList** attribute select Edit.
1. Make sure its Mapping type is set to **Constant** and its value is set to **true**.
1. Select **Ok**.
1. Under the **displayName** attribute select **Edit**.
1. Change the Mapping type to **Expression**.
1. Remove the preexisting expression.
1. Select **Use the expression builder**.
1. Select the function **Append**.
1. In the **Select attributed** field, select the **[displayName]** attribute from the drop-down list.
1. In the **Enter suffix** field, enter **' (Contoso)'** including the space in front of the bracket but without the quotation marks.
1. Select **Add expression**. Your expression on the right should look like `Append([displayName], " (Contoso)")`
1. You can test your expression by selecting a user.
1. Select **Apply expression** and select **Ok** to leave the edit dialog.
1. Select **Save**.
1. Close the Attribute Mapping page by selecting the **X** in the top right corner.

You have now made sure, that all synchronized users will show up in the other tenant's global address list. You also have added a (Contoso) expression to the display name of every synchronized user within the other tenant.

### Task 7 - Enable provisioning and test with your lab partner

In this task you will enable the provisioning and test if your users show up in the other tenant the way you need them to. Since the automatic provisioning may take some time we will trigger a manual provisioning.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com** in the Provisioning settings of your cross-tenant synchronization configuration. If not follow these 2 steps to get back to the configuration page:
   1. On the left navigation pane, expand **Entra ID** then navigate to **External Identities** > **Cross-tenant synchronization** > **Configurations**.
   1. Select **Contoso cross-tenant synchronization**
1. Navigate to **Provision on demand**.
1. Search for **`Grady Archie`** as a member of the scoped **Legal team**.
1. Select **Provision**.
    - You will get a confirmation once the provisioning is done.
1. Close the Perform action page by selecting the **X** in the top right corner.

You have just provisioned your first user manually and when you check your partner tenant's user list, you will see the user Grady Archie (Contoso).

### Task 8 - Rollout the full synchronization

Since the first user provisioning was successfully testet you will now provision the rest of your user list to the other tenant.

1. You should still be logged into the Entra ID portal **https://entra.microsoft.com** in the **Provision on demand** page of your cross-tenant synchronization configuration. If not follow these 2 steps to get back to the configuration page:
   1. On the left navigation pane, expand **Entra ID** then navigate to **External Identities** > **Cross-tenant synchronization** > **Configurations**.
   1. Select **Contoso cross-tenant synchronization**
1. Select **Users and groups**.
1. Select **Add user/group**.
1. On the **Add Assignment** page select **None Selected**.
1. Select the **All employees** group as it is the group containing **all Contoso employees**.
1. Confirm your selection.
1. Select **Assign**.

You have now successfully created a cross-tenant synchronization between your tenant and another tenant. You should be able to adapt everything you have done in your demo tenant to Tailwind Traders' productive system and help them integrate into Contoso.
