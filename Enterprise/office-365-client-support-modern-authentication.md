---
title: Office 365 客户端应用程序支持的现代身份验证
ms.author: robmazz
author: robmazz
manager: laurawi
ms.date: 7/17/2018
audience: ITPro
ms.topic: article
ms.service: Office 365 Administration
localization_priority: None
ms.collection: Strat_O365_Enterprise
description: Office 365 客户端应用程序支持的现代身份验证。
ms.openlocfilehash: 73827d1e19556a31c9eb3a11c9fa6617bee3f566
ms.sourcegitcommit: 4e654517825b74a3bbe171b915b134ba49231e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2018
ms.locfileid: "21541952"
---
# <a name="office-365-client-app-support---modern-authentication"></a><span data-ttu-id="52fd1-103">Office 365 客户端应用程序支持的现代身份验证</span><span class="sxs-lookup"><span data-stu-id="52fd1-103">Office 365 Client App Support - Modern Authentication</span></span>

<span data-ttu-id="52fd1-p101">Microsoft 的现代身份验证功能基于 Active Directory 身份验证库 ADAL 登录的 Office 客户端应用程序允许跨不同的平台。这样，如多因素身份验证 (MFA)、 智能卡和基于证书的身份验证登录功能。</span><span class="sxs-lookup"><span data-stu-id="52fd1-p101">Microsoft’s Modern Authentication capability enables Active Directory Authentication Library (ADAL)-based sign-in for Office client apps across different platforms. This enables sign-in features such as Multi-Factor Authentication (MFA), smart card and certificate-based authentication.</span></span>

<span data-ttu-id="52fd1-106">了解更多有关[多重身份验证](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication)和[基于证书的身份验证](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started)。</span><span class="sxs-lookup"><span data-stu-id="52fd1-106">Learn more about [multi-factor authentication](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication) and [certificate-based authentication](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started).</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="52fd1-107">支持的平台</span><span class="sxs-lookup"><span data-stu-id="52fd1-107">Supported platforms</span></span>

 - <span data-ttu-id="52fd1-108">Windows 10 桌面</span><span class="sxs-lookup"><span data-stu-id="52fd1-108">Windows 10 Desktop</span></span>
 - <span data-ttu-id="52fd1-109">Windows 10 现代应用程序</span><span class="sxs-lookup"><span data-stu-id="52fd1-109">Windows 10 Modern Apps</span></span>
 - <span data-ttu-id="52fd1-110">Web 浏览器</span><span class="sxs-lookup"><span data-stu-id="52fd1-110">Web Browser</span></span>
 - <span data-ttu-id="52fd1-111">Android</span><span class="sxs-lookup"><span data-stu-id="52fd1-111">Android</span></span>
 - <span data-ttu-id="52fd1-112">iOS</span><span class="sxs-lookup"><span data-stu-id="52fd1-112">iOS</span></span>
 - <span data-ttu-id="52fd1-113">macOS</span><span class="sxs-lookup"><span data-stu-id="52fd1-113">macOS</span></span>

## <a name="supported-clients"></a><span data-ttu-id="52fd1-114">支持的客户端</span><span class="sxs-lookup"><span data-stu-id="52fd1-114">Supported clients</span></span>

