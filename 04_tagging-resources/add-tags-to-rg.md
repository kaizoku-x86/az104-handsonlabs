## To Initialize a Basic Env:
Create a ```Resource Group``` called ```lab-rg-0```
The following ```az``` command will deploy a basic environment with:
- Storage Account
- Network Security Group
- Public IP Address
- Network Interface
- Virtual Network
- Virtual Machine
- Disk

>az deployment group create  \\ \
--name az104-handsonlab-basicdp \\ \
--resource-group lab-rg-0 \\ \
--template-file ./arm-templates/lab-rg-0.json \\ \
--no-wait 

## Add Tags to the Resource Group
First list the resource group

>$rg = Get-AzResourceGroup -Name lab-rg-0

Then add/update the tags list. This tags are 'local' tags for this resource

>az group update -n $rg.ResourceGroupName \\ \
--tags "Environment=Production" "Dept=IT" "CreatedBy=Kaizoku" "TagsBy=Update"

Alternative. This Tags are global in the Subscription

>az tag create --resource-id $rg.ResourceId \\ \
--tags Environment=Production Dept=IT CreateBy=Kaizoku TagsBy=Create

## Remove Tags for VM and add Tag MarkForDeletion

First list the vm in the Resource Group 

>$vm = Get-AzVM -ResourceGroupName $rg.ResourceGroupName

>az vm update --resource-group $rg.ResourceGroupName --name $vm.Name \\ \
--set tags.MarkForDeletion=Yes

## Change tags for a Virtual Network
First list the Vnet in the Resource Group

>$vnet = Get-AzVirtualNetwork -ResourceGroupName $rg.ResourceGroupName

This command should work with any kind of Resource by setting the ```--resource-type``` flag

>az resource tag -g $rg.ResourceGroupName -n $vnet.Name --resource-type="Microsoft.Network/virtualNetworks" \\ \
--tags "Dept=IT" "Environment=Production" "CreatedBy=Kaizoku"

# Clean your subscription
After play around, clean up your env.

>az group delete --resource-group $rg.ResourceGroupName