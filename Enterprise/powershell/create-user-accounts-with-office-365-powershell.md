---
title: "使用 Office 365 PowerShell 创建用户帐户"
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 12/15/2017
ms.audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
ms.collection: Ent_O365
ms.custom:
- PowerShell
- apr17entnews
- Ent_Office_Other
- DecEntMigration
- O365ITProTrain
ms.assetid: 6770c5fa-b886-4512-8c67-ffd53226589e
description: "了解如何在 Office 365 中使用 Office 365 PowerShell 来创建用户帐户。"
ms.openlocfilehash: 9f6eb4cafa82ae511e806b7e32f2ed98a065d52e
ms.sourcegitcommit: d31cf57295e8f3d798ab971d405baf3bd3eb7a45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2017
---
# <a name="create-user-accounts-with-office-365-powershell"></a><span data-ttu-id="570dd-103">使用 Office 365 PowerShell 创建用户帐户</span><span class="sxs-lookup"><span data-stu-id="570dd-103">Create user accounts with Office 365 PowerShell</span></span>

<span data-ttu-id="570dd-104">**摘要：**了解如何使用 Office 365 PowerShell Office 365 中创建用户帐户。</span><span class="sxs-lookup"><span data-stu-id="570dd-104">**Summary:** Learn how to use Office 365 PowerShell to create user accounts in Office 365.</span></span>
  
<span data-ttu-id="570dd-p101">您可以使用 Office 365 PowerShell 来高效地创建用户帐户，尤其是多个用户帐户。当您在 Office 365 PowerShell 中创建用户帐户时，某些帐户属性始终是必需的。其他属性对于创建帐户则不是必需的，但也很重要。下表介绍了这些属性：</span><span class="sxs-lookup"><span data-stu-id="570dd-p101">You can use Office 365 PowerShell to efficiently create user accounts, especially multiple user accounts. When you create user accounts in Office 365 PowerShell, certain account properties are always required. Other properties aren't required to create the account, but are otherwise important. These properties are described in the following table:</span></span>
  
****

