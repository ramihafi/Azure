## 2 x VM-Series (4 NIC) for traditional Active/Passive
</br>
</br>
<p align="center">
<img src="https://raw.githubusercontent.com/wwce/azure-arm/master/Azure-Common-Deployments/v1/images/2fw_3nic_avset_active_passive.png">
</p>

### Overview
Please review [Set up Active/Passive HA on Microsoft Azure](https://docs.paloaltonetworks.com/vm-series/9-0/vm-series-deployment/set-up-the-vm-series-firewall-on-azure/configure-activepassive-ha-for-vm-series-firewall-on-azure.html) before proceeding.  

This template deploys the following into a new or existing VNET with 4 subnets:
* 2 x VM-Series firewalls
    * 3 x Interfaces
        * management: `<fw_name>-nic0`
        * dataplane1: `<fw_name>-nic1` (contains 2nd IP that floats between active & passive firewalls)
        * dataplane2: `<fw_name>-nic2` (contains 2nd IP that floats between active & passive firewalls)
        * HA2       : `<fw_name>-nic3`
    * Managed Disks
    * BYOL/Bundle1/Bundle2 License
    * (Optional) Accelerated Networking
    * (Optional) [Bootstrap Capable](https://docs.paloaltonetworks.com/vm-series/8-1/vm-series-deployment/bootstrap-the-vm-series-firewall/bootstrap-the-vm-series-firewall-in-azure)
    * (Optional) Public IPs for interfaces:
        * management: `<fw_name>-nic0-pip`
        * dataplane1: `<fw_name>-nic1-pip` (assigned to floating IP)
* 2 x Network Security Groups
    *  management: `<nsg_name>-mgmt`
    *  dataplane: `<nsg_name>-data`
* 1 x Availability Set

### Important Considerations

#### VNET Considerations
By default, the template will use the deployment resource group as the location of the VNET.  If the VNET is in a different resource group, the resource group must be specified at deployment time. If deploying a **new** VNET into a **different** resource group, the resource group **must exist** before deployment.

#### Template Modifications
Everything resource in the template is built strictly with variables.  The variables are defined based on the parameters values entered at deployment.  If you need to modify the template, most modifications can be done directly in the variable and parameter section without modifying the resource configuration.  

#### First Deployment
Most deployment failures are due to conflicts with existing resources.  If this is your first time running the template, it is recommended to launch the template into a **new** resource group.  If you cannot deploy to a new resource group, it is highly recommended to use the `optional-Append String To Resources` parameter to append a string to all newly created resources.  This will avoid potential naming conflicts among any existing resources.


[<img src="http://azuredeploy.net/deploybutton.png"/>](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Framihafi%2FAzure%2blob%2Fmaster%2FazureDeploy.json)
