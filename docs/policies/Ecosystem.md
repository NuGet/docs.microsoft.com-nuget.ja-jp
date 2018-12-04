---
title: NuGet のエコシステムの概要
description: NuGet エコシステムの包括的なリソースには、NuGet ソース、Microsoft 以外の NuGet プロジェクト、ユーティリティ、およびトレーニング資料が含まれます。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548145"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="89d15-103">NuGet のエコシステムの概要</span><span class="sxs-lookup"><span data-stu-id="89d15-103">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="89d15-104">2010 年の登場以降、NuGet は、開発プロセスのさまざまな側面を改善および自動化するための多くの機会を提供しています。</span><span class="sxs-lookup"><span data-stu-id="89d15-104">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="89d15-105">NuGet は、[Apache v2 ライセンス](http://choosealicense.com/licenses/apache/)で許可されるオープン ソースであるため、他のプロジェクトが NuGet を利用し、企業は自社製品でのサポートを構築できます。</span><span class="sxs-lookup"><span data-stu-id="89d15-105">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="89d15-106">オープン ソース プロジェクトまたはエンタープライズ アプリケーションの開発では、NuGet と、NuGet 上およびその周囲に構築された他のアプリケーションが、ソフトウェア開発プロセスを向上させるため広範なツールのエコシステムを提供します。</span><span class="sxs-lookup"><span data-stu-id="89d15-106">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="89d15-107">これらのプロジェクトのすべては、開発者の貢献によって革新的に発展できます。</span><span class="sxs-lookup"><span data-stu-id="89d15-107">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="89d15-108">NuGet 自体に貢献するのと同様に、不具合の報告、新しい機能のアイデアの提供、フィードバックの提供、ドキュメントの記述、可能な場合はコードの提供によってもこれらのプロジェクトに貢献できます。</span><span class="sxs-lookup"><span data-stu-id="89d15-108">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="89d15-109">.NET Foundation プロジェクト</span><span class="sxs-lookup"><span data-stu-id="89d15-109">.NET Foundation projects</span></span>

