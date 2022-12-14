---
lab:
    title: 'Lab 2: Conditional Mail Routing'
    Exercise: 'Exercise 1: Create mail flow rules'
    Learning Path: 'Learning Path 2: Manage and troubleshoot mail flow in Microsoft 365'
---

# Lab 2 - Exercise 1 – Create Mail Flow Rules

In this lab, you will continue in your role as Holly Dickson, Adatum’s Messaging
Administrator. In the prior lab, you created new send and receive connectors for
Adatum's on-premises Exchange Server 2019 deployment. Since Adatum has deployed
Microsoft 365 and is looking to implement a hybrid Exchange environment, Holly
will now begin configuring Exchange Online.

Holly has decided to create a series of mail flow rules designed to protect
Adatum’s messaging environment. She will do so using her client computer
(LON-CL1) to access the Exchange Admin Center for Exchange Online.

In your continuing role as Holly Dickson, you will create mail flow rules for
the following scenarios:

- **Sensitive material.** The mail flow rule will quarantine messages sent
    from inside the organization that have the words “Secret”, “Classified”, or
    “Sensitive” in the body or subject of the message.

- **Unscanned attachments.** The mail flow rule will quarantine messages that
    have attachments that are unscanned. The rule will also generate a reply
    message that lets the sender know they have sent a message that is
    undeliverable.

- **Partially scanned attachments.** The mail flow rule will quarantine
    messages that have attachments that were scanned, but the message scan did
    not finish. This rule will also generate a reply message that lets the
    sender know they have sent a message that is undeliverable.

- **Email size.** The mail flow rule will restrict the size of emails.

## Task 1 - Create Mail Flow rule for sensitive material

In this exercise you will access the Exchange Admin Center for Exchange Online
using your client PC (LON-CL1). You will then create a mail flow rule that
checks for sensitive information in emails sent from inside the organization.

1. Switch to **LON-CL1** and log in as the **Administrator** account with a
    password of **Pa55w.rd**.

2. Select the **Microsoft Edge** icon either on the desktop or the taskbar.
    Maximize your browser window when it opens.

3. In your browser navigate to the **Office 365 Home** page by entering the following URL in the address bar: **<https://portal.office.com/>**

4. In the **Sign in** dialog box, copy and paste in the **Tenant Email**
    account provided by your lab hosting provider
    (**admin@xxxxxZZZZZZ.onmicrosoft.com**, where xxxxxZZZZZZ is your unique
    tenant prefix provided by your lab hosting provider) and then select
    **Next**.

5. In the **Enter password** dialog box, copy and paste in the **Tenant
    Password** provided by your lab hosting provider and then select **Sign
    in**.

6. On the **Stay signed in?** dialog box, select the **Don’t show this again**
    check box and then select **Yes.**

7. If a **Get your work done with Office 365** dialog box appears, select the
    **X** to close it.

8. In the **Office 365 Home** page, select the **Admin** icon in the column of
    Microsoft 365 app icons on the left-side of the screen.

9. In the **Microsoft 365 admin center**, in the left-hand navigation bar,
    select **Show All** to display all the navigation menu options.

10. On the left-hand navigation bar, in the **Admin centers** section, select
    **Exchange**.

11. In the **Exchange admin center**, in the left-hand navigation
    pane, under **Mail flow**, select the **rules** tab. Stay in this
    tab.

     >[!Alert]  As of October 2022, the new modernized Rules page is still being rolled out. If after you select into the **Rules** tab you see an information flash stating **The Rules page will be updated to a new modernized version soon..** select **Try it now** to switch to the new experience.

12. The first mail flow rule that you create will check for emails sent from
    inside the organization that have sensitive words in the email subject line
    or body. Select the **+ Add a rule** icon in the menu bar, and in the
    drop-down menu that appears, select **Modify messages.**

13. In the **New Transport rule** wizard that appears, under **Set rule conditions** enter **Sensitive material** in the
    **Name** field.

14. At the bottom of the **Set rule conditions** page, select the hyperlink for **Show all rule conditions.**  

15. In the **Set the rule if** drop down menu, select **The subject or body**.

     A new drop down menu will be displayed on the right. From this drop down, select **Subject or body includes any of these words.**

16. In the **specify words or phrases** window that appears, type **secret** in the text field and then select **Add**

17. Repeat the steps above for the words **classified** and **sensitive**.

18. The three words should display below the text field. Once completed, select **Save**.

