---
title: "高可用性联合身份验证阶段 2 配置域控制器"
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 12/15/2017
ms.audience: ITPro
ms.topic: article
ms.service: o365-solutions
localization_priority: Normal
ms.collection:
- Ent_O365
- Ent_O365_Hybrid
- Ent_O365_Hybrid_Top
ms.custom:
- DecEntMigration
- Ent_Solutions
ms.assetid: 6b0eff4c-2c5e-4581-8393-a36f7b36a72f
description: "摘要： 在 Microsoft Azure 中配置域控制器和 Office 365 提供您的高可用性联合身份验证的目录同步服务器。"
ms.openlocfilehash: 86b5630f073a1c07dc2dbf270ac7e9d2220f7503
ms.sourcegitcommit: d31cf57295e8f3d798ab971d405baf3bd3eb7a45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2017
---
# <a name="high-availability-federated-authentication-phase-2-configure-domain-controllers"></a><span data-ttu-id="1ef0f-103">高可用性联合身份验证阶段 2：配置域控制器</span><span class="sxs-lookup"><span data-stu-id="1ef0f-103">High availability federated authentication Phase 2: Configure domain controllers</span></span>

 <span data-ttu-id="1ef0f-104">**摘要：**在 Microsoft Azure 中配置域控制器和 Office 365 提供您的高可用性联合身份验证的目录同步服务器。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-104">**Summary:** Configure the domain controllers and DirSync server for your high availability federated authentication for Office 365 in Microsoft Azure.</span></span>
  
<span data-ttu-id="1ef0f-p101">在为 Azure 基础结构服务中的 Office 365 联合身份验证部署高可用性的这一阶段中，可以在 Azure 虚拟网络中配置两个域控制器和目录同步服务器。然后用于身份验证的客户端 Web 请求可以在 Azure 虚拟网络中进行身份验证，而不是将通过站点到站点 VPN 连接的该身份验证流量发送到本地网络。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p101">In this phase of deploying high availability for Office 365 federated authentication in Azure infrastructure services, you configure two domain controllers and the DirSync server in the Azure virtual network. Client web requests for authentication can then be authenticated in the Azure virtual network, rather than sending that authentication traffic across the site-to-site VPN connection to your on-premises network.</span></span>
  
> [!NOTE]
> <span data-ttu-id="1ef0f-107">Active Directory 联合身份验证服务 (AD FS) 不能用 Azure Active Directory 域服务代替 Windows Server AD 域控制器。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-107">Active Directory Federation Services (AD FS) cannot use Azure Active Directory Domain Services as a substitute for Windows Server AD domain controllers.</span></span> 
  
<span data-ttu-id="1ef0f-p102">您必须先完成这一阶段之前移动到[高可用性联合身份验证阶段 3： 配置 AD FS 服务器](high-availability-federated-authentication-phase-3-configure-ad-fs-servers.md)。请参阅[Office 365 Azure 中部署高可用性联合身份验证](deploy-high-availability-federated-authentication-for-office-365-in-azure.md)所有阶段。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p102">You must complete this phase before moving on to [High availability federated authentication Phase 3: Configure AD FS servers](high-availability-federated-authentication-phase-3-configure-ad-fs-servers.md). See [Deploy high availability federated authentication for Office 365 in Azure](deploy-high-availability-federated-authentication-for-office-365-in-azure.md) for all of the phases.</span></span>
  
## <a name="create-the-domain-controller-virtual-machines-in-azure"></a><span data-ttu-id="1ef0f-110">在 Azure 中创建域控制器虚拟机</span><span class="sxs-lookup"><span data-stu-id="1ef0f-110">Create the domain controller virtual machines in Azure</span></span>

<span data-ttu-id="1ef0f-111">首先，您需要填写表格 M 的**虚拟机名称**列中，根据需要在**最小大小**列中修改虚拟机大小。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-111">First, you need to fill out the **Virtual machine name** column of Table M and modify virtual machine sizes as needed in the **Minimum size** column.</span></span>
  
