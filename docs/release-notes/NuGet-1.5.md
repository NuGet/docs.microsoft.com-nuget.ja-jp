---
title: NuGet 1.5 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.5 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777092"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="c9982-103">NuGet 1.5 リリースノート</span><span class="sxs-lookup"><span data-stu-id="c9982-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="c9982-104">[NuGet 1.4 リリースノート](../release-notes/nuget-1.4.md)  | [NuGet 1.6 リリースノート](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="c9982-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="c9982-105">NuGet 1.5 は、2011年8月30日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="c9982-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="c9982-106">特徴</span><span class="sxs-lookup"><span data-stu-id="c9982-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="c9982-107">NuGet パッケージがプレインストールされるプロジェクトテンプレート</span><span class="sxs-lookup"><span data-stu-id="c9982-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="c9982-108">新しい ASP.NET MVC 3 プロジェクトテンプレートを作成する場合、プロジェクトに含まれる jQuery スクリプトライブラリは、NuGet パッケージをインストールすることによって実際に配置されます。</span><span class="sxs-lookup"><span data-stu-id="c9982-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="c9982-109">ASP.NET MVC 3 プロジェクトテンプレートには、プロジェクトテンプレートが呼び出されたときにインストールされる NuGet パッケージのセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c9982-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="c9982-110">プロジェクトテンプレートを含む NuGet パッケージを追加する機能は、 _すべて_ のプロジェクトテンプレートでを利用できるようになった nuget の機能です。</span><span class="sxs-lookup"><span data-stu-id="c9982-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="c9982-111">この機能の詳細については、この [機能の開発者によるこのブログ投稿](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c9982-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="c9982-112">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="c9982-112">Explicit Assembly References</span></span>

<span data-ttu-id="c9982-113">`<references />`パッケージ内のどのアセンブリを参照する必要があるかを明示的に指定するために使用される新しい要素が追加されました。</span><span class="sxs-lookup"><span data-stu-id="c9982-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="c9982-114">たとえば、次のコードを追加するとします。</span><span class="sxs-lookup"><span data-stu-id="c9982-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="c9982-115">`xunit.dll` `xunit.extensions.dll` フォルダー内に他のアセンブリがある場合でも、とは、フォルダーの適切な[フレームワーク/プロファイルサブフォルダー](../reference/nuspec.md#explicit-assembly-references)から参照され `lib` ます。</span><span class="sxs-lookup"><span data-stu-id="c9982-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="c9982-116">この要素が省略されている場合は、通常の動作が適用されます。これは、フォルダー内のすべてのアセンブリを参照し `lib` ます。</span><span class="sxs-lookup"><span data-stu-id="c9982-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="c9982-117">__この機能はどのように使用されますか。__</span><span class="sxs-lookup"><span data-stu-id="c9982-117">__What is this feature used for?__</span></span>

<span data-ttu-id="c9982-118">この機能は、デザイン時のみのアセンブリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="c9982-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="c9982-119">たとえば、コードコントラクトを使用する場合、コントラクトアセンブリは、Visual Studio が検出できるように拡張するランタイムアセンブリの横にある必要がありますが、コントラクトアセンブリは実際にはプロジェクトによって参照されることはなく、フォルダーにコピーされないようにする必要があり `bin` ます。</span><span class="sxs-lookup"><span data-stu-id="c9982-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="c9982-120">同様に、この機能は、ツールアセンブリをランタイムアセンブリの横に配置する必要があるが、プロジェクト参照から除外される単体テストフレームワーク (XUnit など) に対しても使用できます。</span><span class="sxs-lookup"><span data-stu-id="c9982-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="c9982-121">Nuspec 内のファイルを除外する機能を追加しました。</span><span class="sxs-lookup"><span data-stu-id="c9982-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="c9982-122">`<file>`ファイル内の要素 `.nuspec` を使用して、ワイルドカードを使用して特定のファイルまたは一連のファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="c9982-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="c9982-123">ワイルドカードを使用する場合、含まれているファイルの特定のサブセットを除外する方法はありません。</span><span class="sxs-lookup"><span data-stu-id="c9982-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="c9982-124">たとえば、特定のファイルを除くフォルダー内のすべてのテキストファイルが必要であるとします。</span><span class="sxs-lookup"><span data-stu-id="c9982-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="c9982-125">複数のファイルを指定するには、セミコロンを使用します。</span><span class="sxs-lookup"><span data-stu-id="c9982-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="c9982-126">または、ワイルドカードを使用して、すべてのバックアップファイルなどの一連のファイルを除外します。</span><span class="sxs-lookup"><span data-stu-id="c9982-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="c9982-127">ダイアログボックスを使用してパッケージを削除し、依存関係を削除する</span><span class="sxs-lookup"><span data-stu-id="c9982-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="c9982-128">依存関係を含むパッケージをアンインストールすると、NuGet プロンプトが表示され、パッケージと共にパッケージの依存関係を削除できます。</span><span class="sxs-lookup"><span data-stu-id="c9982-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![依存パッケージの削除](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="c9982-130">`Get-Package` コマンドの改善</span><span class="sxs-lookup"><span data-stu-id="c9982-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="c9982-131">`Get-Package`コマンドでパラメーターがサポートされるようになりました `-ProjectName` 。</span><span class="sxs-lookup"><span data-stu-id="c9982-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="c9982-132">コマンド</span><span class="sxs-lookup"><span data-stu-id="c9982-132">So the command</span></span>

```
Get-Package –ProjectName A
```

<span data-ttu-id="c9982-133">プロジェクト A にインストールされているすべてのパッケージが一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="c9982-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="c9982-134">認証を必要とするプロキシのサポート</span><span class="sxs-lookup"><span data-stu-id="c9982-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="c9982-135">認証を必要とするプロキシの背後で NuGet を使用すると、NuGet はプロキシの資格情報の入力を求められるようになります。</span><span class="sxs-lookup"><span data-stu-id="c9982-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="c9982-136">資格情報を入力すると、NuGet はリモートリポジトリに接続できます。</span><span class="sxs-lookup"><span data-stu-id="c9982-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="c9982-137">認証を必要とするリポジトリのサポート</span><span class="sxs-lookup"><span data-stu-id="c9982-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="c9982-138">NuGet では、基本認証または NTLM 認証を必要とする [プライベートリポジトリ](../hosting-packages/local-feeds.md) への接続がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="c9982-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="c9982-139">ダイジェスト認証のサポートは、今後のリリースで追加される予定です。</span><span class="sxs-lookup"><span data-stu-id="c9982-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="c9982-140">Nuget.org リポジトリのパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="c9982-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="c9982-141">Nuget.org ギャラリーでは、パッケージの一覧と検索をより迅速に行うために、いくつかのパフォーマンスが向上しました。</span><span class="sxs-lookup"><span data-stu-id="c9982-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="c9982-142">ソリューションダイアログプロジェクトのフィルター処理</span><span class="sxs-lookup"><span data-stu-id="c9982-142">Solution dialog project filtering</span></span>
<span data-ttu-id="c9982-143">ソリューションレベルのダイアログでは、インストールするプロジェクトを要求するときに、選択したパッケージと互換性のあるプロジェクトのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c9982-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="c9982-144">パッケージのリリースノート</span><span class="sxs-lookup"><span data-stu-id="c9982-144">Package Release Notes</span></span>
<span data-ttu-id="c9982-145">NuGet パッケージには、リリースノートのサポートが含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="c9982-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="c9982-146">リリースノートは、パッケージの _更新_ を表示するときにのみ表示されます。そのため、最初のリリースに追加することは意味がありません。</span><span class="sxs-lookup"><span data-stu-id="c9982-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![[更新] タブ内のリリースノート](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="c9982-148">リリースノートをパッケージに追加するには、 `<releaseNotes />` NuSpec ファイルで新しい metadata 要素を使用します。</span><span class="sxs-lookup"><span data-stu-id="c9982-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="c9982-149">. nuspec &ltfiles/ &gt; 向上</span><span class="sxs-lookup"><span data-stu-id="c9982-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="c9982-150">`.nuspec`ファイルに空の要素が許可されるようになりました。これにより、 `<files />` パッケージにファイルを含めないように nuget.exe に指示します。</span><span class="sxs-lookup"><span data-stu-id="c9982-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="c9982-151">バグの修正</span><span class="sxs-lookup"><span data-stu-id="c9982-151">Bug Fixes</span></span>
<span data-ttu-id="c9982-152">NuGet 1.5 では、合計107個の作業項目が修正済みです。</span><span class="sxs-lookup"><span data-stu-id="c9982-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="c9982-153">これらの103はバグとしてマークされています。</span><span class="sxs-lookup"><span data-stu-id="c9982-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="c9982-154">NuGet 1.5 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c9982-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="c9982-155">バグ修正:</span><span class="sxs-lookup"><span data-stu-id="c9982-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="c9982-156">[問題 1273](http://nuget.codeplex.com/workitem/1273): `packages.config` パッケージをアルファベット順に並べ替え、余分な空白を削除することで、より多くのバージョンコントロールを使いやすくしました。</span><span class="sxs-lookup"><span data-stu-id="c9982-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="c9982-157">[問題 844](http://nuget.codeplex.com/workitem/844): バージョン番号が正規化され `Install-Package 1.0` 、がバージョンのパッケージで動作するようになりました `1.0.0` 。</span><span class="sxs-lookup"><span data-stu-id="c9982-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="c9982-158">[問題 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe を使用してパッケージを作成するときに、フラグによって `-Version` 要素がオーバーライドされ `<version />` ます。</span><span class="sxs-lookup"><span data-stu-id="c9982-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
