---
lab:
    title: 'Exercise 4 - Manage Sensitivity Labels in Microsoft Defender for Cloud Apps'
    module: 'Module 1 - Implement Information Protection'
---

# Lab 1 - Exercise 4 - Manage sensitivity labels

Joni Sherman, the System Administrator for Contoso Ltd., is implementing a sensitivity labeling plan to ensure that all employee documents in the HR department are appropriately labeled according to the company's information protection policies. Contoso Ltd. is based in Rednitzhembach, Germany, and aims to comply with internal data handling standards and regional regulations.

**Tasks**:

1. Enable support for sensitivity labels
1. Create sensitivity labels
1. Publish sensitivity labels
1. Apply sensitivity labels
1. Configure auto labeling

## Task 1 – Enable support for sensitivity labels

In this task, you'll enable co-authoring for sensitivity labels, which also enables sensitivity labels for files in SharePoint and OneDrive.

1. You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account and logged into Microsoft Purview and Joni Sherman.

1. Open **Microsoft Edge**, then navigate to `https://purview.microsoft.com`.

1. In the left navigation, select **Settings** > **Information Protection**.

1. On the **Information Protection settings** ensure you're on the **Co-authoring for files with sensitivity labels** tab.

1. Select the checkbox for **Turn on co-authoring for files with sensitivity labels**.

1. Select **Apply** at the bottom of the screen.

You have successfully enabled support for sensitivity labels for files in SharePoint and OneDrive.

## Task 2 – Create sensitivity labels

In this task, you'll create a sensitivity label for internal content and a sublabel for documents used by the HR department.

1. You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.

1. In **Microsoft Edge**, navigate to `https://purview.microsoft.com`.

1. In the Microsoft Purview portal, select **Solutions** from the left sidebar, then select **Information Protection**.

1. On the **Microsoft Information Protection** page, on the left sidebar, select **Sensitivity labels**.

1. On the **Sensitivity labels** page select **+ Create a label**.

1. The **New sensitivity label** configuration will start. On the **Provide basic details for this label**, enter:

    - **Name**: `Internal`
    - **Display name**: `Internal`
    - **Description for users**: `Internal sensitivity label.`
    - **Description for admins**: `Internal sensitivity label for Contoso.`

1. Select **Next**.

1. On the **Define the scope for this label** page, select **Items**, then select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.

1. Select **Next**.

1. On the **Choose protection settings for labeled items** page, select **Apply content marking**, then select **Next**.

1. On the **Content marking** page, turn on the **Content marking** toggle

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

1. On the **Sensitivity labels** page, find the newly created **Internal** sensitivity label. Select the vertical ellipsis (**...**) next to it, then select **+ Create sublabel** from the dropdown menu.

    ![Screenshot showing the Action menu to create a sublabel for a sensitivity label.](../Media/create-sublabel-button.png)

1. The **New sensitivity label** wizard will start. On the **Provide basic details for this label** page enter:

   - **Name**: `Employee data (HR)`
   - **Display name**: `Employee data (HR)`
   - **Description for users**: `This HR label is the default label for all specified documents in the HR Department.`
   - **Description for admins**: `This label is created in consultation with Ms. Jones (Head of HR department). Contact her when you want to change settings of the label.`

1. Select **Next**.

1. On the **Define the scope for this label** page, select **Items**, then select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.

1. Select **Next**.

1. On the **Choose protection settings for labeled items** page, select the **Control access** option, then select **Next**.

1. On the **Access control** page, select **Configure access control settings**.

1. Configure the encryption settings with these options:

   - **Assign permissions now or let users decide?**: Assign permissions now
   - **User access to content expires**: Never
   - **Allow offline access**: Only for a number of days
   - **Users have offline access to the content for this many days**: 15
   - Select the **Assign permissions** link. On the **Assign permissions** flyout panel, select the **+ Add any authenticated users**, then select **Save** to apply this setting.

1. On the **Access control** page, select **Next**.

1. On the **Auto-labeling for files and emails** page, select **Next**.

1. On the **Define protection settings for groups and sites** page, select **Next**.

1. On the **Review your settings and finish** page, select **Create label**.

1. On the **Your sensitivity label was created** page, select **Don't create a policy yet**, then select **Done**.

You have successfully created a sensitivity label for your organization's internal policies with content marking and a sublabel for the Human Resources (HR) department with protection settings.

