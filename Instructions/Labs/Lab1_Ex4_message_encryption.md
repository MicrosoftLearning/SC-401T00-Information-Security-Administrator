---
lab:
    title: 'Exercise 4 - Deploy Microsoft Purview Message Encryption'
    module: 'Module 1 - Implement Information Protection'
---
<!--

=======
This lab is broken by Exchange provisioning issues on the tenant
=======

# Lab 1 - Exercise 4 - Deploy Microsoft Purview Message Encryption

Joni Sherman, the Information Security Administrator for Contoso Ltd., has been tasked with ensuring secure communication between departments. To support this, she is configuring Microsoft Purview Message Encryption for Contoso, including modifying the default settings and creating a custom branding experience for the finance department.

**Tasks**:

1. Verify Azure RMS functionality
1. Modify default branding template
1. Validate default branding behavior
1. Create custom branding template
1. Validate custom branding behavior

## Task 1 – Verify Azure RMS functionality

In this task, you'll verify the correct Azure RMS functionality of your tenant.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account.

1. Open PowerShell by right-clicking the Start button in the taskbar and selecting **Terminal (Admin)**.

1. Run the **Install Module** cmdlet in the terminal window to install the latest **Exchange Online PowerShell** module version:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```

1. Confirm the Untrusted repository security dialog with **Y** for Yes and press **Enter**.  This process may take some time to complete.

1. Run the **Connect-ExchangeOnline** cmdlet to use the Exchange Online PowerShell module and connect to your tenant:

    ```powershell
    Connect-ExchangeOnline
    ```

1. When the **Sign in** window is displayed, sign in as `JoniS@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). You will use the password you reset Joni's to in a previous lab.

1. Run the **Get-IRMConfiguration** cmdlet to verify Azure RMS and IRM is activated in your tenant:

    ```powershell
    Get-IRMConfiguration | fl AzureRMSLicensingEnabled
    ```

   The **AzureRMSLicensingEnabled** result should be **True**.

1. Run the **Test-IRMConfiguration** cmdlet to test Azure RMS functionality using Office 365 Message Encryption with **Megan Bowen** as both sender and recipient:

    ```powershell
    Test-IRMConfiguration -Sender MeganB@contoso.com -Recipient MeganB@contoso.com
    ```

    ![IRM validation script result. ](../Media/irm-validation.png)

    Verify all tests are in the status PASS and no errors are shown.

1. Leave the PowerShell window open.

You have successfully installed the Exchange Online PowerShell module, connected to your tenant, and verified the correct functionality of Azure RMS.

## Task 2 – Modify default branding template

There is a requirement in your organization to restrict trust for foreign identity providers, such as Google or Facebook. Because these social IDs are activated by default for accessing messages protected with message encryption, you need to deactivate the use of social IDs for all users in your organization.

1. You should still be logged into your Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account and there should still be an open PowerShell window with Exchange Online connected.

1. Run the **Get-OMEConfiguration** cmdlet to view the default configuration:

    ```powershell
    Get-OMEConfiguration -Identity "OME Configuration" | fl
    ```

   Review the settings and confirm that the SocialIdSignIn property is set to **True**.

    ![Screenshot showing the SocialIdSignIn value set to True. ](../Media/socialidsignin-value-true.png)

1. Run the **Set-OMEConfiguration** cmdlet to restrict the use of social IDs for accessing messages from your tenant protected with OME:

    ```powershell
    Set-OMEConfiguration -Identity "OME Configuration" -SocialIdSignIn:$false
    ```

1. Confirm the warning message for customizing the default template by entering **Y** for Yes then press **Enter**.

1. Run the **Get-OMEConfiguration** cmdlet to check the default configuration again and validate:

    ```powershell
    Get-OMEConfiguration -Identity "OME Configuration" | fl
    ```

    ![Screenshot showing the SocialIdSignIn value set to False. ](../Media/socialidsignin-value-false.png)

   Notice the result should show the SocialIdSignIn is set to **False**. Leave the PowerShell window and client open.

You've successfully disabled social identity providers, helping ensure that encrypted emails from Contoso can only be opened using Microsoft accounts or one-time passcodes—improving control over sensitive message access.

## Task 3 – Validate default branding behavior

