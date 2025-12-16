# Session 2 - Demo 1 - Create a DSPM data risk assessment

In this demo, you'll see how an administrator uses Microsoft Purview DSPM to assess potential data exposure risks related to Microsoft 365 Copilot. The goal is to identify files that lack sensitivity labels and could be referenced in Copilot responses, helping organizations understand where additional labeling or protection may be needed before expanding AI usage.

**Tasks**:

1. Run a data risk assessment to detect unlabeled content

## Task 1 – Create a data risk assessment to detect unlabeled content

Before enforcing new controls, it's important to understand what data might already be exposed. In this task, you'll create a data risk assessment to identify files without sensitivity labels that Copilot could reference in responses.

1. In **Microsoft Edge**, navigate to **`https://purview.microsoft.com`** and log into the Microsoft Purview portal as `admin@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider).

1. In the Microsoft Purview portal, navigate to **DSPM (preview)** > **Data risk assessments**.

   > **Trainer note**:
   >
   > - Call out that DSPM is currently in preview
   > - Reinforce that this is where AI-specific risk signals and assessments live
   >
   > **Suggested talk track**:
   >
   > _DSPM focuses on understanding how data might be used by AI systems, not just where the data lives._

1. On the **Data risk assessments** page, select **Create custom assessment**

1. On the **Basic details** page, enter:

   - **Name**: `Unlabeled content assessment`
   - **Description**: `Identifies files without sensitivity labels that could be exposed in Copilot.`

   > **Trainer note**:
   >
   > - Don't spend time on wording
   > - Emphasize purpose over metadata
   >
   > **Suggested talk track**:
   >
   > _The important part here is what the assessment does, not how the description is written._

1. Select **Next**.

1. On the **Select scan level** page, leave the default selected then select **Next**.

   > **Trainer note**:
   >
   > **Suggested talk track**:
   >
   > _The default scan level is sufficient for identifying exposure patterns without over-scanning._

1. On the **Add users** page, select **All**, then select **Next**.

1. On the **Add data sources to assess** page, select the options for **SharePoint** and **OneDrive**.

   > **Trainer note**:
   >
   > - Call out why scoping matters for SharePoint content
   > - Don't compare SharePoint to other data sources
   >
   > **Suggested talk track**:
   >
   > _SharePoint often contains shared and broadly accessible content, so scoping helps focus the assessment on the sites that matter most. In a real environment, this is where you'd narrow the scan to high-risk or high-visibility sites._

1. For the **SharePoint** location, under **Actions**, select **Scope sites**.

1. On the **Add SharePoint sites** page, select **Include all sites**, then select **Done**

1. Back on the **Add data sources to assess** page, select **Next**.

1. On the **Review and run the data assessment scan** page, select **Save and run**.

1. On the **Data assessment successfully created** page, select **Done**.

You've created a DSPM data risk assessment that scans SharePoint and OneDrive for unlabeled content that could be referenced by Copilot. This gives visibility into potential exposure risks before enforcing additional protections or expanding AI usage.

   > **Trainer note**:
   >
   > **Suggested talk track**:
   >
   > _This assessment doesn't block anything. It gives you insight so you can decide whether to label data, tighten access, or apply policies before Copilot surfaces it._