19. This brings you back to the **Set rule conditions** window. To the right of the **subject or body includes any of...** field, select the (**+**) button.

20. This creates a Boolean **And** condition. In the drop down menu below **And**, select **The
    sender**. In the new drop down menu that appears to the right, select **is external/internal**.

21. In the **select sender location** window that appears, select
    **Inside the organization**, and then select **Save**.

22. In the **Do the following** drop down menu, select **Redirect the message to** and in the drop down menu that appears on the right, select
    **hosted quarantine.**

23. Select the (**+**) button to add another action.

24. In the drop-down menu under the second action field that appears, select **Apply a disclaimer to the message** and in the drop down menu that
    appears on the right, select **append a disclaimer.**

25. Underneath the **Apply a disclaimer to the message** drop down menu select **Enter text.**

26. In the **specify disclaimer text** window, enter the following message in
    the field: **This message contains sensitive material that can harm the
    company or your team.**

27. Select **Save.**

28. Underneath the **Apply a disclaimer to the message** drop down menu select **Select one.**

29. In the **specify fallback action** window that appears, select **Wrap** (Wrap means if the disclaimer cannot be inserted into the original email, it will attach the message to a new disclaimer email) and then select **Save**.

30. Leave the **Except if** condition as the default setting, and then select **Next.**

31. In the **Set rule settings** window that appears select the following settings:

    - Priority: **0**
    - Rule Mode: **Enforce**
    - Severity: **Medium**

32. Leave all other settings as default and then select **Next**.

33. in the **Review and finish** page, Verify the rule conditions and settings are correct. If corrections are needed, select the **Edit rule conditions** or **Edit rule settings** and make the necessary corrections. Once you have verified the conditions and rules are correct, select **Finish**.

    It may take up to a minute to create the rule. Once **Transport rule created successfully** is displayed, select **Done**.

34. You will now be brought back to the **Rules** page. Notice the rule **Sensitive material** shows a status of **Disabled**.

    Select the word **Disabled** which will open up a new window for the **Sensitive material** rule settings. Under **Enable or disable rule** select the slider button so that it shows **Enabled** and then close the window by selecting **X** in the upper right hand corner.

    **Note:** After enabling the rule, it may take up to a minute for the rule to refresh and display as enabled.

35. Leave the Exchange Admin Center open to the **rules** tab on the **mail
    flow** page and proceed to the next task.

## Task 2 - Create first Mail Flow rule for attachments

In this exercise you will create two mail flow rules related to attachments.
Adatum wants to check for emails containing attachments that were either not
scanned or the scanning did not complete. You cannot include both conditions in
one rule, since multiple conditions in a mail flow rule are treated in a Boolean
**AND** fashion (for example, condition 1 is True AND condition 2 is True; this
is similar to what you did in the prior task where you checked for specific
words in the email AND the email was received from inside the organization).

In this case, it does not make logical sense to create just one rule that checks
for attachments that were not scanned AND for attachments in which scanning did
not complete. Therefore, you will need to create two rules; one for messages
with attachments that were not scanned and one for messages with attachments
where scanning of the attachments did not complete. Because these two conditions
will be defined in separate rules, the rules will be applied in a Boolean **OR**
fashion (for example, condition 1 is True OR condition 2 is True).

This task will create the first rule; the next task will create the second rule.

1. You should still be logged into LON-CL1 as the **Administrator** with a
    password of **Pa55w.rd**; however, if the log-in page appears, then log in
    now.

2. In your **Edge** browser, the **Exchange Admin Center** should still be open
    from the prior task, and you should still be on the **rules** tab for the
    **mail flow** page. If so, then proceed to the next step; otherwise,
    navigate to the **Exchange admin center**, then select **mail flow** in the
    left-hand navigation pane and select the **rules** tab, just as you did in
    the prior task.

3. In this task, you will create a mail flow rule that checks for emails that
    contain attachments that cannot be scanned. In the **rules** tab, select the
    **+ Add a rule** icon in the menu bar and in the drop-down menu, select
    **Modify messages.**

4. In the **New Transport rule** wizard that appears, under **Set rule conditions** enter **Attachments could not be scanned** in the
    **Name** field.

5. At the bottom of the **Set rule conditions** page, select the hyperlink for **Show all rule conditions.**

6. Select drop-down arrow in the **Set the rule if** field. In the menu
    that appears, select **Any attachment**.

