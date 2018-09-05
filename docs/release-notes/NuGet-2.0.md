---
title: NuGet 2.0 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.0 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547576"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="be90d-103">NuGet 2.0 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="be90d-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="be90d-104">[NuGet 1.8 のリリース ノート](../release-notes/nuget-1.8.md) | [NuGet 2.1 リリース ノート](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="be90d-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="be90d-105">NuGet 2.0 は、2012 年 6 月 19 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="be90d-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="be90d-106">インストールの既知の問題</span><span class="sxs-lookup"><span data-stu-id="be90d-106">Known Installation Issue</span></span>
<span data-ttu-id="be90d-107">VS 2010 SP1 を実行している場合は、インストールされている以前のバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーが発生実行可能性があります。</span><span class="sxs-lookup"><span data-stu-id="be90d-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="be90d-108">回避策では、単に NuGet をアンインストールしてから、VS 拡張ギャラリーからインストールします。</span><span class="sxs-lookup"><span data-stu-id="be90d-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="be90d-109">参照してください[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)詳細については、または[VS 修正プログラムに直接移動](http://bit.ly/vsixcertfix)します。</span><span class="sxs-lookup"><span data-stu-id="be90d-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="be90d-110">注: Visual Studio ([アンインストール] ボタンは無効です) 拡張機能をアンインストールすることができず、しの場合必要があります「管理者として実行」を使用して Visual Studio を再起動するには</span><span class="sxs-lookup"><span data-stu-id="be90d-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="be90d-111">パッケージの復元の同意はアクティブになりました</span><span class="sxs-lookup"><span data-stu-id="be90d-111">Package restore consent is now active</span></span>

<span data-ttu-id="be90d-112">この」の説明に従って[パッケージ復元の同意に投稿](http://blog.nuget.org/20120518/package-restore-and-consent.html)、NuGet 2.0 が同意するパッケージをダウンロードするパッケージの復元を有効にすることが必要になりました。</span><span class="sxs-lookup"><span data-stu-id="be90d-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="be90d-113">パッケージ マネージャーの構成 ダイアログまたは EnableNuGetPackageRestore 環境変数を使用して同意を入力したことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="be90d-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="be90d-114">ターゲット フレームワークによってグループの依存関係</span><span class="sxs-lookup"><span data-stu-id="be90d-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="be90d-115">バージョン 2.0 以降、パッケージの依存関係が異なる場合は、ターゲット プロジェクトのフレームワーク プロファイルに基づいています。</span><span class="sxs-lookup"><span data-stu-id="be90d-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="be90d-116">これは、更新された`.nuspec`スキーマ。</span><span class="sxs-lookup"><span data-stu-id="be90d-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="be90d-117">`<dependencies>`要素が現在のセットを含めることができます`<group>`要素。</span><span class="sxs-lookup"><span data-stu-id="be90d-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="be90d-118">各グループは、0 個以上含まれています。`<dependency>`要素と`targetFramework`属性。</span><span class="sxs-lookup"><span data-stu-id="be90d-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="be90d-119">ターゲット フレームワークがターゲット プロジェクトのフレームワーク プロファイルと互換性のある場合は、グループ内のすべての依存関係は一緒にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="be90d-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="be90d-120">例えば:</span><span class="sxs-lookup"><span data-stu-id="be90d-120">For example:</span></span>

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

<span data-ttu-id="be90d-121">グループに含めることができますに注意してください**0**依存関係。</span><span class="sxs-lookup"><span data-stu-id="be90d-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="be90d-122">上記の例では、パッケージが Silverlight 3.0 を対象とするプロジェクトにインストールされている以降の場合の依存関係はインストールされません。</span><span class="sxs-lookup"><span data-stu-id="be90d-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="be90d-123">パッケージが .NET 4.0 を対象とするプロジェクトにインストールされている、またはそれ以降の場合は、2 つの依存関係、jQuery、および WebActivator がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="be90d-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="be90d-124">これら 2 つのフレームワーク、またはその他のフレームワークの初期のバージョンを対象とするプロジェクトにパッケージがインストールされている、RouteMagic 1.1.0 がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="be90d-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="be90d-125">グループ間の継承はありません。</span><span class="sxs-lookup"><span data-stu-id="be90d-125">There is no inheritance between groups.</span></span> <span data-ttu-id="be90d-126">プロジェクトのターゲット フレームワークと一致する場合、`targetFramework`属性のグループ、そのグループ内の依存関係のみがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="be90d-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="be90d-127">パッケージは 2 つの形式のいずれかでパッケージの依存関係を指定することができます。 旧形式の単純なリストの`<dependency>`要素、またはグループ。</span><span class="sxs-lookup"><span data-stu-id="be90d-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="be90d-128">場合、`<group>`形式が使用される、2.0 より前のバージョンの NuGet にパッケージをインストールすることはできません。</span><span class="sxs-lookup"><span data-stu-id="be90d-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="be90d-129">2 つの形式の混在が許可されないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="be90d-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="be90d-130">たとえば、次のスニペットは**無効な**NuGet によって拒否されます。</span><span class="sxs-lookup"><span data-stu-id="be90d-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="be90d-131">ターゲット フレームワークによって、コンテンツ ファイルと PowerShell スクリプトをグループ化</span><span class="sxs-lookup"><span data-stu-id="be90d-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="be90d-132">アセンブリの参照だけでなくターゲット フレームワークによってはコンテンツ ファイルと PowerShell スクリプトのグループ化をもできます。</span><span class="sxs-lookup"><span data-stu-id="be90d-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="be90d-133">同じフォルダー構造がある、`lib`ターゲット フレームワークを指定するためのフォルダーを同じ方法で適用できる、`content`と`tools`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="be90d-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="be90d-134">例えば:</span><span class="sxs-lookup"><span data-stu-id="be90d-134">For example:</span></span>

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

<span data-ttu-id="be90d-135">**注**: ため`init.ps1`はソリューション レベルで実行、個々 のプロジェクトには依存しないを置く必要がありますの直下にある、`tools`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="be90d-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="be90d-136">、フレームワーク固有のフォルダーに配置している場合は、これは無視されます。</span><span class="sxs-lookup"><span data-stu-id="be90d-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="be90d-137">また、NuGet 2.0 の新機能は、フレームワーク フォルダーができる*空*、する場合は、NuGet はないアセンブリ参照を追加、コンテンツ ファイルを追加または特定のフレームワークのバージョンの PowerShell スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="be90d-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="be90d-138">フォルダーの上の例では`content\net40`が空です。</span><span class="sxs-lookup"><span data-stu-id="be90d-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="be90d-139">強化されたタブ補完のパフォーマンス</span><span class="sxs-lookup"><span data-stu-id="be90d-139">Improved tab completion performance</span></span>
<span data-ttu-id="be90d-140">NuGet パッケージ マネージャー コンソールの tab 補完機能が大幅にパフォーマンスを向上させる更新されました。</span><span class="sxs-lookup"><span data-stu-id="be90d-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="be90d-141">修正候補のドロップダウンが表示されるまで tab キーが押された時間の間には、はるかに少ない遅延があります。</span><span class="sxs-lookup"><span data-stu-id="be90d-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="be90d-142">バグ修正</span><span class="sxs-lookup"><span data-stu-id="be90d-142">Bug Fixes</span></span>
<span data-ttu-id="be90d-143">NuGet 2.0 には、パッケージ復元の同意とパフォーマンスを重視した多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="be90d-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="be90d-144">作業の完全な一覧の項目で修正された NuGet 2.0 では、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)します。</span><span class="sxs-lookup"><span data-stu-id="be90d-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
