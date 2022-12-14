---
lab:
    title: 'Create Hygiene Filters'
    learning_path: 'Learning Path 3: Manage message security'
    module: 'Module 2: Manage anti-malware and anti-spam policies'
---

# Lab 3 - Exercise 1 - Create Hygiene Filters

In this lab, you will continue in your role as Holly Dickson, Adatum’s Messaging
Administrator. Adatum has experienced a recent rash of malware infections. The
company's CTO has asked Holly to investigate the various options that are
available in Exchange Online to fortify Adatum’s messaging environment. Holly
will begin by creating a series of hygiene filters that are designed to protect
Adatum’s messaging environment. You will create a malware filter, a connection
filter, and a spam filter.

**Note**: In this lab exercise, you will use **Microsoft 365 Defender** to create hygiene filters. Protection services no longer
reside in the EAC for Exchange Online, and instead have been moved to the
Microsoft 365 Defender portal.

## Task 1 - Create a Malware Filter

In this task, you will create a malware filter that checks for attachments that
have a specific file type that indicate a possible malware attachment. If an
attachment is found matching one of those file types and the recipient’s domain
matches Adatum’s Microsoft 365 domain, then a notification message will be
applied to the email.

**Warning:** To create malware filter policies, you must be assigned the Organization Management role, which you will assign to the MOD administrator account at the start of this task. However, it sometimes takes an hour or so for the role permissions to propagate through the system. This is due to the replication process that occurs within the system. In the Microsoft data centers, certain objects are consolidated to save space. You may encounter this delay when you assign RBAC roles in Microsoft 365 Defender, or when you use Exchange Online PowerShell or the Exchange admin center to change one of these objects for the first time.

Therefore, when you create the malware policy later in this task and you attempt to save the filter, you may receive a Client Error that indicates an error occurred when creating the policy. This error occurs because the Organization Management permissions haven’t fully propagated through the system for the MOD Administrator. To work around this, you will be provided with PowerShell instructions that will enable you to customize organization management objects.

1. You should still be logged into LON-CL1 as the **Administrator** with a
    password of **Pa55w.rd**; however, if the log-in page appears, then log in
    now.

2. In your **Edge** browser, you should still have a tab open for the
    **Microsoft 365 admin center**. If so, then select this tab and proceed to
    the next step; otherwise, navigate to the **Office 365 home** page, log in
    as your tenant admin account, navigate to the **Microsoft 365 admin
    center**, and then in the left-hand navigation pane, select **Show all**.

3. In the **Microsoft 365 admin center**, in the left-hand navigation pane under **Admin centers**, select **Security**. This opens **Microsoft 365 Defender** in a new tab.

4. In the **Microsoft 365 Defender** portal, scroll down to the last section in the left-hand
    navigation pane and select **Permissions**.

5. In the **Permissions** page, under the **Email & collaboration roles** group, select **Roles**.

6. In the **Permissions > Permissions** page, enter **org** in the **Search** field
    and then select the magnifying glass icon. This is a quick way to display
    the Organization Management role group so that you don’t have to scroll
    through a list of roles to find it.

    The search will display the **Organization Management** role, which is the
    only role starting with **org**. Select the check box next to this role to
    display the details for this role group.

7. In the **Organization Management** pane that appears on the right, scroll
    down to the **Members** section at the bottom of the pane. To the right of the
    **Members** section, select **Edit**.

8. On the **Editing Choose members** page, select **Choose members**.

9. On the **Choose members** page, select the **+Add** button.

10. In the **Choose which members to add from the list below** field, enter **MOD**. This will display all accounts starting with MOD. Select the check box next to **MOD Administrator** and then select the **Add** button.

11. On the **Choose members** page, MOD Administrator should appear in the list of members
    who will be assigned to this role group. Select **Done**.

12. On the **Editing Choose members** page, select **Save**.

13. On the **Organization Management** pane, MOD Administrator should now appear as the only member of this role group. Select **Close**.

14. In **Microsoft 365 Defender**, in the left-hand
    navigation pane, under the **Email & collaboration** section, select **Policies & rules**.

15. In the **Policies & rules** page, select **Threat policies**.

16. In the **Threat policies** page, under the **Policies** section, select **Anti-malware**.

17. In the **Policies & rules > Threat policies > Anti-malware** page, on the menu bar at the top
    of the window, select **+Create** to add a new malware filter. This starts
    the **Create a new anti-malware policy** wizard.

18. In the **Name your policy** page, enter **Malware Policy** in the **Name**
    field.

