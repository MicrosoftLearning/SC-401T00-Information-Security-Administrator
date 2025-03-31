---
lab:
    title: 'Exercise 1 - Search the Audit log'
    module: 'Module 6 - Audit and search activity in Microsoft purview'
---

## WWL Tenants - Terms of use

If you are being provided with a tenant as a part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training.

Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and are not eligible for extension.

Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time.

# Lab 6 - Exercise 1 - Search the Audit log

scenario

**Tasks**:

1. In Microsoft Edge, navigate to `https://purview.microsoft.com` and sign in to the Microsoft Purview portal as **Joni Sherman** `JoniS@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Joni's password was set in a previous exercise.

1. In Microsoft Purview, navigate to **Solutions** > **Audit**.

1. On the **Search** page, configure your search:

   - **Date and time range (UTC)**:

     - **Start date**: 3 days ago
     - **End date**: Today

   - **Activities – friendly names**: Search for `DLP` and select the following activities under **Information protection and DLP activities**:

     - Created DLP rule
     - Updated DLP rule
     - Deleted DLP rule
     - Created DLP policy
     - Updated DLP policy
     - Deleted DLP policy

   ![Screenshot showing the DLP activities to select in Audit.](../Media/audit-dlp-search.png)

   - **Search name**: `DLP Policy Activity`

1. Select **Search**.

1. It may take several minutes for the search to complete. While Audit processes your search, refresh the page to check the **Job status**, **Progress (%)**, and **Search time**.

1. Once complete, select **DLP Policy Activity** to view the results.

1. Select individual results in the list to review detailed information about each activity.

## Task 2 

1. In Microsoft Purview, navigate to **Solutions** > **Audit**.

1. On the **Search** page, select the **DLP Policy Activity** search you created in the previous task.

1. Select **Export** at the top of the page.

1. In the confirmation dialog, select **OK** to start the export.

1. When the export completes, select the **Download file** link in the green **Your export is complete**. banner.

> **Note**: Audit export files are saved in CSV format and can be opened in any text editor or spreadsheet application. For easier review and filtering, many organizations use Excel or another spreadsheet tool. In this lab, you can open the CSV in Notepad to confirm the export completed successfully.

## Task 3 

1. In Microsoft Purview, navigate to **Solutions** > **Audit**.

1. Select **Policies** from the left sidebar.

1. On the **Policies** page select **New audit retention policy**

1. On the **New audit retention policy** panel, enter:

   - **Policy name**: `Retain DLP Audit Logs`
   - **Description**: `Retains audit logs for DLP activities across Exchange, SharePoint, and endpoints to support investigation and compliance.`
   - **Users**: Leave blank to apply to all users
   - **Record Type**:
      - ComplianceDLPEndpoint
      - ComplianceDLPExchange
      - ComplianceDLPExchangeClassification
      - ComplianceDLPSharePoint
      - ComplianceDLPSharePointClassification
   - Duration: **1 year**

1. Select **Save** to create the audit retention policy.

