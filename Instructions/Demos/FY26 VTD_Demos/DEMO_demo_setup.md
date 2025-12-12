---
lab:
    title: 'Lab setup - Prepare your environment for demos'
    module: 'Lab setup'
---

# Lab setup - Prepare your environment for demos

**This setup is not part of any demo.**

Complete all steps in this lab before recording or delivering Virtual Training Day demos. These tasks prepare the tenant so demos run as expected and don't rely on background configuration being performed live.

Nothing in this lab should be shown, narrated, or completed during a demo.

## What you're preparing

Before recording demos, configure core services required across multiple scenarios. This ensures demos don't stall due to missing prerequisites or disabled features.

During this setup, you'll:

- Enable required services used by multiple demos
- Ensure activity data is available where needed
- Reduce the risk of unexpected prompts or empty views during recording

**Tasks:**

1. Enable Audit in the Microsoft Purview portal  

## Task 1 - Enable Audit in the Microsoft Purview portal

Enable Audit so activity data is available during demos that rely on logging and investigation features. This step should be completed ahead of time and shouldn't be demonstrated live.

1. Log into Client 1 VM (SC-401-CL1) with the **Admin** account.

1. Open Microsoft Edge.

1. In **Microsoft Edge**, navigate to `https://purview.microsoft.com` and sign in as **MOD Administrator**, `admin@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant prefix provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.

1. In Microsoft Edge, navigate to the Microsoft Purview portal, `https://purview.microsoft.com`, and log in.

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
