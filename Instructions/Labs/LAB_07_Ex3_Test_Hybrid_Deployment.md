---
lab:
    title: 'Configure your Hybrid Deployment'
    learning_path: 'Learning Path 8: Manage the hybrid deployment life cycle'
    module: 'Module 5: Troubleshoot hybrid deployments'
---

# Lab 7 - Exercise 3 - Test your Hybrid Deployment

In the prior exercise, you configured Adatum’s Exchange environment for a hybrid
deployment. In this exercise, you will test your new hybrid deployment. This
will require that you:  

- Test the hybrid configuration by sending emails between on-premises and
    cloud users in Task 1

- Migrate a user mailbox from Exchange on-premises to Exchange Online to test
    your connectors in Task 2

- Test the newly migrated mailbox in Task 3

    **IMPORTANT:** Migrating an on-premises mailbox to Microsoft 365 in Task 2 can take up to
    an hour to complete. Instead of waiting around for an hour before you can do Task 3,
    proceed to the Final Assessment lab once you start the migration at the end of Task 2. By the time you finish the Final Assessment lab, the migration process in Task 2 should hopefully be complete, at which time you can
    return to this lab and perform Task 3 to test the newly
    migrated mailbox.

## Task 1: Test the Hybrid topology

In this task, you will verify that your hybrid environment is functioning
properly by performing the following validation steps that send emails between
an on-premises Exchange mailbox and a Microsoft 365 cloud mailbox:

- From your on-premises Exchange Server (LON-EX1) VM, you will first send an
    email from Allan Yoo’s on-premises Exchange Server mailbox to Alex Wilber's cloud mailbox in Microsoft 365.

- You will then open an InPrivate Browsing session in Edge browser so that you
    can log into Alex’s mailbox in Microsoft 365 and verify that he received the
    email from Allan.

- You will then send a reply from Alex's cloud mailbox to Allan's on-premises mailbox, and then verify that Allan
    received the reply.

    **Important:** In this task, note what happens when you send the email from Allan's on-premises
    mailbox to Alex's Microsoft 365 mailbox; or more specifically, note where the email
    is delivered. This situation provides the basis for the Final Assessment lab.

1. You should still be logged into LON-EX1 from the prior exercise; if
    necessary, log in as the **Administrator** with a password of **Pa55w.rd**.

2. You are now going to send an email from Allan Yoo’s on-premises mailbox to
    Alex Wilber’s Microsoft 365 mailbox; therefore, you must sign into Outlook
    using Allan’s on-premises email account.  
    ‎  
    ‎At the end of the prior lab exercise, if your Outbound connector validation
    failed and you verified that it was a false-positive error by opening Allan
    Yoo’s on-premises mailbox to see the test validation email in his Outlook
    Inbox, then skip to step 5.

    However, if your Outbound connector validation succeeded in the prior lab exercise, then perform steps 3-4 to open Allan’s
    on-premises mailbox.

3. If your Outbound connector validation succeeded in the prior lab exercise, then select a new tab in your **Edge
    browser** and open **Outlook Web App** by entering the following URL in the address bar:
    **<https://xxxUPNxxx.xxxCustomDomainxxx.xxx/owa>** (where xxxUPNxxx is the
    unique UPN name assigned to your tenant by your lab hosting provider and
    xxxCustomDomainxxx.xxx is your lab hosting provider’s custom domain).  
  
     **Note:** If you receive a page indicating **Your connection isn’t
    private**, this is due to a certificate issue in the VM environment that you
    can ignore for the purpose of this lab. To bypass this error, select the
    **Advanced** button, and then select **Continue to localhost (unsafe)**.

4. In **Outlook**, enter **adatum\\Allan** in the **Domain\\user name** field,
    enter **Pa55w.rd** in the **Password** field, and then select **sign in**.
    If requested, select your **Language** and **Time zone** and then select
    **Save**.

5. In Allan’s **Inbox**, you should see the email he received from the prior
    lab exercise in which the system validated the Outbound connector that you
    created.  

     You should now send an email from Allan’s on-premises mailbox to Alex
    Wilber’s Microsoft 365 mailbox. Select **New** in the ribbon, and in the
    email’s **To** address line, enter **alexw@xxxxxZZZZZZ.onmicrosoft.com**
    (where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting
    provider).

