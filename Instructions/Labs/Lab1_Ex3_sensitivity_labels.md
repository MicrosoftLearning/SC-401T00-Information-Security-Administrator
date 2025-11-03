---
lab:
    title: 'Exercise 3 - Create and manage sensitivity labels'
    module: 'Module 1 - Implement Information Protection'
---

# Lab 1 - Exercise 3 - Create and manage sensitivity labels

Joni Sherman, an Information Security Administrator at Contoso Ltd., is deploying a modern sensitivity labeling framework to strengthen data protection across the organization. She'll create and publish sensitivity label groups and labels to classify and protect content, including encryption, auto-labeling, and Double Key Encryption (DKE). Joni will also integrate Microsoft Purview with Microsoft Defender for Cloud Apps to extend data protection controls to files stored in cloud locations.

**Tasks**:

1. Enable support for sensitivity labels
1. Migrate to the modern label scheme
1. Create a label group
1. Create a child label
1. Publish labels
1. Configure auto-labeling
1. Create and publish a DKE label for confidential content
1. Enable Microsoft Purview integration in Defender for Cloud Apps
1. Create a file policy to label externally shared files

## Task 1 – Enable support for sensitivity labels

In this task, you'll enable co-authoring for sensitivity labels, which also enables sensitivity labels for files in SharePoint and OneDrive.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account and logged into Microsoft Purview as Joni Sherman.

1. Open **Microsoft Edge**, then navigate to `https://purview.microsoft.com`.

1. In the left navigation, select **Settings** > **Information Protection**.

1. On the **Information Protection settings** page, ensure you're on the **Co-authoring for files with sensitivity labels** tab.

1. Select the checkbox for **Turn on co-authoring for files with sensitivity labels**.

1. Select **Apply** at the bottom of the screen.

You have successfully enabled support for sensitivity labels for files in SharePoint and OneDrive.

## Task 2 – Migrate to the modern label scheme

With sensitivity label support enabled, you'll confirm that the tenant uses the modern label scheme. If it still uses the classic scheme, you'll migrate to the modern one to ensure new labels and policies use the latest configuration model.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account and logged into Microsoft Purview as Joni Sherman.

1. In the left navigation, select **Information Protection** > **Sensitivity labels**.

1. On the **Sensitivity labels** page, review the information box for **Migrate to the modern label scheme**, then select **Get started**.

1. In the **Migrate to the modern label scheme** flyout, review the summary to understand how existing labels and policies will be affected.

1. At the bottom of the flyout, select **Migrate**.

1. In the **Confirm migration to modern label scheme** dialog box, select **Confirm migration**.

    > [!Note] **Note**: The migration process might take a few minutes to complete.

You've successfully migrated your tenant to the modern sensitivity label scheme. New labels and policies you create will now use the modern configuration experience.

## Task 3 – Create a label group

In this task, you'll create a label group to organize internal sensitivity labels. Label groups act as containers for related labels, like department or business unit classifications.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin** account.

1. In **Microsoft Edge**, navigate to `https://purview.microsoft.com`.

1. In the Microsoft Purview portal, select **Solutions** from the left sidebar, then select **Information Protection**.

1. On the **Microsoft Information Protection** page, on the left sidebar, select **Sensitivity labels**.

1. On the **Sensitivity labels** page select **+ Create** > **Label group**.

1. The **New label group** configuration will start. On the **Provide basic details for this label group**, enter:

    - **Name**: `Internal`
    - **Display name**: `Internal`
    - **Description for users**: `Internal sensitivity label.`
    - **Description for admins**: `Internal sensitivity label group for Contoso.`

1. Select **Next**.

1. On the **Review your settings and finish** page, select **Create label group**.

1. On the **Your label group was created successfully** page, select **Don't create a label yet**, then select **Done**.

You've created a label group for internal use. This group helps you manage related labels for specific departments or data categories.

## Task 4 – Create a child label

Now that you've created a label group, you'll add a child label for HR-related content. This label enforces encryption and content markings to protect HR data from unauthorized access.

