# ado-agent-cloud-init

```
RG=rg-ado-agents-eastus
VMSS_NAME=customagentspool

az group create --location eastus --name $RG

az vmss create --name $VMSS_NAME --resource-group $RG --image UbuntuLTS --vm-sku Standard_D2_v3 --storage-sku StandardSSD_LRS --authentication-type SSH --instance-count 2 --disable-overprovision --upgrade-policy-mode manual --single-placement-group false --platform-fault-domain-count 1 --load-balancer "" 

az vmss extension set --vmss-name $VMSS_NAME --resource-group $RG --name CustomScript --version 2.0 --publisher Microsoft.Azure.Extensions --settings '{ "fileUris":["https://raw.githubusercontent.com/implodingduck/ado-agent-cloud-init/main/setup.sh"], "commandToExecute": "bash ./setup.sh" }'


```