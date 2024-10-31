# Global Secure Access

Contoso, whose IT infrastructure is all cloud-based, has recently acquired Tailwind Traders that has not yet migrated their infrastructure to the cloud. Tailwind Traders have an on-premise environment with file servers containing private resources that Contoso users need to access. Until these resources can be migrated to the cloud, the security team wants to ensure secure access to these private resources, but wants to avoid using VPN technology.

### Design Approach

Microsoft Entra Private Access allows its employees to securely remote into local servers within Tailwind Traders local infrastructure and integrates with the existing cloud infrastructure of Contoso Ltd.

Microsoft Entra Private Access is part of the Microsoft Global Secure Access solution, which enables secure and seamless access to any app or resource from anywhere. It is built on the principles of Zero Trust and delivered from Microsoft's Wide Area Network. One compelling use case is remote access to private resources. Microsoft Entra Private Access allows users to securely access private resources hosted on-premises without exposing them to the internet or requiring a VPN. This reduces the attack surface and simplifies network configuration

### Proposed solution

In this exercise, you'll set up a remote access connection from your client endpoint to a resource in your on-premise environment, using Microsoft Entra Private Access.

|Requirement|Solution|Action plan|
|----|----|----|
|Enable secure remote access for on premise server, without VPN| Global Secure Access - Private Access | Enable Global Secure Access and deploy Private Access Network Connector |
|Remote users connect to private apps in the private network. | Global Secure Access - Private Access | Enable Private Access traffic profile, install GSA client, assign users.|

### Task 1: Activate Global Secure Access

The first step is to activate Global Secure Access in your tenant.

1. Log into the **Client 1 VM** (LON-SC1) as the **lon-sc1\admin** account. The password should be provided by your lab hosting provider.
1. Open **Microsoft Edge**, select the address bar, navigate to **https://entra.microsoft.com** and log into the Entra Portal as **MOD Administrator** admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). User´s password should be provided by your lab hosting provider.
1. If you see an information box on the top right of the screen that says Manage multifactor authentication, close it by selecting the **X**.  If you are prompted to setup multifactor authentication, you will be prompted for more information. Follow the instructions.
1. On the Stay signed in? dialog box select the Don’t show this again checkbox and then select **No**.
1. Close the password save dialog from the bottom by selecting **Never**, to not save the default global admins credentials in your browser.
1. In the left navigation pane expand **Global Secure Access** and select **Dashboard**.
1. Under **Activate Global Secure Access in your Tenant** select **Activate**.

You have successfully activated Global Secure Access.

### Task 2: Deploy private network connector

The private network connector is a lightweight agent that is installed on a Windows Server, in your on-premise environment, that has access to the backend resources and applications, and is used to facilitate the connection to the Global Secure Access service.  The Windows server where the connector will be installed must have TLS 1.2 enabled before you install the private network connector.

1. Log into the Server VM, **LON-SC2**, using the local **Administrator** acount. The password should be provided by your lab hosting provider.
1. Before you install the private network connector on the server, you need to enable TLS 1.2.  There are several ways you can do this. For this exercise, you'll copy the commands to set the registry keys into a file and then run that file.
    1. On a browser tab, enter the URL: **`https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors`**.
    1. Scroll-down to the section **Transport Layer Security (TLS) requirements** and from the code box listed under **Set registry keys**, select **Copy**
    1. In the search bar of the taskbar, type **Notepad**, then select **Notepad** to open the application.
    1. Use **Ctrl + v** to paste the code into Notepad.
    1. From Notepad, select **File**. In the **Save as type** field, select **All files** from the drop-down, and in the **File name** field enter **Enable-TLS.reg**, then select **Save**.  It's important that you save the file with the .reg extension.
    1. Open **File Explorer** and navigate to the folder where you saved the file (the default is This PC > Documents).
    1. Double click the file name to run it.  Because you are changing the registry file, you are asked, **Are you sure you want to continue?**  Select **Yes**, then select **Ok**.  
    1. Since you updated the registry, you'll need to restart the server. From the taskbar of the Server VM, select the  **Windows icon**, select the **Power icon**, select **Restart**, then select **Continue**.
    1. After the restart, log back in to the Server VM.
1. Open **Microsoft Edge**, select the address bar, navigate to **`https://entra.microsoft.com`** and log into the Entra Portal as **MOD Administrator** admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). User´s password should be provided by your lab hosting provider.
1. Under **Global Secure Access** on the left navigation pane expand **Connect** and select **Connectors**.
1. Select **Download connector service**.
1. Select **Accept terms & Download**.
1. Select **Install** to install the **Private Network Connector**.
1. During the installation process you have to sign in with your username and password provided by the lab.
1. Once the installation is complete **Close** the installation window and refresh the browser page.  You should see the connector listed and active.
1. Open the **CMD** and execute the **ipconfig** command, then note down the private ip address for your server.

You should see you the onboarded VM and the associated IP address. This means you have successfully established the connector.

### Task 3: Create Share on File Server

In this task, you´ll create a SMB Share on the on premises fileserver, that will be accessed thru GSA.

1. You should still be log in to LON-SC2.
1. Open the **Explorer**, navigate to the C: Drive and create a folder named **Share**.
1. Using the right mouse key, select the Share Folder and open the **Properties**.
1. Select **Sharing**.
1. Select **Share...**.
1. From the dropdown, select **Everyone** and select **Add**.
1. Select **Share**.
1. Select **No, make the network that I am connected to a private network**.
1. Select **Done** then **Close**.

### Task 4: Setup Quick Access and assign User