6. Enter **Hybrid test - On-premises to M365 email** in the **Subject** line,
    enter **From Allan’s on-premises mailbox to Alex’s M365 mailbox** in the
    body of the email, and then select **Send**.

7. At this point, you want to log into Alex Wilber’s Outlook mailbox in
    Microsoft 365 to verify he received the email from Allan Yoo’s on-premises
    mailbox. You then want to send a reply from Alex’s Microsoft 365 mailbox
    back to Allan’s on-premises mailbox.  

    **IMPORTANT:** Since you already have Allan’s mailbox open in Edge browser,
    you CANNOT open Alex’s mailbox in another tab in the same Edge session.
    Doing so will block email from Allan’s on-premises account from being sent
    to Alex’s Microsoft 365 account. **Therefore, you must start an InPrivate
    Browsing session and then open Alex’s mailbox in that session.**  

    To open an InPrivate Browsing session, right select the **Edge browser** icon on the taskbar and in the menu, select **New InPrivate window**.
    This will open a new, InPrivate Edge session that is separate from the Edge
    session that contains the tab with Allan’s mailbox.  

    Maximize the InPrivate browser window and enter the following URL:
    **<https://portal.office.com>**  

8. In the **Sign in** window, enter **alexw@xxxxxZZZZZZ.onmicrosoft.com**
    (where xxxxZZZZZZ is the tenant prefix provided by your lab hosting
    provider) and then select **Next.**

9. In the **Enter password** window, enter your tenant email password provided
    by your lab hosting provider and then select **Sign in**.

10. If a **Get your work done with Office 365** window appears, select **X** to
    close it.

11. In Alex’s **Office 365 Home** page, note all the applications that are displayed in the column of Microsoft 365 apps on the left-side of the screen.
    These are the apps that are enabled for Alex given his Office 365 E5 product
    license. Select the **Outlook** icon.

12. Alex’s Microsoft 365 mailbox will open in **Outlook**. If a **Welcome**
    window appears, select **X** in the upper-right corner to close it.

13. Note that Allan’s email to Alex does not appear in Alex’s Inbox. However,
    select Alex’s **Junk Email** folder. If the email sent by Allan appears in
    Alex’s **Junk Email folder**, then open the email and reply to the message.
    Indicate in the reply that this message is from Alex’s Microsoft 365 mailbox
    to Allan’s on-premises mailbox.  

    **Important:** There is a specific reason why Allan’s email ended up in
    Alex’s Junk Email folder rather than his Inbox. However, the reason will not
    be explained here, since this is the very issue covered in the next lab
    exercise, which is the Final Assessment lab. Once you complete the Final
    Assessment lab, you will understand why this occurred. For now, simply leave
    Allan’s email in Alex’s Junk Email folder and send your reply back to Allan
    as directed earlier in this step.  

14. After sending Alex's reply back to Allan, hover over the **Edge browser** icon on the taskbar and select the session
    that displays **Allan’s** on-premises mailbox. Verify that Allan received
    the reply from Alex (you may need to refresh the Inbox if the reply is not
    there when you return to Allan’s mailbox).  

     You have just verified that your hybrid environment is functioning properly.

15. Close the InPrivate Browsing session but leave your Edge browser session
    open.

16. There is another test that you can perform to validate that your connector
    worked properly, even though the validation may have failed. This test is a message trace.

    Select the **Exchange Admin Center** tab in your Edge browser to display the EAC for
    Exchange Online.

17. In the **Exchange admin center**, select **Mail flow** in the left-hand navigation pane, and then in the expanded group, select **Message trace**.

18. On the **Message trace** window, the **Default queries** tab at the top of the
    page is displayed by default. In the list of queries and reports in this
    tab, select **Messages sent from my primary domain in the last day.**

19. In the **New message trace** pane that appears, the default values for the
    **Messages sent from my primary domain in the last day** query are
    displayed. You can control which messages are selected based on who sent and
    received the messages and how many days ago the messages were sent.  

    All the default settings on this page are sufficient for this message trace that you want to perform, so none of the settings need to be changed:

    - **Senders.** You want to view email from all senders from the xxxUPNxxx.xxxCustomDomainxxx.xxx domain.
    - **Recipients.** You want to view email sent to all recipients.
    - **Time range.** You want to view all email sent in the past day.
    - **Report type.** You want to view the Summary report, which provides instant online access to the message trace search results.

    Since none of the settings need to be changed, simply select the **Search** button at the bottom of the page to initiate the message trace.