|<span data-ttu-id="1ef0f-112">**项**</span><span class="sxs-lookup"><span data-stu-id="1ef0f-112">**Item**</span></span>|<span data-ttu-id="1ef0f-113">**虚拟机的名称**</span><span class="sxs-lookup"><span data-stu-id="1ef0f-113">**Virtual machine name**</span></span>|<span data-ttu-id="1ef0f-114">**插图**</span><span class="sxs-lookup"><span data-stu-id="1ef0f-114">**Gallery image**</span></span>|<span data-ttu-id="1ef0f-115">**存储类型**</span><span class="sxs-lookup"><span data-stu-id="1ef0f-115">**Storage type**</span></span>|<span data-ttu-id="1ef0f-116">**最小大小**</span><span class="sxs-lookup"><span data-stu-id="1ef0f-116">**Minimum size**</span></span>|
|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="1ef0f-117">1.</span><span class="sxs-lookup"><span data-stu-id="1ef0f-117">1.</span></span>  <br/> |<span data-ttu-id="1ef0f-118">______________（第一个域控制器，例如 DC1）</span><span class="sxs-lookup"><span data-stu-id="1ef0f-118">______________ (first domain controller, example DC1)</span></span>  <br/> |<span data-ttu-id="1ef0f-119">Windows Server 2016 数据中心</span><span class="sxs-lookup"><span data-stu-id="1ef0f-119">Windows Server 2016 Datacenter</span></span>  <br/> |<span data-ttu-id="1ef0f-120">StandardLRS</span><span class="sxs-lookup"><span data-stu-id="1ef0f-120">StandardLRS</span></span>  <br/> |<span data-ttu-id="1ef0f-121">Standard_D2</span><span class="sxs-lookup"><span data-stu-id="1ef0f-121">Standard_D2</span></span>  <br/> |
|<span data-ttu-id="1ef0f-122">2.</span><span class="sxs-lookup"><span data-stu-id="1ef0f-122">2.</span></span>  <br/> |<span data-ttu-id="1ef0f-123">______________（第二个域控制器，例如 DC2）</span><span class="sxs-lookup"><span data-stu-id="1ef0f-123">______________ (second domain controller, example DC2)</span></span>  <br/> |<span data-ttu-id="1ef0f-124">Windows Server 2016 数据中心</span><span class="sxs-lookup"><span data-stu-id="1ef0f-124">Windows Server 2016 Datacenter</span></span>  <br/> |<span data-ttu-id="1ef0f-125">StandardLRS</span><span class="sxs-lookup"><span data-stu-id="1ef0f-125">StandardLRS</span></span>  <br/> |<span data-ttu-id="1ef0f-126">Standard_D2</span><span class="sxs-lookup"><span data-stu-id="1ef0f-126">Standard_D2</span></span>  <br/> |
|<span data-ttu-id="1ef0f-127">3.</span><span class="sxs-lookup"><span data-stu-id="1ef0f-127">3.</span></span>  <br/> |<span data-ttu-id="1ef0f-128">______________ （目录同步服务器，示例 DS1）</span><span class="sxs-lookup"><span data-stu-id="1ef0f-128">______________ (DirSync server, example DS1)</span></span>  <br/> |<span data-ttu-id="1ef0f-129">Windows Server 2016 数据中心</span><span class="sxs-lookup"><span data-stu-id="1ef0f-129">Windows Server 2016 Datacenter</span></span>  <br/> |<span data-ttu-id="1ef0f-130">StandardLRS</span><span class="sxs-lookup"><span data-stu-id="1ef0f-130">StandardLRS</span></span>  <br/> |<span data-ttu-id="1ef0f-131">Standard_D2</span><span class="sxs-lookup"><span data-stu-id="1ef0f-131">Standard_D2</span></span>  <br/> |
|<span data-ttu-id="1ef0f-132">4.</span><span class="sxs-lookup"><span data-stu-id="1ef0f-132">4.</span></span>  <br/> |<span data-ttu-id="1ef0f-133">______________ （第一个 AD FS 服务器，示例 ADFS1）</span><span class="sxs-lookup"><span data-stu-id="1ef0f-133">______________ (first AD FS server, example ADFS1)</span></span>  <br/> |<span data-ttu-id="1ef0f-134">Windows Server 2016 数据中心</span><span class="sxs-lookup"><span data-stu-id="1ef0f-134">Windows Server 2016 Datacenter</span></span>  <br/> |<span data-ttu-id="1ef0f-135">StandardLRS</span><span class="sxs-lookup"><span data-stu-id="1ef0f-135">StandardLRS</span></span>  <br/> |<span data-ttu-id="1ef0f-136">Standard_D2</span><span class="sxs-lookup"><span data-stu-id="1ef0f-136">Standard_D2</span></span>  <br/> |
|<span data-ttu-id="1ef0f-137">5.</span><span class="sxs-lookup"><span data-stu-id="1ef0f-137">5.</span></span>  <br/> |<span data-ttu-id="1ef0f-138">______________ （第二个 AD FS 服务器，示例 ADFS2）</span><span class="sxs-lookup"><span data-stu-id="1ef0f-138">______________ (second AD FS server, example ADFS2)</span></span>  <br/> |<span data-ttu-id="1ef0f-139">Windows Server 2016 数据中心</span><span class="sxs-lookup"><span data-stu-id="1ef0f-139">Windows Server 2016 Datacenter</span></span>  <br/> |<span data-ttu-id="1ef0f-140">StandardLRS</span><span class="sxs-lookup"><span data-stu-id="1ef0f-140">StandardLRS</span></span>  <br/> |<span data-ttu-id="1ef0f-141">Standard_D2</span><span class="sxs-lookup"><span data-stu-id="1ef0f-141">Standard_D2</span></span>  <br/> |
|<span data-ttu-id="1ef0f-142">6.</span><span class="sxs-lookup"><span data-stu-id="1ef0f-142">6.</span></span>  <br/> |<span data-ttu-id="1ef0f-143">______________ （第一个 Web 应用程序代理服务器，示例 WEB1）</span><span class="sxs-lookup"><span data-stu-id="1ef0f-143">______________ (first web application proxy server, example WEB1)</span></span>  <br/> |<span data-ttu-id="1ef0f-144">Windows Server 2016 数据中心</span><span class="sxs-lookup"><span data-stu-id="1ef0f-144">Windows Server 2016 Datacenter</span></span>  <br/> |<span data-ttu-id="1ef0f-145">StandardLRS</span><span class="sxs-lookup"><span data-stu-id="1ef0f-145">StandardLRS</span></span>  <br/> |<span data-ttu-id="1ef0f-146">Standard_D2</span><span class="sxs-lookup"><span data-stu-id="1ef0f-146">Standard_D2</span></span>  <br/> |
|<span data-ttu-id="1ef0f-147">7.</span><span class="sxs-lookup"><span data-stu-id="1ef0f-147">7.</span></span>  <br/> |<span data-ttu-id="1ef0f-148">______________ （第二个 Web 应用程序代理服务器，示例 WEB2）</span><span class="sxs-lookup"><span data-stu-id="1ef0f-148">______________ (second web application proxy server, example WEB2)</span></span>  <br/> |<span data-ttu-id="1ef0f-149">Windows Server 2016 数据中心</span><span class="sxs-lookup"><span data-stu-id="1ef0f-149">Windows Server 2016 Datacenter</span></span>  <br/> |<span data-ttu-id="1ef0f-150">StandardLRS</span><span class="sxs-lookup"><span data-stu-id="1ef0f-150">StandardLRS</span></span>  <br/> |<span data-ttu-id="1ef0f-151">Standard_D2</span><span class="sxs-lookup"><span data-stu-id="1ef0f-151">Standard_D2</span></span>  <br/> |
   
 <span data-ttu-id="1ef0f-152">**表 M-Azure 中的 Office 365 的高可用性联合身份验证的虚拟机**</span><span class="sxs-lookup"><span data-stu-id="1ef0f-152">**Table M - Virtual machines for the high availability federated authentication for Office 365 in Azure**</span></span>
  
