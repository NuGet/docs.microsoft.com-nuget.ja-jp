---
title: 個人アカウント
description: パッケージを公開するには、NuGet.org での個人アカウントが必要です
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427137"
---
# <a name="individual-accounts"></a><span data-ttu-id="00a0e-103">個人アカウント</span><span class="sxs-lookup"><span data-stu-id="00a0e-103">Individual accounts</span></span>

<span data-ttu-id="00a0e-104">NuGet.org でパッケージを公開して管理するには、個人アカウントを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="00a0e-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="00a0e-105">個人アカウントと組織アカウント</span><span class="sxs-lookup"><span data-stu-id="00a0e-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="00a0e-106">個人 (ユーザー) アカウントは NuGet.org での自分の ID であり、任意の数の組織のメンバーになることができます。</span><span class="sxs-lookup"><span data-stu-id="00a0e-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="00a0e-107">パッケージは、個人アカウントに属することができるのと同様に、組織アカウントに属することもできます。</span><span class="sxs-lookup"><span data-stu-id="00a0e-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="00a0e-108">パッケージ コンシューマーには、個人アカウントと組織アカウントの違いは表示されません。どちらもパッケージ `owners` として表示されます。</span><span class="sxs-lookup"><span data-stu-id="00a0e-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="00a0e-109">組織アカウントには、そのメンバーとして 1 つまたは複数の個人アカウントが含まれます。</span><span class="sxs-lookup"><span data-stu-id="00a0e-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="00a0e-110">これらのメンバーは、所有権用の単一の ID を維持しながら一連のパッケージを管理することができます。</span><span class="sxs-lookup"><span data-stu-id="00a0e-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="00a0e-111">新しい個人アカウントを追加する</span><span class="sxs-lookup"><span data-stu-id="00a0e-111">Add a new individual account</span></span>

<span data-ttu-id="00a0e-112">NuGet.org アカウントを作成するには、個人の Microsoft アカウント (MSA) または Azure Active Directory (AAD) アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="00a0e-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="00a0e-113">nuget.org アカウントをお持ちでない場合は、[作成](https://signup.live.com)できます。</span><span class="sxs-lookup"><span data-stu-id="00a0e-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="00a0e-114">MSA アカウントまたは AAD アカウントがある場合は、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="00a0e-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="00a0e-115">[NuGet.org のログイン ページ](https://www.nuget.org/users/account/LogOn)に移動します。</span><span class="sxs-lookup"><span data-stu-id="00a0e-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="00a0e-116">**[Sign in with Microsoft]\(Microsoft アカウントでサインイン\)** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="00a0e-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="00a0e-117">Microsoft アカウントまたは Azure Active Directory アカウントの詳細を入力します。</span><span class="sxs-lookup"><span data-stu-id="00a0e-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="00a0e-118">**[はい]** をクリックして、*NuGet.org* アプリケーションにアクセス許可を与えることに同意してください。</span><span class="sxs-lookup"><span data-stu-id="00a0e-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![NuGet.org へのアクセス許可の付与](media/nuget-org-permissions.png)

1. <span data-ttu-id="00a0e-120">*nuget.org* にリダイレクトされ、ユーザー名を登録するように求められます。</span><span class="sxs-lookup"><span data-stu-id="00a0e-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="00a0e-121">入力ボックスに、ユーザー名を指定します。</span><span class="sxs-lookup"><span data-stu-id="00a0e-121">Specify the username in the input box.</span></span> <span data-ttu-id="00a0e-122">ユーザー名は大文字と小文字が**区別され**、後から変更できないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="00a0e-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![NuGet.org でユーザー名を指定する](media/nuget-org-register.png) 

1. <span data-ttu-id="00a0e-124">**[Register]\(登録\)** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="00a0e-124">Click the **Register** button.</span></span>

<span data-ttu-id="00a0e-125">これで NuGet.org アカウントが作成されました。</span><span class="sxs-lookup"><span data-stu-id="00a0e-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="00a0e-126">[アカウント設定](https://www.nuget.org/account)ページで、アカウントの管理を実行できます。</span><span class="sxs-lookup"><span data-stu-id="00a0e-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
