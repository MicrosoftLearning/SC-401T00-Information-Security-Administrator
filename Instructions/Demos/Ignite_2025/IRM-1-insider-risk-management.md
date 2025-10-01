# Lab – Detect and adapt to risky AI usage with Insider Risk Management

Megan Bowen, the Information Security Administrator at Contoso Ltd., is preparing for a broad Copilot rollout. Leadership is concerned about employees unintentionally exposing sensitive data when using Copilot and other AI tools. To address this risk, Megan will configure Insider Risk Management to detect risky prompts and responses, prioritize critical project content, and connect policies with DLP and Adaptive Protection. She'll begin with a pilot for the Mark 8 Project Team.

**Tasks**:

1. Enable analytics
1. Configure global exclusions
1. Configure insider risk indicators
1. Create a Risky AI usage policy
1. Create a notice template
1. Configure insider risk levels
1. Create a DLP policy
1. Enable Adaptive Protection

## Task 1 – Enable analytics

In this task, you'll enable Insider Risk Management analytics to surface organization-wide patterns.

1. Log into Client 1 VM (SC-401-CL1) with the **Admin** account.

1. Open Microsoft Edge.

1. In **Microsoft Edge**, navigate to `https://purview.microsoft.com` and sign in as **Megan Bowen** (`MeganB@WWLxZZZZZZ.onmicrosoft.com`, where ZZZZZZ is your unique tenant ID). Use the password provided by your lab host.

1. Select **Get started** on the welcome message for the new Microsoft Purview portal.

    ![Screenshot showing the Welcome to the new Microsoft Purview portal screen.](./media/welcome-purview-portal.png)

1. From the left sidebar, select **Settings** > **Insider risk management**.

1. On the **Insider Risk Management settings** page, select **Analytics** from the left navigation.

1. On the **Analytics** page, under **Show insights at tenant level**, switch the toggle to **On**.

1. Select **Save** at the bottom of the page.

You've enabled analytics, giving you baseline insights into risky activity that can guide policy decisions.

## Task 2 – Configure global exclusions

In this task, you'll add a global exclusion to reduce alerts from trusted partners.

1. On the **Insider Risk Management settings** page, select **Global exclusions** in the left navigation.

1. On the **Global exclusions** page, select **+ Add domains to exclude**.

1. In the **Add allowed domains** flyout, in the **Domain** field:

   - Type `*.fabrikam.com`
   - Select the checkbox for **Include multi-level subdomains**

1. Press the **Enter** key on your keyboard, then select **Add domains** at the bottom of the flyout.

You've excluded the Fabrikam domain, so sharing with this partner won't trigger insider risk alerts.

## Task 3 – Configure insider risk indicators

In this task, you'll enable indicators that detect risky Copilot activity and DLP alerts.

1. On the **Insider Risk Management settings** page, select the tab on the left for **Policy indicators**.

1. Expand each category and enable the following indicators:

   **Generative AI apps** > **Microsoft Copilot experiences**

   - Receiving sensitive response from Copilot
   - Entering risky prompt in Copilot

   **Generative AI apps** > **Other AI apps**

   - Entering risky prompt in other AI apps

   **Data loss prevention (DLP) alert indicators** > **Detect when DLP policies generate alerts**

   - Select **+Add policy**
   - In the **Add DLP policies** select **Default policy for Teams**, then select **Add** at the bottom of the flyout.

1. Select **Save** at the bottom of the page.

You've turned on AI and DLP indicators, allowing policies to catch risky prompts, responses, and alerts.

## Task 4 – Create a Risky AI usage policy

In this task, you'll create a Risky AI usage policy for the Mark 8 Project Team.

1. In the Microsoft Purview portal, go to **Solutions** > **Insider Risk Management** > **Policies**.

1. On the **Policies** page, select **+ Create policy** > **Custom policy**.

1. On the **Choose a policy template** page, select **Risky AI usage**, then select **Next**.

1. On the **Name your policy** page, enter:

   - **Name**: `Risky AI usage - Mark 8 Project Team`
   - **Description**: `Detects risky Copilot prompts, responses, and AI app usage for the Mark 8 Project Team.`

1. Select **Next**.

1. On the **Choose users, groups, & adaptive scopes** page, select **Specific users, groups, and adaptive scopes**.

1. On the **Choose users, groups, & adaptive scopes** page, under **Groups**:

   - Select **+ Add groups**.
   - In the **Choose groups** flyout, select the checkbox for **Project Falcon**, then select **Add**.

1. Back on the **Choose users, groups, & adaptive scopes** page, select **Next**.

1. On the **Exclude users and groups (optional)** page, under **Groups**:

   - Select **+ Add groups to exclude**.
   - In the **Choose groups** flyout, select the checkbox for **Executives**, then select **Add**.

1. Back on the **Exclude users and groups (optional)** page, select **Next**.

1. On the **Decide whether to prioritize content** page, select **I want to prioritize content**, then select the checkbox for **Sharepoint sites**.

1. Select **Next**.

1. On the **SharePoint sites to prioritize** page, select **+ Add or edit SharePoint sites**.

1. In the **Add or edit SharePoint sites** flyout, select the checkbox for **Mark 8 Project Team**, then select **Add**.

1. Back on the **SharePoint sites to prioritize** page, select **Next**.

