---
title: NuGet 1.5 のリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.5 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548726"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="33b5b-103">NuGet 1.5 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="33b5b-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="33b5b-104">[NuGet 1.4 のリリース ノート](../release-notes/nuget-1.4.md) | [NuGet 1.6 リリース ノート](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="33b5b-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="33b5b-105">NuGet 1.5 は、2011 年 8 月 30 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="33b5b-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="33b5b-106">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="33b5b-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="33b5b-107">プレインストールされている NuGet パッケージを使用したプロジェクト テンプレート</span><span class="sxs-lookup"><span data-stu-id="33b5b-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="33b5b-108">新しい ASP.NET MVC 3 プロジェクト テンプレートを作成するときに、プロジェクトに含まれる jQuery スクリプト ライブラリが NuGet パッケージをインストールすることでがあります配置実際にされます。</span><span class="sxs-lookup"><span data-stu-id="33b5b-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="33b5b-109">ASP.NET MVC 3 プロジェクト テンプレートには、プロジェクト テンプレートが呼び出されたときにインストールされる NuGet パッケージのセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="33b5b-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="33b5b-110">プロジェクト テンプレートを使用した NuGet パッケージを含めるには、この機能は、NuGet の機能であるようになりましたが_任意_プロジェクト テンプレートのメリットを得ることができます。</span><span class="sxs-lookup"><span data-stu-id="33b5b-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="33b5b-111">この機能の詳細については、「この[機能の開発者によるブログの投稿](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="33b5b-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="33b5b-112">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="33b5b-112">Explicit Assembly References</span></span>

<span data-ttu-id="33b5b-113">新しい追加`<references />`要素内でアセンブリを明示的に指定するために使用、パッケージを参照してください。</span><span class="sxs-lookup"><span data-stu-id="33b5b-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="33b5b-114">たとえば、次のコードを追加するとします。</span><span class="sxs-lookup"><span data-stu-id="33b5b-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="33b5b-115">後のみ、`xunit.dll`と`xunit.extensions.dll`から適切な参照は[フレームワーク/プロファイル サブフォルダー](../reference/nuspec.md#explicit-assembly-references)の`lib`フォルダー、フォルダー内の他のアセンブリがある場合でもです。</span><span class="sxs-lookup"><span data-stu-id="33b5b-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="33b5b-116">この要素を省略したかどうかでのすべてのアセンブリを参照しているので、通常の動作が適用されます、`lib`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="33b5b-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="33b5b-117">__この機能のを使用目的は?__</span><span class="sxs-lookup"><span data-stu-id="33b5b-117">__What is this feature used for?__</span></span>

<span data-ttu-id="33b5b-118">この機能は、デザイン時アセンブリのみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="33b5b-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="33b5b-119">たとえば、コード コントラクトを使用する場合、コントラクト アセンブリは Visual Studio は、それらを見つけることができますが、コントラクト アセンブリを選択し、実際に参照しないで、プロジェクトでにコピーしてはならないように拡張するランタイム アセンブリの隣にあるが必要`bin`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="33b5b-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="33b5b-120">同様に、機能は、そのツールのアセンブリはランタイム アセンブリの横にあるが、プロジェクト参照から除外する必要がある XUnit などの単体テスト フレームワークに使用できます。</span><span class="sxs-lookup"><span data-stu-id="33b5b-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="33b5b-121">.Nuspec ファイルを除外する機能を追加しました</span><span class="sxs-lookup"><span data-stu-id="33b5b-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="33b5b-122">`<file>`内の要素を`.nuspec`ファイルを使用して、特定のファイルまたはワイルドカードを使用してファイルのセットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="33b5b-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="33b5b-123">ワイルドカードを使用する場合、含まれているファイルの特定のサブセットを除外する方法はありません。</span><span class="sxs-lookup"><span data-stu-id="33b5b-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="33b5b-124">たとえば、特定の 1 つを除く、フォルダー内のすべてのテキスト ファイルを必要とします。</span><span class="sxs-lookup"><span data-stu-id="33b5b-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="33b5b-125">セミコロンを使用すると、複数のファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="33b5b-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="33b5b-126">または、ワイルドカードを使用して、すべてのバックアップ ファイルなどのファイルのセットを除外するには</span><span class="sxs-lookup"><span data-stu-id="33b5b-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="33b5b-127">ダイアログ ボックスを使用してパッケージを削除する依存関係を削除するように求められます</span><span class="sxs-lookup"><span data-stu-id="33b5b-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="33b5b-128">NuGet が表示されたら、依存関係を使用してパッケージをアンインストールするときに、パッケージとパッケージの依存関係の削除を許可します。</span><span class="sxs-lookup"><span data-stu-id="33b5b-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![依存パッケージを削除します。](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="33b5b-130">`Get-Package` コマンドの向上</span><span class="sxs-lookup"><span data-stu-id="33b5b-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="33b5b-131">`Get-Package`コマンドがサポートされています、`-ProjectName`パラメーター。</span><span class="sxs-lookup"><span data-stu-id="33b5b-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="33b5b-132">したがって、コマンド</span><span class="sxs-lookup"><span data-stu-id="33b5b-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="33b5b-133">A. をプロジェクトにインストールされているすべてのパッケージが一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="33b5b-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="33b5b-134">認証が必要なプロキシのサポート</span><span class="sxs-lookup"><span data-stu-id="33b5b-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="33b5b-135">NuGet を使用して、認証が必要なプロキシの背後にある、NuGet では、プロキシの資格情報が求めるされますようになりました。</span><span class="sxs-lookup"><span data-stu-id="33b5b-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="33b5b-136">NuGet リモート リポジトリに接続するのには、資格情報を入力できます。</span><span class="sxs-lookup"><span data-stu-id="33b5b-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="33b5b-137">認証を必要とするリポジトリのサポート</span><span class="sxs-lookup"><span data-stu-id="33b5b-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="33b5b-138">NuGet への接続を今すぐサポート[プライベート リポジトリ](../hosting-packages/local-feeds.md)基本認証または NTLM 認証を必要とします。</span><span class="sxs-lookup"><span data-stu-id="33b5b-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="33b5b-139">ダイジェスト認証のサポートは、将来のリリースで追加されます。</span><span class="sxs-lookup"><span data-stu-id="33b5b-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="33b5b-140">リポジトリ nuget.org をパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="33b5b-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="33b5b-141">Nuget.org ギャラリー パッケージを一覧表示して、高速検索をいくつかのパフォーマンス強化を行いました。</span><span class="sxs-lookup"><span data-stu-id="33b5b-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="33b5b-142">ソリューション ダイアログ プロジェクトのフィルタ リング</span><span class="sxs-lookup"><span data-stu-id="33b5b-142">Solution dialog project filtering</span></span>
<span data-ttu-id="33b5b-143">ソリューション レベル ダイアログ ボックスで、インストールするには、どのようなプロジェクトのプロンプト時に、選択したパッケージと互換性があるプロジェクトだけを示します。</span><span class="sxs-lookup"><span data-stu-id="33b5b-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="33b5b-144">パッケージのリリース ノート</span><span class="sxs-lookup"><span data-stu-id="33b5b-144">Package Release Notes</span></span>
<span data-ttu-id="33b5b-145">NuGet パッケージには、リリース ノートのサポートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="33b5b-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="33b5b-146">リリース ノートにのみ表示を表示するときに_更新_パッケージのため意味をなさない、最初のリリースに追加します。</span><span class="sxs-lookup"><span data-stu-id="33b5b-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![[更新] タブ内のリリース ノート](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="33b5b-148">にパッケージをリリース ノートを追加する、新しい使用`<releaseNotes />`NuSpec ファイル内のメタデータ要素。</span><span class="sxs-lookup"><span data-stu-id="33b5b-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="33b5b-149">.nuspec & ltfiles/&gt;向上</span><span class="sxs-lookup"><span data-stu-id="33b5b-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="33b5b-150">`.nuspec`ファイルは現在空により`<files />`要素は、すべてのファイルをパッケージに含めない nuget.exe が示されます。</span><span class="sxs-lookup"><span data-stu-id="33b5b-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="33b5b-151">バグ修正</span><span class="sxs-lookup"><span data-stu-id="33b5b-151">Bug Fixes</span></span>
<span data-ttu-id="33b5b-152">NuGet 1.5 では、作業項目の固定 107 の合計がありました。</span><span class="sxs-lookup"><span data-stu-id="33b5b-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="33b5b-153">これらの 103 はバグとしてマークされています。</span><span class="sxs-lookup"><span data-stu-id="33b5b-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="33b5b-154">作業の完全な一覧の項目で修正された NuGet 1.5 では、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)します。</span><span class="sxs-lookup"><span data-stu-id="33b5b-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="33b5b-155">注目すべきバグ修正:</span><span class="sxs-lookup"><span data-stu-id="33b5b-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="33b5b-156">[問題 1273](http://nuget.codeplex.com/workitem/1273): 行った`packages.config`パッケージをアルファベット順に並べ替え、余分な空白を削除してわかりやすい複数のバージョン管理します。</span><span class="sxs-lookup"><span data-stu-id="33b5b-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="33b5b-157">[問題 844](http://nuget.codeplex.com/workitem/844): バージョン番号を正規化するようになりましたように`Install-Package 1.0`バージョンを使用してパッケージで動作`1.0.0`します。</span><span class="sxs-lookup"><span data-stu-id="33b5b-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="33b5b-158">[問題 1060](http://nuget.codeplex.com/workitem/1060)。 nuget.exe を使用してパッケージを作成するときに、`-Version`上書きフラグ、`<version />`要素。</span><span class="sxs-lookup"><span data-stu-id="33b5b-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