1. On the **Sensitivity labels** page, find the **Internal** sensitivity label group. Select the vertical ellipsis (**...**) next to it, then select **+ Create label in group** from the dropdown menu.

    ![Screenshot showing the Action menu to create a label in group for a sensitivity label.](../Media/create-label-in-group.png)

1. The **New sensitivity label** wizard will start. On the **Provide basic details for this label** page enter:

   - **Name**: `Employee data (HR)`
   - **Display name**: `Employee data (HR)`
   - **Description for users**: `This HR label is the default label for all specified documents in the HR Department.`
   - **Description for admins**: `This label is created in consultation with Ms. Jones (Head of HR department). Contact her if you need to change the label settings.`

1. Select **Next**.

1. On the **Define the scope for this label** page, select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.

1. Select **Next**.

1. On the **Choose protection settings for labeled items** page, select the **Control access** and **Apply content marking** options, then select **Next**.

1. On the **Access control** page, select **Configure access control settings**.

1. Configure the encryption settings with these options:

   - **Assign permissions now or let users decide?**: Assign permissions now
   - **User access to content expires**: Never
   - **Allow offline access**: Only for a number of days
   - **Users have offline access to the content for this many days**: 15
   - Select the **Assign permissions** link. On the **Assign permissions** flyout panel, select **+ Add any authenticated users**, then select **Save** to apply this setting.

1. On the **Access control** page, select **Next**.

1. On the **Content marking** page, select the toggle to enable **Content marking**.

1. For each of the following marking types, select the checkbox, then select the edit icon to enter the text:

   |Marking type|Text|
   |:---|:---|
   |Add a watermark|`INTERNAL USE ONLY`|
   |Add a header|`Internal Document`|
   |Add a footer|`Contoso Confidential`|

1. Select **Next**.

1. On the **Auto-labeling for files and emails** page, select **Next**.

1. On the **Define protection settings for groups and sites** page, select **Next**.

1. On the **Review your settings and finish** page, select **Create label**.

1. On the **Your sensitivity label was created** page, select **Don't create a policy yet**, then select **Done**.

You've created a child label within the Internal label group. The label applies encryption and content markings to HR documents, making sensitive data easy to identify and protected by policy.

## Task 5 – Publish labels

Next, you'll publish the HR label from the Internal label group so users in the HR department can apply it to their documents.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-cl1\admin** account, and you should be logged into Microsoft Purview as **Joni Sherman**.

1. In **Microsoft Edge**, the Microsoft Purview portal tab should still be open. If not, navigate to **`https://purview.microsoft.com`** > **Solutions** > **Information Protection** > **Sensitivity labels**.

1. On the **Sensitivity labels** page select **Publish labels**.

1. The publish sensitivity labels configuration will start.

1. On the **Choose sensitivity labels to publish** page, select the **Choose sensitivity labels to publish** link.

1. On the **Sensitivity labels to publish** flyout panel, select the  **Internal/Employee data (HR)** checkbox, then select **Add** at the bottom of the flyout page.

1. Back on the **Choose sensitivity labels to publish** page, select **Next**.

1. On the **Assign admin units** page, select **Next**

1. On the **Publish to users and groups** page, select **Next**.

1. On the **Policy settings** page, select **Next**.

1. On the **Default settings for documents** select **Next**.

1. On the **Default settings for emails** select **Next**.

1. On the **Default settings for meetings and calendar events** select **Next**.

1. On the **Default settings for Fabric and Power BI Content** page, select **Next**.

1. On the **Name your policy** page, enter:

   - **Name**: `Internal HR employee data`

   - **Enter a description for your sensitivity label policy**: `This HR label is to be applied to internal HR employee data.`

1. Select **Next**.

1. On the **Review and finish** page, select **Submit**.

1. On the **New policy created** page, select **Done** to finish publishing your label policy.

You've published the Internal label group and its HR label so users can apply them to HR documents. It might take up to 24 hours for the policy to propagate across services.

## Task 6 – Configure auto-labeling

