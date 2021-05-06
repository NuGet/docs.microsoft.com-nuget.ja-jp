---
title: NuGet.org の概要
description: NuGet.org の概要
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901877"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="960a5-103">NuGet.org の概要</span><span class="sxs-lookup"><span data-stu-id="960a5-103">Overview of NuGet.org</span></span>

<span data-ttu-id="960a5-104">NuGet.org は毎日数百万の .NET および .NET Core 開発者に採用されている NuGet パッケージのパブリック ホストです。</span><span class="sxs-lookup"><span data-stu-id="960a5-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="960a5-105">NuGet エコシステムでの NuGet.org の役割</span><span class="sxs-lookup"><span data-stu-id="960a5-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="960a5-106">NuGet.org 自体にパブリック ホストとしての役割があり、100,000 を超える個別パッケージの中央リポジトリが [nuget.org](https://www.nuget.org) に保持されています。NuGet.org はパッケージ用の唯一のホストではありません。</span><span class="sxs-lookup"><span data-stu-id="960a5-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="960a5-107">また、NuGet テクノロジを使用すると、クラウド (Azure DevOps 上など)、プライベート ネットワーク、さらにはご利用のローカル ファイル システムで、プライベートにパッケージをホストすることもできます。</span><span class="sxs-lookup"><span data-stu-id="960a5-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="960a5-108">別のホストまたはホスティング オプションに関心がある場合は、「[独自の NuGet フィードをホスティングする](../hosting-packages/overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="960a5-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="960a5-109">NuGet.org は、NuGet パッケージの他のホストと同様に、パッケージの "*作成者*" とパッケージの "*コンシューマー*" の間の接続ポイントとして機能します。</span><span class="sxs-lookup"><span data-stu-id="960a5-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="960a5-110">作成者は便利な NuGet パッケージを作成して公開します。</span><span class="sxs-lookup"><span data-stu-id="960a5-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="960a5-111">利用者は、アクセスできるホストで役に立ち互換性のあるパッケージを検索し、ダウンロードしてプロジェクトに組み込みます。</span><span class="sxs-lookup"><span data-stu-id="960a5-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="960a5-112">プロジェクトにインストールされたパッケージの API は、プロジェクト コードの他の部分から利用できます。</span><span class="sxs-lookup"><span data-stu-id="960a5-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![パッケージ作成者、パッケージ ホスト、パッケージ利用者の間の関係](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="960a5-114">[アカウント]</span><span class="sxs-lookup"><span data-stu-id="960a5-114">Accounts</span></span>

<span data-ttu-id="960a5-115">NuGet.org 上でパッケージを公開するには、まず[個人 (ユーザー) アカウント](individual-accounts.md)を作成します。</span><span class="sxs-lookup"><span data-stu-id="960a5-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="960a5-116">これが NuGet.org でのお客様の ID になります。</span><span class="sxs-lookup"><span data-stu-id="960a5-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="960a5-117">NuGet.org では[組織アカウント](organizations-on-nuget-org.md)を作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="960a5-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="960a5-118">組織アカウントには、そのメンバーとして 1 つまたは複数の個人アカウントが含まれます。</span><span class="sxs-lookup"><span data-stu-id="960a5-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="960a5-119">メンバーは、所有権用の単一の ID を維持しながら一連のパッケージを管理することができます。</span><span class="sxs-lookup"><span data-stu-id="960a5-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="960a5-120">ご自分の個人アカウントによって、任意の数の組織のメンバーになることができます。</span><span class="sxs-lookup"><span data-stu-id="960a5-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="960a5-121">パッケージは、個人アカウントに属することができるのと同様に、組織アカウントに属することもできます。</span><span class="sxs-lookup"><span data-stu-id="960a5-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="960a5-122">パッケージ コンシューマーには、個人アカウントと組織アカウントの違いは表示されません。どちらもパッケージ `owners` として表示されます。</span><span class="sxs-lookup"><span data-stu-id="960a5-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="960a5-123">API キー</span><span class="sxs-lookup"><span data-stu-id="960a5-123">API keys</span></span>

<span data-ttu-id="960a5-124">公開する NuGet パッケージ (*.nupkg* ファイル) の用意ができたら、nuget.exe CLI または dotnet.exe CLI のいずれかと、NuGet.org から取得した [API キー](scoped-api-keys.md)を使用して、パッケージを NuGet.org に公開します。</span><span class="sxs-lookup"><span data-stu-id="960a5-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="960a5-125">[パッケージを公開](../create-packages/creating-a-package.md)するときには、CLI コマンドに API キー値を含めます。</span><span class="sxs-lookup"><span data-stu-id="960a5-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="960a5-126">ID プレフィックス</span><span class="sxs-lookup"><span data-stu-id="960a5-126">ID prefixes</span></span>

<span data-ttu-id="960a5-127">パッケージを公開するときには、[ID プレフィックスを予約](id-prefix-reservation.md)することにより、ご自分の ID を予約し保護することができます。</span><span class="sxs-lookup"><span data-stu-id="960a5-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="960a5-128">パッケージをインストールするとき、パッケージのコンシューマーには、ご使用になるパッケージが詐欺的なものでないことをその識別プロパティで示す追加情報が提供されます。</span><span class="sxs-lookup"><span data-stu-id="960a5-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="960a5-129">NuGet.org 用の API エンドポイント</span><span class="sxs-lookup"><span data-stu-id="960a5-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="960a5-130">NuGet クライアントで NuGet.org をパッケージ リポジトリとして使用するには、次の V3 API エンドポイントを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="960a5-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="960a5-131">より古いクライアントでは、引き続き V2 プロトコルを使用して NuGet.org に到達できます。ただし、V2 プロトコルを使用した場合、NuGet クライアント 3.0 以降でサービスの動作が遅くなり、信頼性が低下します。</span><span class="sxs-lookup"><span data-stu-id="960a5-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="960a5-132">`https://www.nuget.org/api/v2` (**V2 プロトコルは非推奨になっています**)</span><span class="sxs-lookup"><span data-stu-id="960a5-132">`https://www.nuget.org/api/v2` (**The V2 protocol is deprecated!**)</span></span>
