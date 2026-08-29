---
lab:
  title: Exercise 1 - Implement and manage DLP policies
  module: Module 2 - Implement Data Loss Prevention
  description: Create, test, and manage DLP policies in Microsoft Purview, including policy templates, simulation mode, and PowerShell configuration.
  duration: 75 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft 365
    - Microsoft Purview
---

## WWL Tenants - Terms of use

If you are provided with a tenant as part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training.

Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and is not eligible for extension.

Tenants must not be converted to a paid subscription. Tenants obtained as part of this course remain the property of Microsoft Corporation, and we reserve the right to obtain access and repossess them at any time.

# Lab 2 – Exercise 1 – Implement and manage DLP policies

Joni Sherman, the newly hired Information Security Administrator at Contoso Ltd., has been asked to configure data loss prevention (DLP) policies to help protect sensitive customer data across Microsoft 365. In this lab, you'll use Microsoft Purview to create and manage DLP policies from templates, customize policy rules, test policies in simulation mode, and configure DLP by using PowerShell.

**Tasks**:

1. Create a DLP policy from a template
1. Create a custom DLP policy in simulation mode
1. Modify a DLP policy
1. Create a DLP policy in PowerShell
1. Activate a policy in simulation mode
1. Modify policy priority

**Estimated time:** 60-75 minutes

## Task 1 – Create a DLP policy from a template

In this task, you'll create a DLP policy from a template to help protect personal data stored in SharePoint and OneDrive. Starting from a template gives you a baseline policy with preconfigured rules that you can review and adjust before enforcement.

1. Log into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account.

1. In **Microsoft Edge**, navigate to **`https://purview.microsoft.com`** and log into the Microsoft Purview portal as **Joni Sherman**. Sign in as `JoniS@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant prefix provided by your lab hosting provider). User account passwords are provided by your lab hosting provider.

1. Select **Solutions** > **Data Loss Prevention** > **Policies**.

1. On the **Policies** page, select **+ Create policy**.

1. On the **What info do you want to protect?** page, select **Enterprise applications & devices**.

1. On the **Start with a template or create a custom policy** page, select **Privacy** under **Categories**, then select **GDPR Enhanced** under **Regulations**.

1. Select **Next**.

1. On the **Name your DLP policy** page, keep the default name and description, then select **Next**.

1. On the **Assign admin units** page, select **Next**.

1. On the **Choose where to apply the policy** page, select the locations for **SharePoint sites** and **OneDrive accounts** only. If any other locations are selected, deselect them.

1. Select **Next**.

1. On the **Policy mode** page, select **Run the policy in simulation mode**.

1. Select the checkboxes for **Show policy tips while in simulation mode** and **Turn the policy on if it's not edited within fifteen days of simulation**.

1. Select **Next**.

1. On the **Review and finish** page, review your settings, then select **Submit**.

1. On the **New policy created** page, select **Done**.

You've created a DLP policy from a template that scans SharePoint and OneDrive content for personal data. The policy runs in simulation mode so you can review matches and user experience before enforcement.

## Task 2 – Create a custom DLP policy in simulation mode

In this task, you'll create a DLP policy in simulation mode that targets credit card numbers in Teams messages. The policy will notify users when they attempt to share sensitive content and allow them to override with justification.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account, and you should be logged into Microsoft Purview as **Joni Sherman**.

1. Select **Solutions** > **Data Loss Prevention** > **Policies**.

1. On the **Policies** page, select **+ Create policy**.

1. On the **What info do you want to protect?** page, select **Enterprise applications & devices**.

1. On the **Start with a template or create a custom policy** page, select **Custom** as the category, then select **Custom policy** under **Regulations**.

1. Select **Next**.

1. On the **Name your DLP policy** page enter:

   - **Name**: `DLP - Credit Card Protection`
   - **Description**: `Detect and restrict sharing of credit card numbers in Teams messages.`

1. Select **Next**.

1. On the **Assign admin units** page, select **Next**.

1. On the **Choose where to apply the policy** page, enable the location for **Teams chat and channel messages** only. If any other locations are selected, deselect them.

1. Select **Next**.

1. On the **Define policy settings** page, select **Create or customize advanced DLP rules**, then select **Next**.

1. On the **Customize advanced DLP rules** page, select **+ Create rule**.

1. In the **Create rule** flyout:
    - In the **Name** field, enter `Credit card information`.

1. Under **Conditions**, select **+ Add condition** > **Content is shared from Microsoft 365**.

1. In the **Content is shared from Microsoft 365** section:
    - Select the option for **with people outside my organization**.

1. Select **+ Add condition** > **Content contains**.

1. In the new **Content contains** section:
    - Select **Add** > **Sensitive info types**.
    - On the **Sensitive info types** page, search for and select `Credit Card Number`, then select **Add**.

1. Under **Actions**, select **+ Add an action** > **Restrict access or encrypt the content in Microsoft 365 locations**.

1. In the **Restrict access or encrypt the content** section:
    - Select **Block only people outside your organization**.

1. Under **User notifications**:
    - Turn on the toggle for **Use notifications to inform your users and help educate them on the proper use of sensitive info.**.
    - Select the checkbox for **Notify users in Office 365 service with a policy tip**.

1. Under **User overrides**:
    - Select the checkbox for **Allow users to override policy restrictions in Fabric (including Power BI), Exchange, SharePoint, OneDrive, and Teams.**
    - Select the checkbox for **Require a business justification to override**.

1. Under **Incident reports**, in the **Use this severity level in admin alerts and reports** dropdown:
    - Select **Low**.

1. At the bottom of the **Create rule** flyout, select **Save**.

1. Back on the **Customize advanced DLP rules**, select **Next**.

1. On the **Policy mode** page, select **Run the policy in simulation mode** and select the checkbox for **Show policy tips while in simulation mode**.

1. Select **Next**.

1. On the **Review and finish** page, review your settings then select **Submit**.

1. On the **New policy created** page, select **Done**.

You've created a DLP policy that scans Teams content for credit card numbers and allows overrides with business justification.

## Task 3 – Modify a DLP policy

In this task, you'll expand the scope of your existing DLP policy to include Exchange email. This helps ensure consistent protection across additional communication channels.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.

1. You should still be on the **Policies** page in Microsoft Purview. If not, open **Microsoft Edge** and navigate to **`https://purview.microsoft.com`**. Select **Solutions** > **Data Loss Prevention** > **Policies**.

