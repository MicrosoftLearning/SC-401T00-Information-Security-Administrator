# Session 2 - Demo 3 - Create a DLP policy for Microsoft 365 Copilot

In this demo, you'll see how an administrator uses Microsoft Purview Data Loss Prevention to control how sensitive, labeled content is handled during Microsoft 365 Copilot interactions. The goal is to validate Copilot-specific DLP behavior in simulation mode before enabling enforcement, so organizations can understand impact without disrupting users.

**Tasks**:

- Create a DLP policy in simulation mode

## Task 1 – Create a DLP policy in simulation mode

Before enforcing Copilot restrictions, it's important to understand how DLP policies evaluate prompts and referenced content. In this task, you'll create a DLP policy that prevents Copilot from processing sensitive, labeled content, while running safely in simulation mode.

1. Log into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account.

1. In **Microsoft Edge**, navigate to **`https://purview.microsoft.com`** and log into the Microsoft Purview portal as **Joni Sherman**. Sign in as `JoniS@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant prefix provided by your lab hosting provider). User account passwords are provided by your lab hosting provider.

   > **Trainer note**:
   >
   > - Emphasize that this is the same DLP engine used across Microsoft Purview
   > - Call out that Copilot is now a first-class DLP location risk signals and assessments live
   >
   > **Suggested talk track**:
   >
   > _Copilot doesn't introduce a new protection model. It extends existing DLP policies into AI interactions._

1. Select **Solutions** > **Data Loss Prevention** > **Policies**.

1. On the **Policies** page, select **+ Create policy**.

1. On the **What info do you want to protect?** page, select **Enterprise applications & devices**, then select **Next**.

1. On the **Start with a template or create a custom policy** page, select **Custom** as the category, then select **Custom policy** under **Regulations**.

1. Select **Next**.

1. On the **Name your DLP policy** page enter:

   - **Name**: `Protect sensitive data in Microsoft 365 Copilot`
   - **Description**: `Prevents sensitive information from being used or exposed through Microsoft 365 Copilot.`

   > **Trainer note**:
   >
   > - Don't spend time on naming conventions
   > - Focus on scoping and behavior
   >
   > **Suggested talk track**:
   >
   > _The name isn't important here. What matters is that the policy is clearly scoped to Copilot._

1. Select **Next**.

1. On the **Assign admin units** page select **Next**.

1. On the **Choose where to apply the policy** page, enable the location for **Microsoft 365 Copilot and Copilot Chat** only. If any other locations are selected, deselect them.

   > **Trainer note**:
   >
   > - Reinforce that only Copilot is selected
   > - Call out that this avoids unintended impact to Exchange, SharePoint, or Teams
   >
   > **Suggested talk track**:
   >
   > _This policy only evaluates Copilot interactions. It doesn't apply to email, files, or chats outside of Copilot._

1. Select **Next**.

1. On the **Define policy settings** page, select **Create or customize advanced DLP rules**, then select **Next**.

1. On the **Customize advanced DLP rules** page, select **+ Create rule**.

   > **Trainer note**:
   >
   > - Emphasize reuse of existing sensitivity labels
   > - Don't explain label creation here
   >
   > **Suggested talk track**:
   >
   > _Copilot protections build on the same labels you're already using to classify data elsewhere._

1. In the **Create rule** flyout:
    - In the **Name** field, enter `Block sensitive data in Copilot`.

1. Under **Conditions**, select **+ Add condition** > **Content contains**.

1. In the new **Content contains** section:
    - Select **Add** > **Sensitivity labels**.
    - On the **Sensitivity labels** page, select **Project - Falcon**, then select **Add**.

1. Under **Actions**, select **+ Add an action** > **Restrict Copilot from processing Content**.

1. In the new **Restrict Copilot from processing Content** section, select the checkbox for **Accessing knowledge sources**.

   > **Trainer note**:
   >
   > - Clarify what "restrict Copilot from processing content" actually does
   > - Avoid deep implementation detail
   >
   > **Suggested talk track**:
   >
   > _This action prevents Copilot from using sensitive content in prompts or responses, even if the user has access to the data._

1. At the bottom of the **Create rule** flyout panel, select **Save**.

1. Back on the **Customize advanced DLP rules**, select **Next**.

1. On the **Policy mode** page select **Run the policy in simulation mode** and select the checkbox for **Show policy tips while in simulation mode**.

   > **Trainer note**:
   >
   > - Strongly reinforce why simulation mode matters for Copilot
   >
   > **Suggested talk track**:
   >
   > _Simulation mode lets you observe how Copilot would behave under enforcement without blocking users. This is especially important when introducing AI controls._

1. Select **Next**.

1. On the **Review and finish** page review your settings then select **Submit**.

1. On the **New policy created** page select **Done**.

You've created a Microsoft Purview DLP policy scoped specifically to Microsoft 365 Copilot and running in simulation mode. This policy prevents Copilot from processing sensitive, labeled content, allowing you to observe how Copilot interactions are evaluated before enforcement is enabled.

This gives organizations confidence to refine policies, review simulation results, and move toward enforcement while minimizing risk to productivity.

   > **Trainer note**:
   >
   > **Suggested talk track**:
   >
   > This doesn't stop Copilot today. It gives visibility into what would happen, so you can make informed decisions before turning enforcement on.
