# Security Operations Center

## Exercise Overview

Contoso has a Security Operations Center (SOC) that monitors and responds to security incidents across the enterprise. The SOC is staffed with security analysts, security engineers, and network engineers. The SOC has decided to use Microsoft Sentinel as their Security Information and Event Management (SIEM) solution. To collect and analyze security logs from across the enterprise, the SOC has a log analytics workspace. The SOC has a requirement to secure access to the log analytics workspace based on the principle of least privilege. The SOC has two different roles, security analyst and security engineer, with different permission requirements. The network team has a requirement to access only the Cisco Umbrella logs.

## Part 1: Design a solution (required)

In this task, you'll design a concept for monitoring and responding to security events with specific access permissions for Contoso's Security Operations Center.

### Design approach

The initial step involves analyzing the requirements based on the described scenario, understanding the objectives, and defining the requirements.

Based on the provided use case, the following requirements can be outlined:

- Deploy SIEM/SOAR Solution
- Limit access to specific SOC roles
- Create a dashboard with custom views for incidents and their alerts

In this scenario, you deploy the SIEM SOAR solution based on Microsoft Sentinel, set up role-based access control in the workspace context, and limit access for the network team to a single table in the log analytics workspace. Workbooks allow security analysts and administrators to visualize security data using graphical displays. They provide a tool for presenting and analyzing data in a dashboard.

### Proposed solution

| Requirement | Solution | Action plan |
| ---- | ---- | ---- |
| Deploy SIEM/SOAR Solution | Microsoft Sentinel, Log Analytics Workspace | Set up log analytics workspace and deploy Microsoft Sentinel |
| Limit access to specific SOC roles | Log Analytics Workspace, Role-based Access Control | Set up RBAC for Log Analytics Workspace |
| Create a dashboard with custom views for incidents and their alerts | Microsoft Sentinel, Workbook | Create a workbook with a custom view on current incidents and alerts |

## Part 2: Implement the solution (optional)

### Task 1 - Create Log Analytics Workspace

In this task, you'll create a log analytics workspace which is required to house all of the data that Microsoft Sentinel will be ingesting and using for its detections and analytics.

1. Log into the Client 1 VM (LON-SC1) as the **lon-sc1\admin** account. The password should be provided by your lab hosting provider.
2. Open **Microsoft Edge**, select the address bar, navigate to **`https://portal.azure.com`** and log into the Azure Portal as user **User1-*******@LODSUATMCA.onmicrosoft.com** (where ****** is your unique tenant ID provided by your lab hosting provider). User´s password should be provided by your lab hosting provider.
3. On the Stay signed in? dialog box, select the Don’t show this again checkbox and then select **No**.
4. Close the password save dialog from the bottom by selecting Never, to not save the default global admins credentials in your browser.
5. Cancel Welcome to Microsoft Azure screen.
6. Select **Create a resource** and search for **log analytics workspace**
7. Find the **Log Analytics Workspace tile**, select **Create**.
8. On Create Log Analytics workspace site, create a new **Resource Group** and name it **`rg_eastus_soc`**.
9. In Instance details enter the name **`law-sentinel`**, select **East US** for region.
10. Select **Review & Create**
11. Select **Create** to start the deployment.

You successfully created the log analytics workspace for your Sentinel deployment.

### Task 2 - Create Sentinel

In this task, you will add Sentinel to the created log analytics workspace and add demo logs, because the demo tenant doesn't have an existing data in the log analytics workspace, you import demo logs to have a better idea of how sentinel works.

1. You should still be logged into the Azure portal **https://portal.azure.com**.
1. In the search bar, in the blue banner at the top of the page, enter **Microsoft Sentinel**, then select it from the search results listed under services.
1. From the **Microsoft Sentinel** page, select **Create**.
1. In the **Add a Microsoft Sentinel to a workspace page** the previously created log analytics workspace should be listed.  Select **law-sentinel** then select **Add**.
1. It may take a few minutes to add Sentinel to the workspace.  Once it's added, the **Microsoft Sentinel | New & guides** page is displayed.  You're notified that the Microsoft Sentinel fre trial is activated.  Select **Ok**.
1. From the center of the page, select **Go to content hub**.  Alternatively, from the left navigation panel expand **Content management** then select **Content hub**.
1. From the Content Hub, you will install **Microsoft Sentinel Training Lab**.  To find this solution, filter on **Provider = Microsoft** and **Category = Training and Tutorials**. Once these filters are set and applied,  **Microsoft Sentinel Training Lab**, will be listed. Select it from the search results, and **Install** the solution.
1. Select **Create**.
1. Choose the resource group **rg_eastus_soc** and workspace **law-sentinel**.
1. Select **Review & Create** then select **Create**.
1. Wait till the solution is successfully installed.

