---
title: NuGet project.json のアーカイブ コンテンツ
description: NuGet のドキュメントの他の分野から削除された project.json のその他のコンテンツ。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: cd0f4bc44c1acaeed3b3ed0241c501ddd281628d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="d7bdb-103">project.json のアーカイブ</span><span class="sxs-lookup"><span data-stu-id="d7bdb-103">project.json archive</span></span>

<span data-ttu-id="d7bdb-104">`project.json` 管理形式は、NuGet 3.x で導入され、特定のプロジェクトの種類に使用されていました。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="d7bdb-105">これは、PackageReference 形式の導入に伴い、非推奨となりました。PackageReference 形式では、依存関係のリストがプロジェクト ファイルに直接格納されます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="d7bdb-106">関連項目:</span><span class="sxs-lookup"><span data-stu-id="d7bdb-106">Also see:</span></span>

- [<span data-ttu-id="d7bdb-107">project.json のスキーマ</span><span class="sxs-lookup"><span data-stu-id="d7bdb-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="d7bdb-108">パッケージ作成者に対する project.json の影響</span><span class="sxs-lookup"><span data-stu-id="d7bdb-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="d7bdb-109">project.json および UWP</span><span class="sxs-lookup"><span data-stu-id="d7bdb-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="d7bdb-110">project.json の管理形式</span><span class="sxs-lookup"><span data-stu-id="d7bdb-110">project.json management format</span></span>

<span data-ttu-id="d7bdb-111">*"もともとは「[パッケージの復元](../what-is-nuget.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="d7bdb-112">管理形式の一覧には次が含まれます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-112">In the list of management formats:</span></span>

- <span data-ttu-id="d7bdb-113">[`project.json`](project-json.md): *(使用されていない)* プロジェクトの依存関係のリストを保持する JSON ファイルです。全体的なパッケージ グラフは関連ファイル `project.lock.json` に含まれます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="d7bdb-114">PackageReference が優先され、この形式は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="d7bdb-115">Mono での NuGet の復元</span><span class="sxs-lookup"><span data-stu-id="d7bdb-115">nuget restore on Mono</span></span>

<span data-ttu-id="d7bdb-116">*"もともとは「[NuGet クライアント ツールのインストール](../install-nuget-client-tools.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="d7bdb-117">`project.json` で機能します。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="d7bdb-118">復元でのパッケージのバージョンの制約</span><span class="sxs-lookup"><span data-stu-id="d7bdb-118">Constraining package versions with restore</span></span>

<span data-ttu-id="d7bdb-119">*"もともとは「[パッケージの復元](../consume-packages/package-restore.md#constraining-package-versions-with-restore)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-119">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="d7bdb-120">`project.json`: 依存関係のバージョン番号でバージョンの範囲を直接指定します。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="d7bdb-121">例:</span><span class="sxs-lookup"><span data-stu-id="d7bdb-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="d7bdb-122">NuGet CLI コマンド</span><span class="sxs-lookup"><span data-stu-id="d7bdb-122">NuGet CLI commands</span></span>

- <span data-ttu-id="d7bdb-123">`project.json`では、`nuget install` は機能しません。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="d7bdb-124">`nuget restore`: `project.json`を使用するプロジェクトでは、必要に応じて、`project.lock.json` ファイルと `<project>.nuget.props` ファイルを生成します。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="d7bdb-125">(どちらのファイルもソース管理から省略できます)。`<projectPath>` 引数は、`project.json` ファイルを指示することができ、`packages.config` またはプロジェクト ファイルを指示する場合同様に動作します。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="d7bdb-126">パッケージ フォルダーの優先順位では、`project.json` を使用する場合、`%userprofile%\.nuget\packages` が最初に検索されます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="d7bdb-127">`nuget update`: Mono の場合、このコマンドは、`project.json` を使用するプロジェクトで機能しません。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="d7bdb-128">PackageReference による依存関係の解決</span><span class="sxs-lookup"><span data-stu-id="d7bdb-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="d7bdb-129">*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-129">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="d7bdb-130">PackageReference の動作は、`project.json` にも適用されます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="d7bdb-131">nuget restore は、依存関係グラフを、`project.json` と同時に `project.lock.json`にも書き込みます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="d7bdb-132">依存関係アセットの管理</span><span class="sxs-lookup"><span data-stu-id="d7bdb-132">Managing dependency assets</span></span>

<span data-ttu-id="d7bdb-133">*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#managing-dependency-assets)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-133">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="d7bdb-134">`project.json` 形式を使用すると、依存関係から最上位のプロジェクトへの資産のフローを制御できます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="d7bdb-135">詳細については、「[project.json](project-json.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="d7bdb-136">参照の除外</span><span class="sxs-lookup"><span data-stu-id="d7bdb-136">Excluding references</span></span>

<span data-ttu-id="d7bdb-137">*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#excluding-references)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-137">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="d7bdb-138">`project.json`: パッケージ C の依存関係に `"exclude" : "all"` を追加します。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

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

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="d7bdb-139">互換性のないパッケージのエラーの解決</span><span class="sxs-lookup"><span data-stu-id="d7bdb-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="d7bdb-140">*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-140">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="d7bdb-141">エラーを解決するための追加手段:</span><span class="sxs-lookup"><span data-stu-id="d7bdb-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="d7bdb-142">**お勧めしません**: パッケージ作成者と作業するときの一時的な解決策として、`netcore`、`netstandard`、および `netcoreapp` を対象とするプロジェクトでは、他のフレームワークを互換性があるものとして指定し、これらの他のフレームワークを対象とするパッケージを使うことができます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="d7bdb-143">[project.json のインポート](project-json.md#imports)に関するページおよび [MSBuild 復元ターゲットの PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback) に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="d7bdb-144">この方法では予期しない動作が発生する可能性があるので、繰り返しますが、パッケージ作成者との共同作業または更新によってパッケージの非互換性を解決することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="d7bdb-145">ターゲット フレームワーク</span><span class="sxs-lookup"><span data-stu-id="d7bdb-145">Target frameworks</span></span>

<span data-ttu-id="d7bdb-146">*"もともとは「[ターゲット フレームワーク](../reference/target-frameworks.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="d7bdb-147">[project.json](project-json.md): `frameworks` ノードで、プロジェクトをコンパイルできるフレームワークのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="d7bdb-148">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="d7bdb-148">Creating a package</span></span>

<span data-ttu-id="d7bdb-149">*"もともとは「[パッケージの作成](../create-packages/creating-a-package.md)」内"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="d7bdb-150">パッケージの種類の設定</span><span class="sxs-lookup"><span data-stu-id="d7bdb-150">Setting a package type</span></span>

<span data-ttu-id="d7bdb-151">.NET Core 1.x では、DotnetCliTool パッケージがインストールされると、Visual Studio により、`dependencies` ノードではなく、`project.json` `tools` ノードに格納されます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="d7bdb-152">パッケージの種類は `project.json` で設定されます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="d7bdb-153">`project.json`: `packOptions.packageType` プロパティ json 内のパッケージの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="d7bdb-154">MSBuild のターゲットとプロパティの追加</span><span class="sxs-lookup"><span data-stu-id="d7bdb-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="d7bdb-155">*"もともとは「[Visual Studio 2015 での .NET Standard NuGet パッケージの作成](../guides/create-net-standard-packages-vs2015.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="d7bdb-156">`project.json` を使用する場合、ターゲットはプロジェクトに追加されませんが、`project.lock.json` を通じて使用できます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="d7bdb-157">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="d7bdb-157">Package versioning</span></span>

<span data-ttu-id="d7bdb-158">*"もともとは「[パッケージのバージョン管理](../reference/package-versioning.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-158">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="d7bdb-159">`project.json`形式を使用する場合、NuGet では、メジャー、マイナー、パッチ、およびプレリリースを示す、番号のサフィックス部分にワイルドカード表記 \*を使用できます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="d7bdb-160">NuGet.Config 参照</span><span class="sxs-lookup"><span data-stu-id="d7bdb-160">NuGet.Config reference</span></span>

<span data-ttu-id="d7bdb-161">*"もともとは「[NuGet.Config 参照](../reference/nuget-config-file.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="d7bdb-162">`globalPackagesFolder` は、`project.json` にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="d7bdb-163">(追加情報: PackageReference にも適用されます。)</span><span class="sxs-lookup"><span data-stu-id="d7bdb-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="d7bdb-164">nuspec ファイル参照</span><span class="sxs-lookup"><span data-stu-id="d7bdb-164">nuspec file reference</span></span>

<span data-ttu-id="d7bdb-165">*"もともとは「[nuspec リファレンス](../reference/nuspec.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="d7bdb-166">`<contentFiles>` 要素は、`project.json` で `<files>` の代わりに使用されます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="d7bdb-167">パッケージ マネージャーのオプションの制御</span><span class="sxs-lookup"><span data-stu-id="d7bdb-167">Package manager options control</span></span>

<span data-ttu-id="d7bdb-168">*もともとは「[パッケージ マネージャー UI リファレンス](../tools/package-manager-ui.md)」内。*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="d7bdb-169">`project.json` 管理形式を使用するプロジェクトでは、**[プレビュー ウィンドウを表示する]** オプションのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="d7bdb-170">Visual Studio テンプレート</span><span class="sxs-lookup"><span data-stu-id="d7bdb-170">Visual Studio Templates</span></span>

<span data-ttu-id="d7bdb-171">*"もともとは「[Visual Studio テンプレートの NuGet パッケージ](../visual-studio-extensibility/visual-studio-templates.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="d7bdb-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="d7bdb-172">ベスト プラクティス: テンプレートに、`project.json` ファイルは含まれません。また、NuGet パッケージがインストールされるときに追加される参照やコンテンツも含まれません。</span><span class="sxs-lookup"><span data-stu-id="d7bdb-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>