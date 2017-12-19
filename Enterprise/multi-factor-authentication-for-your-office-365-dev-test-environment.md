---
title: "Office 365 开发/测试环境的多重身份验证"
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
- Ent_O365_Top
ms.custom:
- DecEntMigration
- mar17entnews
- TLG
- Ent_TLGs
ms.assetid: e2b354b9-7f18-4da0-9107-6245eae0f33f
description: "摘要： 配置使用文本消息发送到 Office 365 的开发/测试环境中的智能电话的多因素身份验证。"
ms.openlocfilehash: 87fdcc2ccd910e8da399e14d37fe3d0d1f0a66d4
ms.sourcegitcommit: d31cf57295e8f3d798ab971d405baf3bd3eb7a45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2017
---
# <a name="multi-factor-authentication-for-your-office-365-devtest-environment"></a><span data-ttu-id="e2498-103">Office 365 开发/测试环境的多重身份验证</span><span class="sxs-lookup"><span data-stu-id="e2498-103">Multi-factor authentication for your Office 365 dev/test environment</span></span>

 <span data-ttu-id="e2498-104">**摘要：**配置使用文本消息发送到智能手机在 Office 365 的开发/测试环境中的多因素身份验证。</span><span class="sxs-lookup"><span data-stu-id="e2498-104">**Summary:** Configure multi-factor authentication using text messages sent to a smart phone in an Office 365 dev/test environment.</span></span>
  
<span data-ttu-id="e2498-p101">对于登录 Office 365 订阅的其他安全级别，可以启用 Azure 多重身份验证，这需要使用用户名和密码之外的其他内容来验证帐户。使用适用于 Office 365 的多重身份验证时，用户需要在正确输入密码后确认智能手机上的电话呼叫、键入通过短信发送的验证码或指定应用密码。仅在满足第二个身份验证因素时才能登录。 </span><span class="sxs-lookup"><span data-stu-id="e2498-p101">For an additional level of security for signing in to your Office 365 subscription, you can enable Azure multi-factor authentication, which requires more than just a username and password to verify an account. With multi-factor authentication for Office 365, users are required to acknowledge a phone call, type a verification code sent in a text message, or specify an app password on their smart phones after correctly entering their passwords. They can sign in only after this second authentication factor has been satisfied.</span></span> 
  
<span data-ttu-id="e2498-108">本文介绍如何为特定 Office 365 帐户启用和测试基于短信的身份验证。</span><span class="sxs-lookup"><span data-stu-id="e2498-108">This article describes how to enable and test text message-based authentication for a specific Office 365 account.</span></span>
  
<span data-ttu-id="e2498-109">在开发/测试环境中，设置 Office 365 多重身份验证包含两个阶段：</span><span class="sxs-lookup"><span data-stu-id="e2498-109">There are two phases to setting up multi-factor authentication for Office 365 in a dev/test environment:</span></span>
  
1. <span data-ttu-id="e2498-110">创建 Office 365 开发/测试环境。</span><span class="sxs-lookup"><span data-stu-id="e2498-110">Create the Office 365 dev/test environment.</span></span>
    
2. <span data-ttu-id="e2498-111">为 User 2 帐户启用并测试多重身份验证。</span><span class="sxs-lookup"><span data-stu-id="e2498-111">Enable and test multi-factor authentication for the User 2 account.</span></span>
    
