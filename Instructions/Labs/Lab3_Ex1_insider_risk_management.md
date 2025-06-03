---
lab:
    title: 'Exercise 1 - Implement Insider Risk Management'
    module: 'Module 3 - Implement Insider Risk Management'
---

## WWL Tenants - Terms of use

If you are being provided with a tenant as a part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training.

Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and are not eligible for extension.

Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time.

# Lab 3 - Exercise 1 - Implement Insider Risk Management

You are Joni Sherman, the Information Security Administrator for Contoso Ltd. Your role involves ensuring regulatory compliance and protecting sensitive information within the organization. Recently, Contoso Ltd. has noticed unusual browsing activities that could potentially expose sensitive data. To proactively address this insider risk, you will implement Microsoft Purview Insider Risk Management, focusing on identifying, analyzing, and responding to potential insider threats effectively.

**Tasks**:

1. Assign insider risk management permissions
1. Configure insider risk indicators
1. Create an insider risk policy
1. Customize the data leaks policy
1. Enable Microsoft Defender for Endpoint integration with Insider Risk Management
1. Enable indicators and configure priority users
1. Create a policy for security policy violations by priority users
1. Create a notice template

## Task 1 – Assign insider risk management permissions

In this task, you'll assign Joni Sherman the Insider Risk Management role so she can access and manage insider risk features in Microsoft Purview.

1. Sign into the Client 1 VM (SC-401-CL1) as the **SC-401-cl1\admin** account.

1. In Microsoft Edge, navigate to **`https://purview.microsoft.com`** and sign into the Microsoft Purview portal as MOD Administrator, `admin@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.

1. Select **Settings** > **Roles and Scopes** > **Role groups**.

1. On the **Role groups for Microsoft Purview solutions** page select **Insider Risk Management**.

1. On the **Insider Risk Management** flyout panel on the right, select **Edit**.

1. On the **Edit members of the role group** page select **+ Choose users**.

1. On the **Choose users** flyout panel, search for `Joni` then select the checkbox for **Joni Sherman**.

1. Select the **Select** button at the bottom of the panel.

1. On the **Edit members of the role group** page select **Next**.

1. On the **Review the role group and finish** page select **Save**.

1. Once you have successfully added Joni to the role group, select **Done** on the **You successfully updated the role group** page.

1. Sign out of the **Mod Administrator** account by selecting the MA icon on the top right of the window, then selecting **Sign out**.

You've assigned Joni the necessary permissions to work with Insider Risk Management in the Microsoft Purview portal.

## Task 2 – Configure insider risk indicators

Before you create an insider risk policy, you'll turn on the indicators needed for detection. These indicators define the types of risky activity the system will look for.

1. In **Microsoft Edge**, navigate to **`https://purview.microsoft.com`** and sign into the Microsoft Purview portal as `JoniS@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider).

1. Select **Settings** > **Insider risk management**.

1. Select the tab on the left for **Policy indicators**.

1. On the **Policy indicators** page, expand and select **Select all** to enable all indicators in these categories:

   - Office indicators
   - Cumulative exfiltration detection

1. Select **Save** at the bottom of the page.

You've enabled key policy indicators so the system can detect sensitive actions like file exfiltration or risky Office activity.

## Task 3 – Create an insider risk policy

In this task, you'll create a data leaks quick policy to automatically detect and respond to risky user behavior related to data exfiltration. Quick policies use built-in templates and default thresholds to simplify setup.

1. In Microsoft Purview, select **Solutions** > **Insider Risk Management** > **Policies**.

1. On the **Policies** page, select **Create policy**, then select **Quick policy**.

1. On the **Create quick policies** flyout, select to **Get started** under **Data leaks**.

1. Review the settings for creating a quick data leak policy, then select **Create policy**.

1. On the **Your data leak policy is being created** page, select the checkboxes for:

   - Email me when policies have unresolved warnings
   - Email me when new high severity alerts are generated

     Then select **Update notification settings**.

1. On the bottom of the **Your data leak policy is being created** page, select **Done**.

You've created a quick policy for detecting potential data leaks using the default settings. Next, you'll customize it to resolve the configuration warning.

## Task 4 – Customize the data leaks policy

Some insider risk policies require additional indicators to function correctly. In this task, you'll modify your policy to enable sequence indicators and bring the policy into a healthy state.

On the **Policies** page for **Insider Risk Management**, you'll notice your data leaks policy has a recommendation.

1. Select the **Data leaks quick policy** you just created.

1. Review the recommendation in the flyout page for the policy. You have a warning stating **Sequence trigger required indicators are not selected**. To resolve this warning, select **Edit policy**.

1. On the **Choose a policy template** page, select **Next**.

1. On the **Name your policy** page, select **Next**.

1. On the **Choose users, groups, & adaptive scopes** page, select **Next**.

1. On the **Exclude users and groups (optional) (preview)** page, select **Next**.

1. On the **Decide whether to prioritize content** page, select **Next**

1. On the **Choose triggering event for this policy** page, review the **Select which sequences will trigger this policy** and view the information stating **Some sequences require specific indicators to be turned on in 'Settings' before they can be selected below.**

1. Select the option to **Turn on indicators** to enable the necessary sequence indicators for this policy.

1. Data leaks is primarily a data exfiltration insider risk policy. In the dialogue to enable sequence indicators, select **Select all** to turn on all required **Exfiltrate indicators**, then select **Save**.

1. Select **Next** on the **Choose triggering event for this policy** page.

1. On the **Choose thresholds for triggering events** page, select **Next**.

1. On the **Indicators** page, select **Next**.

1. On the **Detection options**, select **Next**.

