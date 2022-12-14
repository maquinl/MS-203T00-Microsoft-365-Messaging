---
lab:
    title: 'Create Public Folders'
    learning_path: 'Learning Path 7: Manage recipient objects and resources in Microsoft 365'
    Module: 'Module 2: Create and Manage Exchange Recipients'
---

# Lab 6 - Exercise 1 - Create and manage Public Folders

Holly Dickson wants to continue reviewing the messaging functionality in
Microsoft 365, and more specifically, the use of public folders. In this lab,
you will log into the Exchange admin center for Exchange Online and create a
public folder mailbox and a public folder in Microsoft 365. You will then manage the settings and permissions for the created public folder.

Public folder mailboxes contain the hierarchy information plus the content for
public folders. The first public folder mailbox you create will be the primary
hierarchy mailbox, which contains the only writable copy of the hierarchy. Any
additional public folder mailboxes you create will be secondary mailboxes, which
contain a read-only copy of the hierarchy.

Public folders are designed for shared access and provide an easy and effective
way to collect, organize, and share information with other people in your
workgroup or organization. You can't create a public folder unless you've first
created a public folder mailbox.

## Task 1 - Create a Public Folder Mailbox

In this task, you will create a public folder mailbox as part of Holly’s
Microsoft 365 pilot project. Every public folder must be contained in a public
folder mailbox; therefore, you must create the public folder mailbox first
before you can create a public folder.

1. You should still be logged into LON-CL1 from the prior lab; if necessary,
    log in as the **Administrator** with a password of **Pa55w.rd**.

2. In the Edge browser, the Office 365 home page, the Microsoft 365 admin center, and the Exchange admin center tabs should still be open. Select the **Exchange admin center** tab. Switch back to the New EAC by selecting **New Exchange admin center** at the bottom of the left hand navigation pane.

3. In the **New Exchange admin center**, on the left-hand navigation pane, select **Public folders**.

4. Then in the expanded group, select **Public folders mailboxes**.

5. On the **Public folder mailboxes** page, select the **plus (+) sign** icon on the menu bar to add a new public folder mailbox.

6. In the **new public folder mailbox** window, enter **Test PF mailbox1** in
    the **Name** field, select **Save**, and then select **OK** once the
    information is successfully saved.

7. This will return you to the **public folder mailboxes** page, which should
    now display **Test PF mailbox1**.

8. Leave all browser tabs open and proceed to the next task.

## Task 2 - Create a Public Folder

Now that you have created a public folder mailbox, you can create a public
folder. When using the EAC to create a public folder, you'll only be able to set
the name and the path of the public folder. To configure additional settings,
you'll need to edit the public folder after it's created (which you will do in
the next lab exercise).

1. You should still be in LON-CL1 and you should be in the **Exchange admin
    center** tab in your browser.

2. In the **Exchange admin center**, you should still be in the **public folder mailboxes** page after having completed the prior task.  

    Since you now want to create a public folder, in the EAC navigation pane select **Public folders** and then in the expanded group, select **Public folders** again.

3. On the **Public folders** page, select the **plus (+) sign** icon to add a  new public folder.

4. In the **new public folder** window, enter **Test PF1** in the **Name**
    field, select **Save,** and then select **OK** once the information is
    successfully saved.

5. This will return you to the **public folder** page, which should now display
    **Test PF1**.

6. Leave all browser tabs open and proceed to the next task.

## Task 3 - Manage Public Folder Mail Settings

In this task, you will continue in your role as Holly Dickson and enable the
Test PF1 public folder that you created in the previous task so that it can
receive email.

1. You should still be logged into LON-CL1 from the prior lab; if necessary,
    log in as the **Administrator** with a password of **Pa55w.rd**.

2. In the Edge browser, you should still be in the **Exchange admin center** from the end of the prior task. Specifically, you should still be on the **public folders** page.

3. On the **public folders** page, the **Test PF1** record that you created in the prior task should be highlighted.  

    **Important:** If you closed the EAC tab at the end of the prior task and had to navigate to this page in the prior step, then select the **Test PF1** row. Do not select the **Test PF1** hyperlink as this will open the **Test PF1** public folder window. Instead, select any other portion of the **Test PF1** row to simply highlight the record.

4. By selecting the Test PF1 record, the properties for this public folder are
    displayed in the detail pane on the right. Note the current **Mail
    settings** for Test PF1 is set to Disabled. To enable mail for this public
    folder, select **Enable**.

5. A **Warning** dialog box will appear that asks whether you want to enable
    email for the selected public folders. Select **Yes**.

6. In the detail pane on the right, the **Mail settings** should now be
    **Enabled.**

7. Leave all browser tabs open and proceed to the next task.

## Task 4 - Manage Public Folder Settings

In this task, you will manage several settings for the Test PF1 public folder.

1. You should still be in LON-CL1 and you should be in the **Exchange admin
    center** tab in your browser.

2. In the **Exchange admin center**, you should still be in the **public folders** page.

3. On the **public folders** page, the **Test PF1** record that you updated in the prior task should be highlighted.  

    **Important:** If you closed the EAC tab at the end of the prior task and
    had to navigate to this page in the prior step, then select the **Test PF1**
    row. Do not select the **Test PF1** hyperlink as this will open the **Test
    PF1** public folder window. Instead, select any other portion of the **Test
    PF1** row to simply highlight the record.

4. With the **Test PF1** record highlighted in the public folder list, select
    the **pencil (Edit)** icon in the menu bar to edit the record. This opens
    the **Test PF1** properties window.

5. In the **Test PF1** properties window, the **general** tab in the left-hand
    navigation pane is displayed by default. Review the fields in this tab and
    note the value in the **Public folder mailbox** field; this indicates that
    **Test PF1** was automatically assigned to the **Test PF mailbox1** that you
    created in the first task in this exercise.

6. In the **Test PF1** properties window, in the left-hand navigation pane,
    select the **general mail properties** tab.

7. Change the value of the **Display Name** field to **First public folder.**

8. Select the **Hide from Exchange address list** checkbox.  

    **Note:** By selecting this check box, the public folder will not appear in
    Adatum’s address book and other address lists, but it will still receive
    email.

9. In the left-hand navigation pane, select the **mail flow settings** tab.

10. Under the **Display Name** field, select the **Require that all senders are
    authenticated** check box.

11. Select **Save**. Once the settings have been saved, select **Close**.

12. Leave all browser tabs open and proceed to the next task.

## Task 5 - Manage Public Folder Permissions

In this task, you will manage the permissions for the Test PF1 public folder.

1. You should still be in LON-CL1 and you should be in the **Exchange admin
    center** tab in your browser.

2. In the **Exchange admin center**, you should still be in the **public folders** page.

3. On the **public folders** page, the **Test PF1** record that you updated in the prior task should be highlighted.

4. With the **Test PF1** record highlighted in the public folder list, a **Test
    PF1** detail pane will be displayed on the right side of the screen. In the
    detail pane, under **Folder permissions**, select **Manage**.

5. A **Test PF1** window will appear that enables you to add or remove users
    who can access this public folder and edit its permissions. Select the
    **plus (+) sign** icon to add users.

6. In the **public folder permissions** window, select the **Browse** button to
    the right of the **User** field, select **MOD Administrator**, and then select **OK**.

7. Select the drop-down arrow in the **Permission level** field and select
    **Owner.**

8. Select **Save** at the bottom of the **public folder permissions** window.

9. Select **Save** at the bottom of the **Test PF1** window. Once the settings
    have been saved, select **Close**.

10. Leave all browser tabs open and proceed to the next lab.

## Proceed to Lab 6 - Exercise 2
