
#  Release Management Hints
This is not a step-by-step guide. Instead it's a collection of screenshots which will help you complete the DevOpsHack challenges.
This is on purpose: We want you to explore and play with the different options of VSTS.

***Hint: Before you switch windows or close your configuration, make sure you save your modification.***

## Create Release Definition in VSTS
![Create Release Definition](/ReleaseManagement/images/releaseManagementAdd.jpg)

## Choose a Release Definition template in VSTS
Start with an empty template!
![Choose a Release Definition template in VSTS](/ReleaseManagement/images/releaseManagementTemplate.jpg)

## Modify Release Definition Workflow in VSTS
* Make sure you connect the Output of the build definition as an input artifact.
* Make sure you set the trigger
* Add additional environments if required - you can specify if they should be targetd automatically
* Add "tasks" for your environment to describe the process of deployment

![Modify Release Definition Workflow in VSTS](/ReleaseManagement/images/releaseManagementWorkflow.jpg)

## Add task to deploy infrastructure on Azure
![Add task to deploy infrastructure on Azure](/ReleaseManagement/images/releaseManagementRG.jpg)

## Override parameters

**Make sure you copy the whole line and do not forget some leading or trailing parts of the string!**
**Hint:** Some browsers allow to triple-click the following line to mark it end to end. This allows easy copy & paste.)
In case you're wondering what you're doing here:
You're providing parameters for your ARM Template. Your ARM Template (FullEnvironmentSetupMerged.json) describes an infrastructure on Azure (Infrastructure as code). You typically parameterize this ARM template to be more flexible when it comes to e.g. website names or DB connections.

**Hint:** AdminPassword and AdminPasswordTest must be equal!

All parameter values like  $(myParametername) are "variables" within VSTS which need to be specified in the variables tab. Make sure you choose a globally unique entry for  servername & websitename.
Additionaly click the lock symbol for your passwords - this will make sure that you can use them, however they'll be hidden.

  ``` 
  -WebsiteName $(WebsiteName) -PartsUnlimitedServerName $(ServerName) -PartsUnlimitedServerAdminLogin AdminUser -PartsUnlimitedServerAdminLoginPassword "(ConvertTo-SecureString -String '$(AdminPassword)' -AsPlainText -Force)" -PartsUnlimitedServerAdminLoginPasswordForTest "(ConvertTo-SecureString -String '$(AdminTestPassword)' -AsPlainText -Force)" -PartsUnlimitedDBName PartsUnlimitedDB -PartsUnlimitedDBCollation SQL_Latin1_General_CP1_CI_AS -PartsUnlimitedDBEdition Basic -PartsUnlimitedHostingPlanName $(HostingPlan) -PartsUnlimitedHostingPlanSKU Standard -PartsUnlimitedHostingPlanWorkerSize 0 -EnableRules true -CdnStorageAccountName $(StorageAccountName) -CdnStorageContainerName $(ContainerName) -CdnStorageAccountNameForDev $(StorageAccountName)-dev -CdnStorageContainerNameForDev $(ContainerName)-dev -CdnStorageAccountNameForStaging $(StorageAccountName)-stage -CdnStorageContainerNameForStaging $(ContainerName)-stage  
```



## Specify all parameters
Make sure both passwords are equal!

![Specify paras as parameters](/ReleaseManagement/images/releaseManagementParajpg.JPG)
