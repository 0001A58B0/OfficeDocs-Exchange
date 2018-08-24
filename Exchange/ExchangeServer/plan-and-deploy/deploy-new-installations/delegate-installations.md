---
title: "Delegate the installation of an Exchange 2016 server"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 6/8/2018
ms.audience: ITPro
ms.topic: get-started-article
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.collection: Strat_EX_Admin
ms.assetid: f2fc8680-0c7c-4a29-b8f5-d77404fec280
description: "Summary: How to allow people who aren't members of the Organization Management role group to install Exchange."
---

# Delegate the installation of an Exchange 2016 server

 **Summary**: How to allow people who aren't members of the Organization Management role group to install Exchange.
  
Exchange Server 2016 lets you delegate the installation of Exchange servers to people who aren't members of the Exchange 2016 Organization Management role group. This is often helpful in large companies where the people who install and set up servers aren't the same people who manage services, like Exchange. If this sounds like something you want to do, this topic's for you.
  
Normally, when Exchange is installed, the people installing it need to be members of the [Organization Management](http://technet.microsoft.com/library/0bfd21c1-86ac-4369-86b7-aeba386741c8.aspx) role group. This is because when Exchange is installed, changes are made to Active Directory, and only Exchange administrators, who are members of the Organization Management role group, can make those changes. The following list shows the changes that are made: 
  
- A server object is created in the **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<Organization Name\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<Root Domain\>** configuration partition.
    
- The following access control entries (ACEs) are added to the server object within the configuration partition for the Delegated Setup role group:
    
  - Full Control on the server object and its child objects
    
  - Deny access control entry for the Send As extended right
    
  - Deny access control entry for the Receive As extended right
    
  - Deny CreateChild and DeleteChild permissions for Exchange Public Folder Store objects
    
    > [!NOTE]
    > Public folders are administered at an organizational level; therefore, the creation and deletion of public folder stores is restricted to Exchange administrators.
  
- The Active Directory computer account for the server is added to the Exchange Servers group.
    
- The server is added as a provisioned server in the Exchange Admin Center.
    
In large companies, the people who install and set up new servers often aren't Exchange administrators. To enable them to install Exchange, an Exchange administrator can *provision* the server in Active Directory. When a server is provisioned, all of the changes needed for the new Exchange server to function are made to Active Directory separately from the actual installation of Exchange on a computer. An Exchange administrator can provision a new server in Active Directory hours or even days before Exchange is installed on the new computer. After a server has been provisioned, the person doing the installation needs only to be a member of the [Delegated Setup](http://technet.microsoft.com/library/49362059-e53f-4135-ad2b-9edfbfff9a1e.aspx) role group to install Exchange. The Delegated Setup role group only allows members to install provisioned servers.
  
Keep the following in mind when thinking about using delegated setup:
  
- At least one Exchange 2016 server has to already be installed before you can delegate the installation of additional servers. The person who installs the first server needs to be an Exchange administrator.
    
- A delegated user can't uninstall an Exchange server. To uninstall an Exchange server, you need to be an Exchange administrator.
    
## How do I provision an Exchange 2016 server?

To provision a server for Exchange, you need to use Exchange 2016 command-line Setup. If you aren't very familiar with the Windows Command Prompt, don't worry. This topic steps you through exactly what you need to do. Before we start, here are a couple of things to keep in mind:
  
- You need to be a member of the Organization Management role group to provision a server.
    
- You should have the latest release of Exchange 2016. You can get the download link from [Install the Exchange 2016 Mailbox role using the Setup wizard](install-mailbox-role.md).
    
The command that you need to use to provision the server depends on whether you're running Setup from the computer you're provisioning or whether you're running it from another computer. Choose the command in the following steps that matches where you're running Setup:
  
1. Press the Windows key + 'R' to open the **Run** window.
    
2. In **Open**, typecmd.exe, and then press Enter to open a **Windows Command Prompt**.
    
3. Change directories to where you downloaded and expanded the Exchange 2016 install files. If the install files are located in  `C:\Downloads\Exchange 2016`, use the following command.
    
  ```
  CD "C:\Downloads\Exchange 2016"
  ```

4. Choose the command that matches where you're running Setup:
    
  - **If you're running Setup on the computer that's being provisioned**, run the following command:
    
    ```
    Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
    ```

  - **If you're running Setup on another computer**, run the following command:
    
    ```
    Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms
    ```

5. After you provision the server, you need to make sure that you've added the users who should be able to install Exchange on provisioned servers to the Delegated Setup role group. To see how to add users to a role group, see [Add members to a role group](../../permissions/role-group-members.md#add).
    
When you're done with these steps, the computer will be ready for Exchange to be installed. Exchange 2016 can be installed on a provisioned server by using the steps in [Install the Exchange 2016 Mailbox role using the Setup wizard](install-mailbox-role.md).
  
## How do I know this worked?

To make sure the server was properly provisioned for Exchange, you can do the following:
  
1. Go to **Start** \> **Administrative Tools**, and then open **Active Directory Users and Computers**.
    
2. Select **Microsoft Exchange Security Groups**, double-click **Exchange Servers**, and then select the **Members** tab.
    
3. On the **Members** tab, check to see if the server you just provisioned is listed as a member of the security group.
    
If your server is listed as a member of the Exchange Servers security group, it was properly provisioned. Someone who's a member of the Delegated Setup role group can now install Exchange on that server.
  
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