You'll now create a child label for financial data and configure it to apply automatically to content containing financial identifiers such as credit card or bank routing numbers.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-cl1\admin** account.

1. In **Microsoft Edge**, navigate to `https://purview.microsoft.com` and log into the Microsoft Purview portal as **Joni Sherman**.

1. In the Microsoft Purview portal, select **Solutions** > **Information protection** > **Sensitivity labels**.

1. On the **Sensitivity labels** page, find the **Internal** sensitivity label. Select the vertical ellipsis (**...**), then select **+ Create label in group** from the dropdown menu.

1. On the **Provide basic details for this label** page, enter:

   |Details|Text|
   |---|---|
   |**Name**|`Financial Data`|
   |**Display name**|`Financial Data`|
   |**Description for users**|`This content contains financial data that must be labeled and protected.`|
   |**Description for admins**|`This label is used for content that includes sensitive financial identifiers.`|

1. Select **Next**.

1. On the **Define the scope for this label** page, select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.

1. Select **Next**.

1. On the **Choose protection settings for labeled items** page, select **Next**.

1. On the **Auto-labeling for files and emails** page, set the **Auto-labeling for files and emails** to enabled.

1. In the **Detect content that matches these conditions** section, select **+ Add condition** > **Content contains**.

1. In **Content contains** section, select the **Add** > **Sensitive info types**.

1. In the **Sensitive info types** flyout page, search for and select these sensitive info types:

   - `Credit Card Number`
   - `ABA Routing Number`
   - `SWIFT Code`

1. Select **Add**.

1. Back on the **Auto-labeling for files and emails** page, select **Next**.

1. On the **Define protection settings for groups and sites** page, select **Next**.

1. On the **Review your settings and finish** page, select **Create label**.

1. On the **Your sensitivity label was created** page, select **Automatically apply label to sensitive content**, then select **Done**.

1. On the **Create auto-labeling policy** flyout page, select **Review policy**.

1. On the **Name your auto-labeling policy** page, leave the default, then select **Next**.

1. On the **Choose a label to auto-apply** page, review to ensure the _Internal/Financial Data_ label is selected, then select **Next**.

1. On the **Assign admin units** page, select **Next**.

1. On the **Choose locations where you want to apply the label** page, select the options for:

   - Exchange email
   - SharePoint sites
   - OneDrive accounts

1. Select **Next**.

1. On the **Set up common or advanced rules** page, leave the default **Common rules** selected, then select **Next**.

1. On the **Define rules for content in all locations** page, expand the rules for _Financial Data rule_ to ensure the expected rules are defined, then select **Next**.

1. On the **Additional settings for email** page, select **Next**.

1. On the **Decide if you want to test out the policy now or later** page, select **Run policy in simulation mode**, and select the checkbox for **Automatically turn on policy if not modified after 7 days in simulation.**

1. Select **Next**.

1. On the **Review and finish** page, select **Create policy**.

1. On the **Your auto-labeling policy was created** page, select **Done**.

You've created a child label for financial data and configured an auto-labeling policy that detects and labels content containing financial information.

## Task 7 – Create and publish a DKE label for confidential content

Next, you'll create a child label in the Internal group that uses Double Key Encryption (DKE) and dynamic watermarking to protect confidential legal content.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-cl1\admin** account.

1. In **Microsoft Edge**, navigate to `https://purview.microsoft.com` and log into the Microsoft Purview portal as **Joni Sherman**.

1. In the Microsoft Purview portal, select **Solutions** > **Information Protection** > **Sensitivity labels**.

1. On the **Sensitivity labels** page, find the **Internal** sensitivity label group. Select the vertical ellipsis (**...**), then select **+ Create label in group** from the dropdown menu.

1. On the **Provide basic details for this label** page, enter:

   |Details|Text|
   |---|---|
   |**Name**|`Confidential Legal`|
   |**Display name**|`Confidential Legal`|
   |**Description for users**|`Use this label for highly sensitive content that must be encrypted using Double Key Encryption.`|
   |**Description for admins**|`Label configured with DKE and dynamic watermarking for highly sensitive content.`|

