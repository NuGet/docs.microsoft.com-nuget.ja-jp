---
title: NuGet project.json のアーカイブ コンテンツ | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet のドキュメントの他の分野から削除された project.json のその他のコンテンツ。
keywords: NuGet project.json ファイル
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 16361fe16d8ecc7064af4b6d636435a31a5663dc
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="5e5fe-104">project.json のアーカイブ</span><span class="sxs-lookup"><span data-stu-id="5e5fe-104">project.json archive</span></span>

<span data-ttu-id="5e5fe-105">`project.json` 管理形式は、NuGet 3.x で導入され、特定のプロジェクトの種類に使用されていました。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-105">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="5e5fe-106">これは、PackageReference 形式の導入に伴い、使用されなくなりました。PackageReference 形式では、依存関係のリストがプロジェクト ファイルに直接格納されます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-106">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="5e5fe-107">関連項目:</span><span class="sxs-lookup"><span data-stu-id="5e5fe-107">Also see:</span></span>

- [<span data-ttu-id="5e5fe-108">project.json のスキーマ</span><span class="sxs-lookup"><span data-stu-id="5e5fe-108">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="5e5fe-109">パッケージ作成者に対する project.json の影響</span><span class="sxs-lookup"><span data-stu-id="5e5fe-109">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="5e5fe-110">project.json および UWP</span><span class="sxs-lookup"><span data-stu-id="5e5fe-110">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="5e5fe-111">project.json の管理形式</span><span class="sxs-lookup"><span data-stu-id="5e5fe-111">project.json management format</span></span>

<span data-ttu-id="5e5fe-112">*"もともとは「[パッケージの復元](../what-is-nuget.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-112">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="5e5fe-113">管理形式の一覧には次が含まれます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-113">In the list of management formats:</span></span>

- <span data-ttu-id="5e5fe-114">[`project.json`](project-json.md): *(使用されていない)* プロジェクトの依存関係のリストを保持する JSON ファイルです。全体的なパッケージ グラフは関連ファイル `project.lock.json` に含まれます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-114">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="5e5fe-115">PackageReference が優先され、この形式は使用されていません。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-115">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="5e5fe-116">Mono での NuGet の復元</span><span class="sxs-lookup"><span data-stu-id="5e5fe-116">nuget restore on Mono</span></span>

<span data-ttu-id="5e5fe-117">*"もともとは「[NuGet クライアント ツールのインストール](../install-nuget-client-tools.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-117">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="5e5fe-118">`project.json` で機能します。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-118">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="5e5fe-119">復元でのパッケージのバージョンの制約</span><span class="sxs-lookup"><span data-stu-id="5e5fe-119">Constraining package versions with restore</span></span>

<span data-ttu-id="5e5fe-120">*"もともとは「[パッケージの復元](../consume-packages/package-restore.md#constraining-package-versions-with-restore)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-120">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="5e5fe-121">`project.json`: 依存関係のバージョン番号でバージョンの範囲を直接指定します。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-121">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="5e5fe-122">例:</span><span class="sxs-lookup"><span data-stu-id="5e5fe-122">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="5e5fe-123">NuGet CLI コマンド</span><span class="sxs-lookup"><span data-stu-id="5e5fe-123">NuGet CLI commands</span></span>

- <span data-ttu-id="5e5fe-124">`project.json`では、`nuget install` は機能しません。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-124">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="5e5fe-125">`nuget restore`: `project.json`を使用するプロジェクトでは、必要に応じて、`project.lock.json` ファイルと `<project>.nuget.props` ファイルを生成します。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-125">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="5e5fe-126">(どちらのファイルもソース管理から省略できます)。`<projectPath>` 引数は、`project.json` ファイルを指示することができ、`packages.config` またはプロジェクト ファイルを指示する場合同様に動作します。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-126">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="5e5fe-127">パッケージ フォルダーの優先順位では、`project.json` を使用する場合、`%userprofile%\.nuget\packages` が最初に検索されます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-127">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="5e5fe-128">`nuget update`: Mono の場合、このコマンドは、`project.json` を使用するプロジェクトで機能しません。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-128">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="5e5fe-129">PackageReference による依存関係の解決</span><span class="sxs-lookup"><span data-stu-id="5e5fe-129">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="5e5fe-130">*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-130">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="5e5fe-131">PackageReference の動作は、`project.json` にも適用されます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-131">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="5e5fe-132">nuget restore は、依存関係グラフを、`project.json` と同時に `project.lock.json`にも書き込みます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-132">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="5e5fe-133">依存関係アセットの管理</span><span class="sxs-lookup"><span data-stu-id="5e5fe-133">Managing dependency assets</span></span>

<span data-ttu-id="5e5fe-134">*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#managing-dependency-assets)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-134">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="5e5fe-135">`project.json` 形式を使用すると、依存関係から最上位のプロジェクトへの資産のフローを制御できます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-135">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="5e5fe-136">詳細については、「[project.json](project-json.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-136">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="5e5fe-137">参照の除外</span><span class="sxs-lookup"><span data-stu-id="5e5fe-137">Excluding references</span></span>

<span data-ttu-id="5e5fe-138">*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#excluding-references)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-138">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="5e5fe-139">`project.json`: パッケージ C の依存関係に `"exclude" : "all"` を追加します。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-139">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

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

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="5e5fe-140">互換性のないパッケージのエラーの解決</span><span class="sxs-lookup"><span data-stu-id="5e5fe-140">Resolving incompatible package errors</span></span>

<span data-ttu-id="5e5fe-141">*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-141">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="5e5fe-142">エラーを解決するための追加手段:</span><span class="sxs-lookup"><span data-stu-id="5e5fe-142">An added means of resolving errors:</span></span>

- <span data-ttu-id="5e5fe-143">**お勧めしません**: パッケージ作成者と作業するときの一時的な解決策として、`netcore`、`netstandard`、および `netcoreapp` を対象とするプロジェクトでは、他のフレームワークを互換性があるものとして指定し、これらの他のフレームワークを対象とするパッケージを使うことができます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-143">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="5e5fe-144">[project.json のインポート](project-json.md#imports)に関するページおよび [MSBuild 復元ターゲットの PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback) に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-144">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="5e5fe-145">この方法では予期しない動作が発生する可能性があるので、繰り返しますが、パッケージ作成者との共同作業または更新によってパッケージの非互換性を解決することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-145">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="5e5fe-146">ターゲット フレームワーク</span><span class="sxs-lookup"><span data-stu-id="5e5fe-146">Target frameworks</span></span>

<span data-ttu-id="5e5fe-147">*"もともとは「[ターゲット フレームワーク](../reference/target-frameworks.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-147">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="5e5fe-148">[project.json](project-json.md): `frameworks` ノードで、プロジェクトをコンパイルできるフレームワークのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-148">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="5e5fe-149">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="5e5fe-149">Creating a package</span></span>

<span data-ttu-id="5e5fe-150">*"もともとは「[パッケージの作成](../create-packages/creating-a-package.md)」内"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-150">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="5e5fe-151">パッケージの種類の設定</span><span class="sxs-lookup"><span data-stu-id="5e5fe-151">Setting a package type</span></span>

<span data-ttu-id="5e5fe-152">.NET Core 1.x では、DotnetCliTool パッケージがインストールされると、Visual Studio により、`dependencies` ノードではなく、`project.json` `tools` ノードに格納されます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-152">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="5e5fe-153">パッケージの種類は `project.json` で設定されます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-153">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="5e5fe-154">`project.json`: `packOptions.packageType` プロパティ json 内のパッケージの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-154">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="5e5fe-155">MSBuild のターゲットとプロパティの追加</span><span class="sxs-lookup"><span data-stu-id="5e5fe-155">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="5e5fe-156">*"もともとは「[Visual Studio 2015 での .NET Standard NuGet パッケージの作成](../guides/create-net-standard-packages-vs2015.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-156">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="5e5fe-157">`project.json` を使用する場合、ターゲットはプロジェクトに追加されませんが、`project.lock.json` を通じて使用できます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-157">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="5e5fe-158">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="5e5fe-158">Package versioning</span></span>

<span data-ttu-id="5e5fe-159">*"もともとは「[パッケージのバージョン管理](../reference/package-versioning.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-159">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="5e5fe-160">`project.json`形式を使用する場合、NuGet では、メジャー、マイナー、パッチ、およびプレリリースを示す、番号のサフィックス部分にワイルドカード表記 \*を使用できます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-160">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="5e5fe-161">NuGet.Config 参照</span><span class="sxs-lookup"><span data-stu-id="5e5fe-161">NuGet.Config reference</span></span>

<span data-ttu-id="5e5fe-162">*"もともとは「[NuGet.Config 参照](../reference/nuget-config-file.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-162">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="5e5fe-163">`globalPackagesFolder` は、`project.json` にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-163">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="5e5fe-164">(追加情報: PackageReference にも適用されます。)</span><span class="sxs-lookup"><span data-stu-id="5e5fe-164">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="5e5fe-165">nuspec ファイル参照</span><span class="sxs-lookup"><span data-stu-id="5e5fe-165">nuspec file reference</span></span>

<span data-ttu-id="5e5fe-166">*"もともとは「[nuspec リファレンス](../reference/nuspec.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-166">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="5e5fe-167">`<contentFiles>` 要素は、`project.json` で `<files>` の代わりに使用されます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-167">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="5e5fe-168">パッケージ マネージャーのオプションの制御</span><span class="sxs-lookup"><span data-stu-id="5e5fe-168">Package manager options control</span></span>

<span data-ttu-id="5e5fe-169">*もともとは「[パッケージ マネージャー UI リファレンス](../tools/package-manager-ui.md)」内。*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-169">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="5e5fe-170">`project.json` 管理形式を使用するプロジェクトでは、**[プレビュー ウィンドウを表示する]** オプションのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-170">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="5e5fe-171">Visual Studio テンプレート</span><span class="sxs-lookup"><span data-stu-id="5e5fe-171">Visual Studio Templates</span></span>

<span data-ttu-id="5e5fe-172">*"もともとは「[Visual Studio テンプレートの NuGet パッケージ](../visual-studio-extensibility/visual-studio-templates.md)」内。"*</span><span class="sxs-lookup"><span data-stu-id="5e5fe-172">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="5e5fe-173">ベスト プラクティス: テンプレートに、`project.json` ファイルは含まれません。また、NuGet パッケージがインストールされるときに追加される参照やコンテンツも含まれません。</span><span class="sxs-lookup"><span data-stu-id="5e5fe-173">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>