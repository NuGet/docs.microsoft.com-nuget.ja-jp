---
title: NuGet パッケージの依存関係の解決
description: NuGet 2.x と NuGet 3.x 以降の両方について、NuGet パッケージの依存関係が解決されてインストールされるプロセスを詳しく説明します。
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: cdbe13df04bb27091b684a4ae27b0e751da1098f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549035"
---
# <a name="how-nuget-resolves-package-dependencies"></a><span data-ttu-id="64c03-103">NuGet でのパッケージ依存関係の解決方法</span><span class="sxs-lookup"><span data-stu-id="64c03-103">How NuGet resolves package dependencies</span></span>

<span data-ttu-id="64c03-104">パッケージがインストールまたは再インストールされるときは常に ([復元](../consume-packages/package-restore.md)プロセスの一部としてインストールされる場合も含めて)、NuGet はその最初のパッケージが依存する他のパッケージもすべてインストールします。</span><span class="sxs-lookup"><span data-stu-id="64c03-104">Any time a package is installed or reinstalled, which includes being installed as part of a [restore](../consume-packages/package-restore.md) process, NuGet also installs any additional packages on which that first package depends.</span></span>

<span data-ttu-id="64c03-105">これらの直接依存するものにもそれぞれに独自の依存関係が存在する可能性があり、任意の深さまでそれが続きます。</span><span class="sxs-lookup"><span data-stu-id="64c03-105">Those immediate dependencies might then also have dependencies on their own, which can continue to an arbitrary depth.</span></span> <span data-ttu-id="64c03-106">これにより、*依存関係グラフ*と呼ばれるものが生成されます。これには、すべてのレベルにおけるパッケージ間の関係が記述されています。</span><span class="sxs-lookup"><span data-stu-id="64c03-106">This produces what's called a *dependency graph* that describes the relationships between packages at all levels.</span></span>

<span data-ttu-id="64c03-107">複数のパッケージに同じ依存関係がある場合、グラフに同じパッケージ ID が異なるバージョン制約で複数回出現する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="64c03-107">When multiple packages have the same dependency, then the same package ID can appear in the graph multiple times, potentially with different version constraints.</span></span> <span data-ttu-id="64c03-108">ただし、プロジェクトで使用可能な指定されたパッケージのバージョンは 1 つのみであるため、NuGet は、使用されるバージョンを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="64c03-108">However, only one version of a given package can be used in a project, so NuGet must choose which version is used.</span></span> <span data-ttu-id="64c03-109">実際のプロセスは、使われているパッケージ管理の形式によって異なります。</span><span class="sxs-lookup"><span data-stu-id="64c03-109">The exact process depends on the package management format being used.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="64c03-110">PackageReference による依存関係の解決</span><span class="sxs-lookup"><span data-stu-id="64c03-110">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="64c03-111">PackageReference 形式を使用してパッケージをプロジェクトにインストールする場合、NuGet は、フラットなパッケージ グラフへの参照を適切なファイルに追加して、競合を未然に解決します。</span><span class="sxs-lookup"><span data-stu-id="64c03-111">When installing packages into projects using the PackageReference format, NuGet adds references to a flat package graph in the appropriate file and resolves conflicts ahead of time.</span></span> <span data-ttu-id="64c03-112">このプロセスは、"*推移的な復元*" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="64c03-112">This process is referred to as *transitive restore*.</span></span> <span data-ttu-id="64c03-113">この場合、パッケージの再インストールまたは復元はグラフに列記されているパッケージをダウンロードするプロセスであり、結果としてビルドはいっそう高速で予測可能になります。</span><span class="sxs-lookup"><span data-stu-id="64c03-113">Reinstalling or restoring packages is then a process of downloading the packages listed in the graph, resulting in faster and more predictable builds.</span></span> <span data-ttu-id="64c03-114">また、ワイルドカード (浮動) バージョン (2.8\* など) を利用することもでき、コストがかかってエラーが発生しやすい `nuget update` の呼び出しをクライアント コンピューターやビルド サーバーで回避できます。</span><span class="sxs-lookup"><span data-stu-id="64c03-114">You can also take advantage of wildcard (floating) versions, such as 2.8.\*, avoiding expensive and error prone calls to `nuget update` on the client machines and build servers.</span></span>

