# Session 2 - Demo 4 - Create an Insider Risk Management policy for Risky AI Usage

In this demo, you'll see how an administrator enables the signals required for risky AI usage detection and quickly creates an Insider Risk Management policy using built-in defaults. The goal is to begin identifying risky AI-related browsing behavior with minimal configuration.

**Tasks**:

1. Configure insider risk indicators
1. Create a risky AI usage policy

## Task 1 – Configure insider risk indicators

Before a risky AI usage policy can evaluate activity, Insider Risk Management needs signals that describe the types of behavior it should analyze. In this task, you'll enable the indicators that support risky AI usage detection.

1. In **Microsoft Edge**, navigate to **`https://purview.microsoft.com`** and log into the Microsoft Purview portal as `admin@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider).

1. Select **Settings** > **Insider risk management**.

1. Select the tab on the left for **Policy indicators**.

1. On the **Policy indicators** page, expand **Risky browsing indicators (preview)**, then select the **Select all** checkbox to enable all indicators in this category.

   > **Trainer note**:
   >
   > - Call out that indicators define what activity can be evaluated
   > - Emphasize that risky AI usage relies on browsing signals
   >
   > **Suggested talk track**:
   >
   > _Risky AI usage policies rely on browsing indicators like these, but they also depend on devices being onboarded so browser activity can be evaluated. That's why this works across managed devices without inspecting prompts._

1. Select **Save** at the bottom of the page.

You've enabled the indicators that allow Insider Risk Management to evaluate risky browsing activity related to AI tools.

## Task 2 – Create a risky AI usage policy

With indicators enabled, you can now create a risky AI usage policy. In this task, you'll use a quick policy to apply Microsoft's built-in defaults and start detection without manual tuning.

1. In Microsoft Purview, select **Solutions** > **Insider Risk Management** > **Policies**.

1. On the **Policies** page, select **Create policy**, then select **Quick policy**.

1. On the **Create quick policies** flyout, select **Get started** under **Risky AI Usage**.

   > **Trainer note**:
   >
   > - Call out that this is a quick policy
   > - Emphasize speed and built-in defaults
   > - Don't open advanced customization
   >
   > **Suggested talk track**:
   >
   > _Quick policies are designed to get detection running quickly, using defaults that balance visibility and impact._

1. Review the settings for creating a quick risky AI usage policy, then select **Create policy**.

1. On the **Your risky AI usage policy is being created** page, select the checkboxes for:

   - Email me when policies have unresolved warnings
   - Email me when new high severity alerts are generated

     Then select **Update notification settings**.

1. On the bottom of the **Your data leak policy is being created** page, select **Done**.

   > **Trainer note**:
   >
   > **Suggested talk track**:
   >
   > _This policy doesn't block activity. It provides visibility so security teams can investigate and respond to risky AI usage patterns._

You've created a risky AI usage policy using built-in defaults to begin detecting potentially risky AI-related activity.