<span data-ttu-id="1ef0f-153">虚拟机大小的完整列表，请参阅[虚拟机大小](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes)。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-153">For the complete list of virtual machine sizes, see [Sizes for virtual machines](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>
  
<span data-ttu-id="1ef0f-p103">下面的 Azure PowerShell 命令块创建的两个域控制器虚拟机。为指定的值的变量，删除\<和 > 字符。请注意此 Azure PowerShell 命令块，使用下表中的值：</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p103">The following Azure PowerShell command block creates the virtual machines for the two domain controllers. Specify the values for the variables, removing the \< and > characters. Note that this Azure PowerShell command block uses values from the following tables:</span></span>
  
- <span data-ttu-id="1ef0f-157">表 M，用于虚拟机</span><span class="sxs-lookup"><span data-stu-id="1ef0f-157">Table M, for your virtual machines</span></span>
    
- <span data-ttu-id="1ef0f-158">表 R，用于资源组</span><span class="sxs-lookup"><span data-stu-id="1ef0f-158">Table R, for your resource groups</span></span>
    
- <span data-ttu-id="1ef0f-159">表 V，用于虚拟网络设置</span><span class="sxs-lookup"><span data-stu-id="1ef0f-159">Table V, for your virtual network settings</span></span>
    
- <span data-ttu-id="1ef0f-160">表 S，用于子网</span><span class="sxs-lookup"><span data-stu-id="1ef0f-160">Table S, for your subnets</span></span>
    
