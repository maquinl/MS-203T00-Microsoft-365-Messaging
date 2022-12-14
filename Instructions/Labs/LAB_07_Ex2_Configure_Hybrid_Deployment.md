---
lab:
    title: 'Configure your Hybrid Deployment'
    module: 'Learning Path 8: Manage the hybrid deployment life cycle'
---

# Lab 7 - Exercise 2 - Configure Your Hybrid Deployment

In this lab you will continue in your role as Holly Dickson, Adatum’s Messaging
Administrator. Adatum has decided to transition from their current on-premises
Exchange Server 2019 deployment to a hybrid deployment that also utilizes
Microsoft 365 Exchange Online.

In the prior lab, you prepared Azure Active Directory to support the hybrid
synchronization between Adatum’s on-premises Exchange Server 2019 environment
and their cloud-based Exchange Online deployment. In this lab, you will set up
Exchange for a hybrid deployment. This will require that you:

- Run the Hybrid Configuration Wizard (HCW) to create your hybrid deployment

- Configure Exchange admin center (EAC) settings to accommodate cloud and
    on-premises users within the same domain

- Configure the Outbound Connector from Microsoft 365 to your Exchange Server

To set up Exchange for a hybrid deployment, you must first run the Hybrid
Configuration Wizard on your Exchange Server (LON-EX1). Once your hybrid
deployment is installed, you will then test your hybrid deployment in the next
exercise to verify that it’s functioning properly.

## Task 1: Create Adatum’s Hybrid Exchange deployment

In this task, you will download and install the Hybrid Configuration Wizard
(HCW) on the Exchange Server (LON-EX1) using the Exchange admin center for
Exchange Online. Running the HCW will create Adatum’s hybrid deployment.

1. Switch to **LON-EX1** and, if necessary, log in as the **Administrator**
    account with a password of **Pa55w.rd**.

2. Select the Microsoft Edge icon on the taskbar to open a new browser session,
    then enter the following URL in the address bar: **<https://portal.office.com>**

3. In the **Sign in** window, enter your tenant admin username
    (admin\@xxxxxZZZZZZ.onmicrosoft.com, where xxxxxZZZZZZ is the tenant prefix
    provided by your lab hosting provider) and select **Next**.  

    In the **Enter password** window, enter the tenant admin password provided
    by your lab hosting provider and then select **Sign in**.

4. In the **Stay signed in?** window, select the **Don’t show this again**
    check box and select **Yes**.

5. In the **Microsoft Office Home** page, in the column of Microsoft app icons
    on the left-side of the screen, select the **Admin** icon.

6. In the **Microsoft 365 admin center**, select **Show all** in the left-hand
    navigation pane and under **Admin centers**, select **Exchange**. This will
    open the EAC for Exchange Online.

7. In the **Exchange admin center** for Exchange Online, select **Classic Exchange admin center** from the left-hand navigation pane, this will display the **dashboard** tab
    in the left-hand navigation pane by default, which displays the
    **Welcome** page.

    Scroll to the bottom of the **Welcome** page and select **setup** under **hybrid**.

8. On the **setup** page there are two **configure** buttons. The first button
    configures an Exchange hybrid deployment, while the second button downloads the Exchange Online PowerShell module for supporting
    Multi-factor authentication.  

    Select the first **configure** button to configure Adatum’s hybrid
    deployment.

9. A new tab will open in your Edge browser, and in the **Open this file?**
    window that appears at the top of the page, select **Open**.

    This will initiate the **Application Install** wizard, which will download and install the Hybrid Configuration Wizard.

10. If the wizard begins and a **Do you want to install this application?**
    window appears, then proceed to the next step.  

    However, because of security features in the VMs within your lab hosting
    environment, this wizard may not appear. Instead, when you select the
    **configure** button, the system may open a new tab, try to access a site,
    then close the tab and return to the **setup** page with the two
    **configure** buttons. If this occurs, then you must perform the following
    steps to open an **InPrivate Browsing** session within Edge to
    bypass the security constraints built into your training lab environment
    (this would not occur in a real world scenario). You will then open the
    Microsoft 365 admin center and initiate the hybrid deployment process.

    - To open an InPrivate Browsing session, right-click the **Edge browser**
        icon on the taskbar and in the menu, select **Start InPrivate
        Browsing**. This will open a new, InPrivate Edge session that is
        separate from the Edge session that you were just in.

    - Maximize the InPrivate browser window (if necessary), repeat steps 2
        through 9, and then continue with the next step to install the Hybrid
        Configuration Wizard.  

