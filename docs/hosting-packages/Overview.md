---
title: 独自の NuGet フィードのホスティングの概要
description: ローカルまたはリモートのいずれかで、独自の NuGet パッケージ フィードまたはギャラリーをホスティングするためにオープンにされている概要です。
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 737b13be70de9aaa7dec7904d4c2a4ec494ef7b3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317546"
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="bfdc3-103">独自の NuGet フィードをホスティングする</span><span class="sxs-lookup"><span data-stu-id="bfdc3-103">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="bfdc3-104">パッケージをパブリックに利用できるようにする代わりに、組織やワークグループなど、制限された対象ユーザーのみにパッケージをリリースする必要がある可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-104">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="bfdc3-105">また、一部の会社では、開発者が使用する可能性があるサードパーティ製のライブラリを制限する必要がある場合があります。そのため、開発者に nuget.org ではなく、制限されたパッケージ ソースから引き出すように指示します。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-105">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="bfdc3-106">このようなすべての目的のために、NuGet では次の方法でプライベート パッケージ ソースの設定をサポートします。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-106">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="bfdc3-107">ローカル フィード:パッケージは適切なネットワーク ファイル共有に単純に配置され、`nuget init` と `nuget add` を使用して、階層フォルダー構造 (NuGet 3.3 以降) を作成するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-107">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="bfdc3-108">詳細については、「[ローカル フィード](../hosting-packages/local-feeds.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-108">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="bfdc3-109">NuGet.Server:パッケージは、ローカル HTTP サーバー経由で有効にされます。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-109">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="bfdc3-110">詳細については、「[NuGet.Server](../hosting-packages/nuget-server.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-110">For details, see [NuGet.Server](../hosting-packages/nuget-server.md).</span></span>
- <span data-ttu-id="bfdc3-111">NuGet ギャラリー:パッケージは、[NuGet ギャラリー プロジェクト](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com) を使用して、インターネット サーバー上にホストされます。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-111">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="bfdc3-112">NuGet ギャラリーは、nuget.org と同様に、ブラウザー内からパッケージを検索できる広範な Web UI など、ユーザーの管理や機能を備えています。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-112">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="bfdc3-113">また、次のようなその他のいくつかの NuGet ホスティング製品でも、リモート プライベート フィードをサポートします。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-113">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="bfdc3-114">[Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)。これは、Team Foundation Server 2017 以降でも利用できます。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-114">[Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="bfdc3-115">MyGet</span><span class="sxs-lookup"><span data-stu-id="bfdc3-115">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="bfdc3-116">[ProGet](http://inedo.com/proget) (Inedo)</span><span class="sxs-lookup"><span data-stu-id="bfdc3-116">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- [<span data-ttu-id="bfdc3-117">GitHub パッケージ レジストリ</span><span class="sxs-lookup"><span data-stu-id="bfdc3-117">GitHub package registry</span></span>](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- <span data-ttu-id="bfdc3-118">[NuGet Server](http://nugetserver.net/)。Inedo のコミュニティ プロジェクト</span><span class="sxs-lookup"><span data-stu-id="bfdc3-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="bfdc3-119">[NuGet Server (オープン ソース)](http://nuget-server.net)。Inedo の NuGet Server と同様のオープンソースの実装</span><span class="sxs-lookup"><span data-stu-id="bfdc3-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="bfdc3-120">[LiGet](https://github.com/ai-traders/liget)。Docker の Kestrel 上で実行される NuGet V2 サーバーのオープン ソースの実装</span><span class="sxs-lookup"><span data-stu-id="bfdc3-120">[LiGet](https://github.com/ai-traders/liget), an open-source implementation of NuGet V2 server that runs on kestrel in docker</span></span>
- <span data-ttu-id="bfdc3-121">[BaGet](https://github.com/loic-sharma/BaGet)。ASP.NET Core 上に構築された NuGet V3 サーバーのオープン ソースの実装</span><span class="sxs-lookup"><span data-stu-id="bfdc3-121">[BaGet](https://github.com/loic-sharma/BaGet), an open-source implementation of NuGet V3 server built on ASP.NET Core</span></span>
- <span data-ttu-id="bfdc3-122">[Sleet](https://github.com/emgarten/sleet)。オープン ソースの NuGet V3 静的フィード ジェネレーター</span><span class="sxs-lookup"><span data-stu-id="bfdc3-122">[Sleet](https://github.com/emgarten/sleet), an open-source NuGet V3 static feed generator</span></span>
- <span data-ttu-id="bfdc3-123">[Artifactory](https://www.jfrog.com/artifactory/) (JFrog)</span><span class="sxs-lookup"><span data-stu-id="bfdc3-123">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="bfdc3-124">[Nexus](http://www.sonatype.org/nexus/) (Sonatype)</span><span class="sxs-lookup"><span data-stu-id="bfdc3-124">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="bfdc3-125">[TeamCity](https://www.jetbrains.com/teamcity/) (JetBrains)</span><span class="sxs-lookup"><span data-stu-id="bfdc3-125">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="bfdc3-126">パッケージがどのようにホストされているかに関係なく、`NuGet.Config` で利用可能なソースの一覧にパッケージを追加して、アクセスします。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-126">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="bfdc3-127">これは、「[パッケージ ソース](../consume-packages/install-use-packages-visual-studio.md#package-sources)」に示されているように Visual Studio で、またはコマンド ラインから [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) を使用して実行できます。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-127">This can be done in Visual Studio as described in [Package Sources](../consume-packages/install-use-packages-visual-studio.md#package-sources), or from the command line using [`nuget sources`](../reference/cli-reference/cli-ref-sources.md).</span></span> <span data-ttu-id="bfdc3-128">ソースへのパスは、ローカル フォルダーのパス名、ネットワーク名、または URL にすることができます。</span><span class="sxs-lookup"><span data-stu-id="bfdc3-128">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