You must confirm that no social IDs dialog is displayed for external recipients when receiving a message protected with Office 365 Message Encryption from users of your tenant and they need to use the OTP at any time accessing the encrypted content.

> [!alert] External email delivery might be blocked in some lab environments. This task might not complete as expected.

1. You should still be logged into your Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin**.

1. Open **Microsoft Edge** in an InPrivate window by right clicking Microsoft Edge from the task bar and selecting **New InPrivate window**.

1. Navigate to **`https://outlook.office.com`** and log into Outlook on the web as `LynneR@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Lynne's password was set in a previous exercise.

1. On the **Stay signed in?** dialog box, select the checkbox for **Don't show this again** then select **No**.

1. In Outlook on the web, select **New mail**.

1. In the **To** line enter your personal or other third-party email address that isn't in the tenant domain. Enter **`Secret Message`** in the subject line and **`My super-secret message.`** in the body of the email.

1. From the top pane, select **Options** then **Encrypt** to encrypt the message. Once you've successfully encrypted the message, you should see a notice that says "Encrypt: This message is encrypted. Recipients can't remove encryption."

      ![Screenshot of Encryption settings](../Media/OptionsEncrypt.png)

1. Select **Send** to send the message. Leave the Outlook window open.

1. Sign into your personal email account in a new window and open the message from Lynne Robbins. If you sent this email to a Microsoft account (like @outlook.com) the encryption might be processed automatically, and you'll see the message automatically. If you sent the email to another email service like (@gmail.com), you might have to perform the next steps to process the encryption and read the message.

    > [!Note] **Note**: You might need to check your junk or spam folder for the message from Lynne Robbins.

1. Select **Read the message**.

1. Because social IDs are disabled, you shouldn't see an option to sign in with a third-party account.

1. Select **Sign in with a One-time passcode** to receive a limited time passcode.

1. Go to your personal email portal and open the message with subject **Your one-time passcode to view the message**.

1. Copy the passcode, paste it into the'portal and select **Continue**.

1. Review the encrypted message.

You have successfully tested the modified default'template with deactivated social IDs.

## Task 4 – Create custom branding template

Protected messages sent by your organizations finance department require special branding, including customized introduction and body texts and a Disclaimer link in the footer. The finance messages shall also expire after seven days. In this task, you will create a new custom'configuration and create a transport rule to apply the'configuration to all mail sent from the finance department.

1. You should still be logged into your Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin**, and there should still be an open PowerShell window with Exchange Online connected.

1. Run the **New-OMEConfiguration** cmdlet to create a new configuration:

    ```powershell
    New-OMEConfiguration -Identity "Finance Department" -ExternalMailExpiryInDays 7
    ```

1. Confirm the warning message for customizing the template with **Y** for Yes and press **Enter**.

1. Run the **Set-OMEConfiguration** cmdlet with the _IntroductionText_ parameter to change the introduction text:

    ```powershell
    Set-OMEConfiguration -Identity "Finance Department" -IntroductionText " from Contoso Ltd. finance department has sent you a secure message."
    ```

1. Confirm the warning message for customizing the template with **Y** for Yes and press **Enter**.

1. Run the **Set-OMEConfiguration** cmdlet with the _EmailText_ parameter to update the body text of the encrypted email:

    ```powershell
    Set-OMEConfiguration -Identity "Finance Department" -EmailText "Encrypted message sent from Contoso Ltd. finance department. Handle the content responsibly."
    ```

1. Confirm the warning message for customizing the template with **Y** for Yes and press **Enter**.

1. Run the **Set-OMEConfiguration** cmdlet with the _PrivacyStatementURL_ parameter to change the disclaimer URL to point to Contoso's privacy statement site:

    ```powershell
    Set-OMEConfiguration -Identity "Finance Department" -PrivacyStatementURL "https://contoso.com/privacystatement.html"
    ```

1. Confirm the warning message for customizing the template with **Y** for Yes and press **Enter**.

1. Run the **New-TransportRule** cmdlet to create a mail flow rule, which applies the custom'template to all messages sent from the finance team. This process might take a few seconds to complete.

    ```powershell
    New-TransportRule -Name "Encrypt all mails from Finance team" -FromScope InOrganization -FromMemberOf "Finance Team" -ApplyRightsProtectionCustomizationTemplate "Finance Department" -ApplyRightsProtectionTemplate Encrypt
    ```

1. Run the **Get-OMEConfiguration** cmdlet to verify changes.

    ```powershell
    Get-OMEConfiguration -Identity "Finance Department" | Format-List
    ```

1. Close the PowerShell window after reviewing the results

You've configured a transport rule that ensures emails from the finance department are encrypted and branded consistently, reinforcing Contoso's messaging and security standards.

## Task 5 – Validate custom branding behavior

To validate the new custom configuration, you need to use the account of Lynne Robbins again, who is a member of the finance team.

> [!alert] External email restrictions might prevent this message from being received. Branding might not appear as expected.

1. Go back to **Microsoft Edge**  with the InPrivate Outlook on the web window where you should still be logged in as **Lynne Robbins**.

1. Select **New mail** from the upper left side part of Outlook on the web.

1. In the **To** line enter your personal or other third-party email address that isn't in the tenant domain. Enter **`Finance Report`** in the subject line and enter **`Secret finance information.`** in the body of the email.

1. Select **Send** to send the message, then close the InPrivate window where you're logged in as Lynne.

1. Sign into your personal email account and open the message from Lynne Robbins.

1. You should see a message from Lynne Robbins that looks like the image below.  Select **Read the message**.

    ![Sample encrypted email from Lynne Robbins. ](../Media/EncryptedEmail.png)

1. In the customized configuration, both authentication options are available, indicating that social ID sign-in is enabled. Select **Sign in with a One-time passcode** to receive a limited time passcode.

1. Go to your personal email portal and open the message with subject **Your one-time passcode to view the message**.

1. Copy the passcode, paste it into the portal and select **Continue**.

1. Review the encrypted message with custom branding. Close the window with your email account open.

You have successfully tested the new customized template.

-->

# Lab 1 - Exercise 4 - Deploy Microsoft Purview Message Encryption

Joni Sherman, an Information Security Administrator at Contoso Ltd., is implementing secure email communication to protect sensitive information exchanged between departments. As part of this effort, she'll configure Microsoft Purview Message Encryption (OME) by using the Exchange admin center to automatically encrypt messages sent from the Finance department and include a clear notice that the message was sent securely.

**Tasks**:

1. Create a mail flow rule to encrypt messages from the Finance department
1. Add a disclaimer to encrypted messages
1. Enable the mail flow rule  
1. Validate message encryption

## Task 1 – Create a mail flow rule to encrypt messages from the Finance department

In this task, you'll use the Exchange admin center to create a mail flow rule that applies Microsoft Purview Message Encryption to all messages sent by members of the Finance Team group.

1. In **Microsoft Edge**, go to `https://admin.exchange.microsoft.com` and sign in as JoniS@WWLxZZZZZZ.onmicrosoft.com (replace ZZZZZZ with your unique tenant ID).

