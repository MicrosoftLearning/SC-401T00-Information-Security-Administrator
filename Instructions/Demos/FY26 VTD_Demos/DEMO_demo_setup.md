# Lab setup - Prepare your environment for demos

**This setup is not part of any demo.**

Complete all steps in this lab **24 hours** before recording or delivering Virtual Training Day demos. These tasks prepare the tenant so demos run as expected and don't rely on background configuration being performed live.

Nothing in this lab should be shown, narrated, or completed during a demo.

## What you're preparing

Before recording demos, configure core services required across multiple scenarios. This ensures demos don't stall due to missing prerequisites or disabled features.

During this setup, you'll:

- Enable required services used by multiple demos
- Ensure activity data is available where needed
- Reduce the risk of unexpected prompts or empty views during recording

**Tasks:**

1. Enable Audit in the Microsoft Purview portal
1. Enable support for sensitivity labels
1. Enable insider risk analytics
1. Enable device onboarding
1. Onboard a device for endpoint DLP

## Task 1 - Enable Audit in the Microsoft Purview portal

Enable Audit so activity data is available during demos that rely on logging and investigation features. This step should be completed ahead of time and shouldn't be demonstrated live.

1. Log into Client 1 VM (SC-401-CL1) with the **Admin** account.

1. Open Microsoft Edge.

1. In **Microsoft Edge**, navigate to `https://purview.microsoft.com` and sign in as **MOD Administrator**, `admin@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant prefix provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.

1. A message about the new Microsoft Purview portal will appear on the screen. Select **Get started** to access the new portal.

    ![Screenshot showing the Welcome to the new Microsoft Purview portal screen.](../Media/welcome-purview-portal.png)

1. Select **Solutions** from the left sidebar, then select **Audit**.

1. On the **Search** page, select the **Start recording user and admin activity** bar to enable audit logging.

    ![Screenshot showing the Start recording user and admin activity button.](../Media/enable-audit-button.png)

1. Once you select this option, the blue bar should disappear from this page.

    >[!Note] **Note: If the Audit button doesn't enable logging**
    >
    >Use this method only if Audit can't be enabled through the portal. Don't perform this during a demo.
    >
    >If this happens, you can enable Audit through PowerShell instead:
    >
    >1. Open an elevated Terminal window by right-clicking the Windows button and selecting **Terminal (Admin)**.  
    >
    >1. Install the latest **Exchange Online PowerShell** module:
    >
    >     ```powershell
    >     Install-Module ExchangeOnlineManagement
    >     ```
    >
    >     Confirm any prompts by typing **Y** for Yes and pressing **Enter**.
    >
    >1. Run the following command to change your execution policy:
    >
    >     ```powershell
    >     Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    >     ```
    >
    >1. Close the elevated Terminal window and open a regular PowerShell session.
    >
    >1. Connect to Exchange Online:
    >
    >     ```powershell
    >     Connect-ExchangeOnline
    >     ```
    >
    >    Sign in as `admin@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant prefix provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.
    >
    >1. Check if Audit is enabled:
    >
    >     ```powershell
    >     Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    >     ```
    >
    >    If it returns **_False_**, enable Audit:
    >
    >     ```powershell
    >     Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    >     ```
    >
    >1. Verify that it's now enabled:
    >
    >     ```powershell
    >     Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    >     ```
    >
    >    The command should return **_True_** once Audit is active.

You have successfully enabled auditing in Microsoft 365.

## Task 2 – Enable support for sensitivity labels

In this task, you'll enable co-authoring for sensitivity labels, which also enables sensitivity labels for files in SharePoint and OneDrive.

1. In the Microsoft Purview portal, on the left navigation pane, select **Settings** > **Information Protection**.

1. On the **Information Protection settings** page, ensure you're on the **Co-authoring for files with sensitivity labels** tab.

1. Select the checkbox for **Turn on co-authoring for files with sensitivity labels**.

1. Select **Apply** at the bottom of the screen.

You have successfully enabled support for sensitivity labels for files in SharePoint and OneDrive.

## Task 3 – Enable insider risk analytics

In this task, you'll enable analytics and data sharing for Insider Risk Management.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account and logged in as the MOD Administrator in Microsoft Purview.

1. In Microsoft Purview, navigate to **Settings** > **Insider Risk Management** > **Analytics**.

1. Toggle these settings to **On**:

   - **Show insights at tenant level**

   - **Show insights at user level**

1. Select **Save** at the bottom of the page.

You have enabled analytics for Insider Risk Management.

## Task 4 – Enable device onboarding

In this task, you'll enable device onboarding for your organization.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account and logged in as the MOD Administrator in Microsoft Purview.

1. Select **Settings** from the left sidebar, then expand **Device onboarding**.

1. On the **Device onboarding** page, select **Devices**.

1. On the **Devices** page, select **Turn on device onboarding** then select **Ok** to confirm.

1. When prompted, select **OK** to confirm that device onboarding is being turned on.

You have now enabled device onboarding and can start to onboard devices to be protected with Endpoint DLP policies. The process of enabling the feature might take up to 30 minutes.

## Task 5 – Onboard a device for endpoint DLP

Insider Risk Management demos that use the risky browser usage template require at least one onboarded device to generate and surface related activity. Complete this task ahead of time so these scenarios work as expected during demos.

1. Select **Settings** from the left sidebar.

1. On the left sidebar, expand **Device onboarding**, then select **Onboarding**.

1. On the **Onboarding** page, in the **Deployment method** dropdown menu, select **Local Script (for up to 10 machines)**, then select **Download package**.

1. In the **Downloads** dialog, hover over the download, then select the folder icon to **Show in folder**.

1. Extract the zip file to the **Desktop** of SC-401-CL1. You should see a script named **DeviceComplianceLocalOnboardingScript.cmd**.

1. On the desktop right click the **DeviceComplianceLocalOnboardingScript.cmd** file you just extracted and select **Show more options**, then select **Properties**.

1. Towards the bottom of the **General** tab of the properties window, in the **Security** section, select **Unblock**, then select **OK** to save this setting.

1. Back on the desktop, right click **DeviceComplianceLocalOnboardingScript.cmd**, then select **Run as administrator**. On the **User Account Control** dialogue, select **Yes**.

1. In the **Command Prompt** screen, type **Y** to confirm, then press Enter.

1. When the script is complete, you'll get a success message and a prompt to **Press any key to continue**. Press any key to close the command line window. It can take a minute to complete the onboarding.

1. Open the start menu and search for `Access work or school`. Select **Access work or school** under **Best match**.

1. In the **Access work or school** window for **Add a work or school account** select **Connect**.

1. In the **Set up a work or school account** dialog, select the **Join this device to Microsoft Entra ID** link and sign in as **MOD Administrator** `admin@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant prefix provided by your lab hosting provider). User account passwords are provided by your lab hosting provider.

1. In the **Make sure this is your organization** dialog, review the tenant URL and select **Join**.  

1. Once your device has connected select **Done** on the **You're all set!** screen.

1. Restart Client 1 VM (SC-401-CL1).

You've successfully onboarded the device and joined it to Microsoft Entra ID. It can now be protected by endpoint DLP policies.