| | | | | | |
|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="52fd1-115">![深入图标](images/o365-delve-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-115">![Delve icon](images/o365-delve-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-116">Delve</span><span class="sxs-lookup"><span data-stu-id="52fd1-116">Delve</span></span>](https://products.office.com/business/intelligent-search) | <span data-ttu-id="52fd1-117">![Dynamics 365 图标](images/o365-dynamics365-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-117">![Dynamics 365 icon](images/o365-dynamics365-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-118">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="52fd1-118">Dynamics 365</span></span>](https://dynamics.microsoft.com) | <span data-ttu-id="52fd1-119">![Excel 图标](images/o365-excel-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-119">![Excel icon](images/o365-excel-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-120">Excel</span><span class="sxs-lookup"><span data-stu-id="52fd1-120">Excel</span></span>](https://products.office.com/excel) | <span data-ttu-id="52fd1-121">![流图标](images/o365-flow-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-121">![Flow icon](images/o365-flow-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-122">Flow</span><span class="sxs-lookup"><span data-stu-id="52fd1-122">Flow</span></span>](https://flow.microsoft.com) | <span data-ttu-id="52fd1-123">![表单图标](images/o365-forms-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-123">![Forms icon](images/o365-forms-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-124">Forms</span><span class="sxs-lookup"><span data-stu-id="52fd1-124">Forms</span></span>](https://flow.microsoft.com/connectors/shared_microsoftforms/microsoft-forms/) | 
| <span data-ttu-id="52fd1-125">![Kaizala 图标](images/o365-kaizala-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-125">![Kaizala icon](images/o365-kaizala-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-126">Kaizala</span><span class="sxs-lookup"><span data-stu-id="52fd1-126">Kaizala</span></span>](https://products.office.com/en/business/microsoft-kaizala) | <span data-ttu-id="52fd1-127">![Office 365 管理图标](images/o365-o365admin-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-127">![Office 365 Admin icon](images/o365-o365admin-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-128">Office 365<br>管理</span><span class="sxs-lookup"><span data-stu-id="52fd1-128">Office 365 <br> Admin</span></span>](https://products.office.com/business/manage-office-365-admin-app) | <span data-ttu-id="52fd1-129">![镜头图标](images/o365-lens-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-129">![Lens icon](images/o365-lens-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-130">Office Lens</span><span class="sxs-lookup"><span data-stu-id="52fd1-130">Office Lens</span></span>](https://www.microsoft.com/p/office-lens/9wzdncrfj3t8?activetab=pivot%3Aoverviewtab) | <span data-ttu-id="52fd1-131">![OneDrive for Business 图标](images/o365-OneDrive-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-131">![OneDrive for Business icon](images/o365-OneDrive-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-132">OneDrive</span><span class="sxs-lookup"><span data-stu-id="52fd1-132">OneDrive</span></span>](https://products.office.com/onedrive-for-business/online-cloud-storage) | <span data-ttu-id="52fd1-133">![OneNote 图标](images/o365-OneNote-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-133">![OneNote icon](images/o365-OneNote-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-134">OneNote</span><span class="sxs-lookup"><span data-stu-id="52fd1-134">OneNote</span></span>](https://products.office.com/onenote)
| <span data-ttu-id="52fd1-135">![Outlook 图标](images/o365-outlook-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-135">![Outlook icon](images/o365-outlook-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-136">Outlook</span><span class="sxs-lookup"><span data-stu-id="52fd1-136">Outlook</span></span>](https://products.office.com/outlook) | <span data-ttu-id="52fd1-137">![计划工具图标](images/o365-planner-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-137">![Planner icon](images/o365-planner-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-138">Planner</span><span class="sxs-lookup"><span data-stu-id="52fd1-138">Planner</span></span>](https://products.office.com/business/task-management-software) | <span data-ttu-id="52fd1-139">![PowerBI 图标](images/o365-powerbi-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-139">![PowerBI icon](images/o365-powerbi-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-140">Power BI</span><span class="sxs-lookup"><span data-stu-id="52fd1-140">Power BI</span></span>](https://powerbi.microsoft.com) | <span data-ttu-id="52fd1-141">![PowerPoint 图标](images/o365-powerpoint-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-141">![PowerPoint icon](images/o365-powerpoint-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-142">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="52fd1-142">PowerPoint</span></span>](https://products.office.com/powerpoint) | <span data-ttu-id="52fd1-143">![项目图标](images/o365-project-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-143">![Project icon](images/o365-project-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-144">Project</span><span class="sxs-lookup"><span data-stu-id="52fd1-144">Project</span></span>](https://products.office.com/project) 
| <span data-ttu-id="52fd1-145">![SharePoint 图标](images/o365-sharepoint-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-145">![SharePoint icon](images/o365-sharepoint-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-146">Sharepoint</span><span class="sxs-lookup"><span data-stu-id="52fd1-146">Sharepoint</span></span>](https://products.office.com/sharepoint) | <span data-ttu-id="52fd1-147">![Skype 业务图标](images/o365-skypeforbusiness-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-147">![Skype for Business icon](images/o365-skypeforbusiness-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-148">Skype 的<br>业务</span><span class="sxs-lookup"><span data-stu-id="52fd1-148">Skype for <br> Business</span></span>](https://www.skype.com/business/) | <span data-ttu-id="52fd1-149">![StaffHub 图标](images/o365-staffhub-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-149">![StaffHub icon](images/o365-staffhub-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-150">StaffHub</span><span class="sxs-lookup"><span data-stu-id="52fd1-150">StaffHub</span></span>](https://products.office.com/microsoft-staffhub/staff-scheduling-software) | <span data-ttu-id="52fd1-151">![流图标](images/o365-stream-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-151">![Stream icon](images/o365-stream-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-152">流</span><span class="sxs-lookup"><span data-stu-id="52fd1-152">Stream</span></span>](https://stream.microsoft.com) | <span data-ttu-id="52fd1-153">![Sway 图标](images/o365-sway-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-153">![Sway icon](images/o365-sway-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-154">Sway</span><span class="sxs-lookup"><span data-stu-id="52fd1-154">Sway</span></span>](https://sway.com)
| <span data-ttu-id="52fd1-155">![团队图标](images/o365-teams-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-155">![Teams icon](images/o365-teams-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-156">Teams</span><span class="sxs-lookup"><span data-stu-id="52fd1-156">Teams</span></span>](https://products.office.com/microsoft-teams/group-chat-software) | <span data-ttu-id="52fd1-157">![待办事项图标](images/o365-todo-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-157">![To-Do icon](images/o365-todo-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-158">微软待办</span><span class="sxs-lookup"><span data-stu-id="52fd1-158">To-Do</span></span>](https://todo.microsoft.com) | <span data-ttu-id="52fd1-159">![Visio 图标](images/o365-visio-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-159">![Visio icon](images/o365-visio-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-160">Visio</span><span class="sxs-lookup"><span data-stu-id="52fd1-160">Visio</span></span>](https://products.office.com/visio/flowchart-software) | <span data-ttu-id="52fd1-161">![Word 图标](images/o365-word-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-161">![Word icon](images/o365-word-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-162">Word</span><span class="sxs-lookup"><span data-stu-id="52fd1-162">Word</span></span>](https://products.office.com/word) | <span data-ttu-id="52fd1-163">![Yammer 图标](images/o365-yammer-64x64.png)</span><span class="sxs-lookup"><span data-stu-id="52fd1-163">![Yammer icon](images/o365-yammer-64x64.png)</span></span> <br> [<span data-ttu-id="52fd1-164">Yammer</span><span class="sxs-lookup"><span data-stu-id="52fd1-164">Yammer</span></span>](https://products.office.com/yammer/yammer-overview)