---
title: NuGet 2.0 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.0 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383068"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="27dc4-103">NuGet 2.0 リリースノート</span><span class="sxs-lookup"><span data-stu-id="27dc4-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="27dc4-104">Nuget [1.8 リリースノート](../release-notes/nuget-1.8.md) | [Nuget 2.1 リリースノート](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="27dc4-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="27dc4-105">NuGet 2.0 は、2012年6月19日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="27dc4-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="27dc4-106">インストールに関する既知の問題</span><span class="sxs-lookup"><span data-stu-id="27dc4-106">Known Installation Issue</span></span>
<span data-ttu-id="27dc4-107">VS 2010 SP1 を実行している場合は、以前のバージョンがインストールされている場合に NuGet をアップグレードしようとすると、インストールエラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="27dc4-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="27dc4-108">この回避策は、単純に NuGet をアンインストールし、VS 拡張機能ギャラリーからインストールすることです。</span><span class="sxs-lookup"><span data-stu-id="27dc4-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="27dc4-109">詳細については、「<https://support.microsoft.com/kb/2581019>」を参照するか、 [VS 修正プログラムに直接アクセス](http://bit.ly/vsixcertfix)してください。</span><span class="sxs-lookup"><span data-stu-id="27dc4-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="27dc4-110">注: Visual Studio で拡張機能をアンインストールできない場合 ([アンインストール] ボタンが無効になっている場合)、"管理者として実行" を使用して Visual Studio を再起動する必要が生じる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="27dc4-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="27dc4-111">パッケージの復元の同意がアクティブになりました</span><span class="sxs-lookup"><span data-stu-id="27dc4-111">Package restore consent is now active</span></span>

<span data-ttu-id="27dc4-112">パッケージの復元[の同意に関するこの記事](http://blog.nuget.org/20120518/package-restore-and-consent.html)で説明されているように、NuGet 2.0 では、パッケージの復元をオンラインにしてパッケージをダウンロードできるようにするための同意が必要になります。</span><span class="sxs-lookup"><span data-stu-id="27dc4-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="27dc4-113">パッケージマネージャーの構成ダイアログまたは EnableNuGetPackageRestore 環境変数のいずれかを使用して同意したことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="27dc4-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="27dc4-114">ターゲットフレームワークによる依存関係のグループ化</span><span class="sxs-lookup"><span data-stu-id="27dc4-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="27dc4-115">バージョン2.0 以降では、パッケージの依存関係はターゲットプロジェクトのフレームワークプロファイルによって異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="27dc4-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="27dc4-116">これは、更新された `.nuspec` スキーマを使用して実現されます。</span><span class="sxs-lookup"><span data-stu-id="27dc4-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="27dc4-117">`<dependencies>` 要素に `<group>` の要素のセットを含めることができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="27dc4-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="27dc4-118">各グループには、0個以上の `<dependency>` 要素と `targetFramework` 属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="27dc4-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="27dc4-119">ターゲットフレームワークがターゲットプロジェクトフレームワークプロファイルと互換性がある場合、グループ内のすべての依存関係が一緒にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="27dc4-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="27dc4-120">例:</span><span class="sxs-lookup"><span data-stu-id="27dc4-120">For example:</span></span>

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

<span data-ttu-id="27dc4-121">グループには、 **0 個**の依存関係を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="27dc4-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="27dc4-122">上記の例では、パッケージが Silverlight 3.0 以降を対象とするプロジェクトにインストールされている場合、依存関係はインストールされません。</span><span class="sxs-lookup"><span data-stu-id="27dc4-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="27dc4-123">パッケージが .NET 4.0 以降を対象とするプロジェクトにインストールされている場合は、jQuery と WebActivator の2つの依存関係がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="27dc4-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="27dc4-124">パッケージが、これら2つのフレームワークの初期バージョンまたはその他のフレームワークを対象とするプロジェクトにインストールされている場合は、RouteMagic 1.1.0 がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="27dc4-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="27dc4-125">グループ間に継承はありません。</span><span class="sxs-lookup"><span data-stu-id="27dc4-125">There is no inheritance between groups.</span></span> <span data-ttu-id="27dc4-126">プロジェクトのターゲットフレームワークがグループの `targetFramework` 属性と一致する場合、そのグループ内の依存関係のみがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="27dc4-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="27dc4-127">パッケージは、次の2つの形式のいずれかでパッケージの依存関係を指定できます。 `<dependency>` 要素の単純なリストの古い形式、またはグループです。</span><span class="sxs-lookup"><span data-stu-id="27dc4-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="27dc4-128">`<group>` 形式が使用されている場合、2.0 より前のバージョンの NuGet にパッケージをインストールすることはできません。</span><span class="sxs-lookup"><span data-stu-id="27dc4-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="27dc4-129">2つの形式を混在させることはできません。</span><span class="sxs-lookup"><span data-stu-id="27dc4-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="27dc4-130">たとえば、次のスニペットは**無効**であり、NuGet によって拒否されます。</span><span class="sxs-lookup"><span data-stu-id="27dc4-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="27dc4-131">ターゲットフレームワークによるコンテンツファイルと PowerShell スクリプトのグループ化</span><span class="sxs-lookup"><span data-stu-id="27dc4-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="27dc4-132">アセンブリ参照だけでなく、コンテンツファイルと PowerShell スクリプトをターゲットフレームワーク別にグループ化することもできます。</span><span class="sxs-lookup"><span data-stu-id="27dc4-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="27dc4-133">ターゲットフレームワークを指定するための `lib` フォルダーにある同じフォルダー構造を、`content` フォルダーと `tools` フォルダーに同じ方法で適用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="27dc4-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="27dc4-134">例:</span><span class="sxs-lookup"><span data-stu-id="27dc4-134">For example:</span></span>

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

<span data-ttu-id="27dc4-135">**注**: `init.ps1` はソリューションレベルで実行され、個々のプロジェクトに依存していないため、`tools` フォルダーの直下に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="27dc4-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="27dc4-136">フレームワーク固有のフォルダー内に配置されている場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="27dc4-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="27dc4-137">また、NuGet 2.0 の新機能として、フレームワークフォルダーを*空*にすることができます。この場合、nuget では、アセンブリ参照の追加、コンテンツファイルの追加、特定のフレームワークバージョンの PowerShell スクリプトの実行は行われません。</span><span class="sxs-lookup"><span data-stu-id="27dc4-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="27dc4-138">上記の例では、`content\net40` フォルダーは空です。</span><span class="sxs-lookup"><span data-stu-id="27dc4-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="27dc4-139">タブ補完のパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="27dc4-139">Improved tab completion performance</span></span>
<span data-ttu-id="27dc4-140">NuGet パッケージマネージャーコンソールのタブ補完機能が更新され、パフォーマンスが大幅に向上しました。</span><span class="sxs-lookup"><span data-stu-id="27dc4-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="27dc4-141">[候補] ドロップダウンが表示されるまで、tab キーが押されるまでにかかる時間が大幅に短縮されます。</span><span class="sxs-lookup"><span data-stu-id="27dc4-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="27dc4-142">バグ修正</span><span class="sxs-lookup"><span data-stu-id="27dc4-142">Bug Fixes</span></span>
<span data-ttu-id="27dc4-143">NuGet 2.0 には、パッケージの復元の同意とパフォーマンスを重視した多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="27dc4-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="27dc4-144">NuGet 2.0 で修正された作業項目の完全な一覧については、[このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="27dc4-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