1. Select **Next**.

1. On the **Define the scope for this label** page, select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.

1. On the **Choose protection settings for the types of items you selected** page, select **Control access**, then select **Next**.

1. On the **Access control** page, select **Configure access control settings**.

1. Configure the encryption settings with these options:

   - **Assign permissions now or let users decide?**: Assign permissions now

   - **User access to content expires**: A number of days after label is applied

   - **Access expires this many days after the label is applied**: 5

   - **Allow offline access**: Never

   - Select the **Assign permissions** link. On the **Assign permissions** flyout panel, select the **+ Add users or groups**.

   - On the **Add users or groups** flyout page, search for and select `Legal Team` and `Joni Sherman`, and select **Add**.

   - On the **Assign permissions** page, select **Save**.

1. Back on the **Access control** page, select the checkbox for **Use dynamic watermarking**, then select **Customize text (optional)**.

1. On the **Add custom text to watermark (optional)** page, enter `Confidential`, then select **UPN** and **Timestamp**.

1. Select **Save** at the bottom of the flyout page.

1. Back on the **Access control** page, select the checkbox for **Use Double Key Encryption**, and enter `https://testingdke1.azurewebsites.net/Test` as the URL for the Double Key Encryption service.

1. Select **Next**.

1. On the **Auto-labeling for files and emails** page, select **Next**.

1. On the **Define protection settings for groups and sites** page, select **Next**.

1. On the **Review your settings and finish** page, select **Create label**.

1. On the **Your sensitivity label was created** page, select **Publish label to users' apps**, then select **Done**.

1. On the **Publish label** flyout page, select **Create new label policy**.

1. On the **Choose sensitivity labels to publish** page, select **Choose sensitivity labels to publish** and add the **Internal/Confidential Legal** label, then select **Add**.

1. Select **Next**.

1. On the **Assign admin units** page, select **Next**.

1. On the **Publish to users and groups** page, leave the default selected, then select **Next**.

1. On the **Policy settings** page, select the checkbox for **Users must provide a justification to remove a label or lower its classification**, then select **Next**.

1. On the **Default settings for documents​** page, select **Next**.

1. On the **Default settings for emails​** page, select **Next**.

1. On the **Default settings for meetings and calendar events​** page, select **Next**.

1. On the **Default settings for Fabric and Power BI content​** page, select **Next**.

1. On the **Name your policy** page, enter:

   - **Name**: `Confidential Legal`

   - **Description**: `Enables manual use of the DKE label for confidential content accessible by Legal.`

1. Select **Next**.

1. On the **Review and finish** page, select **Submit**.

1. On the **New policy created** page, select **Done**.

You've created and published a child label using Double Key Encryption and dynamic watermarking. This label restricts access to authorized users and enforces justification for downgrading classifications.

## Task 8 – Enable Microsoft Purview integration in Defender for Cloud Apps

With your sensitivity labels created and published, you'll now integrate Microsoft Purview with Microsoft Defender for Cloud Apps. This integration allows Defender to scan files for sensitivity labels and apply file monitoring.

1. You should still be logged into Client 1 VM (SC-401-CL1) as the **SC-401-CL1\admin**, and you should still be logged in as Joni Sherman.

1. Open **Microsoft Edge**, then go to **Microsoft Defender** by navigating to `https://security.microsoft.com`.

1. In the left navigation, select **Settings**, then select **Cloud Apps**.

1. Under the **Information Protection** section in the left pane, select **Microsoft Information Protection**.

1. On the **Microsoft Information Protection** page, select both checkboxes available on the page.

    ![Screenshot showing both checkboxes enabled for Information Protection in the Defender portal.](../Media/defender-information-protection-settings.png)

   - **Automatically scan new files for Microsoft Information Protection sensitivity labels and content inspection warnings**

      Enables Defender for Cloud Apps to automatically scan new or modified files for sensitivity labels and content inspection warnings from Microsoft Purview.

   - **Only scan files for Microsoft Information Protection sensitivity labels and content inspection warnings from this tenant**

      Limits scanning to labels and warnings created in your own organization. Labels applied by external tenants will be ignored.

