---
title: "NuGet 1.3 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.3 リリース ノートです。"
keywords: "NuGet 1.3 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="2f77e-104">NuGet 1.3 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="2f77e-104">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="2f77e-105">[NuGet 1.2 リリース ノート](../release-notes/nuget-1.2.md) | [NuGet 1.4 のリリース ノート](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="2f77e-105">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="2f77e-106">NuGet 1.3 は、2011 年 4 月 25 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="2f77e-106">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="2f77e-107">新機能</span><span class="sxs-lookup"><span data-stu-id="2f77e-107">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="2f77e-108">シンボル サーバーの統合パッケージの作成を簡素化</span><span class="sxs-lookup"><span data-stu-id="2f77e-108">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="2f77e-109">チームと提携して NuGet チーム[SymbolSource.org](http://www.symbolsource.org/)をソースと PDB をパッケージと共に公開の非常に簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="2f77e-109">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="2f77e-110">これにより、パッケージのコンシューマーは、デバッガーでは、パッケージのソースにステップ インできます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-110">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="2f77e-111">詳細については、読み取り[の作成とシンボル パッケージを公開する](../create-packages/symbol-packages.md)ソースと NuGet パッケージを公開する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="2f77e-111">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="2f77e-112">ライブ デモについてこの機能の深さで NuGet の一部として Mix11 話しも監視できます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-112">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="2f77e-113">この機能は完全にビデオの 20 分間のマークで始まる説明します。</span><span class="sxs-lookup"><span data-stu-id="2f77e-113">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="2f77e-114">`Open-PackagePage`コマンド</span><span class="sxs-lookup"><span data-stu-id="2f77e-114">`Open-PackagePage` Command</span></span>

<span data-ttu-id="2f77e-115">このコマンドでは、簡単に、パッケージ マネージャー コンソール内からパッケージのプロジェクト ページにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-115">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="2f77e-116">ライセンスの URL と、不正使用のレポート ページ、パッケージを開くオプションも用意されています。</span><span class="sxs-lookup"><span data-stu-id="2f77e-116">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="2f77e-117">コマンドの構文です。</span><span class="sxs-lookup"><span data-stu-id="2f77e-117">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="2f77e-118">`-PassThru`オプションを使用して、指定された URL の値を返します。</span><span class="sxs-lookup"><span data-stu-id="2f77e-118">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="2f77e-119">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2f77e-119">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="2f77e-120">Ninject パッケージで指定されたプロジェクト URL をブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-120">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="2f77e-121">Ninject パッケージで指定されたライセンス URL をブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-121">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="2f77e-122">指定したパッケージの不正使用を報告に使用される現在のパッケージ ソースで URL をブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-122">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="2f77e-123">ブラウザーで URL を開かずに、その変数 $url にライセンス URL を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-123">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="2f77e-124">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="2f77e-124">Performance Improvements</span></span>

<span data-ttu-id="2f77e-125">NuGet 1.3 では、多数のパフォーマンスの向上について説明します。</span><span class="sxs-lookup"><span data-stu-id="2f77e-125">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="2f77e-126">NuGet 1.3 では、ユーザーごとのローカル キャッシュを含めることによって、同じバージョンのパッケージを複数回ダウンロードを回避できます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-126">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="2f77e-127">キャッシュのアクセスし、パッケージ マネージャーの設定ダイアログを介したクリアできます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-127">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![NuGet パッケージ キャッシュの設定で [オプション] ダイアログ](./media/nuget-options.png)

<span data-ttu-id="2f77e-129">その他のパフォーマンスの向上には、HTTP 圧縮サポートを追加して、Visual Studio でパッケージのインストールの処理速度の向上が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-129">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="2f77e-130">Visual Studio と nuget.exe 同じパッケージ ソースの一覧を使用します。</span><span class="sxs-lookup"><span data-stu-id="2f77e-130">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="2f77e-131">NuGet 1.3 の前に同じ場所に nuget.exe と NuGet Visual Studio アドインで使用されるパッケージ ソースの一覧を保持できませんでした。</span><span class="sxs-lookup"><span data-stu-id="2f77e-131">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="2f77e-132">今すぐ NuGet 1.3 は両方の場所で同じリストを使用します。</span><span class="sxs-lookup"><span data-stu-id="2f77e-132">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="2f77e-133">一覧に入っている`NuGet.Config`AppData フォルダーに格納されているとします。</span><span class="sxs-lookup"><span data-stu-id="2f77e-133">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="2f77e-134">nuget.exe 無視ファイルとフォルダーで始まる '.' 既定</span><span class="sxs-lookup"><span data-stu-id="2f77e-134">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="2f77e-135">NuGet Subversion と Mercurial のようなソース管理システムで機能するために、nuget.exe を無視ファイルとフォルダーの開始が、'.' 文字のパッケージを作成するときにします。</span><span class="sxs-lookup"><span data-stu-id="2f77e-135">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="2f77e-136">これは、次の 2 つの新しいフラグを使用してオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="2f77e-136">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="2f77e-137">__-NoDefaultExcludes__にこの設定を上書きし、すべてのファイルを含めるために使用します。</span><span class="sxs-lookup"><span data-stu-id="2f77e-137">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="2f77e-138">__-除外__パターンの使用を除外するファイルとフォルダーは、他の追加に使用します。</span><span class="sxs-lookup"><span data-stu-id="2f77e-138">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="2f77e-139">たとえば、".bak 拡張子を持つすべてのファイルを除外するには</span><span class="sxs-lookup"><span data-stu-id="2f77e-139">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="2f77e-140">_注: パターンは、既定では再帰的ではありません。_</span><span class="sxs-lookup"><span data-stu-id="2f77e-140">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="2f77e-141">WiX プロジェクトと .NET マイクロ Framework のサポート</span><span class="sxs-lookup"><span data-stu-id="2f77e-141">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="2f77e-142">コミュニティの皆様に感謝 NuGet には、WiX プロジェクトの種類だけでなく、.NET マイクロ Framework のサポートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="2f77e-142">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="2f77e-143">バグ修正</span><span class="sxs-lookup"><span data-stu-id="2f77e-143">Bug Fixes</span></span>

<span data-ttu-id="2f77e-144">バグの修正プログラムの一覧についてを参照してください、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="2f77e-144">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="2f77e-145">注目すべきバグ修正</span><span class="sxs-lookup"><span data-stu-id="2f77e-145">Bug fixes worth noting</span></span>

* <span data-ttu-id="2f77e-146">パッケージのソース ファイルには、両方の web サイトおよび Web アプリケーション プロジェクト機能します。</span><span class="sxs-lookup"><span data-stu-id="2f77e-146">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="2f77e-147">Web サイトのソース ファイルのコピー、`App_Code`フォルダー</span><span class="sxs-lookup"><span data-stu-id="2f77e-147">For Websites, source files are copied into the `App_Code` folder</span></span>
