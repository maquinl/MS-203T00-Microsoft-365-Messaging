---
lab:
    title: 'Lab 7: Manage a Hybrid Deployment'
    Exercise: 'Exercise 1: Prepare Azure AD for a Hybrid Deployment'
    Learning Path: 'Learning Path 8: Manage the hybrid deployment life cycle'
---

# Lab 7 - Exercise 1 - Prepare Azure AD for Hybrid Synchronization

In this lab you will continue in your role as Holly Dickson, Adatum’s Messaging
Administrator. Adatum has decided to transition from their current Microsoft
Exchange on-premises deployment to a hybrid deployment that utilizes Exchange
Online within Microsoft 365. Adatum’s CTO has tasked you with implementing this
hybrid deployment. In this lab, you will perform the tasks necessary to prepare
your messaging environment for your eventual hybrid deployment.

To complete this task, you must first prepare Azure Active Directory to support
the hybrid synchronization between Exchange on-premises and Exchange Online.
This will require that you:

- Configure your lab environment to support local mail transport

- Add an accepted domain to your Azure AD forest

- Configure the UPN Name for the new domain

- Configure Exchange to use the new domain

- Enable directory synchronization by installing and running the Microsoft
    Azure Active Directory Connect tool

- Perform a Full Synchronization to migrate Adatum’s on-premises user accounts
    to the new domain in Microsoft 365

While your trial tenant has already been set up by your lab hosting provider,
you must ensure that your local, on-premises Active Directory is ready for
hybrid synchronization before you create your hybrid deployment. You will do
this by adding a custom, accepted domain to the Azure Active Directory forest
and then configure Exchange to use the new accepted domain.

Once you finish configuring Azure AD for hybrid synchronization in this lab, you
will then set up Exchange for a hybrid deployment and then test your new
deployment.

## Task 1: Configure your tenant to support local mail transport

Before you begin setting up Adatum’s hybrid deployment, you must first configure
your hosted lab environment to support local mail transport.

**IMPORTANT:** The steps that you perform in this task are NOT required to set
up a hybrid environment in a real-world scenario. Instead, they must be
performed to configure the hosted virtual machines used in this training lab so
that email can be sent locally between on-premises and cloud users when testing
your hybrid deployment.

1. Switch to **LON-EX1** and if necessary, log in as the **Administrator** account
    with a password of **Pa55w.rd**.

2. If your Edge browser is still open from Lab 1, then minimize the browser now
    (do not close it).

3. You need to open the **Network and Sharing Center**. To do so, select the
    network icon on the right-side of the system tray at the bottom of the
    screen (which displays **Adatum.com Internet access**), and in the menu that
    appears, select **Open Network & Internet settings**.

4. In the **Settings** window, scroll to the bottom of the **Status** pane on
    the right and select **Network and Sharing Center**.

5. In the **Network and Sharing Center**, under the **View your active
    networks** group, select **Ethernet** (which appears to the right of
    **Connections**:).

    **WARNING:** select **Ethernet**, not **Ethernet 2**.

6. In the **Ethernet Status** window, select the **Properties** button that
    appears at the bottom of the window.

7. In the **Ethernet Properties** window, select **Internet Protocol Version 4
    (TCP/IPv4)** and then select the **Properties** button.  
    ‎  
    ‎**WARNING:** Do NOT select the check box for **Internet Protocol Version 4
    (TCP/IPv4)**, which will uncheck it. This check box MUST remain checked.
    Simply select this item to highlight it so that you can update its
    properties.

8. The **Internet Protocol Version 4 (TCP/IPv4) Properties** window is already
    set up to use an existing IP address. Since you are going to add an
    additional IP address, select the **Advanced** button in the bottom-right
    corner of the screen.

9. In the **Advanced TCP/IP Settings** window, in the **IP Settings** tab, it
    displays two groups: **IP addresses** and **Default gateways**.

    Under the **IP addresses** group, select the **Add…** button.

10. A **TCP/IP Address** pop-up window is displayed. Enter **10.0.0.6** in the
    **IP address** field, enter **255.255.255.0** in the **Subnet mask** field,
    and then select **Add**.  
    ‎  
    ‎**NOTE:** If you enter the IP address or subnet mask incorrectly, you will
    receive an error when selecting **Add**. If this occurs, you must close the
    window and then reopen it before entering the correct values. If you do not
    close the window and reopen it, you will still receive the error even if you
    enter the values correctly.

11. In the **Advanced TCP/IP Settings** window, it should now display
    **10.0.0.6** as a supported IP address, with a subnet mask of
    **255.255.255.0**. Select **OK**.

12. In the **Internet Protocol Version 4 (TCP/IPv4) Properties** window, select
    **OK**.

13. In the **Ethernet Properties** window, select **Close**.

14. In the **Ethernet Status** window, select **Close**.

15. Close the **Network and Sharing Center** window.

16. Close the **Settings** window.

## Task 2: Create a Custom Domain in Microsoft 365

Not every company has just one domain; in fact, many companies have more than
one domain. Adatum has just purchased a new domain
(xxxUPNxxx.xxxCustomDomainxxx.xxx; the exact name of which is provided by your
lab hosting provider) that resides in Microsoft Azure but not in Adatum's
on-premises environment. To support Adatum’s new custom domain, your lab hosting
provider took on the role of Adatum’s third-party domain registrar.

In this task, you will gain experience adding this domain to Adatum' Microsoft
365 deployment. When you add a domain to Microsoft 365, it's called an accepted,
or custom domain. Custom domains allow companies to have their own branding on
emails and accounts so that customers can verify who is emailing them (for
example, \@Contoso.com). When a company adds a new domain to Microsoft 365, it
must also maintain the DNS records that are necessary to support the services
required by the company for the new domain.

Most companies do not personally manage their domains' DNS records themselves;
instead, they have a third-party resource that manages these records for them.
To assist in this effort, Microsoft 365 provides certain third-party domain
registrars with an automation tool that automatically adds and replaces a
company’s DNS records. The automation tool also federates the sign in
credentials for the third-party registrars and Microsoft 365. Using a tool to
automatically maintain DNS records is a much-welcomed improvement from the days
when companies had to manually maintain these records, which oftentimes
introduced human error into a rather complicated process. Because these tools
eliminate the need to manually add the DNS records, they eliminate human error
from the process.

That being said, for the purpose of this lab, you will be asked to manually
create the necessary DNS records required by this new custom domain. In the
other Microsoft 365 training courses that use a custom domain (such as MS-101T00), the custom domain and its DNS records will be added into
Adatum's Microsoft 365 deployment by the lab hosting provider, who will take on
the role of the third-party domain registrar for Adatum. However, this MS-203T00
training course will task you with adding the domain and creating its required
DNS records so that you gain experience and understanding of what the DNS
records are about and why they are required for a new domain.

In your hosted lab environment, Adatum already has an existing on-premises
domain titled **adatum.com**, along with a Microsoft 365 domain titled
**xxxxxZZZZZZ.onmicrosoft.com**. In this lab, you will create a second Microsoft
365 domain for Adatum that will be titled **xxxUPNxxx.xxxCustomDomainxxx.xxx**;
you will replace **xxxUPNxxx** with the UPN name assigned to your tenant by your
lab hosting provider, and you will replace **xxxCustomDomainxxx.xxx** with your
lab hosting provider's custom domain name. Your instructor will provide you with
your lab hosting's provider's custom domain name as well as show you how to
locate the UPN name.

