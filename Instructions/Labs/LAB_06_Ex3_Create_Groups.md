---
lab:
    title: 'Create groups'
    learning_path: 'Learning Path 7: Manage recipient objects and resources in Microsoft 365'
    module: 'Module 2: Create and Manage Exchange Recipients'
---

# Lab 6 - Exercise 3 - Create Groups

In this exercise, you will continue in your role as Holly Dickson, Adatum’s
Messaging Administrator. As part of her pilot project for deploying Microsoft
365, Holly wants to examine how creating groups in her on-premises Exchange
Server 2019 environment differs from creating groups in Microsoft 365 for
Exchange Online. You will begin by creating an on-premises distribution group
for Exchange Server 2019 and then a cloud distribution group in Microsoft 365.
You will finish by creating a Microsoft 365 group.

## Task 1 - Create an On-premises Distribution Group

In this task you will log into the Exchange Server (LON-EX1) virtual machine and
create an on-premises distribution group in the Exchange admin center for
Exchange Server 2019.

1. Switch to **LON-EX1**, and if necessary, log in as the **Administrator**
    with a password of **Pa55w.rd**.

2. In the **Edge** browser, you should still have the on-premises **Exchange
    admin center** open from a prior lab exercise; if so, then proceed to the
    next step. Otherwise, on the taskbar at the bottom of the page, select the
    **Start** icon, select the **Microsoft Exchange Server 2019** group in the
    menu, and in the drop-down list, select **Exchange Administrative Center**.
    Sign into the EAC as **adatum\\Administrator** with a password of
    **Pa55w.rd**.

3. In the **Exchange admin center**, in the left-hand navigation pane, select
    **recipients**.

4. On the **recipients** page, select the **groups** tab at the top of the
    page.

5. Select the **plus (+) sign** icon on the menu bar to add a new group, and in
    the drop-down menu, select **Distribution group**.

6. In the **new distribution group** window, enter **Finance** in both the
    **Display name** and **Alias** fields.

7. Enter **This is the Finance team** in the **Notes** field.

8. Select the **Browse** button to the right of the **Organizational unit**
    field.

9. In the **select an organizational unit** window, select **Users** and then
    select **OK**.

10. Under the **Owners** field, note that the **Administrator** account, which
    you are signed in as, is automatically listed as an owner of this group.
    Since you want to add Holly Dickson as an additional owner for this group,
    select **plus (+) sign** icon.

11. In the **Select Owner** window, select **Holly Dickson**, select the
    **add->** button, and then select **OK**.

12. In the **new distribution group** window, scroll down to the **Members**
    section. Since you are just adding the group now, there are no group members
    at this time.  

    However, verify that the **Add group owners as members** check box is
    selected so that Holly and the Administrator account, who are the two
    owners, will be automatically added as members of the group. Then select the
    **plus (+) sign** icon to add additional group members.

13. In the **Select Members** window, select **Jessica Hofer**, select the
    **add->** button, and then select **OK**.

14. This will be a Closed group, so in the two settings at the bottom of the
    page below the list of Members, select the **Closed** option for both the
    **Choose whether owner approval is required to join the group** setting and
    the **Choose whether the group is open to leave** setting.

15. Select **Save**.

16. On the **groups** page, the **Finance** distribution group should now appear
    in the list of groups.

17. Leave the Exchange admin center open and proceed to the next task.

## Task 2 - Create a Cloud Distribution Group

Now that Holly has experienced adding a distribution group in Adatum’s
on-premises Exchange Server 2019 environment, she wants to add a distribution
group in Microsoft 365. To avoid any confusion, Holly will switch to LON-CL1 to
access the Exchange admin center for Exchange Online.

1. Switch to LON-CL1 and if necessary, log in as the **Administrator** with a
    password of **Pa55w.rd.**

2. In the Edge browser, you should still have the following tabs open from the
    prior lab exercise: the **Office 365 Home** tab, the **Microsoft 365 admin
    center** tab, and the **Exchange admin center** tab.  

3. On the **Exchange admin center** select **recipients**, then in the expanded menu select **Groups**.

4. On the **Groups** page, the **Microsoft 365** tab should be selected by default. Instead, select the **Distribution list** tab and then **Add a group**.

5. The **Add a group** wizard will be displayed on a new page. Under **Choose a group type** choose **Distribution** and then select **Next**.

6. Under **Set up the basics** enter the following and then select **Next**:

     - Name: **Marketing**
     - Description: **This is the Marketing team**

7. Under **Assign owners**, select **+ Assign owners**.

8. in the new **Assign owners** pane that is displayed, search for and select **MOD Administrator**, then select **Add (1)**.

    Select **Next** to proceed.

9. Under **Add Members**, do not add any members yet, you will do this in a later step. Instead, select **Next**.

10. Under **Edit settings**, type **Marketing** in the **Group email address field**.

11. This will be a closed group, so select the **Closed** option for both the **Joining the group** setting and **Leaving the group** setting. Then select **Next**.

12. under **Review and finish adding group**, select **Create group**.  

    **Important:** Note the message that appears once the marketing group has been created stating **It can take up to an hour for Marketing group to appear in your groups list.

    Select **Close**.

13. On the **Groups** page, select **Refresh** on the menu bar to display the Marketing group in the list of distribution groups.

    **Note:** Lab testing has indicated that this group typically appears within a few minutes, so select
    **Refresh** within 5 minutes to see whether the Marketing group appears.  

    **Important:** You cannot continue until the Marketing group appears in this list
    of distribution groups.

14. Once the Marketing group appears in the list of distribution groups, select  the **Marketing** group name.

15. In the **Marketing** pane that appears, the **General** tab is displayed by default. Select the **Members** Tab.