You have successfully deployed Sentinel to the log analytics workspace and added data. 

### Task 3 - Setup RBAC

You have to secure the access based on least privilege, you´ll create role assignments for the specific role requirements. In your upcoming productive deployment, there´ll be two different roles in the Security Operation Center.
Furthermore, the network team needs access to Cisco umbrella logs. You must ensure that the network team can only access these logs.

#### Permission requirements

| Role | Permissions |
|---|---|
| Security analyst | View data, incidents, worksbooks and other Sentinel resources |
| | Assigning/dismissing incidents. |
| Security engineer | Create and edit workbooks and analytics rules |
| | Install and update solutions from content hub |
| Network Team | Read Permissions for Group: **NOC** on Table: **Cisco_Umbrella_dns_CL**|

---

1. You should still be logged into the Azure portal **https://portal.azure.com**.
1. In the top searchbar, search for **Resoure groups** and select your previously created resource group **rg_eastus_soc**.
1. In the left navigation pane, select **Access control (IAM)**.
1. Select **Add**, from the dropdown select **Add role assignment**.
1. Search for **`Microsoft Sentinel Responder`** and select **View** in the Details column.
1. Review that the permissions match the requirements.
1. Close the window with **X** in the top right corner.
1. Select **Next**.
1. Select **+Select members**.
1. Search for **`SOC Analysts`** Group, select **SOC Analysts** from the search results, press **Select**  and add the role assignment.
1. Select **Review + assign**.
1. You'll repeat the steps for the Sentinel Contributor role. Select **Add**, from the dropdown select **Add role assignment**.
1. Search for **`Microsoft Sentinel Contributor`** and select the role.
1. Select **Next**.
1. Select **+Select members**.
1. On the **Select members** blade, search for the **SOC Engineers** Group.  From the search results select **SOC Engineers** press **Select** to add the role assignment.
1. Select **Review + assign** twice.
1. Select **Role assignments tab**, Confirm that the role assignments are set.
1. Now you'll add a custom role. Select **Add**, from the dropdown select **Add custom role**.
1. Name it, **`NOC-CiscoUmbrellaCL-Read`**.
1. For **Baseline Permission**, select **Start from scratch**.
1. Select **Next**.
1. On the **Permissions** tab, select **Add permissions**.
1. Search for **`Microsoft.OperationalInsights`**, Select the **Azure Log Analytics** card.
1. Add the following permissions.
    - Microsoft.OperationalInsights/workspaces
        - Read : Get Workspace
        - Other : Search Workspace Data

    - Microsoft.OperationalInsights/workspaces/analytics
        - Other : Search

    - Microsoft.OperationalInsights/workspaces/query
        - Read : Query Data in Workspace

    - Microsoft.OperationalInsights/workspaces/tables/query
        - Read : Query workspace table data

1. Select **Review + Create**.
1. Select **Create**, then select **Ok**
1. In the top search bar, search for **`Resource groups`** and select **rg_eastus_soc**.
1. Open the log analytics workspace **law-sentinel**.
1. In the left navigation pane, expand **Settings** and select **Tables**.
1. Search for **`Cisco_Umbrella_dns_CL`**.
1. Click on the ellipses (...), select **Access control (IAM)**.
1. Select **Add** > **Add role assignment**.
1. Search for **`NOC-CiscoUmbrellaCL-Read`** and select the custom role.
1. Select **Next**.
1. Select **Select Members**, search for **NOC**, select it from the search results then press **Select**
1. Select **Review + assign** twice.

You successfully created role based access model for the role requirements for Contoso´s security operations team and created a custom role for the network team and assigned the role on the specific table in your log analytics workspace.

### Task 4 - Create Workbook

In this task, you´ll create a workbook, to get a dashboard with custom views and current incidents and their alerts.

1. You should still be logged into the Azure portal **https://portal.azure.com**.
1. On the Search bar on the top, search for **`Microsoft Sentinel`** and open it.
1. Select **law-sentinel**.
1. In the left navigation pane, expand **Threat management** and select **Workbooks**.
1. Select **Add Workbook**.
1. Select **Edit**.
1. Select the first **Edit** button on the right side.
1. Select **Add** > **Add parameters**.
1. Select **Add parameter** and fill out the following information:
     - **Parameter name:** TimeRange
     - **Parameter type:** Time range picker