19. In the **Description** field, enter **This policy has been created to
    protect Adatum’s messaging environment** and then select **Next**.

20. In the **Users and domains** page, enter **onmicrosoft.com** in the
    **Domains** field. This will display the list of Adatum domains containing
    **onmicrosoft.com**. Select the **M365xZZZZZZ.onmicrosoft.com** domain
    that’s displayed and then select **Next**.

21. On the **Protection settings** page, under the **Protection settings**
    group, select the check boxes for the following settings:

    - **Enable the common attachments filter** (if it’s not already selected)
    - **Enable zero-hour auto purge for malware (recommended)**.

22. In the **Notification** section, do not select any of the notification
    options since this filter will not generate any notifications. Select **Next**.

23. On the **Review** page, review all the information for this malware policy.
    If anything needs to be changed, select the **Back** button and make the
    necessary corrections. When all the information is correct, select
    **Submit**.

24. If the anti-malware policy was successfully created, then skip to the next
    step.  

    However, if you receive a **Client Error** dialog box that indicates an
    error occurred when creating the policy, then the permissions assigned to
    Holly through the Organization Management role haven’t fully propagated
    through the system. For this lab, instead of waiting an hour or so for this
    permission replication to occur, select **OK** in this dialog box and then
    perform the following PowerShell commands that will enable you to customize organization
    management objects. Once you’ve completed these steps, you will resubmit the
    **Review** page to save the malware policy that you just created.

    1. On LON-CL1, you must open an elevated instance of **Windows
        PowerShell**. Select the magnifying glass (Search) icon on the taskbar
        at the bottom of the screen ad type **powershell** in the Search box
        that appears. In the list of search results, right-click on **Windows
        PowerShell** (do NOT select Windows PowerShell ISE) and select **Run as
        administrator** in the drop-down menu.

    2. Maximize your PowerShell window. In Windows PowerShell, at the command
        prompt, type the following command and press Enter:

        `Install-Module -name ExchangeOnlineManagement`

    3. If you are prompted to confirm whether you want to install the module from
    an untrusted repository (PSGallery), enter **A** to select **[A] Yes to
    All.**

    4. At the command prompt, type the following command and press Enter:

        `Connect-ExchangeOnline`

    5. A **Microsoft 365 Sign in** window will appear. Enter in the username for
    the **Mod Administrator** account provided by your learning provider
    (admin@M365xZZZZZZ.onmicrosoft.com) and then select **Next**.

    6. In the **Enter password** window, enter the password for this admin account
    provided by your learning provider, and then select **Sign in**. It may take
    a moment to sign in before it returns a command prompt.

    7. At the command prompt, type the following command and press Enter:

        `Enable-OrganizationCustomization`

    8. Close the PowerShell window.

    9. Return to your **Edge** browser and the **Review** page for your new
    anti-malware policy. Select **Submit** to resubmit your anti-malware policy.
    This time the policy should be successfully saved.

25. On the **Created new anti-malware policy** page, it indicates the new policy
    has been created and will go into effect immediately. Select **Done.**

     **Note**: If a dialog box appears with a message that
    indicates your organization settings need to be updated, select **Yes** to
    continue. It may take a minute for your organization settings to be updated.

26. Leave your browser open for the next task.

## Task 2 - Create a Connection Filter

In this task, you will modify the default connection filter to include an
allowed IP address and a blocked IP address. Any messages originating from the
allowed IP address will always be accepted, and any messages originating from
the blocked IP address will always be blocked.

1. You should still be logged into Microsoft 365 as the MOD Administrator after completing the prior task. Your Edge browser should still be in the **Microsoft 365 Defender** portal on the **Policies & rules > Threat policies > Anti-malware** window.

2. In the the **Policies & rules > Threat policies > Anti-malware** thread at the top of the page, select **Threat policies**.

3. In the **Threat policies** window, under the **Policies** section, select
    **Anti-spam**.

4. The **Policies & rules > Threat policies > Anti-spam policies** window displays a list of
    default **Anti-spam policies** that control how messages are handled by
    Microsoft 365 anti-spam policies.

    In the list of policies, select the **Connection filter policy (Default)**.
    This displays the current settings for this default spam filter in the
    right-hand pane.

5. In the **Connection filter policy (Default)** pane, the **Connection
    filtering** section displays options regarding which IP Addresses may send
    messages to your environment and what IP addresses will be blocked from
    sending messages.

    You will NOT be adding IP addresses to the allow or block lists. You can do
    this if you have a known IP address you would like to test against. It
    typically takes up to 1 hour to propagate the change within the system. For
    this lab, simply review the fact that you can create allowed and blocked
    lists of IP addresses.