7. In the the new drop-down menu that appears to the right of
    **Set the rule if**, select **content can’t be inspected.**

8. In the drop-down menu under **Do the following**, select **Redirect the message to** and in the drop down menu that appears on the right, select
    **hosted quarantine.**

9. Select the **(+)** button to the right of **hosted quarantine** to add an new action.

10. This creates a Boolean **And** condition. In the drop down menu below **And**, select **Apply a disclaimer to the message**. In the new drop down menu that appears to the right, select **append a disclaimer.**

11. Underneath the **Apply a disclaimer to the message** drop down menu select **Enter text.**

12. In the **specify disclaimer text** window, enter the following message in
    the field: **Attachments in this message were not scanned.**

13. Select **Save.**

14. Underneath the **Apply a disclaimer to the message** drop down menu select **Select one.**

15. In the **specify fallback action** window that appears, select **Wrap** and then select **Save**.

16. Leave the **Except if** condition as the default setting, and then select **Next.**

17. In the **Set rule settings** window that appears select the following settings:

    - Priority: **1**
    - Rule Mode: **Enforce**
    - Severity: **Medium**

18. Leave all other settings as default and then select **Next**.

19. in the **Review and finish** page, Verify the rule conditions and settings are correct. If corrections are needed, select the **Edit rule conditions** or **Edit rule settings** and make the necessary corrections. Once you have verified the conditions and rules are correct, select **Finish**.

    It may take up to a minute to create the rule. Once **Transport rule created successfully** is displayed, select **Done**.

20. You will now be brought back to the **Rules** page. Notice the rule **Attachments could not be scanned** shows a status of **Disabled**.

    Select the word **Disabled** which will open up a new window for the **Attachments could not be scanned** rule settings. Under **Enable or disable rule** select the slider button so that it shows **Enabled** and then close the window by selecting **X** in the upper right hand corner.

    **Note:** After enabling the rule, it may take up to a minute for the rule to refresh and display as enabled.

21. Leave the Exchange Admin Center open to the **rules** tab on the **mail
    flow** page and proceed to the next task.

## Task 3 - Create second Mail Flow rule for attachments

In the prior task, you created a mail flow rule for messages with attachments
that were not scanned. In this task, you will create a second mail flow rule for
messages with attachments; however, in this case, it will be for messages with
attachments in which scanning of the attachments did not complete. Because these
conditions will be defined in separate rules, the rules will be applied in a
Boolean OR fashion.

1. You should still be logged into LON-CL1 as the **Administrator** with a
    password of **Pa55w.rd**; however, if the log-in page appears, then log in
    now.

2. If the **Exchange admin center** is still open from the prior task, then
    proceed to the next step; otherwise, navigate to the **Exchange admin
    center**, then select **mail flow** in the left-hand navigation pane and
    select the **rules** tab.

3. You will now create a mail flow rule that checks for emails that contain
    attachments where the scanning of the attachments didn’t finish. In the **rules** tab, select the
    **+ Add a rule** icon in the menu bar and in the drop-down menu, select
    **Modify messages.**

4. In the **New Transport rule** wizard that appears, under **Set rule conditions** enter **Attachment scanning did not complete** in the
    **Name** field.

5. At the bottom of the **Set rule conditions** page, select the hyperlink for **Show all rule conditions.**

6. Select drop-down arrow in the **Set the rule if** field. In the menu
    that appears, select **Any attachment**.

7. In the the new drop-down menu that appears to the right of
    **Set the rule if**, select **didn't complete scanning.**

8. In the drop-down menu under **Do the following**, select **Redirect the message to** and in the drop down menu that appears on the right, select
    **hosted quarantine.**

9. Select the **(+)** button to the right of **hosted quarantine** to add an new action.

10. This creates a Boolean **And** condition. In the drop down menu below **And**, select **Apply a disclaimer to the message**. In the new drop down menu that appears to the right, select **append a disclaimer.**

11. Underneath the **Apply a disclaimer to the message** drop down menu select **Enter text.**

12. In the **specify disclaimer text** window, enter the following message in
    the field: **Scanning of attachments in this message did not complete.**

13. Select **Save.**

14. Underneath the **Apply a disclaimer to the message** drop down menu select **Select one.**

15. In the **specify fallback action** window that appears, select **Wrap** and then select **Save**.

16. Leave the **Except if** condition as the default setting, and then select **Next.**

