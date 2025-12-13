---
lab:
    title: 'Exercise 1 - Implement Insider Risk Management'
    module: 'Module 4 - Implement Insider Risk Management'
---

## WWL Tenants - Terms of use

If you are being provided with a tenant as a part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training.

Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and are not eligible for extension.

Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time.

# Lab 4 - Exercise 1 - Implement Insider Risk Management

You are Joni Sherman, the Information Security Administrator for Contoso Ltd. Your role involves ensuring regulatory compliance and protecting sensitive information within the organization. Recently, Contoso Ltd. has noticed unusual browsing activities that could potentially expose sensitive data. To proactively address this insider risk, you will implement Microsoft Purview Insider Risk Management, focusing on identifying, analyzing, and responding to potential insider threats effectively.

**Tasks**:

1. Configure insider risk indicators
1. Create an insider risk policy

## Task 1 – Configure insider risk indicators

Before you create an insider risk policy, you'll turn on the indicators needed for detection. These indicators define the types of risky activity the system will look for.

1. Return to the Microsoft Edge window where you're signed in as Joni Sherman. Refresh the tab to ensure the new permissions are active.

1. Select **Settings** > **Insider risk management**.

1. Select the tab on the left for **Policy indicators**.

1. On the **Policy indicators** page, expand and select **Select all** to enable all indicators in these categories:

   - Office indicators
   - Cumulative exfiltration detection

1. Select **Save** at the bottom of the page.

You've enabled key policy indicators so the system can detect sensitive actions like file exfiltration or risky Office activity.

## Task 2 – Create an insider risk policy

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
