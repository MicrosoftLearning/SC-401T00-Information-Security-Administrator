# Lab 2 – Implement and manage DLP policies

Joni Sherman, the newly hired Information Security Administrator at Contoso Ltd., has been asked to configure data loss prevention (DLP) policies to help protect sensitive customer data across Microsoft 365. In this lab, you'll use Microsoft Purview and Microsoft Defender to create and manage DLP policies that detect and restrict the sharing of sensitive information such as credit card numbers and employee IDs.

**Tasks**:

1. Create a DLP policy in simulation mode
1. Modify a DLP policy

## Task 1 – Create a DLP policy in simulation mode

In this task, you'll create a DLP policy in simulation mode that targets credit card numbers in Teams messages. The policy will notify users when they attempt to share sensitive content and allow them to override with justification.

1. Log into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account.

1. In **Microsoft Edge**, navigate to **`https://purview.microsoft.com`** and log into the Microsoft Purview portal.

1. Select **Solutions** > **Data Loss Prevention** > **Policies**.

1. On the **Policies** page, select **+ Create policy**.

1. On the **What info do you want to protect?** page, select **Enterprise applications & devices**, then select **Next**.

1. On the **Start with a template or create a custom policy** page, select **Financial** as the category, then select **PCI Data Security Standard (PCI DSS)** under **Regulations**.

1. Select **Next**.

1. On the **Name your DLP policy** page, select **Next**.

1. On the **Assign admin units** page select **Next**.

1. On the **Choose where to apply the policy** page, enable the location for **Teams chat and channel messages** only. If any other locations are selected, deselect them.

1. Select **Next**.

1. On the **Define policy settings** page, select **Review and customize default settings from the template**, then select **Next**.

1. On the **Info to protect** page, under **Content contains any of these sensitive info types**, select **Edit**.

1. On the **Choose the types of content to protect** flyout, under **Credit Card Number** select **Add** > **Sensitive info types**.

1. On the **Sensitive info types** flyout, search for `IBAN`, then select the checkbox for **International Banking Account Number (IBAN)**.

1. Select **Add** at the bottom of the flyout.

1. Back on the **Choose the types of content to protect** flyout, select **Save**.

1. Back on the **Info to protect page**, ensure the checkbox for **Detect when this content is shared in Microsoft 365** is selected, and the option for **With people outside my organization** is selected.

1. Select **Next**.

1. On the **Protection actions** page, review the default settings, then select **Next**.

1. On the **Customize access and override settings** page, select the checkbox for **Restrict access or encrypt the content in Microsoft 365 locations**, then select **Next**.

1. On the **Policy mode** page, select **Turn the policy on immediately**, then select **Next**.

1. On the **Review and finish** page review your settings then select **Submit**.

1. On the **New policy created** page select **Done**.

You've created a DLP policy that scans Teams content for credit card numbers and allows overrides with business justification.
