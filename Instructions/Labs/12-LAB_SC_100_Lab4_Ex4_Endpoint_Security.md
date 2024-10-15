---
    lab: 4
    title: 'Exercise 4 - Endpoint Security'
---

# Endpoint Security

Contoso uses Microsoft Intune to manage its devices and provides its employees with Windows 10 and Windows 11 devices. The company has implemented several configuration profiles in the past. However, a company-wide infrastructure analysis revealed that the existing policies were created independently, making it difficult to view them holistically and trace them. As the company's cyber security architect, you have decided to consolidate all the necessary and critical configurations in one place. 

In addition, the analysis revealed that Tailwind Traders uses macOS devices in its environment. As part of the upcoming merger, you plan to prepare the Contoso tenant for the new macOS devices.

## Part 1: Design a solution (required)

In this task you will design a concept to address the challenges Contoso Ltd. is facing.

### Design Approach

In the given scenario, the following requirements can be outlined:

- Consolidate all configurations for Windows devices in one place
- Protect MacOS devices

Microsoft Endpoint Manager, with security baselines, centrally manages and secures endpoints, including desktops, laptops, mobile devices, and servers. It integrates tools like Intune and Configuration Manager, enabling efficient deployment of applications, policy enforcement, compliance, and device monitoring. 

A security baseline policy comprises a set of configuration settings recommended by Microsoft, detailing their security implications. These settings are formulated based on input from Microsoft security engineering teams, product groups, partners, and customers. These baselines encompass device configuration settings similar to those within various Intune policies. Customizing each deployed baseline enables the enforcement of necessary settings and values. When establishing a security baseline profile within Intune, you're essentially creating a template comprising multiple device configuration profiles. These recommendations must be regularly reviewed and adapted according to the respective business requirements.

### Proposed Solution

|Requirement|Solution|Action plan|
|----|----|----|
|Consolidate all configurations for Windows devices in one place|Microsoft Endpoint Manager - Endpoint Seucurity|Deploy security baseline policies
|Protect MacOS devices|Micorosft Endpoint Manager|Deploy antivirus on macOS devices|

## Part 2: Implement the solution (optional)

### Task 1: Deploy endpoint security baseline policies

Your overall goal is to secure your endpoints appropiately and consolidate as many policies as possible in one place. You will achieve this by creating endpoint security baseline policies for Windows devices in Intune.

1. Sign-in to the Microsoft Intune admin center **https://intune.microsoft.com** as Allan Deyoung using his administrator account **MOD Administrator**.
2. In the Microsoft Intune admin center, in the left navigation pane select **Endpoint Security**.
3. On the **Endpoint security | Overview** page, under **Overview** select **Security baselines**.
4. On the **Endpoint security | Security baselines** page select **Security Baseline for Windows 10 and later**.
5. On the **MDM Security Baseline | Profiles** page select **+ Create profile**.
1. Review the description on the **Create a profile** blade and select **Create**.
1. On the **Basics** blade enter a name and a description.
1. Select **Next**.
1. On the **Configuration settings** blade investigate the different configuration options. When you have finished, select **Next**.
1. On the **Scope tags** blade select **Next**.
1. On the **Assignments** blade under **Included groups** select **Add all users** and select **Next**.
1. On the **Review + create** blade select **Create**.
1. Go back to **Endpoint security | Security baselines** page.
1. On the **Endpoint security | Security baselines** page select **Microsoft Defender for Endpoint Security Baseline**.
1. On the **Microsoft Defender for Endpoint Security baseline | Profiles** select **+ Create profile**.
1. Review the description on the **Create a profile** blade and select **Create**.
1. On the **Basics** blade enter a name and a description.
1. Select **Next**.
1. On the **Configuration settings** blade investigate the different configuration options. When you have finished, select **Next**.
1. On the **Scope tags** blade select **Next**. 
1. On the **Assignments** blade, under **Included groups** select **Add all users** and select **Next**.
1. On the **Review + create** blade select **Create**.