1. Select **Save** to apply the settings.

1. Under the **Information Protection** section in the left pane, select **Files**.

1. On the **Files** page, select **Enable file monitoring**.

1. Select **Save** to apply the settings.

You've enabled Microsoft Purview integration in Defender for Cloud Apps. Defender can now detect sensitivity labels and monitor files for policy evaluation and governance actions.

<!---

NOTE - Reworking task 8 due to tenant issue

## Task 8 – Create a file policy to auto-label externally shared files

Now that label scanning is enabled, you'll create a file policy that applies the **Highly Confidential - Project - Falcon** sensitivity label to files in the Mark 8 Project folders that are shared outside your organization. This policy is categorized as DLP because it protects sensitive data from unintended exposure.

1. In **Microsoft Defender**, navigate to **Cloud apps** > **Policies** > **Policy management**.

1. Select the **Information protection** tab, then select **Create policy** > **File policy**.

    ![Screenshot showing where to navigate to create a file policy in Microsoft Defender.](../Media/file-policy-defender.png)

1. On the **Create file policy** page, configure:

   - **Policy name**: `Auto-label external sharing for Project Falcon files`

   - **Policy severity**: **High**

   - **Category**: **DLP**

   - **Apply to**: **Selected folders**

      - Select **Add folder(s)**, then search for `Project` in the **File name** field.

      - Select the checkbox for the **Mark 8 Project Team Notebook** and **Mark 8 Project team** SharePoint folders.

      - Select **Done** to close the **Select a folder** window.

   - In the **Files matching all of the following section**:

      - For the first filter, configure the dropdowns to: **Access level equals external**

      - For the second filter, configure the dropdowns to: **Last modified after (date)** and use today's date

          ![Screenshot showing the filter settings in Defender.](../Media/configure-file-policy-filter.png)

   - Under **Governance actions**, expand **Microsoft OneDrive for Business**:

      - Select the checkbox for **Apply sensitivity label**

      - In the dropdown select **Highly Confidential-Project - Falcon**

   - Repeat the same process for **Microsoft SharePoint Online**

      - Select the checkbox for **Apply sensitivity label**

      - Select **Highly Confidential-Project - Falcon** from the dropdown

1. Select **Create** to finish creating the file policy.

You've created a file policy that applies a highly confidential sensitivity label to externally shared files located in the Mark 8 Project folders in SharePoint and OneDrive. Once a matching file is detected, Defender for Cloud Apps will apply the label automatically.
-->

## Task 9 – Create a file policy to label externally shared files

Finally, you'll create a file policy that automatically applies a sensitivity label to files shared externally. This ensures sensitive content remains protected even when shared outside the organization.

1. In **Microsoft Defender**, navigate to **Cloud apps** > **Policies** > **Policy management**.

1. Select the **Information protection** tab, then select **Create policy** > **File policy**.

    ![Screenshot showing where to navigate to create a file policy in Microsoft Defender.](../Media/file-policy-defender.png)

1. On the **Create file policy** page, configure:

   - **Policy name**: `Auto-label externally shared files`

   - **Policy severity**: **High**

   - **Category**: **DLP**

   - In the **Files matching all of the following section**:

      - For the first filter, configure the dropdowns to: **Access level equals external**

      - For the second filter, configure the dropdowns to: **Last modified after (date)** and use today's date

          ![Screenshot showing the filter settings in Defender.](../Media/configure-file-policy-filter.png)

   - Under **Governance actions**, expand **Microsoft OneDrive for Business**:

      - Select the checkbox for **Apply sensitivity label**

      - In the dropdown select **Highly Confidential-Specified People**

   - Repeat the same process for **Microsoft SharePoint Online**

      - Select the checkbox for **Apply sensitivity label**

      - Select **Highly Confidential-Specified People** from the dropdown

1. Select **Create** to finish creating the file policy.

You've created a file policy that applies sensitivity labels to externally shared files. This policy extends your information protection strategy to cloud-stored content.