## Task 3 – Publish sensitivity labels

You will now publish the Internal and HR sensitivity label so that the published sensitivity labels will be available for the HR users to apply to their HR documents.

1. You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft Purview as **Joni Sherman**.

1. In **Microsoft Edge**, the Microsoft Purview portal tab should still be open. If not, navigate to **`https://purview.microsoft.com`** > **Solutions** > **Information Protection** > **Sensitivity labels**.

1. On the **Sensitivity labels** page select **Publish labels**.

1. The publish sensitivity labels configuration will start.

1. On the **Choose sensitivity labels to publish** page, select the **Choose sensitivity labels to publish** link.

1. On the **Sensitivity labels to publish** flyout panel, select the **Internal** and **Internal/Employee Data (HR)** checkboxes, then select **Add** at the bottom of the flyout page.

1. Back on the **Choose sensitivity labels to publish** page, select **Next**.

1. On the **Assign admin units** page, select **Next**

1. On the **Publish to users and groups** page, select **Next**.

1. On the **Policy settings** page, select **Next**.

1. On the **Default settings for documents** select **Next**.

1. On the **Default settings for emails** select **Next**.

1. On the **Default settings for meetings and calendar events** select **Next**.

1. On the **Default settings for Power BI Content** select **Next**.

1. On the **Name your policy** page, enter:

   - **Name**: `Internal HR employee data`
   - **Enter a description for your sensitivity label policy**: `This HR label is to be applied to internal HR employee data.`

1. Select **Next**.

1. On the **Review and finish** page, select **Submit**.

1. On the **New policy created** page, select **Done** to finish publishing your label policy.

You have successfully published the Internal and HR sensitivity labels. Note that it can take up to 24 hours for changes to replicate to all users and services.

## Task 4 – Apply sensitivity labels

In this task, you'll apply a sensitivity label to a document in Word to simulate how users can manually label content. This helps ensure that HR documents are protected according to the label policy you published earlier.

1. You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman** `JoniS@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Joni's password was set in a previous exercise.

1. In **Microsoft Edge**, open a new Word document by selecting the meatball menu in the top left and selecting **Word**.

    ![Screenshot showing where to select Word from the meatball menu.](../Media/meatball-menu-word.png)

1. Select **Blank document** to create a new document.

1. On the **Your privacy option** dialogue, select **Close**.

1. Enter this text in the new blank document:

   `Important HR employee document.`

1. Select **Sensitivity** from the navigation ribbon and select **Internal** > **Employee Data (HR)** to apply the newly created sensitivity label to this document.

    ![Screenshot showing the sensitivity label button in Word.](../Media/word_label.png)

    >**Note:** It can take 24-48 hours for newly published sensitivity labels to be available for application. If the newly created sensitivity labels aren't available, you can use **Confidential** > **All Employees** for this exercise.

1. In the upper left of the document, select **Document** to rename this file, and rename it to **`HR Document`**. Press enter to apply this name change.

    ![Screenshot showing where to rename a file in Word on the web.](../Media/rename-web-word-file.png)

You successfully applied the HR sensitivity label to a Word document saved in OneDrive.

## Task 5 – Configure auto labeling

In this task, you'll create a sensitivity label for financial data and configure it to apply automatically to content containing specific financial identifiers, such as credit card numbers and bank routing information.

1. You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.

1. In **Microsoft Edge**, navigate to `https://purview.microsoft.com` and log into the Microsoft Purview portal as **Joni Sherman**.

1. In the Microsoft Purview portal, select **Solutions** > **Information protection** > **Sensitivity labels**.

1. On the **Sensitivity labels** page, find the **Internal** sensitivity label. Select the vertical ellipsis (**...**), then select **+ Create sublabel** from the dropdown menu.

1. On the **Provide basic details for this label** page, enter:

   |Details|Text|
   |---|---|
   |**Name**|`Financial Data`|
   |**Display name**|`Financial Data`|
   |**Description for users**|`This content contains financial data that must be labeled and protected.`|
   |**Description for admins**|`This label is used for content that includes sensitive financial identifiers.`|

1. Select **Next**.

1. On the **Define the scope for this label** page, select **Items**, then select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.

1. Select **Next**.

1. On the **Choose protection settings for labeled items** page, select **Next**.

1. On the **Auto-labeling for files and emails** page, set the **Auto-labeling for files and emails** to enabled.