|<span data-ttu-id="570dd-109">**属性名称**</span><span class="sxs-lookup"><span data-stu-id="570dd-109">**Property name**</span></span>|<span data-ttu-id="570dd-110">**是否必需？**</span><span class="sxs-lookup"><span data-stu-id="570dd-110">**Required?**</span></span>|<span data-ttu-id="570dd-111">**说明**</span><span class="sxs-lookup"><span data-stu-id="570dd-111">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="570dd-112">**DisplayName**</span><span class="sxs-lookup"><span data-stu-id="570dd-112">**DisplayName**</span></span> <br/> |<span data-ttu-id="570dd-113">是</span><span class="sxs-lookup"><span data-stu-id="570dd-113">Yes</span></span>  <br/> |<span data-ttu-id="570dd-p102">这是在 Office 365 服务中使用的显示名称。例如，Caleb Sills。</span><span class="sxs-lookup"><span data-stu-id="570dd-p102">This is the display name that's used in Office 365 services. For example, Caleb Sills.</span></span>  <br/> |
|<span data-ttu-id="570dd-116">**UserPrincipalName**</span><span class="sxs-lookup"><span data-stu-id="570dd-116">**UserPrincipalName**</span></span> <br/> |<span data-ttu-id="570dd-117">是</span><span class="sxs-lookup"><span data-stu-id="570dd-117">Yes</span></span>  <br/> |<span data-ttu-id="570dd-p103">这是用于登录到 Office 365 服务的帐户名称。例如，CalebS@contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="570dd-p103">This is the account name that's used to sign in to Office 365 services. For example, CalebS@contoso.onmicrosoft.com.</span></span>  <br/> |
|<span data-ttu-id="570dd-120">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="570dd-120">**FirstName**</span></span> <br/> |<span data-ttu-id="570dd-121">否</span><span class="sxs-lookup"><span data-stu-id="570dd-121">No</span></span>  <br/> ||
|<span data-ttu-id="570dd-122">**LastName**</span><span class="sxs-lookup"><span data-stu-id="570dd-122">**LastName**</span></span> <br/> |<span data-ttu-id="570dd-123">否</span><span class="sxs-lookup"><span data-stu-id="570dd-123">No</span></span>  <br/> ||
|<span data-ttu-id="570dd-124">**LicenseAssignment**</span><span class="sxs-lookup"><span data-stu-id="570dd-124">**LicenseAssignment**</span></span> <br/> |<span data-ttu-id="570dd-125">否</span><span class="sxs-lookup"><span data-stu-id="570dd-125">No</span></span>  <br/> |<span data-ttu-id="570dd-p104">这是许可计划（也称为许可证计划、Office 365 计划或 SKU），使用它可以将可用的许可证分配给用户帐户。该许可证定义可供帐户使用的 Office 365 服务。当您创建帐户时，您没有向用户分配许可证，但该帐户需要许可证才能访问 Office 365 服务。创建用户帐户后，您有 30 天的时间可以对该用户帐户授权。</span><span class="sxs-lookup"><span data-stu-id="570dd-p104">This is the licensing plan (also known as the license plan, Office 365 plan, or SKU) from which an available license is assigned to the user account. The license defines the Office 365 services that are available to account. You don't have to assign a license to a user when you create the account, but the account requires a license to access Office 365 services. You have 30 days to license the user account after you create it.  </span></span><br/> <span data-ttu-id="570dd-p105">使用**Get MsolAccountSku** cmdlet 可以查看贵组织中的授权计划 ( **AccountSkuId** ) 和可用的许可证。有关详细信息，请参阅[查看许可证和 Office 365 PowerShell 的服务](view-licenses-and-services-with-office-365-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="570dd-p105">Use the **Get-MsolAccountSku** cmdlet to view the licensing plans ( **AccountSkuId** ) and available licenses in your organization. For more information, see [View licenses and services with Office 365 PowerShell](view-licenses-and-services-with-office-365-powershell.md).  </span></span><br/> |
|<span data-ttu-id="570dd-132">**Password**</span><span class="sxs-lookup"><span data-stu-id="570dd-132">**Password**</span></span> <br/> |<span data-ttu-id="570dd-133">否</span><span class="sxs-lookup"><span data-stu-id="570dd-133">No</span></span>  <br/> | <span data-ttu-id="570dd-p106">如果您没有指定密码，将向用户帐户分配一个随机密码，且该密码将显示在命令结果中。如果您指定了密码，则需要满足以下复杂性要求：</span><span class="sxs-lookup"><span data-stu-id="570dd-p106">If you don't specify a password, a random password is assigned to the user account, and the password is visible in the results of the command. If you specify a password, it needs to meet the following complexity requirements:</span></span> <br/>  <span data-ttu-id="570dd-136">8 到 16 个 ASCII 文本字符。</span><span class="sxs-lookup"><span data-stu-id="570dd-136">8 to 16 ASCII text characters.</span></span> <br/>  <span data-ttu-id="570dd-137">下列三种类型的字符：小写字母、大写字母、数字和符号。</span><span class="sxs-lookup"><span data-stu-id="570dd-137">Characters from any three of the following types: lowercase letters, uppercase letters, numbers, and symbols.</span></span> <br/> |
|<span data-ttu-id="570dd-138">**UsageLocation**</span><span class="sxs-lookup"><span data-stu-id="570dd-138">**UsageLocation**</span></span> <br/> |<span data-ttu-id="570dd-139">否</span><span class="sxs-lookup"><span data-stu-id="570dd-139">No</span></span>  <br/> |<span data-ttu-id="570dd-p107">这是一个由两位字母组成的有效 ISO 3166-1 国家/地区代码。例如，US 代表美国，FR 代表法国。请务必提供此值，因为某些 Office 365 服务在某些国家不可用，因此不能为用户帐户分配许可证，除非该帐户已配置此值。有关详细信息，请参阅[关于许可证限制](https://go.microsoft.com/fwlink/p/?LinkId=691730)。</span><span class="sxs-lookup"><span data-stu-id="570dd-p107">This is a valid ISO 3166-1 alpha-2 country code. For example, US for the United States, and FR for France. It's important to provide this value, because some Office 365 services aren't available in certain countries, so you can't assign a license to a user account unless the account has this value configured. For more information, see [About license restrictions](https://go.microsoft.com/fwlink/p/?LinkId=691730).  </span></span><br/> |
   
## <a name="before-you-begin"></a><span data-ttu-id="570dd-144">开始之前</span><span class="sxs-lookup"><span data-stu-id="570dd-144">Before you begin</span></span>

<span data-ttu-id="570dd-p108">若要执行此主题中的过程，必须连接到 Office 365 PowerShell。有关说明，请参阅[连接到 Office 365 PowerShell](connect-to-office-365-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="570dd-p108">The procedures in this topic require you to connect to Office 365 PowerShell. For instructions, see [Connect to Office 365 PowerShell](connect-to-office-365-powershell.md).</span></span>
  
## <a name="use-office-365-powershell-to-create-individual-user-accounts"></a><span data-ttu-id="570dd-147">使用 Office 365 PowerShell 创建单个用户帐户</span><span class="sxs-lookup"><span data-stu-id="570dd-147">Use Office 365 PowerShell to create individual user accounts</span></span>

<span data-ttu-id="570dd-148">若要创建单个帐户，请使用下面的语法：</span><span class="sxs-lookup"><span data-stu-id="570dd-148">To create an individual account, use the following syntax:</span></span>
  
```
New-MsolUser -DisplayName <DisplayName> -FirstName <FirstName> -LastName <LastName> -UserPrincipalName <Account> -UsageLocation <CountryCode> -LicenseAssignment <AccountSkuID> [-Password <Password>]
```

<span data-ttu-id="570dd-149">本示例为美国用户 Caleb Sills 创建一个帐户并通过  `contoso:ENTERPRISEPACK` (Office 365 企业版 E3) 许可计划分配了一个许可证。</span><span class="sxs-lookup"><span data-stu-id="570dd-149">This example creates an account for the United States user named Caleb Sills, and assigns a license from the  `contoso:ENTERPRISEPACK` (Office 365 Enterprise E3) licensing plan.</span></span>
  
```
New-MsolUser -DisplayName "Caleb Sills" -FirstName Caleb -LastName Sills -UserPrincipalName calebs@contoso.onmicrosoft.com -UsageLocation US -LicenseAssignment contoso:ENTERPRISEPACK
```

## <a name="use-office-365-powershell-to-create-multiple-user-accounts"></a><span data-ttu-id="570dd-150">使用 Office 365 PowerShell 创建多个用户帐户</span><span class="sxs-lookup"><span data-stu-id="570dd-150">Use Office 365 PowerShell to create multiple user accounts</span></span>

1. <span data-ttu-id="570dd-p109">创建包含所需用户帐户信息的以逗号分隔值 (CSV) 文件。例如：</span><span class="sxs-lookup"><span data-stu-id="570dd-p109">Create a comma-separated value (CSV) file that contains the required user account information. For example:</span></span>
    
  ```
  UserPrincipalName,FirstName,LastName,DisplayName,UsageLocation,AccountSkuId
ClaudeL@contoso.onmicrosoft.com,Claude,Loiselle,Claude Loiselle,US,contoso:ENTERPRISEPACK
LynneB@contoso.onmicrosoft.com,Lynne,Baxter,Lynne Baxter,US,contoso:ENTERPRISEPACK
ShawnM@contoso.onmicrosoft.com,Shawn,Melendez,Shawn Melendez,US,contoso:ENTERPRISEPACK
  ```

 > [!NOTE]
><span data-ttu-id="570dd-153">列名和它们的 CSV 文件的第一行中的顺序是任意的但请确保该文件的其余部分中的数据相匹配的列名称的顺序和在 Office 365 PowerShell 命令中使用的参数值的列名称。</span><span class="sxs-lookup"><span data-stu-id="570dd-153">The column names and their order in the first row of the CSV file are arbitrary, but make sure the data in the rest of the file matches the order of the column names, and use the column names for the parameter values in the Office 365 PowerShell command.</span></span>
    
2. <span data-ttu-id="570dd-154">使用以下语法：</span><span class="sxs-lookup"><span data-stu-id="570dd-154">Use the following syntax:</span></span>
    
  ```
  Import-Csv -Path <Input CSV File Path and Name> | foreach {New-MsolUser -DisplayName $_.DisplayName -FirstName $_.FirstName -LastName $_.LastName -UserPrincipalName $_.UserPrincipalName -UsageLocation $_.UsageLocation -LicenseAssignment $_.AccountSkuId [-Password $_.Password]} | Export-Csv -Path <Output CSV File Path and Name>
  ```

<span data-ttu-id="570dd-155">本示例从名为 C:\My Documents\NewAccounts.csv 的文件创建用户帐户，并将结果记录在名为 C:\My Documents\NewAccountResults.csv 的文件中</span><span class="sxs-lookup"><span data-stu-id="570dd-155">This example creates the user accounts from the file named C:\My Documents\NewAccounts.csv, and logs the results in the file named C:\My Documents\NewAccountResults.csv</span></span>
    
  ```
  Import-Csv -Path "C:\My Documents\NewAccounts.csv" | foreach {New-MsolUser -DisplayName $_.DisplayName -FirstName $_.FirstName -LastName $_.LastName -UserPrincipalName $_.UserPrincipalName -UsageLocation $_.UsageLocation -LicenseAssignment $_.AccountSkuId} | Export-Csv -Path "C:\My Documents\NewAccountResults.csv"
  ```

3. <span data-ttu-id="570dd-p110">查看输出文件以查看结果。我们没有指定密码，以便在输出文件中显示生成的随机密码。</span><span class="sxs-lookup"><span data-stu-id="570dd-p110">Review the output file to see the results. We didn't specify passwords, so the random passwords that were generated are visible in the output file.</span></span>
    
## <a name="use-the-azure-active-directory-v2-powershell-module-to-create-individual-user-accounts"></a><span data-ttu-id="570dd-158">使用 Azure Active Directory V2 PowerShell 模块创建个人用户帐户</span><span class="sxs-lookup"><span data-stu-id="570dd-158">Use the Azure Active Directory V2 PowerShell module to create individual user accounts</span></span>

<span data-ttu-id="570dd-p111">若要使用**New AzureADUser** cmdlet 从 Azure 活动目录 V2 PowerShell 模块，必须首先连接到您的订购。有关说明，请参阅[使用 Azure 活动目录 V2 PowerShell 模块连接](https://go.microsoft.com/fwlink/?linkid=842218)。</span><span class="sxs-lookup"><span data-stu-id="570dd-p111">To use the **New-AzureADUser** cmdlet from the Azure Active Directory V2 PowerShell module, you must first connect to your subscription. For the instructions, see [Connect with the Azure Active Directory V2 PowerShell module](https://go.microsoft.com/fwlink/?linkid=842218).</span></span>
  
<span data-ttu-id="570dd-161">连接后，使用下列语法创建个人帐户：</span><span class="sxs-lookup"><span data-stu-id="570dd-161">After you have connected, use the following syntax to create an individual account:</span></span>
  
```
$PasswordProfile=New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
$PasswordProfile.Password="<user account password>"
New-AzureADUser -DisplayName <DisplayName> -GivenName <FirstName> -SurName <LastName> -UserPrincipalName <Account> -UsageLocation <CountryCode> -MailNickName <mailbox name> -PasswordProfile $PasswordProfile -AccountEnabled $true
```

<span data-ttu-id="570dd-162">本示例为名为 Caleb Sills 的美国用户创建一个帐户：</span><span class="sxs-lookup"><span data-stu-id="570dd-162">This example creates an account for the United States user named Caleb Sills:</span></span>
  
```
$PasswordProfile=New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
$PasswordProfile.Password="3Rv0y1q39/chsy"
New-AzureADUser -DisplayName "Caleb Sills" -GivenName "Caleb" -SurName "Sills" -UserPrincipalName calebs@contoso.onmicrosoft.com -UsageLocation US -MailNickName calebs -PasswordProfile $PasswordProfile -AccountEnabled $true
```
  
## <a name="see-also"></a><span data-ttu-id="570dd-163">See also</span><span class="sxs-lookup"><span data-stu-id="570dd-163">See also</span></span>

<span data-ttu-id="570dd-164">这些有关管理用户使用 Office 365 PowerShell 的其他主题，请参阅：</span><span class="sxs-lookup"><span data-stu-id="570dd-164">See these additional topics about managing users with Office 365 PowerShell:</span></span>
  
- [<span data-ttu-id="570dd-165">使用 Office 365 PowerShell 删除和还原用户账户</span><span class="sxs-lookup"><span data-stu-id="570dd-165">Delete and restore user accounts with Office 365 PowerShell</span></span>](delete-and-restore-user-accounts-with-office-365-powershell.md)
    
- [<span data-ttu-id="570dd-166">使用 Office 365 PowerShell 冻结用户账户</span><span class="sxs-lookup"><span data-stu-id="570dd-166">Block user accounts with Office 365 PowerShell</span></span>](block-user-accounts-with-office-365-powershell.md)
    
- [<span data-ttu-id="570dd-167">使用 Office 365 PowerShell 向用户帐户分配许可证</span><span class="sxs-lookup"><span data-stu-id="570dd-167">Assign licenses to user accounts with Office 365 PowerShell</span></span>](assign-licenses-to-user-accounts-with-office-365-powershell.md)
    
- [<span data-ttu-id="570dd-168">使用 Office 365 PowerShell 删除用户帐户的许可证</span><span class="sxs-lookup"><span data-stu-id="570dd-168">Remove licenses from user accounts with Office 365 PowerShell</span></span>](remove-licenses-from-user-accounts-with-office-365-powershell.md)
    
<span data-ttu-id="570dd-169">有关在这些步骤中使用的 cmdlet 的详细信息，请参阅下列主题：</span><span class="sxs-lookup"><span data-stu-id="570dd-169">For more information about the cmdlets that are used in these procedures, see the following topics:</span></span>
  
- [<span data-ttu-id="570dd-170">Export-Csv</span><span class="sxs-lookup"><span data-stu-id="570dd-170">Export-Csv</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=113299)
    
- [<span data-ttu-id="570dd-171">Import-Csv</span><span class="sxs-lookup"><span data-stu-id="570dd-171">Import-Csv</span></span>](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-csv)
    
- [<span data-ttu-id="570dd-172">新 MsolUser</span><span class="sxs-lookup"><span data-stu-id="570dd-172">New-MsolUser</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=691547)
    
- [<span data-ttu-id="570dd-173">ForEach 对象</span><span class="sxs-lookup"><span data-stu-id="570dd-173">ForEach-Object</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=113300)
    
- [<span data-ttu-id="570dd-174">新 AzureADUser</span><span class="sxs-lookup"><span data-stu-id="570dd-174">New-AzureADUser</span></span>](https://docs.microsoft.com/powershell/module/azuread/new-azureaduser?view=azureadps-2.0)
    