> [!TIP]
> <span data-ttu-id="e2498-112">单击[此处](http://aka.ms/catlgstack)为可视化映射到一个 Microsoft 云测试实验室指南堆栈中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="e2498-112">Click [here](http://aka.ms/catlgstack) for a visual map to all the articles in the One Microsoft Cloud Test Lab Guide stack.</span></span>
  
## <a name="phase-1-build-out-your-lightweight-or-simulated-enterprise-office-365-devtest-environment"></a><span data-ttu-id="e2498-113">第 1 阶段：构建轻型或模拟的企业 Office 365 开发/测试环境</span><span class="sxs-lookup"><span data-stu-id="e2498-113">Phase 1: Build out your lightweight or simulated enterprise Office 365 dev/test environment</span></span>

<span data-ttu-id="e2498-114">如果您只是想要测试中达到最低要求的轻量方法的多因素身份验证，则按照在阶段 2 和 3 的[Office 365 的开发/测试环境](office-365-dev-test-environment.md)的说明。</span><span class="sxs-lookup"><span data-stu-id="e2498-114">If you just want to test multi-factor authentication in a lightweight way with the minimum requirements, follow the instructions in phases 2 and 3 of [Office 365 dev/test environment](office-365-dev-test-environment.md).</span></span>
  
<span data-ttu-id="e2498-115">如果您想要测试中模拟企业的多因素身份验证，请按[您 Office 365 的开发/测试环境的目录同步](dirsync-for-your-office-365-dev-test-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="e2498-115">If you want to test multi-factor authentication in a simulated enterprise, follow the instructions in [DirSync for your Office 365 dev/test environment](dirsync-for-your-office-365-dev-test-environment.md).</span></span>
  
> [!NOTE]
> <span data-ttu-id="e2498-p102">测试多重身份验证不需要模拟的企业开发/测试环境，该环境中包括连接到 Internet 的模拟内部网和 Windows Server AD 林的目录同步。它在此处作为一个选项提供，以便你可以测试多重身份验证，并在代表典型组织的环境中对其进行试验。</span><span class="sxs-lookup"><span data-stu-id="e2498-p102">Testing multi-factor authentication does not require the simulated enterprise dev/test environment, which includes a simulated intranet connected to the Internet and directory synchronization for a Windows Server AD forest. It is provided here as an option so that you can test multi-factor authentication and experiment with it in an environment that represents a typical organization.</span></span> 
  
## <a name="phase-2-enable-and-test-multi-factor-authentication-for-the-user-2-account"></a><span data-ttu-id="e2498-118">阶段 2：启用和测试 User 2 帐户的多重身份验证</span><span class="sxs-lookup"><span data-stu-id="e2498-118">Phase 2: Enable and test multi-factor authentication for the User 2 account</span></span>

<span data-ttu-id="e2498-119">通过以下步骤为 User 2 帐户启用多重身份验证：</span><span class="sxs-lookup"><span data-stu-id="e2498-119">Enable multi-factor authentication for the User 2 account with these steps:</span></span>
  
1. <span data-ttu-id="e2498-120">打开一个单独的浏览器实例，请转到 Office 365 门户网站 ([https://portal.office.com](https://portal.office.com))，然后登录到您的 Office 365 试用预订使用全局管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="e2498-120">Open a separate instance of your browser, go to the Office 365 portal ([https://portal.office.com](https://portal.office.com)), and then sign in to your Office 365 trial subscription with your global administrator account.</span></span>
    
2. <span data-ttu-id="e2498-121">从主门户页面中，单击**管理**。</span><span class="sxs-lookup"><span data-stu-id="e2498-121">From the main portal page, click **Admin**.</span></span>
    
3. <span data-ttu-id="e2498-122">在左边的导航，请单击**用户 > 活动用户**。</span><span class="sxs-lookup"><span data-stu-id="e2498-122">In the left navigation, click **Users > Active users**.</span></span>
    
4. <span data-ttu-id="e2498-123">在活动用户窗格中，单击**更 > 设置 Azure 多因素身份验证**。</span><span class="sxs-lookup"><span data-stu-id="e2498-123">In the Active users pane, click **More > Setup Azure multi-factor auth**.</span></span>
    
5. <span data-ttu-id="e2498-124">在列表中，单击**用户 2**帐户。</span><span class="sxs-lookup"><span data-stu-id="e2498-124">In the list, click the **User 2** account.</span></span>
    
6. <span data-ttu-id="e2498-125">在**用户 2**部分下**快速步骤**中, 单击**启用**。</span><span class="sxs-lookup"><span data-stu-id="e2498-125">In the **User 2** section, under **Quick steps**, click **Enable**.</span></span>
    
7. <span data-ttu-id="e2498-126">**有关启用多因素身份验证**对话框中，单击**启用多因素身份验证**。</span><span class="sxs-lookup"><span data-stu-id="e2498-126">In the **About enabling multi-factor auth** dialog box, click **Enable multi-factor auth**.</span></span>
    
8. <span data-ttu-id="e2498-127">在**更新成功**对话框中，单击**关闭**。</span><span class="sxs-lookup"><span data-stu-id="e2498-127">In the **Update successful** dialog box, click **Close**.</span></span>
    
9. <span data-ttu-id="e2498-128">**Microsoft Office 主页**选项卡上，单击右上方的用户帐户图标，然后单击**注销**。</span><span class="sxs-lookup"><span data-stu-id="e2498-128">On the **Microsoft Office Home** tab, click the user account icon in the upper right, and then click **Sign out**.</span></span>
    
10. <span data-ttu-id="e2498-129">关闭浏览器实例。</span><span class="sxs-lookup"><span data-stu-id="e2498-129">Close your browser instance.</span></span>
    
<span data-ttu-id="e2498-130">完成 User 2 帐户的配置，通过以下步骤，使用短信对其进行验证和测试：</span><span class="sxs-lookup"><span data-stu-id="e2498-130">Complete the configuration for the User 2 account to use a text message for validation and test it with these steps:</span></span>
  
1. <span data-ttu-id="e2498-131">打开浏览器的新实例。</span><span class="sxs-lookup"><span data-stu-id="e2498-131">Open a new instance of your browser.</span></span>
    
2. <span data-ttu-id="e2498-132">请转到 Office 365 门户网站 ([https://portal.office.com](https://portal.office.com)) 和登录用户 2 帐户 (用户 @ 2\<组织名称 >。 onmicrosoft.com) 和密码。</span><span class="sxs-lookup"><span data-stu-id="e2498-132">Go to the Office 365 portal ([https://portal.office.com](https://portal.office.com)) and sign in with the User 2 account (user2@\<organization name>.onmicrosoft.com) and password.</span></span>
    
3. <span data-ttu-id="e2498-p103">登录后，您可以设置额外的安全验证的帐户。单击**立即设置**。</span><span class="sxs-lookup"><span data-stu-id="e2498-p103">After signing in, you are prompted to set up the account for additional security validation. Click **Set it up now**.</span></span>
    
4. <span data-ttu-id="e2498-135">在**更高的安全性验证**页上：</span><span class="sxs-lookup"><span data-stu-id="e2498-135">On the **Additional security verification** page:</span></span>
    
  - <span data-ttu-id="e2498-136">选择你所在的国家或地区。</span><span class="sxs-lookup"><span data-stu-id="e2498-136">Select your country or region.</span></span>
    
  - <span data-ttu-id="e2498-137">键入接收短信的智能手机的电话号码。</span><span class="sxs-lookup"><span data-stu-id="e2498-137">Type phone number of the smart phone that will receive text messages.</span></span>
    
  - <span data-ttu-id="e2498-138">选择**向我发送文本消息的代码**。</span><span class="sxs-lookup"><span data-stu-id="e2498-138">Select **Send me a code by text message**.</span></span>
    
5. <span data-ttu-id="e2498-139">单击**我的联系人**。</span><span class="sxs-lookup"><span data-stu-id="e2498-139">Click **Contact me**.</span></span>
    
6. <span data-ttu-id="e2498-140">从智能手机上收到的短信输入验证码，然后单击**验证**。</span><span class="sxs-lookup"><span data-stu-id="e2498-140">Enter the verification code from the text message received on your smart phone, and then click **Verify**.</span></span>
    
7. <span data-ttu-id="e2498-141">在**第 3 步： 保留现有的应用程序**页上，在一个安全的位置，记录用户 2 帐户的显示应用程序密码，然后单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="e2498-141">On the **Step 3: Keep your existing applications** page, record the displayed app password for the User 2 account in a secure location, and then click **Done**.</span></span>
    
8. <span data-ttu-id="e2498-142">重新打开登录页中，键入用户 2 帐户的密码，然后单击**登录**。</span><span class="sxs-lookup"><span data-stu-id="e2498-142">Back on the sign-in page, type the password for the User 2 account and click **Sign in**.</span></span>
    
9. <span data-ttu-id="e2498-143">从智能手机上收到的短信输入验证码，然后单击**登录**。</span><span class="sxs-lookup"><span data-stu-id="e2498-143">Enter the verification code from the text message received on your smart phone, and then click **Sign in**.</span></span>
    
10. <span data-ttu-id="e2498-p104">如果是第一次您登录用户 2 帐户，系统会提示您更改密码。两次，输入原密码和新密码，然后单击**更新密码并登录**。在一个安全的位置中记录新的密码。</span><span class="sxs-lookup"><span data-stu-id="e2498-p104">If this is the first time you signed in with the User 2 account, you are prompted to change the password. Type the original password and a new password twice, and then click **Update password and sign in**. Record the new password in a secure location.</span></span>
    
    <span data-ttu-id="e2498-147">应能看到 User 2 的 Office 365 门户。</span><span class="sxs-lookup"><span data-stu-id="e2498-147">You should see the Office 365 portal for User 2.</span></span>
    
## <a name="see-also"></a><span data-ttu-id="e2498-148">See Also</span><span class="sxs-lookup"><span data-stu-id="e2498-148">See Also</span></span>

[<span data-ttu-id="e2498-149">云采用测试实验室指南 (TLG)</span><span class="sxs-lookup"><span data-stu-id="e2498-149">Cloud adoption Test Lab Guides (TLGs)</span></span>](cloud-adoption-test-lab-guides-tlgs.md)
  
[<span data-ttu-id="e2498-150">基础配置开发/测试环境</span><span class="sxs-lookup"><span data-stu-id="e2498-150">Base Configuration dev/test environment</span></span>](base-configuration-dev-test-environment.md)
  
[<span data-ttu-id="e2498-151">Office 365 开发/测试环境</span><span class="sxs-lookup"><span data-stu-id="e2498-151">Office 365 dev/test environment</span></span>](office-365-dev-test-environment.md)
  
[<span data-ttu-id="e2498-152">云应用和混合解决方案</span><span class="sxs-lookup"><span data-stu-id="e2498-152">Cloud adoption and hybrid solutions</span></span>](cloud-adoption-and-hybrid-solutions.md)

[<span data-ttu-id="e2498-153">多因素身份验证对于 Office 365 的部署计划</span><span class="sxs-lookup"><span data-stu-id="e2498-153">Plan for multi-factor authentication for Office 365 Deployments</span></span>](https://support.office.com/article/Plan-for-multi-factor-authentication-for-Office-365-Deployments-043807b2-21db-4d5c-b430-c8a6dee0e6ba)
