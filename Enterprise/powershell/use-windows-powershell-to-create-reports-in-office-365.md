---
title: "使用 Windows PowerShell 在 Office 365 中创建报告"
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 12/15/2017
ms.audience: ITPro
ms.topic: hub-page
ms.service: o365-administration
localization_priority: Normal
ms.collection: Ent_O365
ms.custom:
- Ent_Office_Other
- DecEntMigration
ms.assetid: 1ea4d4ec-af89-496f-9678-701867f5a6fc
description: "摘要：使用 Office 365 PowerShell 来创建无法在 Office 365 管理中心生成的报告。"
ms.openlocfilehash: b1cbbbef73a266a62a417d2714fefcd630c604c4
ms.sourcegitcommit: d31cf57295e8f3d798ab971d405baf3bd3eb7a45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2017
---
# <a name="use-windows-powershell-to-create-reports-in-office-365"></a><span data-ttu-id="6c216-103">使用 Windows PowerShell 在 Office 365 中创建报告</span><span class="sxs-lookup"><span data-stu-id="6c216-103">Use Windows PowerShell to create reports in Office 365</span></span>

 <span data-ttu-id="6c216-104">**摘要：**使用 Office 365 PowerShell 创建无法在 Office 365 管理中心生成的报告。</span><span class="sxs-lookup"><span data-stu-id="6c216-104">**Summary:** Use Office 365 PowerShell to create reports that you cannot produce in the Office 365 Admin center.</span></span>
  
<span data-ttu-id="6c216-p101">Office 365 管理中心中提供很多不同的报告。但是，这些报告提供的信息有限，有时你可能需要更多信息。这就是你需要 Office 365 PowerShell 的时候</span><span class="sxs-lookup"><span data-stu-id="6c216-p101">There are many different reports available in the Office 365 Admin center. However, these reports only provide so much information and sometimes you need more. That's when you need Office 365 PowerShell</span></span>
  
<span data-ttu-id="6c216-108">这些文章介绍如何使用 Office 365 PowerShell 以从你的 Office 365 租户获取信息：</span><span class="sxs-lookup"><span data-stu-id="6c216-108">These articles that describe how to use Office 365 PowerShell to obtain information from your Office 365 tenant:</span></span>
  
