---
title: NuGet 1.3 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.3 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777125"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="ead86-103">NuGet 1.3 リリースノート</span><span class="sxs-lookup"><span data-stu-id="ead86-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="ead86-104">[NuGet 1.2 リリースノート](../release-notes/nuget-1.2.md)  | [NuGet 1.4 リリースノート](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="ead86-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="ead86-105">NuGet 1.3 は、2011年4月25日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="ead86-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="ead86-106">新機能</span><span class="sxs-lookup"><span data-stu-id="ead86-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="ead86-107">シンボルサーバー統合による合理化されるパッケージの作成</span><span class="sxs-lookup"><span data-stu-id="ead86-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="ead86-108">NuGet チームは、 [SymbolSource.org](http://www.symbolsource.org/) の担当者と提携して、パッケージと共にソースと PDB を簡単に公開する方法を提供しています。</span><span class="sxs-lookup"><span data-stu-id="ead86-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="ead86-109">これにより、パッケージのコンシューマーは、デバッガーでパッケージのソースにステップインできます。</span><span class="sxs-lookup"><span data-stu-id="ead86-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="ead86-110">詳細については、「 [シンボルパッケージの作成と発行](../create-packages/symbol-packages.md) 」を参照してください。ソースと共に NuGet パッケージを発行する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="ead86-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="ead86-111">また、この機能のライブデモについては、Mix11 で詳しく説明されている NuGet の一部としてもご覧いただけます。</span><span class="sxs-lookup"><span data-stu-id="ead86-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="ead86-112">この機能は、ビデオの20分のマークから完全に示されています。</span><span class="sxs-lookup"><span data-stu-id="ead86-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="ead86-113">`Open-PackagePage` コマンド</span><span class="sxs-lookup"><span data-stu-id="ead86-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="ead86-114">このコマンドを使用すると、パッケージマネージャーコンソール内からパッケージのプロジェクトページを簡単に取得できます。</span><span class="sxs-lookup"><span data-stu-id="ead86-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="ead86-115">また、パッケージのライセンス URL とレポートの不正使用ページを開くためのオプションも用意されています。</span><span class="sxs-lookup"><span data-stu-id="ead86-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="ead86-116">コマンドの構文は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ead86-116">The syntax for the command is:</span></span>

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

<span data-ttu-id="ead86-117">`-PassThru`オプションは、指定された URL の値を返すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="ead86-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="ead86-118">例 :</span><span class="sxs-lookup"><span data-stu-id="ead86-118">Examples:</span></span>

```
PM> Open-PackagePage Ninject
```

<span data-ttu-id="ead86-119">Ninject パッケージに指定されているプロジェクト URL をブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="ead86-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

```
PM> Open-PackagePage Ninject -License
```

<span data-ttu-id="ead86-120">Ninject パッケージに指定されているライセンス URL をブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="ead86-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

```
PM> Open-PackagePage Ninject -ReportAbuse
```

<span data-ttu-id="ead86-121">指定したパッケージの誤用を報告するために使用する、現在のパッケージソースの URL をブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="ead86-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

<span data-ttu-id="ead86-122">ブラウザーで URL を開かずに、$url の変数にライセンス URL を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="ead86-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="ead86-123">パフォーマンスの強化</span><span class="sxs-lookup"><span data-stu-id="ead86-123">Performance Improvements</span></span>

<span data-ttu-id="ead86-124">NuGet 1.3 では、パフォーマンスが大幅に向上しています。</span><span class="sxs-lookup"><span data-stu-id="ead86-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="ead86-125">NuGet 1.3 では、ローカルのユーザーごとのキャッシュを含めることにより、同じバージョンのパッケージが複数回ダウンロードされることを回避しています。</span><span class="sxs-lookup"><span data-stu-id="ead86-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="ead86-126">キャッシュには、[パッケージマネージャーの設定] ダイアログを使用してアクセスしたり、消去したりできます。</span><span class="sxs-lookup"><span data-stu-id="ead86-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![パッケージキャッシュ設定を含む NuGet オプションダイアログ](./media/nuget-options.png)

<span data-ttu-id="ead86-128">その他のパフォーマンスの向上には、HTTP 圧縮のサポートの追加と、Visual Studio 内でのパッケージのインストール速度の向上が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ead86-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="ead86-129">Visual Studio と nuget.exe は、同じパッケージソースの一覧を使用します。</span><span class="sxs-lookup"><span data-stu-id="ead86-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="ead86-130">NuGet 1.3 より前では、nuget.exe によって使用されているパッケージソースの一覧と NuGet Visual Studio Add-In が同じ場所に格納されていませんでした。</span><span class="sxs-lookup"><span data-stu-id="ead86-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="ead86-131">NuGet 1.3 では、両方の場所で同じリストが使用されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ead86-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="ead86-132">リストはに格納され、 `NuGet.Config` AppData フォルダーに格納されます。</span><span class="sxs-lookup"><span data-stu-id="ead86-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="ead86-133">既定では、'. ' で始まるファイルとフォルダーは無視され nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ead86-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="ead86-134">NuGet を Subversion や Mercurial などのソース管理システムで適切に機能させるために、nuget.exe では、パッケージの作成時に '. ' 文字で始まるフォルダーやファイルは無視されます。</span><span class="sxs-lookup"><span data-stu-id="ead86-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="ead86-135">これは、2つの新しいフラグを使用してオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="ead86-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="ead86-136">__-Nodefaultexcludes__ は、この設定を上書きし、すべてのファイルを含めるために使用されます。</span><span class="sxs-lookup"><span data-stu-id="ead86-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="ead86-137">__-Exclude__ は、パターンを使用して除外する他のファイルやフォルダーを追加するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="ead86-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="ead86-138">たとえば、".bak" ファイル拡張子を持つすべてのファイルを除外するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="ead86-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="ead86-139">_注: 既定では、パターンは再帰的ではありません。_</span><span class="sxs-lookup"><span data-stu-id="ead86-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="ead86-140">WiX プロジェクトと .NET Micro Framework のサポート</span><span class="sxs-lookup"><span data-stu-id="ead86-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="ead86-141">コミュニティへの投稿により、NuGet には、WiX プロジェクトの種類と .NET Micro Framework のサポートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ead86-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ead86-142">バグの修正</span><span class="sxs-lookup"><span data-stu-id="ead86-142">Bug Fixes</span></span>

<span data-ttu-id="ead86-143">バグ修正の完全な一覧については、 [このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="ead86-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="ead86-144">バグの修正に値する注意点</span><span class="sxs-lookup"><span data-stu-id="ead86-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="ead86-145">ソースファイルを含むパッケージは、Web サイトと Web アプリケーションプロジェクトの両方で動作します。</span><span class="sxs-lookup"><span data-stu-id="ead86-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="ead86-146">Web サイトの場合、ソースファイルはフォルダーにコピーされます。 `App_Code`</span><span class="sxs-lookup"><span data-stu-id="ead86-146">For Websites, source files are copied into the `App_Code` folder</span></span>
