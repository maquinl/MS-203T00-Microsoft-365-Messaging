---
lab:
    title: 'Create Connectors'
    learning path: '[Learning Path 1: Manage the transport pipeline in Microsoft 365](https://learn.microsoft.com/en-us/training/paths/manage-transport-pipeline-microsoft-365/?azure-portal=true)'
    module: 'Module 2: Configure message transport'
---

# Lab Introduction

Adatum Corporation runs their legacy applications (such as Microsoft Exchange Server 2019) in an on-premises deployment. However, they recently subscribed to Microsoft 365, thereby creating a hybrid deployment in which they must synchronize their on-premises and cloud deployments.

Throughout the labs in this course, you will take on the persona of Holly Dickson, Adatum's Messaging Administrator. You have been tasked with integrating Adatum's on-premises Exchange environment with Microsoft 365 and Exchange Online. Adatum's project team has decided to implement Microsoft 365 in a pilot project that will not only provide them with experience using the product, but also enable them to match their messaging requirements with the Microsoft 365 feature set.

Your instructor will provide guidance on how to obtain your Microsoft 365 credentials in your lab-hosted environment. You will use these credentials throughout the remaining labs in this course.

In your lab environment, your lab hosting provider has already:

- Deployed the trial tenant
- Created a default tenant administrator account (known as the MOD Administrator)
- Created 9 additional user accounts
- Created a custom Microsoft 365 domain in Microsoft Azure
- Created the DNS records in Microsoft Azure that are required to support the custom domain and the selected Microsoft 365 services

1. On **LON-CL1**, you must select **Ctrl+Alt+Delete** to log in (your instructor will guide you on how to find this option in your VM environment). Log into LON-CL1 as the local Adatum administrator account that was created by your lab hosting provider (**Administrator**) with the password **Pa55w.rd**.

2. Once logged into **LON-CL1**, open an elevated instance of **Windows PowerShell**. Select the magnifying glass (Search) icon on the taskbar
   at the bottom of the screen ad type **powershell** in the Search box that appears. In the list of search results, right-click on **Windows
   PowerShell** (do NOT select Windows PowerShell ISE) and select **Run as administrator** in the drop-down menu.

3. Maximize your PowerShell window. In Windows PowerShell, at the command prompt, type the following command and press Enter:

      `Install-Module -Name ExchangeOnlineManagement`

4. You might be prompted "NuGet provider is required to continue", enter [Y] Yes [N] No [S] Suspend [?], enter **Y** to select **[Y] Yes**

5. If you are prompted to confirm whether you want to install the module from an untrusted repository (PSGallery), enter **A** to select **[A] Yes to
    All.**

6. At the command prompt, type the following command and press Enter:

     `Connect-ExchangeOnline`

7. A **Microsoft 365 Sign in** window will appear. Enter in the username for the **Mod Administrator** account provided by your learning provider
    (admin@M365xZZZZZZ.onmicrosoft.com) and then select **Next**.

8. In the **Enter password** window, enter the password for this admin account provided by your learning provider, and then select **Sign in**. It may take
    a moment to sign in before it returns a command prompt.

9. At the command prompt, type the following command and press Enter:

      `get-mailbox`

10. Close the PowerShell window.

## Exercise 1 - Create Connectors

As part of her pilot project for Adatum’s Exchange deployment, Holly wants to begin by creating custom send and receive connectors in her on-premises Exchange Server using the on-premises Exchange admin center.

Exchange uses connectors on Exchange servers to enable incoming and outgoing mail flow between services in the transport pipeline on the local Exchange server. In this lab you will log into the Exchange Server VM (LON-EX1) and create custom Receive and Send connectors using the on-premises Exchange Admin Center (EAC) for Adatum's Exchange Server 2019 deployment.

As you complete each task, you should leave the EAC open in your browser for the next lab. This will save you from having to open the EAC at the start of each lab.

### Task 1 - Obtain Your Microsoft 365 Credentials

Once you launch the lab, a free trial tenant will be automatically created for you to access Microsoft 365 in the Microsoft Virtual Lab environment. Within this tenant, your lab hosting provider will create a Microsoft 365 user account for a default tenant administrator named MOD Administrator. Your lab hosting provider will assign this user account a unique username and password, and the account will be assigned the Microsoft 365 Global administrator role. You must retrieve this username and password so that you can sign into Microsoft 365 within the Microsoft Virtual Lab environment. You will also be assigned a unique network IP address and UPN name for your Microsoft 365 blob. You will also use this UPN name in various tasks throughout the labs for this course.

