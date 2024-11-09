# Setup lab

The purpose of this setup lab is to get Microsoft Defender XDR ready by the time you get to the second lab.

### Task - Set up Microsoft Defender XDR

In this task you will trigger the process for Defender to prepare new spaces for your data and connects them so it is ready by the time you get to the second lab.

1. Log into the Windows client VM **LON-SC1** with the local **Administrator** account. The password should be provided by your lab hosting provider.
1. Open **Microsoft Edge**, select the address bar, navigate to **`https://security.microsoft.com`** and log into Microsoft Defender as **MOD Administrator** admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.
1. On the **Stay signed in?** dialog box, select the **Don’t show this again** checkbox and then select **No**.
1. Close the password save dialog from the bottom by selecting **Never**, to not save the default global admins credentials in your browser.
1. If you see an information box on the top right of the screen that says **Manage multifactor authentication**, close it by selecting the **X**.
1. On the left navigation pane, expand **System** then select **Settings**, then select **Microsoft Defender XDR**.
1. Under the section **General**, select **Permissions and roles**.
1. Since this is the first time you are accessing Microsoft Defender settings, it will take some time for Defender to prepare new spaces for your data and connects them.
1. Keep this browser tab open, you'll come back to it in the second lab.

You have initiated the process for Defender to prepare new spaces for your data and connects them so it is ready by the time you get to the second lab.  Keep the browser tab open and proceed to your first lab.