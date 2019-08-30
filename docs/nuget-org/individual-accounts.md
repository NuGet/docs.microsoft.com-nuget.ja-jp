---
title: 個人アカウント - NuGet.org
description: パッケージを公開するには、NuGet.org での個人アカウントが必要です
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 63c6b5eb5ad635e436b4d53a5f833af35f72d76f
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999975"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="2a66b-103">NuGet.org での個人アカウント</span><span class="sxs-lookup"><span data-stu-id="2a66b-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="2a66b-104">NuGet.org でパッケージを公開して管理するには、個人アカウントを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a66b-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="2a66b-105">個人アカウントと組織アカウント</span><span class="sxs-lookup"><span data-stu-id="2a66b-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="2a66b-106">個人 (ユーザー) アカウントは NuGet.org での自分の ID であり、任意の数の組織のメンバーになることができます。</span><span class="sxs-lookup"><span data-stu-id="2a66b-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="2a66b-107">パッケージは、個人アカウントに属することができるのと同様に、組織アカウントに属することもできます。</span><span class="sxs-lookup"><span data-stu-id="2a66b-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="2a66b-108">パッケージ コンシューマーには、個人アカウントと組織アカウントの違いは表示されません。どちらもパッケージ `owners` として表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a66b-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="2a66b-109">組織アカウントには、そのメンバーとして 1 つまたは複数の個人アカウントが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2a66b-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="2a66b-110">これらのメンバーは、所有権用の単一の ID を維持しながら一連のパッケージを管理することができます。</span><span class="sxs-lookup"><span data-stu-id="2a66b-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="2a66b-111">新しい個人アカウントを追加する</span><span class="sxs-lookup"><span data-stu-id="2a66b-111">Add a new individual account</span></span>

<span data-ttu-id="2a66b-112">NuGet.org アカウントを作成するには、個人の Microsoft アカウント (MSA) または Azure Active Directory (AAD) アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="2a66b-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="2a66b-113">nuget.org アカウントをお持ちでない場合は、[作成](https://signup.live.com)できます。</span><span class="sxs-lookup"><span data-stu-id="2a66b-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="2a66b-114">MSA アカウントまたは AAD アカウントがある場合は、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="2a66b-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="2a66b-115">[NuGet.org のログイン ページ](https://www.nuget.org/users/account/LogOn)に移動します。</span><span class="sxs-lookup"><span data-stu-id="2a66b-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="2a66b-116">**[Sign in with Microsoft]\(Microsoft アカウントでサインイン\)** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="2a66b-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="2a66b-117">Microsoft アカウントまたは Azure Active Directory アカウントの詳細を入力します。</span><span class="sxs-lookup"><span data-stu-id="2a66b-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="2a66b-118">**[はい]** をクリックして、*NuGet.org* アプリケーションにアクセス許可を与えることに同意してください。</span><span class="sxs-lookup"><span data-stu-id="2a66b-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![NuGet.org へのアクセス許可の付与](media/nuget-org-permissions.png)

1. <span data-ttu-id="2a66b-120">*nuget.org* にリダイレクトされ、ユーザー名を登録するように求められます。</span><span class="sxs-lookup"><span data-stu-id="2a66b-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="2a66b-121">入力ボックスに、ユーザー名を指定します。</span><span class="sxs-lookup"><span data-stu-id="2a66b-121">Specify the username in the input box.</span></span> <span data-ttu-id="2a66b-122">ユーザー名は大文字と小文字が**区別され**、後から変更できないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2a66b-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![NuGet.org でユーザー名を指定する](media/nuget-org-register.png) 

1. <span data-ttu-id="2a66b-124">**[Register]\(登録\)** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="2a66b-124">Click the **Register** button.</span></span>

<span data-ttu-id="2a66b-125">これで NuGet.org アカウントが作成されました。</span><span class="sxs-lookup"><span data-stu-id="2a66b-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="2a66b-126">[アカウント設定](https://www.nuget.org/account)ページで、アカウントの管理を実行できます。</span><span class="sxs-lookup"><span data-stu-id="2a66b-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="2a66b-127">2 要素認証を有効にする (2FA)</span><span class="sxs-lookup"><span data-stu-id="2a66b-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="2a66b-128">アカウントの保護を強化するには、2 要素認証を有効にします (推奨)。</span><span class="sxs-lookup"><span data-stu-id="2a66b-128">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="2a66b-129">アカウントにログインしたら、プロファイルを開き、 **[ログイン アカウント]** で **[有効にする]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2a66b-129">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![2FA を有効にする](media/nuget-org-register-2fa.png)

   <span data-ttu-id="2a66b-131">*nuget.org* への次回サインイン時に追加の資格情報の入力を求められることを示すメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2a66b-131">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="2a66b-132">この時点で認証を完了するには、サインアウトしてからもう一度サインインします。</span><span class="sxs-lookup"><span data-stu-id="2a66b-132">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="2a66b-133">サインインする際に、2 番目の認証形式としてテキストまたは電子メールを選択します。</span><span class="sxs-lookup"><span data-stu-id="2a66b-133">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="2a66b-134">Microsoft アカウントに既に関連付けられている電話番号または電子メールを確認します。</span><span class="sxs-lookup"><span data-stu-id="2a66b-134">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="2a66b-135">アカウントの新しい電話番号または電子メール アドレスを入力する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="2a66b-135">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="2a66b-136">その場合は、指示に従って必要な情報を入力し、 **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2a66b-136">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![2FA を有効にする](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="2a66b-138">デバイスまたは電子メールアカウントを確認し、先ほど送信したコードを入力します。</span><span class="sxs-lookup"><span data-stu-id="2a66b-138">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![2FA を有効にする](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="2a66b-140">追加の指示に従って、2 要素認証を完了します。</span><span class="sxs-lookup"><span data-stu-id="2a66b-140">Follow any additional instructions to complete Two-factor authentication.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="2a66b-141">NuGet.org アカウントを削除する</span><span class="sxs-lookup"><span data-stu-id="2a66b-141">Delete a NuGet.org account</span></span>

<span data-ttu-id="2a66b-142">NuGet.org アカウントの削除など、アカウント関連のその他のタスクについては、「[NuGet.org のアカウント管理](nuget-org-faq.md#nugetorg-account-management)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2a66b-142">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