1. Switch to **LON-DC1** and, if necessary, log in as **Administrator** and
    password **Pa55w.rd**.

2. You must now open **Windows PowerShell**. Select the magnifying glass
    (Search) icon on the taskbar at the bottom of the screen and type
    **powershell** in the Search box that appears.

    In the list of search results, right-click on **Windows PowerShell** (do not
    select Windows PowerShell ISE) and select **Run as administrator** in the
    drop-down menu that appears. Maximize your PowerShell window.

3. At the command prompt, you should run the following command to create a new
    zone in your on-premises DNS:

    **IMPORTANT:** Before you run the following command, remember to replace
    **xxxUPNxxx** with the unique UPN name assigned to your tenant by your lab
    hosting provider, and replace **xxxCustomDomainxxx.xxx** with your lab
    hosting provider's custom domain name:

    `dnscmd /zoneadd xxxUPNxxx.xxxCustomDomainxxx.xxx /DsPrimary`

4. Minimize your Windows PowerShell window (do NOT close it as you will use it
    later).

5. Switch to **LON-EX1**

6. Open **PowerShell** as and Administrator and run the following command:

     `dnscmd /zoneadd xxxUPNxxx.xxxCustomDomainxxx.xxx /Secondary 10.0.0.4`

7. Return back to **LON-DC1**  

8. You will now access the **Microsoft 365 admin center** from LON-DC1. Select
    the **Microsoft Edge** icon on your taskbar and enter the following URL in
    the address bar: **<https://portal.office.com>.**

9. On the **Sign in** page, enter **admin@xxxxxZZZZZZ.onmicrosoft.com** (where
    xxxxxZZZZZZ is the tenant prefix provided by your lab hosting provider), and
    then enter the tenant email password provided by your lab hosting provider
    on the **Enter password** page. Select **Sign in.**

10. On the **Stay signed in?** window, select the **Don’t show this again**
    check box and then select **Yes.**

11. If a **Get your work done with Office 365** window appears, select the **X**
    in the upper right-hand corner to close it.

12. In the **Office 365 home** page, in the column of Microsoft 365 app icons on
    the left-side of the screen, select the **Admin** icon to navigate to the
    **Microsoft 365 admin center**.

13. In the **Microsoft 365 admin center**, in the left-hand navigation bar,
    select **Show all,** select **Settings**, and then under the **Settings**
    group select **Domains**.

14. On the **Domains** page, note that in the list of domains, only the
    **xxxxxZZZZZZ.onmicrosoft.com** domain appears. The existing on-premises
    **adatum.com** domain does not appear in the list of Microsoft 365 domains.

    To add Adatum's new Microsoft 365 domain, select **+Add domain** in the menu
    bar that appears above the list of domains; this will start the **Add
    domain** wizard.