17. In the **Set rule settings** window that appears select the following settings:

    - Priority: **2**
    - Rule Mode: **Enforce**

18. Leave all other settings as default and then select **Next**.

19. in the **Review and finish** page, Verify the rule conditions and settings are correct. If corrections are needed, select the **Edit rule conditions** or **Edit rule settings** and make the necessary corrections. Once you have verified the conditions and rules are correct, select **Finish**.

    It may take up to a minute to create the rule. Once **Transport rule created successfully** is displayed, select **Done**.

20. You will now be brought back to the **Rules** page. Notice the rule **Attachment scanning did not complete** shows a status of **Disabled**.

    Select the word **Disabled** which will open up a new window for the **Attachment scanning did not complete** rule settings. Under **Enable or disable rule** select the slider button so that it shows **Enabled** and then close the window by selecting **X** in the upper right hand corner.

    **Note:** After enabling the rule, it may take up to a minute for the rule to refresh and display as enabled.

21. Leave the Exchange Admin Center open to the **rules** tab on the **mail
    flow** page and proceed to the next task.

## Task 4 – Create Mail Flow rule restricting email size

After Holly reviewed the messaging environment at Adatum Corporation, she
realized that she could provide a more efficient and secure environment by
creating some targeted mail flow rules. She has decided to create a set of mail
flow rules that identify and act on messages that are in-transit through her
Exchange Online organization, as opposed to simply waiting until the messages
are delivered to mailboxes before being acted upon by Inbox rules in Outlook and
Outlook on the web.

Holly has discovered that mail flow rules contain a richer set of conditions,
exceptions, and actions, all of which will provide her with the flexibility to
implement many types of messaging policies for Adatum. She is eager to put this
to the test regarding a significant issue currently affecting Adatum’s messaging
environment - users who send extremely large email messages. She has decided to
address this issue by creating a mail flow rule that restricts email size.

1. You should still be logged into LON-CL1 as the **Administrator** with a
    password of **Pa55w.rd**; however, if the log-in page appears, then log in
    now.

2. If the **Exchange admin center** is still open from the prior task, then
    proceed to the next step; otherwise, navigate to the **Exchange admin
    center**, then select **mail flow** in the left-hand navigation pane and
    select the **rules** tab.

3. You will now create a mail flow rule that checks the size of emails and restricts those that exceed a specific size. In the **rules** tab, select the
    **+ Add a rule** icon in the menu bar and in the drop-down menu, select
    **Filter messages by size.**

4. In the **New Transport rule** wizard that appears, enter **Email size restriction** in the
    **Name** field.

5. Notice the two fields under **Set the rule if** are already populated with **The message** and **Size is greater than or equal to** by default. These are the correct settings for the purpose of this exercise, however if they are not pre-populated please set them accordingly.

6. Underneath the **Set the rule if** conditions, select **Enter text.**

7. In the **specify size (kb)** window that appears, enter the text: **1024** and then select **Save**

8. In the drop-down menu under **Do the following**, select **Block the message** and in the drop down menu that appears on the right, select
    **reject the message and include an explanation.**

9. in the **specify rejection reason** window that appears, enter the following text: **Your message exceeds the size limit. Please adjust the message size
    or compress the email content and send it as a zipped file.**

10. Select **Save**

11. Leave the **Except if** condition as the default setting, and then select **Next.**

12. In the **Set rule settings** window that appears select the following settings:

    - Priority: **3**
    - Rule Mode: **Enforce**

13. Leave all other settings as default and then select **Next**.

14. in the **Review and finish** page, Verify the rule conditions and settings are correct. If corrections are needed, select the **Edit rule conditions** or **Edit rule settings** and make the necessary corrections. Once you have verified the conditions and rules are correct, select **Finish**.

    It may take up to a minute to create the rule. Once **Transport rule created successfully** is displayed, select **Done**.

15. You will now be brought back to the **Rules** page. Notice the rule **Email size restriction** shows a status of **Disabled**.

    Select the word **Disabled** which will open up a new window for the **Email size restriction** rule settings. Under **Enable or disable rule** select the slider button so that it shows **Enabled** and then close the window by selecting **X** in the upper right hand corner.

    **Note:** After enabling the rule, it may take up to a minute for the rule to refresh and display as enabled.

16. Leave the Exchange Admin Center open to the **rules** tab on the **mail
    flow** page and proceed to the next task.

## End of Lab 2