20. On the **Message trace search results** window, you should see each of the emails
    that have been sent and received:

    - the O365ConnectorValidation email from the Outbound connector validation
        process to Allan Yoo

    - the email you sent from Allan Yoo to Alex Wilber that was received into
        Alex’s Junk Email folder (note the **Status** of this email, which is
        **FilteredAsSpam**)

21. Leave your browser and all its tabs open and proceed to the next exercise.

## Task 2: Migrate an on-premises mailbox to test your connectors

In this task, you will log into your Exchange Server (EX1) VM, open the
New Exchange Online admin center, and migrate Allan Yoo’s on-premises mailbox
(along with his mail) to Microsoft 365. The purpose of this task is to verify
whether your connectors are correctly set up and to provide a level of
simplicity for the user.

When users are cloud-hosted they do not have to use a VPN tunnel to access
company files; they can log in from any PC or device and work from any location
that has a stable internet connection. In contrast, hosting mailboxes
on-premises and accessing files typically requires a VPN tunnel to keep company
data secure.

1. You should still be logged into LON-EX1 from the prior exercise; if
    necessary, log in as the **Administrator** with a password of **Pa55w.rd**.

2. In your **Edge browser**, you should have the two **Exchange admin center**
    (EAC) tabs open from the prior exercise – one for the on-premises EAC and
    one for the EAC for Exchange Online.

    Select the **send connectors – Microsoft Exchange** tab to display the on-premises EAC.

3. In the on-premises **Exchange admin center**, in the left-hand navigation
    pane, select **servers**, then select the **virtual directories** tab.

4. In the **virtual directories** tab, you should see a list of virtual directories you created earlier on in this lab (Exercise 1 step 4). Find and select the **EWS (Default Web Site)** entry you created and select the pencil icon to edit.

5. In the new page that opens, you should be on the general tab by default, ensure that the last option, **Enable MRS Proxy endpoint**, is enabled (marked by a check box), then select **Save**.

6. Switch over to the **Message trace - Exchange admin center** to switch to Exchange Online EAC, which should still be open from the previous exercise, In the left hand navigation pane, select **Migration**.

7. On the **Migration batches** page that opens up, select **Add migration batch**.

8. The **Add a migration batch** wizard will open on a new page. Under the **Give migration batch a unique name** field enter **Migrating Allan Yoo**, then in the **Select the mailbox migration path** field select **migration to Exchange online**, and then select **Next**.

9. On the **Select the migration type** page, choose **Remote move migration** and then select **Next**

10. On the **Prerequisites for remote migration** page, select **Next**.

11. On the **Set a migration endpoint** field choose **Create a new migration endpoint**, and then select **Next**.

    The migration endpoint contains the connection settings for an on-premises Exchange server that is running the MRS proxy service, which is required to perform remote move migrations to and from Exchange Online. Since this is your first migration, we will proceed with the steps of creating a migration endpoint that could be used for future mailbox migrations from Exchange On-premises to Exchange Online.

12. On the **On-premises account credentials** page configure the following settings and then select  **Next**:
     - Migration Endpoint name - enter **Hybrid Migration**
     - Account with privileges - enter **Adatum\Administrator**.
     - Password of account with privileges - enter **Pa55w.rd**.
     - Remote MRS Proxy server - enter **xxxUPNxxx.xxxCustomDomainxxx.xxx** (where xxxUPNxxx is the unique UPN Name and xxxCustomDomainxxx.xxx is the custom domain name, both of which were provided by your lab hosting provider).

13. On the **Confirm the migration endpoint** page, leave both **maximum concurrent migrations** and **maximum concurrent incremental syncs** at their default values, and then select **Next**.

14. On the **Check endpoint setup status** page, once completed you will see **New endpoint Hybrid Migration created**, then select **Next**.

    **IMPORTANT:** If this step fails, ensure that you entered the details correctly on step #12. If you continue to fail, by default a migration endpoint named **Hybrid Migration Endpoint - EWS (Default Web Site)** should already exist. Instead of creating the Endpoint Manually, you can go back to step #11 and select this Migration Endpoint and skip to step #15.