<span data-ttu-id="89d15-110">NuGet は、Microsoft の開発プラットフォーム用の無料のオープン ソース パッケージ管理システムを提供します。</span><span class="sxs-lookup"><span data-stu-id="89d15-110">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="89d15-111">NuGet は、いくつかのクライアント ツール、および[公式 NuGet ギャラリー](http://www.nuget.org)を構成する一連のサービスで構成されます。</span><span class="sxs-lookup"><span data-stu-id="89d15-111">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="89d15-112">これらを組み合わせることで形成される NuGet プロジェクトは、[.NET Foundation](http://www.dotnetfoundation.org/) によって管理されます。</span><span class="sxs-lookup"><span data-stu-id="89d15-112">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="89d15-113">NuGet 組織には、GitHub 上のさまざまなリポジトリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="89d15-113">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="89d15-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) には、すべてのリポジトリの概要と、さまざまな NuGet コンポーネントが見つかる場所が記載されています。</span><span class="sxs-lookup"><span data-stu-id="89d15-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="89d15-115">Microsoft Project</span><span class="sxs-lookup"><span data-stu-id="89d15-115">Microsoft projects</span></span>

<span data-ttu-id="89d15-116">Microsoft は、NuGet の開発に広範囲に貢献しました。</span><span class="sxs-lookup"><span data-stu-id="89d15-116">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="89d15-117">Microsoft の社員によって行われたすべての貢献もオープン ソースであり、.NET Foundation に寄付されています (著作権を含む)。</span><span class="sxs-lookup"><span data-stu-id="89d15-117">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="89d15-118">Microsoft 以外のプロジェクト</span><span class="sxs-lookup"><span data-stu-id="89d15-118">Non-Microsoft projects</span></span>

<span data-ttu-id="89d15-119">その他の多くの個人や企業が、NuGet エコシステムに大きな貢献を行っています。</span><span class="sxs-lookup"><span data-stu-id="89d15-119">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="89d15-120">ここに表示される各プロジェクトは、NuGet のコア コンポーネントとは別のライセンスがある可能性があります。そのため、使用前にライセンス条項に同意できることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="89d15-120">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

- [<span data-ttu-id="89d15-121">AppVeyor CI</span><span class="sxs-lookup"><span data-stu-id="89d15-121">AppVeyor CI</span></span>](https://www.appveyor.com/)
- [<span data-ttu-id="89d15-122">Artifactory</span><span class="sxs-lookup"><span data-stu-id="89d15-122">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
- [<span data-ttu-id="89d15-123">BoxStarter</span><span class="sxs-lookup"><span data-stu-id="89d15-123">BoxStarter</span></span>](http://boxstarter.org/)
- [<span data-ttu-id="89d15-124">Chocolatey</span><span class="sxs-lookup"><span data-stu-id="89d15-124">Chocolatey</span></span>](https://chocolatey.org/)
- [<span data-ttu-id="89d15-125">CoApp</span><span class="sxs-lookup"><span data-stu-id="89d15-125">CoApp</span></span>](http://coapp.org/)
- [<span data-ttu-id="89d15-126">JetBrains ReSharper</span><span class="sxs-lookup"><span data-stu-id="89d15-126">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
- [<span data-ttu-id="89d15-127">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="89d15-127">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
- [<span data-ttu-id="89d15-128">Klondike</span><span class="sxs-lookup"><span data-stu-id="89d15-128">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
- [<span data-ttu-id="89d15-129">MinimalNugetServer</span><span class="sxs-lookup"><span data-stu-id="89d15-129">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
- [<span data-ttu-id="89d15-130">MyGet (または NuGet-as-a-service)</span><span class="sxs-lookup"><span data-stu-id="89d15-130">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
- [<span data-ttu-id="89d15-131">NuGet パッケージ エクスプローラー</span><span class="sxs-lookup"><span data-stu-id="89d15-131">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [<span data-ttu-id="89d15-132">NuGet サーバー</span><span class="sxs-lookup"><span data-stu-id="89d15-132">NuGet Server</span></span>](http://nugetserver.net/)
- [<span data-ttu-id="89d15-133">OctopusDeploy</span><span class="sxs-lookup"><span data-stu-id="89d15-133">OctopusDeploy</span></span>](https://octopus.com/)
- [<span data-ttu-id="89d15-134">Paket</span><span class="sxs-lookup"><span data-stu-id="89d15-134">Paket</span></span>](https://fsprojects.github.io/Paket/)
- [<span data-ttu-id="89d15-135">ProGet (Inedo)</span><span class="sxs-lookup"><span data-stu-id="89d15-135">ProGet (Inedo)</span></span>](http://inedo.com/proget)
- [<span data-ttu-id="89d15-136">scriptcs</span><span class="sxs-lookup"><span data-stu-id="89d15-136">scriptcs</span></span>](http://scriptcs.net/)
- [<span data-ttu-id="89d15-137">SharpDevelop</span><span class="sxs-lookup"><span data-stu-id="89d15-137">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [<span data-ttu-id="89d15-138">Sonatype Nexus</span><span class="sxs-lookup"><span data-stu-id="89d15-138">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
- [<span data-ttu-id="89d15-139">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="89d15-139">SymbolSource</span></span>](http://www.symbolsource.org/Public)
- [<span data-ttu-id="89d15-140">Xamarin と MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="89d15-140">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a><span data-ttu-id="89d15-141">その他の NuGet ベース ユーティリティ</span><span class="sxs-lookup"><span data-stu-id="89d15-141">Other NuGet-based utilities</span></span>

<span data-ttu-id="89d15-142">以下は、NuGet 上に構築されたツールとユーティリティです。</span><span class="sxs-lookup"><span data-stu-id="89d15-142">These are tools and utilities built on NuGet:</span></span>

- <span data-ttu-id="89d15-143">[Glimpse の拡張機能](http://getglimpse.com/Packages) (プラグインはパッケージ)</span><span class="sxs-lookup"><span data-stu-id="89d15-143">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
- [<span data-ttu-id="89d15-144">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="89d15-144">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
- <span data-ttu-id="89d15-145">[Orchard](http://www.orchardproject.net/) (CMS モジュールは、Orchard Gallery でホストされる v1 NuGet フィードから取得されます)</span><span class="sxs-lookup"><span data-stu-id="89d15-145">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
- [<span data-ttu-id="89d15-146">NuGet サーバーの Java 実装</span><span class="sxs-lookup"><span data-stu-id="89d15-146">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- <span data-ttu-id="89d15-147">[NuGetLatest](https://twitter.com/NuGetLatest) (新しいパッケージの公開をツイートする Twitter bot)</span><span class="sxs-lookup"><span data-stu-id="89d15-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
- <span data-ttu-id="89d15-148">[DefinitelyTyped](http://definitelytyped.org/) (NuGet に公開される[自動](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [定義](http://www.nuget.org/packages?q=DefinitelyTyped))</span><span class="sxs-lookup"><span data-stu-id="89d15-148">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="89d15-149">トレーニング資料と参照</span><span class="sxs-lookup"><span data-stu-id="89d15-149">Training materials and references</span></span>

<span data-ttu-id="89d15-150">通常、新しいツールまたはテクノロジの使用には、学習曲線が伴います。</span><span class="sxs-lookup"><span data-stu-id="89d15-150">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="89d15-151">幸運なことに、NuGet には急な学習曲線はまったくありません。</span><span class="sxs-lookup"><span data-stu-id="89d15-151">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="89d15-152">実際に、すべてのユーザーが[パッケージの使用を](../quickstart/use-a-package.md)すぐに開始できます。</span><span class="sxs-lookup"><span data-stu-id="89d15-152">In fact, anyone can [get started consuming packages](../quickstart/use-a-package.md) quickly.</span></span>

<span data-ttu-id="89d15-153">ただし、パッケージを作成し (特に良いパッケージ)、さらに自動化されたビルドと配置プロセスに NuGet を対応させる場合、次のリソースに少し時間を費やす必要があります。</span><span class="sxs-lookup"><span data-stu-id="89d15-153">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="89d15-154">NuGet ブログ</span><span class="sxs-lookup"><span data-stu-id="89d15-154">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="89d15-155">Twitter の NuGet チーム@nuget</span><span class="sxs-lookup"><span data-stu-id="89d15-155">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="89d15-156">ブック:</span><span class="sxs-lookup"><span data-stu-id="89d15-156">Books:</span></span>
  - [<span data-ttu-id="89d15-157">Apress Pro NuGet</span><span class="sxs-lookup"><span data-stu-id="89d15-157">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
  - [<span data-ttu-id="89d15-158">NuGet 2 Essentials</span><span class="sxs-lookup"><span data-stu-id="89d15-158">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="89d15-159">個々のパッケージのドキュメント</span><span class="sxs-lookup"><span data-stu-id="89d15-159">Documentation for individual packages</span></span>

<span data-ttu-id="89d15-160">[NuDoq](http://nudoq.org) は、簡単にアクセスおよび更新できる NuGet パッケージのドキュメントを提供します。</span><span class="sxs-lookup"><span data-stu-id="89d15-160">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="89d15-161">NuDoq は、nuget.org ギャラリー サーバーを定期的にポーリングし、最新のパッケージの更新を取得し、ライブラリ ドキュメント ファイルをアンパックして処理し、状況に応じてサイトを更新します。</span><span class="sxs-lookup"><span data-stu-id="89d15-161">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="89d15-162">プロジェクトを追加する</span><span class="sxs-lookup"><span data-stu-id="89d15-162">Adding your project</span></span>

<span data-ttu-id="89d15-163">このページへの貴重な追加となる NuGet エコシステム プロジェクトがある場合は、編集して pull request をこのページに送信してください。</span><span class="sxs-lookup"><span data-stu-id="89d15-163">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>
