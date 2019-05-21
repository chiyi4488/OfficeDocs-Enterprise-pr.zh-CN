---
title: Office 365 客户端应用程序支持—单一登录
ms.author: robmazz
author: robmazz
manager: laurawi
audience: ITPro
ms.topic: article
ms.service: Office 365 Administration
localization_priority: Normal
ms.collection:
- Strat_O365_Enterprise
- M365-subscription-management
search.appverid:
- MET150
description: Office 365 客户端应用程序支持单一登录。
ms.openlocfilehash: 1ab1a2d7c461c1ae44f0fefba4b9a3663753fb97
ms.sourcegitcommit: 9c6e31204aa326c31d60befe80e610f702e65800
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "33990903"
---
# <a name="office-365-client-app-support--single-sign-on"></a>Office 365 客户端应用程序支持—单一登录

当用户登录到 Azure Active Directory (Azure AD) 中的应用程序时, 单一登录 (SSO) 将增加安全性和方便性。 通过单一登录, 用户可使用一个帐户登录一次, 以访问加入域的设备、公司资源、软件即服务 (SaaS) 应用程序和 web 应用程序。

了解有关[单一登录](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on)的详细信息。

## <a name="supported-platforms"></a>支持的平台

 - Windows 10 桌面版
 - Windows 10 新式应用
 - Web 浏览器
 - Android
 - iOS<sup>1</sup>
 - macOS

有关 Office 365 中平台支持的详细信息, 请参阅[office 365 的系统要求](https://products.office.com/office-system-requirements)。

## <a name="supported-clients"></a>支持的客户端

以下客户端的最新版本支持单一登录:

| | | | | | |
|:---:|:---:|:---:|:---:|:---:|:---:|
| ![访问图标](media/o365-access-64x64.png) <br> [访问](https://products.office.com/access) | ![公司门户图标](media/o365-microsoft-64x64.png) <br> [公司<br>门户](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal) | ![边缘图标](media/o365-edge-64x64.png) <br> [距](https://www.microsoft.com/windows/microsoft-edge) | ![Excel 图标](media/o365-excel-64x64.png) <br> [Excel](https://products.office.com/excel) | ![流图标](media/o365-flow-64x64.png) <br> [Flow](https://flow.microsoft.com) 
| ![镜头图标](media/o365-lens-64x64.png) <br> [Office Lens](https://www.microsoft.com/p/office-lens/9wzdncrfj3t8?activetab=pivot%3Aoverviewtab) | ![OneDrive for Business 图标](media/o365-OneDrive-64x64.png) <br> [OneDrive](https://products.office.com/onedrive-for-business/online-cloud-storage) |  ![OneNote 图标](media/o365-OneNote-64x64.png) <br> [OneNote](https://products.office.com/onenote) | ![Outlook 图标](media/o365-outlook-64x64.png) <br> [Outlook](https://products.office.com/outlook) | ![Planner 图标](media/o365-planner-64x64.png) <br> [Planner](https://products.office.com/business/task-management-software) 
| ![PowerBI 图标](media/o365-powerbi-64x64.png) <br> [Power BI](https://powerbi.microsoft.com)| ![PowerPoint 图标](media/o365-powerpoint-64x64.png) <br> [PowerPoint](https://products.office.com/powerpoint) | ![项目图标](media/o365-project-64x64.png) <br> [项目](https://products.office.com/project) | ![Publisher 图标](media/o365-publisher-64x64.png) <br> [Publisher](https://products.office.com/publisher) | ![SharePoint 图标](media/o365-sharepoint-64x64.png) <br> [Sharepoint](https://products.office.com/sharepoint) 
| ![Skype for Business 图标](media/o365-skypeforbusiness-64x64.png) <br> [Skype for <br> business](https://www.skype.com/business/) | ![粘滞便笺图标](media/o365-stickynotes-64x64.png) <br> [粘滞便笺](https://www.microsoft.com/p/microsoft-sticky-notes/9nblggh4qghw) | ![Sway 图标](media/o365-sway-64x64.png) <br> [Sway](https://sway.com) | ![团队图标](media/o365-teams-64x64.png) <br> [团队<sup>1</sup>](https://products.office.com/microsoft-teams/group-chat-software) | ![待办情况图标](media/o365-todo-64x64.png) <br> [微软待办](https://todo.microsoft.com) 
| ![Visio 图标](media/o365-visio-64x64.png) <br> [Visio](https://products.office.com/visio/flowchart-software) | ![Word 图标](media/o365-word-64x64.png) <br> [Word](https://products.office.com/word) | ![Yammer 图标](media/o365-yammer-64x64.png) <br> [Yammer](https://products.office.com/yammer/yammer-overview) |

## <a name="supported-powershell-modules"></a>支持的 PowerShell 模块

| | | | | | |
|:---:|:---:|:---:|:---:|:---:|:---:|
| ![Azure 图标](media/o365-azure-64x64.png) <br> [Azure AD <br> PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0) | ![Exchange 图标](media/o365-exchange-64x64.png) <br> [Exchange Online <br> PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/exchange-online-powershell?view=exchange-ps) | ![SharePoint 图标](media/o365-sharepoint-64x64.png) <br> [SharePoint Online <br> PowerShell](https://docs.microsoft.com/sharepoint/manage-team-and-communication-sites-in-powershell)

> [!NOTE]
> <sup>1</sup>仅支持 iOS 上的团队。 <br>