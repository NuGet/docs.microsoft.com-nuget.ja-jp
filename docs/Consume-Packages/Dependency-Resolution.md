---
title: "NuGet パッケージの依存関係の解決 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1d530a72-3486-4a0d-b6fb-017524616f91
description: "NuGet 2.x と NuGet 3.x 以降の両方について、NuGet パッケージの依存関係が解決されてインストールされるプロセスを詳しく説明します。"
keywords: "NuGet パッケージの依存関係, NuGet のバージョン管理, 依存関係のバージョン, バージョン グラフ, バージョンの解決, 推移的な復元"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 44c69c07990fed72b439698d22021ebcbb2eed89
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="how-nuget-resolves-package-dependencies"></a><span data-ttu-id="17918-104">NuGet でのパッケージ依存関係の解決方法</span><span class="sxs-lookup"><span data-stu-id="17918-104">How NuGet resolves package dependencies</span></span>

<span data-ttu-id="17918-105">パッケージがインストールまたは再インストールされるときは常に ([復元](../consume-packages/package-restore.md)プロセスの一部としてインストールされる場合も含めて)、NuGet はその最初のパッケージが依存する他のパッケージもすべてインストールします。</span><span class="sxs-lookup"><span data-stu-id="17918-105">Any time a package is installed or reinstalled, which includes being installed as part of a [restore](../consume-packages/package-restore.md) process, NuGet also installs any additional packages on which that first package depends.</span></span>

<span data-ttu-id="17918-106">これらの直接依存するものにもそれぞれに独自の依存関係が存在する可能性があり、任意の深さまでそれが続きます。</span><span class="sxs-lookup"><span data-stu-id="17918-106">Those immediate dependencies might then also have dependencies on their own, which can continue to an arbitrary depth.</span></span> <span data-ttu-id="17918-107">これにより、すべてのレベルにおけるパッケージ間の関係が記述された "*依存関係グラフ*" と呼ばれるものが生成されます。</span><span class="sxs-lookup"><span data-stu-id="17918-107">This produces what's called a *dependency graph* that describes the relationships between packages are all levels.</span></span>

<span data-ttu-id="17918-108">複数のパッケージに同じ依存関係がある場合、グラフに同じパッケージ ID が異なるバージョン制約で複数回出現する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="17918-108">When multiple packages have the same dependency, then the same package ID can appear in the graph multiple times, potentially with different version constraints.</span></span> <span data-ttu-id="17918-109">ただし、プロジェクトで使うことができる指定されたパッケージのバージョンは 1 つだけなので、NuGet は使うバージョンを選ぶ必要があります。</span><span class="sxs-lookup"><span data-stu-id="17918-109">However, only one version of a given package can be used in a project, so NuGet must choose which version is be used.</span></span> <span data-ttu-id="17918-110">実際のプロセスは、使われているパッケージ参照の形式によって異なります。</span><span class="sxs-lookup"><span data-stu-id="17918-110">The exact process depends on the package reference format being used.</span></span>