1. In the **Detect content that matches these conditions** section, select **+ Add condition** > **Content contains**.

1. In **Content contains** section select the **Add** > **Sensitive info types**.

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

You have successfully created a sensitivity label for financial data and configured an auto-labeling policy to detect and label content that contains sensitive financial information.

## Task 6 – Create and publish a DKE label for highly confidential content

In this task, you'll create a sublabel under the built-in Highly Confidential label. This sublabel will use Double Key Encryption (DKE) and dynamic watermarking to protect sensitive content accessed only by Legal. You'll also configure a label policy that requires justification for downgrading the label.

1. You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.

1. In **Microsoft Edge**, navigate to `https://purview.microsoft.com` and log into the Microsoft Purview portal as **Joni Sherman**.

1. In the Microsoft Purview portal, select **Solutions** > **Information protection** > **Sensitivity labels**.

1. On the **Sensitivity labels** page, find the **Highly Confidential** sensitivity label. Select the vertical ellipsis (**...**), then select **+ Create sublabel** from the dropdown menu.

1. On the **Provide basic details for this label** page, enter:

   |Details|Text|
   |---|---|
   |**Name**|`Highly Confidential - Legal`|
   |**Display name**|`Highly Confidential - Legal`|
   |**Description for users**|`Use this label for highly sensitive content that must be encrypted using Double Key Encryption.`|
   |**Description for admins**|`Label configured with DKE and dynamic watermarking for highly sensitive content.`|

1. Select **Next**.

1. On the **Define the scope for this label** page, select **Items**, then select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.

1. On the **Choose protection settings for the types of items you selected** page, select **Control access**, then select **Next**.

1. On the **Access control** page, select **Configure access control settings**.

1. Configure the encryption settings with these options:

   - **Assign permissions now or let users decide?**: Assign permissions now
   - **User access to content expires**: A number of days after label is applied
   - **Access expires this many days after the label is applied**: 5
   - **Allow offline access**: Only for a number of days
   - **Users have offline access to the content for this many days**: Never
   - Select the **Assign permissions** link. On the **Assign permissions** flyout panel, select the **+ Add users or groups**.
   - On the **Add users or groups** or groups flyout page, search for and select `Legal Team` and `Joni Sherman`, and select **Add**.
   - On the **Assign permissions** page, select **Save**.

1. Back on the **Access control** page, select the checkbox for **Use dynamic watermarking**, then select **Customize text (optional)**.

1. On the **Add custom text to watermark (optional)** page, Enter `Confidential`, then select the links for **UPN** and **Timestamp**.

1. Select **Save** at the bottom of the flyout page.

1. Back on the **Access control** page, select the checkbox for **Use Double Key Encryption**, and enter `https://testingdke1.azurewebsites.net/Test` as the the URL for the Double Key Encryption service.

1. Select **Next**.

1. On the **Auto-labeling for files and emails** page, select **Next**.

1. On the **Define protection settings for groups and sites** page, select **Next**.

1. On the **Review your settings and finish** page, select **Create label**.

1. On the **Your sensitivity label was created** page, select **Publish label to users' apps**, then select **Done**.

1. On the **Publish label** flyout page, select **Create new label policy**.

1. On the **Choose sensitivity labels to publish** page, select **Choose sensitivity labels to publish** and add the **Highly Confidential** label and **Highly Confidential - DKE** sublabel, then select **Add**.

1. Select **Next**.

1. On the **Assign admin units** page, select **Next**.

1. On the **Publish to users and groups** page, leave the default selected, then select **Next**.

1. On the **Policy settings** page, select the checkbox for **Users must provide a justification to remove a label or lower its classification**, then select **Next**.

1. On the **Default settings for documents​** page, select **Next**.

1. On the **Default settings for emails​** page, select **Next**.

1. On the **Default settings for meetings and calendar events​** page, select **Next**.

1. On the **Default settings for Fabric and Power BI content​** page, select **Next**.

1. On the **Name your policy** page, enter:

   - **Name**: `Highly Confidential - Legal`
   - **Description**: `Enables manual use of the DKE label for highly confidential content accessible by Legal.`

1. Select **Next**.

1. On the **Review and finish** page, select **Submit**.

1. On the **New policy created** page, select **Done**.

You have successfully created and published a sublabel using Double Key Encryption with dynamic watermarking. This label provides strong protection for highly confidential content and enforces restricted access and justification for classification changes.

## Task 7