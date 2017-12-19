---
title: "高可用性联合身份验证阶段 1 配置 Azure"
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
ms.assetid: 91266aac-4d00-4b5f-b424-86a1a837792c
description: "摘要： 配置 Microsoft Azure 基础结构主机的高可用性到 Office 365 的联合身份验证。"
ms.openlocfilehash: fed6b24af2ba54bef95be22641fd140f7c1be717
ms.sourcegitcommit: d31cf57295e8f3d798ab971d405baf3bd3eb7a45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2017
---
# <a name="high-availability-federated-authentication-phase-1-configure-azure"></a><span data-ttu-id="e8886-103">高可用性联合身份验证阶段 1:配置 Azure</span><span class="sxs-lookup"><span data-stu-id="e8886-103">High availability federated authentication Phase 1: Configure Azure</span></span>

 <span data-ttu-id="e8886-104">**摘要：**配置 Microsoft Azure 基础结构主机为 Office 365 的高可用性，联合身份验证。</span><span class="sxs-lookup"><span data-stu-id="e8886-104">**Summary:** Configure the Microsoft Azure infrastructure to host high availability federated authentication for Office 365.</span></span>
  
<span data-ttu-id="e8886-p101">在此阶段中，您可以创建资源组，存储帐户，Azure 将承载在阶段 2、 3 和 4 中的虚拟机中的虚拟网络 (VNet) 和可用性设置。您必须先完成这一阶段之前移动到[高可用性联合身份验证阶段 2： 配置域控制器](high-availability-federated-authentication-phase-2-configure-domain-controllers.md)。请参阅[Office 365 Azure 中部署高可用性联合身份验证](deploy-high-availability-federated-authentication-for-office-365-in-azure.md)所有阶段。</span><span class="sxs-lookup"><span data-stu-id="e8886-p101">In this phase, you create the resource groups, storage accounts, virtual network (VNet), and availability sets in Azure that will host the virtual machines in phases 2, 3, and 4. You must complete this phase before moving on to [High availability federated authentication Phase 2: Configure domain controllers](high-availability-federated-authentication-phase-2-configure-domain-controllers.md). See [Deploy high availability federated authentication for Office 365 in Azure](deploy-high-availability-federated-authentication-for-office-365-in-azure.md) for all of the phases.</span></span>
  
<span data-ttu-id="e8886-108">这些基本组件，必须设置 azure:</span><span class="sxs-lookup"><span data-stu-id="e8886-108">Azure must be provisioned with these basic components:</span></span>
  
- <span data-ttu-id="e8886-109">资源组</span><span class="sxs-lookup"><span data-stu-id="e8886-109">Resource groups</span></span>
    
- <span data-ttu-id="e8886-110">使用子网托管 Azure 虚拟机的跨界 Azure 虚拟网络 (VNet)</span><span class="sxs-lookup"><span data-stu-id="e8886-110">A cross-premises Azure virtual network (VNet) with subnets for hosting the Azure virtual machines</span></span>
    
- <span data-ttu-id="e8886-111">执行子网隔离的网络安全组</span><span class="sxs-lookup"><span data-stu-id="e8886-111">Network security groups for performing subnet isolation</span></span>
    
- <span data-ttu-id="e8886-112">可用性集</span><span class="sxs-lookup"><span data-stu-id="e8886-112">Availability sets</span></span>
    
## <a name="configure-azure-components"></a><span data-ttu-id="e8886-113">配置 Azure 组件</span><span class="sxs-lookup"><span data-stu-id="e8886-113">Configure Azure components</span></span>

<span data-ttu-id="e8886-p102">配置 Azure 的组件之前，请填写下表。为了帮助您配置 Azure 的过程中，打印此部分并记下所需的信息或复制到文档的此部分并填写。VNet 的设置，请填写表格 V。</span><span class="sxs-lookup"><span data-stu-id="e8886-p102">Before you begin configuring Azure components, fill in the following tables. To assist you in the procedures for configuring Azure, print this section and write down the needed information or copy this section to a document and fill it in. For the settings of the VNet, fill in Table V.</span></span>
  
