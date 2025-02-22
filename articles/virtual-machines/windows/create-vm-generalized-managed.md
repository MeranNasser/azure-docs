---
title: Create VM from a managed image in Azure 
description: Create a Windows virtual machine from a generalized managed image using Azure PowerShell or the portal.
author: cynthn
ms.service: virtual-machines
ms.subservice: imaging
ms.workload: infrastructure-services
ms.topic: how-to
ms.date: 09/17/2018
ms.author: cynthn

---
# Create a VM from a managed image

**Applies to:** :heavy_check_mark: Windows VMs 

You can create multiple virtual machines (VMs) from an Azure managed VM image using the Azure portal or PowerShell. A managed VM image contains the information necessary to create a VM, including the OS and data disks. The virtual hard disks (VHDs) that make up the image, including both the OS disks and any data disks, are stored as managed disks. 

Before creating a new VM, you'll need to [create a managed VM image](capture-image-resource.md) to use as the source image and grant read access on the image to any user who should have access to the image. 

One managed image supports up to 20 simultaneous deployments. Attempting to create more than 20 VMs concurrently, from the same managed image, may result in provisioning timeouts due to the storage performance limitations of a single VHD. To create more than 20 VMs concurrently, use an [Azure Compute Gallery](../shared-image-galleries.md) (formerly known as Shared Image Gallery) image configured with 1 replica for every 20 concurrent VM deployments.

## Use the portal

1. Go to the [Azure portal](https://portal.azure.com) to find a managed image. Search for and select **Images**.
3. Select the image you want to use from the list. The image **Overview** page opens.
4. Select **Create VM** from the menu.
5. Enter the virtual machine information. The user name and password entered here will be used to log in to the virtual machine. When complete, select **OK**. You can create the new VM in an existing resource group, or choose **Create new** to create a new resource group to store the VM.
6. Select a size for the VM. To see more sizes, select **View all** or change the **Supported disk type** filter. 
7. Under **Settings**, make changes as necessary and select **OK**. 
8. On the summary page, you should see your image name listed as a **Private image**. Select **Ok** to start the virtual machine deployment.


## Use PowerShell

You can use PowerShell to create a VM from an image by using the simplified parameter set for the [New-AzVm](/powershell/module/az.compute/new-azvm) cmdlet. The image needs to be in the same resource group where you'll create the VM.

 

The simplified parameter set for [New-AzVm](/powershell/module/az.compute/new-azvm) only requires that you provide a name, resource group, and image name to create a VM from an image. New-AzVm will use the value of the **-Name** parameter as the name of all of the resources that it creates automatically. In this example, we provide more detailed names for each of the resources but let the cmdlet create them automatically. You can also create resources beforehand, such as the virtual network, and pass the resource name into the cmdlet. New-AzVm will use the existing resources if it can find them by their name.

The following example creates a VM named *myVMFromImage*, in the *myResourceGroup* resource group, from the image named *myImage*. 


```azurepowershell-interactive
New-AzVm `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVMfromImage" `
	-ImageName "myImage" `
    -Location "East US" `
    -VirtualNetworkName "myImageVnet" `
    -SubnetName "myImageSubnet" `
    -SecurityGroupName "myImageNSG" `
    -PublicIpAddressName "myImagePIP" 
```



## Next steps
[Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md)