- <span data-ttu-id="1ef0f-161">表 I，用于静态 IP 地址</span><span class="sxs-lookup"><span data-stu-id="1ef0f-161">Table I, for your static IP addresses</span></span>
    
- <span data-ttu-id="1ef0f-162">表 A（针对可用性集）</span><span class="sxs-lookup"><span data-stu-id="1ef0f-162">Table A, for your availability sets</span></span>
    
<span data-ttu-id="1ef0f-163">记得您定义表 R、 V、 S、 I、 和中的[高可用性联合身份验证阶段 1： 配置 Azure](high-availability-federated-authentication-phase-1-configure-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-163">Recall that you defined Tables R, V, S, I, and A in [High availability federated authentication Phase 1: Configure Azure](high-availability-federated-authentication-phase-1-configure-azure.md).</span></span>
  
> [!NOTE]
> <span data-ttu-id="1ef0f-p104">下面的命令设置使用 Azure PowerShell 的最新版本。请参阅[开始使用 Azure PowerShell cmdlet](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/)。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p104">The following command sets use the latest version of Azure PowerShell. See [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/).</span></span> 
  
<span data-ttu-id="1ef0f-166">提供所有正确值后，在 Azure PowerShell 提示符处或本地计算机的 PowerShell 集成脚本环境 (ISE) 上运行生成块。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-166">When you have supplied all the correct values, run the resulting block at the Azure PowerShell prompt or in the PowerShell Integrated Script Environment (ISE) on your local computer.</span></span>
  
> [!TIP]
> <span data-ttu-id="1ef0f-167">对于包含所有这篇文章并生成基于您的自定义设置的现成 PowerShell 命令块的 Microsoft Excel 配置工作簿中的 PowerShell 命令的文本文件，请参阅[Office 365 的联合身份验证中的Azure 部署工具包](https://gallery.technet.microsoft.com/Federated-Authentication-8a9f1664)。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-167">For a text file that contains all of the PowerShell commands in this article and a Microsoft Excel configuration workbook that generates ready-to-run PowerShell command blocks based on your custom settings, see the [Federated Authentication for Office 365 in Azure Deployment Kit](https://gallery.technet.microsoft.com/Federated-Authentication-8a9f1664).</span></span> 
  
```
# Set up variables common to both virtual machines
$locName="<your Azure location>"
$vnetName="<Table V - Item 1 - Value column>"
$subnetName="<Table S - Item 1 - Value column>"
$avName="<Table A - Item 1 - Availability set name column>"
$rgNameTier="<Table R - Item 1 - Resource group name column>"
$rgNameInfra="<Table R - Item 4 - Resource group name column>"

$rgName=$rgNameInfra
$vnet=Get-AzureRMVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
$subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName

$rgName=$rgNameTier
$avSet=Get-AzureRMAvailabilitySet -Name $avName -ResourceGroupName $rgName 

# Create the first domain controller
$vmName="<Table M - Item 1 - Virtual machine name column>"
$vmSize="<Table M - Item 1 - Minimum size column>"
$staticIP="<Table I - Item 1 - Value column>"
$diskStorageType="<Table M - Item 1 - Storage type column>"
$diskSize=<size of the extra disk for Windows Server AD data in GB>

$nic=New-AzureRMNetworkInterface -Name ($vmName +"-NIC") -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PrivateIpAddress $staticIP
$vm=New-AzureRMVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avset.Id
$vm=Set-AzureRmVMOSDisk -VM $vm -Name ($vmName +"-OS") -DiskSizeInGB 128 -CreateOption FromImage -StorageAccountType $diskStorageType
$diskConfig=New-AzureRmDiskConfig -AccountType $diskStorageType -Location $locName -CreateOption Empty -DiskSizeGB $diskSize
$dataDisk1=New-AzureRmDisk -DiskName ($vmName + "-DataDisk1") -Disk $diskConfig -ResourceGroupName $rgName
$vm=Add-AzureRmVMDataDisk -VM $vm -Name ($vmName + "-DataDisk1") -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
$cred=Get-Credential -Message "Type the name and password of the local administrator account for the first domain controller." 
$vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
$vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version "latest"
$vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

# Create the second domain controller
$vmName="<Table M - Item 2 - Virtual machine name column>"
$vmSize="<Table M - Item 2 - Minimum size column>"
$staticIP="<Table I - Item 2 - Value column>"
$diskStorageType="<Table M - Item 2 - Storage type column>"
$diskSize=<size of the extra disk for Windows Server AD data in GB>

$nic=New-AzureRMNetworkInterface -Name ($vmName +"-NIC") -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PrivateIpAddress $staticIP
$vm=New-AzureRMVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avset.Id
$vm=Set-AzureRmVMOSDisk -VM $vm -Name ($vmName +"-OS") -DiskSizeInGB 128 -CreateOption FromImage -StorageAccountType $diskStorageType
$diskConfig=New-AzureRmDiskConfig -AccountType $diskStorageType -Location $locName -CreateOption Empty -DiskSizeGB $diskSize
$dataDisk1=New-AzureRmDisk -DiskName ($vmName + "-DataDisk1") -Disk $diskConfig -ResourceGroupName $rgName
$vm=Add-AzureRmVMDataDisk -VM $vm -Name ($vmName + "-DataDisk1") -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
$cred=Get-Credential -Message "Type the name and password of the local administrator account for the second domain controller." 
$vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
$vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version "latest"
$vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

# Create the DirSync server
$vmName="<Table M - Item 3 - Virtual machine name column>"
$vmSize="<Table M - Item 3 - Minimum size column>"
$staticIP="<Table I - Item 3 - Value column>"
$diskStorageType="<Table M - Item 3 - Storage type column>"

$nic=New-AzureRMNetworkInterface -Name ($vmName +"-NIC") -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PrivateIpAddress $staticIP
$vm=New-AzureRMVMConfig -VMName $vmName -VMSize $vmSize

$cred=Get-Credential -Message "Type the name and password of the local administrator account for the DirSync server." 
$vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
$vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version "latest"
$vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
$vm=Set-AzureRmVMOSDisk -VM $vm -Name ($vmName +"-OS") -DiskSizeInGB 128 -CreateOption FromImage -StorageAccountType $diskStorageType
New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm
```

> [!NOTE]
> <span data-ttu-id="1ef0f-p105">由于这些虚拟机的内部网应用程序，它们不是分配的公共 IP 地址或 DNS 域名称标签，暴露给 Internet。但是，这也意味着您不能从 Azure 门户连接到它们。查看虚拟机的属性时，**连接**选项不可用。使用远程桌面连接附件或另一个远程桌面的工具连接到虚拟机使用其专用的 IP 地址或 intranet DNS 名称。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p105">Because these virtual machines are for an intranet application, they are not assigned a public IP address or a DNS domain name label and exposed to the Internet. However, this also means that you cannot connect to them from the Azure portal. The **Connect** option is unavailable when you view the properties of the virtual machine. Use the Remote Desktop Connection accessory or another Remote Desktop tool to connect to the virtual machine using its private IP address or intranet DNS name.</span></span>
  
## <a name="configure-the-first-domain-controller"></a><span data-ttu-id="1ef0f-172">配置第一个域控制器</span><span class="sxs-lookup"><span data-stu-id="1ef0f-172">Configure the first domain controller</span></span>

<span data-ttu-id="1ef0f-p106">使用你选择的远程桌面客户端并创建到第一个域控制器虚拟机的远程桌面连接。使用其 Intranet DNS 或计算机名称以及本地管理员帐户的凭据。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p106">Use the remote desktop client of your choice and create a remote desktop connection to the first domain controller virtual machine. Use its intranet DNS or computer name and the credentials of the local administrator account.</span></span>
  
<span data-ttu-id="1ef0f-175">接下来，添加额外的数据磁盘使用此命令的第一个域控制器从 Windows PowerShell 命令提示符**上第一个域控制器虚拟机**：</span><span class="sxs-lookup"><span data-stu-id="1ef0f-175">Next, add the extra data disk to the first domain controller with this command from a Windows PowerShell command prompt **on the first domain controller virtual machine**:</span></span>
  
```
Get-Disk | Where PartitionStyle -eq "RAW" | Initialize-Disk -PartitionStyle MBR -PassThru | New-Partition -AssignDriveLetter -UseMaximumSize | Format-Volume -FileSystem NTFS -NewFileSystemLabel "WSAD Data"
```

<span data-ttu-id="1ef0f-176">接下来，使用**ping**命令名称和您组织的网络上的资源的 IP 地址执行 ping 测试的第一个域控制器连接到组织网络上的位置。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-176">Next, test the first domain controller's connectivity to locations on your organization network by using the **ping** command to ping names and IP addresses of resources on your organization network.</span></span>
  
<span data-ttu-id="1ef0f-p107">此过程确保 DNS 名称解析正常进行（已为该虚拟机正确配置本地 DNS 服务器），并可以向/从跨本地虚拟网络发送数据。如果这个基本测试失败，请与你的 IT 部门联系，来解决 DNS 名称解析和数据包传递问题。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p107">This procedure ensures that DNS name resolution is working correctly (that the virtual machine is correctly configured with on-premises DNS servers) and that packets can be sent to and from the cross-premises virtual network. If this basic test fails, contact your IT department to troubleshoot the DNS name resolution and packet delivery issues.</span></span>
  
<span data-ttu-id="1ef0f-179">接下来，从第一个域控制器的 Windows PowerShell 命令提示符处运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="1ef0f-179">Next, from the Windows PowerShell command prompt on the first domain controller, run the following commands:</span></span>
  
```
$domname="<DNS domain name of the domain for which this computer will be a domain controller, such as corp.contoso.com>"
$cred = Get-Credential -Message "Enter credentials of an account with permission to join a new domain controller to the domain"
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Install-ADDSDomainController -InstallDns -DomainName $domname  -DatabasePath "F:\\NTDS" -SysvolPath "F:\\SYSVOL" -LogPath "F:\\Logs" -Credential $cred
```

<span data-ttu-id="1ef0f-p108">系统将提示你提供域管理员帐户的凭据。计算机将重新启动。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p108">You will be prompted to supply the credentials of a domain administrator account. The computer will restart.</span></span>
  
## <a name="configure-the-second-domain-controller"></a><span data-ttu-id="1ef0f-182">配置第二个域控制器</span><span class="sxs-lookup"><span data-stu-id="1ef0f-182">Configure the second domain controller</span></span>

<span data-ttu-id="1ef0f-p109">使用你选择的远程桌面客户端并创建到第二个域控制器虚拟机的远程桌面连接。使用其 Intranet DNS 或计算机名称以及本地管理员帐户的凭据。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p109">Use the remote desktop client of your choice and create a remote desktop connection to the second domain controller virtual machine. Use its intranet DNS or computer name and the credentials of the local administrator account.</span></span>
  
<span data-ttu-id="1ef0f-185">接下来，您需要从 Windows PowerShell 命令提示符**上第二个域控制器虚拟机**向具有此命令的第二个域控制器中添加额外的数据磁盘：</span><span class="sxs-lookup"><span data-stu-id="1ef0f-185">Next, you need to add the extra data disk to the second domain controller with this command from a Windows PowerShell command prompt **on the second domain controller virtual machine**:</span></span>
  
```
Get-Disk | Where PartitionStyle -eq "RAW" | Initialize-Disk -PartitionStyle MBR -PassThru | New-Partition -AssignDriveLetter -UseMaximumSize | Format-Volume -FileSystem NTFS -NewFileSystemLabel "WSAD Data"
```

<span data-ttu-id="1ef0f-186">接下来，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="1ef0f-186">Next, run the following commands:</span></span>
  
```
$domname="<DNS domain name of the domain for which this computer will be a domain controller, such as corp.contoso.com>"
$cred = Get-Credential -Message "Enter credentials of an account with permission to join a new domain controller to the domain"
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Install-ADDSDomainController -InstallDns -DomainName $domname  -DatabasePath "F:\\NTDS" -SysvolPath "F:\\SYSVOL" -LogPath "F:\\Logs" -Credential $cred

```

<span data-ttu-id="1ef0f-p110">系统将提示你提供域管理员帐户的凭据。计算机将重新启动。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p110">You will be prompted to supply the credentials of a domain administrator account. The computer will restart.</span></span>
  
<span data-ttu-id="1ef0f-p111">接下来，您需要更新的 DNS 服务器的虚拟网络，以便该 Azure 将虚拟机分配了两个新的域控制器用作其 DNS 服务器的 IP 地址。填充的变量中，然后从 Windows PowerShell 命令提示符运行这些命令，您的本地计算机上：</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p111">Next, you need to update the DNS servers for your virtual network so that Azure assigns virtual machines the IP addresses of the two new domain controllers to use as their DNS servers. Fill in the variables and then run these commands from a Windows PowerShell command prompt on your local computer:</span></span>
  
```
$rgName="<Table R - Item 4 - Resource group name column>"
$adrgName="<Table R - Item 1 - Resource group name column>"
$locName="<your Azure location>"
$vnetName="<Table V - Item 1 - Value column>"
$onpremDNSIP1="<Table D - Item 1 - DNS server IP address column>"
$onpremDNSIP2="<Table D - Item 2 - DNS server IP address column>"
$staticIP1="<Table I - Item 1 - Value column>"
$staticIP2="<Table I - Item 2 - Value column>"
$firstDCName="<Table M - Item 1 - Virtual machine name column>"
$secondDCName="<Table M - Item 2 - Virtual machine name column>"

$vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
$vnet.DhcpOptions.DnsServers.Add($staticIP1)
$vnet.DhcpOptions.DnsServers.Add($staticIP2) 
$vnet.DhcpOptions.DnsServers.Remove($onpremDNSIP1)
$vnet.DhcpOptions.DnsServers.Remove($onpremDNSIP2) 
Set-AzureRMVirtualNetwork -VirtualNetwork $vnet
Restart-AzureRMVM -ResourceGroupName $adrgName -Name $firstDCName
Restart-AzureRMVM -ResourceGroupName $adrgName -Name $secondDCName
```

<span data-ttu-id="1ef0f-p112">请注意，我们重新启动两个域控制器，这样不会为它们配置本地 DNS 服务器作为 DNS 服务器。因为这两个控制器本身就是 DNS 服务器，因此在升级为域控制器后会自动为它们配置本地 DNS 服务器作为 DNS 转发器。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p112">Note that we restart the two domain controllers so that they are not configured with the on-premises DNS servers as DNS servers. Because they are both DNS servers themselves, they were automatically configured with the on-premises DNS servers as DNS forwarders when they were promoted to domain controllers.</span></span>
  
<span data-ttu-id="1ef0f-p113">接下来，我们需要创建一个 Active Directory 复制站点以确保 Azure 虚拟网络中的服务器使用本地域控制器。使用域管理员帐户连接到任一域控制器，从管理员级 Windows PowerShell 提示符处运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p113">Next, we need to create an Active Directory replication site to ensure that servers in the Azure virtual network use the local domain controllers. Connect to either domain controller with a domain administrator account and run the following commands from an administrator-level Windows PowerShell prompt:</span></span>
  
```
$vnet="<Table V - Item 1 - Value column>"
$vnetSpace="<Table V - Item 4 - Value column>"
New-ADReplicationSite -Name $vnet 
New-ADReplicationSubnet -Name $vnetSpace -Site $vnet
```

## <a name="configure-the-dirsync-server"></a><span data-ttu-id="1ef0f-195">配置目录同步服务器</span><span class="sxs-lookup"><span data-stu-id="1ef0f-195">Configure the DirSync server</span></span>

<span data-ttu-id="1ef0f-p114">使用您所选的远程桌面客户端，并创建与目录同步服务器虚拟机的远程桌面连接。使用内联网 DNS 或计算机名称和本地管理员帐户的凭据。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-p114">Use the remote desktop client of your choice and create a remote desktop connection to the DirSync server virtual machine. Use its intranet DNS or computer name and the credentials of the local administrator account.</span></span>
  
<span data-ttu-id="1ef0f-198">接下来，通过 Windows PowerShell 提示符下的这些命令将其加入相应的 Windows Server AD 域。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-198">Next, join it to the appropriate Windows Server AD domain with these commands at the Windows PowerShell prompt.</span></span>
  
```
$domName="<Windows Server AD domain name to join, such as corp.contoso.com>"
$cred=Get-Credential -Message "Type the name and password of a domain acccount."
Add-Computer -DomainName $domName -Credential $cred
Restart-Computer
```

<span data-ttu-id="1ef0f-199">以下是因成功完成这一阶段后生成的配置，包含占位符计算机名称。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-199">Here is the configuration resulting from the successful completion of this phase, with placeholder computer names.</span></span>
  
<span data-ttu-id="1ef0f-200">**第 2 阶段： 域控制器，您的高可用性 Azure 中的联合身份验证基础结构的目录同步服务器**</span><span class="sxs-lookup"><span data-stu-id="1ef0f-200">**Phase 2: The domain controllers and DirSync server for your high availability federated authentication infrastructure in Azure**</span></span>

![阶段 2：在包含域控制器的 Azure 中配置高可用性 Office 365 联合身份验证基础结构](images/b0c1013b-3fb4-499e-93c1-bf310d8f4c32.png)
  
## <a name="next-step"></a><span data-ttu-id="1ef0f-202">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1ef0f-202">Next step</span></span>

<span data-ttu-id="1ef0f-203">使用[高可用性联合身份验证阶段 3： 配置 AD FS 服务器](high-availability-federated-authentication-phase-3-configure-ad-fs-servers.md)继续配置此工作负载。</span><span class="sxs-lookup"><span data-stu-id="1ef0f-203">Use [High availability federated authentication Phase 3: Configure AD FS servers](high-availability-federated-authentication-phase-3-configure-ad-fs-servers.md) to continue configuring this workload.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="1ef0f-204">See Also</span><span class="sxs-lookup"><span data-stu-id="1ef0f-204">See Also</span></span>

[<span data-ttu-id="1ef0f-205">在 Azure 中部署 Office 365 的高可用性联合身份验证</span><span class="sxs-lookup"><span data-stu-id="1ef0f-205">Deploy high availability federated authentication for Office 365 in Azure</span></span>](deploy-high-availability-federated-authentication-for-office-365-in-azure.md)
  
[<span data-ttu-id="1ef0f-206">用于 Office 365 开发/测试环境的联合身份</span><span class="sxs-lookup"><span data-stu-id="1ef0f-206">Federated identity for your Office 365 dev/test environment</span></span>](federated-identity-for-your-office-365-dev-test-environment.md)
  
[<span data-ttu-id="1ef0f-207">云应用和混合解决方案</span><span class="sxs-lookup"><span data-stu-id="1ef0f-207">Cloud adoption and hybrid solutions</span></span>](cloud-adoption-and-hybrid-solutions.md)

[<span data-ttu-id="1ef0f-208">Office 365 的联合标识</span><span class="sxs-lookup"><span data-stu-id="1ef0f-208">Federated identity for Office 365</span></span>](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