<span data-ttu-id="17918-111">このトピックの内容</span><span class="sxs-lookup"><span data-stu-id="17918-111">In this topic:</span></span>
- [<span data-ttu-id="17918-112">PackageReference と project.json での依存関係の解決</span><span class="sxs-lookup"><span data-stu-id="17918-112">Dependency resolution with PackageReference and project.json</span></span>](#dependency-resolution-with-packagereference-and-projectjson)
- [<span data-ttu-id="17918-113">packages.config での依存関係の解決</span><span class="sxs-lookup"><span data-stu-id="17918-113">Dependency resolution with packages.config</span></span>](#dependency-resolution-with-packagesconfig)
- <span data-ttu-id="17918-114">[参照の除外](#excluding-references)。あるプロジェクトで指定されている依存関係と、別のプロジェクトによって生成されるアセンブリの間に競合があるときに必要になります。</span><span class="sxs-lookup"><span data-stu-id="17918-114">[Excluding references](#excluding-references), which is necessary when there's a conflict between a dependency specified in one project and an assembly that's produced by another.</span></span>
- [<span data-ttu-id="17918-115">パッケージをインストールする間の依存関係の更新</span><span class="sxs-lookup"><span data-stu-id="17918-115">Dependency updates during package install</span></span>](#dependency-updates-during-package-install)
- [<span data-ttu-id="17918-116">互換性のないパッケージのエラーの解決</span><span class="sxs-lookup"><span data-stu-id="17918-116">Resolving incompatible package errors</span></span>](#resolving-incompatible-package-errors)

## <a name="dependency-resolution-with-packagereference-and-projectjson"></a><span data-ttu-id="17918-117">PackageReference と project.json での依存関係の解決</span><span class="sxs-lookup"><span data-stu-id="17918-117">Dependency resolution with PackageReference and project.json</span></span>

<span data-ttu-id="17918-118">PackageReference または `project.json` の形式を使ってプロジェクトにパッケージをインストールする場合、NuGet はフラットなパッケージ グラフへの参照を適切なファイルに追加して、事前に競合を解決します。</span><span class="sxs-lookup"><span data-stu-id="17918-118">When installing packages into projects using the PackageReference or `project.json` formats, NuGet adds references to a flat package graph in the appropriate file and resolves conflicts ahead of time.</span></span> <span data-ttu-id="17918-119">このプロセスは、"*推移的な復元*" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="17918-119">This process is referred to as *transitive restore*.</span></span> <span data-ttu-id="17918-120">この場合、パッケージの再インストールまたは復元はグラフに列記されているパッケージをダウンロードするプロセスであり、結果としてビルドはいっそう高速で予測可能になります。</span><span class="sxs-lookup"><span data-stu-id="17918-120">Reinstalling or restoring packages is then a process of downloading the packages listed in the graph, resulting in faster and more predictable builds.</span></span> <span data-ttu-id="17918-121">また、ワイルドカード (浮動) バージョン (2.8\* など) を利用することもでき、コストがかかってエラーが発生しやすい `nuget update` の呼び出しをクライアント コンピューターやビルド サーバーで回避できます。</span><span class="sxs-lookup"><span data-stu-id="17918-121">You can also take advantage of wildcard (floating) versions, such as 2.8.\*, avoiding expensive and error prone calls to `nuget update` on the client machines and build servers.</span></span>

<span data-ttu-id="17918-122">ビルド前に実行した NuGet の復元プロセスは、最初にメモリ内で依存関係を解決した後、結果のグラフを、PackageReference を使うプロジェクトの `obj` フォルダーの `project.assets.json` という名前のファイルに、または `project.json` と共に使われる `project.lock.json` という名前のファイルに書き込みます。</span><span class="sxs-lookup"><span data-stu-id="17918-122">When the NuGet restore process runs prior to a build, it resolves dependencies first in memory, then writes the resulting graph to a file called `project.assets.json` in the `obj` folder of a project using PackageReference, or in a file named `project.lock.json` alongside `project.json`.</span></span> <span data-ttu-id="17918-123">その後、MSBuild はこのファイルを読み取り、潜在的な参照が見つかるフォルダーのセットに変換して、メモリ内のプロジェクト ツリーに追加します。</span><span class="sxs-lookup"><span data-stu-id="17918-123">MSBuild then reads this file and translates it into a set of folders where potential references can be found, and then adds them to the project tree in memory.</span></span>

<span data-ttu-id="17918-124">ロック ファイルは一時的なものであり、ソース管理に追加してはなりません。</span><span class="sxs-lookup"><span data-stu-id="17918-124">The lock file is temporary and should not be added to source control.</span></span> <span data-ttu-id="17918-125">ロック ファイルは既定で `.gitignore` と `.tfignore` の両方に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="17918-125">It's listed by default in both `.gitignore` and `.tfignore`.</span></span> <span data-ttu-id="17918-126">「[パッケージとソース管理](Packages-and-Source-Control.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="17918-126">See [Packages and source control](Packages-and-Source-Control.md).</span></span>

### <a name="dependency-resolution-rules"></a><span data-ttu-id="17918-127">依存関係の解決ルール</span><span class="sxs-lookup"><span data-stu-id="17918-127">Dependency resolution rules</span></span>

<span data-ttu-id="17918-128">推移的な復元では、依存関係を解決するために、適用可能な最低バージョン、浮動バージョン、最近優先、いとこ依存関係の 4 つの主要なルールが適用されます。</span><span class="sxs-lookup"><span data-stu-id="17918-128">Transitive restore applies four main rules to resolve dependencies: lowest applicable version, floating versions, nearest-wins, and cousin dependencies.</span></span>

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a><span data-ttu-id="17918-129">適用可能な最低バージョン</span><span class="sxs-lookup"><span data-stu-id="17918-129">Lowest applicable version</span></span>

<span data-ttu-id="17918-130">適用可能な最低バージョン ルールは、依存関係によって定義されている最低の可能なバージョンのパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="17918-130">The lowest applicable version rule restores the lowest possible version of a package as defined by its dependencies.</span></span> <span data-ttu-id="17918-131">また、[浮動](#floating-versions)と宣言されていない限り、アプリケーションまたはクラス ライブラリの依存関係にも適用されます。</span><span class="sxs-lookup"><span data-stu-id="17918-131">It also applies to dependencies on the application or the class library unless declared as [floating](#floating-versions).</span></span>

<span data-ttu-id="17918-132">次の図では、たとえば 1.0-beta は 1.0 より低いと見なされるので、NuGet は 1.0 バージョンを選びます。</span><span class="sxs-lookup"><span data-stu-id="17918-132">In the following figure, for example, 1.0-beta is considered lower than 1.0 so NuGet chooses the 1.0 version:</span></span>

![適用可能な最低バージョンの選択](media/projectJson-dependency-1.png)

<span data-ttu-id="17918-134">次の図では、バージョン 2.1 はフィードで利用できませんが、バージョンの制約が 2.1 以上なので、NuGet は見つかった次に低いバージョンである 2.2 を選びます。</span><span class="sxs-lookup"><span data-stu-id="17918-134">In the next figure, version 2.1 is not available on the feed but because the version constraint is >= 2.1 NuGet picks the next lowest version it can find, in this case 2.2:</span></span>

![フィードで利用可能な次に低いバージョンの選択](media/projectJson-dependency-2.png)

<span data-ttu-id="17918-136">アプリケーションで厳密なバージョン (1.2 など) が指定されていて、フィードでそれを利用できない場合、パッケージをインストールまたは復元しようとした NuGet はエラーで失敗します。</span><span class="sxs-lookup"><span data-stu-id="17918-136">When an application specifies an exact version number, such as 1.2, that is not available on the feed, NuGet fails with an error when attempting to install or restore the package:</span></span>

![厳密に指定されたバージョンのパッケージを利用できない場合、NuGet はエラーを生成する](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a><span data-ttu-id="17918-138">浮動 (ワイルドカード) バージョン</span><span class="sxs-lookup"><span data-stu-id="17918-138">Floating (wildcard) versions</span></span>

<span data-ttu-id="17918-139">浮動依存関係バージョンまたはワイルドカード依存関係バージョンは、6.0.\* のように \* ワイルドカードを使って指定します。</span><span class="sxs-lookup"><span data-stu-id="17918-139">A floating or wildcard dependency version is specified with the \* wildcard, as with 6.0.\*.</span></span> <span data-ttu-id="17918-140">このバージョン指定は、"最新の 6.0.x バージョンを使う" ということです。たとえば、4.\* は "最新の 4.x バージョンを使う" ことを意味します。</span><span class="sxs-lookup"><span data-stu-id="17918-140">This version specification says "use the latest 6.0.x version"; 4.\* means "use the latest 4.x version."</span></span> <span data-ttu-id="17918-141">ワイルドカードを使うと、使用する側のアプリケーション (またはパッケージ) を変更することなく、依存関係のパッケージのバージョンを上げることができます。</span><span class="sxs-lookup"><span data-stu-id="17918-141">Using a wildcard allows a dependency package to continue evolving without requiring a change to the consuming application (or package).</span></span>

<span data-ttu-id="17918-142">ワイルドカードを使った場合、NuGet はバージョン パターンと一致する最高バージョンのパッケージを解決します。たとえば、6.0.\* は 6.0 で始まるパッケージの最高バージョンになります。</span><span class="sxs-lookup"><span data-stu-id="17918-142">When using a wildcard, NuGet resolves the highest version of a package that matches the version pattern, for example 6.0.\* gets the highest version of a package that starts with 6.0:</span></span>

![浮動バージョン 6.0.* が要求されたときは、バージョン 6.0.1 を選ぶ](media/projectJson-dependency-4.png)

> [!Note]
> <span data-ttu-id="17918-144">ワイルドカードの動作およびプレリリース バージョンについては、「[パッケージのバージョン管理](../reference/package-versioning.md#version-ranges-and-wildcards)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="17918-144">For information on the behavior of wildcards and pre-release versions, see [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a><span data-ttu-id="17918-145">最近優先</span><span class="sxs-lookup"><span data-stu-id="17918-145">Nearest wins</span></span>

<span data-ttu-id="17918-146">アプリケーションのパッケージ グラフに同じパッケージの異なるバージョンが含まれる場合、NuGet はグラフ内でアプリケーションに最も近いパッケージを選び、他のすべてのパッケージは無視します。</span><span class="sxs-lookup"><span data-stu-id="17918-146">When the package graph for an application contains different versions of the same package, NuGet chooses the package that's closest to the application in the graph and ignores all others.</span></span> <span data-ttu-id="17918-147">この動作により、アプリケーションは依存関係グラフ内で特定のパッケージのバージョンを上書きできます。</span><span class="sxs-lookup"><span data-stu-id="17918-147">This behavior allows an application to override any particular package version in the dependency graph.</span></span>

<span data-ttu-id="17918-148">次の例では、アプリケーションはバージョン制約 2.0 以上でパッケージ B に直接依存しています。</span><span class="sxs-lookup"><span data-stu-id="17918-148">In the example below, the application depends directly on Package B with a version constraint of >=2.0.</span></span> <span data-ttu-id="17918-149">また、アプリケーションはパッケージ A にも依存していますが、パッケージ A も 1.0 以上の制約でパッケージ B に依存しています。</span><span class="sxs-lookup"><span data-stu-id="17918-149">The application also depends on Package A which in turn also depends on Package B, but with a >=1.0 constraint.</span></span> <span data-ttu-id="17918-150">パッケージ B 2.0 に対する依存関係の方がグラフでアプリケーションに近いので、バージョン 2.0 が使われます。</span><span class="sxs-lookup"><span data-stu-id="17918-150">Because the dependency on Package B 2.0 is nearer to the application in the graph, that version is used:</span></span>

![最近優先ルールを使うアプリケーション](media/projectJson-dependency-5.png)

>[!Warning]
> <span data-ttu-id="17918-152">最近優先ルールでは、パッケージのバージョンのダウングレードが発生することがあるので、グラフ内の他の依存関係が損なわれる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="17918-152">The Nearest Wins rule can result in a downgrade of the package version, thus potentially breaking other dependencies in the graph.</span></span> <span data-ttu-id="17918-153">そのため、このルールを適用するとユーザーに警告が通知されます。</span><span class="sxs-lookup"><span data-stu-id="17918-153">Hence this rule is applied with a warning to alert the user.</span></span>

<span data-ttu-id="17918-154">また、このルールでは、指定された依存関係が無視されると、NuGet はグラフのその分岐にある残りの依存関係もすべて無視するので、大規模な依存関係グラフ (BCL パッケージを含むものなど) での効率が大幅に向上する効果もあります。</span><span class="sxs-lookup"><span data-stu-id="17918-154">This rule also results in greater efficiency with a large dependency graph (such as those with the BCL packages) because once a given dependency is ignored, NuGet also ignores all remaining dependencies on that branch of the graph.</span></span> <span data-ttu-id="17918-155">たとえば、次の図では、パッケージ C 2.0 が使われるため、NuGet は古いバージョンのパッケージ C を参照しているグラフ内のすべての分岐を無視します。</span><span class="sxs-lookup"><span data-stu-id="17918-155">In the diagram below, for example, because Package C 2.0 is used, NuGet ignores any branches in the graph that refer to an older version of Package C:</span></span>

![NuGet は、グラフ内のパッケージを無視するとき、その分岐全体を無視する](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a><span data-ttu-id="17918-157">いとこ依存関係</span><span class="sxs-lookup"><span data-stu-id="17918-157">Cousin dependencies</span></span>

<span data-ttu-id="17918-158">グラフ内のアプリケーションから同じ距離で、同じパッケージの異なるバージョンが参照されている場合、NuGet はすべてのバージョン要件が満たされる最低バージョンを使います ([適用可能な最低バージョン](#lowest-applicable-version)および[浮動バージョン](#floating-versions) ルールと同様)。</span><span class="sxs-lookup"><span data-stu-id="17918-158">When different package versions are referred to at the same distance in the graph from the application, NuGet uses the lowest version that satisfies all version requirements (as with the [lowest applicable version](#lowest-applicable-version) and [floating versions](#floating-versions) rules).</span></span> <span data-ttu-id="17918-159">たとえば、次の図では、パッケージ B のバージョン 2.0 はいとこの 1.0 以上という制約を満たすので、バージョン 2.0 が使われます。</span><span class="sxs-lookup"><span data-stu-id="17918-159">In the image below, for example, version 2.0 of Package B satisfies the other >=1.0 constraint, and is thus used:</span></span>

![すべての制約を満たす最低バージョンを使う、いとこ依存関係の解決](media/projectJson-dependency-7.png)

<span data-ttu-id="17918-161">状況によっては、すべてのバージョン要件を満たすことができない場合があります。</span><span class="sxs-lookup"><span data-stu-id="17918-161">In some cases, it is not possible to meet all version requirements.</span></span> <span data-ttu-id="17918-162">次に示すように、パッケージ A ではパッケージ B 1.0 だけが必要であり、パッケージ C ではパッケージ B 2.0 以上が必要である場合、NuGet は依存関係を解決できずエラーを生成します。</span><span class="sxs-lookup"><span data-stu-id="17918-162">As shown below, if Package A requires exactly Package B 1.0 and Package C requires Package B >=2.0, then NuGet cannot resolve the dependencies and gives an error.</span></span>

![厳密なバージョン要件のために解決できない依存関係](media/projectJson-dependency-8.png)

<span data-ttu-id="17918-164">このような状況では、最上位のコンシューマー (アプリケーションまたはパッケージ) がパッケージ B に対する独自の直接依存関係を追加して、[最近優先](#nearest-wins)ルールが適用されるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="17918-164">In these situations, the top-level consumer (the application or package) should add its own direct dependency on Package B so that the [Nearest Wins](#nearest-wins) rule applies.</span></span>

## <a name="dependency-resolution-with-packagesconfig"></a><span data-ttu-id="17918-165">packages.config での依存関係の解決</span><span class="sxs-lookup"><span data-stu-id="17918-165">Dependency resolution with packages.config</span></span>

<span data-ttu-id="17918-166">`packages.config` では、プロジェクトの依存関係はフラット リストとして `packages.config` に書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="17918-166">With `packages.config`, a project's dependencies are written to `packages.config` as a flat list.</span></span> <span data-ttu-id="17918-167">これらのパッケージの依存関係も、同じリストに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="17918-167">Any dependencies of those packages are also written in the same list.</span></span> <span data-ttu-id="17918-168">パッケージがインストールされると、NuGet は `.csproj` ファイル、`app.config`、`web.config`、および他の個別ファイルも変更する場合があります。</span><span class="sxs-lookup"><span data-stu-id="17918-168">When packages are installed, NuGet might also modify the `.csproj` file, `app.config`, `web.config`, and other individual files.</span></span>

<span data-ttu-id="17918-169">`packages.config` の場合、NuGet は個々のパッケージのインストール中に依存関係の競合の解決を試みます。</span><span class="sxs-lookup"><span data-stu-id="17918-169">With `packages.config`, NuGet attempts to resolve dependency conflicts during the installation of each individual package.</span></span> <span data-ttu-id="17918-170">つまり、パッケージ B に依存するパッケージ A がインストールされていて、パッケージ B が別のものの依存関係として `packages.config` のリストに既に含まれる場合、NuGet は要求されているパッケージ B のバージョンを比較し、すべてのバージョン制約を満たすバージョンの発見を試みます。</span><span class="sxs-lookup"><span data-stu-id="17918-170">That is, if Package A is being installed and depends on Package B, and Package B is already listed in `packages.config` as a dependency of something else, NuGet compares the versions of Package B being requested and attempts to find a version that satisfies all version constraints.</span></span> <span data-ttu-id="17918-171">具体的には、NuGet は依存関係を満たす低い方の *major.minor* バージョンを選びます。</span><span class="sxs-lookup"><span data-stu-id="17918-171">Specifically, NuGet selects the lower *major.minor* version that satisfies dependencies.</span></span>

<span data-ttu-id="17918-172">既定では、2.7 以前の NuGet は最も高い "*パッチ*" バージョンを解決します (*major.minor.patch.build* 表記規則を使います)。</span><span class="sxs-lookup"><span data-stu-id="17918-172">By default, NuGet 2.7 and earlier resolves the highest *patch* version (using the *major.minor.patch.build* convention).</span></span> <span data-ttu-id="17918-173">[NuGet 2.8 以降](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)では、この動作が最低のパッチ バージョンを既定で探すように変更されています。</span><span class="sxs-lookup"><span data-stu-id="17918-173">[NuGet 2.8 and higher](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) changes this behavior to look for the lowest patch version by default.</span></span> <span data-ttu-id="17918-174">この設定は、`Nuget.Config` の `DependencyVersion` 属性およびコマンド ラインの `-DependencyVersion` スイッチで制御できます。</span><span class="sxs-lookup"><span data-stu-id="17918-174">You can control this setting through the `DependencyVersion` attribute in `Nuget.Config` and the `-DependencyVersion` switch on the command line.</span></span>  

<span data-ttu-id="17918-175">`packages.config` の依存関係解決プロセスは、大規模な依存関係グラフでは複雑になります。</span><span class="sxs-lookup"><span data-stu-id="17918-175">The `packages.config` process for resolving dependencies gets complicated for larger dependency graphs.</span></span> <span data-ttu-id="17918-176">パッケージの各新規インストールでは、グラフ全体を走査して、バージョン間の競合の可能性を明らかにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="17918-176">Each new package installation requires a traversal of the whole graph and raises the chance for version conflicts.</span></span> <span data-ttu-id="17918-177">競合が発生するときは、インストールが停止されて、プロジェクトは不明な状態のままになります (特に、プロジェクト ファイル自体への変更の可能性がある場合)。</span><span class="sxs-lookup"><span data-stu-id="17918-177">When a conflict occurs, installation is stopped, leaving the project in an indeterminate state, especially with potential modifications to the project file itself.</span></span> <span data-ttu-id="17918-178">他のパッケージ参照形式を使うと、このような問題はありません。</span><span class="sxs-lookup"><span data-stu-id="17918-178">This is not an issue when using other package reference formats.</span></span>


## <a name="managing-dependency-assets"></a><span data-ttu-id="17918-179">依存関係の資産の管理</span><span class="sxs-lookup"><span data-stu-id="17918-179">Managing dependency assets</span></span>

<span data-ttu-id="17918-180">`project.json` 形式または PackageReference 形式を使うと、依存関係から最上位レベルのプロジェクトへの資産のフローを制御できます。</span><span class="sxs-lookup"><span data-stu-id="17918-180">When using the `project.json` or PackageReference formats, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="17918-181">詳しくは、「[project.json reference](../Schema/project-json.md)」(project.json リファレンス) および「[Package references in project files](Package-References-in-Project-Files.md#controlling-dependency-assets)」(プロジェクト ファイルでのパッケージ参照) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="17918-181">For details, see [project.json](../Schema/project-json.md) and [Package references in project files](Package-References-in-Project-Files.md#controlling-dependency-assets).</span></span>

<span data-ttu-id="17918-182">最上位レベルのプロジェクト自体がパッケージである場合は、`include` および `exclude` 属性と `.nuspec` ファイルの依存関係リストを使って、このフローを制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="17918-182">When the top-level project is itself a package, you also have control over this flow by using the `include` and `exclude` attributes with dependencies listed in the `.nuspec` file.</span></span> <span data-ttu-id="17918-183">「.nuspec Reference」(.nuspec リファレンス) の「[Dependencies](../Schema/nuspec.md#dependencies)」(依存関係) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="17918-183">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="17918-184">参照の除外</span><span class="sxs-lookup"><span data-stu-id="17918-184">Excluding references</span></span>

<span data-ttu-id="17918-185">同じ名前のアセンブリがプロジェクト内の複数の箇所で参照されていて、設計時エラーおよびビルド時エラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="17918-185">There are scenarios in which assemblies with the same name might be referenced more than once in a project, producing design-time and build-time errors.</span></span> <span data-ttu-id="17918-186">あるプロジェクトは、`C.dll` のカスタム バージョンを含み、やはり `C.dll` を含むパッケージ C を参照しているものとします。</span><span class="sxs-lookup"><span data-stu-id="17918-186">Consider a project that contains a custom version of `C.dll`, and references Package C that also contains `C.dll`.</span></span> <span data-ttu-id="17918-187">同時に、このプロジェクトはパッケージ B にも依存しており、パッケージ B もパッケージ C と `C.dll` に依存しています。</span><span class="sxs-lookup"><span data-stu-id="17918-187">At the same time, the project also depends on Package B which also depends on Package C and `C.dll`.</span></span> <span data-ttu-id="17918-188">結果として、NuGet はどの `C.dll` を使えばよいのか決定できず、かといってパッケージ B もパッケージ C に依存しているため、プロジェクトでのパッケージ C に対する依存関係を単に削除するわけにもいきません。</span><span class="sxs-lookup"><span data-stu-id="17918-188">As a result, NuGet can't determine which `C.dll` to use, but you can't just remove the project's dependency on Package C because Package B also depends on it.</span></span>

<span data-ttu-id="17918-189">これを解決するには、必要な `C.dll` を直接参照し (または、適切なパッケージを参照している別のパッケージを使い)、すべての資産を除外するパッケージ C への依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="17918-189">To resolve this, you must directly reference the `C.dll` you want (or use another package that references the right one), and then add a dependency on Package C that excludes all its assets.</span></span> <span data-ttu-id="17918-190">これは、使われているパッケージ参照形式に応じて、次のように行われます。</span><span class="sxs-lookup"><span data-stu-id="17918-190">This is done as follows depending on the package reference format in use:</span></span>

- <span data-ttu-id="17918-191">[PackageReference](../consume-packages/package-references-in-project-files.md): 依存関係に `Exclude="All"` を追加します。</span><span class="sxs-lookup"><span data-stu-id="17918-191">[PackageReference](../consume-packages/package-references-in-project-files.md): add `Exclude="All"` in the dependency:</span></span>

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- <span data-ttu-id="17918-192">`packages.config`: 必要なバージョンの `C.dll` だけを参照するように、`.csproj` ファイルからパッケージ C への参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="17918-192">`packages.config`: remove the reference to PackageC from the `.csproj` file so that it references only the version of `C.dll` that you want.</span></span>
    
- <span data-ttu-id="17918-193">`project.json`: パッケージ C の依存関係に `"exclude" : "all"` を追加します。</span><span class="sxs-lookup"><span data-stu-id="17918-193">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="dependency-updates-during-package-install"></a><span data-ttu-id="17918-194">パッケージをインストールする間の依存関係の更新</span><span class="sxs-lookup"><span data-stu-id="17918-194">Dependency updates during package install</span></span> 

<span data-ttu-id="17918-195">2.4.x 以前の NuGet では、依存関係がプロジェクトに既に存在するパッケージがインストールされるときに、既存のバージョンが制約を満たしている場合であっても、バージョンの制約を満たす最新のバージョンに依存関係が更新されます。</span><span class="sxs-lookup"><span data-stu-id="17918-195">With NuGet 2.4.x and earlier, when a package is installed whose dependency already exists in the project, the dependency is updated to the latest version that satisfies the version constraints, even if the existing version also satisfies those constraints.</span></span> 

<span data-ttu-id="17918-196">たとえば、パッケージ A はパッケージ B に依存し、バージョン番号として 1.0 が指定されているものとします。</span><span class="sxs-lookup"><span data-stu-id="17918-196">For example, consider package A that depends on package B and specifies 1.0 for the version number.</span></span> <span data-ttu-id="17918-197">ソース リポジトリには、パッケージ B のバージョン 1.0、1.1、1.2 が含まれます。B のバージョン 1.0 が既に含まれるプロジェクトに A をインストールした場合、B はバージョン 1.2 に更新されます。</span><span class="sxs-lookup"><span data-stu-id="17918-197">The source repository contains both versions 1.0, 1.1, and 1.2 of package B. If A is installed in a project that already contains B version 1.0, then B is updated to version 1.2.</span></span> 

<span data-ttu-id="17918-198">NuGet 2.5 以降では、依存関係のバージョンが既に満たされている場合、他のパッケージのインストール中に依存関係は更新されません。</span><span class="sxs-lookup"><span data-stu-id="17918-198">With NuGet 2.5 and later, if a dependency version is already satisfied, the dependency isn't updated during other package installations.</span></span> 

<span data-ttu-id="17918-199">上と同じ例で、NuGet 2.5 以降のプロジェクトにパッケージ A をインストールすると、パッケージ B は既にバージョン制約を満たしているので 1.0 のままになります。</span><span class="sxs-lookup"><span data-stu-id="17918-199">In the same example above, installing package A into a project with NuGet 2.5 and later leaves package B 1.0 in the project, as it already satisfies the version constraint.</span></span> <span data-ttu-id="17918-200">ただし、パッケージ A で B のバージョン 1.1 以上が要求されていた場合は、B 1.2 がインストールします。</span><span class="sxs-lookup"><span data-stu-id="17918-200">However, if package A had requests version 1.1 or higher of B, then B 1.2 would be installed.</span></span> 

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="17918-201">互換性のないパッケージのエラーの解決</span><span class="sxs-lookup"><span data-stu-id="17918-201">Resolving incompatible package errors</span></span>

<span data-ttu-id="17918-202">パッケージの復元操作の間に、"1 つ以上のパッケージは <プロジェクトのターゲット フレームワーク> と互換性がありません" またはパッケージはプロジェクトのターゲット フレームワークと "互換性がありません" という内容のエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="17918-202">During a package restore operation, you may see the error "One or more packages are not compatible..." or that a package "is not compatible" with the project's target framework.</span></span>

<span data-ttu-id="17918-203">このエラーは、プロジェクトで参照されているパッケージの 1 つ以上が、プロジェクトのターゲット フレームワークをサポートしていることを示さない場合に発生します。つまり、パッケージの `lib` フォルダーには、プロジェクトと互換性のあるターゲット フレームワーク用の適切な DLL が含まれません </span><span class="sxs-lookup"><span data-stu-id="17918-203">This error occurs when one or more of the packages referenced in your project do not indicate that they support the project's target framework; that is, the package does not contain a suitable DLL in its `lib` folder for a target framework that is compatible with the project.</span></span> <span data-ttu-id="17918-204">(「[Target frameworks](../Schema/Target-Frameworks.md)」(ターゲット フレームワーク) をご覧ください)。</span><span class="sxs-lookup"><span data-stu-id="17918-204">(See [Target frameworks](../Schema/Target-Frameworks.md) for a list.)</span></span> 

<span data-ttu-id="17918-205">たとえば、プロジェクトのターゲットが `netstandard1.6` である場合に、`lib\net20` および `\lib\net45` フォルダーだけに DLL が含まれるパッケージをインストールしようとすると、パッケージおよび場合によっては依存関係に対し、次のようなメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="17918-205">For example, if a project targets `netstandard1.6` and you attempt to install a package that contains DLLs in only the `lib\net20` and `\lib\net45` folders, then you'll see messages like the following for the package and possibly its dependents:</span></span>

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

<span data-ttu-id="17918-206">互換性の問題を解決するには、次のいずれかのようにします。</span><span class="sxs-lookup"><span data-stu-id="17918-206">To resolve incompatibilities, do one of the following:</span></span>

- <span data-ttu-id="17918-207">使うパッケージでサポートされているフレームワークに、プロジェクトのターゲットを変更します。</span><span class="sxs-lookup"><span data-stu-id="17918-207">Retarget your project to a framework that is supported by the packages you want to use.</span></span>
- <span data-ttu-id="17918-208">パッケージの作成者に連絡し、協力して、選んだフレームワークに対するサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="17918-208">Contact the author of the packages and work with them to add support for your chosen framework.</span></span> <span data-ttu-id="17918-209">[nuget.org](https://www.nuget.org/) の各パッケージ リスト ページには、そのための **[Contact Owners]** リンクがあります。</span><span class="sxs-lookup"><span data-stu-id="17918-209">Each package listing page on [nuget.org](https://www.nuget.org/) has a **Contact Owners** link for this purpose.</span></span>
- <span data-ttu-id="17918-210">**お勧めしません**: パッケージ作成者と作業するときの一時的な解決策として、`netcore`、`netstandard`、および `netcoreapp` を対象とするプロジェクトでは、他のフレームワークを互換性があるものとして指定し、これらの他のフレームワークを対象とするパッケージを使うことができます。</span><span class="sxs-lookup"><span data-stu-id="17918-210">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="17918-211">[project.json のインポート](../Schema/project-json.md#imports)に関するページおよび [MSBuild 復元ターゲットの PackageTargetFallback](../Schema/msbuild-targets.md#packagetargetfallback) に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="17918-211">See [project.json imports](../Schema/project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../Schema/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="17918-212">この方法では予期しない動作が発生する可能性があるので、繰り返しますが、パッケージ作成者との共同作業または更新によってパッケージの非互換性を解決することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="17918-212">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>