Private Access provides two ways to configure the private resources that you want to tunnel through the service. Quick Access or Global Secure Access applications. For this exercise, you'll use Quick Access.

Quick Access is the primary group of FQDNs and IP addresses that you want to secure. When you configure the Quick Access, you're creating a new enterprise application that serves as a container for the private resources that you want to secure.

In order for your users to access the resources the file server through the GSA client you need to enable Quick Access and assign it to your test users.

1. You can stay in LON-SC2 for this step, as you're using the VM to access the GSA service from the Microsoft Entra admin center.
1. In the left navigation pane expand **Global Secure Access**, expand **Applications**, then select **Quick Access**. Enter the following information:
    - Name: **SMB to ContosoFS**
    - Connector Group: **Default**
1. Select **Add Quick Access application segment** and fill in the following information:
    - Destination type: **IP address**
    - IP address: the private IP address of your server that you noted in the earlier step.
    - Ports: **445**
1. Select **Apply**.
1. Select **Save**. Once you see the status field for the application segment show success, refresh the browser page. Upon refreshing the page, you're taken to the **Quick Access | Network access properties** page.
1. On the left select **User and groups**.
1. Select **Add user/group**.
1. Select **None Selected**.
1. Add **MOD Administrator**.
1. From the bottom of the page, press **Select** then select **Assign**.

You have successfully enabled quick access for your test user, in this case your admin account.

### Task 5: Device join Entra ID

In order to use Global Secure Access, you need to join the client endpoint, the LON-SC1 VM, to Microsoft Entra ID. Otherwise the GSA client will not work.

1. Switch back to the **LON-SC1** VM (this is your client endpoint VM)
1. Using the right mouse key, select the Windows icon in the task bar and select **Settings**.
1. From the left navigation panel, select **Accounts**.
1. From the Accounts page, select  **Access work or school**.
1. To add a work or school account select **Connect**.
1. From the bottom of the window, select **Join Device with Entra ID**.
1. Sign in with your **MOD Administrator** admin credentials provided by the lab provider.
1. From the **Make sure this is your organization** window, review the information then select **Join**.
1. Review the information on the **You're all set** window and select **Done**.
1. Now that your device is Entra ID  joined, logout from the local admin account and log back in using your MOD Administrator account.
    1. Close the settings page and close the browser.
    1. From the taskbar, using the right mouse key select the **Windows** icon, select **Shut down or sign out**, then select **Sign out**.
    1. From the bottom left of the window, select **Other user**, then log in with your MOD administrator account.
    1. It will take a few minutes to set up the account, then you'll see a **More information required** window appear. This will initiate the process to setup multifactor authentication.  Follow the instructions.

Once your endpoint is joined to Entra ID you will be able to use the GSA client to connect to any resources you are protecting with Global Secure Access.

### Task 6: Activate the traffic forwarding profile and download the GSA desktop client

To enable access to private resources or applications in your on-premises environment, you need to enable the traffic forwarding profile for Private Access and assign users.

You also need to download and install the Global Secure Access desktop client.  

Private access traffic can be forwarded to the service by connecting through the Global Secure Access desktop client.

1. You should still be on **LON-SC1**, to which you have signed in with the your MOD Administrator account.
1. Open **Microsoft Edge**. You'll be prompted to setup Microsoft Edge.
1. From the Microsoft Edge, navigate to **`https://entra.microsoft.com`**.
1. From the Global Secure Access menu in the left navigation pane of the Microsoft Entra admin center, expand **Connect** and choose **Traffic forwarding**.
1. Check **Private access profile** then select **OK**.
1. Now that you've enabled the private access profile, you'll need to assign users.
    1. From the Private access profile card, under **User and group assignments**, select **View**.
    1. Select where it says **0 users, 0 groups assigned**
    1. Select **Add user/group**.
    1. Select **None Selected**.
    1. In the search bar, enter **MOD**, select **MOD Administrator**, press **Select**, then select **Assign**.
1. In the left navigation pane under **Connect** choose **Client download**.
1. Under Windows 10/11 select **Download client**.
1. Once the download is complete, select **Open file**
1. Select **I agree to the license terms and conditions**, then select **Install**. In the User Account Control window that pops up, select **Yes**.
1. Once the installation successfully completes, **Close** the window.
1. On the task bar, select the up arrow to show the Global Secure Access client icon.  It can take 5-10 minutes to show with a green checkmark to indicate it is connected.
1. Open **Explorer** in Windows and navigate to **This PC** menu bar select the ellipses (...) and select **Map network drive**.
1. In the Folder field, enter `\\IP-ADDRESS\Share`. Use the IP address you are noted earlier AND select **Connect using different credentials**.
1. Select **Finish**.
1. To map the network drive, use the credentials for the local administrator account on LON-SC2.  
    1. Email field: **`Administrator`** (this may vary by lab hoster).
    1. Password field: **`Pa55w.rd`** (this may vary by lab hoster).
      >[!NOTE] It's acknowledged that using the local Administrator account is not a typical scenario. It's used in this exercise due to the simplified on-premises environment. A more realistic scenario would have the user access the private resources with their Entra ID login.  This requires synchronization of identities between Microsoft Entra and the on-premises AD DS. using Microsoft Entra Connect Sync or Entra Cloud Sync.

You have successfully connected to the file server by using Global Secure Access. In a more realistic on-premise scenario, you would have your Microsoft Entra ID users synced with on the premises server so that users could access the private resources or applications in the on-premises server using their Entra ID account.  You could also setup conditional access policies for greater security.