11. In the **Application Install** wizard, on the **Do you want to install this
    application?** window, select **Install** to download the Hybrid
    Configuration Wizard.

12. After the download completes, on the **Hybrid Configuration Wizard** window,
    select **next** to run the wizard.  
  
    This starts the **Hybrid Configuration Wizard** (it can sometimes take up to
    a minute or so for the setup wizard to start, so please be patient).

13. The wizard begins by trying to detect the on-premises Exchange Server. Wait
    for the server detection to complete, which then displays the **On-premises
    Exchange Server Organization** window. The **Detect the optimal Exchange
    server** option will be selected by default, and the wizard will detect the
    **LON-EX1** server.  

    Accept the default settings by selecting **next**.

14. The next page displays the **On-premises Exchange Account** and the **Office
    365 Exchange Online Account**.  

    Under the **Office 365 Exchange Online Account** section, select the **sign
    in…** button.

15. In the **Sign in** window, enter the tenant email account provided by your
    lab hosting provider (**admin\@xxxxxZZZZZZ.onmicrosoft.com**; in a
    real-world scenario, this must be a Microsoft 365 user who has been assigned
    the Global Admin role) and then select **Next**.  

    In the **Enter password** window, enter the tenant email password provided
    by your lab hosting provider and then select **Sign in**.

16. This returns you to the **On-premises Exchange Account** page, which now
    displays the **Tenant Email** account that you entered for the **Office 365
    Exchange Online Account**.

    Once the account appears (which may take a few seconds), select **next**.

17. On the **Gathering Configuration Information** page, wait until the
    information gathering process is complete for both **Exchange**
    (on-premises) and **Office 365** (Exchange Online). Once both indicate they
    have **Succeeded** (which may take a minute or two), select **next**.

18. On the **Hybrid Features** page, select the **Full Hybrid Configuration**
    option and then select **next**.

19. On the **Hybrid Topology** page, the **Use Exchange Classic Hybrid
    Topology** option is selected by default.  

    **Note:** We want you to use this **Classic** option instead of the
    **Modern** option so that you gain experience creating the necessary
    connectors in this wizard. The Modern option uses an agent to create the
    connectors between Exchange on-premises and Exchange Online, whereas the
    Classic option still configures the connectors, but does not use an agent to
    do so. In addition, since we are using published endpoints through the
    Domain Controller, it’s preferable to use the Classic option. If we used a
    third-party such as GoDaddy, then the Modern option would be preferable.  

    Verify the **Use Exchange Classic Hybrid Topology** option is selected and
    then select **next**.

20. On the **On-premises Account for Migration** page, select the **enter…**
    button to enter the credentials to your on-premises Exchange Web Service.

21. In the **Office 365** window that appears, the **Domain\\username** is
    already prefilled with the **ADATUM\Administrator** account. Enter
    **Pa55w.rd** in the **Password** field and then select **ok.**

22. On the **On-premises Account for Migration** page, the
    **ADATUM\Administrator** account is displayed, so select **next**.

23. On the **Hybrid Configuration** page, verify the **Configure my Client
    Access and Mailbox servers for secure mail transport (typical)** option is
    selected by default (select it if necessary) and then select **next**.

24. On the **Receive Connector Configuration** page, select the drop-down arrow.
    This displays the **LON-EX1** server. Select the check box for this server
    and then select **next**.

25. On the **Send Connector Configuration** page, select the drop-down arrow.
    This displays the **LON-EX1** server. Select the check box for this server
    and then select **next**.

26. On the **Transport Certificate** page, select the drop-down arrow. This
    displays several existing certificates. Select the
    \***.xxxCustomDomainxxx.xxx** certificate (where xxxCustomDomainxxx.xxx is
    the lab hosting provider’s custom domain name) and then select **next.**

