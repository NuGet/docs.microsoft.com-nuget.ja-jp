---
title: "独自の NuGet フィードのホスティングの概要 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 97577ddd-c294-432d-81a7-b4aebe88bd1c
description: "ローカルまたはリモートのいずれかで、独自の NuGet パッケージ フィードまたはギャラリーをホスティングするためにオープンにされている概要です。"
keywords: "NuGet フィード、NuGet ギャラリー、カスタム パッケージ フィード、NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: c3c6b17cdeb4fe959adbc56bdc6ace73202a98fc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="969b5-104">独自の NuGet フィードをホスティングする</span><span class="sxs-lookup"><span data-stu-id="969b5-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="969b5-105">パッケージをパブリックに利用できるようにする代わりに、組織やワークグループなど、制限された対象ユーザーのみにパッケージをリリースする必要がある可能性があります。</span><span class="sxs-lookup"><span data-stu-id="969b5-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="969b5-106">また、一部の会社では、開発者が使用する可能性があるサードパーティ製のライブラリを制限する必要がある場合があります。そのため、開発者に nuget.org ではなく、制限されたパッケージ ソースから引き出すように指示します。</span><span class="sxs-lookup"><span data-stu-id="969b5-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="969b5-107">このようなすべての目的のために、NuGet では次の方法でプライベート パッケージ ソースの設定をサポートします。</span><span class="sxs-lookup"><span data-stu-id="969b5-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="969b5-108">ローカル フィード: パッケージは適切なネットワーク ファイル共有に単純に配置され、`nuget init` と `nuget add` を使用して、階層フォルダー構造 (NuGet 3.3 以降) を作成するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="969b5-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="969b5-109">詳細については、「[ローカル フィード](../hosting-packages/local-feeds.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="969b5-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="969b5-110">NuGet.Server: パッケージは、ローカル HTTP サーバー経由で有効にされます。</span><span class="sxs-lookup"><span data-stu-id="969b5-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="969b5-111">詳細については、「[NuGet.Server](../hosting-packages/NuGet-Server.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="969b5-111">For details, see [NuGet.Server](../hosting-packages/NuGet-Server.md).</span></span>
- <span data-ttu-id="969b5-112">NuGet ギャラリー: パッケージは、[NuGet ギャラリー プロジェクト](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com) を使用して、インターネット サーバー上にホストされます。</span><span class="sxs-lookup"><span data-stu-id="969b5-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="969b5-113">NuGet ギャラリーは、nuget.org と同様に、ブラウザー内からパッケージを検索できる広範な Web UI など、ユーザーの管理や機能を備えています。</span><span class="sxs-lookup"><span data-stu-id="969b5-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="969b5-114">また、次のようなその他のいくつかの NuGet ホスティング製品でも、リモート プライベート フィードをサポートします。</span><span class="sxs-lookup"><span data-stu-id="969b5-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="969b5-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish)。これは、Team Foundation Server 2017 以降でも利用できます。</span><span class="sxs-lookup"><span data-stu-id="969b5-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="969b5-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="969b5-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="969b5-117">[ProGet](http://inedo.com/proget) (Inedo)</span><span class="sxs-lookup"><span data-stu-id="969b5-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="969b5-118">[NuGet Server](http://nugetserver.net/)。Inedo のコミュニティ プロジェクト</span><span class="sxs-lookup"><span data-stu-id="969b5-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="969b5-119">[NuGet Server (オープン ソース)](http://nuget-server.net)。Inedo の NuGet Server と同様のオープンソースの実装</span><span class="sxs-lookup"><span data-stu-id="969b5-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="969b5-120">[Artifactory](https://www.jfrog.com/artifactory/) (JFrog)</span><span class="sxs-lookup"><span data-stu-id="969b5-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="969b5-121">[Nexus](http://www.sonatype.org/nexus/) (Sonatype)</span><span class="sxs-lookup"><span data-stu-id="969b5-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="969b5-122">[TeamCity](https://www.jetbrains.com/teamcity/) (JetBrains)</span><span class="sxs-lookup"><span data-stu-id="969b5-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="969b5-123">パッケージがどのようにホストされているかに関係なく、`NuGet.Config` で利用可能なソースの一覧にパッケージを追加して、アクセスします。</span><span class="sxs-lookup"><span data-stu-id="969b5-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="969b5-124">これは、「[パッケージ ソース](../tools/package-manager-ui.md#package-sources)」に示されているように Visual Studio で、またはコマンド ラインから [`nuget sources`](../tools/cli-ref-sources.md) を使用して実行できます。</span><span class="sxs-lookup"><span data-stu-id="969b5-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="969b5-125">ソースへのパスは、ローカル フォルダーのパス名、ネットワーク名、または URL にすることができます。</span><span class="sxs-lookup"><span data-stu-id="969b5-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