Because this course can be offered by learning partners using any one of several authorized lab hosting providers, the actual steps involved to retrieve the UPN name, network IP address, and tenant ID associated with your tenant may vary by lab hosting provider. Therefore, your instructor will provide you with the necessary instructions on how to retrieve this information for your course.

You should write down the following information (provided by your instructor) for later use:

- **Tenant prefix.** This tenant prefix is for the Microsoft 365 user accounts that you will use to sign into Microsoft 365 throughout the labs in this course. The domain for each Microsoft 365 user account is in the format of {user alias}@xxxxxZZZZZZ.onmicrosoft.com, where xxxxxZZZZZZ is the tenant prefix. It consists of two parts - your lab hoster's prefix (xxxxx; some hosters use a generic prefix such as M365x, while others use their company initials or some other designation) and the tenant ID (ZZZZZZ; usually a 6 digit number). Record this xxxxxZZZZZZ tenant prefix value for later use. When any of the lab steps direct you to sign into Microsoft 365 as one of the user accounts (such as the MOD Administrator), you must enter the xxxxxZZZZZZ value that you obtained here as the tenant prefix portion of your .onmicrosoft.com domain.

- **Tenant password.** This is the password provided by your lab hosting provider for the tenant admin account.

- **Custom Domain name.** Your lab hosting provider has created a custom domain name for Adatum that you will use when adding a custom domain into Microsoft 365 in a later lab exercise. The domain name is in the format **xxxUPNxxx.xxxCustomDomainxxx.xxx.** You must replace **xxxUPNxxx** with the UPN name provided by your lab hosting provider, and you must replace **xxxCustomDomainxxx.xxx** with the lab hosting provider's domain name. For example, let's assume your lab hosting provider is Fabrikam Inc. If the UPN number it assigns to your tenant is AMPVU3a and its custom domain name is Fabrikam.us, then the domain name for your new custom domain would be AMPVU3a.fabrikam.us. Your instructor will provide you with your lab hosting provider's UPN number and custom domain name.  
- **Network IP address.** Write down the IP Address value (this is the IP Address of your parent domain (for example, 64.64.206.13).

### Task 2 - Create a Custom Receive Connector

Adatum has Microsoft Exchange Server 2019 installed on the Exchange Server VM (LON-EX1). In this task, you will use the Exchange admin center for Exchange Server 2019 to create a custom receive connector for Adatum's on-premises Exchange deployment.

1. Switch to the Exchange Server VM (LON-EX1) and log on as Adatum’s **Administrator** account with a password of **Pa55w.rd**.

2. After logging in, the **Server Manager** application will automatically open. Select the **X** in the upper-right corner of the screen to close it.

3. Holly wants to create custom connectors using the on-premises **Exchange Admin Center (EAC)**. To do so, select the **Windows** icon in the lower-left corner of the taskbar, and in the Start menu select the **Microsoft Exchange Server 2019** group. In the program group, select **Exchange Administrative Center**.

4. This will open **Microsoft Edge**, which will attempt to access the EAC. Maximize your browser window.

     Edge will display an error page indicating **Your connection isn't private**.

     Select **Advanced**, which displays a message indicating **This server couldn't prove that it's localhost; its security certificate is from LON-EX1. This may be caused by a misconfiguration or an attacker intercepting your connection.** You received this message because a certificate for the EAC was not included in your VM lab training environment. In a real-world deployment, this certificate would be required.

     Select **Continue to localhost (unsafe)**.

5. In the **Exchange Admin Center** log-in page, enter **adatum\Administrator** in the **Domain\user name** field and **Pa55w.rd** in the **Password** field, and then select **sign in**.

6. In the **Exchange admin center**, in the left-hand navigation pane, select **mail flow.**

7. You will begin by creating a custom receive connector. On the menu bar at the top of the **mail flow** page, select **receive connectors**.

8. On the **receive connectors** page, select the **plus (+) sign** icon on the menu bar to add a new receive connector.

9. In the **new receive connector** window that appears, enter **NewReceiveConnector1** in the **Name** field.

10. Under **Role**, select the **Frontend Transport** option.

11. Under **Type,** select the **Internet (For example, to receive internet mail)** option and then select **Next**.

12. This returns a **new receive connector** window in which you can update **Network Adapter Bindings** for the new receive connector. The purpose of this page is to identify the accepted IP addresses and port that are bound to this new receive connector. In other words, this new receive connector will only receive email from the IP address and port identified here before in turn sending it to the Exchange Server.  

    **Note:** In a real-world environment, some companies will create a receive connector that receives email from all IP addresses and a specific port, which in effect forces their email filters to do the heavy lifting of validating email from specific IP addresses for possible threats. Conversely, other companies that may have been hit by known threats will use custom receive connectors to only accept email from specific IP addresses they know are safe.
  
    When you create a new receive connector, you can select the IP addresses for that connector from the following options:  

    - All available IPv4 addresses  
    - All available IPv6 addresses  
    - A specific IPv4 or IPv6 address  

    When creating a new receive connector, this page displays the default combination of **All available IPv4** addresses and **Port 25** .

    Holly has decided use this default setting; therefore, select **Finish** to assign this default combination of IP addresses and port number to the new receive connector.  

    **IMPORTANT:** By selecting **Finish**, you will receive an **Error** message. You were purposely instructed to select **Finish** so that you can see this error, which indicates that the **Default Frontend LON-EX1** receive connector is already configured to accept all available IPv4 addresses (in other words, IP addresses 0.0.0.0 through 255.255.255.255) for Port 25. **Therefore, this new receive connector that you are creating must have a unique combination of IP address and port number that is different from any existing receive connectors.**

    Select **OK** to close the **Error** message.

13. This returns you to the **New receive connector** window. Select the **pencil (edit)** icon on the menu bar to edit the IP address and port number that will be linked to your new receive connector.

14. In the **edit IP address** window, under the **Address** field, select the **Specify an IPv4 address or an IPv6 address** option.

15. After receiving the previous error, Holly met with Adatum’s IT Administrator, who has identified **172.16.0.11** as the IP address he wants bound to this new receive connector (for port 25); therefore, enter this value in the **Address** field.

16. Leave the **Port** at **25**, and then select **Save**. Note how the Network adapter binding for this new receive connector now points to this IP address and port number.

    **Note:** By updating this network adapter binding, all email sent from the Internet and from IP address **172.16.0.11** through port 25 will be received by this new connector, which in turn will send it to Adatum's Exchange Server.

17. Select **Finish**. Your new receive connector should appear in the list of receive connectors.

18. Leave the Exchange Admin Center open in your browser for the next task.

### Task 3 - Create a Custom Send Connector

You will now create a custom send connector in Adatum’s on-premises Exchange Server (LON-EX1) using the on-premises EAC.

1. You should still be logged into LON-EX1 as the **Administrator** with a password of **Pa55w.rd**; however, if the log-in page appears, then log in now.

2. In your Edge browser session, the on-premises **Exchange admin center** should still be open; if not, then perform the same steps that you did in task 2 (steps 3-5) to open it now.

3. In the **Exchange admin center**, you should still be displaying the **receive connectors** tab on the **mail flow** page from the prior task. In the list of tabs at the top of the page, select the **send connectors** tab.

4. On the **send connectors** window, select the **plus (+) sign** icon on the menu bar to add a new send connector.

5. In the **new send connector** window, enter **NewSendConnector1** in the **Name** field.

6. Under **Type,** select the **Internet (For example, to send internet email)** option and then select **Next**.

7. This returns a **new send connector** window in which you can update **Network settings** for the new send connector. Select the **MX record associated with recipient domain** option and then select **Next**.

8. This returns a **new send connector** window in which you can update the connector’s **Address space**. Select the **plus (+) sign** to add a new address space record.

9. In the **add domain** window, you must enter the **Full Qualified Domain Name (FQDN)** of the domain associated with Adatum's Microsoft 365 tenant.

     **Note:** In Task 1 of this exercise, your instructor provided instruction on how to retrieve your tenant email address. Your FQDN is the value to the right of the @ sign in the **Tenant Email** (for example, **xxxxxZZZZZZ.onmicrosoft.com**, where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting provider). Enter your FQDN in the **Full Qualified Domain Name (FQDN)** field.

10. Leave the value of the **Cost** field to **1**, and then select **Save.**

11. Your new **Address space** record for this send connector should now be displayed. Select **Next**.

12. This returns a **new send connector** window in which you can update the **Source server** for the new send connector. Select the **plus (+) sign** to add a new Source server record.

13. In the **Select a Server** window, you want to select your **Mail server**, which in this virtual lab environment is your **LON-EX1** VM. Since the LON-EX1 server is selected by default, select the **add -&gt;** button, and then select **OK**.

14. LON-EX1 should now appear in the Source server list for this new send connector. Select **Finish**.

15. Close the Exchange admin center.

## End of Lab 1  