<span data-ttu-id="64c03-115">ビルド以前に NuGet の復元プロセスを実行すると、最初にメモリ内で依存関係が解決された後、PackageReference を使用するプロジェクトの `obj` フォルダー内にある `project.assets.json` という名前のファイルに、結果のグラフを書き込みます。</span><span class="sxs-lookup"><span data-stu-id="64c03-115">When the NuGet restore process runs prior to a build, it resolves dependencies first in memory, then writes the resulting graph to a file called `project.assets.json` in the `obj` folder of a project using PackageReference.</span></span> <span data-ttu-id="64c03-116">その後、MSBuild はこのファイルを読み取り、潜在的な参照が見つかるフォルダーのセットに変換して、メモリ内のプロジェクト ツリーに追加します。</span><span class="sxs-lookup"><span data-stu-id="64c03-116">MSBuild then reads this file and translates it into a set of folders where potential references can be found, and then adds them to the project tree in memory.</span></span>

<span data-ttu-id="64c03-117">ロック ファイルは一時的なものであり、ソース管理に追加してはなりません。</span><span class="sxs-lookup"><span data-stu-id="64c03-117">The lock file is temporary and should not be added to source control.</span></span> <span data-ttu-id="64c03-118">ロック ファイルは既定で `.gitignore` と `.tfignore` の両方に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="64c03-118">It's listed by default in both `.gitignore` and `.tfignore`.</span></span> <span data-ttu-id="64c03-119">「[パッケージとソース管理](packages-and-source-control.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="64c03-119">See [Packages and source control](packages-and-source-control.md).</span></span>

### <a name="dependency-resolution-rules"></a><span data-ttu-id="64c03-120">依存関係の解決ルール</span><span class="sxs-lookup"><span data-stu-id="64c03-120">Dependency resolution rules</span></span>

<span data-ttu-id="64c03-121">推移的な復元では、依存関係を解決するために、適用可能な最低バージョン、浮動バージョン、最近優先、いとこ依存関係の 4 つの主要なルールが適用されます。</span><span class="sxs-lookup"><span data-stu-id="64c03-121">Transitive restore applies four main rules to resolve dependencies: lowest applicable version, floating versions, nearest-wins, and cousin dependencies.</span></span>

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a><span data-ttu-id="64c03-122">適用可能な最低バージョン</span><span class="sxs-lookup"><span data-stu-id="64c03-122">Lowest applicable version</span></span>

