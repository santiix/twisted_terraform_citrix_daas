Twisted Terraform testing READ ME


The examples in the repository provided were normalized from working terraform files to provide you with visibility into whats needed in the file to get the Citrix Terraform Provider to work with a new or existing Azure deployment.

The examples assume there is nothing in the environment and are building from scratch in a clean resource location to create the following:  
Azure Hosting Connection, Resource Group, Machine Catalog and Delivery Group.

**Be Aware, Still In Tech Preview, not GA Yet!**
If you plan on using the Citrix Terraform Provider to manage an existing environment, you will need to use the import command within each module to import that data into your terraform configuration to use.
If not done correcty, you may wipe out existing infrastructure, so be careful.  FYI, even if you Fkup, you can recreate it back with Terraform! (I did!) LOL

**Import Details For Managing Existing Citrix Deployments**
You need to successfully import your configuration before you move forward.  If not, any portion that failed may become tainted and terraform will try to destroy
it, so review your "terraform plan" output carefully.

# IMPORT HYPERVISOR # 
First you need to download, install and run the Citrix DaaS Remote Powershell SDK: https://www.citrix.com/downloads/citrix-cloud/product-software/xenapp-and-xendesktop-service.html
To load the Citrix SDK, run asnp Citrix*  Then run the following command: Get-BrokerHypervisorConnection

**Take note of the: HypHypervisorConnectionUid**
terraform import citrix_daas_hypervisor.AZURE-HYPERVISOR HypHypervisorConnectionUid

# IMPORT HYPERVISOR POOL # 
If not already done so, you need to download, install and run the Citrix DaaS Remote Powershell SDK: https://www.citrix.com/downloads/citrix-cloud/product-software/xenapp-and-xendesktop-service.html
To load the Citrix SDK, run asnp Citrix*  Then run the following command:dir XDHyp:\HostingUnits

**Take note of the: HostingUnitUid** 
terraform import citrix_daas_hypervisor_resource_pool.RESOURCE-POOL HypHypervisorConnectionUid,HostingUnitUid