- <span data-ttu-id="6c216-109">开始使用 Office 365 PowerShell 进行报告：</span><span class="sxs-lookup"><span data-stu-id="6c216-109">Getting started with reporting using Office 365 PowerShell:</span></span>
    
  - [<span data-ttu-id="6c216-110">Office 365 PowerShell 可能会显示你通过管理中心无法看到的其他信息</span><span class="sxs-lookup"><span data-stu-id="6c216-110">Office 365 PowerShell can reveal additional information that you cannot see with the Admin center</span></span>](https://technet.microsoft.com/library/dn568034.aspx#reveal)
    
  - [<span data-ttu-id="6c216-111">Office 365 PowerShell 善于筛选数据</span><span class="sxs-lookup"><span data-stu-id="6c216-111">Office 365 PowerShell is great at filtering data</span></span>](https://technet.microsoft.com/library/dn568034.aspx#filter)
    
  - [<span data-ttu-id="6c216-112">Office 365 PowerShell 方便打印或保存数据</span><span class="sxs-lookup"><span data-stu-id="6c216-112">Office 365 PowerShell makes it easy to print or save data</span></span>](https://technet.microsoft.com/library/dn568034.aspx#printsave)
    
- <span data-ttu-id="6c216-113">用户帐户和许可证报告：</span><span class="sxs-lookup"><span data-stu-id="6c216-113">Reports for user accounts and licenses:</span></span>
    
  - [<span data-ttu-id="6c216-114">使用 Office 365 PowerShell 查看许可证和服务</span><span class="sxs-lookup"><span data-stu-id="6c216-114">View licenses and services with Office 365 PowerShell</span></span>](view-licenses-and-services-with-office-365-powershell.md)
    
  - [<span data-ttu-id="6c216-115">使用 Office 365 PowerShell 查看授权和未授权的用户</span><span class="sxs-lookup"><span data-stu-id="6c216-115">View licensed and unlicensed users with Office 365 PowerShell</span></span>](view-licensed-and-unlicensed-users-with-office-365-powershell.md)
    
  - [<span data-ttu-id="6c216-116">使用 Office 365 PowerShell 查看帐户许可证和服务详细信息</span><span class="sxs-lookup"><span data-stu-id="6c216-116">View account license and service details with Office 365 PowerShell</span></span>](view-account-license-and-service-details-with-office-365-powershell.md)
    
  - [<span data-ttu-id="6c216-117">查看用户帐户与 Office 365 PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c216-117">View user accounts with Office 365 PowerShell</span></span>](view-user-accounts-with-office-365-powershell.md)
    
- <span data-ttu-id="6c216-118">SharePoint Online 报告：</span><span class="sxs-lookup"><span data-stu-id="6c216-118">Reports for SharePoint Online:</span></span>
    
  - [<span data-ttu-id="6c216-119">使用 Office 365 PowerShell 管理 SharePoint Online 用户和组</span><span class="sxs-lookup"><span data-stu-id="6c216-119">Manage SharePoint Online users and groups with Office 365 PowerShell</span></span>](http://technet.microsoft.com/library/9680af2e-a965-4e62-92ee-da72105c7800.aspx)
    
  - [<span data-ttu-id="6c216-120">Manage SharePoint Online site groups with Office 365 PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c216-120">Manage SharePoint Online site groups with Office 365 PowerShell</span></span>](http://technet.microsoft.com/library/122f4099-c78d-4cce-bab0-4343b04596ae.aspx)
    
- <span data-ttu-id="6c216-121">Exchange Online 报告：</span><span class="sxs-lookup"><span data-stu-id="6c216-121">Reports for Exchange Online:</span></span>
    
  - [<span data-ttu-id="6c216-122">Display Exchange Online mailbox information with Office 365 PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c216-122">Display Exchange Online mailbox information with Office 365 PowerShell</span></span>](http://technet.microsoft.com/library/13843002-56ca-4b75-81c5-84386522b01b.aspx)
    
  - [<span data-ttu-id="6c216-123">Display Exchange Online reports with Office 365 PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c216-123">Display Exchange Online reports with Office 365 PowerShell</span></span>](http://technet.microsoft.com/library/4873a063-9fc4-4ed9-826a-6e935fef61d4.aspx)
    
## <a name="see-also"></a><span data-ttu-id="6c216-124">See also</span><span class="sxs-lookup"><span data-stu-id="6c216-124">See also</span></span>

#### 

[<span data-ttu-id="6c216-125">使用 Office 365 PowerShell 管理 Office 365</span><span class="sxs-lookup"><span data-stu-id="6c216-125">Manage Office 365 with Office 365 PowerShell</span></span>](manage-office-365-with-office-365-powershell.md)
  
[<span data-ttu-id="6c216-126">Office 365 PowerShell 入门</span><span class="sxs-lookup"><span data-stu-id="6c216-126">Getting started with Office 365 PowerShell</span></span>](getting-started-with-office-365-powershell.md)
  
[<span data-ttu-id="6c216-127">使用 Office 365 PowerShell 管理 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6c216-127">Manage SharePoint Online with Office 365 PowerShell</span></span>](manage-sharepoint-online-with-office-365-powershell.md)
  
[<span data-ttu-id="6c216-128">使用 Office 365 PowerShell 管理用户帐户和许可证</span><span class="sxs-lookup"><span data-stu-id="6c216-128">Manage user accounts and licenses with Office 365 PowerShell</span></span>](manage-user-accounts-and-licenses-with-office-365-powershell.md)
  
[<span data-ttu-id="6c216-129">使用 Excel 检索 Office 365 报告数据</span><span class="sxs-lookup"><span data-stu-id="6c216-129">Using Excel to Retrieve Office 365 Reporting Data</span></span>](using-excel-to-retrieve-office-365-reporting-data.md)
