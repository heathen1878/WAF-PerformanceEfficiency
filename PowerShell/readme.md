# PowerShell

[Home](../readme.md)

## <a name="Scaling"></a>Scaling 

Prerequisites...

* [Virtual Machine](https://github.com/heathen1878/Azure/blob/master/VirtualMachine/readme.md)

Scaling up and down

```powershell
# Get a list of VMs and select the one to work with
$vm = Get-AzVM | Out-GridView -Title 'Select the VM to resize' -PassThru

# Get a list of available VM sizes on the current cluster - you must make sure the new size supports all the existing features e.g. premium disks...
$newSize = Get-AzVMSize -ResourceGroupName $vm.ResourceGroupName -VMName $vm.Name | Select-Object Name | Out-GridView -Title 'Select the new VM Sku' -Passthru

# Update the VM
$vm.HardwareProfile.VmSize = $newSize.Name

# Update the VM
Update-AzVM -VM $vm -ResourceGroupName $vm.ResourceGroupName

```

Learn more [here](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/resize-vm)