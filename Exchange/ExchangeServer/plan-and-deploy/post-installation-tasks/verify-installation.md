---
title: "Verify an Exchange 2016 installation"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 6/8/2018
ms.audience: ITPro
ms.topic: get-started-article
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.collection: Strat_EX_Admin
ms.assetid: fdd20a2a-c8c1-4d17-b813-3c05d88a4411
description: "Summary: Learn how to verify your Exchange 2016 installation and make troubleshooting easier."
---

# Verify an Exchange 2016 installation

 **Summary**: Learn how to verify your Exchange 2016 installation and make troubleshooting easier.
  
After you install Microsoft Exchange Server 2016, we recommend that you verify the installation by running the **Get-ExchangeServer** cmdlet and by reviewing the setup log file. If the setup process fails or errors occur during installation, you can use the setup log file to track down the source of the problem.
  
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
  
## Run Get-ExchangeServer

To verify that Exchange 2016 installed successfully, run the **Get-ExchangeServer** cmdlet in the Exchange Management Shell. A list is displayed of all Exchange 2016 server roles that are installed on the specified server when this cmdlet is run.
  
For detailed syntax and parameter information, see [Get-ExchangeServer](http://technet.microsoft.com/library/96543903-10fa-46fe-9ea0-90570ca0ad2e.aspx).
  
## Review the setup log file

You can also learn more about the installation and configuration of Exchange 2016 by reviewing the setup log file created during the setup process.
  
During installation, Exchange Setup logs events in the **Application** log of **Event Viewer** on computers that are running Windows Server 2012 and Windows Server 2012 R2. Review the **Application** log, and make sure there are no warning or error messages related to Exchange setup. These log files contain a history of each action that the system takes during Exchange 2016 setup and any errors that may have occurred. By default, the logging method is set to `Verbose`. Information is available for each installed server role.
  
You can find the setup log file at _\<system drive\>_\ExchangeSetupLogs\ExchangeSetup.log. The _\<system drive\>_ variable represents the root directory of the drive where the operating system is installed.
  
The setup log file tracks the progress of every task that is performed during the Exchange 2016 installation and configuration. The file contains information about the status of the prerequisite and system readiness checks that are performed before installation starts, the application installation progress, and the configuration changes that are made to the system. Check this log file to verify that the server roles were installed as expected.
  
We recommend that you start your review of the setup log file by searching for any errors. If you find an entry that indicates that an error occurred, read the associated text to determine the cause of the error.
  