1. Check the following settings:
     - **Required?**
1. Select **Save**.
1. In the **TimeRange:** dropdown menu in the lower left, select **Last 7 days**.
1. Select **Add parameter** and fill out the following information:
     - **Parameter name:** AlertSeverity
     - **Parameter type:** Drop down
1. Check the following settings:
     - **Required?**
     - **Allow multiple selections**
     - **Hide parameter in reading mode**
1. Under **Log Analytics workspace Logs Query** paste in:

    ```KQL
    SecurityAlert
    | summarize Count = count() by AlertSeverity
    | order by Count desc, AlertSeverity
    | project Value = AlertSeverity, Label = strcat(AlertSeverity, ' - ', Count)
    ```

1. In the **Time Range** dropdown menu Select **TimeRange**.
1. Scroll down to **Include in the drop down**, check **All** and set **Default selected item** to **All**.
1. Select **Save**.
1. Select **Add parameter** and fill out the following information:
     - **Parameter name:** ProductName
     - **Parameter type:** Drop down
1. Check the following settings:
     - **Required?**
     - **Allow multiple selections**
     - **Hide parameter in reading mode**

1. Under **Log Analytics workspace Logs Query** paste in:

    ```KQL
    SecurityAlert
    | summarize Count = count() by ProductName
    | order by Count desc, ProductName asc
    | project Value = ProductName, Label = strcat(ProductName, ' - ', Count)
    ```

1. In the **Time Range** dropdown menu Select **TimeRange**
1. Scroll down to **Include in the drop down**, check **All** and set **Default selected item** to **All**.
1. Select **Save**.
1. Select **Add** and choose **Add query**.
1. Under **Log Analytics workspace Logs Query** paste in:

    ```KQL
    SecurityIncident
    | where CreatedTime {TimeRange:value}
    | summarize arg_max(TimeGenerated,*) by tostring(IncidentNumber)
    | extend IncidentID = IncidentName
    | extend Alerts = extract("\\[(.*?)\\]", 1, tostring(AlertIds))
    | mv-expand AlertIds to typeof(string)
    | join
    (
        SecurityAlert
        | extend AlertEntities = parse_json(Entities)
        | mv-expand AlertEntities
    ) on $left.AlertIds == $right.SystemAlertId
    | summarize AlertCount=dcount(AlertIds) by IncidentNumber, Status, Severity, Title, Alerts, IncidentUrl, IncidentID
    | project IncidentNumber, IncidentID, Title, Severity, Status, AlertCount, Alerts, IncidentUrl
    | order by Severity
    ```

1. Choose **TimeRange** in the Time Range drop down menu.
You´ll setup dynamic content to get all alerts for the selected incident. Alerts will be exported and available outside this query.
1. Select the **Advanced Settings** tab at the top of the **Editing query** window.
1. Check the following settings:
    - **When items are selected, export parameters** 
1. Select **Add Parameter** and fill in the following information:
    - **Field to export:** Alerts
    - **Parameter name:** Alerts
1. Select **Save**.
1. Go back to the **Settings** tab.
1. Select **Run Query**.
1. Select **Column Settings**.
1. Select **IncidentUrl**.
1. Set Column renderer to **Link**.
1. Under Link Settings set **View to open** to **Url**.
1. Select **Save and Close**.
1. Next, You´ll create the alerts view based on which incident is selected.
1. Select **+ Add** on the bottom of the **Editing query item** window. Select **Add query**.
1. Paste the KQL in the Log Analytics workspace Logs Query

    ```KQL
    SecurityAlert
    | where SystemAlertId in ({Alerts})
    | summarize by  DisplayName, StartTime, EndTime,  SystemAlertId
    | sort by EndTime desc
    ```

1. Choose **TimeRange** in the Time Range drop down.
1. Select **Done Editing**.
1. Select **Done Editing** in the top bar of the **New workbook** window.
1. Select an **Incident**.
1. Alerts to the linked Incident will show up below.
1. Save your query by selecting the Save icon.  
1. In the **Save as** window, enter a title for your new workbook, select the **rg_eastus_soc** resource group from the drop-down, then select **Save as**.

You successfully created a dashboard with custom views for incidents and the associated alerts.