1. On the **Policies** page, select the checkbox for the recently created **DLP - Credit Card Protection**, then select **Edit policy** to open the policy configuration.

1. On the **Name your DLP policy** page, edit the description to `Detect and restrict sharing of credit card numbers in Teams and Exchange messages.`

1. Select **Next**.

1. On the **Assign admin units** page, select **Next**.

1. On the **Choose where to apply the policy** page, select the checkbox for **Exchange email** to add this location to your DLP policy.

1. Select **Next** until you reach the **Review and finish** page.

1. Select **Submit** on the **Review and finish** page to apply the change you made to the policy.

1. Once the policy is updated, select **Done** on the **Policy updated** page.

You've successfully updated the policy to scan email along with Teams messages.

## Task 4 – Create a DLP policy in PowerShell

In this task, you'll create a DLP policy using PowerShell to block sharing of employee IDs via email. This approach demonstrates how to define and enforce policy settings through scripting.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account.

1. Open an elevated PowerShell window by right-clicking the **Start** button in the task bar, then select **Terminal (Admin)**.

1. Run the **Install Module** cmdlet in the terminal window to install the latest **Exchange Online PowerShell** module version:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```

1. Confirm the Untrusted repository security dialog with **Y** for Yes and press **Enter**.  This process might take some time to complete.

1. Run the **Connect-IPPSSession** cmdlet to connect to the Security & Compliance PowerShell:

    ```powershell
    Connect-IPPSSession
    ```

1. Sign in as **Joni Sherman** `JoniS@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant prefix provided by your lab hosting provider) in the **Sign in to your account** pop-up window. User account passwords are provided by your lab hosting provider.

1. Run the **New-DlpCompliancePolicy** cmdlet to create a DLP policy that scans all Exchange mailboxes:

    ```powershell
    New-DlpCompliancePolicy -Name "EmployeeID DLP Policy" -Comment "This policy blocks sharing of Employee IDs" -ExchangeLocation All
    ```

1. Run the **New-DlpComplianceRule** cmdlet to add a DLP rule to the DLP policy you created in the previous step. This policy uses the **Contoso Employee IDs** sensitive info type created in a previous exercise:

    ```powershell
    New-DlpComplianceRule -Name "EmployeeID DLP rule" -Policy "EmployeeID DLP Policy" -BlockAccess $true -ContentContainsSensitiveInformation @{Name="Contoso Employee IDs"}
    ```

1. Run the **Get-DLPComplianceRule** cmdlet to review the **EmployeeID DLP rule**:

    ```powershell
    Get-DLPComplianceRule -Identity "EmployeeID DLP rule"
    ```

You've successfully used PowerShell to create a DLP policy that blocks the sharing of employee IDs.

## Task 5 – Activate a policy in simulation mode

Now that your DLP policy has been tested in simulation, you'll activate it to begin enforcing its actions.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.

1. In **Microsoft Edge**, navigate to DLP policies by going to **`https://purview.microsoft.com`** > **Solutions** > **Data Loss Prevention** then select **Policies** from the left sidebar.

1. On the **Policies** page, select the **DLP - Credit Card Protection** policy.

1. At the bottom of the flyout on the right, select **View simulation**.

1. On the simulation page, take a moment to explore:

   - The **Simulation overview** tab, which shows scanning progress, total matches, and scanning status by location.
   - The **Items for review** tab, where any predicted matches will appear once available.
   - The **Alerts** tab, where any alerts triggered in simulation mode would be listed.

1. After exploring the insights in simulation mode, select **Turn the policy on**, then **Confirm** to activate the DLP policy.

   A confirmation flyout will appear indicating that the policy has been published successfully.

The policy is now active and enforcing restrictions on credit card information in Teams and Exchange.

## Task 6 – Modify policy priority

When multiple policies exist, their priority determines which one applies first. In this task, you'll move the employee ID policy to the highest priority.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.

1. In **Microsoft Edge**, the Microsoft Purview portal tab should still be open to the **Policies** page. If not, open **Microsoft Edge** and navigate to **`https://purview.microsoft.com`**. Select **Solutions** > **Data Loss Prevention** > **Policies**.

1. On the **Policies** page, select the **EmployeeID DLP Policy**.

1. Select **Reprioritize** from the top navigation ribbon, then select **Move to top (highest priority)**.

1. In the **Data loss prevention** window, select **Refresh** and review the priority in the **Order** column of the policy table.

You've updated policy priority so that the employee ID policy takes precedence over others.
