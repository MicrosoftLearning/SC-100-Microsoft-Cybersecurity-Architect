# Lab 4 - Exercise 2 - Global Secure Access

After setting up the monitoring server, you need to establish secure networking to the file server using Global Secure Access (GSA). You want to ensure that access to these machines is secured until these file servers can be migrated to secure cloud storage, especially if Tailwind Traders is bringing local servers into your company IT infrastructure. You decided against reworking the VPN infrastructure of Tailwind Traders to allow your employees access to the servers. 

To establish secure networking, you will start by creating an Azure App Proxy and enrolling the client to Entra ID, before creating a connector. After that, you will configure an access policy and install the GSA client. Finally, you will test the GSA connection to ensure that everything is working properly.

## Part 1: Design a solution (required)

In this task you will secure remote access to your on premise environment.

### Design approach

The initial step involves analyzing the requirements based on the described scenario, understanding the objectives and defining the requirements.

Based on the provided use-case, the following requirements can be outlined:

- Enable secure remote access for on premise servers
- Integrate with existing infrastructure
- Do not use deprecated infrastructure of Tailwind Traders

Global Secure Access integrates with the existing cloud infrastructure of Contoso Ltd. and allows your employees to securely remote into local servers within Tailwind Traders local infrastructure. Review GSA and consider the differences to other strategies for remote access to services.

### Proposed solution
<!--BITE AUSFÜLLEN-->
|Requirement|Solution|Action plan|
|----|----|----|
|Enable secure remote access for on premise servers| EntraID Global Secure Access | Enable Global Secure Access  |
|Integrate with existing infrastructure | Application Proxy | Deploy Application proxy on Contoso´s Fileserver |

## Part 2: Implement the solution (optional)

## Task 1: Activate Global Secure Access

The first step is to activate Global Secure Access in your tenant. This will allow you to use an Azure App Proxy to provide secure access to OnPremises resources.

1. Log into the **Client 1 VM** (LON-SC1) as the **lon-sc1\admin** account. The password should be provided by your lab hosting provider.
2. Open **Microsoft Edge**, select the address bar, navigate to **https://entra.microsoft.com** and log into the Entra Portal as **MOD Administrator** admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). User´s password should be provided by your lab hosting provider.
3. You will be asked to setup multifactor authentication, follow the instructions.
4. On the Stay signed in? dialog box select the Don’t show this again checkbox and then select **No**.
5. Close the password save dialog from the bottom by selecting Never, to not save the default global admins credentials in your browser.
6. In the left navigation pane expand **Global Secure Access** and select **Dashboard**.
7. Under **Activate Global Secure Access in your Tenant** select **Activate**.

You have successfully activated Global Secure Access.

## Task 2: Deploy Application Proxy

Global Secure Access is based on Application Proxy which will allow you to create a secure cloud endpoint for your local resources. In this case you will allow the test server you have set up earlier to communicate through the proxy infrastructure.

1. Log into the **Server 1 VM** (LON-SC2) as the **lon-sc1\admin** account. The password should be provided by your lab hosting provider.
2. Open **Microsoft Edge**, select the address bar, navigate to **https://entra.microsoft.com** and log into the Entra Portal as **MOD Administrator** admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). User´s password should be provided by your lab hosting provider.
3. Under **Global Secure Access** on the left navigation pane expand **Connect** and select **Connectors**.
4. Select **Download connector service**.
5.  Select **Accept terms & Download**.
6.  Install the **Microsoft Azure Active Directory Application Proxy Connector**.
7.  During the installation process you have to sign in with your username and password provided by the lab.
8.  Open the **CMD** and execute the **ipconfig** command, then note down the ip address.
9.  Go back to the Entra portal and refresh the Connectors page.

You should see you the onboarded VM and the associated IP address. This means you have successfully established the connector.

## Task 3: Create Share on File Server

In this task, you´ll create a SMB Share on the on premises Fileserver, that will be accessed thru GSA.

1. You should still be log in to LON-SC2.
2. Open the **Explorer**, navigate to the C: Drive and create a folder named **Share**.
3. Select the Share Folder and open the **Properties**.
4. Select **Sharing**.
5. Select **Share...**.
6. Select **Everyone** from the dropdown and select **Add**.
7. Select **Share**.
8. Select **No, make the network that I am connected to a private network**.

## Task 4: Setup Quick Access and assign User

In order for your users to access the file server through the GSA client you need to enable Quick Access and assign it to your test users. Without this configuration the test user will not be able to connect to the file server.

1. In the left navigation pane expand **Applications** and select **Quick Access**. Enter the following information:
    - Name: **SMB to ContosoFS**
    - Connector Group: **Default**
1. Select **Add Quick Access application segment** and fill in the following information:
    - Destination type: IP address
    - IP address: "**YOUR VM IP**"
    - Ports: 445
1. Select **Apply**.
1. Select **Save** and reload the Quick Access menu.
1. On the left select **User and groups**.
1. Select **Add user/group**.
1. Select **None Selected**.
1. Add **MOD Administrator**.
1. Click **Select** > **Assign**.

You have successfully enabled quick access for your test user, in this case your admin account.

## Task 5: Device join Entra ID

In order to use Global Secure Access, you need to join the client endpoint to Entra ID. Otherwise the GSA client will not work.

1. Connect to LON-SC1, open the start menu and select **Settings**.
2. Select **Accounts** > **Access work or school**.
3. To add a work or school account select **Connect**.
4. Click on **Join Device with Entra ID**.
5. Sign in with your **MOD Administrator** admin credentials provided by the lab provider.

Once your endpoint is joined to Entra ID you will be able to use the GSA client to connect to any resources you are protecting with Global Secure Access.

## Task 6: Activate profile and validate connection

Global Secure Access is split into two parts. The part you are working on is called Private Access and secures your local and private resources like file servers or OnPremises applications. To enable access to your file server you have to enable the private access profile which allows users to access resources that are assigned to them through Quick Access.

1. From the Global Secure Access menu in the left navigation pane of the Microsoft Entra admin center, expand **Connect** and choose **Traffic forwarding**.
2. Check **Private access profile**.
3. Select **OK**.
4. In the left navigation pane under **Connect** choose **Client download**.
5. Under Windows 10/11 select **Download client**.
6. Install the **Global Secure Access Client**.
7. During installation process you have to sign with your MOD Administrator.
8. Open **Explorer** in Windows and navigate to **This PC** menu bar select the ellipses (...) and select **Map network drive**.
9. Folder: `\\IP-ADDRESS\Share`
Use the Ipaddress you are noted earlier.
10. Select **Finish**.
11. Enter the local Username and Password to map the network drive.


You have successfully connected to the file server by using Global Secure Access.
