---
title: 将内容限制到某个地理位置
ms.author: mikeplum
author: MikePlumleyMSFT
manager: pamgreen
ms.audience: ITPro
ms.topic: article
ms.service: o365-solutions
ms.custom: ''
ms.collection: Strat_SP_gtc
localization_priority: Priority
description: 了解如何将 SharePoint 站点限制到多地理位置环境中的指定地理位置。
ms.openlocfilehash: 59301a591e5465bdcda4aa84a18880961c0b615b
ms.sourcegitcommit: 8ba20f1b1839630a199585da0c83aaebd1ceb9fc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "30933944"
---
# <a name="restrict-content-to-a-geo-location"></a><span data-ttu-id="20b20-103">将内容限制到某个地理位置</span><span class="sxs-lookup"><span data-stu-id="20b20-103">Restrict content to a geo location</span></span>

<span data-ttu-id="20b20-104">在某些情况下，你可能会选择通过以下方式将某个站点及其文件内容强制保留在（在其中创建了站点的）地理位置中：防止转移站点，或者防止将站点的文件内容缓存在另一个地理位置中。</span><span class="sxs-lookup"><span data-stu-id="20b20-104">Under some circumstances you may choose to enforce a site and its file content to remain in the geo location where the site was created, either by preventing the site from being moved or by preventing the caching of the site's file content in another geo location.</span></span>

<span data-ttu-id="20b20-105">可使用 **RestrictedToGeo** 参数通过 [Set-SPOSite](https://docs.microsoft.com/powershell/module/sharepoint-online/set-sposite) cmdlet 来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="20b20-105">You can do this by using the [Set-SPOSite](https://docs.microsoft.com/powershell/module/sharepoint-online/set-sposite) cmdlet with the **RestrictedToGeo** parameter.</span></span> <span data-ttu-id="20b20-106">此参数的默认值为 NULL，但你可以将其更改为以下值之一：</span><span class="sxs-lookup"><span data-stu-id="20b20-106">This parameter has a default value of NULL, but you can change it to one of the following:</span></span>

|<span data-ttu-id="20b20-107">限制</span><span class="sxs-lookup"><span data-stu-id="20b20-107">Restriction</span></span>|<span data-ttu-id="20b20-108">说明</span><span class="sxs-lookup"><span data-stu-id="20b20-108">Description</span></span>|
|:----------|:----------|
|<span data-ttu-id="20b20-109">NoRestriction</span><span class="sxs-lookup"><span data-stu-id="20b20-109">NoRestriction</span></span>|<span data-ttu-id="20b20-110">可将站点转移到另一个地理位置。</span><span class="sxs-lookup"><span data-stu-id="20b20-110">The site can be moved to another geo location.</span></span>|
|<span data-ttu-id="20b20-111">BlockMoveOnly</span><span class="sxs-lookup"><span data-stu-id="20b20-111">BlockMoveOnly</span></span>|<span data-ttu-id="20b20-112">无法将站点转移到另一个地理位置，但可将站点内容缓存在其他地理位置中。</span><span class="sxs-lookup"><span data-stu-id="20b20-112">Site cannot be moved to another geo location, but site content can be cached in other geo locations.</span></span>|
|<span data-ttu-id="20b20-113">BlockFull</span><span class="sxs-lookup"><span data-stu-id="20b20-113">BlockFull</span></span>|<span data-ttu-id="20b20-114">无法将站点转移到另一个地理位置，并且不会在其他地理位置中缓存完整文件内容。</span><span class="sxs-lookup"><span data-stu-id="20b20-114">Site cannot be moved to another geo location, and full file content is not cached in other geo locations.</span></span> <span data-ttu-id="20b20-115">文件的标题（从内容中获取）、文件名和文件的其他属性仍可缓存在其他地理位置中。</span><span class="sxs-lookup"><span data-stu-id="20b20-115">Files' title (harvested from the content), file name, and other properties of the file can still be cached in other geo-locations.</span></span><br><span data-ttu-id="20b20-116">将该参数配置为 BlockFull 之前存储在站点中的内容可能继续缓存在其他地理位置中。</span><span class="sxs-lookup"><span data-stu-id="20b20-116">Content stored in the site before it was configured to BlockFull, may continue to be cached in other geo locations.</span></span>|

<span data-ttu-id="20b20-117">使用以下语法：</span><span class="sxs-lookup"><span data-stu-id="20b20-117">Use the following syntax:</span></span>

`Set-SPOSite -Identity <siteURL> -RestrictedToGeo <restriction>`

<span data-ttu-id="20b20-118">例如：</span><span class="sxs-lookup"><span data-stu-id="20b20-118">For example:</span></span>

`Set-SPOSite -Identity https://contoso.sharepoint.com/sites/RegionRestrictedTeamSite -RestrictedToGeo BlockFull`