6. At the bottom of the **Connection filtering** section, select the **Edit
    connection filter policy** link.

7. In the **Connection filter policy (Default)** pane, select the **Turn on
    safe list** check box. This is a best practice that enables for your tenant the most common third-party sources of trusted senders that Microsoft
    subscribes to. Selecting this check box skips spam filtering on messages
    sent from these senders, ensuring they are never mistakenly marked as spam.

8. Select **Save** to save this filter, and then select **Close** once the
    changes are successfully saved.

9. Leave your Edge browser open to the **Microsoft 365 Defender** portal for the next task.

## Task 3 - Create a Spam Filter

For Microsoft 365 customers whose mailboxes are hosted in Microsoft Exchange
Online, their email messages are automatically protected against spam and
malware. Microsoft 365 has built-in malware and spam filtering capabilities that
help protect inbound and outbound messages from malicious software and help
protect users from receiving spam messages.

As Adatum’s Messaging Administrator, Holly doesn't need to set up or maintain
the filtering technologies, which are enabled by default. However, she can make
company-specific filtering customizations in the Exchange admin center. She has
decided to test this out by configuring a spam policy to grant or deny an email
by focusing on the language of the email and the location of the email's origin.

1. In the **Microsoft 365 Defender** portal, the **Policies & rules > Threat policies > Anti-spam policies** window should still be displayed after having completed
    the prior task.

    In the list of anti-spam policies, select the **Anti-spam inbound policy (Default)**.

2. In the **Anti-spam inbound policy (Default)** pane that appears, take a
    moment and review the policy settings that are available in this filter.
    There are three sections of settings – **Bulk email threshold & spam
    properties**, **Actions**, and **Allowed and blocked senders and domains**.

3. Once you’ve finished reviewing these settings, scroll to the bottom of the
    **Bulk email threshold & spam properties** section and select the **Edit
    spam threshold and properties** link.

4. In the **Spam threshold and properties** pane that appears, the **Bulk email
    threshold** at the top of the pane is set to **7** by default. Drag the slider to the left on the slider bar and change this value
    to **5.**

5. Under the **Mark as spam** section, update the following settings:

    - Empty messages: **Off**

    - Embedded tags in HTML: **On**

    - JavaScript or VBScript in HTML: **On**

    - SPF record hard fail: **On**

    - Sender ID filtering hard fail: **On**

    **Note:** These next two settings allow you to automatically tag messages
        as spam when they originate from countries/regions that are to be
        avoided or distrusted, as well as messages written in specific languages.

    - Contains specific languages: **On**  

        You should already know the languages that you want to filter. In the
        blank field that appears below the **Contains specific languages**
        field, enter the first letter of a language that you want to filter.
        This will display all languages that start with that letter (as well as
        any languages that contain that letter within the name of the language).

        Enter a letter and then select a language with the letter in it that you
        want to filter. Repeat this step for a couple of languages.

    - From these countries: **On**

      You should already know the countries that you want to filter. In the
        blank field that appears below the **From these countries** field, enter
        the first letter of a country that you want to filter. This will display
        all countries that start with that letter (as well as any countries that
        contain that letter within the name of the language).

      Enter a letter and then select a country with the letter in it that you
        want to filter. Repeat this step for a couple of countries.

6. Leave all other settings as default, and the select **Save**.

7. This returns you to the **Anti-spam inbound policy (Default)** pane. Scroll
    to the bottom of the **Actions** section and select the **Edit actions**
    link.

8. In the **Actions** pane, update the following settings:

    - Spam: **Move message to Junk Email folder**

    - High confidence spam: **Prepend subject line with text**

    - Phishing email: **Quarantine message**

    - High confidence phishing email: **Quarantine message**

    - Bulk complaint level (BCL) met or exceeded: **Move message to Junk Email folder**

    - Retain spam in quarantine for this many days: **10**

    - Prepend subject line with this text: enter **WARNING: This message
        contains potential spam!**

    - Enable spam safety tips: select this check box

9. Select **Save** to update the settings, and then select **Close** to close
    the **Anti-spam inbound policy (Default)** pane.

10. In your Edge browser, leave the **Office 365 Home** tab open as well as the **Microsoft 365 admin center** tab. Close all other tabs and proceed to the next lab.

## End of Lab 3
