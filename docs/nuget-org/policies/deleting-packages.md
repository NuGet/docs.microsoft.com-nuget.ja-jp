---
title: nuget.org から NuGet パッケージを削除する
description: nuget.org の一覧からパッケージを削除するポリシーです。パッケージが他のポリシーに違反しない限り、完全な削除はサポートされません。
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 574ee874e2d6555a2e3e0a0643962e33b7ec1b09
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859448"
---
# <a name="deleting-packages"></a><span data-ttu-id="5f68d-103">パッケージを削除する</span><span class="sxs-lookup"><span data-stu-id="5f68d-103">Deleting packages</span></span>

<span data-ttu-id="5f68d-104">nuget.org では、パッケージの完全な削除はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="5f68d-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="5f68d-105">この操作を行うには、パッケージの機能に応じて、特にパッケージの復元を含むビルドのワークフローで、すべてのプロジェクトを中断します。</span><span class="sxs-lookup"><span data-stu-id="5f68d-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="5f68d-106">nuget.org では、[パッケージの一覧からの削除](#unlisting-a-package)がサポートされています。これは Web サイトのパッケージ管理ページで行うことができます。</span><span class="sxs-lookup"><span data-stu-id="5f68d-106">nuget.org does support [unlisting a package](#unlisting-a-package), which can be done in the package management page on the web site.</span></span> <span data-ttu-id="5f68d-107">一覧から削除されたパッケージは、nuget.org または Visual Studio UI に表示されません。また、検索結果にも表示されません。</span><span class="sxs-lookup"><span data-stu-id="5f68d-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="5f68d-108">ただし、一覧から削除されたパッケージは、引き続きパッケージの復元をサポートする正確なバージョン番号を使用し、ダウンロードしてインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="5f68d-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="5f68d-109">さらに、一覧から削除されたパッケージは、次の特定のシナリオで引き続き検出される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5f68d-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="5f68d-110">バージョンまたは依存関係の制約を満たす使用できる最新パッケージが一覧から削除されたパッケージの場合の、最新バージョンを使用したパッケージの復元 (例: `1.0.0-*`)。</span><span class="sxs-lookup"><span data-stu-id="5f68d-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="5f68d-111">(カタログに一覧から削除されたパッケージも含まれるように) カタログを使用したパッケージのレプリケーション。</span><span class="sxs-lookup"><span data-stu-id="5f68d-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="5f68d-112">例外</span><span class="sxs-lookup"><span data-stu-id="5f68d-112">Exceptions</span></span>

<span data-ttu-id="5f68d-113">著作権侵害や問題を起こす可能性のあるコンテンツなどの例外状況では、パッケージは NuGet チームによって手動で削除することができます。</span><span class="sxs-lookup"><span data-stu-id="5f68d-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="5f68d-114">NuGet.org のパッケージ詳細ページで、[不正使用を報告] ボタンを使用してパッケージを報告することができます。</span><span class="sxs-lookup"><span data-stu-id="5f68d-114">You can report a package using the "Report abuse" button on the NuGet.org package details page.</span></span> <span data-ttu-id="5f68d-115">パッケージの所有者は、NuGet.org アカウントにログインし、NuGet.org パッケージ詳細ページの [Contact support]\(サポートへの問い合わせ\) ボタンを使用して NuGet サポートに連絡することができます。</span><span class="sxs-lookup"><span data-stu-id="5f68d-115">If you are the package owner, login to your NuGet.org account to reach NuGet support using the "Contact support" button on the NuGet.org package details page.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="5f68d-116">禁止事項</span><span class="sxs-lookup"><span data-stu-id="5f68d-116">Prohibited use</span></span>

<span data-ttu-id="5f68d-117">次のいずれかの基準を満たすパッケージは、パブリック NuGet ギャラリー上で許可されません。また、そのようなパッケージは、ディスカッションされることなく、すぐに削除されます。</span><span class="sxs-lookup"><span data-stu-id="5f68d-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="5f68d-118">ただし、パッケージの所有者は、削除の通知を受けます。</span><span class="sxs-lookup"><span data-stu-id="5f68d-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="5f68d-119">マルウェア、アドウェア、またはあらゆる種類のスパイウェアが含まれる</span><span class="sxs-lookup"><span data-stu-id="5f68d-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="5f68d-120">開発者のワークステーションまたは組織に損害を与えるように設計されている</span><span class="sxs-lookup"><span data-stu-id="5f68d-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="5f68d-121">著作権を侵害したり、ライセンスに違反したりしている</span><span class="sxs-lookup"><span data-stu-id="5f68d-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="5f68d-122">違法なコンテンツを含む</span><span class="sxs-lookup"><span data-stu-id="5f68d-122">Contains illegal content.</span></span>
- <span data-ttu-id="5f68d-123">生産性のないコンテンツを含むパッケージなど、パッケージの識別子を占拠するために使用されている。</span><span class="sxs-lookup"><span data-stu-id="5f68d-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="5f68d-124">パッケージにコードが含まれるか、所有者が実際に出荷する製品を所有しているユーザーに識別子を譲る必要があります。</span><span class="sxs-lookup"><span data-stu-id="5f68d-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="5f68d-125">ギャラリーで明示的に実行するように設計されていない操作を行うようにしている。</span><span class="sxs-lookup"><span data-stu-id="5f68d-125">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="5f68d-126">以上の違反項目に該当するパッケージを見つけた場合、パッケージ詳細ページの **[不正使用を報告]** リンクをクリックし、報告してください。</span><span class="sxs-lookup"><span data-stu-id="5f68d-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="5f68d-127">NuGet チームと .NET Foundation は、いつでもこれらの条件を変更する権利を保有することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5f68d-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>

## <a name="unlisting-a-package"></a><span data-ttu-id="5f68d-128">パッケージを一覧から削除する</span><span class="sxs-lookup"><span data-stu-id="5f68d-128">Unlisting a package</span></span>
<span data-ttu-id="5f68d-129">パッケージ バージョンを一覧から削除すると、そのバージョンが検索と nuget.org パッケージ詳細ページで非表示になります。</span><span class="sxs-lookup"><span data-stu-id="5f68d-129">Unlisting a package version hides it from search and from nuget.org package details page.</span></span> <span data-ttu-id="5f68d-130">これにより、パッケージを既に利用している人は引き続き利用できますが、パッケージが検索に表示されないため、新しい利用が減ります。</span><span class="sxs-lookup"><span data-stu-id="5f68d-130">This allows existing users of the package to continue using it but reduces new adoption since the package is not visible in search.</span></span>

<span data-ttu-id="5f68d-131">パッケージを一覧から削除する手順:</span><span class="sxs-lookup"><span data-stu-id="5f68d-131">Steps to unlist a package:</span></span>

1. <span data-ttu-id="5f68d-132">(右上隅) で `Your account name` を選択し、さらに `Manage packages`、`Published packages` の順に選択します</span><span class="sxs-lookup"><span data-stu-id="5f68d-132">Select `Your account name` (at the top right corner) >`Manage packages` > `Published packages`</span></span>
1. <span data-ttu-id="5f68d-133">[Manage package]\(パッケージの管理\) アイコンを選択します</span><span class="sxs-lookup"><span data-stu-id="5f68d-133">Select the "Manage package" icon</span></span>
1. <span data-ttu-id="5f68d-134">[一覧] セクションを展開し、パッケージ バージョンを選択します</span><span class="sxs-lookup"><span data-stu-id="5f68d-134">Expand the "Listing" section and select the package version</span></span>
1. <span data-ttu-id="5f68d-135">[List in search results]\(検索結果の一覧\) のチェックマークを外し、[保存] を選択します</span><span class="sxs-lookup"><span data-stu-id="5f68d-135">Uncheck “List in search results” and select "Save"</span></span>

<span data-ttu-id="5f68d-136">特定のパッケージ バージョンがこれで一覧から削除されました。</span><span class="sxs-lookup"><span data-stu-id="5f68d-136">The specific package version has now been unlisted.</span></span> <span data-ttu-id="5f68d-137">これを確認するには、アカウントからログアウトし、バージョンを指定せず、パッケージ ページ (例: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/ ) に移動します。</span><span class="sxs-lookup"><span data-stu-id="5f68d-137">In order to verify this, logout of your account and navigate to the package page (without the version part) e.g.: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/.</span></span> <span data-ttu-id="5f68d-138">そのパッケージのバージョンのうち、一覧から削除されて **いない** バージョンがすべで表示されます。</span><span class="sxs-lookup"><span data-stu-id="5f68d-138">You will see all versions of that package that have **not** been unlisted.</span></span> <span data-ttu-id="5f68d-139">ただし、パッケージの所有者がログインした場合、すべてのバージョンとそれが一覧に表示されるかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="5f68d-139">However, the package owner, when logged in, can see all versions and their listing status.</span></span>

<span data-ttu-id="5f68d-140">パッケージ バージョンを非推奨にすることもできます (パッケージ バージョンを削除できない場合)。</span><span class="sxs-lookup"><span data-stu-id="5f68d-140">It's also possible to deprecate a package version (in case you can't delete a package version).</span></span> <span data-ttu-id="5f68d-141">パッケージ バージョンを非推奨にする方法については、「[パッケージの廃止](../deprecate-packages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5f68d-141">For more information about deprecating package versions, see [Deprecating packages](../deprecate-packages.md).</span></span>