15. In the **Add a domain** page, in the **Domain name** field, enter your
    domain name in the form of **xxxUPNxxx.xxxCustomDomainxxx.xxx** (where
    xxxUPNxxx is the unique UPN name provided by your lab hosting provider, and
    xxxCustomDomainxxx.xxx is your lab hosting provider's domain name), and then
    select the **Use this domain** button at the bottom of the page.

16. In the **Verify you own your domain** page, you must select a
    verification method to prove you own the domain. For this lab, select the
    **Add a TXT record to the domain's DNS records** option and then select
    **Continue**.

17. On the **Verify you own this domain** page, you must copy the **TXT value**
    (NOT the TXT name) so that you can configure the domain later on in DNS
    Manager.

    To do so, select the **Copy record** icon that appears to the left of the
    **TXT value** (to the left of **MS=msXXXXXXXX**). If a dialog box appears,
    select **Allow access** to copy this value from the webpage to your
    clipboard.

    ‎**Important:** Do NOT select the **Verify** button at this point; **instead,
    proceed to the next step.** However, if you did select the **Verify**
    button, you will receive an error indicating the system could not find the
    record you added for this domain (you can do this if you want to see the
    error; there is no harm in it). Therefore, you must complete the next series
    of steps to add the TXT record to this domain in **DNS Manager**. Once you
    finish that process, you will be instructed to return to this page and
    select the **Verify** button so that you can complete the process of adding
    this domain in the Microsoft 365 admin center.

18. Before you can verify you own this domain in the **Add domain** wizard, you
    must first add a DNS record for this domain in Server Manager. Select the
    **Server Manager** icon that appears in your taskbar at the bottom of the
    page. Maximize the Server Manager window if necessary.

19. In **Server Manager Dashboard,** select **Tools** in the top right corner of
    the window. In the drop-down menu that appears, select **DNS**, which will
    open **DNS Manager**. Maximize the DNS Manager window.

20. In the **DNS Manager** window, in the **File Explorer** section in the
    left-hand column, under **LON-DC1** expand the **Forward Lookup Zones**
    folder and then select the **xxxUPNxxx.xxxCustomDomainxxx.xxx** zone that
    you previously added in Windows PowerShell (where xxxUPNxxx is the unique
    UPN name provided by your lab hosting provider and xxxCustomDomainxxx.xxx is
    your lab hosting provider's domain name).

21. Right-click on this **xxxUPNxxx.xxxCustomDomainxxx.xxx** and click **Properties.**

22. Click the **Zone Transfers** tab, and check the box to **Allow zone transfers.**

23. Tick the option **Only to the following servers** and click **Edit.**

24. In the **IP Address** enter **10.0.0.6** and click **OK**, **Apply** and then **OK** again4.

25. Right-click on this **xxxUPNxxx.xxxCustomDomainxxx.xxx** zone, and in the
    menu that appears, select **Other New Records...**

26. In the **Resource Record Type** window that appears, in the **Select a
    resource record type** field, scroll down and select **Text (TXT),** and
    then select the **Create Record...** button at the bottom of the window.

27. In the **New Resource Record** box, in the **Text (TXT)** tab, leave the
    **Record name** field blank. However, right-click in the **Text** field and
    select **Paste** from the menu that appears. This will paste in the TXT
    valued of **MS=msXXXXXXXX** that you copied to the clipboard when you were
    in the Microsoft 365 admin center.

28. Select **OK** to create the record.

29. In the **Resource Record Type** window, select **Done**. Note how this Text
    (TXT) record appears in the details pane on the right for the
    xxxUPNxxx.xxxCustomDomainxxx.xxx domain that you previously created.

    Leave your **DNS Manager** window open but minimize it as you will return to
    it in a later step in this task. Minimize the **Server Manager** window as
    well.

30. Switch back to **LON-EX1** and from **Server Manager** open **DNS**.

31. Expand **Forward Lookup Zones** and click your **Custom Domain, xxxUPNxxx.xxxCustomDomainxxx.xxx** to verify the TXT file has has transferred from **LON-DC1**.

    > Note: It may take several minutes for the record to appear.  You can refresh and reload the zone to force it to update.  Wait until the TXT file appears before proceeding. It may be helpful to close and open **DNS Manager**, and if several minutes have passed you can Right-click on the **xxxUPNxxx.xxxCustomDomainxxx.xxx** zone, and in the
    menu that appears, select **Transfer from master**.

    >[!Alert] **If the TXT record does not appear Complete the Same Zone Transfer steps on DC-1 that you did on EX-1 except use 10.0.0.5 instead of 10.0.0.6 so the DC-1 and EX-1 can talk to each other**.

32. When the TXT appears, switch back to **LON-DC1**

33. You are now ready to return to the Microsoft 365 admin center and resume
    adding the domain record. If you’ll recall, when you were earlier adding the
    domain in the Microsoft 365 admin center, you indicated that you wanted to
    verify the domain using a TXT record. At that point you had to switch to DNS
    Manger and add the TXT record. Now that you’ve added the TXT record, you can
    go back to the Microsoft 365 admin center and proceed with the domain
    verification process.

    ‎In your Edge browser, you should be back in the **Microsoft 365 admin
    center** tab that displays the **Verify you own this domain** page from the
    **Add domain** wizard. The **TXT name** should display your UPN name
    (xxxUPNxxx) and the **TXT value** should display your MS=msXXXXXXXX value.

34. Scroll to the bottom of the window and select **Verify.**

    **Note:** If you selected **Verify** in the prior step when you copied the
    TXT value just to see the error that you would receive, the **Verify**
    button changed to **Try again**. In you did this, then select **Try again**
    rather than **Verify**.

    **Warning:** It can sometimes take up 5 to 10 minutes for the change that
    you just made to propagate through the system, and sometimes it can take
    significantly longer depending on your registrar (in this case, your lab
    hosting provider). If you receive an error indicating the system could not
    detect the record that you added, wait 5 minutes and select the **Try
    again** button. Continue to do so every 5 minutes or so until the TXT record
    is successfully verified, at which point the **Activate records** window
    will appear.

    ‎**Important:** If you had a typo or any other configuration mistakes, the
    domain will not be verified. If this occurs, the **How do you want to
    connect to your domain?** window in the next step will not appear. In this
    case, select the **Back** button to repeat this task. Take your time when
    configuring the domain to make sure you don’t run into similar issues at
    this step in the process.

35. If your Text (TXT) record was successfully verified, the **How do you want
    to connect to your domain?** window will appear. Select **Continue**.

36. In the **Add DNS records** window, it enables you to add DNS records for
    three services that DNS supports - Exchange and Exchange Online Protection,
    Skype for Business, and Intune and Mobile Device Management for Microsoft
    365. **Exchange and Exchange Online Protection** is displayed by default and its
    check box is also selected by default.

    To see the other two services, select
    **Advanced Options**. Note that under **Advanced Options**, neither the
    **Skype for Business** nor the **Intune and Mobile Device Management for
    Microsoft 365** check boxes are selected.

    **Important:** Only the **Exchange and Exchange Online Protection** check box
    should be selected for the purpose of this lab; this is sufficient for Adatum.

    **Do NOT select either of the other two check boxes.** We had you select
    **Advanced Options** just to see where you would select these other two services in the event you would need to do so in your real-world deployment.

37. Under the **Exchange and Exchange Online Protection** service, the
    description indicates that three DNS records are needed for it to work properly:
    a Mail Exchanger (MX) record, an Alias (CNAME) record, and an additional
    Text (TXT) record. You must now switch back and forth between this **Add DNS
    records** page and **DNS Manager** to add these three additional DNS records
    for the new domain. For each DNS record that you add in DNS Manager, you
    will copy information from this **Add DNS records** page and then paste it
    into each corresponding DNS record that you create in DNS Manager.

    On the **Add DNS records** page, under the **Exchange and Exchange Online
    Protection** section, select the arrow (**\>**) in the **MX Records**
    section to expand it. This displays the **Expected value** that the domain
    setup wizard expects to see in the MX record that you create for this domain
    in DNS Manager.

    Then select the arrow (**\>**) in the **CNAME Records** section and the
    **TXT Records** section. All three record types should now be expanded.

    > [!alert] At each stage of the verification process described below, after entering the value on **LON-DC1**, you should verify in **DNS Manager** on **LON-EX1** that the new entry has appeared there before returning to **LON-DC1** to continue with the verification process.
    >
    > It may take several minutes for the record to appear.  To speed the process you can right-click the Custom DNS zone on **LON-EX1** and select **Transfer new copy of zone from Master** and then select **Refresh**. Wait until the new entry appears before proceeding.

38. You will begin by adding the **MX record** required by the **Exchange and
    Exchange Online Protection** service.

    - In the **MX Records** section, under the **Points to address or value**
        column, select the copy icon that appears to the left of the expected
        value (for example,
        **xxxUPNxxx-xxxCustomDomainxxx-xxx.mail.protection.outlook.com**) to
        copy this value to the clipboard. If a dialog box appears, select
        **Allow access** to allow the webpage to copy the value to the
        clipboard.

    - You must now switch to DNS Manager. On the taskbar at the bottom of the
        page, select the **DNS Manager** icon.

    - In **DNS Manager**, under **Forward Lookup Zones**, the
        **xxxUPNxxx.xxxCustomDomainxxx.xxx** domain should be selected from when
        you earlier left off. If not, select this zone now. You should see the
        **TXT** record that you created earlier. You must now create a **Mail
        Exchanger (MX)** record for this domain.

        Under **Forward Lookup Zones**, right-click the
        **xxxUPNxxx.xxxCustomDomainxxx.xxx** domain and select **New Mail
        Exchanger (MX)...**

    - In the **New Resource Record** window, in the **Mail Exchanger (MX)**
        tab, leave the **Host or child domain** field blank, but right-click in
        the **Fully qualified domain name (FQDN) of mail server** field and
        select **Paste** from the menu that appears. This will paste in the
        expected **Points to address or value** that you just copied to the clipboard.

    - Select **OK**. Note how this Mail Exchanger (MX) record appears in the
        details pane on the right for the xxxUPNxxx.xxxCustomDomainxxx.xxx
        domain that you previously created. Leave your DNS Manager window open
        as you will return to it in a later step in this task.

    - Switch back to the **Add DNS records** page in the Microsoft 365 admin
        center by selecting the **Microsoft Edge** icon on the taskbar at the
        bottom of the page. At this point, you can either select **Continue** at
        the bottom of the **Add DNS records** page to verify the MX record that
        you just added, or you can wait until you have added all three records
        and then select **Continue** to verify all three records at once.

        For the purposes of this lab, you will verify each record as you create
        it. Therefore, select **Continue**. It will display either a check mark
        or an exclamation point next to **MX Records**. The check mark in a
        green circle indicates that it successfully validated the MX record for
        this domain in DNS Manager, and the exclamation point in a red circle
        indicates that there was a problem with the MX record, and it did not
        validate successfully. If the MX record did not validate successfully,
        then review the record to ensure you entered the proper information,
        make any necessary corrections, and then select **Continue** again.

39. Once a check mark appears next to **MX Records**, you must perform the
    following steps to add the **CNAME record** required by Exchange and
    Exchange Online Protection service.

    - On the **Add DNS records** page, in the **CNAME Records** section, under
        the **Points to address or value** column, select the copy icon that
        appears to the left of the expected value (for example,
        autodiscover.outlook.com).

        **Important:** You will NOT copy the expected **Host Name** value. The
        value listed here as the expected host name is
        **autodiscover.xxxUPNxxx** (where xxxUPNxxx is your UPN name). However,
        if you paste this value in the **Alias name** field in the CNAME record
        in DNS Manager, the CNAME record validation on this page will fail. When
        you create the CNAME record in DNS Manager in the following steps, you
        will simply enter **autodiscover** as the **Alias name** and NOT
        **autodiscover.xxxUPNxxx**.

        The reason for using only **autodiscover** as the **Alias name** is that
        Autodiscover is an Exchange service that minimizes configuration and
        deployment. For small, single SMTP namespace organizations such as
        Adatum, only autodiscover is needed as the Alias, as opposed to
        autodiscover.xxxUPNxxx for larger organizations with multiple SMTP
        namespaces. By adding the CNAME record to your on-premises DNS server,
        you're creating a redirect record that allows users to configure Outlook
        and access OWA by using either Basic Authentication or Modern
        Authentication (OAUTH).

        Therefore, the only value you need to copy for the CNAME record is the
        expected value for the **Points to address or value** column (for
        example, autodiscover.outlook.com).

    - On the taskbar at the bottom of the page, select the **DNS Manager**
        icon.

    - In **DNS Manager**, under **Forward Lookup Zones**, right-click the
        **xxxUPNxxx.xxxCustomDomainxxx.xxx** domain and select **New Alias
        (CNAME)...**

    - In the **New Resource Record** window, enter **autodiscover** in the
        **Alias name (uses parent domain if left blank)** field.

    - Right-click in the **Fully qualified domain name (FQDN) for target
        host** field and select **Paste** from the menu that appears. This will
        paste in the expected **Points to address or value** that you earlier
        copied to the clipboard.

    - Select **OK**. Note how this Alias (CNAME) record appears in the details
        pane on the right for the xxxUPNxxx.xxxCustomDomainxxx.xxx domain that
        you previously created. Leave your DNS Manager window open as you will
        return to it in a later step in this task.

    - Switch back to the **Add DNS records** page in the Microsoft 365 admin
        center. On the taskbar at the bottom of the page, select the **Microsoft
        Edge** icon and select the **Microsoft 365 admin center** tab. At this
        point, you can either select **Continue** at the bottom of the **Add DNS
        records** page to verify the CNAME record, or you can wait until you
        have added all three records and then select **Continue** to verify all
        three records at once.

        For the purpose of this lab, select **Continue**. It will display either
        a check mark or an exclamation point next to **CNAME Record**. The check
        mark in a green circle indicates that it successfully validated the
        CNAME record for this domain in DNS Manager, and the exclamation point
        in a red circle indicates that there was a problem with the CNAME
        record, and it did not validate successfully. If the CNAME record did
        not validate successfully, then review the record to ensure you entered
        the proper information, make any necessary corrections, and then select
        **Continue** again.

40. Once a check mark appears next to **CNAME Records**, you will finish by
    adding the **TXT record** required by Exchange and Exchange Online
    Protection service.

    - On the **Add DNS records** page, in the **TXT Records** section, under
        the **TXT value** column, select the copy icon that appears to the left
        of the expected value (for example, **v=spf1
        include:spf.protection.outlook.com -all**) to copy this value to the
        clipboard.

    - On the taskbar at the bottom of the page, select the **DNS Manager**
        icon.

    - In **DNS Manager**, under **Forward Lookup Zones**, right-click the
        **xxxUPNxxx.xxxCustomDomainxxx.xxx** domain and select **Other New
        Records...**

    - In the **Resource Record Type** window that appears, in the **Select a
        resource record type** field, scroll down and select **Text (TXT),** and
        then select the **Create Record...** button at the bottom of the window.

    - In the **New Resource Record** window, in the **Text (TXT)** tab, leave
        the **Record name** field blank. However, right-click in the **Text**
        field and select **Paste** from the menu that appears. This will paste
        in the expected **TXT value** that you earlier copied to the clipboard.

    - Select **OK**.

    - On the **Resource Record Type** window, select **Done**.

41. In **DNS Manager**, you should now see the TXT record that you originally
    created to verify the domain, along with the MX, CNAME, and TXT records that
    you created for the Exchange service to work within this domain.

    Minimize the DNS Manager window.

42. This should return you to the **Add DNS records** window in your Edge
    browser. Select **Continue** to complete the new domain setup. If you
    selected **Continue** after adding the MX and CNAME records, and if each
    validated successfully, then only the TXT record will be validated at this
    point. However, if you did not select **Continue** after adding the MX and
    CNAME records, then all three records will be validated at this point.

    - If all three records have been successfully validated, then the **Domain
    setup is complete** page will appear. If this occurs, then select the
    **Done** button to complete the domain setup process.

    - However, if any of the three records did not validate successfully, then the
    **Add DNS records** window will return, and it will display either a check
    mark or an exclamation point next to each record type to indicate which ones
    validated successfully and which ones did not. An exclamation point in a red
    circle indicates that there was a problem with the record, and it did not
    validate successfully (note that the Actual value for the record is left
    blank). If this occurs, you must correct the data on the corresponding
    record in DNS Manager and then select **Continue** again. You must repeat
    this process until all three records have successfully validated and the
    **Domain setup is complete** page appears.

43. Once the domain setup process is complete and the three DNS records
    validated successfully for the **Exchange and Exchange Online Protection**
    service, the **Domains** page will be displayed. Verify the **Domain
    status** for your new domain is **Healthy**.

44. Remain logged into the LON-DC1 VM with both **Microsoft Edge** and **Windows
    PowerShell** left open for the next task.

45. To complete the domain setup process, you must add an **A record** for this domain in DNS Manager. An **A record** connects the domain name to an IP address so that web browsers can find the website. In the next lab, you will validate the Outbound connector to connect Microsoft 365 to your email server. If you do not create an **A record**, the validation will fail and you will be unable to send external emails to your on-premises mailboxes.  

    - On the taskbar at the bottom of the page, select the **DNS Manager** icon.

    - In **DNS Manager**, under **Forward Lookup Zones**, right-click the **xxxUPNxxx.xxxCustomDomainxxx.xxx** domain and select **New Host (A or AAAA)...**

    - In the **New Host** window that appears, leave the **Name** field blank. In the **IP address** field, enter the IP address for your parent domain that was provided by your lab hosting provider (for example, 64.64.221.224).

    - Select **Add Host**, and then select **OK** in the dialog box indicating the host record was successfully created.

    - In the **New Host** window, select **Done**. The **Host (A)** record should now be displayed along with the other DNS records that you created for this domain.

46. Create another record for your internal clients to resolve your **Custom Domain**

    - On the taskbar at the bottom of the page, select the **DNS Manager** icon.

    - In **DNS Manager**, under **Forward Lookup Zones**, right-click the **xxxUPNxxx.xxxCustomDomainxxx.xxx** domain and select **New Host (A or AAAA)...**

    - In the **New Host** window that appears, leave the **Name** field blank. In the **IP address** field, enter the IP address **10.0.0.5**

    - Select **Add Host**, and then select **OK** in the dialog box indicating the host record was successfully created.

    - In the **New Host** window, select **Done**. The **Host (A)** record should now be displayed along with the other DNS records that you created for this domain.

47. Close DNS Manager.

48. Remain logged into the LON-DC1 VM with both **Internet Explorer** and **Windows PowerShell** left open for the next task.

## Task 3: Configure the UPN name for custom domain

In Active Directory, the default User Principal Name (UPN) suffix is the DNS
name of the domain where the user account was created. The Azure AD Connect
wizard uses the UserPrincipalName attribute, or it lets you specify the
on-premises attribute (in a custom installation) to be used as the user
principal name in Azure AD. This is the value that is used for signing into
Azure AD.

If you recall, your VM environment was created by your lab hosting provider with
an on-premises domain titled **adatum.com**. This domain included several
on-premises user accounts, such as Holly Spencer, Laura Atkins, and so on. Then
in the prior task, you created a custom, accepted domain for Adatum titled
**xxxUPNxxx.xxxCustomDomainxxx.xxx** (where xxxUPNxxx was the unique UPN name
assigned to your tenant, and xxxCustomDomainxxx.xxx was the name of your lab
hosting provider's custom domain).

In this task, you will use PowerShell to change the user principal name of the
domain for the entire Adatum Corporation by replacing the originally established
**adatum.com** domain with the custom **xxxUPNxxx.xxxCustomDomainxxx.xxx**
domain. In doing so, you will update the UPN suffix for the primary domain and
the UPN on every on-premises user account in AD DS with
**\@xxxUPNxxx.xxxCustomDomainxxx.xxx**.

A company may change its domain name for a variety of reasons. For example, a
company may purchase a new domain name, or a company may change its name and it
wants its domain name to reflect the new company name, or a company may be sold
and it wants its domain name to reflect the new parent company’s name.
Regardless of the underlying reason, the goal of changing a domain name is
typically to change the domain name on each user’s email address.

For this lab, Adatum has purchased a new domain (provided by your lab hosting
provider); therefore, it wants to change the domain name of all its on-premises
users’ email addresses from \@adatum.com to \@ xxxUPNxxx.xxxCustomDomainxxx.xxx.

1. You should still be logged into LON-DC1 as the **Administrator** with a
    password of **Pa55w.rd**; if necessary, log in now.

2. In this task, you will run two PowerShell commands. To save you from having
    to manually type in the commands (which are quite lengthy) into PowerShell, you will copy the
    commands from these instructions and then paste them into Notepad. You will
    then use the "Replace" functionality in Notepad to find and replace the custom domain name placeholder in the commands with the
    actual domain name, and then you will copy and paste each command from
    Notepad into PowerShell.  
    ‎  
    ‎Select the **magnifying glass (Search)** icon on the taskbar and then enter
    **note** in the Search field. In the menu that appears, select **Notepad**.
    Maximize the Notepad window once it opens.

3. While the PowerShell commands that you need to run are provided in steps 7
    and 8, it will be easier to copy these steps into Notepad, perform a
    **Replace** command to replace the custom domain name parameter with your
    actual new domain name, and then copy the commands in Notepad and paste them
    into PowerShell. This will save you from having to enter some lengthy
    PowerShell commands.  
    ‎  
    ‎Therefore, copy the PowerShell commands from **steps 7 and 8** below and
    paste them into Notepad.

    **Hint:** To simplify this process, copy all the text for
    steps 7 and 8 and not just the PowerShell commands; that way you can do one
    Copy statement rather than two Copy statements of just the PowerShell
    commands.

    **Note:** your lab provider may have already updated the PowerShell commands in Steps 7 and 8 with the correct custom domain name so you can simply copy and paste the PowerShell commands.

4. Once you have copied steps 7 and 8 into Notepad, select **Edit** on the
    Notepad menu bar and then select **Replace**.

5. In the **Replace** window, copy **xxxUPNxxx.xxxCustomDomainxxx.xxx** and
    paste it into the **Find what** field. In the **Replace with** field, enter
    the new domain you previously added, select **Replace all**, and then close
    the **Replace** window.  
    ‎  
    ‎**Important:** Review the Notepad document and verify that both commands
    were updated by replacing **xxxUPNxxx.xxxCustomDomainxxx.xxx** with the new
    accepted domain name. Verify you spelled the new domain name correctly.

6. If **Windows PowerShell** is still open, then select the **Windows
    PowerShell** icon on your taskbar; otherwise, you must open and elevated
    instance of **Windows PowerShell** just as you did earlier (remember to
    **Run as administrator)**.

7. You will now begin the process of copying each of the PowerShell commands
    (from this step through step 8) from Notepad and pasting them one at a time into
    Windows PowerShell and then running them.  
    ‎  
    ‎‎In the following PowerShell command, the **Set-ADForest** cmdlet modifies
    the properties of an Active Directory forest, and the **-identity**
    parameter specifies the Active Directory forest to modify.  
    ‎  
    ‎Select the **Notepad** icon on the taskbar and then copy the following
    command from Notepad (select the command, right-click on it, and then select
    **Copy**), paste it into PowerShell at the command prompt (right click on
    the command prompt and select **Paste**), and then hit ENTER to run it.  
    ‎  
    ‎**Note:** Traditionally, you must right-click at the command prompt, select
    Paste, and then hit ENTER on the keyboard to run a command. However, in some
    VM environments, you just have to right-click at the command prompt to both
    paste in the copied command AND run it.

    `Set-ADForest -identity adatum.com -UPNSuffixes @{replace="xxxUPNxxx.xxxCustomDomainxxx.xxx"}`

8. Copy the following command from Notepad, paste it into PowerShell at the
    command prompt, and then run it.  
    ‎  
    ‎This command changes all existing adatum.com accounts to the new UPN
    \@xxxUPNxxx.xxxCustomDomainxxx.xxx domain:  
    ‎  
    `Get-ADUser -Filter * -Properties SamAccountName | ForEach-Object {Set-ADUser $_ -UserPrincipalName ($_.SamAccountName + "@xxxUPNxxx.xxxCustomDomainxxx.xxx" )}`

9. Wait for PowerShell to complete the prior command and return to the command
    prompt, and then close the Windows PowerShell window.

10. Close Notepad (do not save the untitled document).

11. Leave the Edge browser and all tabs open and proceed to the next task.

## Task 4: Enable Exchange for the Custom Domain

In this task, you will log into the on-premises Exchange Server (LON-EX1) VM and
enable your Exchange on-premises environment for the accepted domain
(**xxxUPNxxx.xxxCustomDomainxxx.xxx**) that you added and configured in the
prior tasks. You will run a series of PowerShell commands in the Exchange
Management Shell, and you will update additional settings in the on-premises
Exchange Admin Center. In the prior task, you ran the PowerShell commands in Windows PowerShell on LON-DC1. In this task, you will run Exchange-specific PowerShell commands on LON-EX1; therefore, you will use the Exchange Management Shell rather than Windows PowerShell.

To save you from having to manually type in the commands (which are quite lengthy) into the Exchange Management Shell, you will copy the commands from these instructions and then paste them into Notepad, just as you did in the prior task. You will then use the "Replace" functionality in Notepad to find and replace the custom domain name placeholder in the commands with the actual domain name, and then you will copy and paste each command from Notepad into the Exchange Management Shell.

1. Switch to **LON-EX1** and, if necessary, log in as the **Administrator**
    with a password of **Pa55w.rd**. If you had to log in and the **Server
    Manager** application automatically opened, then close it now.

2. In this task, you will enter a series of Exchange-specific PowerShell
    commands through the **Exchange Management Shell**. These commands will
    enable your on-premises Exchange environment for the new
    **xxxUPNxxx.xxxCustomDomainxxx.xxx** accepted domain.  
    ‎  
    ‎To expedite running these commands, open **Notepad** just as you did in the
    prior task, maximize the Notepad window, and then copy **steps 5-15**
    below and paste them into the Notepad document (to make it easy, copy all
    the text for steps 5-15 and not just the PowerShell commands; that way you
    can do one Copy statement rather than 11 Copy statements of just the
    PowerShell commands).

    **Warning:** Some lab hosting providers’ VM environments limit the amount
    of text that can be copy and pasted at one time into a VM. If this occurs
    within your VM environment, you may have to copy and paste steps 5-15 in
    chunks to get all 11 steps copied into Notepad.

    **Note: your lab provider may have already updated the PowerShell commands in Steps 5-15 with the correct custom domain name so you can simply copy and paste the PowerShell commands.**

3. In the prior task, after you copied the two steps into Notepad, you did one
    mass replace on xxxUPNxxx.xxxCustomDomainxxx.xxx. However, in this task, one
    of the commands just references xxxCustomDomainxxx.xxx and not the xxxUPNxxx
    UPN name, so in this task, you should replace each portion of the domain
    name separately.  
    ‎  
    ‎After copying the commands from steps 5-15 into Notepad, perform the
    following two (2) **Replace** commands in Notepad:

    - Replace all instances of **xxxUPNxxx** with the **UPN Name** provided by
        your lab hosting provider.

    - Replace all instances of **xxxCustomDomainxxx.xxx** with the accepted
        domain provided by your lab hosting provider.

    - **Important:** Review the Notepad document and verify that all instances
        of xxxUPNxxx have been replaced with your UPN Name, and all instances of
        xxxCustomDomainxxxx.xxx have been replaced with your new domain name.

    - Close the **Replace** window.

4. To open the **Exchange Management Shell**, select the Windows icon on the
    bottom left corner of the taskbar, and then in the menu select **Microsoft
    Exchange Server 2019** to expand this program group, and then in the group,
    select **Exchange Management Shell**.

    Maximize the **Exchange Management Shell** window once it opens. Wait for
    the command prompt to appear before proceeding.

5. You will now begin the process of copying each of the PowerShell commands in
    Notepad and then pasting and running them in the Exchange Management Shell.  
    ‎  
    ‎Select the **Notepad** icon on the taskbar, and in your Notepad document,
    start with this Step 5.  
    ‎  
    ‎Select the following PowerShell command from step 5 in the Notepad document,
    right-click on it, and select **Copy**, paste it into the Exchange
    Management Shell at the command prompt (right click on the command prompt
    and select **Paste;** Note – in some VM environments, just right-clicking at
    the command prompt will paste in the copied command), and then press Enter
    on your keyboard.  
    ‎  
    ‎This command will add a new send connector with a wildcard (asterisk) to
    accept all emails from any domain:  
    ‎  
    `New-SendConnector -Name "To Internet" -AddressSpaces "*"`

6. Copy the following command from Notepad, paste it into the Exchange
    Management Shell at the command prompt, and then run it. This command will
    add the accepted xxxUPNxxx.xxxCustomDomainxxx.xxx domain as a Micro, set it
    as a trusted domain, and assign it the Alias of A.Datum:

    `New-AcceptedDomain -DomainName "xxxUPNxxx.xxxCustomDomainxxx.xxx" -DomainType Authoritative -Name "A.Datum"`

7. Copy the following command from Notepad, paste it into the Exchange
    Management Shell at the command prompt, and then run it. This command will
    set the default email policy for every user to have its primary email
    address as the accepted domain of xxxUPNxxx.xxxCustomDomainxxx.xxx:

    `Set-EmailAddressPolicy -Identity "Default Policy" -EnabledPrimarySMTPAddressTemplate "SMTP:%m@xxxUPNxxx.xxxCustomDomainxxx.xxx"`

8. Copy the following command from Notepad, paste it into the Exchange
    Management Shell at the command prompt, and then run it. This command will
    update the default email policy that was just changed in the previous
    command:

    `Update-EmailAddressPolicy -Identity "Default Policy"`

9. Copy the following command from Notepad, paste it into the Exchange
    Management Shell at the command prompt, and then run it. This command will
    set the internal and external address for the OWA Virtual Directory to
    <https://xxxUPNxxx.xxxCustomDomainxxx.xxx/OWA>:

    `Set-OwaVirtualDirectory -Identity "LON-EX1\OWA (Default Web Site)" -ExternalUrl https://xxxUPNxxx.xxxCustomDomainxxx.xxx/OWA -InternalUrl https://xxxUPNxxx.xxxCustomDomainxxx.xxx/OWA`
    ‎  
    ‎**NOTE:** Ignore the warning that’s displayed. This warning is addressed
    when you run the next command.

10. Copy the following command from Notepad, paste it into the Exchange
    Management Shell at the command prompt, and then run it. This command will
    set the internal and external address for the ECP Virtual Directory to
    <https://xxxUPNxxx.xxxCustomDomainxxx.xxx/ECP>:

    `Set-EcpVirtualDirectory -Identity "LON-EX1\ECP (Default Web Site)" -ExternalUrl https://xxxUPNxxx.xxxCustomDomainxxx.xxx/ECP -InternalUrl https://xxxUPNxxx.xxxCustomDomainxxx.xxx/ECP`

11. Copy the following command from Notepad, paste it into the Exchange
    Management Shell at the command prompt, and then run it. This command will
    set the internal and external address for the Active Sync Virtual Directory
    to <https://xxxUPNxxx.xxxCustomDomainxxx.xxx/Microsoft-Server-Activesync>:

    `Set-ActiveSyncVirtualDirectory -Identity "LON-EX1\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl https://xxxUPNxxx.xxxCustomDomainxxx.xxx/Microsoft-Server-Activesync -InternalUrl https://xxxUPNxxx.xxxCustomDomainxxx.xxx/Microsoft-Server-Activesync`

12. Copy the following command from Notepad, paste it into the Exchange
    Management Shell at the command prompt, and then run it. This command will
    set the internal and external address for the Web Services Virtual Directory
    to <https://xxxUPNxxx.xxxCustomDomainxxx.xxx/ews/exchange.asmx>:

    `Set-WebServicesVirtualDirectory -Identity "LON-EX1\EWS (Default Web Site)" -ExternalUrl https://xxxUPNxxx.xxxCustomDomainxxx.xxx/ews/exchange.asmx -InternalUrl https://xxxUPNxxx.xxxCustomDomainxxx.xxx/ews/exchange.asmx`
    ‎  
    ‎**NOTE:** This command takes a little time to process once you hit Enter. After several seconds (possibly up to 10-20 seconds), you will receive a prompt that indicates the InternalURL parameter can’t be resolved. At the prompt, enter **A** for **Yes to All** to continue and then press **Enter**.

13. Copy the following command from Notepad, paste it into the Exchange
    Management Shell at the command prompt, and then run it. This command will
    set the internal and external address for the OAB Virtual Directory to
    <https://xxxUPNxxx.xxxCustomDomainxxx.xxx> /OAB:

    `Set-OabVirtualDirectory -Identity "LON-EX1\OAB (Default Web Site)" -ExternalUrl https://xxxUPNxxx.xxxCustomDomainxxx.xxx/OAB -InternalUrl https://xxxUPNxxx.xxxCustomDomainxxx.xxx/OAB`

14. Copy the following command from Notepad, paste it into the Exchange
    Management Shell at the command prompt, and then run it. This command will
    set the internal and external address for the Outlook Anywhere external host
    name to xxxUPNxxx.xxxCustomDomainxxx.xxx and to set the authentication
    method to NTLM and to require external clients to use SSL to make the
    connection:

    `Set-OutlookAnywhere -Identity "LON-EX1\Rpc (Default Web Site)" -ExternalHostname xxxUPNxxx.xxxCustomDomainxxx.xxx -ExternalClientsRequireSsl $true -ExternalClientAuthenticationMethod NTLM -InternalHostname xxxUPNxxx.xxxCustomDomainxxx.xxx -InternalClientsRequireSsl $true -InternalClientAuthenticationMethod NTLM`

15. Copy the following command from Notepad, paste it into the Exchange
    Management Shell at the command prompt, and then run it. This command will
    set the Outlook certificate to \*.xxxCustomDomainxxx.xxx:

    `Set-OutlookProvider EXPR -CertPrincipalName:*.xxxCustomDomainxxx.xxx`
    ‎

16. Close your Exchange Management Shell window.

17. Close Notepad (do not save the untitled document).

18. To enable Exchange for the custom domain, you must identify the Exchange
    services that you want to assign to the \*.xxxCustomDomainxxx.xxx
    certificate.  
    ‎  
    ‎If you have a tab open in your Edge browser for the on-premises **Exchange
    admin center,** then proceed to the next step; otherwise, select the
    **Windows** icon on the taskbar, select the **Microsoft Exchange Server
    2019** group, select **Exchange Administrative Center.**

    **Note:** If you receive a page indicating **This site is not secure**, this
    is due to a certificate issue in the VM environment that you can ignore for
    the purpose of this lab. To bypass this error, select **More information**,
    and then select **Go on to the webpage (not recommended)**.

19. In the **Exchange Admin Center**, log in as **adatum\\Administrator** with a
    password of **Pa55w.rd**.

20. In the **Exchange admin center**, select **servers** in the left-hand
    navigation pane.

21. On the **servers** page, the **servers** tab is displayed by default in the
    list of tabs across the top of the page. Select the **certificates** tab.

22. In the list of certificates, select the **wildcard_xxxCustomDomainxxx_xxx**
    certificate (where xxxCustomDomainxxx_xxx is the name of your accepted
    domain) and then select the **pencil (Edit)** icon on the menu bar.

23. You will now specify the Exchange services that you want to assign to this certificate for your accepted domain. In the **wildcard_xxxCustomDomainxxx_xxx** window, select **services** in the left-hand pane.

24. In the list of services, select the **SMTP** check box and the **IIS** check
    box, and then select **Save**. Select **Yes** in the **Warning** dialog box
    that appears.

25. In the **Exchange admin center**, select **mail flow** in the left-hand
    navigation pane and then select the **accepted domains** tab at the top of
    the page.

26. In the list of accepted domains, you must set the **A.Datum** domain (where
    the **Accepted Domain** is xxxUPNxxx.xxxCustomDomainxxx.xxx) as the Default
    domain. Select this domain (if it’s not already selected by default), then
    select the **pencil (Edit)** icon on the menu bar above the list of domains.

27. In the **A.Datum** window, under the **This accepted domain is** setting,
    verify the **Authoritative** option is selected (this should have been set
    to Authoritative in the step 6 PowerShell command). Then select the **Make
    this the default domain** check box and select **Save**.  
    ‎  
    ‎In the list of domains, the **A.Datum** domain should now be listed as the
    **default domain** and the **Domain Type** should be **Authoritative**.

28. Close the Edge browser so that you close the Exchange admin center and
    proceed to the next task.

## Task 5: Migrate On-premises User Accounts to the Custom Domain

In this lab, you will log into the Domain Controller (LON-DC1) VM and enable
directory synchronization. To do this, you must first download the setup wizard
for the Microsoft Azure Active Directory Connect tool. You will then run the
installation wizard to enable and configure directory synchronization. This will
perform a full synchronization that migrates all of Adatum’s on-premises user
accounts to the new accepted domain in Microsoft 365.

1. Switch to **LON-DC1** and, if necessary, log in as the **Administrator**
    with a password of **Pa55w.rd**.

2. In your Edge browser session, the **Microsoft Office Home** tab and the
    **Microsoft 365 admin center** tab should still be open; if not, then
    navigate to them now.  
    ‎  
    ‎Select the **Microsoft 365 admin center** tab, which should be displaying
    the **Domains** page.

3. In the **Microsoft 365 admin center**, in the left-hand navigation pane,
    select **Users**, and then select **Active users**.

4. You are now going to navigate to the **Microsoft Download Center** to
    download the **Azure AD Connect** tool.  
    ‎  
    ‎In the **Active users** window, on the menu bar, select the **ellipsis (More
    actions)** icon, and then in the drop-down menu that appears, select
    **Directory synchronization**.  
    ‎  
    ‎**Note:** If the **ellipsis (…)** icon does not appear on the menu bar, then
    at the very top of the left-hand navigation pane, select the **Navigation
    menu (three vertical lines)** icon to minimize the navigation pane, which
    removes the text. This expands the size of the **Active users** page, so the
    ellipsis icon should now appear on the menu bar. If for some reason you
    cannot locate the **Directory synchronization** option, then you can
    navigate directly to the **Azure AD Connect** page in the **Microsoft
    Download Center** by opening a new tab in your Edge browser and entering the
    following URL in the address bar (if you navigate directly to this URL, you
    can skip the next step): **<https://www.microsoft.com/en-us/download/details.aspx?id=47594>**

5. In the **Azure Active Directory preparation** window, select **Go to the
    Download center to get the Azure AD Connect tool**. This opens a new tab in
    your browser and takes you to the Microsoft Download Center.

6. In the **Microsoft Download Center**, scroll down to the **Microsoft Azure
    Active Directory Connect** section and select the **Download** button.

7. The notification bar at the top of the
    page will display the status of the download operation. Once the download is complete, select **Open file** that appears below the **AzureADConnect.msi**
    file.

8. This initiates the installation of the **Microsoft Azure Active Directory
    Connect Tool**.

    **Note:** After the wizard begins, the **Microsoft Azure AD Connect Tool**
    window may disappear. If this occurs, find the icon for it on the task bar
    and select it.

    On the **Welcome to Azure AD Connect** window in the setup wizard, select
    the **I agree to the license terms and privacy notice** check box and then
    select **Continue**.

9. On the **Express Settings** page, read the instruction regarding a single
    Windows Server AD forest (which is the scenario in your VM lab environment)
    and then select **Use express settings**.

10. On the **Connect to Azure AD** window, you must enter the user credentials
    for a Microsoft 365 user account that has been assigned the Microsoft 365
    Global Administrator role. Enter **admin\@xxxxxZZZZZZ.onmicrosoft.com**
    (where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting
    provider) in the **USERNAME** field, enter (or copy and paste) the tenant
    email password provided by your lab hosting provider in the **PASSWORD**
    field, and then select **Next.**

    **Note:** You may have to tab out of the **PASSWORD** field to enable the
    **Next** button.

11. On the **Connect to AD DS** page, enter **adatum\\Administrator** in the
    **USERNAME** field, enter **Pa55w.rd** in the **PASSWORD** field, and then
    select **Next.**

    **Note:** You may have to tab out of the **PASSWORD** field to enable the
    **Next** button.

12. In the **Azure AD sign-in configuration** window, select the **Continue
    without matching all UPN suffixes to verified domains** check box at the
    bottom of the page and then select **Next**.

13. On the **Ready to configure** screen, select the **Start the synchronization
    process when configuration completes** check box (if it’s not already
    selected), and select the **Exchange hybrid deployment** check box since you
    are preparing Azure AD Connect for an Exchange hybrid deployment.

    Select **Install**.

14. The installation will usually take 5 to 10 minutes to complete. On the
    **Configuration complete** window, verify you receive a message at the top
    of the window indicating **Azure AD Connect configuration succeeded. The synchronization process has been initiated**.
    Ignore the warning indicating the Active Directory Recycle Bin is not
    enabled for your forest. This recycle bin will not be needed for the
    purposes of this VM lab environment.  
    ‎  
    ‎Select **Exit**.

15. In the taskbar at the bottom of the screen, select the **magnifying glass
    (Search)** icon, and then in the Search box, enter **sync**. In the menu
    that appears, select the **Synchronization Service** desktop application to
    open it.

16. Maximize the **Synchronization Service Manager** window.

17. In the **Synchronization Service Manager** window, on the ribbon at the top
    of the page, the **Operations** tab is displayed by default so that you can
    monitor the synchronization process.

18. Wait for the **Export** profile to complete for
    **xxxxxZZZZZZ.onmicrosoft.com** (the second task in the list); when it
    finishes, its **Status** should be **completed-export-errors**.  
    ‎  
    ‎Once this status appears, select this row.

19. In the bottom portion of the screen, a detail pane appears showing the
    detailed information for this operation that you just selected.

    - In the **Export Statistics** section, note the number of users that were
        added and the number that were updated.

    - In the **Export Errors** section on the right, note the two errors that
        appear. Select the link for the first error that appears under the
        **Export Errors** column.

        The first error is an “add user”” error for user **Ngoc Bich Tran**.
        Review the error and then close the window. Select the link for the
        second error, which is an “add user” error for user **An Dung Dao**.
        Review this error and then close the window.

    - So why did synchronization fail for these two users?

        To find out, select the **DataValidationFailed** link for the first error (under the **2 Error(s)** column). In the window that appears, select the **Detail** button. The **Error Information** window that appears indicates Ngoc Bich Tran's on-premises user account has an invalid UPN, which in
        turn caused a UPN validation error during the synchronization process;
        therefore, Ngoc's on-premises user account was not synchronized to Microsoft 365 by the Azure AD Connect
        tool. Select **Close** to close this window, and then select **Close** to close the Error Information window.

        If you select the **DataValidationFailed** link for the second error and then select the **Detail** button, you will note that An Dung Dao experienced the same UPN validation error.

    - **IMPORTANT:** Because a synchronization had not been performed prior to
        this, the initial synchronization was a **Full Synchronization** (see
        the **Profile Name** column in the **Connector Operations** pane at the
        top of the page). Because the synchronization process will continue to
        run automatically every 30 minutes, any subsequent synchronizations will
        display **Delta Synchronization** as its **Profile Name**.

        If you leave the **Synchronization Service Manager** window open, after 30 minutes
        you will see that it attempts to synchronize the two users who were not
        synchronized during the initial synchronization. This operation will display as a
        **Delta Synchronization**.

20. Close the **Synchronization Service Manager**.

21. In your Edge browser, close the **Download Microsoft Azure AD Connect** tab,
    and then in the **Microsoft 365 admin center** tab, close the **Azure Active
    Directory preparation** pane. This will return you to the **Active users**
    list.  
    ‎  
    ‎**Note:** If you had to select the **Navigation menu** icon at the very top
    of the left-hand navigation pane in the earlier step to see the ellipsis
    icon, then select this **Navigation menu** icon again to expand the pane and
    display the text associated with each icon. Seeing the text associated with
    each icon makes it easier to navigate through the admin center.

22. On the **Active users** page, note that all the existing Microsoft 365 user
    accounts are the predefined users that were created in your tenant by your
    lab hosting provider.

    Select **Refresh** on the menu bar to see all
    the on-premises user accounts that were migrated to the new accepted domain
    in Microsoft 365.  
    ‎  
    ‎Note the **Username** for each of these accounts, which should be in the
    format of **\&lt;alias&gt;\@xxxUPNxxx.xxxCustomDomainxxx.xxx**. Also note
    that each of these user accounts is **Unlicensed**; this indicates that
    while the on-premises accounts have been migrated to the new domain in
    Microsoft 365, they have not been assigned an Office 365 license.  
    ‎  
    ‎If you scroll down through the list of **Active users**, note that you will
    see both unlicensed and licensed users; the licensed users are the original
    list of Microsoft 365 user accounts created by your lab hosting provider.

23. On the right-side of the menu bar at the top of the page, select **Filter**.
    In the menu that appears, select **Licensed users**. This will display only
    those user accounts that were all assigned an Office 365 license (these are
    the Microsoft 365 user accounts that were created by your lab hosting
    provider).  
    ‎  
    ‎In the **Username** column, note how these user accounts were assigned to
    the **xxxxxZZZZZZ.onmicrosoft.com** domain when they were created by your
    lab hosting provider.

24. Note how the **Filter** option on the menu bar now displays **Licensed
    users**. Select **Licensed users** and in the menu that appears, select
    **Unlicensed users**. This will display all the user accounts that were just
    migrated from the on-premises **adatum.com** domain to the
    **xxxUPNxxx.xxxCustomDomainxxx.xxx** domain. The migration process did not
    assign a license to any of these new Microsoft 365 accounts that were just
    created. If you scroll down through this list, you should not see any of the
    licensed user accounts in the **xxxxxZZZZZZ.onmicrosoft.com** domain.  
    ‎  
    ‎In the **Username** column, note how these user accounts were assigned to
    the **xxxUPNxxx.xxxCustomDomainxxx.xxx** domain that you earlier created in
    Microsoft 365.  
    ‎

25. The **Filter** option on the menu bar should now display **Unlicensed
    users**. Select **Unlicensed users** and in the menu that appears, select
    **All users**. This will return you to the list of all active user accounts
    in both the **xxxUPNxxx.xxxCustomDomainxxx.xxx** and
    **xxxxxZZZZZZ.onmicrosoft.com** domains.  
    ‎  
    ‎Congratulations! You have just verified that the Full Synchronization
    process migrated Adatum’s on-premises user accounts to the new accepted
    domain.

26. Leave your Edge browser and all tabs open as it will be used in the next
    lab.

## Proceed to Lab 7 - Exercise 2