27. On the **Organization FQDN** page, enter
    **xxxUPNxxx.xxxCustomDomainxxx.xxx** (where xxxUPNxxx is your unique UPN
    name assigned to your tenant by your lab hosting provider and
    xxxCustomDomainxxx.xxx is your lab hosting provider’s custom domain) and
    then select **next**.

28. On the **Ready for Update** page, select **update.**

29. This initiates the configuration process, which usually takes a few minutes
    to complete.

    - If the configuration is successful, you will receive a
        **Congratulations!** page that indicates hybrid services are now
        configured between Exchange Online in your Office 365 tenant and your
        on-premises Exchange environment. If you receive this window, then
        select **close.**

    - If the configuration fails, it’s typically the result of an **Access is
        Denied** error. As you just saw, there are several pages in the setup
        wizard that require you to enter username and password credentials. The
        wizard does not validate the credentials at the time you enter them;
        rather, it simply stores them and then validates the credentials in this
        final configuration step. Experience has shown that an **Access is
        Denied** error is usually the result of entering an incorrect username
        and/or password (for example, if you copy and paste in a username or
        password, copying in a trailing space after the username or password
        will cause it to fail).

        **IMPORTANT:** If you receive an **Access is Denied** error (or any
        error), you can simply repeat this entire task and re-run the Hybrid
        Configuration Wizard, which has been designed to allow multiple re-runs
        without negatively affecting the system.  

30. If you had to open an InPrivate browsing session to run the HCW, then close
    the InPrivate session.

31. In your Edge browser, close all tabs except for the **Microsoft Office
    Home** tab, the **Microsoft 365 admin center** tab, and the **Exchange
    admin center** tab.

## Task 2: Configure Mail Flow Settings

In this task, you will configure mail flow settings in both the on-premises
Exchange admin center (EAC) and the EAC for Exchange Online. First, you will log
into the Exchange Server (LON-EX1) VM and then, through the on-premises EAC, you
will configure the onmicrosoft.com domain so that on-premises users can send
emails to cloud users within the same domain.

Second, you must verify the default settings in the Microsoft 365 EAC so that
emails from cloud users to on-premises users in the same domain do not get stuck
in an internal loop and never make it to their recipients’ on-premises
mailboxes.

**IMPORTANT:** You will open BOTH Exchange admin centers in this task in your
LON-EX1 VM. Once you finish this task, you will leave both EAC’s open on LON-EX1
for future tasks in this exercise.

1. You should still be logged into LON-EX1; if necessary, log in as the
    **Administrator** with a password of **Pa55w.rd**.

2. Select the **Windows** icon on the taskbar and in the menu that appears,
    select the **Microsoft Exchange Server 2019** group. In the expanded group,
    select **Exchange Administrative Center**.  

    This will open a new tab in your current Edge browser session that will display the on-premises Exchange admin center.

    **Note:** If you receive a page indicating **Your connection isn’t
    private**, this is due to a certificate issue in the VM environment that you
    can ignore for the purpose of this lab. To bypass this error, select the
    **Advanced** button, and then select **Continue to localhost (unsafe)**.

3. In the on-premises **Exchange Admin Center**, log in as **adatum\\Administrator** with a
    password of **Pa55w.rd**.

4. In the on-premises **Exchange admin center**, select **mail flow** in the
    left-hand navigation pane, and then select the **accepted domains** tab at
    the top of the page.

5. In the list of accepted domains, select the
    **xxxxxZZZZZZ.mail.onmicrosoft.com** domain (where xxxxxZZZZZZ is the tenant
    prefix provided by the lab hosting provider).

6. Note the **Domain Type** for this onmicrosoft.com domain is set to **Authoritative**. You must change
    it to **Internal relay**. To do so, select the **pencil (Edit)** icon on the
    menu bar above the list of domains.

7. In the **xxxxxZZZZZZ.mail.onmicrosoft.com** window that appears, under the **This
    accepted domain is:** setting, select the **Internal relay** option and then
    select **Save**.

8. On the **mail flow** page, select the **send connectors** tab that appears
    at the top of the page.

9. In the list of send connectors, select the **Outbound to Office 365**
    connector and then select the **pencil (Edit)** icon on the menu bar.

10. On the **Outbound to Office 365** send connector window that appears, select the
    **scoping** tab in the left-hand navigation pane.

