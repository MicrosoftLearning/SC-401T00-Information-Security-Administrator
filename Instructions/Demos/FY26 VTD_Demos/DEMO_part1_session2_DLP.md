# Demo 2 – Implement and manage DLP policies

In this demo, you'll see how an administrator creates a data loss prevention (DLP) policy using a built-in template. The demo shows how to start from a template, make a small customization to the data being detected, and apply the policy so it protects Teams messages in Microsoft 365.

**Tasks**:

- Create a DLP policy from a built-in template.

## Task 1 – Create a DLP policy from a built-in template

In this task, you'll create a DLP policy using a built-in template and customize it slightly to match business needs.

   > **Trainer note**:
   >
   > - Set expectations up front that this demo uses a template
   > - Emphasize speed and starting points, not full customization
   >
   > **Suggested talk track**:
   >
   > _Most organizations don't start DLP from scratch. They start from a template and adjust it. That's what we're doing here._

1. Log into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account.

1. In **Microsoft Edge**, navigate to **`https://purview.microsoft.com`** and log into the Microsoft Purview portal.

1. Select **Solutions** > **Data Loss Prevention** > **Policies**.

1. On the **Policies** page, select **+ Create policy**.

1. On the **What info do you want to protect?** page, select **Enterprise applications & devices**, then select **Next**.

1. On the **Start with a template or create a custom policy** page, select **Financial** as the category, then select **PCI Data Security Standard (PCI DSS)** under **Regulations**.

   > **Trainer note**:
   >
   > - One sentence only
   >
   > **Suggested talk track**:
   >
   > _Templates give you a baseline policy with recommended settings that you can adapt._

1. Select **Next**.

1. On the **Name your DLP policy** page, select **Next**.

1. On the **Assign admin units** page select **Next**.

1. On the **Choose where to apply the policy** page, enable the location for **Teams chat and channel messages** only. If any other locations are selected, deselect them.

   > **Trainer note**:
   >
   > - Call out scoping
   > - Don't explain every location
   >
   > **Suggested talk track**:
   >
   > _Scoping policies to specific workloads helps reduce noise and unintended impact._

1. Select **Next**.

1. On the **Define policy settings** page, select **Review and customize default settings from the template**, then select **Next**.

   > **Trainer note**:
   >
   > - This is a key moment
   >
   > **Suggested talk track**:
   >
   > _This option lets you see what the template configured and make targeted changes._

1. On the **Info to protect** page, under **Content contains any of these sensitive info types**, select **Edit**.

1. On the **Choose the types of content to protect** flyout, under **Credit Card Number** select **Add** > **Sensitive info types**.

1. On the **Sensitive info types** flyout, search for `IBAN`, then select the checkbox for **International Banking Account Number (IBAN)**.

1. Select **Add** at the bottom of the flyout.

1. Back on the **Choose the types of content to protect** flyout, select **Save**.

   > **Trainer note**:
   >
   > - Call out why this matters
   >
   > **Suggested talk track**:
   >
   > _This is a common step. You start with a template and add data types that are relevant to your organization._

1. Back on the **Info to protect page**, ensure the checkbox for **Detect when this content is shared in Microsoft 365** is selected, and the option for **With people outside my organization** is selected.

1. Select **Next**.

1. On the **Protection actions** page, review the default settings, then select **Next**.

   > **Trainer note**:
   >
   > - Do not enumerate actions
   >
   > **Suggested talk track**:
   >
   > _Templates also define how content is protected, not just what's detected._

1. On the **Customize access and override settings** page, select the checkbox for **Restrict access or encrypt the content in Microsoft 365 locations**, then select **Next**.

1. On the **Policy mode** page, select **Turn the policy on immediately**, then select **Next**.

   > **Trainer note**:
   >
   > - Contrast with simulation mode without going deep
   >
   > **Suggested talk track**:
   >
   > _In production, policies often start in simulation. Here we're turning it on to show the full lifecycle._

1. On the **Review and finish** page review your settings then select **Submit**.

1. On the **New policy created** page select **Done**.

You've created a DLP policy that scans Teams content for financial data and applies protection based on the template settings.

   > **Trainer note**:
   >
   > - Tie back to the slide
   >
   > **Suggested talk track**:
   >
   > _At this point, the policy is created from a template, customized for additional data types, scoped to Teams, and enforcing protection._