15. On the **Add user mailboxes** page, select **Manually add users to migrate** and search for **Allan@xxxUPNxxx.xxxCustomDomainxxx.xxx** (where xxxUPNxxx is the           unique UPN Name and xxxCustomDomainxxx.xxx is the custom domain name, both of which were provided by your lab hosting provider), Once Allan's mailbox is added select next.

16. On the **Move configuration** page, under the **Target delivery domain** there should only be one option to choose from, select **xxxxxZZZZZZ.mail.onmicrosoft.com**     (where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting provider), and select Next.

17. On the **schedule batch migration** page, choose  **Automatically start the batch** and **Automatically complete the migration batch**.

    The default admin account populated in the first field can be left for sending reports to. Once finished select save.

    In the real world, you would rarely be migrating a users mailbox during business hours. However, for the purposes of this lab we want to start and finish this migration immediately. On this page, you would be able set delayed starts and completions for your batch migration to match business needs.

18. on the **status** page, wait until you see **batch creation successful!**, then select done.

19. After selecting done, you will be brought back to the **Migration batches** page within the **Exchange admin center** where you can monitor the status of the of the migration. The Status column will begin by displaying Syncing, and eventually it will change to Completed.

    **IMPORTANT:** Migrating an on-premises mailbox to Microsoft 365 can take up to an hour to complete. Therefore, once you have finished this task, proceed to the Final Assessment lab. Once you have finished the final assessment, return to this lab exercise and perform Task 3 to test the newly migrated mailbox.

## Task 3: Test the newly migrated mailbox

The prior exercise migrated Allan Yoo’s on-premises mailbox to Microsoft 365. In
this task, you will validate whether Outlook features are working properly for
Allan’s new Microsoft 365 mailbox. When testing in a real-world environment,
ensure that mail flow isn’t impeded, and that the user can access his or her
mail by going to **outlook.office365.com**. This ensures that no complications
occurred during the migration process. As a best practice, you should always
test your mail flow to validate a migration.

In this task, you will test mail flow by sending an email from Allan’s new
Microsoft 365 mailbox to Beth Burke’s on-premises mailbox (which you created in
the prior lab exercise). You will also send meeting requests from Allan to Beth.
This task will verify whether your connectors are correctly set up.

1. You should still be logged into LON-EX1 after having completed the Final
    Assessment lab; if necessary, log in as the **Administrator** account with a
    password of **Pa55w.rd**.

2. On the **Migration batches** page, monitor the status of the migration. The
    **Status** column will begin by displaying **Syncing,** and eventually it
    will change to **Completed**.  

    **IMPORTANT:** You cannot perform this task until the mailbox migration is
    complete. If the migration did not complete while you were working on the
    Final Assessment lab, then you must wait until it finishes before
    proceeding.  

    **Note:** You can select your migration batch and in the Details pane on the right side of the screen to see more
    information on the migration. The Details pane that appears also displays
    the batch status. However, please note that this status is NOT the same as
    the status that displays on the **Migration batches** window in the EAC for Exchange
    Online. The Details pane status is reflective of the objects being moved
    from on-premises to the cloud, so while this status may display
    **Completed**, that does NOT mean the migration is complete. In fact, this
    Details pane may indicate **Completed,** but the status on the migration
    window can still show **Syncing**. The reason for this is that even after
    the objects are moved, there are still several additional tasks that the
    migration must perform before it’s complete.  

    In summary, you should NOT proceed to the next task until the
    status on the **Migration batches** window displays **Completed** for your batch.  

3. Since you just completed the Final Assessment lab prior to returning to this
    task, you should have Beth Burke’s on-premises mailbox open in your Edge
    browser session, and you should have Alex Wilber’s Microsoft 365 mailbox
    open in an InPrivate Browsing session. Therefore, you must close Alex’s
    mailbox and open Allan’s mailbox in the InPrivate Browsing session.  

    You should begin by logging out of Microsoft 365 as Alex Wilber. Hover your
    mouse over the Edge browser icon on the taskbar, select Alex’s mailbox tab
    in the InPrivate Browsing session. On Alex’s mailbox, select Alex’s user
    icon in the upper right corner of the screen and select **Sign out**.  

     Once you are signed out as Alex, close the Microsoft Office Home tab in your
    InPrivate Browsing session.