<span data-ttu-id="64c03-123">適用可能な最低バージョン ルールは、依存関係によって定義されている最低の可能なバージョンのパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="64c03-123">The lowest applicable version rule restores the lowest possible version of a package as defined by its dependencies.</span></span> <span data-ttu-id="64c03-124">また、[浮動](#floating-versions)と宣言されていない限り、アプリケーションまたはクラス ライブラリの依存関係にも適用されます。</span><span class="sxs-lookup"><span data-stu-id="64c03-124">It also applies to dependencies on the application or the class library unless declared as [floating](#floating-versions).</span></span>

<span data-ttu-id="64c03-125">次の図では、たとえば 1.0-beta は 1.0 より低いと見なされるので、NuGet は 1.0 バージョンを選びます。</span><span class="sxs-lookup"><span data-stu-id="64c03-125">In the following figure, for example, 1.0-beta is considered lower than 1.0 so NuGet chooses the 1.0 version:</span></span>

![適用可能な最低バージョンの選択](media/projectJson-dependency-1.png)

<span data-ttu-id="64c03-127">次の図では、バージョン 2.1 はフィードで利用できませんが、バージョンの制約が 2.1 以上なので、NuGet は見つかった次に低いバージョンである 2.2 を選びます。</span><span class="sxs-lookup"><span data-stu-id="64c03-127">In the next figure, version 2.1 is not available on the feed but because the version constraint is >= 2.1 NuGet picks the next lowest version it can find, in this case 2.2:</span></span>

![フィードで利用可能な次に低いバージョンの選択](media/projectJson-dependency-2.png)

<span data-ttu-id="64c03-129">アプリケーションで厳密なバージョン (1.2 など) が指定されていて、フィードでそれを利用できない場合、パッケージをインストールまたは復元しようとした NuGet はエラーで失敗します。</span><span class="sxs-lookup"><span data-stu-id="64c03-129">When an application specifies an exact version number, such as 1.2, that is not available on the feed, NuGet fails with an error when attempting to install or restore the package:</span></span>

![厳密に指定されたバージョンのパッケージを利用できない場合、NuGet はエラーを生成する](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a><span data-ttu-id="64c03-131">浮動 (ワイルドカード) バージョン</span><span class="sxs-lookup"><span data-stu-id="64c03-131">Floating (wildcard) versions</span></span>

<span data-ttu-id="64c03-132">浮動依存関係バージョンまたはワイルドカード依存関係バージョンは、6.0.\* のように \* ワイルドカードを使って指定します。</span><span class="sxs-lookup"><span data-stu-id="64c03-132">A floating or wildcard dependency version is specified with the \* wildcard, as with 6.0.\*.</span></span> <span data-ttu-id="64c03-133">このバージョン指定は、"最新の 6.0.x バージョンを使う" ということです。たとえば、4.\* は "最新の 4.x バージョンを使う" ことを意味します。</span><span class="sxs-lookup"><span data-stu-id="64c03-133">This version specification says "use the latest 6.0.x version"; 4.\* means "use the latest 4.x version."</span></span> <span data-ttu-id="64c03-134">ワイルドカードを使うと、使用する側のアプリケーション (またはパッケージ) を変更することなく、依存関係のパッケージのバージョンを上げることができます。</span><span class="sxs-lookup"><span data-stu-id="64c03-134">Using a wildcard allows a dependency package to continue evolving without requiring a change to the consuming application (or package).</span></span>

<span data-ttu-id="64c03-135">ワイルドカードを使った場合、NuGet はバージョン パターンと一致する最高バージョンのパッケージを解決します。たとえば、6.0.\* は 6.0 で始まるパッケージの最高バージョンになります。</span><span class="sxs-lookup"><span data-stu-id="64c03-135">When using a wildcard, NuGet resolves the highest version of a package that matches the version pattern, for example 6.0.\* gets the highest version of a package that starts with 6.0:</span></span>

![浮動バージョン 6.0.\* が要求されたときは、バージョン 6.0.1 を選ぶ](media/projectJson-dependency-4.png)

> [!Note]
> <span data-ttu-id="64c03-137">ワイルドカードの動作およびプレリリース バージョンについては、「[パッケージのバージョン管理](../reference/package-versioning.md#version-ranges-and-wildcards)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="64c03-137">For information on the behavior of wildcards and pre-release versions, see [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a><span data-ttu-id="64c03-138">最近優先</span><span class="sxs-lookup"><span data-stu-id="64c03-138">Nearest wins</span></span>

<span data-ttu-id="64c03-139">アプリケーションのパッケージ グラフに同じパッケージの異なるバージョンが含まれる場合、NuGet はグラフ内でアプリケーションに最も近いパッケージを選び、他のすべてのパッケージは無視します。</span><span class="sxs-lookup"><span data-stu-id="64c03-139">When the package graph for an application contains different versions of the same package, NuGet chooses the package that's closest to the application in the graph and ignores all others.</span></span> <span data-ttu-id="64c03-140">この動作により、アプリケーションは依存関係グラフ内で特定のパッケージのバージョンをオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="64c03-140">This behavior allows an application to override any particular package version in the dependency graph.</span></span>

<span data-ttu-id="64c03-141">次の例では、アプリケーションはバージョン制約 2.0 以上でパッケージ B に直接依存しています。</span><span class="sxs-lookup"><span data-stu-id="64c03-141">In the example below, the application depends directly on Package B with a version constraint of >=2.0.</span></span> <span data-ttu-id="64c03-142">また、アプリケーションはパッケージ A にも依存していますが、パッケージ A も 1.0 以上の制約でパッケージ B に依存しています。</span><span class="sxs-lookup"><span data-stu-id="64c03-142">The application also depends on Package A which in turn also depends on Package B, but with a >=1.0 constraint.</span></span> <span data-ttu-id="64c03-143">パッケージ B 2.0 に対する依存関係の方がグラフでアプリケーションに近いので、バージョン 2.0 が使われます。</span><span class="sxs-lookup"><span data-stu-id="64c03-143">Because the dependency on Package B 2.0 is nearer to the application in the graph, that version is used:</span></span>

![最近優先ルールを使うアプリケーション](media/projectJson-dependency-5.png)

>[!Warning]
> <span data-ttu-id="64c03-145">最近優先ルールでは、パッケージのバージョンのダウングレードが発生することがあるので、グラフ内の他の依存関係が損なわれる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="64c03-145">The Nearest Wins rule can result in a downgrade of the package version, thus potentially breaking other dependencies in the graph.</span></span> <span data-ttu-id="64c03-146">そのため、このルールを適用するとユーザーに警告が通知されます。</span><span class="sxs-lookup"><span data-stu-id="64c03-146">Hence this rule is applied with a warning to alert the user.</span></span>

<span data-ttu-id="64c03-147">また、このルールでは、指定された依存関係が無視されると、NuGet はグラフのその分岐にある残りの依存関係もすべて無視するので、大規模な依存関係グラフ (BCL パッケージを含むものなど) での効率が大幅に向上する効果もあります。</span><span class="sxs-lookup"><span data-stu-id="64c03-147">This rule also results in greater efficiency with a large dependency graph (such as those with the BCL packages) because once a given dependency is ignored, NuGet also ignores all remaining dependencies on that branch of the graph.</span></span> <span data-ttu-id="64c03-148">たとえば、次の図では、パッケージ C 2.0 が使われるため、NuGet は古いバージョンのパッケージ C を参照しているグラフ内のすべての分岐を無視します。</span><span class="sxs-lookup"><span data-stu-id="64c03-148">In the diagram below, for example, because Package C 2.0 is used, NuGet ignores any branches in the graph that refer to an older version of Package C:</span></span>

![NuGet は、グラフ内のパッケージを無視するとき、その分岐全体を無視する](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a><span data-ttu-id="64c03-150">いとこ依存関係</span><span class="sxs-lookup"><span data-stu-id="64c03-150">Cousin dependencies</span></span>

<span data-ttu-id="64c03-151">グラフ内のアプリケーションから同じ距離で、同じパッケージの異なるバージョンが参照されている場合、NuGet はすべてのバージョン要件が満たされる最低バージョンを使います ([適用可能な最低バージョン](#lowest-applicable-version)および[浮動バージョン](#floating-versions) ルールと同様)。</span><span class="sxs-lookup"><span data-stu-id="64c03-151">When different package versions are referred to at the same distance in the graph from the application, NuGet uses the lowest version that satisfies all version requirements (as with the [lowest applicable version](#lowest-applicable-version) and [floating versions](#floating-versions) rules).</span></span> <span data-ttu-id="64c03-152">たとえば、次の図では、パッケージ B のバージョン 2.0 はいとこの 1.0 以上という制約を満たすので、バージョン 2.0 が使われます。</span><span class="sxs-lookup"><span data-stu-id="64c03-152">In the image below, for example, version 2.0 of Package B satisfies the other >=1.0 constraint, and is thus used:</span></span>

![すべての制約を満たす最低バージョンを使う、いとこ依存関係の解決](media/projectJson-dependency-7.png)

<span data-ttu-id="64c03-154">状況によっては、すべてのバージョン要件を満たすことができない場合があります。</span><span class="sxs-lookup"><span data-stu-id="64c03-154">In some cases, it's not possible to meet all version requirements.</span></span> <span data-ttu-id="64c03-155">次に示すように、パッケージ A ではパッケージ B 1.0 だけが必要であり、パッケージ C ではパッケージ B 2.0 以上が必要である場合、NuGet は依存関係を解決できずエラーを生成します。</span><span class="sxs-lookup"><span data-stu-id="64c03-155">As shown below, if Package A requires exactly Package B 1.0 and Package C requires Package B >=2.0, then NuGet cannot resolve the dependencies and gives an error.</span></span>

![厳密なバージョン要件のために解決できない依存関係](media/projectJson-dependency-8.png)

<span data-ttu-id="64c03-157">このような状況では、最上位のコンシューマー (アプリケーションまたはパッケージ) がパッケージ B に対する独自の直接依存関係を追加して、[最近優先](#nearest-wins)ルールが適用されるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="64c03-157">In these situations, the top-level consumer (the application or package) should add its own direct dependency on Package B so that the [Nearest Wins](#nearest-wins) rule applies.</span></span>

## <a name="dependency-resolution-with-packagesconfig"></a><span data-ttu-id="64c03-158">packages.config での依存関係の解決</span><span class="sxs-lookup"><span data-stu-id="64c03-158">Dependency resolution with packages.config</span></span>

<span data-ttu-id="64c03-159">`packages.config` では、プロジェクトの依存関係はフラット リストとして `packages.config` に書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="64c03-159">With `packages.config`, a project's dependencies are written to `packages.config` as a flat list.</span></span> <span data-ttu-id="64c03-160">これらのパッケージの依存関係も、同じリストに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="64c03-160">Any dependencies of those packages are also written in the same list.</span></span> <span data-ttu-id="64c03-161">パッケージがインストールされると、NuGet は `.csproj` ファイル、`app.config`、`web.config`、および他の個別ファイルも変更する場合があります。</span><span class="sxs-lookup"><span data-stu-id="64c03-161">When packages are installed, NuGet might also modify the `.csproj` file, `app.config`, `web.config`, and other individual files.</span></span>

<span data-ttu-id="64c03-162">`packages.config` の場合、NuGet は個々のパッケージのインストール中に依存関係の競合の解決を試みます。</span><span class="sxs-lookup"><span data-stu-id="64c03-162">With `packages.config`, NuGet attempts to resolve dependency conflicts during the installation of each individual package.</span></span> <span data-ttu-id="64c03-163">つまり、パッケージ B に依存するパッケージ A がインストールされていて、パッケージ B が別のものの依存関係として `packages.config` のリストに既に含まれる場合、NuGet は要求されているパッケージ B のバージョンを比較し、すべてのバージョン制約を満たすバージョンの発見を試みます。</span><span class="sxs-lookup"><span data-stu-id="64c03-163">That is, if Package A is being installed and depends on Package B, and Package B is already listed in `packages.config` as a dependency of something else, NuGet compares the versions of Package B being requested and attempts to find a version that satisfies all version constraints.</span></span> <span data-ttu-id="64c03-164">具体的には、NuGet は依存関係を満たす低い方の *major.minor* バージョンを選びます。</span><span class="sxs-lookup"><span data-stu-id="64c03-164">Specifically, NuGet selects the lower *major.minor* version that satisfies dependencies.</span></span>

<span data-ttu-id="64c03-165">NuGet 2.8 は、既定により、最も低い "パッチ" バージョンを探します (「[NuGet 2.8 のリリース ノート](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="64c03-165">By default, NuGet 2.8 looks for the lowest patch version (see [NuGet 2.8 release notes](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)).</span></span> <span data-ttu-id="64c03-166">この設定は、`Nuget.Config` の `DependencyVersion` 属性およびコマンド ラインの `-DependencyVersion` スイッチで制御できます。</span><span class="sxs-lookup"><span data-stu-id="64c03-166">You can control this setting through the `DependencyVersion` attribute in `Nuget.Config` and the `-DependencyVersion` switch on the command line.</span></span>  

<span data-ttu-id="64c03-167">`packages.config` の依存関係解決プロセスは、大規模な依存関係グラフでは複雑になります。</span><span class="sxs-lookup"><span data-stu-id="64c03-167">The `packages.config` process for resolving dependencies gets complicated for larger dependency graphs.</span></span> <span data-ttu-id="64c03-168">パッケージの各新規インストールでは、グラフ全体を走査して、バージョン間の競合の可能性を明らかにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="64c03-168">Each new package installation requires a traversal of the whole graph and raises the chance for version conflicts.</span></span> <span data-ttu-id="64c03-169">競合が発生するときは、インストールが停止されて、プロジェクトは不明な状態のままになります (特に、プロジェクト ファイル自体への変更の可能性がある場合)。</span><span class="sxs-lookup"><span data-stu-id="64c03-169">When a conflict occurs, installation is stopped, leaving the project in an indeterminate state, especially with potential modifications to the project file itself.</span></span> <span data-ttu-id="64c03-170">他のパッケージ管理形式を使うと、このような問題はありません。</span><span class="sxs-lookup"><span data-stu-id="64c03-170">This is not an issue when using other package management formats.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="64c03-171">依存関係アセットの管理</span><span class="sxs-lookup"><span data-stu-id="64c03-171">Managing dependency assets</span></span>

<span data-ttu-id="64c03-172">PackageReference 形式を使用すると、依存関係から最上位のプロジェクトへの資産のフローを制御できます。</span><span class="sxs-lookup"><span data-stu-id="64c03-172">When using the PackageReference format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="64c03-173">詳細については、[PackageReference](package-references-in-project-files.md#controlling-dependency-assets) に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="64c03-173">For details, see [PackageReference](package-references-in-project-files.md#controlling-dependency-assets).</span></span>

<span data-ttu-id="64c03-174">最上位レベルのプロジェクト自体がパッケージである場合は、`include` および `exclude` 属性と `.nuspec` ファイルの依存関係リストを使って、このフローを制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="64c03-174">When the top-level project is itself a package, you also have control over this flow by using the `include` and `exclude` attributes with dependencies listed in the `.nuspec` file.</span></span> <span data-ttu-id="64c03-175">「.nuspec Reference」(.nuspec リファレンス) の「[Dependencies](../reference/nuspec.md#dependencies)」(依存関係) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="64c03-175">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="64c03-176">参照の除外</span><span class="sxs-lookup"><span data-stu-id="64c03-176">Excluding references</span></span>

<span data-ttu-id="64c03-177">同じ名前のアセンブリがプロジェクト内の複数の箇所で参照されていて、設計時エラーおよびビルド時エラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="64c03-177">There are scenarios in which assemblies with the same name might be referenced more than once in a project, producing design-time and build-time errors.</span></span> <span data-ttu-id="64c03-178">あるプロジェクトは、`C.dll` のカスタム バージョンを含み、やはり `C.dll` を含むパッケージ C を参照しているものとします。</span><span class="sxs-lookup"><span data-stu-id="64c03-178">Consider a project that contains a custom version of `C.dll`, and references Package C that also contains `C.dll`.</span></span> <span data-ttu-id="64c03-179">同時に、このプロジェクトはパッケージ B にも依存しており、パッケージ B もパッケージ C と `C.dll` に依存しています。</span><span class="sxs-lookup"><span data-stu-id="64c03-179">At the same time, the project also depends on Package B which also depends on Package C and `C.dll`.</span></span> <span data-ttu-id="64c03-180">結果として、NuGet はどの `C.dll` を使えばよいのか決定できず、かといってパッケージ B もパッケージ C に依存しているため、プロジェクトでのパッケージ C に対する依存関係を単に削除するわけにもいきません。</span><span class="sxs-lookup"><span data-stu-id="64c03-180">As a result, NuGet can't determine which `C.dll` to use, but you can't just remove the project's dependency on Package C because Package B also depends on it.</span></span>

<span data-ttu-id="64c03-181">これを解決するには、必要な `C.dll` を直接参照し (または、適切なパッケージを参照している別のパッケージを使い)、すべての資産を除外するパッケージ C への依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="64c03-181">To resolve this, you must directly reference the `C.dll` you want (or use another package that references the right one), and then add a dependency on Package C that excludes all its assets.</span></span> <span data-ttu-id="64c03-182">これは、使われているパッケージ管理形式に応じて、次のように行われます。</span><span class="sxs-lookup"><span data-stu-id="64c03-182">This is done as follows depending on the package management format in use:</span></span>

- <span data-ttu-id="64c03-183">[PackageReference](../consume-packages/package-references-in-project-files.md): 依存関係に `Exclude="All"` を追加します。</span><span class="sxs-lookup"><span data-stu-id="64c03-183">[PackageReference](../consume-packages/package-references-in-project-files.md): add `Exclude="All"` in the dependency:</span></span>

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- <span data-ttu-id="64c03-184">`packages.config`: 必要なバージョンの `C.dll` だけを参照するように、`.csproj` ファイルからパッケージ C への参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="64c03-184">`packages.config`: remove the reference to PackageC from the `.csproj` file so that it references only the version of `C.dll` that you want.</span></span>
    
## <a name="dependency-updates-during-package-install"></a><span data-ttu-id="64c03-185">パッケージをインストールする間の依存関係の更新</span><span class="sxs-lookup"><span data-stu-id="64c03-185">Dependency updates during package install</span></span> 

<span data-ttu-id="64c03-186">依存関係のバージョンが既に満たされている場合、他のパッケージのインストール中に依存関係は更新されません。</span><span class="sxs-lookup"><span data-stu-id="64c03-186">If a dependency version is already satisfied, the dependency isn't updated during other package installations.</span></span> <span data-ttu-id="64c03-187">たとえば、パッケージ A はパッケージ B に依存し、バージョン番号として 1.0 が指定されているものとします。</span><span class="sxs-lookup"><span data-stu-id="64c03-187">For example, consider package A that depends on package B and specifies 1.0 for the version number.</span></span> <span data-ttu-id="64c03-188">ソース リポジトリには、パッケージ B のバージョン 1.0、1.1、および 1.2 が含まれます。B のバージョン 1.0 が既に含まれているプロジェクトに A をインストールした場合、B 1.0 はバージョン制約を満たしているので、そのまま使用されます。</span><span class="sxs-lookup"><span data-stu-id="64c03-188">The source repository contains versions 1.0, 1.1, and 1.2 of package B. If A is installed in a project that already contains B version 1.0, then B 1.0 remains in use because it satisfies the version constraint.</span></span> <span data-ttu-id="64c03-189">ただし、パッケージ A で B のバージョン 1.1 以上が要求されていた場合は、B 1.2 がインストールします。</span><span class="sxs-lookup"><span data-stu-id="64c03-189">However, if package A had requests version 1.1 or higher of B, then B 1.2 would be installed.</span></span> 

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="64c03-190">互換性のないパッケージのエラーの解決</span><span class="sxs-lookup"><span data-stu-id="64c03-190">Resolving incompatible package errors</span></span>

<span data-ttu-id="64c03-191">パッケージの復元操作の間に、"1 つ以上のパッケージは <プロジェクトのターゲット フレームワーク> と互換性がありません" またはパッケージはプロジェクトのターゲット フレームワークと "互換性がありません" という内容のエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="64c03-191">During a package restore operation, you may see the error "One or more packages are not compatible..." or that a package "is not compatible" with the project's target framework.</span></span>

<span data-ttu-id="64c03-192">このエラーは、プロジェクトで参照されているパッケージの 1 つ以上が、プロジェクトのターゲット フレームワークをサポートしていることを示さない場合に発生します。つまり、パッケージの `lib` フォルダーには、プロジェクトと互換性のあるターゲット フレームワーク用の適切な DLL が含まれません </span><span class="sxs-lookup"><span data-stu-id="64c03-192">This error occurs when one or more of the packages referenced in your project do not indicate that they support the project's target framework; that is, the package does not contain a suitable DLL in its `lib` folder for a target framework that is compatible with the project.</span></span> <span data-ttu-id="64c03-193">(「[Target frameworks](../reference/target-frameworks.md)」(ターゲット フレームワーク) をご覧ください)。</span><span class="sxs-lookup"><span data-stu-id="64c03-193">(See [Target frameworks](../reference/target-frameworks.md) for a list.)</span></span> 

<span data-ttu-id="64c03-194">たとえば、プロジェクトのターゲットが `netstandard1.6` で、`lib\net20` フォルダーと `\lib\net45` フォルダーのみに DLL が含まれるパッケージをインストールしようとすると、パッケージおよび場合によっては依存関係について、次のようなメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="64c03-194">For example, if a project targets `netstandard1.6` and you attempt to install a package that contains DLLs in only the `lib\net20` and `\lib\net45` folders, then you see messages like the following for the package and possibly its dependents:</span></span>

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

<span data-ttu-id="64c03-195">互換性の問題を解決するには、次のいずれかのようにします。</span><span class="sxs-lookup"><span data-stu-id="64c03-195">To resolve incompatibilities, do one of the following:</span></span>

- <span data-ttu-id="64c03-196">使うパッケージでサポートされているフレームワークに、プロジェクトのターゲットを変更します。</span><span class="sxs-lookup"><span data-stu-id="64c03-196">Retarget your project to a framework that is supported by the packages you want to use.</span></span>
- <span data-ttu-id="64c03-197">パッケージの作成者に連絡し、協力して、選んだフレームワークに対するサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="64c03-197">Contact the author of the packages and work with them to add support for your chosen framework.</span></span> <span data-ttu-id="64c03-198">[nuget.org](https://www.nuget.org/) の各パッケージ リスト ページには、そのための **[Contact Owners]** リンクがあります。</span><span class="sxs-lookup"><span data-stu-id="64c03-198">Each package listing page on [nuget.org](https://www.nuget.org/) has a **Contact Owners** link for this purpose.</span></span>

