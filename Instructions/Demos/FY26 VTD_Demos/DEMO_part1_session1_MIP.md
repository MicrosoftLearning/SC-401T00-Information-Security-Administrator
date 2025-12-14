# Session 1 - Demo 1 - Create and manage sensitivity labels

In this demo, you’ll see how an administrator organizes and publishes sensitivity labels to protect sensitive data. The demo shows how to create a label group, configure a sensitivity label that enforces encryption, and publish the label so it’s available in user apps.

**Tasks**:

1. Create a label group
1. Create and publish a child label

## Task 1 – Create a label group

In this task, you'll create a label group that acts as a container for related sensitivity labels.

   > **Trainer note**:
   >
   > - Briefly explain that label groups help organize labels at scale
   > - Don't spend time on naming conventions or hierarchy strategy
   >
   > **Suggested talk track**:
   >
   > _Label groups are just organizational containers. They don't apply protection by themselves, but they make labels easier to manage as environments grow_

### Steps

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

You've created a label group for internal use.

## Task 2 – Create and publish a child label

Next, you'll create a child label within the group and apply basic protection.

1. On the **Sensitivity labels** page, find the **Internal** sensitivity label group. Select the vertical ellipsis (**...**) next to it, then select **+ Create label in group** from the dropdown menu.

    ![Screenshot showing the Action menu to create a label in group for a sensitivity label.](../Media/create-label-in-group.png)

1. The **New sensitivity label** wizard will start. On the **Provide basic details for this label** page enter:

   - **Name**: `Employee data (HR)`
   - **Display name**: `Employee data (HR)`
   - **Description for users**: `This HR label is the default label for all specified documents in the HR Department.`

1. Select **Next**.

1. On the **Define the scope for this label** page, select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.

   > **Trainer note**:
   >
   > - Call out Files and Emails only
   > - Don't explain Meetings unless asked
   >
   > **Suggested talk track**:
   >
   > _This label applies to files and emails. We're keeping the scope narrow for this example._

1. Select **Next**.

1. On the **Choose protection settings for labeled items** page, select the **Control access**, then select **Next**.

   > **Trainer note**:
   > - Emphasize that labels can apply protection automatically
   > - Don't enumerate every protection option
   >
   > **Suggested talk track**:
   >
   > _This is where labels start enforcing protection, not just classification._

1. On the **Access control** page, select **Configure access control settings**.

   > **Trainer note**:
   > - Call out only two changes:
   >   - offline access duration
   >   - who can access the content
   > - Explicitly say defaults are being left in place
   >
   > **Suggested talk track**:
   >
   > _I'm only changing two things here. I'm setting offline access to 15 days and allowing access for authenticated users. Everything else stays at its default to keep the demo focused._
   >
   > Then move on quickly.

1. Configure the encryption settings with these options:

   - **Assign permissions now or let users decide?**: Assign permissions now
   - **User access to content expires**: Never
   - **Allow offline access**: Only for a number of days
   - **Users have offline access to the content for this many days**: 15
   - Select the **Assign permissions** link. On the **Assign permissions** flyout panel, select **+ Add any authenticated users**, then select **Save** to apply this setting.

1. On the **Access control** page, select **Next**.

1. On the **Auto-labeling for files and emails** page, select **Next**.

1. On the **Define protection settings for groups and sites** page, select **Next**.

1. On the **Review your settings and finish** page, select **Create label**.

1. On the **Your sensitivity label was created** page, select **Publish label to users' apps**, then select **Done**.

1. On the **Publish label** flyout, select **Create new label policy**.

   > **Trainer note**:
   >
   > - Reinforce the separation between creation and availability
   > - Don’t explain every policy page
   >
   >**Suggested talk track**:
   >
   >_Creating a label defines the protection. Publishing it is what actually makes it available in user apps._

1. On the **Choose sensitivity labels to publish** page, select the **Choose sensitivity labels to publish** link.

1. On the **Sensitivity labels to publish** flyout panel, select the  **Internal/Employee data (HR)** checkbox, then select **Add** at the bottom of the flyout page.

1. Back on the **Choose sensitivity labels to publish** page, select **Next**.

1. Select **Next** until you reach the **Policy settings** page.

1. On the **Policy settings** page, select the checkbox next to **Users must provide a justification to remove a label or lower its classification**, then select **Next**.

   > **Trainer note**:
   >
   > - One sentence only
   >
   > **Suggested talk track**:
   >
   > _This setting requires justification if someone removes or downgrades the label, which helps with accountability._
   >
   > Then continue clicking.

1. Select **Next** until you reach the **Name your policy** page.

1. On the **Name your policy** page, enter:

   - **Name**: `Internal HR employee data`

   - **Enter a description for your sensitivity label policy**: `This HR label is to be applied to internal HR employee data.`

1. Select **Next**.

1. On the **Review and finish** page, select **Submit**.

1. On the **New policy created** page, select **Done** to finish publishing your label policy.

You've published the Internal label group and its HR label so users can apply them to HR documents. It might take up to 24 hours for the policy to propagate across services.

   > **Trainer note**:
   >
   > - Tie back to the slide
   >
   > **Suggested talk track**:
   >
   > _At this point, the label exists, enforces encryption, and is available to users. That’s the full lifecycle from creation to use._