4. On the **Sign out** tab in the InPrivate Browsing session, browse to
    **<https://outlook.office365.com>.** On the **Pick an account** window, select
    **Use another account.** On the **Sign in** window, enter
    **Allan@xxxUPNxxx.xxxCustomDomainxxx.xxx** (where xxxUPNxxx is your unique

    UPN Name and xxxCustomDomainxxx.xxx is the accepted domain) and then select
    **Next**. On the **Enter password** window, enter **Pa55w.rd** and then
    select **Sign in**.

5. If prompted, select your **Language** and **Time zone** and then select
    **Save**.

6. If a **Welcome** window appears, then close it.

7. You are now signed into Allan’s mailbox that was just migrated from the
    on-premises LON-EX1 Exchange Server to Microsoft 365. Note the emails in
    Allan’s Inbox; these were messages he received when the mailbox was still
    on-premises. This verifies that his messages were migrated to Microsoft 365
    along with his mailbox.  

    Create a new test email and send it to **Beth Burke**. Beth’s email address
    is **Beth@xxxUPNxxx.xxxCustomDomainxxx.xxx** (where xxxUPNxxx is your
    unique UPN Name and xxxCustomDomainxxx.xxx is the accepted domain).

8. At this point, you must log into Beth Burke’s on-premises mailbox to verify
    she received the email from Allan Yoo’s Office 365 mailbox. You then want to
    send a reply from Beth’s on-premises mailbox back to Allan’s Office 365
    mailbox.  

     **Note:** In the Final Assessment lab that you just completed, you opened
    Beth’s on-premises mailbox to test your final assessment lab solution. Hover
    your mouse over the Edge browser icon on the taskbar and select Beth’s
    mailbox.  

     However, if you closed Beth’s mailbox after the Final Assessment lab, then
    open it again in your Edge browser session (not in the InPrivate Browsing
    session that has Allan’s mailbox open) by navigating to
    **<https://xxxUPNxxx.xxxCustomDomainxxx.xxx/owa>** and signing in as
    **adatum\\beth** with a Password of **Pa55w.rd.**

9. The email that Allan just sent to Beth should appear in her **Inbox**. Open
    the email and reply to the message.

10. Hover over the **Edge browser** icon on the taskbar and select the InPrivate
    Browsing session that displays **Allan’s** Microsoft 365 mailbox. If Beth’s
    reply does not appear in Allan’s **Inbox**, then refresh the Inbox.  

    Seeing Beth’s reply verifies that mail flow is working properly between an
    on-premises mailbox and Allan’s newly migrated Microsoft 365 mailbox.

11. You will now test whether Calendar functionality is working properly in
    Allan’s new Microsoft 365 mailbox. In Allan’s mailbox, select the
    **calendar** icon in the upper-left corner of the window.

12. Create a new meeting with a subject **Test meeting**.

13. Add **Beth Burke** as a required meeting attendee, then select **Scheduling
    Assistant**.

14. Both Allan and Beth’s calendars will be displayed, and they should both show
    that their respective user is free. Select **Done** to accept the time and
    then select **Send** to send the meeting request to Beth.

15. Hover over the **Edge browser** icon on the taskbar and select **Beth’s**
    on-premises mailbox.

16. In Beth’s Inbox, **Accept** the meeting request and select **Send the
    response now**.

17. Hover over the **Edge browser** icon on the taskbar and select the InPrivate Session that’s displaying **Allan’s** calendar. Select the meeting on Allan's calendar and verify that Beth has accepted meeting request.

18. Create another meeting request with a subject of **Test 2**. Add **Beth
    Burke** as a meeting attendee again, then select **Scheduling Assistant**.  

    Beth’s calendar should show her as busy for the first meeting request.
    Select **Discard** to close the Scheduling Assistant, select **Discard** to
    cancel the meeting request, and then select **OK** to confirm the
    cancellation.  

    You have now verified that the mail flow is functioning properly between a
    newly migrated Microsoft 365 mailbox (Allan) and an on-premises mailbox
    (Beth). From within Allan’s calendar, you can also access Beth’s calendar to
    see her status when creating a meeting request. This verifies that your
    connectors are correctly set up.  

**CONGRATULATIONS!** You have completed all the labs in this course!
