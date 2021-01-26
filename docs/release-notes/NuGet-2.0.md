---
title: NuGet 2.0 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.0 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776989"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="9cf7a-103">NuGet 2.0 リリースノート</span><span class="sxs-lookup"><span data-stu-id="9cf7a-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="9cf7a-104">[NuGet 1.8 リリースノート](../release-notes/nuget-1.8.md)  | [NuGet 2.1 リリースノート](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="9cf7a-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="9cf7a-105">NuGet 2.0 は、2012年6月19日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="9cf7a-106">インストールに関する既知の問題</span><span class="sxs-lookup"><span data-stu-id="9cf7a-106">Known Installation Issue</span></span>
<span data-ttu-id="9cf7a-107">VS 2010 SP1 を実行している場合は、以前のバージョンがインストールされている場合に NuGet をアップグレードしようとすると、インストールエラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="9cf7a-108">この回避策は、単純に NuGet をアンインストールし、VS 拡張機能ギャラリーからインストールすることです。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="9cf7a-109">詳細については、「」を参照 <https://support.microsoft.com/kb/2581019> するか、 [VS 修正プログラムに直接アクセス](http://bit.ly/vsixcertfix)してください。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="9cf7a-110">注: Visual Studio で拡張機能をアンインストールできない場合 ([アンインストール] ボタンが無効になっている場合)、"管理者として実行" を使用して Visual Studio を再起動する必要が生じる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="9cf7a-111">パッケージの復元の同意がアクティブになりました</span><span class="sxs-lookup"><span data-stu-id="9cf7a-111">Package restore consent is now active</span></span>

<span data-ttu-id="9cf7a-112">パッケージの復元 [の同意に関するこの記事](http://blog.nuget.org/20120518/package-restore-and-consent.html)で説明されているように、NuGet 2.0 では、パッケージの復元をオンラインにしてパッケージをダウンロードできるようにするための同意が必要になります。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="9cf7a-113">パッケージマネージャーの構成ダイアログまたは EnableNuGetPackageRestore 環境変数のいずれかを使用して同意したことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="9cf7a-114">ターゲットフレームワークによる依存関係のグループ化</span><span class="sxs-lookup"><span data-stu-id="9cf7a-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="9cf7a-115">バージョン2.0 以降では、パッケージの依存関係はターゲットプロジェクトのフレームワークプロファイルによって異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="9cf7a-116">これは、更新されたスキーマを使用して実現され `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="9cf7a-117">`<dependencies>`要素に要素のセットを含めることができるようになりました `<group>` 。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="9cf7a-118">各グループには、0個以上 `<dependency>` の要素と1つの属性が含まれてい `targetFramework` ます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="9cf7a-119">ターゲットフレームワークがターゲットプロジェクトフレームワークプロファイルと互換性がある場合、グループ内のすべての依存関係が一緒にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="9cf7a-120">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-120">For example:</span></span>

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

<span data-ttu-id="9cf7a-121">グループには、 **0 個** の依存関係を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="9cf7a-122">上記の例では、パッケージが Silverlight 3.0 以降を対象とするプロジェクトにインストールされている場合、依存関係はインストールされません。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="9cf7a-123">パッケージが .NET 4.0 以降を対象とするプロジェクトにインストールされている場合は、jQuery と WebActivator の2つの依存関係がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="9cf7a-124">パッケージが、これら2つのフレームワークの初期バージョンまたはその他のフレームワークを対象とするプロジェクトにインストールされている場合は、RouteMagic 1.1.0 がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="9cf7a-125">グループ間に継承はありません。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-125">There is no inheritance between groups.</span></span> <span data-ttu-id="9cf7a-126">プロジェクトのターゲットフレームワークがグループの属性と一致する場合 `targetFramework` 、そのグループ内の依存関係のみがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="9cf7a-127">パッケージは、次の2つの形式のいずれかでパッケージの依存関係を指定できます。1つは、要素の単純なリストの古い形式です。 `<dependency>`</span><span class="sxs-lookup"><span data-stu-id="9cf7a-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="9cf7a-128">形式が使用されている場合は、 `<group>` 2.0 より前のバージョンの NuGet にパッケージをインストールすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="9cf7a-129">2つの形式を混在させることはできません。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="9cf7a-130">たとえば、次のスニペットは **無効** であり、NuGet によって拒否されます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="9cf7a-131">ターゲットフレームワークによるコンテンツファイルと PowerShell スクリプトのグループ化</span><span class="sxs-lookup"><span data-stu-id="9cf7a-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="9cf7a-132">アセンブリ参照だけでなく、コンテンツファイルと PowerShell スクリプトをターゲットフレームワーク別にグループ化することもできます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="9cf7a-133">ターゲットフレームワークを指定するためにフォルダーで見つかったものと同じフォルダー構造を、フォルダー `lib` とフォルダーに対して同じ方法で適用できるようになりました `content` `tools` 。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="9cf7a-134">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-134">For example:</span></span>

```
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
```

<span data-ttu-id="9cf7a-135">**注**: `init.ps1` はソリューションレベルで実行され、個々のプロジェクトに依存しないため、フォルダーの直下に配置する必要があり `tools` ます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="9cf7a-136">フレームワーク固有のフォルダー内に配置されている場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="9cf7a-137">また、NuGet 2.0 の新機能として、フレームワークフォルダーを *空* にすることができます。この場合、nuget では、アセンブリ参照の追加、コンテンツファイルの追加、特定のフレームワークバージョンの PowerShell スクリプトの実行は行われません。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="9cf7a-138">上記の例では、フォルダー `content\net40` は空です。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="9cf7a-139">タブ補完のパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="9cf7a-139">Improved tab completion performance</span></span>
<span data-ttu-id="9cf7a-140">NuGet パッケージマネージャーコンソールのタブ補完機能が更新され、パフォーマンスが大幅に向上しました。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="9cf7a-141">[候補] ドロップダウンが表示されるまで、tab キーが押されるまでにかかる時間が大幅に短縮されます。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="9cf7a-142">バグの修正</span><span class="sxs-lookup"><span data-stu-id="9cf7a-142">Bug Fixes</span></span>
<span data-ttu-id="9cf7a-143">NuGet 2.0 には、パッケージの復元の同意とパフォーマンスを重視した多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="9cf7a-144">NuGet 2.0 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9cf7a-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
