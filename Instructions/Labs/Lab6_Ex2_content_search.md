---
lab:
    title: 'Exercise 2 - Perform a content search'
    module: 'Module 6 - Audit and search activity in Microsoft Purview'
---

## WWL Tenants - Terms of use

If you are being provided with a tenant as a part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training.

Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and are not eligible for extension.

Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time.

# Lab 6 - Exercise 2 - Perform a content search

You are Joni Sherman, an Information Security Administrator at Contoso Ltd. The organization has received an alert that sensitive financial data may have been exposed. You've been asked to use Microsoft Purview to search for content containing key financial terms across Microsoft 365 services. Your goal is to determine whether any sensitive content was shared inappropriately and support the investigation.

**Tasks**:

1. Assign eDiscovery permissions
1. Search for content using sensitive financial terms

## Task 1 – Assign eDiscovery permissions

In this task, you'll assign eDiscovery permissions to Joni Sherman so she can perform a content search in Microsoft Purview.

1. Sign into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account.

1. If you're signed in as Joni, sign out and close all browser windows.

1. In **Microsoft Edge**, navigate to **`https://purview.microsoft.com`** and log into the Microsoft Purview portal as **MOD Administrator** `admin@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.

1. In the left sidebar, select **Settings** > **Roles and Scopes** > **Role groups**.

1. On the **Role groups for Microsoft Purview solutions** page, search for `eDiscovery`, then select **eDiscovery Manager**.

1. On the **eDiscovery Manager** flyout panel, select **Edit**.

1. On the **Manage eDiscovery Manager** page, select **Choose users**.

1. On the **Choose users** flyout page, search for `Joni`, then select the checkbox for **Joni Sherman**. Select the **Select** button at the bottom of the panel.

1. Back on the **Manage eDiscovery Manager** page, select **Next**.

1. On the **Manage eDiscovery Administrator** page, select **Next**.

1. On the **Review the role group and finish** page, select **Save**.

1. On the **You successfully updated the role group** page, select **Done**.

1. Sign out of the MOD Administrator account by selecting the **MA** icon on the top right of the window, then select **Sign out**.

You've assigned eDiscovery permissions to Joni Sherman, enabling her to search for sensitive content as part of the investigation.

## Task 2 – Search for content using sensitive financial terms

1. In Microsoft Edge, navigate to `https://purview.microsoft.com` and sign in to the Microsoft Purview portal as **Joni Sherman** `JoniS@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Joni's password was set in a previous exercise.

1. In Microsoft Purview, navigate to **Solutions** > **eDiscovery**.

1. On the **Cases** page, select the dropdown next to **Create case**, then select **Create search**.

   ![Screenshot showing where to create a search in eDiscovery.](../Media/ediscovery-create-search.png)

1. On the **Enter details to get started** dialogue, enter:

   - **Case name**: `Financial Data Exposure Review`
   - **Search name**: `Financial Data Leak Investigation`
   - **Case description**: `Case opened to support security investigation efforts by identifying potential exposure of sensitive financial terms in Microsoft 365 content.`
   - **Search description**: `Search targets common high-risk financial keywords to support data security monitoring and policy validation.`

1. Select **Create** to create the search.

1. On the **Financial Data Leak Investigation** page, under **Data sources** select **+** (plus sign) > **Add data sources**.

   ![Screenshot showing add data sources in Content Search.](../Media/content-search-data-sources.png)

1. On the **Search for sources** flyout, select the **Finance team** group, then select **Save and close**.

1. In the **Condition builder** pane, add the keywords `bank account` and `credit card`, then select **Run query**.

   ![Screenshot showing the condition builder in COntent Search.](../Media/content-search-query-builder.png)

1. In the **Choose search results** flyout under **Statistics**, select the checkboxes for **Include categories** and **Include query keywords report**, then select **Run Query**.

1. Review the results of the search by:

   - Select the **Statistics** tab to view a summary of search metrics.
   - Select the **Sample** tab to preview matched content.

You've performed a keyword-based content search to help identify whether sensitive financial data was shared inappropriately. These results support security investigations and help guide risk response.
