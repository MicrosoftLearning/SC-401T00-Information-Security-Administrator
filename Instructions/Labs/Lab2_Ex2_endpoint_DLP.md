---
lab:
    title: 'Exercise 2 - Implement and manage endpoint DLP'
    module: 'Module 2 - Implement Data Loss Prevention'
---

# Lab 2 – Exercise 2 – Implement and manage endpoint DLP

Joni Sherman, the newly hired Information Security Administrator at Contoso Ltd., has been asked to strengthen DLP controls on company devices. Some employees have been copying sensitive customer information to USB drives, increasing the risk of data exposure. In this lab, Joni will configure an endpoint DLP policy to block these transfers.

**Tasks**:

1. Onboard a device for endpoint DLP
1. Create an endpoint DLP policy
1. Configure Endpoint DLP settings
1. Configure Microsoft Purview extension

## Task 1 – Onboard a device for endpoint DLP

In this task, you'll onboard a Windows 11 device so it's ready to be protected by endpoint DLP policies.

1. Log into **Client 2 VM (SC-401-CL2)** as the **SC-401-cl2\admin** account.

1. Open Microsoft Edge, and navigate to **`https://purview.microsoft.com`** and log into the Microsoft Purview portal as **Joni Sherman**. Sign in as `JoniS@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Joni's password was set in a previous exercise.

1. Select **Settings** from the left sidebar.

1. On the left sidebar, expand **Device onboarding**, then select **Onboarding**.

1. On the **Onboarding** page, in the **Deployment method** dropdown menu, select **Local Script (for up to 10 machines)** and select **Download package**.

1. In the **Downloads** dialog, hover over the download, then select the folder icon to **Show in folder**.

1. Extract the zip file to the **Desktop** of SC-401-CL2. You should see a script named **DeviceComplianceLocalOnboardingScript.cmd**.

1. On the desktop right click the **DeviceComplianceLocalOnboardingScript.cmd** file you just extracted and select **Show more options**, then select **Properties**.

1. Towards the bottom of the **General** tab of the properties window, in the **Security** section, select **Unblock**, then select **OK** to save this setting.

1. Back on the desktop, right click **DeviceComplianceLocalOnboardingScript.cmd**, then select **Run as administrator**. On the **User Account Control** dialogue, select **Yes**.

1. In the **Command Prompt** screen type **Y** to confirm, and then press Enter.

1. When the script is complete, you'll get a success message and a prompt to **Press any key to continue**. Press any key to close the command line window. It can take a minute to complete the onboarding.

1. Open the start menu and search for `Access work or school`. Select **Access work or school** under **Best match**.

1. In the **Access work or school** window for **Add a work or school account** select **Connect**.

1. In the **Set up a work or school account** dialog, select the **Join this device to Microsoft Entra ID** link and sign in as **Joni Sherman** `JoniS@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Joni's password was set in a previous exercise.

1. In the **Make sure this is your organization** dialog, review the tenant URL and select **Join**.  

1. Once your device has connected select **Done** on the **You're all set!** screen.

1. Restart Client 2 VM (SC-401-CL2).

1. Log back into Client 1 VM (SC-401-CL1).

1. The Microsoft Purview window should still be open at the **Devices** page. Refresh this page and verify the device has been successfully onboarded.

You've successfully onboarded the device and joined it to Microsoft Entra ID. It can now be protected by endpoint DLP policies.

## Task 2 – Create an endpoint DLP policy

In this task, you'll create a DLP policy that blocks the transfer of sensitive information to USB drives. This helps reduce the risk of data being taken offsite without authorization.

1. Sign in to Client 1 VM (SC-401-CL1) as the SC-401-cl1\admin account.

1. You should still be at the **Devices** page in the Microsoft Purview portal, logged in as Joni Sherman.

1. In the Microsoft Purview portal, select **Solutions** > **Data Loss Prevention**.

1. From the left, navigation pane, select **Policies** then select **+ Create policy**.

1. On the **Choose what type of data to protect** page, select **Data stored in connected sources**, then select **Next**.

1. On the **Start with a template or create a custom policy** page, select **Custom** and **Custom policy**, then select **Next**.

1. On the **Name your DLP policy** page, enter:

    - **Name**: `Block USB transfers`
    - **Description**: `Prevent transferring sensitive data to USB devices.`

1. On the **Assign admin units** page, select **Next**.

1. On the **Choose locations to apply the policy** page, ensure only the **Devices** location is selected. If any other location is selected, ensure they're deselected, then select **Next**.

1. On the **Define policy settings** page, select **Create or customize advanced DLP rules** then select **Next**.

1. On the **Customize advanced DLP rules** page, select **+ Create rule**.

