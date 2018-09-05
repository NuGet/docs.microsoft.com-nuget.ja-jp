---
title: NuGet の 1.3 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.3 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551352"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="f7a18-103">NuGet の 1.3 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="f7a18-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="f7a18-104">[NuGet 1.2 リリース ノート](../release-notes/nuget-1.2.md) | [NuGet 1.4 のリリース ノート](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="f7a18-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="f7a18-105">NuGet 1.3 は、2011 年 4 月 25 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="f7a18-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="f7a18-106">新機能</span><span class="sxs-lookup"><span data-stu-id="f7a18-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="f7a18-107">シンボル サーバーの統合を簡素化されたパッケージの作成</span><span class="sxs-lookup"><span data-stu-id="f7a18-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="f7a18-108">開発者と提携して、NuGet チーム[SymbolSource.org](http://www.symbolsource.org/)と共に、パッケージの公開、ソースとの PDB の非常に簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="f7a18-109">これにより、デバッガーでパッケージのソースにステップ インするパッケージのコンシューマーができます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="f7a18-110">詳細については、「[の作成とシンボル パッケージを公開](../create-packages/symbol-packages.md)ソースと NuGet パッケージを公開する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="f7a18-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="f7a18-111">ライブ デモについてこの機能の深さで NuGet の一部として Mix11 講演を視聴することもできます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="f7a18-112">ビデオの 20 分後に開始、この機能が完全に示します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="f7a18-113">`Open-PackagePage` コマンド</span><span class="sxs-lookup"><span data-stu-id="f7a18-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="f7a18-114">このコマンドでは、簡単にパッケージ マネージャー コンソール内からパッケージのプロジェクト ページを表示できます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="f7a18-115">ライセンスの URL と、パッケージのレポートの不正使用のページを開くためのオプションも提供します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="f7a18-116">コマンドの構文です。</span><span class="sxs-lookup"><span data-stu-id="f7a18-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="f7a18-117">`-PassThru`オプションを使用して、指定した URL の値を返します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="f7a18-118">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="f7a18-119">Ninject パッケージで指定されたプロジェクトの URL をブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="f7a18-120">Ninject パッケージで指定されたライセンスの URL にブラウザーを開きます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="f7a18-121">指定したパッケージの不正使用を報告するために使用、現在のパッケージ ソース URL をブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="f7a18-122">ブラウザーで URL を開くことがなく、変数 $url にライセンス URL を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="f7a18-123">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="f7a18-123">Performance Improvements</span></span>

<span data-ttu-id="f7a18-124">NuGet 1.3 では、多数のパフォーマンスの機能強化について説明します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="f7a18-125">NuGet 1.3 では、ユーザーごとのローカル キャッシュを含めることによって、同じバージョンのパッケージを複数回のダウンロードを回避できます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="f7a18-126">キャッシュのアクセスおよびパッケージ マネージャー設定 ダイアログでクリアできます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![NuGet のパッケージ キャッシュの設定のオプション ダイアログ ボックス](./media/nuget-options.png)

<span data-ttu-id="f7a18-128">その他のパフォーマンスの向上には、HTTP 圧縮のサポートを追加して、Visual Studio 内でパッケージのインストールの処理速度の向上が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="f7a18-129">Visual Studio と nuget.exe 同じパッケージ ソースのリストを使用します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="f7a18-130">NuGet 1.3 では、前に、nuget.exe および NuGet Visual Studio アドインで使用されるパッケージ ソースの一覧は、同じ場所に保持できませんでした。</span><span class="sxs-lookup"><span data-stu-id="f7a18-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="f7a18-131">今すぐ、NuGet 1.3 は、両方の場所で同じリストを使用します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="f7a18-132">一覧が格納されている`NuGet.Config`AppData フォルダーに格納されているとします。</span><span class="sxs-lookup"><span data-stu-id="f7a18-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="f7a18-133">nuget.exe を無視ファイルとフォルダーで始まる '.' 既定</span><span class="sxs-lookup"><span data-stu-id="f7a18-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="f7a18-134">フォルダーとファイルで始まる NuGet Subversion と Mercurial のようなソース管理システムでうまく動作するために、nuget.exe を無視します '.' パッケージを作成するときに文字します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="f7a18-135">これは、2 つの新しいフラグを使用してオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="f7a18-136">__-NoDefaultExcludes__この設定を上書きし、すべてのファイルを含めるために使用します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="f7a18-137">__-除外__パターンを使用してを除外するファイルとフォルダーは、他の追加に使用されます。</span><span class="sxs-lookup"><span data-stu-id="f7a18-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="f7a18-138">たとえば、".bak"ファイル拡張子を持つすべてのファイルを除外するには</span><span class="sxs-lookup"><span data-stu-id="f7a18-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="f7a18-139">_注: パターンは、既定では再帰ではありません。_</span><span class="sxs-lookup"><span data-stu-id="f7a18-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="f7a18-140">WiX プロジェクトと .NET Micro Framework のサポート</span><span class="sxs-lookup"><span data-stu-id="f7a18-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="f7a18-141">コミュニティへの投稿に協力してくれた NuGet には、WiX プロジェクトの種類に加えて、.NET Micro Framework のサポートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f7a18-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="f7a18-142">バグ修正</span><span class="sxs-lookup"><span data-stu-id="f7a18-142">Bug Fixes</span></span>

<span data-ttu-id="f7a18-143">バグの修正の完全な一覧を参照してください、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="f7a18-144">注目すべきバグの修正</span><span class="sxs-lookup"><span data-stu-id="f7a18-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="f7a18-145">パッケージ ソース ファイルでは、両方の web サイトでと Web アプリケーション プロジェクトで作業します。</span><span class="sxs-lookup"><span data-stu-id="f7a18-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="f7a18-146">Web サイトのソース ファイルのコピー、`App_Code`フォルダー</span><span class="sxs-lookup"><span data-stu-id="f7a18-146">For Websites, source files are copied into the `App_Code` folder</span></span>