1. In the left navigation pane, expand **Mail flow**, then select **Rules**.

1. On the **Rules** page, select **+ Add a rule** > **Apply Office 365 Message Encryption and rights protection to messages**.

1. On the **Set rule conditions** page, configure:

   - **Name:** `Encrypt messages from Finance department`

   - In the **Apply this rule if** section, configure:

      - For dropdown 1: **The sender**

      - For dropdown 2: **is a member of this group**, then select **Finance team** and **Save** in the **Select members** flyout.

   - In the **Do the following** section:

     - Leave the default **Modify the message security** and **Apply Office 365 Message Encryption and rights protection** selected

     - Select the **Select one** link under the **Do the following** section.

       ![Screenshot showing where to select Select one in the Exchange Admin Center.](../Media/rights-protect-message-options.png)

     - In the **Select RMS template** flyout, select **Encrypt**, then select **Save**.

     - Select **Next** back on the **Set rule conditions** page.

1. On the **Set rule settings** page, leave the default selected, then select **Next**.

1. On the **Review and finish** page, review your mail flow rule, then select **Finish**.

1. Select **Done** once your mail flow rule has been created.

You've successfully created a mail flow rule that encrypts messages sent from the Finance department using Microsoft Purview Message Encryption. This ensures that sensitive financial communications are protected before leaving the organization.

