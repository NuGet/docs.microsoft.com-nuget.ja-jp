---
title: nuget.org から NuGet パッケージを削除する
description: nuget.org の一覧からパッケージを削除するポリシーです。パッケージが他のポリシーに違反しない限り、完全な削除はサポートされません。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 833f4a67bc75c5d650e85180b52ecd8f69218f15
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196188"
---
# <a name="deleting-packages"></a><span data-ttu-id="6ab02-103">パッケージの削除</span><span class="sxs-lookup"><span data-stu-id="6ab02-103">Deleting packages</span></span>

<span data-ttu-id="6ab02-104">nuget.org では、パッケージの完全な削除はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6ab02-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="6ab02-105">この操作を行うには、パッケージの機能に応じて、特にパッケージの復元を含むビルドのワークフローで、すべてのプロジェクトを中断します。</span><span class="sxs-lookup"><span data-stu-id="6ab02-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="6ab02-106">nuget.org では、Web サイト上のパッケージ管理ページで実行できる、パッケージの*一覧からの削除*はサポートされません。</span><span class="sxs-lookup"><span data-stu-id="6ab02-106">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="6ab02-107">一覧から削除されたパッケージは、nuget.org または Visual Studio UI に表示されません。また、検索結果にも表示されません。</span><span class="sxs-lookup"><span data-stu-id="6ab02-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="6ab02-108">ただし、一覧から削除されたパッケージは、引き続きパッケージの復元をサポートする正確なバージョン番号を使用し、ダウンロードしてインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="6ab02-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="6ab02-109">さらに、一覧から削除されたパッケージは、次の特定のシナリオで引き続き検出される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6ab02-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="6ab02-110">バージョンまたは依存関係の制約を満たす使用できる最新パッケージが一覧から削除されたパッケージの場合の、最新バージョンを使用したパッケージの復元 (例: `1.0.0-*`)。</span><span class="sxs-lookup"><span data-stu-id="6ab02-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="6ab02-111">(カタログに一覧から削除されたパッケージも含まれるように) カタログを使用したパッケージのレプリケーション。</span><span class="sxs-lookup"><span data-stu-id="6ab02-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="6ab02-112">例外</span><span class="sxs-lookup"><span data-stu-id="6ab02-112">Exceptions</span></span>

<span data-ttu-id="6ab02-113">著作権侵害や問題を起こす可能性のあるコンテンツなどの例外状況では、パッケージは NuGet チームによって手動で削除することができます。</span><span class="sxs-lookup"><span data-stu-id="6ab02-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="6ab02-114">NuGet.org のパッケージ詳細ページで、[不正使用を報告] ボタンを使用してパッケージを報告することができます。</span><span class="sxs-lookup"><span data-stu-id="6ab02-114">You can report a package using the "Report abuse" button on the NuGet.org package details page.</span></span> <span data-ttu-id="6ab02-115">パッケージの所有者は、NuGet.org アカウントにログインし、NuGet.org パッケージ詳細ページの [Contact support]\(サポートへの問い合わせ\) ボタンを使用して NuGet サポートに連絡することができます。</span><span class="sxs-lookup"><span data-stu-id="6ab02-115">If you are the package owner, login to your NuGet.org account to reach NuGet support using the "Contact support" button on the NuGet.org package details page.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="6ab02-116">禁止事項</span><span class="sxs-lookup"><span data-stu-id="6ab02-116">Prohibited use</span></span>

<span data-ttu-id="6ab02-117">次のいずれかの基準を満たすパッケージは、パブリック NuGet ギャラリー上で許可されません。また、そのようなパッケージは、ディスカッションされることなく、すぐに削除されます。</span><span class="sxs-lookup"><span data-stu-id="6ab02-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="6ab02-118">ただし、パッケージの所有者は、削除の通知を受けます。</span><span class="sxs-lookup"><span data-stu-id="6ab02-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="6ab02-119">マルウェア、アドウェア、またはあらゆる種類のスパイウェアが含まれる</span><span class="sxs-lookup"><span data-stu-id="6ab02-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="6ab02-120">開発者のワークステーションまたは組織に損害を与えるように設計されている</span><span class="sxs-lookup"><span data-stu-id="6ab02-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="6ab02-121">著作権を侵害したり、ライセンスに違反したりしている</span><span class="sxs-lookup"><span data-stu-id="6ab02-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="6ab02-122">違法なコンテンツを含む</span><span class="sxs-lookup"><span data-stu-id="6ab02-122">Contains illegal content.</span></span>
- <span data-ttu-id="6ab02-123">生産性のないコンテンツを含むパッケージなど、パッケージの識別子を占拠するために使用されている。</span><span class="sxs-lookup"><span data-stu-id="6ab02-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="6ab02-124">パッケージにコードが含まれるか、所有者が実際に出荷する製品を所有しているユーザーに識別子を譲る必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ab02-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="6ab02-125">ギャラリーで明示的に実行するように設計されていない操作を行うようにしている。</span><span class="sxs-lookup"><span data-stu-id="6ab02-125">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="6ab02-126">これらの項目のいずれかに違反しているパッケージを見つけた場合は、パッケージの詳細ページで **[不正使用を報告]** リンクをクリックして、レポートを送信します。</span><span class="sxs-lookup"><span data-stu-id="6ab02-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="6ab02-127">NuGet チームと .NET Foundation は、いつでもこれらの条件を変更する権利を保有することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6ab02-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