11. Under the **Address space** group at the top of the page, select the **plus
    (+) sign** icon to add the accepted domain.

12. In the **add domain** window, in the **Full Qualified Domain Name (FQDN)**
    field, enter \***.xxxCustomDomainxxx.xxx** (where xxxCustomDomainxxx.xxx is
    the lab hosting provider’s custom domain name) and then select **Save.**

13. In the **Outbound to Office 365** send connector page, select **Save**.

14. You are currently in the on-premises EAC. You should also have the EAC for Exchange Online open in your Edge browser from the prior task (see the **Exchange admin center** tab); if so, select this tab (which should be the New Exchange Admin center).

    However, if you closed the EAC for Exchange Online at the end of the prior
    task, then open it again by entering the following URL (this shortcut saves
    you from navigating to the Office 365 home page, then to the Microsoft 365
    admin center, and then to the EAC): **<https://admin.exchange.microsoft.com>**

15. In the **Exchange admin center** for Exchange Online, in the left-hand
    navigation pane, select **mail flow**.

16. In the expanded group, select **Accepted domains**.

17. In the list of accepted domains, select the
    **xxxUPNxxx.xxxCustomDomainxxx.xxx** domain (this is the accepted domain
    that you added in the prior lab exercise) and then select the domain.

18. In the **xxxUPNxxx.xxxCustomDomainxxx.xxx** pane that opens, under the **This accepted domain is:** setting, select the **Internal relay** option, select
    **Save**, and then close the pane.

19. in the **mail flow** expanded group, select **Connectors**.  

    **Note:** There are several differences between the on-premises EAC and the
    EAC for Exchange Online. In the on-premises EAC, the
    **connectors** tab is split out into a separate **receive connectors** tab
    and a separate **send connectors** tab. In the EAC for Exchange Online that you are currently viewing,
    only one **connectors** tab is available.

20. In the **connectors** tab, the list of connectors displays an **Inbound**
    and **Outbound** connector. Select the **Inbound** connector.

21. in the **Inbound** Connector pane that opens, under the **How to identify email sent from your email server**, select **Edit sent email identity**.

22. On the **Authenticating sent email** page, verify the option is selected that states: **By verifying that the subject name on the certificate that the
    sending server uses to authenticate with Office 365 matches the domain entered in the text bos below (recommended).**  

    You should also verify that \***.xxxCustomDomainxxx.xxx** is displayed in
    the corresponding domain name field below this **“By verifying…”** option
    (where xxxCustomDomainxxx.xxx is the lab hosting provider’s custom domain
    name); if not, you should enter this \***.xxxCustomDomainxxx.xxx** now.

23. Close the connector window.

24. Leave the two Exchange admin center tabs open in your Edge browser session
    and proceed to the next task.  

## Task 3: Create on-premises user mailboxes for testing

In this task, you will remain in your Exchange Server (LON-EX1) VM, navigate to
the on-premises Exchange admin center, and then create on-premises mailboxes for
Allan Yoo and Beth Burke. You will later use Allan and Beth to test your hybrid
deployment.

1. You should still be logged into LON-EX1; if necessary, log in as the
    **Administrator** with a password of **Pa55w.rd**.

2. In your **Edge browser**, you should have the two **Exchange admin center**
    (EAC) tabs open from the earlier tasks in this exercise – one for the
    on-premises EAC and one for the EAC for Exchange Online.

    - One EAC tab should be titled **send connectors – Microsoft Exchange**.
        This is the on-premises EAC. Select this tab and note that in the
        left-hand side of the blue bar at the top of the page, it displays
        **Enterprise** and **Office 365**. This will help you identify this as
        the on-premises EAC.

    - The second EAC tab should be titled **Exchange admin center**.
        This is the EAC for Exchange Online. Select this tab and note that
        it does not include the blue bar with the Enterprise and Office 365 options.
        This will help you identify this as the EAC for Exchange Online.

        Select the **send connectors – Microsoft Exchange** tab to display the
        on-premises EAC.

