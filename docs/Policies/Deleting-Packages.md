---
title: "nuget.org から NuGet パッケージを削除する | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "nuget.org の一覧からパッケージを削除するポリシーです。パッケージが他のポリシーに違反しない限り、完全な削除はサポートされません。"
keywords: "NuGet パッケージの削除、NuGet パッケージを一覧から削除、パッケージ使用の禁止事項"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6169e46e55176757bc1ad471a3d80885cb50e403
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="deleting-packages"></a><span data-ttu-id="4f832-104">パッケージの削除</span><span class="sxs-lookup"><span data-stu-id="4f832-104">Deleting packages</span></span>

<span data-ttu-id="4f832-105">nuget.org では、パッケージの完全な削除はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="4f832-105">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="4f832-106">この操作を行うには、パッケージの機能に応じて、特にパッケージの復元を含むビルドのワークフローで、すべてのプロジェクトを中断します。</span><span class="sxs-lookup"><span data-stu-id="4f832-106">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="4f832-107">nuget.org では、Web サイト上のパッケージ管理ページで実行できる、パッケージの*一覧からの削除*はサポートされません。</span><span class="sxs-lookup"><span data-stu-id="4f832-107">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="4f832-108">一覧から削除されたパッケージは、nuget.org または Visual Studio UI に表示されません。また、検索結果にも表示されません。</span><span class="sxs-lookup"><span data-stu-id="4f832-108">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="4f832-109">ただし、一覧から削除されたパッケージは、引き続きパッケージの復元をサポートする正確なバージョン番号を使用し、ダウンロードしてインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="4f832-109">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="4f832-110">さらに、一覧から削除されたパッケージは、次の特定のシナリオで引き続き検出される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4f832-110">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="4f832-111">バージョンまたは依存関係の制約を満たす使用できる最新パッケージが一覧から削除されたパッケージの場合の、最新バージョンを使用したパッケージの復元 (例: `1.0.0-*`)。</span><span class="sxs-lookup"><span data-stu-id="4f832-111">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="4f832-112">(カタログに一覧から削除されたパッケージも含まれるように) カタログを使用したパッケージのレプリケーション。</span><span class="sxs-lookup"><span data-stu-id="4f832-112">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="4f832-113">例外</span><span class="sxs-lookup"><span data-stu-id="4f832-113">Exceptions</span></span>

<span data-ttu-id="4f832-114">著作権侵害や問題を起こす可能性のあるコンテンツなどの例外状況では、パッケージは NuGet チームによって手動で削除することができます。</span><span class="sxs-lookup"><span data-stu-id="4f832-114">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="4f832-115">このプロセスを開始するには、[NuGet ギャラリー](http://www.nuget.org)からサポート リクエストを送信します。</span><span class="sxs-lookup"><span data-stu-id="4f832-115">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="4f832-116">禁止事項</span><span class="sxs-lookup"><span data-stu-id="4f832-116">Prohibited use</span></span>

<span data-ttu-id="4f832-117">次のいずれかの基準を満たすパッケージは、パブリック NuGet ギャラリー上で許可されません。また、そのようなパッケージは、ディスカッションされることなく、すぐに削除されます。</span><span class="sxs-lookup"><span data-stu-id="4f832-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="4f832-118">ただし、パッケージの所有者は、削除の通知を受けます。</span><span class="sxs-lookup"><span data-stu-id="4f832-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="4f832-119">マルウェア、アドウェア、またはあらゆる種類のスパイウェアが含まれる</span><span class="sxs-lookup"><span data-stu-id="4f832-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="4f832-120">開発者のワークステーションまたは組織に損害を与えるように設計されている</span><span class="sxs-lookup"><span data-stu-id="4f832-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="4f832-121">著作権を侵害したり、ライセンスに違反したりしている</span><span class="sxs-lookup"><span data-stu-id="4f832-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="4f832-122">違法なコンテンツを含む</span><span class="sxs-lookup"><span data-stu-id="4f832-122">Contains illegal content.</span></span>
- <span data-ttu-id="4f832-123">生産性のないコンテンツを含むパッケージなど、パッケージの識別子を占拠するために使用されている。</span><span class="sxs-lookup"><span data-stu-id="4f832-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="4f832-124">パッケージにコードが含まれるか、所有者が実際に出荷する製品を所有しているユーザーに識別子を譲る必要があります。</span><span class="sxs-lookup"><span data-stu-id="4f832-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="4f832-125">ギャラリーで明示的に実行するように設計されていない操作を行うようにしている。</span><span class="sxs-lookup"><span data-stu-id="4f832-125">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="4f832-126">これらの項目のいずれかに違反しているパッケージを見つけた場合は、パッケージの詳細ページで **[不正使用を報告]** リンクをクリックして、レポートを送信します。</span><span class="sxs-lookup"><span data-stu-id="4f832-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="4f832-127">NuGet チームと .NET Foundation は、いつでもこれらの条件を変更する権利を保有することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4f832-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