1. On the **Decide whether to score only activity with priority content** page, select **Get alerts for all activity**, then select **Next**.

1. On the **Choose triggering event for this policy** page, select **Risky or sensitive content in Microsoft Copilot experiences, Enterprise AI apps and web versions of other AI apps**.

1. Under **Select which activities will trigger this policy**, check the boxes for:

   - Entering risky prompt in Copilot
   - Receiving sensitive response from Copilot
   - Entering risky prompt in other AI apps

1. Select **Next**.

1. On the **Choose thresholds for triggering events** page, select **Apply built-in thresholds**, then select **Next**.

1. On the **Indicators** page, confirm that the Copilot, other AI apps, and DLP indicators are selected, then select **Next**.

1. On the **Detection options** page, leave the defaults selected, then select **Next**.

1. On the **Choose threshold type for indicators** page, select **Apply thresholds provided by Microsoft**, then select **Next**.

1. On the **Review settings and finish** page, review your settings, then select **Submit**.

1. On the **Your policy was created** page, select **Done**.

You've created a policy that detects risky prompts and responses in Copilot and other AI apps.

## Task 5 – Create a notice template

In this task, you'll create a notice template to notify users when risky AI activity is detected.

1. In the Microsoft Purview portal, from the **Policies** page, select **Notice templates** from the left navigation.

1. On the **Notice templates** page, select **+ Create notice template**.

1. In the **Create a new notice template** flyout, enter:

   - **Template name**: `Risky AI activity alert`
   - **Send from**: `Megan Bowen`
   - **Subject**: `Review required: Risky AI activity detected`
   - **Message body**:

        ```html
        <!DOCTYPE html>
        <html>
        <body>
        <h2>AI Usage Alert</h2>
        <p>We've detected potentially risky activity in your use of Copilot or other AI apps. This may include submitting sensitive prompts or receiving sensitive responses.</p>
        <p>Please review your recent activity to ensure it complies with Contoso's acceptable use policies. If you believe this alert was generated in error, contact the IT Security team.</p>
        <p>Refer to the <a href="https://contoso.com/ai-guidelines">AI usage guidelines</a> for best practices.</p>
        <p>Thank you,</p>
        <p><em>Contoso Security and Compliance Team</em></p>
        </body>
        </html>
        ```

1. Select **Create** to save the template.

1. Back on the **Notice templates** page, verify that the `Risky AI activity alert` template appears in the list.

You've created a notice template that reviewers can use to send consistent guidance to users.

## Task 6 – Configure insider risk levels

In this task, you'll map your AI usage policy to insider risk levels so risky Copilot activity can escalate enforcement.

1. In the Microsoft Purview portal, go to **Solutions** > **Insider Risk Management** > **Adaptive Protection**.

1. From the left navigation, select **Insider risk levels**.

1. On the **Insider risk levels** page:

   - In the **Insider risk policy** dropdown, select the **Risky AI usage - Mark 8 Project Team** policy you created earlier.
   - Leave the default risk level settings unchanged.
   - Select **Save**.

You've connected your Risky AI usage policy to risk levels, letting Copilot and AI signals raise a user's risk status.

## Task 7 – Create a DLP policy

In this task, you'll create a DLP policy that blocks external sharing when risky Copilot activity pushes a user to an elevated risk level.

1. On the **Adaptive Protection** page, select **Data Loss Prevention** from the left navigation.

1. On the **Data Loss Prevention policies** page, select **+ Create policy**.

1. On the **Choose what type of data to protect** page, select **Data stored in connected sources**, then select **Next**.

1. On the **Start with a template or create a custom policy** page, under **Categories**, select **Privacy**. Under **Regulations**, select **U.S. Personally Identifiable Information (PII) Data Enhanced**, then select **Next**.

1. Keep the defaults selected until you reach the **Info to protect** page.

1. On the **Info to protect** page, expand **Insider risk level for Adaptive Protection** and select **Elevated risk**.

1. Select **Next**.

1. On the **Protection actions** page, select **Next**.

1. On the **Customize access and override settings** page:

   - Select **Restrict access or encrypt the content in Microsoft 365 locations**.
   - Choose **Block only people outside your organization**.
   - Select **Next**.

1. On the **Policy mode** page, select **Run the policy in simulation mode**, then select the checkboxes for:

   - **Show policy tips while in simulation mode**
   - **Turn the policy on if it's not edited within fifteen days of simulation**

1. Select **Next**.

1. On the **Review and finish** page, select **Submit**.

1. On the **New policy created** page, select **Done**.

You've created a DLP policy that blocks external sharing for users with risky Copilot activity, containing exposure before it spreads.

## Task 8 – Enable Adaptive Protection

In this task, you'll enable Adaptive Protection so DLP reacts automatically to risky Copilot usage.

1. On the **Adaptive Protection** page, select **Adaptive Protection settings** from the left navigation.

1. Set the toggle to **On** under **Adaptive Protection** to enable Adaptive Protection.

You've turned on Adaptive Protection, allowing DLP policies to tighten enforcement the moment risky AI behavior is detected.

## Lab complete

You enabled analytics, set exclusions, and turned on AI risk indicators. You then built a Risky AI usage policy, connected it to Adaptive Protection, and linked it with DLP enforcement. With these controls in place, Contoso can detect risky Copilot and AI activity and automatically strengthen protections before sensitive data is exposed.