3. In the on-premises **Exchange admin center**, select **recipients** in the
    left-hand navigation pane. The **mailboxes** tab at the top of the page is
    displayed by default.  

    **Note:** Even though there are numerous on-premises user accounts (as noted
    by the on-premises user accounts that you previously synchronized into
    Microsoft 365), only one of those users had an on-premises mailbox set up in
    Exchange Server 2019 by your lab hosting provider. This user was the
    **Administrator** account, which was the only on-premises mailbox at the
    beginning of the labs, then you created three additional user mailboxes in
    the Module 6 lab, so now there are four mailboxes in the list.  
  
    In the remaining steps in this task, you will add on-premises mailboxes for
    two additional on-premises user accounts.

4. In the **mailboxes** tab, select the **plus (+) sign** icon on the menu bar
    to add a new on-premises mailbox. In the drop-down menu, select **User
    mailbox**.

5. In the **new user mailbox** window, you want to create a mailbox for Allan
    Yoo, who’s an existing on-premises user. You can leave the **Alias** field
    blank as this will default to the user’s first name as long as there is no
    conflict with the alias for an existing mailbox.

6. The **Existing user** option is selected by default, so select the
    **Browse** button next to the existing user field.

7. In the **Select User** window, select **Allan Yoo** in the list of users and
    then select **OK**.

8. In the **new user mailbox** window, select **Save**. In the list of
    mailboxes, Allan Yoo’s mailbox should now appear. You will use Allan’s
    on-premises mailbox when testing the Outbound Connector that you create in
    the next task.

9. Repeat steps 4 through 8 to create an on-premises mailbox for **Beth
    Burke**. You will use Beth’s on-premises mailbox when testing mailbox
    migration in the next lab exercise.

    Allan and Beth's mailboxes should now appear in the list of mailboxes along with the Administrator's mailbox.

10. Leave your browser and all its tabs open and proceed to the next task.

## Task 4: Create a new Outbound Connector

In this task, you will remain in your on-premises Exchange Server (LON-EX1) VM.
In the EAC for Exchange Online, you will delete the existing outbound connector
from Microsoft 365 to Adatum’s on-premises Exchange Server (LON-EX1), and you
will create a new outbound connector to take its place.

The short version as to why you must do this is because the VM lab environment
for this course has a limitation related to updating a Microsoft Exchange
certificate from a third-party certificate authority (CA); therefore, you must
perform this workaround to bypass this issue with your lab environment.

The long version as to why you must do this begins with the fact that, by
default, the existing Outbound connector has a dependency domain registration.
Yet because you recently changed domains, the self-signed certificate is
pointing to the adatum.com domain on LON-EX1 (your Exchange Server), while the
third-party wildcard certificate for the xxxCustomDomainxxx.xxx domain also
points to LON-EX1. Since the xxxCustomDomainxxx.xxx is not registered to the
Exchange server, routing by the domain name will not work.

So how does this affect the Outbound connector? Well, normally at this point in
the hybrid configuration process, you would validate the existing Outbound
connector by using the primary domain name to route message traffic. However,
because one of the two domain names isn’t a registered point for your Microsoft
Exchange Server, the validation of the Outbound connector will fail because the third-party certificate domain for the xxxCustomDomainxxx.xxx domain has not
been validated to this Exchange Server.

In a real-world scenario in which you replace or add the domain just to your
domain controller, you would update your Microsoft Exchange server certificate
to point to the new domain. Unfortunately, the VM lab environment has a
dependency to using Adatum.com as the primary domain; therefore, changing the domain
would cause several communication issues with all the existing domain PC’s and
servers.

As a result, you must perform this workaround in the VM lab environment
in which you delete the existing Outbound connector and then create a new one
that routes email messages to the IP address associated with the Microsoft 365
tenant provided by your lab hosting provider. This removes the dependency
between the Outbound connector and the Microsoft Exchange certificate that
points to the Adatum.com domain, which in turn bypasses the conflict in which
two domains point to the same Exchange Server.

**STOP:** After finishing the previous task, you should wait at least 15 minutes
before starting this task. The reason for this delay is that when you created
the on-premises Exchange mailboxes for Allan Yoo and Beth Burke, it can take up
to 15 minutes to propagate those updates throughout the system. **If you do not
wait at least 15 minutes before starting this task, there is a good chance it
will fail.**