16. Under the **Owners (1)** section, the **MOD Administrator** account is displayed, Select **View all and manage owners** to add additional owners.

17. In the pane that appears, select **+ Add owners**.

18. Search for and select **Holly Dickson**, then select **Add (1)**.

19. Once **Saved** is displayed, select the **back arrow** to navigate back to the members tab.

20. This time select **View all and manage members**.

21. On the **Members** window, select **+ Add members** to add new members.

22. Search for and select the following users, then select **Add (3)**.

    - **Joni Sherman**
    - **Megan Bowen**
    - **Nestor Wilke**

23. Verify the **Members** page includes **Joni Sherman**, **Megan Bowen**, and **Nestor Wilke**. Then select **X** in the top right hand corner to exit close the pane.

24. Leave your browser and all the tabs open and proceed to the next task.

## Task 3 - Create a Microsoft 365 Group

In this task you will create a Microsoft 365 group, which is similar to an
on-premises distribution group but with additional collaboration functionality.
While email can be sent to each type of group, members of a distribution group
receive email in their Inbox whenever someone sends an email to the email
address associated with distribution group; whereas a Microsoft 365 group
appears as an individual entity in Outlook and Outlook on the web if the user is
a member of the Microsoft 365 group. Therefore, whenever an email is sent to a
Microsoft 365 group, it does not land in the user’s Inbox; rather, it lands in
the separate group folder that is created in the user’s mailbox in Outlook or
Outlook on the web.

Another major difference between the two types of groups is that a Microsoft 365
Group is cloud-only and can be used for Team collaboration. Besides having a
shared mailbox and calendar, a Microsoft 365 group can be created along with an
associated SharePoint library, OneNote notebook, Microsoft Teams, Yammer,
Planner, and PowerBI, all of which allows teams to seamlessly work together.

1. You should still be in the LON-CL1 VM; if necessary, log in as the
    **Administrator** account with a password of **Pa55w.rd**.

2. In your browser, if you have the **Microsoft 365 admin center** open in a
    tab from the previous task, then select this tab and proceed to the next
    step; otherwise, navigate to [](https://portal.office.com/) and sign in
    using the **Tenant Email** and **Password** provided by your lab hosting
    provider, and then navigate to the **Microsoft 365 admin center**.

3. In the **Microsoft 365 admin center**, select **Teams & groups** in the left-hand
    navigation pane, and then in the expanded group select **Active teams & groups**.

4. In the **Active teams & groups** window, select **Add a group** on the menu bar.
    This initiates the **Add a group** wizard.

5. In the **Choose a group type** page, select **Microsoft 365 (recommended)**
    and then select **Next**.

6. In the **Set up the basics** window, enter **Sales** in the **Name** field,
    and then enter **Collaboration group for the Sales team** in the
    **Description** field. Select **Next**.

7. In the **Assign owners** page, you will assign Allan Deyoung and Patti
    Fernandez as owners of this group by selecting **+ Assign owners**. Select **Allan Deyoung** and **Patti Fernandez** from list of users.

    - Select **Add (2)**.

    - Select **Next**.

8. In the **Add members** page, select **Next**.

9. In the **Edit settings** page, enter **sales** in the **Group email
    address** field.

10. Under the **Privacy** section, select the **Private** option.

11. Under the **Add Microsoft Teams to your group** section, verify the **Create
    a team for this group** check box is selected (select it if need be).

12. Select **Next**.

13. In the **Review and finish adding group** page, review the content that you
    entered. If everything is correct, select **Create group**; otherwise,
    select **Back** and fix anything that needs correction (or select **Edit**
    under the specific area that needs adjustment).

14. On the **New group created** page, note the comment at the top of the page
    that it may take 5 minutes for the new group to appear in the list of
    groups.

    Select **Close**. This returns you to the **Groups** page.

15. If the new Sales group does not appear in the **Groups** list, wait a minute
    or so and then select **Refresh** on the menu bar. If the Sales group still
    does not appear, then refresh the page every minute or so until it does.

    **Note:** Two additional group types are Mail-enabled Security groups and
    Distribution groups. Neither of these group types were used in this lab
    because it can take up to an hour for these two types of groups to appear in
    the Groups list; whereas Microsoft 365 groups and Security groups usually
    take just a matter of minutes to appear.

16. You’re now ready to add members to the Sales group. In the list of **Active teams & groups**, select the **Sales** group.

17. In the **Sales** pane that appears, the **General** tab is displayed by
    default. Select the **Members** tab.

18. Under the **Owners** section, you can see the two owners (Allan and Patti).

19. In the **Members** section, select **Add members**.

20. In the **Search by name or email address** field, type and select the following user names (one at a time). Once finished, select **Add (2)**

    - **Diego Siciliani**
    - **Lynne Robbins**

21. You are returned to the **Add team members to sales** window, verify that the message **2 members are added as team members** and then select the **back arrow**.

22. On the **Sales** window, Diego and Lynne should now appear as members of the group. If they do not appear, select the **Refresh** icon in the upper  right-hand corner of the screen.  

    Once Lynn and Diego appear as members of the group, select the **X** in the
    upper right-hand corner to close the window.

23. On the **Active teams and groups** window, note the difference between the
    **Marketing** distribution list that you added in the prior task and the
    **Sales** group that you added in this task.

    Under the **Teams status** column, note the Sales group displays an icon
    indicating the group is connected to Microsoft Teams (hover your mouse over
    the icon to see the icon tag). However, the Marketing distribution list,
    which was added through the Exchange admin center for Exchange Online, does
    not display this icon. This is because the EAC does not provide this Teams
    option when adding a group through the EAC.

24. Leave your browser and all the tabs open for the next exercise.

## End of Lab 6