You have successfully created two security baseline policies for Windows devices.

### Task 2: Deploy antivirus on macOS devices

After securing Windows devices with endpoint security baseline policies you will deploy antivirus and enable encrpytion on macOS devices to prepare your environment for merging with Trailwind Traders.

1. You should still be logged into the Microsoft Intune admin center **https://intune.microsoft.com**.
2. In the Microsoft Intune admin center, in the left navigation pane select **Endpoint Security**.
3. On the **Endpoint security | Overview** page under **Manage** select **Antivirus**.
4. On the **Endpoint security | Antivirus** page select **+ Create policy**.
5. On the **Create a profile** pane, under **Platform** select **macOS** and under **Profile** select **Microsoft Defender Antivirus**.
6. Select **Create**.
7. On the **Basics** blade enter a name and a description.
8. Select **Next**
9. On the **Configuration settings** blade ensure the settings are configured as follows:

#### Cloud delivered protection preferences

- **Enable / disable cloud delivered protection**: Enabled (Default)
- **Enable/ disable automatic sample submissions**: Enabled (Default)
- **Diagnostic collection level**: optional (Default)
- **Automatic security intelligence upate**: Enabled (Default)

#### Antivirus engine

- **Enable real-time protecion**: Enabled (Default)
- **Enable passive mode**: Disabled (Default)
- **Exclusion merge** : admin_only
- Under **Threat type settings** select **+ Add**
  - **Threat type**: potentially_unwanted_application
  - **Action to take**: block
- **Threat type settings merge**: admin_only
- **Enable file hash computation**: True
- **Run a scan after definitions are updated**: Enabled (Default)
- **Enforcement level**: real_time

#### Network protection

- **Enforcement level**: block
  
#### Tamper protection

- **Enforcement level**: block (Default)

#### User interface preferences

- **Control sign-in to consumer version**: enabled (Default)
- **Show / hide status menu icon**: Disabled (Default)
- **User initiated feedback**: enabled (Default)

1.  Select **Next**.
2.  On the **Scope tags** blade select **Next**.
3.  On the **Assignments** blade in the text box enter **All users** and select it.
4.  Select **Next**.
5.  On the **Review + create** blade select **Save**.

You have successfully configured and deployed antivirus for macOS devices.

### Task 3 Encrypt macOS devices

In this task you will encrypt macOS devices.

1. You should still be logged into the Microsoft Intune admin center **https://intune.microsoft.com**.
2. In the Microsoft Intune admin center, in the left navigation pane select **Endpoint Security**.
3. On the **Endpoint security | Overview** page, under **Manage** select **Disk encryption**.
4. On the **Endpoint security | Disk encryption** page select **+ Create Policy**.
5. On the **Create a profile** pane, under **Platform** select **macOS** and under **Profile** select **FileVault**.
6. Select **Create**.
7. On the **Basic** blade enter a name and description. Select **Next**.
8. On the **Configuration settings** blade under **Encryption** configure the following settings:
   - **Enable FileVault**: Yes
   - **Personal recovery key rotation**: 6 months
   - **Escrow location description of personal recovery key**: To recover a lost or recently rotated recovery key, log in to the Intune Company Portal website using any device. Navigate to the Devices section within the portal, choose the device with FileVault enabled, and then select the option to retrieve the recovery key. The portal will display the current recovery key for that device.
   - **Number of times allowed to bypass**: 3
   - **Allow deferral until sign out**: Yes
   - **Disable prompt at sign-out**: Yes
   - **Hide recovery key**: Yes
  
9.  Select **Next**.
10. On the **Scope tags** blade select **Next**.
11. On the **Assignments** blade, under **Included groups** select **Add all users**.
12. Select **Next**.
13. On the **Review + create** blade select **Create**.

You have successfully configured and deployed a FileVault profile to encrypt macOS devices.