1. On the **Create rule** page, enter:

    - **Name**: `USB transfer rule`
    - **Description**: `Block USB transfers of sensitive data.`

1. Under **Conditions** select **+ Add condition** then select **Content contains**.

1. In the new **Content contains** section:
    - Select **Add** > **Sensitive info types**.
    - On the **Sensitive info types** page, search for these sensitive info types:
       - `Credit Card Number`
       - `U.S. Social Security Number (SSN)`
       - `U.S. Driver's License Number`
       - `Contoso Employee IDs`

1. Under **Actions**, select **+ Add an action** > **Audit or restrict activities on devices**.

1. In the new **Audit or restrict activities on devices** section:
    - In the **File activities for all apps** section, ensure **Copy to a removable USB device** is selected.
    - Select the dropdown to the left of **Copy to a removable USB device** to change the action from **Audit only** to **Block**.

1. Under **User notifications**:
    - Turn **On** the toggle for **Use notifications to inform your users and help educate them on the proper use of sensitive info.**.
    - Select the checkbox to **Show users a policy tip notification when an activity is restricted**.

1. Select **Save** at the bottom of the **Create rule** flyout.

1. Back on the **Customize advanced DLP rules**, select **Next**.

1. On the **Policy mode** page select **Run the policy in simulation mode**.
   - Select the checkbox to **Show policy tips while in simulation mode**.
   - Also, select the checkbox to **Turn the policy on if it's not edited within fifteen days of simulation**.

1. Select **Next**.

1. On the **Review and finish** page, review your policy settings then select **Submit** to create the policy.

1. Once the policy is created select **Done** on the **New policy created** page.

You've successfully created a DLP policy in simulation mode that blocks USB transfers of sensitive data. If the policy is not edited, it will automatically be turned on after 15 days.

## Task 3 – Configure endpoint DLP settings

In this task, you'll fine-tune endpoint DLP settings by excluding a local folder, setting browser restrictions, and blocking a cloud domain.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.

1. In Microsoft Purview, from the left navigation pane, select **Settings** > **Data Loss Prevention**.

1. The **Data Loss Prevention settings** page should open to the **Endpoint DLP settings**.

1. On the **Endpoint DLP settings** page, expand **File path exclusions for Windows**  then select **+ Add file path exclusion**.

1. On the **Exclude these file paths from Windows devices** flyout page in the **File path exclusion** field, enter `C:\FilePathExclusionTest` then select the **+** button to the right. Select **Save** to save this entry.

1. Back on the **Endpoint DLP settings** page, expand **Browser and domain restrictions to sensitive data** and select **+ Add or edit unallowed browsers**.

1. On the **Add unallowed browsers** flyout page select the checkbox for **Google Chrome** and select **Save**.

1. Back on the **Endpoint DLP settings** page, select the dropdown for **Service domains** and change it from **Off** to **Block**.

1. In the **Update cloud app mode** dialogue select **Yes** to activate the block mode.

1. Under **Service domains** select **+ Add cloud service domain**.

1. On the **Add cloud service domain** flyout page in the **Domain** field enter `dropbox.com` then select the **+** (plus) icon to add the path. Select **Save** to save this setting.

You've applied custom endpoint DLP settings that refine the behavior of your policy, including exclusions, browser restrictions, and blocking access to specific domains.

## Task 4 – Configure Microsoft Purview extension

In this task, you'll install the Microsoft Purview Extension in Google Chrome to test endpoint DLP policy behavior in supported browsers.

1. Open the Edge browser from the task bar.

1. Navigate to the Google Chrome download at **`https://chrome.google.com`**.

1. Select **Download Chrome** and select **Open file** from the **Downloads** notification for **ChromeSetup.exe**.

1. Select **Yes** in the **User Account Control** dialog to install the Chrome browser.

1. When the installation is finished, on the **Sign in to Chrome** screen, select **No thanks** or **Don't sign in**.

1. Select **Skip** on the **Set your default browser** page.

1. When the newly installed Chrome browser window opens, navigate to the **Microsoft Purview Extension** in the **Chrome web store** at:

   `https://chrome.google.com/webstore/detail/microsoft-purview-extensi/echcggldkblhodogklpincgchnpgcdco`

1. Confirm you're on the correct extension page, then select **Add to Chrome**.

1. On the **Add "Microsoft Purview Extension"?** window, select **Add extension**.

1. Close the notification for the extension being added to Chrome, then navigate to **`chrome://extensions`**.

1. Validate the **Microsoft Purview Extension** is visible and activated.

1. Close the Chrome browser window.

You've successfully installed Chrome and added the Microsoft Purview Extension. The device now supports DLP policy enforcement in both Edge and Chrome.
