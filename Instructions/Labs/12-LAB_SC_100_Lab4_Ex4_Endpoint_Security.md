# Endpoint Security

## Lab scenario

Contoso uses Microsoft Intune to manage its devices. A company-wide infrastructure analysis revealed that existing policies were created independently, making them difficult to view holistically. As the cyber security architect, you have decided to consolidate critical configurations using endpoint security baselines. Additionally, with the upcoming merger with Tailwind Traders, which uses macOS devices, you need to prepare the Contoso tenant for new macOS devices.

In this lab, you will:
- Deploy endpoint security baseline policies for Windows devices
- Deploy antivirus protection for macOS devices
- Configure disk encryption (FileVault) for macOS devices

**Estimated time: 25-35 minutes**

## Lab tasks

### Task 1: Deploy endpoint security baseline policies

Your overall goal is to secure your endpoints appropriately and consolidate as many policies as possible in one place. You will achieve this by creating endpoint security baseline policies for Windows devices in Intune.

1. Log into the Windows client VM **LON-SC1** with the local **Administrator** account. The password should be provided by your lab hosting provider.
1. Sign-in to the Microsoft Intune admin center **`https://intune.microsoft.com`** as **MOD Administrator** admin@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). User´s password should be provided by your lab hosting provider.
1. If asked to complete multifactor authentication, follow the steps.
1. In the Microsoft Intune admin center, in the left navigation pane select **Endpoint Security**.
1. On the **Endpoint security | Overview** page, under **Overview** select **Security baselines**.
1. On the **Endpoint security | Security baselines** page select **Security Baseline for Windows 10 and later**.
1. On the **Security Baseline for Windows 10 and later | Profiles** page select **+ Create policy**.
1. Review the description on the **Create a profile** blade and select **Create**.
1. On the **Basics** blade enter:
    1. Name: **`Secure Windows Endpoints`**
    1. Description: **`The Security Baseline for Windows 10 and later represents the recommendations for configuring Windows.`**.
1. Select **Next**.
1. On the **Configuration settings** blade investigate the different configuration options. When you have finished, select **Next**.
1. On the **Scope tags** blade select **Next**.
1. On the **Assignments** blade under **Included groups** select **Add all users** and select **Next**.
1. On the **Review + create** blade select **Create**.
1. Go back to **Endpoint security | Security baselines** page.
1. On the **Endpoint security | Security baselines** page select **Microsoft Defender for Endpoint Security Baseline**.
1. On the **Microsoft Defender for Endpoint Security baseline | Profiles** select **+ Create policy**.
1. Review the description on the **Create a profile** blade and select **Create**.
1. On the **Basics** blade enter:
    1. Name: **`Defender for Endpoint Security Baseline`**
    1. Description: **`Security best practices for the Microsoft security stack on devices managed by Intune`**.
1. Select **Next**.
1. On the **Configuration settings** blade investigate the different configuration options. When you have finished, select **Next**.
1. On the **Scope tags** blade select **Next**.
1. On the **Assignments** blade, under **Included groups** select **Add all users** and select **Next**.
1. On the **Review + create** blade select **Create**.

You have successfully created two security baseline policies for Windows devices.

### Task 2: Deploy antivirus on macOS devices

After securing Windows devices with endpoint security baseline policies you will deploy antivirus and enable encryption on macOS devices to prepare your environment for merging with Trailwind Traders.

1. You should still be logged into the Microsoft Intune admin center **https://intune.microsoft.com**.
1. In the Microsoft Intune admin center, in the left navigation pane select **Endpoint Security**.
1. On the **Endpoint security | Overview** page under **Manage** select **Antivirus**.
1. On the **Endpoint security | Antivirus** page select **+ Create policy**.
1. On the **Create a profile** pane, under **Platform** select **macOS** and under **Profile** select **Microsoft Defender Antivirus**.
1. Select **Create**.
1. On the **Basics** blade enter:
    1. Name: **`Deploy antivirus on macOS devices`**
    1. Description: **`Deploy antivirus and enable encryption on macOS devices to prepare your environment for merging with Trailwind Traders.`**
1. Select **Next**
1. On the **Configuration settings** tab ensure the settings are configured as follows:
1. Under **Cloud delivered protection preferences**:
    - Enable / disable cloud delivered protection: **Enabled (Default)**
    - Enable/ disable automatic sample submissions: **Enabled (Default)**
    - Diagnostic collection level: **optional (Default)**
    - Automatic security intelligence update: **Enabled (Default)**
1. Under **Antivirus engine**:
    - Enable real-time protecion: **Enabled (Default)**
    - Enable passive mode: **Disabled (Default)**
    - Exclusion merge: **admin_only**
1. Under **Threat type settings** select **+ Add**:
    - In the text box for Threat type, enter: **potentially_unwanted_application**
    - Action to take: **block**
    - Threat type settings merge: **admin_only**
1. Enable file hash computation: **True****
1. Run a scan after definitions are updated: **Enabled (Default)**
1. Enforcement level: **real_time**
1. Under **Network protection**:
    - Enforcement level: block
1. Under **Tamper protection**:
    - Enforcement level: **block (Default)**
1. Under **User interface preferences**
    - Control sign-in to consumer version: **enabled (Default)**
    - Show / hide status menu icon: **Disabled (Default)**
    - User initiated feedback: **enabled (Default)**
1. Select **Next**.
1. On the **Scope tags** blade select **Next**.
1. On the **Assignments** tab, in the text box enter **All users** and select it.
1. Select **Next**.
1. On the **Review + create** tab select **Save**.

You have successfully configured and deployed antivirus for macOS devices.

### Task 3 Encrypt macOS devices

In this task you will encrypt macOS devices.

1. You should still be logged into the Microsoft Intune admin center **https://intune.microsoft.com**.
1. In the Microsoft Intune admin center, in the left navigation pane select **Endpoint Security**.
1. On the **Endpoint security | Overview** page, under **Manage** select **Disk encryption**.
1. On the **Endpoint security | Disk encryption** page select **+ Create Policy**.
1. On the **Create a profile** pane, under **Platform** select **macOS** and under **Profile** select **MacOS FileVault**.
1. Select **Create**.
1. On the **Basic** blade enter:
    1. Name: **`Encrypt macOS devices`**
    1. Description: **`FileVault provides built-in Full Disk Encryption for macOS devices.`**
    1. Select **Next**.
1. On the **Configuration settings** expand **Full Disk Encryption** configure the following settings:
   - Defer: **Enabled**
   - Defer Don't ask At User Logout: **Enabled**.
   - Defer Force at User Login Max Bypass Attempts: set slider to **Configured** then enter **3** in the field that follows.
   - Enable FileVault: **On**
   - Personal recovery key rotation: **6 months**
   - Under FileValut Recovery Key Escrow, in the location field enter: **`To recover a lost or recently rotated recovery key, log in to the Intune Company Portal website using any device. Navigate to the Devices section within the portal, choose the device with FileVault enabled, and then select the option to retrieve the recovery key. The portal will display the current recovery key for that device.`**
   - Number of times allowed to bypass: **3**
   - Allow deferral until sign out: **Yes**
   - Disable prompt at sign-out: **Yes**
   - Hide recovery key: **Yes**
   - Select **Next**.
1. On the **Scope tags** blade select **Next**.
1. On the **Assignments** blade, under **Included groups** select **Add all users** then select **Next**.
1. On the **Review + create** blade select **Create**.

You have successfully configured and deployed a FileVault profile to encrypt macOS devices.