1. You should still be in LON-EX1 after having completed the prior task; if
    necessary, log into LON-EX1 as the **Administrator** with a password of
    **Pa55w.rd**.

2. In your **Edge browser**, you should still have the two EAC tabs open from
    the earlier task – one for the on-premises EAC and one for the EAC for
    Exchange Online.

3. In your browser, select the **Exchange admin center** tab in your
    browser. This tab displays the EAC for Exchange Online.

4. In the **Exchange admin center** for Exchange Online, in the left-hand
    navigation pane, select **mail flow**.

5. In the expanded group, select **Connectors**.

6. You will begin by deleting the existing Outbound connector. The list of
    connectors currently displays an Inbound and Outbound connector. Select the
    **Outbound** connector to highlight it.  

    **NOTE:** The Details pane on the right-side of the screen displays the
    details of the Outbound connector. Under the **Mail flow scenario** section,
    it indicates that this is the outbound connector from Office 365 to your
    organization’s (on-premises) email server (which in Adatum’s deployment is
    LON-EX1).

7. With the **Outbound** connector highlighted, select the **trash can
    (Delete)** icon on the menu bar.

8. On the warning dialog box, select **Confirm** to confirm that you want to
    delete this outbound connector. This will delete the outbound connector,
    which will be removed from the list of connectors. Close the window.

9. You must now add a new Outbound connector. On the menu bar, select
**+ Add a connector**.

10. On the **New connector** page, under **Connection from**, select **Office 365**.  

    Then, under **Connection to**, select **Your organization’s email server**. Select **Next**.

11. On the **Connector name** page, enter **Outbound connector to LON-EX1** in
    the **Name** field and then select **Next**.

12. On the **Use of connector** page, select the **For email messages sent to all accepted domains
    in your organization** option and then select **Next**.

13. On the **Routing** page, enter the **IP address**
    provided by your lab hosting provider (for example, 64.64.221.224) for your
    Microsoft 365 domain, select the **plus (+) sign** icon.

14. Once the IP address has been added, select **Next**.  

    **Note:** In a real-world environment, you would typically enter a Fully
    qualified domain name (FQDN) here. However, given the settings of the VM lab
    environment, we instead must enter the IP address of our email server to
    bypass an internal conflict that appears to exist between Microsoft 365, the
    new xxxUPNxxx.xxxCustomDomainxxx.xxx domain, and the adatum.com domain.

15. On the **Security restrictions** page, leave the default settings (if necessary, select them), and then select **Next**:

    - The **Always use Transport Layer Security (TLS) to secure the connection
        (recommended)** check box should be selected.

    - The **Issued by a trusted certificate authority (CA)** option should be
        selected.

16. On the **Security restrictions** page, accept the default settings (if necessary, select them):

    - Below the **Issued by a trusted certificate authority (CA)** option,
        select the **And the subject name or subject alternative name (SAN)
        matches this domain name** check box, and then enter \***.
        xxxCustomDomainxxx.xxx** (where xxxCustomDomainxxx.xxx is your accepted
        domain name) in the domain name field that appears below this check box,
        and then select **Next**.

17. On the **Validate email** page, you will enter Allan Yoo’s on-premises email address, which will be used to
    validate this connector.

18. On the **Validate email** window that appears, enter Allan Yoo’s email address of
    **Allan@xxxUPNxxx.xxxCustomDomainxxx.xxx** (where xxxUPNxxx is the unique
    UPN Name and xxxCustomDomainxxx.xxx is the custom domain name, both of which
    were provided by your lab hosting provider), select the **plus (+) sign** icon.

    **NOTE:** If it’s been less than 15 minutes since you completed the previous
    task in which you created the on-premises mailbox for Allan, then you may
    receive an error message indicating that the email address is invalid. If
    this occurs, select **Cancel**, then wait several more minutes and try
    again.

19. Allan’s email address should now appear on the **Validate email**
    page. Select **Validate**.

20. On the **Validation Result** page, the validation will either be successful, or it will have
    failed. Perform the appropriate steps below depending on which result you
    receive.

