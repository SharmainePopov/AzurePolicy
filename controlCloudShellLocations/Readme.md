#### Date : December 8 2020 ####
### Notice : These are samples only with no guarantees. Please validate in your own environment before use. ###
### Status : All info relating to Cloud Shell is what is pubicly available as of December 8 2020. If Cloud Shell configuration changes with subsequent Cloud Shell relases, these policies may need to be updated to remain useful. There is no specific intent to maintain these samples. ###

These policies might be able to control the deployment of Cloud Shell resources, to prevent creation outside of Allowed Locations. 
Cloud Shell environment set up creates a Resource Group, Storage Account, and an Azure Fileshare. 

In the write up below, DEFAULT Cloud Shell resources are what is created automatically when a user simply clicks the "Create Storage" button in the Cloud Shell interface. CUSTOM resources are what are created by clicking "Advanced Settings" and making choices. See Other Info section for a link which will explain this.

Other Info
-----------
Here is a link to current (December 8 2020) docs on Cloud Shell  https://docs.microsoft.com/en-us/azure/cloud-shell/persisting-shell-storage#create-new-storage 
Here is a link to current (December 8 2020) general info on Azure policy https://docs.microsoft.com/en-us/azure/governance/policy/overview

Overview
---------
If you apply both policies at the subscriptions scope, then   
a)Cloud Shell DEFAULT setup will not create any  Resource Groups or Storage Accounts outside of Allowed Locations. If the location chosesn by Cloud Shell during the default set up is outside of your Allowed Locations, the user will get an error.
b)Cloud Shell CUSTOM setup allow creation of a Resource Group outside Allowed Locations, but creation of the associated Storage Account will fail. The user will get an error. There will be empty Resource Groups that will need to be removed. A Policy implemented at the Subscription scope to Audit deployment of resources outside of Allowed Locations should report these as non-compliant.
c)Cloud Shell will allow the the environment setup of Resource Group and 


Policy : Deny Creation of Default Cloud Shell Resource Group Outside of Allowed Locations
------------------------------------------------------------------------------------------

What It Will Do :
----------------
DENY creation of NEW DEFAULT Cloud Shell Resource Groups outside of Allowed Locations. 
Use this Policy to prevent the creation of NEW DEFAULT Cloud Shell Resoure Groups outside of Allowed Locations. 
The creation of associated NEW DEFAULT Cloud Shell Storage Accounts are implicitly denied as well.
Users will get an error message.

What It Won't Do:
-----------------
This policy will not prevent the creation fo NEW CUSTOM Cloud Shell Resource Groups, or their associated Storage Accounts, outside of Allowed Locations. 
To prevent the creation of CUSTOM Cloud Shell Resource Groups outside of Allowed Locations, apply a DENY Policy at Subscription Scope, note that policy will then impact any Resource Group creation in the Subscription, not just to those created by Cloud Shell.
To prevent the creation of CUSTOM Cloud Shell Storage Accounts outside of Allowed Locatons use "Deny Creation of  Cloud Shell Storage Accounts Outside of Allowed Locations". The use of that Policy will allow a Custom Cloud Shell Resource Group to be created outside of Allowed Locations - but it will be empty, it will have no Storage Accounts created within. The user will get an error message.

What Else It Won't Do:
----------------------
This Policy will not impact any EXISTING reourses, Cloud Shell or otherwise,  or limit a user's ability to access EXISTNG resource for Cloud Shell use.
So a user can successfully select an EXISTING Resource Group, Storage Account and Fileshare during a CUSTOM set up of Cloud Shell, even those outside of Allowed Locatiosn. A user can also continue to use EXISTING DEFAULT Cloud Shell resources, even those outside of Allowed Locations.


Other Info:
Here is a link to current (December 8 2020) docs on Cloud Shell that explain what is set up by the DEFAULT configuration https://docs.microsoft.com/en-us/azure/cloud-shell/persisting-shell-storage#create-new-storage 
Here is a link to current (December 9 2020) docs on Cloud Shell that explain what is set up by the CUSTOM configuration 

Policy : Deny Creation of Default Cloud Shell Storage Accounts Outside of Allowed Locations
-------------------------------------------------------------------------------------------

What It Will Do
---------------
DENY creation of NEW Cloud Shell Storage Accounts  outside of allowed locations. This will work for DEFAULT and CUSTOM Cloud Shell configurations. But only for Storage Accounts, it does not prevent creation of Resource Groups.
Use this Policy to prevent the creation of CUSTOM Cloud Shell Storage Accounts  outside of Allowed Locations. 
To prevent the creation of DEFAULT Cloud Shell Storage Accounts outside of Allowed Locations, you should use "DENY creation of NEW Cloud Shell Storage Accounts Outside of Allowed Locations" because it will also prevent creation of the DEFAULT Cloud Shell Resource Group.

What It Won't Do
-----------------
There is no way to specifically prevent the creation of CUSTOM Cloud Shell Resource Groups outside of Allowed Locations. 
To prevent the creation of DEFAULT Cloud Shell Storage Accounts outside of Allowed Locatons use "Deny Creation of Default Cloud Shell  Resource Groups  Outside of Allowed Locations" which will prevent creation of both Resource Group and Storage Account.

