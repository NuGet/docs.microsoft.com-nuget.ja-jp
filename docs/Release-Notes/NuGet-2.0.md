---
title: "NuGet 2.0 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.0 のリリース ノートします。"
keywords: "NuGet 2.0 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eaa3c8db1cce72ff93671a1df63698748cdfab70
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="a407f-104">NuGet 2.0 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="a407f-104">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="a407f-105">[NuGet 1.8 リリース ノート](../release-notes/nuget-1.8.md) | [NuGet 2.1 リリース ノート](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="a407f-105">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="a407f-106">NuGet 2.0 は、2012 年 6 月 19 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="a407f-106">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="a407f-107">インストールの既知の問題</span><span class="sxs-lookup"><span data-stu-id="a407f-107">Known Installation Issue</span></span>
<span data-ttu-id="a407f-108">VS 2010 SP1 を実行している場合、インストールされている古いバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーに発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a407f-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="a407f-109">回避策では、NuGet をシンプルにアンインストールし、VS 拡張機能ギャラリーからインストールします。</span><span class="sxs-lookup"><span data-stu-id="a407f-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="a407f-110">参照してください[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)詳細については、または[VS 修正プログラムに直接進んで](http://bit.ly/vsixcertfix)です。</span><span class="sxs-lookup"><span data-stu-id="a407f-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="a407f-111">注意: Visual Studio には、(削除 ボタンは無効になっている) 拡張機能をアンインストールすることを許可しません、可能性の高い場合"管理者として実行 を使用して Visual Studio を再起動するには</span><span class="sxs-lookup"><span data-stu-id="a407f-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="a407f-112">パッケージ復元同意はアクティブになりました</span><span class="sxs-lookup"><span data-stu-id="a407f-112">Package restore consent is now active</span></span>

<span data-ttu-id="a407f-113">この」の説明に従って[パッケージ復元同意に投稿](http://blog.nuget.org/20120518/package-restore-and-consent.html)、NuGet 2.0 は、同意がオンラインでパッケージをダウンロードするパッケージの復元を有効に指定する必要がありますようになりました。</span><span class="sxs-lookup"><span data-stu-id="a407f-113">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="a407f-114">パッケージ マネージャーの構成 ダイアログまたは EnableNuGetPackageRestore 環境変数のどちらか経由での同意を入力したことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="a407f-114">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="a407f-115">ターゲット フレームワークでグループの依存関係</span><span class="sxs-lookup"><span data-stu-id="a407f-115">Group dependencies by target frameworks</span></span>

<span data-ttu-id="a407f-116">バージョン 2.0 以降では、パッケージの依存関係が異なる場合は、ターゲット プロジェクトのフレームワークのプロファイルに基づいています。</span><span class="sxs-lookup"><span data-stu-id="a407f-116">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="a407f-117">これは、更新された`.nuspec`スキーマです。</span><span class="sxs-lookup"><span data-stu-id="a407f-117">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="a407f-118">`<dependencies>`要素のセットを含めるようになりましたことができます`<group>`要素。</span><span class="sxs-lookup"><span data-stu-id="a407f-118">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="a407f-119">各グループは、0 個以上含まれています。`<dependency>`要素および`targetFramework`属性。</span><span class="sxs-lookup"><span data-stu-id="a407f-119">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="a407f-120">ターゲット フレームワークをプロジェクトのターゲット フレームワーク プロファイルと互換性がある場合、グループ内のすべての依存関係が一緒にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a407f-120">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="a407f-121">例:</span><span class="sxs-lookup"><span data-stu-id="a407f-121">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="a407f-122">グループを含めることができる注**0**の依存関係。</span><span class="sxs-lookup"><span data-stu-id="a407f-122">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="a407f-123">上記の例では、パッケージが Silverlight 3.0 を対象とするプロジェクトにインストールされているか、後で、場合の依存関係はインストールされません。</span><span class="sxs-lookup"><span data-stu-id="a407f-123">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="a407f-124">パッケージがインストール先を .NET 4.0 を対象とするプロジェクトまたはそれ以降の場合は、次の 2 つの依存関係、jQuery、および WebActivator がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a407f-124">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="a407f-125">パッケージが、以前のバージョンのこれら 2 つのフレームワークまたはその他の任意のフレームワークを対象とするプロジェクトにインストールされている場合は、RouteMagic 1.1.0 がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a407f-125">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="a407f-126">グループ間の継承はありません。</span><span class="sxs-lookup"><span data-stu-id="a407f-126">There is no inheritance between groups.</span></span> <span data-ttu-id="a407f-127">プロジェクトのターゲット フレームワークと一致する場合、`targetFramework`グループ、そのグループ内の依存関係のみの属性はインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a407f-127">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="a407f-128">パッケージは、2 つの形式のいずれかでパッケージの依存関係を指定できます: 旧形式の単純なリストの`<dependency>`要素、またはグループ。</span><span class="sxs-lookup"><span data-stu-id="a407f-128">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="a407f-129">場合、`<group>`形式が使用される、2.0 より前のバージョンの NuGet パッケージをインストールすることはできません。</span><span class="sxs-lookup"><span data-stu-id="a407f-129">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="a407f-130">2 つの形式を混在させるを使用できないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a407f-130">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="a407f-131">たとえば、次のスニペットは**無効な**とは、NuGet によって拒否されます。</span><span class="sxs-lookup"><span data-stu-id="a407f-131">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="a407f-132">ターゲット フレームワークでコンテンツ ファイルおよび PowerShell スクリプトをグループ化</span><span class="sxs-lookup"><span data-stu-id="a407f-132">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="a407f-133">アセンブリの参照に加えてターゲット フレームワークではコンテンツ ファイルおよび PowerShell スクリプトのグループ化をもできます。</span><span class="sxs-lookup"><span data-stu-id="a407f-133">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="a407f-134">同じフォルダー構造がで見つかった、`lib`ターゲット フレームワークを指定するためのフォルダーに同じ方法で適用できます、`content`と`tools`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="a407f-134">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="a407f-135">例:</span><span class="sxs-lookup"><span data-stu-id="a407f-135">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="a407f-136">**注**: ため`init.ps1`ソリューション レベルで実行され、は、個々 のプロジェクトには依存しない、配置しなければなりません直下にある、`tools`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="a407f-136">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="a407f-137">フレームワーク固有のフォルダー内で、配置している場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="a407f-137">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="a407f-138">フレームワーク フォルダーがあることを NuGet 2.0 の新機能はまた、*空*、この場合は、NuGet はいないアセンブリ参照を追加、コンテンツ ファイルを追加または特定のフレームワークのバージョンの PowerShell スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="a407f-138">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="a407f-139">フォルダー上の例で`content\net40`が空です。</span><span class="sxs-lookup"><span data-stu-id="a407f-139">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="a407f-140">強化されたタブ補完のパフォーマンス</span><span class="sxs-lookup"><span data-stu-id="a407f-140">Improved tab completion performance</span></span>
<span data-ttu-id="a407f-141">NuGet パッケージ マネージャー コンソールの tab 補完機能が大幅にパフォーマンスを向上させる更新されました。</span><span class="sxs-lookup"><span data-stu-id="a407f-141">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="a407f-142">修正候補のドロップダウン リストが表示されるまで tab キーが押された時間の間には、はるかに少ない遅延があります。</span><span class="sxs-lookup"><span data-stu-id="a407f-142">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a407f-143">バグ修正</span><span class="sxs-lookup"><span data-stu-id="a407f-143">Bug Fixes</span></span>
<span data-ttu-id="a407f-144">NuGet 2.0 には、パッケージの復元の同意画面およびパフォーマンスに重点を置いて、多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a407f-144">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="a407f-145">作業の完全な一覧の項目で修正 NuGet 2.0 では、くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="a407f-145">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