1. On the **Choose threshold type for indicators** page, select **Next**.

   This policy uses a built-in triggering event and indicators. It starts evaluating user activity only when Microsoft Defender for Endpoint detects threats like defense evasion or unwanted software.

1. On the **Review settings and finish** page, select **Submit**.

1. Select **Done** on the **Your policy was created** page.

1. Back on the **Policies** page, your policy should now have a **Healthy** status.

Your insider risk policy is now healthy and ready to detect risky activities based on sequence triggers and enabled indicators.

## Task 5 – Enable Microsoft Defender for Endpoint integration with Insider Risk Management

In this task, you'll enable integration between Microsoft Defender for Endpoint and Microsoft Purview so security alerts can be used in insider risk policies.

1. In Microsoft Edge, navigate to Microsoft Defender by going to `https://security.microsoft.com`.

1. In the left navigation pane, select **Settings** > **Endpoints** > **Advanced features**.

1. Scroll down and select the toggle to **On** to **Share endpoint alerts with Microsoft Compliance Center**.

   ![Screenshot showing the Share endpoints with Microsoft Compliance Center toggle.](../Media/enable-irm-in-mde.png)

1. Select **Save preferences** at the bottom of the screen.

You've successfully enabled Defender for Endpoint to share alerts with Microsoft Purview.

## Task 6 – Enable indicators and configure priority users

In this task, you'll configure the policy indicators and create a priority user group that can be used in insider risk policies.

> [!note] Microsoft Defender for Endpoint indicators might appear greyed out and unselectable if the integration from the previous task hasn't finished processing. If that happens, wait a few minutes and refresh the page before continuing.

1. In **Microsoft Edge**, navigate to `https://purview.microsoft.com`.

1. Select **Settings** > **Insider risk management**.

1. Select the tab on the left for **Policy indicators**.

1. On the **Policy indicators** page, expand and select **Select all** to enable all indicators in these categories:

   - Microsoft Defender for Endpoint indicators (preview)
   - Risky browsing indicators (preview)

1. Select **Save** at the bottom of the page.

1. Select the **Priority user groups** tab, then select **+ Create priority user group**.

1. On the **Name and describe the priority user group** page, enter:

   - **Name**: `Finance team`
   - **Description**: `Team members who manage financial operations, budgeting, and payroll systems.`

1. Select **Next**.

1. On the **Members** page, select **+ Members**.

1. In the **Members** flyout, search for and select:

   - `Lynne Robbins`
   - `Debra Berger`
   - `Megan Bowen`

1. Select **Add** to add the three members to the Finance team priority group.

1. Select **Next**.

1. On the **Choose who can view data involving users in this priority group**, select **+ Choose users and role groups**.

1. In the flyout, select the checkbox for **Insider Risk Management**, then select **Add**.

1. Select **Next**.

1. **Review** and **Submit** your settings, then select **Done** once your priority user group has been created.

You've configured policy indicators and created a priority group for monitoring high-risk users.

## Task 7 – Create a policy for security policy violations by priority users

In this task, you'll create an insider risk policy that detects Defender for Endpoint alerts for risky activity by priority users.

1. In Microsoft Purview, select **Solutions** > **Insider Risk Management** > **Policies**.

1. On the **Policies** page, select **Create policy**, then select **Custom policy**.

1. On the **Choose a policy template** page, select **Security policy violations by priority users (preview)**, then select Next.

1. On the **Name your policy** page, enter:

   - **Name**: `Security policy violations - Priority users`
   - **Description**: `Detects Defender for Endpoint alerts for risky activity by priority users, such as malware or disabled protections.`

1. Select **Next**.

1. On the **Choose users, groups, & adaptive scopes** page, select **Add or edit priority user groups**.

1. On the **Choose priority user groups** flyout, select the checkbox for the **Finance team** group, then select Add.

1. Select **Next**.

1. On the **Decide whether to prioritize content** page, select **Next**.

1. On the **Choose triggering event for this policy** page, select **Next**.

1. On the **Indicators** page, select **Next**.

1. On the **Choose threshold type for indicators** page, leave the default **Apply thresholds provided by Microsoft** option selected, then select **Next**.

1. On the **Review settings and finish** page, select **Submit**.

1. On the **Your policy was created** page, select **Done**.

You've created a custom insider risk policy that uses Defender for Endpoint signals to detect risky activity from priority users.

## Task 8 – Create a notice template

In this task, you'll create a notice template in Microsoft Purview to notify users when an insider risk alert is triggered.

1. In Microsoft Purview, select **Solutions** > **Insider Risk Management** > **Notice templates**.

1. On the **Notice templates** page, select **+ Create notice template**.

1. Fill out the necessary information in **Create a new notice template** flyout panel on the right.

    - **Template name**: `Security Violation Alert`
    - **Send from**: `Joni Sherman`
    - **Subject**: `Unusual activity detected - please review`
    - **Message body**:

        ````html
        <!DOCTYPE html>
        <html>
        <body>
        <h2>Security Alert</h2>
        <p>We've detected activity from your account that might violate our organization's security policies. This could be due to malware, disabled protections, or other risky behavior.</p>
        <p>Please review your recent actions and ensure your device security settings are up to date. If you believe this alert was generated in error, contact the IT Security team for assistance.</p>
        <p>To avoid future issues, refer to the <a href="https://contoso.com/security-guidelines">Contoso Security Guidelines</a>.</p>
        <p>Thank you,</p>
        <p><em>Compliance and Security Team</em></p>
        </body>
        </html>
        ````

1. Select **Create**.

1. Back on the **Notice templates** page you'll see the **Security Violation Alert** template you just created.

You've created a notice template that Insider Risk Management can use to notify users of security policy violations.