## Task 2 – Add a disclaimer to encrypted messages

Next, you'll modify the existing encryption rule to append a disclaimer. This disclaimer acts as a simple form of message branding, notifying recipients that the message was sent securely by Contoso Ltd.

1. On the **Rules** page, select the newly created **Encrypt messages from Finance department**.

1. In the **Encrypt messages from Finance department** flyout, select **Edit rule conditions**.

1. Select the **+** to the right of the **Do the following** section to add another action.

   ![Screenshot showing where the plus (+) is to add another mail flow action.](../Media/add-mail-flow-condition.png)

1. In the newly created **And** section:

   - For dropdown 1: **Apply a disclaimer to the message**

   - For dropdown 2: **append a disclaimer**.

   - Under the dropdowns, select **Enter text**, then enter `This email has been encrypted and sent securely by Contoso Ltd.` in the **specify disclaimer text** flyout.

   - Select **Save** at the bottom of the flyout.

   - Select the link to add a fallback action. In the **specify fallback action** flyout, select **Wrap**, then select **Save** at the bottom of the flyout.

1. Select **Save** at the bottom **Encrypt messages from Finance department** flyout.

1. Once the rule has been changed, you'll see a message stating **Transport rule updated successfully**.

1. Close the flyout by selecting the **X** in the top right corner of the flyout.

You've updated the encryption rule to append a disclaimer to each protected message. This makes it clear to recipients that the email was encrypted and securely transmitted from Contoso Ltd.

## Task 3 – Enable the mail flow rule

By default, new mail flow rules are created in a disabled state. In this task, you'll enable the encryption rule so it can begin protecting messages from the Finance department.

1. On the **Rules** page, select **Disabled** for the newly created **Encrypt messages from Finance department**.

1. In the **Encrypt messages from Finance department** flyout, set the toggle under **Enable or disable rule** to **Enabled**.

1. The mail flow rule will enable automatically. You'll see a message stating **Updating the rule status, please wait...**. Once the rule is enabled, you'll see a message stating **Rule status updated successfully**.

1. Close the flyout by selecting the **X** in the top right corner of the flyout.

The encryption rule is now active and enforcing Microsoft Purview Message Encryption for messages sent from the Finance department. Any future messages from Finance users will be automatically encrypted and include the Contoso Ltd. disclaimer.

## Task 4 – Validate message encryption

In this task, you'll send a test email from a member of the Finance department to confirm that Microsoft Purview Message Encryption is applied automatically and that the recipient sees the secure message notice.

> [!alert] External email delivery might be blocked in some lab environments. This task might not complete as expected.

1. Open **Microsoft Edge** in an InPrivate window by right clicking Microsoft Edge from the task bar and selecting **New InPrivate window**.

1. Navigate to **`https://outlook.office.com`** and log into Outlook on the web as `LynneR@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Lynne's password was set in a previous exercise.

1. On the **Stay signed in?** dialog box, select the checkbox for **Don't show this again** then select **No**.

1. In Outlook on the web, select **New mail**.

1. In the **To** line enter your personal or other third-party email address that isn't in the tenant domain. Enter **`Secret Message`** in the subject line and **`My super-secret message.`** in the body of the email.

1. Select **Send** to send the message. Leave the Outlook window open.

1. Sign into your personal email account in a new window and open the message from Lynne Robbins. If you sent the message to a Microsoft account (such as @outlook.com), it might open automatically. If you sent the email to another email service like (@gmail.com), you might have to perform the next steps to process the encryption and read the message.

    > [!Note] **Note**: You might need to check your junk or spam folder for the message from Lynne Robbins.

1. Select **Read the message**.

1. Select **Sign in with a One-time passcode** to receive a limited time passcode.

1. Go to your personal email portal and open the message with subject **Your one-time passcode to view the message**.

1. Copy the passcode, paste it into the portal and select **Continue**.

1. Review the encrypted message. You should see the **This email has been encrypted and sent securely by Contoso Ltd.** message at the bottom of your email.

You've successfully validated that messages from the Finance department are automatically encrypted and include the appended Contoso disclaimer, confirming that Microsoft Purview Message Encryption is working as expected.