|<span data-ttu-id="e8886-117">**项**</span><span class="sxs-lookup"><span data-stu-id="e8886-117">**Item**</span></span>|<span data-ttu-id="e8886-118">**配置设置**</span><span class="sxs-lookup"><span data-stu-id="e8886-118">**Configuration setting**</span></span>|<span data-ttu-id="e8886-119">**说明**</span><span class="sxs-lookup"><span data-stu-id="e8886-119">**Description**</span></span>|<span data-ttu-id="e8886-120">**值**</span><span class="sxs-lookup"><span data-stu-id="e8886-120">**Value**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="e8886-121">1.</span><span class="sxs-lookup"><span data-stu-id="e8886-121">1.</span></span>  <br/> |<span data-ttu-id="e8886-122">VNet 名称</span><span class="sxs-lookup"><span data-stu-id="e8886-122">VNet name</span></span>  <br/> |<span data-ttu-id="e8886-123">要分配给 VNet 的名称（示例 FedAuthNet）。</span><span class="sxs-lookup"><span data-stu-id="e8886-123">A name to assign to the VNet (example FedAuthNet).</span></span>  <br/> |<span data-ttu-id="e8886-124">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-124"></span></span>  <br/> |
|<span data-ttu-id="e8886-125">2.</span><span class="sxs-lookup"><span data-stu-id="e8886-125">2.</span></span>  <br/> |<span data-ttu-id="e8886-126">VNet 的位置</span><span class="sxs-lookup"><span data-stu-id="e8886-126">VNet location</span></span>  <br/> |<span data-ttu-id="e8886-127">将包含虚拟网络的区域 Azure 数据中心。</span><span class="sxs-lookup"><span data-stu-id="e8886-127">The regional Azure datacenter that will contain the virtual network.</span></span>  <br/> |<span data-ttu-id="e8886-128">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-128"></span></span>  <br/> |
|<span data-ttu-id="e8886-129">3.</span><span class="sxs-lookup"><span data-stu-id="e8886-129">3.</span></span>  <br/> |<span data-ttu-id="e8886-130">VPN 设备 IP 地址</span><span class="sxs-lookup"><span data-stu-id="e8886-130">VPN device IP address</span></span>  <br/> |<span data-ttu-id="e8886-131">Internet 上 VPN 设备接口的公共 IPv4 地址。 </span><span class="sxs-lookup"><span data-stu-id="e8886-131">The public IPv4 address of your VPN device's interface on the Internet.</span></span>  <br/> |<span data-ttu-id="e8886-132">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-132"></span></span>  <br/> |
|<span data-ttu-id="e8886-133">4.</span><span class="sxs-lookup"><span data-stu-id="e8886-133">4.</span></span>  <br/> |<span data-ttu-id="e8886-134">VNet 地址空间</span><span class="sxs-lookup"><span data-stu-id="e8886-134">VNet address space</span></span>  <br/> |<span data-ttu-id="e8886-p103">虚拟网络的地址空间。与 IT 部门协作，以确定该地址空间。</span><span class="sxs-lookup"><span data-stu-id="e8886-p103">The address space for the virtual network. Work with your IT department to determine this address space.</span></span>  <br/> |<span data-ttu-id="e8886-137">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-137"></span></span>  <br/> |
|<span data-ttu-id="e8886-138">5.</span><span class="sxs-lookup"><span data-stu-id="e8886-138">5.</span></span>  <br/> |<span data-ttu-id="e8886-139">IPsec 共享的密钥</span><span class="sxs-lookup"><span data-stu-id="e8886-139">IPsec shared key</span></span>  <br/> |<span data-ttu-id="e8886-p104">32 个字符随机的字母数字字符串，用于进行身份验证的站点到站点 VPN 连接的两端。使用您的 IT 或安全部门来确定此项的值。另外，请参阅[创建 IPsec 预共享密钥的随机字符串](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e8886-p104">A 32-character random, alphanumeric string that will be used to authenticate both sides of the site-to-site VPN connection. Work with your IT or security department to determine this key value. Alternately, see [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx).  </span></span><br/> |<span data-ttu-id="e8886-143">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-143"></span></span>  <br/> |
   
 <span data-ttu-id="e8886-144">**表 V：跨部署虚拟网络配置**</span><span class="sxs-lookup"><span data-stu-id="e8886-144">**Table V: Cross-premises virtual network configuration**</span></span>
  
<span data-ttu-id="e8886-p105">接下来，填写针对此解决方案的子网的表 S。所有地址空间应为无类别域际路由选择 (CIDR) 格式，也称为网络前缀格式。例如，10.24.64.0/20。</span><span class="sxs-lookup"><span data-stu-id="e8886-p105">Next, fill in Table S for the subnets of this solution. All address spaces should be in Classless Interdomain Routing (CIDR) format, also known as network prefix format. An example is 10.24.64.0/20.</span></span>
  
<span data-ttu-id="e8886-p106">对于前三个子网，请指定名称和基于虚拟网络地址空间的单个 IP 地址空间。对于网关子网，请通过以下过程为 Azure 网关子网确定 27 位地址空间（带有 /27 前缀长度）：</span><span class="sxs-lookup"><span data-stu-id="e8886-p106">For the first three subnets, specify a name and a single IP address space based on the virtual network address space. For the gateway subnet, determine the 27-bit address space (with a /27 prefix length) for the Azure gateway subnet with the following:</span></span>
  
1. <span data-ttu-id="e8886-150">将 VNet 地址空间的可变位设置为 1，直到用于网关子网的位，然后将剩余位设置为 0。</span><span class="sxs-lookup"><span data-stu-id="e8886-150">Set the variable bits in the address space of the VNet to 1, up to the bits being used by the gateway subnet, then set the remaining bits to 0.</span></span>
    
2. <span data-ttu-id="e8886-151">将生成位转换为十进制并表示为一个地址空间，其中将前缀长度设置为网关子网的大小。</span><span class="sxs-lookup"><span data-stu-id="e8886-151">Convert the resulting bits to decimal and express it as an address space with the prefix length set to the size of the gateway subnet.</span></span>
    
<span data-ttu-id="e8886-152">请参阅[Azure 的网关的子网的地址空间计算器](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed)PowerShell 命令块和 C# 或 Python 控制台应用程序为您执行此计算。</span><span class="sxs-lookup"><span data-stu-id="e8886-152">See [Address space calculator for Azure gateway subnets](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed) for a PowerShell command block and C# or Python console application that performs this calculation for you.</span></span>
  
<span data-ttu-id="e8886-153">与 IT 部门协作以确定这些虚拟网络地址空间中的地址空间。</span><span class="sxs-lookup"><span data-stu-id="e8886-153">Work with your IT department to determine these address spaces from the virtual network address space.</span></span>
  
|<span data-ttu-id="e8886-154">**项目**</span><span class="sxs-lookup"><span data-stu-id="e8886-154">**Item**</span></span>|<span data-ttu-id="e8886-155">**子网名称**</span><span class="sxs-lookup"><span data-stu-id="e8886-155">**Subnet name**</span></span>|<span data-ttu-id="e8886-156">**子网地址空间**</span><span class="sxs-lookup"><span data-stu-id="e8886-156">**Subnet address space**</span></span>|<span data-ttu-id="e8886-157">**目的**</span><span class="sxs-lookup"><span data-stu-id="e8886-157">**Purpose**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="e8886-158">1.</span><span class="sxs-lookup"><span data-stu-id="e8886-158">1.</span></span>  <br/> |<span data-ttu-id="e8886-159">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-159"></span></span>  <br/> |<span data-ttu-id="e8886-160">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-160"></span></span>  <br/> |<span data-ttu-id="e8886-161">Windows Server Active Directory (AD) 域控制器和目录同步服务器虚拟机 (VM) 使用的子网。</span><span class="sxs-lookup"><span data-stu-id="e8886-161">The subnet used by the Windows Server Active Directory (AD) domain controller and DirSync server virtual machines (VMs).</span></span>  <br/> |
|<span data-ttu-id="e8886-162">2.</span><span class="sxs-lookup"><span data-stu-id="e8886-162">2.</span></span>  <br/> |<span data-ttu-id="e8886-163">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-163"></span></span>  <br/> |<span data-ttu-id="e8886-164">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-164"></span></span>  <br/> |<span data-ttu-id="e8886-165">AD FS VM 使用的子网。</span><span class="sxs-lookup"><span data-stu-id="e8886-165">The subnet used by the AD FS VMs.</span></span>  <br/> |
|<span data-ttu-id="e8886-166">3.</span><span class="sxs-lookup"><span data-stu-id="e8886-166">3.</span></span>  <br/> |<span data-ttu-id="e8886-167">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-167"></span></span>  <br/> |<span data-ttu-id="e8886-168">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-168"></span></span>  <br/> |<span data-ttu-id="e8886-169">Web 应用程序代理 VM 使用的子网。</span><span class="sxs-lookup"><span data-stu-id="e8886-169">The subnet used by the web application proxy VMs.</span></span>  <br/> |
|<span data-ttu-id="e8886-170">4.</span><span class="sxs-lookup"><span data-stu-id="e8886-170">4.</span></span>  <br/> |<span data-ttu-id="e8886-171">GatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="e8886-171">GatewaySubnet</span></span>  <br/> |<span data-ttu-id="e8886-172">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-172"></span></span>  <br/> |<span data-ttu-id="e8886-173">Azure 网关 VM 使用的子网。</span><span class="sxs-lookup"><span data-stu-id="e8886-173">The subnet used by the Azure gateway VMs.</span></span>  <br/> |
   
 <span data-ttu-id="e8886-174">**表 S：虚拟网络中的子网**</span><span class="sxs-lookup"><span data-stu-id="e8886-174">**Table S: Subnets in the virtual network**</span></span>
  
<span data-ttu-id="e8886-175">下一步，针对分配给虚拟机和负载平衡器实例的静态 IP 地址填写表 I。</span><span class="sxs-lookup"><span data-stu-id="e8886-175">Next, fill in Table I for the static IP addresses assigned to virtual machines and load balancer instances.</span></span>
  
|<span data-ttu-id="e8886-176">**项**</span><span class="sxs-lookup"><span data-stu-id="e8886-176">**Item**</span></span>|<span data-ttu-id="e8886-177">**用途**</span><span class="sxs-lookup"><span data-stu-id="e8886-177">**Purpose**</span></span>|<span data-ttu-id="e8886-178">**在子网的 IP 地址**</span><span class="sxs-lookup"><span data-stu-id="e8886-178">**IP address on the subnet**</span></span>|<span data-ttu-id="e8886-179">**值**</span><span class="sxs-lookup"><span data-stu-id="e8886-179">**Value**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="e8886-180">1.</span><span class="sxs-lookup"><span data-stu-id="e8886-180">1.</span></span>  <br/> |<span data-ttu-id="e8886-181">第一个域控制器的静态 IP 地址</span><span class="sxs-lookup"><span data-stu-id="e8886-181">Static IP address of the first domain controller</span></span>  <br/> |<span data-ttu-id="e8886-182">在表 S 的项目 1 中定义的子网地址空间的第四个可能的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e8886-182">The fourth possible IP address for the address space of the subnet defined in Item 1 of Table S.</span></span>  <br/> |<span data-ttu-id="e8886-183">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-183"></span></span>  <br/> |
|<span data-ttu-id="e8886-184">2.</span><span class="sxs-lookup"><span data-stu-id="e8886-184">2.</span></span>  <br/> |<span data-ttu-id="e8886-185">第二个域控制器的静态 IP 地址</span><span class="sxs-lookup"><span data-stu-id="e8886-185">Static IP address of the second domain controller</span></span>  <br/> |<span data-ttu-id="e8886-186">在表 S 的项目 1 中定义的子网地址空间的第五个可能的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e8886-186">The fifth possible IP address for the address space of the subnet defined in Item 1 of Table S.</span></span>  <br/> |<span data-ttu-id="e8886-187">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-187"></span></span>  <br/> |
|<span data-ttu-id="e8886-188">3.</span><span class="sxs-lookup"><span data-stu-id="e8886-188">3.</span></span>  <br/> |<span data-ttu-id="e8886-189">目录同步服务器的静态 IP 地址</span><span class="sxs-lookup"><span data-stu-id="e8886-189">Static IP address of the DirSync server</span></span>  <br/> |<span data-ttu-id="e8886-190">在表 S 的第 1 项中定义的子网地址空间的第六个可能的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e8886-190">The sixth possible IP address for the address space of the subnet defined in Item 1 of Table S.</span></span>  <br/> |<span data-ttu-id="e8886-191">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-191"></span></span>  <br/> |
|<span data-ttu-id="e8886-192">4.</span><span class="sxs-lookup"><span data-stu-id="e8886-192">4.</span></span>  <br/> |<span data-ttu-id="e8886-193">AD FS 服务器内部负载均衡器的静态 IP 地址</span><span class="sxs-lookup"><span data-stu-id="e8886-193">Static IP address of the internal load balancer for the AD FS servers</span></span>  <br/> |<span data-ttu-id="e8886-194">在表 S 的项目 2 中定义的子网地址空间的第四个可能的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e8886-194">The fourth possible IP address for the address space of the subnet defined in Item 2 of Table S.</span></span>  <br/> |<span data-ttu-id="e8886-195">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-195"></span></span>  <br/> |
|<span data-ttu-id="e8886-196">5.</span><span class="sxs-lookup"><span data-stu-id="e8886-196">5.</span></span>  <br/> |<span data-ttu-id="e8886-197">第一个 AD FS 服务器的静态 IP 地址</span><span class="sxs-lookup"><span data-stu-id="e8886-197">Static IP address of the first AD FS server</span></span>  <br/> |<span data-ttu-id="e8886-198">在表 S 的项目 2 中定义的子网地址空间的第五个可能的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e8886-198">The fifth possible IP address for the address space of the subnet defined in Item 2 of Table S.</span></span>  <br/> |<span data-ttu-id="e8886-199">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-199"></span></span>  <br/> |
|<span data-ttu-id="e8886-200">6.</span><span class="sxs-lookup"><span data-stu-id="e8886-200">6.</span></span>  <br/> |<span data-ttu-id="e8886-201">第二个 AD FS 服务器的静态 IP 地址</span><span class="sxs-lookup"><span data-stu-id="e8886-201">Static IP address of the second AD FS server</span></span>  <br/> |<span data-ttu-id="e8886-202">在表 S 的项目 2 中定义的子网地址空间的第六个可能的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e8886-202">The sixth possible IP address for the address space of the subnet defined in Item 2 of Table S.</span></span>  <br/> |<span data-ttu-id="e8886-203">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-203"></span></span>  <br/> |
|<span data-ttu-id="e8886-204">7.</span><span class="sxs-lookup"><span data-stu-id="e8886-204">7.</span></span>  <br/> |<span data-ttu-id="e8886-205">第一个 Web 应用程序代理服务器的静态 IP 地址</span><span class="sxs-lookup"><span data-stu-id="e8886-205">Static IP address of the first web application proxy server</span></span>  <br/> |<span data-ttu-id="e8886-206">在表 S 的项目 3 中定义的子网地址空间的第四个可能的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e8886-206">The fourth possible IP address for the address space of the subnet defined in Item 3 of Table S.</span></span>  <br/> |<span data-ttu-id="e8886-207">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-207"></span></span>  <br/> |
|<span data-ttu-id="e8886-208">8。</span><span class="sxs-lookup"><span data-stu-id="e8886-208">8.</span></span>  <br/> |<span data-ttu-id="e8886-209">第二个 Web 应用程序代理服务器的静态 IP 地址</span><span class="sxs-lookup"><span data-stu-id="e8886-209">Static IP address of the second web application proxy server</span></span>  <br/> |<span data-ttu-id="e8886-210">在表 S 的项目 3 中定义的子网地址空间的第五个可能的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e8886-210">The fifth possible IP address for the address space of the subnet defined in Item 3 of Table S.</span></span>  <br/> |<span data-ttu-id="e8886-211">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-211"></span></span>  <br/> |
   
 <span data-ttu-id="e8886-212">**在虚拟网络中的表格 i： 静态 IP 地址**</span><span class="sxs-lookup"><span data-stu-id="e8886-212">**Table I: Static IP addresses in the virtual network**</span></span>
  
<span data-ttu-id="e8886-213">对于本地网络中你最初在虚拟网络中设置域控制器时想要使用的两个域名系统 (DNS) 服务器，请填写表 D。与 IT 部门协作，以确定该列表。</span><span class="sxs-lookup"><span data-stu-id="e8886-213">For two Domain Name System (DNS) servers in your on-premises network that you want to use when initially setting up the domain controllers in your virtual network, fill in Table D. Work with your IT department to determine this list.</span></span>
  
|<span data-ttu-id="e8886-214">**项目**</span><span class="sxs-lookup"><span data-stu-id="e8886-214">**Item**</span></span>|<span data-ttu-id="e8886-215">**DNS 服务器的友好名称**</span><span class="sxs-lookup"><span data-stu-id="e8886-215">**DNS server friendly name**</span></span>|<span data-ttu-id="e8886-216">**DNS 服务器的 IP 地址**</span><span class="sxs-lookup"><span data-stu-id="e8886-216">**DNS server IP address**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="e8886-217">1.</span><span class="sxs-lookup"><span data-stu-id="e8886-217">1.</span></span>  <br/> |<span data-ttu-id="e8886-218">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-218"></span></span>  <br/> |<span data-ttu-id="e8886-219">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-219"></span></span>  <br/> |
|<span data-ttu-id="e8886-220">2.</span><span class="sxs-lookup"><span data-stu-id="e8886-220">2.</span></span>  <br/> |<span data-ttu-id="e8886-221">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-221"></span></span>  <br/> |<span data-ttu-id="e8886-222">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-222"></span></span>  <br/> |
   
 <span data-ttu-id="e8886-223">**表 D：本地 DNS 服务器**</span><span class="sxs-lookup"><span data-stu-id="e8886-223">**Table D: On-premises DNS servers**</span></span>
  
<span data-ttu-id="e8886-p107">要通过站点间 VPN 连接将数据包从跨界网络传输到组织网络，你必须使用本地网络配置虚拟网络。此本地网络包含组织的本地网络上所有可访问位置的地址空间列表（使用 CIDR 表示法）。用于定义本地网络的地址空间列表必须是唯一的，并且不得与用于其他虚拟网络或其他本地网络的地址空间重叠。</span><span class="sxs-lookup"><span data-stu-id="e8886-p107">To route packets from the cross-premises network to your organization network across the site-to-site VPN connection, you must configure the virtual network with a local network that contains a list of the address spaces (in CIDR notation) for all of the reachable locations on your organization's on-premises network. The list of address spaces that define your local network must be unique and must not overlap with the address space used for other virtual networks or other local networks.</span></span>
  
<span data-ttu-id="e8886-p108">对于本地网络地址空间集，请填写表 L。请注意已列出三个空白条目，但通常需要更多。与 IT 部门协作，以确定该地址空间列表。</span><span class="sxs-lookup"><span data-stu-id="e8886-p108">For the set of local network address spaces, fill in Table L. Note that three blank entries are listed but you will typically need more. Work with your IT department to determine this list of address spaces.</span></span>
  
|<span data-ttu-id="e8886-228">**项目**</span><span class="sxs-lookup"><span data-stu-id="e8886-228">**Item**</span></span>|<span data-ttu-id="e8886-229">**本地网络地址空间**</span><span class="sxs-lookup"><span data-stu-id="e8886-229">**Local network address space**</span></span>|
|:-----|:-----|
|<span data-ttu-id="e8886-230">1.</span><span class="sxs-lookup"><span data-stu-id="e8886-230">1.</span></span>  <br/> |<span data-ttu-id="e8886-231">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-231"></span></span>  <br/> |
|<span data-ttu-id="e8886-232">2.</span><span class="sxs-lookup"><span data-stu-id="e8886-232">2.</span></span>  <br/> |<span data-ttu-id="e8886-233">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-233"></span></span>  <br/> |
|<span data-ttu-id="e8886-234">3.</span><span class="sxs-lookup"><span data-stu-id="e8886-234">3.</span></span>  <br/> |<span data-ttu-id="e8886-235">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-235"></span></span>  <br/> |
   
 <span data-ttu-id="e8886-236">**表 L：本地网络的地址前缀**</span><span class="sxs-lookup"><span data-stu-id="e8886-236">**Table L: Address prefixes for the local network**</span></span>
  
<span data-ttu-id="e8886-237">现在让我们开始构建 Azure 基础结构来托管你的 Office 365 联合身份验证。</span><span class="sxs-lookup"><span data-stu-id="e8886-237">Now let's begin building the Azure infrastructure to host your federated authentication for Office 365.</span></span>
  
> [!NOTE]
> <span data-ttu-id="e8886-p109">下面的命令设置使用 Azure PowerShell 的最新版本。请参阅[开始使用 Azure PowerShell cmdlet](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/)。</span><span class="sxs-lookup"><span data-stu-id="e8886-p109">The following command sets use the latest version of Azure PowerShell. See [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/).</span></span> 
  
<span data-ttu-id="e8886-240">首先，启动 Azure PowerShell 提示符并登录到你的帐户。</span><span class="sxs-lookup"><span data-stu-id="e8886-240">First, start an Azure PowerShell prompt and login to your account.</span></span>
  
```
Login-AzureRMAccount
```

> [!TIP]
> <span data-ttu-id="e8886-241">对于包含所有这篇文章并生成基于您的自定义设置的现成 PowerShell 命令块的 Microsoft Excel 配置工作簿中的 PowerShell 命令的文本文件，请参阅[Office 365 的联合身份验证中的Azure 部署工具包](https://gallery.technet.microsoft.com/Federated-Authentication-8a9f1664)。</span><span class="sxs-lookup"><span data-stu-id="e8886-241">For a text file that contains all of the PowerShell commands in this article and a Microsoft Excel configuration workbook that generates ready-to-run PowerShell command blocks based on your custom settings, see the [Federated Authentication for Office 365 in Azure Deployment Kit](https://gallery.technet.microsoft.com/Federated-Authentication-8a9f1664).</span></span> 
  
<span data-ttu-id="e8886-242">使用以下命令获得订阅名称。</span><span class="sxs-lookup"><span data-stu-id="e8886-242">Get your subscription name using the following command.</span></span>
  
```
Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="e8886-243">对于 Azure PowerShell 的旧版本，而是使用此命令。</span><span class="sxs-lookup"><span data-stu-id="e8886-243">For older versions of Azure PowerShell, use this command instead.</span></span>
  
```
Get-AzureRMSubscription | Sort Name | Select SubscriptionName
```

<span data-ttu-id="e8886-p110">设置 Azure 订购。引号，包括的所有内容替换\<和 > 字符，用正确的名称。</span><span class="sxs-lookup"><span data-stu-id="e8886-p110">Set your Azure subscription. Replace everything within the quotes, including the \< and > characters, with the correct name.</span></span>
  
```
$subscr="<subscription name>"
Get-AzureRmSubscription -SubscriptionName $subscr | Select-AzureRmSubscription
```

<span data-ttu-id="e8886-p111">接下来，创建新的资源组。要确定唯一的一组资源组名称，请使用此命令列出现有的资源组。</span><span class="sxs-lookup"><span data-stu-id="e8886-p111">Next, create the new resource groups. To determine a unique set of resource group names, use this command to list your existing resource groups.</span></span>
  
```
Get-AzureRMResourceGroup | Sort ResourceGroupName | Select ResourceGroupName
```

<span data-ttu-id="e8886-248">为一组唯一资源组名称填写下表。</span><span class="sxs-lookup"><span data-stu-id="e8886-248">Fill in the following table for the set of unique resource group names.</span></span>
  
|<span data-ttu-id="e8886-249">**项**</span><span class="sxs-lookup"><span data-stu-id="e8886-249">**Item**</span></span>|<span data-ttu-id="e8886-250">**资源组名称**</span><span class="sxs-lookup"><span data-stu-id="e8886-250">**Resource group name**</span></span>|<span data-ttu-id="e8886-251">**目的**</span><span class="sxs-lookup"><span data-stu-id="e8886-251">**Purpose**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="e8886-252">1.</span><span class="sxs-lookup"><span data-stu-id="e8886-252">1.</span></span>  <br/> |<span data-ttu-id="e8886-253">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-253"></span></span>  <br/> |<span data-ttu-id="e8886-254">域控制器</span><span class="sxs-lookup"><span data-stu-id="e8886-254">Domain controllers</span></span>  <br/> |
|<span data-ttu-id="e8886-255">2.</span><span class="sxs-lookup"><span data-stu-id="e8886-255">2.</span></span>  <br/> |<span data-ttu-id="e8886-256">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-256"></span></span>  <br/> |<span data-ttu-id="e8886-257">AD FS 服务器</span><span class="sxs-lookup"><span data-stu-id="e8886-257">AD FS servers</span></span>  <br/> |
|<span data-ttu-id="e8886-258">3.</span><span class="sxs-lookup"><span data-stu-id="e8886-258">3.</span></span>  <br/> |<span data-ttu-id="e8886-259">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-259"></span></span>  <br/> |<span data-ttu-id="e8886-260">Web 应用程序代理服务器</span><span class="sxs-lookup"><span data-stu-id="e8886-260">Web application proxy servers</span></span>  <br/> |
|<span data-ttu-id="e8886-261">4.</span><span class="sxs-lookup"><span data-stu-id="e8886-261">4.</span></span>  <br/> |<span data-ttu-id="e8886-262">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-262"></span></span>  <br/> |<span data-ttu-id="e8886-263">基础结构元素</span><span class="sxs-lookup"><span data-stu-id="e8886-263">Infrastructure elements</span></span>  <br/> |
   
 <span data-ttu-id="e8886-264">**： 表资源组**</span><span class="sxs-lookup"><span data-stu-id="e8886-264">**Table R: Resource groups**</span></span>
  
<span data-ttu-id="e8886-265">使用这些命令创建新的资源组。</span><span class="sxs-lookup"><span data-stu-id="e8886-265">Create your new resource groups with these commands.</span></span>
  
```
$locName="<an Azure location, such as West US>"
$rgName="<Table R - Item 1 - Name column>"
New-AzureRMResourceGroup -Name $rgName -Location $locName
$rgName="<Table R - Item 2 - Name column>"
New-AzureRMResourceGroup -Name $rgName -Location $locName
$rgName="<Table R - Item 3 - Name column>"
New-AzureRMResourceGroup -Name $rgName -Location $locName
$rgName="<Table R - Item 4 - Name column>"
New-AzureRMResourceGroup -Name $rgName -Location $locName
```

<span data-ttu-id="e8886-266">接下来，请创建 Azure 虚拟网络及其子网。</span><span class="sxs-lookup"><span data-stu-id="e8886-266">Next, you create the Azure virtual network and its subnets.</span></span>
  
```
$rgName="<Table R - Item 4 - Resource group name column>"
$locName="<your Azure location>"
$vnetName="<Table V - Item 1 - Value column>"
$vnetAddrPrefix="<Table V - Item 4 - Value column>"
$dnsServers=@( "<Table D - Item 1 - DNS server IP address column>", "<Table D - Item 2 - DNS server IP address column>" )
# Get the shortened version of the location
$locShortName=(Get-AzureRmResourceGroup -Name $rgName).Location

# Create the subnets
$subnet1Name="<Table S - Item 1 - Subnet name column>"
$subnet1Prefix="<Table S - Item 1 - Subnet address space column>"
$subnet1=New-AzureRMVirtualNetworkSubnetConfig -Name $subnet1Name -AddressPrefix $subnet1Prefix
$subnet2Name="<Table S - Item 2 - Subnet name column>"
$subnet2Prefix="<Table S - Item 2 - Subnet address space column>"
$subnet2=New-AzureRMVirtualNetworkSubnetConfig -Name $subnet2Name -AddressPrefix $subnet2Prefix
$subnet3Name="<Table S - Item 3 - Subnet name column>"
$subnet3Prefix="<Table S - Item 3 - Subnet address space column>"
$subnet3=New-AzureRMVirtualNetworkSubnetConfig -Name $subnet3Name -AddressPrefix $subnet3Prefix
$gwSubnet4Prefix="<Table S - Item 4 - Subnet address space column>"
$gwSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $gwSubnet4Prefix

# Create the virtual network
New-AzureRMVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $locName -AddressPrefix $vnetAddrPrefix -Subnet $gwSubnet,$subnet1,$subnet2,$subnet3 -DNSServer $dnsServers

```

<span data-ttu-id="e8886-p112">接下来，创建网络安全组的每个子网包含的虚拟机。若要执行的子网隔离，可以允许或拒绝的子网的网络安全组通信的特定类型的规则。</span><span class="sxs-lookup"><span data-stu-id="e8886-p112">Next, you create network security groups for each subnet that contains virtual machines. To perform subnet isolation, you can add rules for the specific types of traffic allowed or denied to the network security group of a subnet.</span></span>
  
```
# Create network security groups
$vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

New-AzureRMNetworkSecurityGroup -Name $subnet1Name -ResourceGroupName $rgName -Location $locShortName
$nsg=Get-AzureRMNetworkSecurityGroup -Name $subnet1Name -ResourceGroupName $rgName
Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnet1Name -AddressPrefix $subnet1Prefix -NetworkSecurityGroup $nsg

New-AzureRMNetworkSecurityGroup -Name $subnet2Name -ResourceGroupName $rgName -Location $locShortName
$nsg=Get-AzureRMNetworkSecurityGroup -Name $subnet2Name -ResourceGroupName $rgName
Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnet2Name -AddressPrefix $subnet2Prefix -NetworkSecurityGroup $nsg

New-AzureRMNetworkSecurityGroup -Name $subnet3Name -ResourceGroupName $rgName -Location $locShortName
$nsg=Get-AzureRMNetworkSecurityGroup -Name $subnet3Name -ResourceGroupName $rgName
Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnet3Name -AddressPrefix $subnet3Prefix -NetworkSecurityGroup $nsg
```

<span data-ttu-id="e8886-269">下一步，请使用这些命令来创建站点间 VPN 连接的网关。</span><span class="sxs-lookup"><span data-stu-id="e8886-269">Next, use these commands to create the gateways for the site-to-site VPN connection.</span></span>
  
```
$rgName="<Table R - Item 4 - Resource group name column>"
$locName="<Azure location>"
$vnetName="<Table V - Item 1 - Value column>"
$vnet=Get-AzureRMVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
$subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "GatewaySubnet"

# Attach a virtual network gateway to a public IP address and the gateway subnet
$publicGatewayVipName="PublicIPAddress"
$vnetGatewayIpConfigName="PublicIPConfig"
New-AzureRMPublicIpAddress -Name $vnetGatewayIpConfigName -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
$publicGatewayVip=Get-AzureRMPublicIpAddress -Name $vnetGatewayIpConfigName -ResourceGroupName $rgName
$vnetGatewayIpConfig=New-AzureRMVirtualNetworkGatewayIpConfig -Name $vnetGatewayIpConfigName -PublicIpAddressId $publicGatewayVip.Id -Subnet $subnet

# Create the Azure gateway
$vnetGatewayName="AzureGateway"
$vnetGateway=New-AzureRMVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $rgName -Location $locName -GatewayType Vpn -VpnType RouteBased -IpConfigurations $vnetGatewayIpConfig

# Create the gateway for the local network
$localGatewayName="LocalNetGateway"
$localGatewayIP="<Table V - Item 3 - Value column>"
$localNetworkPrefix=@( <comma-separated, double-quote enclosed list of the local network address prefixes from Table L, example: "10.1.0.0/24", "10.2.0.0/24"> )
$localGateway=New-AzureRMLocalNetworkGateway -Name $localGatewayName -ResourceGroupName $rgName -Location $locName -GatewayIpAddress $localGatewayIP -AddressPrefix $localNetworkPrefix

# Define the Azure virtual network VPN connection
$vnetConnectionName="S2SConnection"
$vnetConnectionKey="<Table V - Item 5 - Value column>"
$vnetConnection=New-AzureRMVirtualNetworkGatewayConnection -Name $vnetConnectionName -ResourceGroupName $rgName -Location $locName -ConnectionType IPsec -SharedKey $vnetConnectionKey -VirtualNetworkGateway1 $vnetGateway -LocalNetworkGateway2 $localGateway

```

> [!NOTE]
> <span data-ttu-id="e8886-p113">联合身份验证单个用户的不依赖于任何内部资源。但是，如果此站点到站点 VPN 连接不可用，在 VNet 中的域控制器不会收到用户帐户和组在内部部署 Windows 服务器 AD 中所做的更新。为确保这不会发生，可以为站点到站点 VPN 连接配置高可用性。有关详细信息，请参阅[高度可跨内部和 VNet 到 VNet 的连接](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable)</span><span class="sxs-lookup"><span data-stu-id="e8886-p113">Federated authentication of individual users does not rely on any on-premises resources. However, if this site-to-site VPN connection becomes unavailable, the domain controllers in the VNet will not receive updates to user accounts and groups made in the on-premises Windows Server AD. To ensure this does not happen, you can configure high availability for your site-to-site VPN connection. For more information, see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable)</span></span>
  
<span data-ttu-id="e8886-274">接下来，从此命令的显示内容中，记录用于虚拟网络的 Azure VPN 网关的公用 IPv4 地址。</span><span class="sxs-lookup"><span data-stu-id="e8886-274">Next, record the public IPv4 address of the Azure VPN gateway for your virtual network from the display of this command:</span></span>
  
```
Get-AzureRMPublicIpAddress -Name $publicGatewayVipName -ResourceGroupName $rgName
```

<span data-ttu-id="e8886-p114">接下来，配置内部部署 VPN 设备连接到 Azure VPN 网关。有关详细信息，请参阅[配置 VPN 设备](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices)。</span><span class="sxs-lookup"><span data-stu-id="e8886-p114">Next, configure your on-premises VPN device to connect to the Azure VPN gateway. For more information, see [Configure your VPN device](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices).</span></span>
  
<span data-ttu-id="e8886-277">若要配置本地 VPN 设备，需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="e8886-277">To configure your on-premises VPN device, you will need the following:</span></span>
  
- <span data-ttu-id="e8886-278">Azure VPN 网关的公用 IPv4 地址。</span><span class="sxs-lookup"><span data-stu-id="e8886-278">The public IPv4 address of the Azure VPN gateway.</span></span>
    
- <span data-ttu-id="e8886-279">站点到站点 VPN 连接 （表 V-项目 5-值列） IPsec 预共享的密钥。</span><span class="sxs-lookup"><span data-stu-id="e8886-279">The IPsec pre-shared key for the site-to-site VPN connection (Table V - Item 5 - Value column).</span></span>
    
<span data-ttu-id="e8886-p115">接下来，请确保虚拟网络的地址空间是可以从本地网络访问。这通常是通过以下操作完成：将对应于虚拟网络地址空间的路由添加到 VPN 设备中，然后将该路由公布到组织网络中其余的路由基础结构。与 IT 部门协作，以确定如何完成上述操作。</span><span class="sxs-lookup"><span data-stu-id="e8886-p115">Next, ensure that the address space of the virtual network is reachable from your on-premises network. This is usually done by adding a route corresponding to the virtual network address space to your VPN device and then advertising that route to the rest of the routing infrastructure of your organization network. Work with your IT department to determine how to do this.</span></span>
  
<span data-ttu-id="e8886-p116">接下来，定义三个可用性集的名称。填写表 A。</span><span class="sxs-lookup"><span data-stu-id="e8886-p116">Next, define the names of three availability sets. Fill out Table A.</span></span> 
  
|<span data-ttu-id="e8886-285">**项**</span><span class="sxs-lookup"><span data-stu-id="e8886-285">**Item**</span></span>|<span data-ttu-id="e8886-286">**用途**</span><span class="sxs-lookup"><span data-stu-id="e8886-286">**Purpose**</span></span>|<span data-ttu-id="e8886-287">**可用性设置名称**</span><span class="sxs-lookup"><span data-stu-id="e8886-287">**Availability set name**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="e8886-288">1.</span><span class="sxs-lookup"><span data-stu-id="e8886-288">1.</span></span>  <br/> |<span data-ttu-id="e8886-289">域控制器</span><span class="sxs-lookup"><span data-stu-id="e8886-289">Domain controllers</span></span>  <br/> |<span data-ttu-id="e8886-290">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-290"></span></span>  <br/> |
|<span data-ttu-id="e8886-291">2.</span><span class="sxs-lookup"><span data-stu-id="e8886-291">2.</span></span>  <br/> |<span data-ttu-id="e8886-292">AD FS 服务器</span><span class="sxs-lookup"><span data-stu-id="e8886-292">AD FS servers</span></span>  <br/> |<span data-ttu-id="e8886-293">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-293"></span></span>  <br/> |
|<span data-ttu-id="e8886-294">3.</span><span class="sxs-lookup"><span data-stu-id="e8886-294">3.</span></span>  <br/> |<span data-ttu-id="e8886-295">Web 应用程序代理服务器</span><span class="sxs-lookup"><span data-stu-id="e8886-295">Web application proxy servers</span></span>  <br/> |<span data-ttu-id="e8886-296">_______________________________</span><span class="sxs-lookup"><span data-stu-id="e8886-296"></span></span>  <br/> |
   
 <span data-ttu-id="e8886-297">**表 a： 可用性设置**</span><span class="sxs-lookup"><span data-stu-id="e8886-297">**Table A: Availability sets**</span></span>
  
<span data-ttu-id="e8886-298">在第 2、3 和 4 阶段中创建虚拟机时，将需要这些名称。</span><span class="sxs-lookup"><span data-stu-id="e8886-298">You will need these names when you create the virtual machines in phases 2, 3, and 4.</span></span>
  
<span data-ttu-id="e8886-299">通过这些 Azure PowerShell 命令创建新的可用性集。</span><span class="sxs-lookup"><span data-stu-id="e8886-299">Create the new availability sets with these Azure PowerShell commands.</span></span>
  
```
$locName="<the Azure location for your new resource group>"
$rgName="<Table R - Item 1 - Resource group name column>"
$avName="<Table A - Item 1 - Availability set name column>"
New-AzureRMAvailabilitySet -Name $avName -ResourceGroupName $rgName -Location $locName
$rgName="<Table R - Item 2 - Resource group name column>"
$avName="<Table A - Item 2 - Availability set name column>"
New-AzureRMAvailabilitySet -Name $avName -ResourceGroupName $rgName -Location $locName
$rgName="<Table R - Item 3 - Resource group name column>"
$avName="<Table A - Item 3 - Availability set name column>"
New-AzureRMAvailabilitySet -Name $avName -ResourceGroupName $rgName -Location $locName
```

<span data-ttu-id="e8886-300">这是该阶段成功完成后生成的配置。</span><span class="sxs-lookup"><span data-stu-id="e8886-300">This is the configuration resulting from the successful completion of this phase.</span></span>
  
<span data-ttu-id="e8886-301">**第 1 阶段： Azure 基础结构以实现高可用性的 Office 365 的联合身份验证**</span><span class="sxs-lookup"><span data-stu-id="e8886-301">**Phase 1: The Azure infrastructure for high availability federated authentication for Office 365**</span></span>

![阶段 1：在包含 Azure 基础结构的 Azure 中配置高可用性 Office 365 联合身份验证](images/4e7ba678-07df-40ce-b372-021bf7fc91fa.png)
  
## <a name="next-step"></a><span data-ttu-id="e8886-303">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e8886-303">Next step</span></span>

<span data-ttu-id="e8886-304">使用[高可用性联合身份验证阶段 2： 配置域控制器](high-availability-federated-authentication-phase-2-configure-domain-controllers.md)要继续进行此工作负载的配置。</span><span class="sxs-lookup"><span data-stu-id="e8886-304">Use [High availability federated authentication Phase 2: Configure domain controllers](high-availability-federated-authentication-phase-2-configure-domain-controllers.md) to continue with the configuration of this workload.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="e8886-305">See Also</span><span class="sxs-lookup"><span data-stu-id="e8886-305">See Also</span></span>

[<span data-ttu-id="e8886-306">在 Azure 中部署 Office 365 的高可用性联合身份验证</span><span class="sxs-lookup"><span data-stu-id="e8886-306">Deploy high availability federated authentication for Office 365 in Azure</span></span>](deploy-high-availability-federated-authentication-for-office-365-in-azure.md)
  
[<span data-ttu-id="e8886-307">用于 Office 365 开发/测试环境的联合身份</span><span class="sxs-lookup"><span data-stu-id="e8886-307">Federated identity for your Office 365 dev/test environment</span></span>](federated-identity-for-your-office-365-dev-test-environment.md)
  
[<span data-ttu-id="e8886-308">云应用和混合解决方案</span><span class="sxs-lookup"><span data-stu-id="e8886-308">Cloud adoption and hybrid solutions</span></span>](cloud-adoption-and-hybrid-solutions.md)

[<span data-ttu-id="e8886-309">Office 365 的联合标识</span><span class="sxs-lookup"><span data-stu-id="e8886-309">Federated identity for Office 365</span></span>](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