21. If the validation was successful, the two validation tasks should be

    displayed: **checking connectivity to the IP address** and **sending a test
    email to an on-premises user mailbox within this IP address**. The status of
    both tasks should be **Succeeded**.  

    Select **Next**, and then select **Create connector** and **Done**. Proceed to the final step in this task; you can skip the remaining steps, which provide instruction on what to do if the validation failed. Since your validation was successful, you can skip to the final step.

22. If either of the validation tasks failed, select the failed task and then
    select the **pencil** icon to display the **Details** about that task. This
    will help you troubleshoot the issue that caused the task failure.

    - If the **Send test email** task failed with a message indicating it
        could not find the user’s on-premises mailbox, it’s usually because you
        did not wait at least 15 minutes after creating Allan Yoo’s on-premises
        mailbox in the prior task before performing this task. If this occurs,
        wait several minutes, select the **Back** button, and then select the
        **Validate** button again.

    - However, if the **Send test email** task failed with a message
        indicating **The test email was routed out from O365 without using any
        connector**, our lab testing has indicated that is typically a
        false-positive error (due to the conflict mentioned earlier between our
        VM lab environment and Microsoft 365), and in fact, the test-email was
        successfully routed to Allan Yoo’s on-premises mailbox.  

        To verify this, select **Close** to close the detail window, and then on
        the **Validation Result** window, select **Save**. You should save the
        connector even though the validation failed. This will display a
        **Warning** dialog box confirming whether you want to save the connector
        even though the validation failed. Select **Yes**, and then select
        **OK** once the information is successfully saved.

23. To verify whether Allan received the validation email, select a **New InPrivate window** in
    your **Edge browser** and open **Outlook Web App** by entering the following
    URL: **<https://xxxUPNxxx.xxxCustomDomainxxx.xxx/owa>** (where xxxUPNxxx is
    the unique UPN name assigned to your tenant by your lab hosting provider and
    xxxCustomDomainxxx.xxx is your lab hosting provider’s custom domain).  

    **Note:** If you receive a page indicating **Your connection isn’t
    private**, this is due to a certificate issue in the VM environment that you
    can ignore for the purpose of this lab. To bypass this error, select the
    **Advanced** button, and then select **Continue to localhost (unsafe)**.

24. In the **Outlook** sign in window, enter **adatum\\Allan** in the
    **Domain\\username** field, enter **Pa55w.rd** in the **Password** field,
    and then select **sign in**. If necessary, select your Language and Time
    Zone and select **Save**.

25. In Allan’s Inbox, you may or may not see an email from **O365ConnectorValidation@xxxUPNxxx.xxxCustomDomainxxx.xxx**.

    - If you see this email, then open it. The message in the email indicates
        it was sent from Office 365 to check that an email could be delivered
        using the new connector.  

        **Note:** If the outbound connector validation indicated the test email
        failed to be delivered, the presence of this email indicates that it
        was, in fact, delivered to Allan’s mailbox. In the next lab exercise,
        you will perform a task to further show the connectors are working in
        Adatum’s hybrid deployment.

    - If you do not see the test email, then typically what happened is that
        the Outbound connector did not finish its internal configuration by the
        time the validation process sent the email. When this occurs, the mail
        gets stuck in an internal loop and when the Hop count is eventually
        exceeded, the validation fails and the message is not delivered.  

        In the event the test email did not appear in Allan’s Inbox, you will
        revalidate the Outbound connector that you just created and saved. On
        the **connectors** page, you should see the Outbound connector that you
        created. Select the **Outbound connector to LON-EX1** and then select
        the **pencil (edit)** icon on the menu bar. This will walk you through
        all the steps that you previously performed to create and validate the
        connector (steps 12-21). However, this time, all the information that
        you entered when you created the connector will be prefilled for you, so
        you basically just have to select **Edit (name or status, use, routing, restrictions, etc..)** / **Validate this connector** to modify / validate the connector.  

        Chances are, if the validation failed the first time, it will fail
        again. However, this time, once it fails, select **Allan’s mailbox tab**
        in your browser and you should see the validation email in his Inbox. By
        the time you run this validation a second time, the Outbound connector
        should have finished its configuration, so the mail should be delivered
        (even though from a validation standpoint, it does not think it did).

26. Leave your browser and all its tabs open and proceed to the next exercise.

## Proceed to Lab 7 - Exercise 3
