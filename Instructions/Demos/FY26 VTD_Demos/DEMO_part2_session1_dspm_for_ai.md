# Session 2 - Demo 1 - Create a DSPM for AI data risk assessment

You are Joni Sherman, the Information Security Administrator for Contoso Ltd. As AI tools like Microsoft Copilot become more integrated into daily workflows, your team has been asked to assess and improve protections around sensitive data. In this lab, you'll explore how Microsoft Purview DSPM for AI can help secure data interactions with AI tools through policy enforcement, risk detection, and exposure assessments.

**Tasks**:

1. Run a data assessment to detect unlabeled content

## Task 1 – Create a data risk assessment to detect unlabeled content

To understand potential gaps in labeling coverage, you'll run a data risk assessment to identify files without sensitivity labels that may be accessed by Copilot.

1. In **DSPM for AI**, select the recommendation titled **Protect sensitive data referenced in Copilot and agent responses**.

1. In the **Protect sensitive data referenced in Copilot and agent responses** pane, review the summary, then select **Go to assessments**.

1. On the **Data risk assessments** page, select **Create custom assessment**

1. On the **Basic details** page, enter:

   - **Name**: `Unlabeled File Exposure Assessment`
   - **Description**: `Identifies files without sensitivity labels that may be exposed in Microsoft 365 Copilot responses and provides recommendations to reduce oversharing risks.`

1. Select **Next**.

1. On the **Add users** page, select **All**, then select **Next**.

1. On the **Add data sources to assess** page, leave the default location of **SharePoint** selected, then select **Next**.

1. On the **Review and run the data assessment scan** page, select **Save and run**.

1. On the **Data assessment successfully created** page, select **Done**.

You've now used Microsoft Purview DSPM for AI to detect AI-related risks, enforce policies, and assess sensitive data exposure, helping your organization use AI securely.