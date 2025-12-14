# Demo 3 - Implement Insider Risk Management

In this demo, you'll see how an administrator enables insider risk detection and quickly creates a policy to identify potential data exfiltration. The demo shows how to turn on the required indicators and use a quick policy to start detecting risky user activity with minimal setup.

**Tasks**:

1. Configure insider risk indicators
1. Create an insider risk policy

## Task 1 – Configure insider risk indicators

In this task, you'll enable the indicators that Insider Risk Management uses to detect risky activity. Policies rely on these indicators to evaluate user behavior.

   > **Trainer note**:
   >
   > - Set expectations that indicators are prerequisites
   > - Emphasize that nothing is detected until these are enabled
   >
   > **Suggested talk track**:
   >
   > _Before any insider risk policy can work, the service needs signals. These indicators define what types of activity Insider Risk Management can evaluate._

1. Return to the Microsoft Edge window where you're signed in as Joni Sherman. Refresh the tab to ensure the new permissions are active.

1. Select **Settings** > **Insider risk management**.

1. Select the tab on the left for **Policy indicators**.

1. On the **Policy indicators** page, expand and select **Select all** to enable all indicators in these categories:

   - Office indicators
   - Cumulative exfiltration detection

1. Select **Save** at the bottom of the page.

   > **Trainer note**:
   >
   > **Suggested talk track**:
   >
   > _At this point, the system can start evaluating user activity. Without this step, policies either won't work or will remain in a warning state._

You've enabled key policy indicators so the system can detect sensitive actions like file exfiltration or risky Office activity.

## Task 2 – Create an insider risk policy

In this task, you'll create a quick data leaks policy to start detecting risky data exfiltration behavior using built-in defaults.

   > **Trainer note**:
   >
   > - Call out that this is a quick policy
   > - Emphasize speed and safe defaults
   > - Do not open customization
   >
   > **Suggested talk track**:
   >
   > _Now the service can evaluate behavior. Any policy created before this would stay in a warning state._

1. In Microsoft Purview, select **Solutions** > **Insider Risk Management** > **Policies**.

1. On the **Policies** page, select **Create policy**, then select **Quick policy**.

1. On the **Create quick policies** flyout, select to **Get started** under **Data leaks**.

1. Review the settings for creating a quick data leak policy, then select **Create policy**.

   > **Trainer note**:
   >
   > - One sentence only
   >
   > **Suggested talk track**:
   >
   > _These notifications help security teams stay aware of policy health and high-risk activity without constantly checking the portal._

1. On the **Your data leak policy is being created** page, select the checkboxes for:

   - Email me when policies have unresolved warnings
   - Email me when new high severity alerts are generated

     Then select **Update notification settings**.

1. On the bottom of the **Your data leak policy is being created** page, select **Done**.

   > **Trainer note**:
   >
   > **Suggested talk track**:
   >
   > _At this point, insider risk detection is active. Indicators are enabled, and a policy is in place to identify potential data exfiltration._

You've created a quick policy for detecting potential data leaks using the default settings.
