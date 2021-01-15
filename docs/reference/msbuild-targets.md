---
title: MSBuild ターゲットとしての NuGet の pack と restore
description: NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7de3f0f1133a89848e9268d489751293fb3cbf25
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235699"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="807ea-103">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="807ea-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="807ea-104">*NuGet 4.0 以降*</span><span class="sxs-lookup"><span data-stu-id="807ea-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="807ea-105">[PackageReference](../consume-packages/package-references-in-project-files.md)形式では、NuGet 4.0 以降では、個別のファイルを使用するのではなく、すべてのマニフェストメタデータをプロジェクトファイル内に直接格納でき `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="807ea-106">MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。</span><span class="sxs-lookup"><span data-stu-id="807ea-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="807ea-107">これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます </span><span class="sxs-lookup"><span data-stu-id="807ea-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="807ea-108">MSBuild を使用して NuGet パッケージを作成する手順については、「 [msbuild を使用した nuget パッケージの作成](../create-packages/creating-a-package-msbuild.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="807ea-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="807ea-109">(NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../reference/cli-reference/cli-ref-pack.md) および [restore](../reference/cli-reference/cli-ref-restore.md) コマンドを使用します)。</span><span class="sxs-lookup"><span data-stu-id="807ea-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="807ea-110">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="807ea-110">Target build order</span></span>

<span data-ttu-id="807ea-111">`pack` と `restore` は MSBuild のターゲットなので、アクセスするとワークフローを強化できます。</span><span class="sxs-lookup"><span data-stu-id="807ea-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="807ea-112">たとえば、パック後にパッケージをネットワーク共有にコピーするとします。</span><span class="sxs-lookup"><span data-stu-id="807ea-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="807ea-113">この場合、プロジェクト ファイルに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="807ea-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="807ea-114">同様に、MSBuild タスクを記述し、独自のターゲットを記述して、MSBuild タスクで NuGet プロパティを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="807ea-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="807ea-115">`$(OutputPath)` は相対であり、プロジェクトのルートからコマンドを実行していることを想定しています。</span><span class="sxs-lookup"><span data-stu-id="807ea-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="807ea-116">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="807ea-116">pack target</span></span>

<span data-ttu-id="807ea-117">PackageReference 形式を使用する .NET Standard プロジェクトでは、を使用して、 `msbuild -t:pack` NuGet パッケージの作成で使用する入力をプロジェクトファイルから描画します。</span><span class="sxs-lookup"><span data-stu-id="807ea-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="807ea-118">以下の表では、最初の `<PropertyGroup>` ノード内のプロジェクト ファイルに追加できる MSBuild のプロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="807ea-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="807ea-119">Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="807ea-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="807ea-120">便宜上、テーブルは[ `.nuspec` ファイル](../reference/nuspec.md)内の同等のプロパティによって整理されています。</span><span class="sxs-lookup"><span data-stu-id="807ea-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="807ea-121">`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="807ea-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="807ea-122">属性/NuSpec の値</span><span class="sxs-lookup"><span data-stu-id="807ea-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="807ea-123">MSBuild のプロパティ</span><span class="sxs-lookup"><span data-stu-id="807ea-123">MSBuild Property</span></span> | <span data-ttu-id="807ea-124">Default</span><span class="sxs-lookup"><span data-stu-id="807ea-124">Default</span></span> | <span data-ttu-id="807ea-125">Notes</span><span class="sxs-lookup"><span data-stu-id="807ea-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="807ea-126">Id</span><span class="sxs-lookup"><span data-stu-id="807ea-126">Id</span></span> | <span data-ttu-id="807ea-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="807ea-127">PackageId</span></span> | <span data-ttu-id="807ea-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="807ea-128">AssemblyName</span></span> | <span data-ttu-id="807ea-129">MSBuild の $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="807ea-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="807ea-130">Version</span><span class="sxs-lookup"><span data-stu-id="807ea-130">Version</span></span> | <span data-ttu-id="807ea-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="807ea-131">PackageVersion</span></span> | <span data-ttu-id="807ea-132">Version</span><span class="sxs-lookup"><span data-stu-id="807ea-132">Version</span></span> | <span data-ttu-id="807ea-133">これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345")</span><span class="sxs-lookup"><span data-stu-id="807ea-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="807ea-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="807ea-134">VersionPrefix</span></span> | <span data-ttu-id="807ea-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="807ea-135">PackageVersionPrefix</span></span> | <span data-ttu-id="807ea-136">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-136">empty</span></span> | <span data-ttu-id="807ea-137">PackageVersion を設定すると、PackageVersionPrefix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="807ea-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="807ea-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="807ea-138">VersionSuffix</span></span> | <span data-ttu-id="807ea-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="807ea-139">PackageVersionSuffix</span></span> | <span data-ttu-id="807ea-140">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-140">empty</span></span> | <span data-ttu-id="807ea-141">MSBuild の $(VersionSuffix)</span><span class="sxs-lookup"><span data-stu-id="807ea-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="807ea-142">PackageVersion を設定すると、PackageVersionSuffix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="807ea-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="807ea-143">Authors</span><span class="sxs-lookup"><span data-stu-id="807ea-143">Authors</span></span> | <span data-ttu-id="807ea-144">Authors</span><span class="sxs-lookup"><span data-stu-id="807ea-144">Authors</span></span> | <span data-ttu-id="807ea-145">現在のユーザーのユーザー名</span><span class="sxs-lookup"><span data-stu-id="807ea-145">Username of the current user</span></span> | |
| <span data-ttu-id="807ea-146">所有者</span><span class="sxs-lookup"><span data-stu-id="807ea-146">Owners</span></span> | <span data-ttu-id="807ea-147">該当なし</span><span class="sxs-lookup"><span data-stu-id="807ea-147">N/A</span></span> | <span data-ttu-id="807ea-148">NuSpec にはありません</span><span class="sxs-lookup"><span data-stu-id="807ea-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="807ea-149">Title</span><span class="sxs-lookup"><span data-stu-id="807ea-149">Title</span></span> | <span data-ttu-id="807ea-150">Title</span><span class="sxs-lookup"><span data-stu-id="807ea-150">Title</span></span> | <span data-ttu-id="807ea-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="807ea-151">The PackageId</span></span>| |
| <span data-ttu-id="807ea-152">説明</span><span class="sxs-lookup"><span data-stu-id="807ea-152">Description</span></span> | <span data-ttu-id="807ea-153">説明</span><span class="sxs-lookup"><span data-stu-id="807ea-153">Description</span></span> | <span data-ttu-id="807ea-154">"パッケージの説明"</span><span class="sxs-lookup"><span data-stu-id="807ea-154">"Package Description"</span></span> | |
| <span data-ttu-id="807ea-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="807ea-155">Copyright</span></span> | <span data-ttu-id="807ea-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="807ea-156">Copyright</span></span> | <span data-ttu-id="807ea-157">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-157">empty</span></span> | |
| <span data-ttu-id="807ea-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="807ea-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="807ea-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="807ea-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="807ea-160">false</span><span class="sxs-lookup"><span data-stu-id="807ea-160">false</span></span> | |
| <span data-ttu-id="807ea-161">license</span><span class="sxs-lookup"><span data-stu-id="807ea-161">license</span></span> | <span data-ttu-id="807ea-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="807ea-162">PackageLicenseExpression</span></span> | <span data-ttu-id="807ea-163">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-163">empty</span></span> | <span data-ttu-id="807ea-164">`<license type="expression">` に対応します</span><span class="sxs-lookup"><span data-stu-id="807ea-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="807ea-165">license</span><span class="sxs-lookup"><span data-stu-id="807ea-165">license</span></span> | <span data-ttu-id="807ea-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="807ea-166">PackageLicenseFile</span></span> | <span data-ttu-id="807ea-167">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-167">empty</span></span> | <span data-ttu-id="807ea-168">`<license type="file">` に相当します。</span><span class="sxs-lookup"><span data-stu-id="807ea-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="807ea-169">参照されているライセンスファイルを明示的にパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="807ea-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-170">LicenseUrl</span></span> | <span data-ttu-id="807ea-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-171">PackageLicenseUrl</span></span> | <span data-ttu-id="807ea-172">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-172">empty</span></span> | <span data-ttu-id="807ea-173">`PackageLicenseUrl` 非推奨です。パッケージのパッケージを使用して、パッケージのプロパティを</span><span class="sxs-lookup"><span data-stu-id="807ea-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="807ea-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-174">ProjectUrl</span></span> | <span data-ttu-id="807ea-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-175">PackageProjectUrl</span></span> | <span data-ttu-id="807ea-176">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-176">empty</span></span> | |
| <span data-ttu-id="807ea-177">アイコン</span><span class="sxs-lookup"><span data-stu-id="807ea-177">Icon</span></span> | <span data-ttu-id="807ea-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="807ea-178">PackageIcon</span></span> | <span data-ttu-id="807ea-179">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-179">empty</span></span> | <span data-ttu-id="807ea-180">参照されているアイコンイメージファイルを明示的にパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="807ea-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-181">IconUrl</span></span> | <span data-ttu-id="807ea-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-182">PackageIconUrl</span></span> | <span data-ttu-id="807ea-183">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-183">empty</span></span> | <span data-ttu-id="807ea-184">ベストダウンレベルのエクスペリエンスを向上させるには、 `PackageIconUrl` に加えてを指定する必要があり `PackageIcon` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="807ea-185">長期的には `PackageIconUrl` 非推奨となります。</span><span class="sxs-lookup"><span data-stu-id="807ea-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="807ea-186">タグ</span><span class="sxs-lookup"><span data-stu-id="807ea-186">Tags</span></span> | <span data-ttu-id="807ea-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="807ea-187">PackageTags</span></span> | <span data-ttu-id="807ea-188">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-188">empty</span></span> | <span data-ttu-id="807ea-189">複数のタグはセミコロン (;) で区切られます。</span><span class="sxs-lookup"><span data-stu-id="807ea-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="807ea-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="807ea-190">ReleaseNotes</span></span> | <span data-ttu-id="807ea-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="807ea-191">PackageReleaseNotes</span></span> | <span data-ttu-id="807ea-192">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-192">empty</span></span> | |
| <span data-ttu-id="807ea-193">リポジトリ/Url</span><span class="sxs-lookup"><span data-stu-id="807ea-193">Repository/Url</span></span> | <span data-ttu-id="807ea-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-194">RepositoryUrl</span></span> | <span data-ttu-id="807ea-195">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-195">empty</span></span> | <span data-ttu-id="807ea-196">ソースコードの複製または取得に使用されるリポジトリの URL。</span><span class="sxs-lookup"><span data-stu-id="807ea-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="807ea-197">よう *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="807ea-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="807ea-198">リポジトリ/種類</span><span class="sxs-lookup"><span data-stu-id="807ea-198">Repository/Type</span></span> | <span data-ttu-id="807ea-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="807ea-199">RepositoryType</span></span> | <span data-ttu-id="807ea-200">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-200">empty</span></span> | <span data-ttu-id="807ea-201">リポジトリの種類。</span><span class="sxs-lookup"><span data-stu-id="807ea-201">Repository type.</span></span> <span data-ttu-id="807ea-202">例: *git*、 *tfs*。</span><span class="sxs-lookup"><span data-stu-id="807ea-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="807ea-203">リポジトリ/ブランチ</span><span class="sxs-lookup"><span data-stu-id="807ea-203">Repository/Branch</span></span> | <span data-ttu-id="807ea-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="807ea-204">RepositoryBranch</span></span> | <span data-ttu-id="807ea-205">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-205">empty</span></span> | <span data-ttu-id="807ea-206">リポジトリのブランチ情報 (オプション)。</span><span class="sxs-lookup"><span data-stu-id="807ea-206">Optional repository branch information.</span></span> <span data-ttu-id="807ea-207">このプロパティを含めるには、 *RepositoryUrl* も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="807ea-208">例: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="807ea-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="807ea-209">リポジトリ/コミット</span><span class="sxs-lookup"><span data-stu-id="807ea-209">Repository/Commit</span></span> | <span data-ttu-id="807ea-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="807ea-210">RepositoryCommit</span></span> | <span data-ttu-id="807ea-211">empty</span><span class="sxs-lookup"><span data-stu-id="807ea-211">empty</span></span> | <span data-ttu-id="807ea-212">任意のリポジトリ コミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。</span><span class="sxs-lookup"><span data-stu-id="807ea-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="807ea-213">このプロパティを含めるには、 *RepositoryUrl* も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="807ea-214">例: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="807ea-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="807ea-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="807ea-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="807ea-216">まとめ</span><span class="sxs-lookup"><span data-stu-id="807ea-216">Summary</span></span> | <span data-ttu-id="807ea-217">サポートなし</span><span class="sxs-lookup"><span data-stu-id="807ea-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="807ea-218">pack ターゲットの入力</span><span class="sxs-lookup"><span data-stu-id="807ea-218">pack target inputs</span></span>

- <span data-ttu-id="807ea-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="807ea-219">IsPackable</span></span>
- <span data-ttu-id="807ea-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="807ea-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="807ea-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="807ea-221">PackageVersion</span></span>
- <span data-ttu-id="807ea-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="807ea-222">PackageId</span></span>
- <span data-ttu-id="807ea-223">Authors</span><span class="sxs-lookup"><span data-stu-id="807ea-223">Authors</span></span>
- <span data-ttu-id="807ea-224">説明</span><span class="sxs-lookup"><span data-stu-id="807ea-224">Description</span></span>
- <span data-ttu-id="807ea-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="807ea-225">Copyright</span></span>
- <span data-ttu-id="807ea-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="807ea-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="807ea-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="807ea-227">DevelopmentDependency</span></span>
- <span data-ttu-id="807ea-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="807ea-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="807ea-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="807ea-229">PackageLicenseFile</span></span>
- <span data-ttu-id="807ea-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="807ea-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-231">PackageProjectUrl</span></span>
- <span data-ttu-id="807ea-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-232">PackageIconUrl</span></span>
- <span data-ttu-id="807ea-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="807ea-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="807ea-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="807ea-234">PackageTags</span></span>
- <span data-ttu-id="807ea-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="807ea-235">PackageOutputPath</span></span>
- <span data-ttu-id="807ea-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="807ea-236">IncludeSymbols</span></span>
- <span data-ttu-id="807ea-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="807ea-237">IncludeSource</span></span>
- <span data-ttu-id="807ea-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="807ea-238">PackageTypes</span></span>
- <span data-ttu-id="807ea-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="807ea-239">IsTool</span></span>
- <span data-ttu-id="807ea-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-240">RepositoryUrl</span></span>
- <span data-ttu-id="807ea-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="807ea-241">RepositoryType</span></span>
- <span data-ttu-id="807ea-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="807ea-242">RepositoryBranch</span></span>
- <span data-ttu-id="807ea-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="807ea-243">RepositoryCommit</span></span>
- <span data-ttu-id="807ea-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="807ea-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="807ea-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="807ea-245">MinClientVersion</span></span>
- <span data-ttu-id="807ea-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="807ea-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="807ea-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="807ea-247">IncludeContentInPack</span></span>
- <span data-ttu-id="807ea-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="807ea-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="807ea-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="807ea-249">ContentTargetFolders</span></span>
- <span data-ttu-id="807ea-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="807ea-250">NuspecFile</span></span>
- <span data-ttu-id="807ea-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="807ea-251">NuspecBasePath</span></span>
- <span data-ttu-id="807ea-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="807ea-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="807ea-253">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="807ea-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="807ea-254">依存関係を表示しない</span><span class="sxs-lookup"><span data-stu-id="807ea-254">Suppress dependencies</span></span>

<span data-ttu-id="807ea-255">生成された NuGet パッケージからパッケージの依存関係を抑制するに `SuppressDependenciesWhenPacking` は、をに設定します。これにより、生成された `true` nupkg ファイルからのすべての依存関係がスキップされます。</span><span class="sxs-lookup"><span data-stu-id="807ea-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="807ea-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="807ea-256">PackageIconUrl</span></span>

<span data-ttu-id="807ea-257">`PackageIconUrl` は、新しいプロパティを優先するように非推奨とされ [`PackageIcon`](#packageicon) ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="807ea-258">NuGet 5.3 & Visual Studio 2019 バージョン16.3 以降では、 `pack` パッケージメタデータでのみが指定されている場合、 [NU5048](./errors-and-warnings/nu5048.md) warning が発生し `PackageIconUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="807ea-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="807ea-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="807ea-260">を `PackageIcon` `PackageIconUrl` まだサポートしていないクライアントとソースとの下位互換性を維持するには、との両方を指定する必要があり `PackageIcon` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="807ea-261">Visual Studio では `PackageIcon` 、将来のリリースでフォルダーベースのソースからのパッケージがサポートされるようになります。</span><span class="sxs-lookup"><span data-stu-id="807ea-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="807ea-262">アイコンイメージファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="807ea-262">Packing an icon image file</span></span>

<span data-ttu-id="807ea-263">アイコンイメージファイルをパッキングする場合は、パッケージ `PackageIcon` のルートに対して相対的なパッケージパスを指定するために、プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="807ea-264">また、ファイルがパッケージに含まれていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="807ea-265">イメージファイルのサイズは 1 MB に制限されています。</span><span class="sxs-lookup"><span data-stu-id="807ea-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="807ea-266">サポートされているファイル形式は、JPEG および PNG です。</span><span class="sxs-lookup"><span data-stu-id="807ea-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="807ea-267">128x128 のイメージの解像度をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="807ea-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="807ea-268">例:</span><span class="sxs-lookup"><span data-stu-id="807ea-268">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="807ea-269">[パッケージアイコンのサンプル](https://github.com/NuGet/Samples/tree/master/PackageIconExample)です。</span><span class="sxs-lookup"><span data-stu-id="807ea-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="807ea-270">Nuspec に相当するものについては、「 [nuspec reference for icon」を参照](nuspec.md#icon)してください。</span><span class="sxs-lookup"><span data-stu-id="807ea-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="807ea-271">出力アセンブリ</span><span class="sxs-lookup"><span data-stu-id="807ea-271">Output assemblies</span></span>

<span data-ttu-id="807ea-272">`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="807ea-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="807ea-273">コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。</span><span class="sxs-lookup"><span data-stu-id="807ea-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="807ea-274">出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。</span><span class="sxs-lookup"><span data-stu-id="807ea-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="807ea-275">`IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。</span><span class="sxs-lookup"><span data-stu-id="807ea-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="807ea-276">`BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="807ea-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="807ea-277">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="807ea-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="807ea-278">パッケージ参照</span><span class="sxs-lookup"><span data-stu-id="807ea-278">Package references</span></span>

<span data-ttu-id="807ea-279">「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="807ea-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="807ea-280">プロジェクト間参照</span><span class="sxs-lookup"><span data-stu-id="807ea-280">Project to project references</span></span>

<span data-ttu-id="807ea-281">プロジェクト間参照は、既定で NuGet パッケージ参照として見なされています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="807ea-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="807ea-282">また、次のメタデータをプロジェクト参照に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="807ea-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="807ea-283">パッケージにコンテンツを含める</span><span class="sxs-lookup"><span data-stu-id="807ea-283">Including content in a package</span></span>

<span data-ttu-id="807ea-284">コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="807ea-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="807ea-285">次のようなエントリでオーバーライドしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="807ea-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="807ea-286">次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="807ea-287">(`content` および `contentFiles` フォルダーの両方ではなく) すべてのコンテンツを特定のルート フォルダーにのみコピーする場合、MSBuild プロパティの `ContentTargetFolders` を使用できます。このプロパティの既定値は "content;contentFiles" ですが、他の任意のフォルダー名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="807ea-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="807ea-288">`ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="807ea-289">`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="807ea-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="807ea-290">空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="807ea-291">たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="807ea-292">また、MSBuild プロパティの `$(IncludeContentInPack)` もあります。既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="807ea-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="807ea-293">これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="807ea-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="807ea-294">上記の任意の項目に設定できる他の pack 固有のメタデータとして、NuSpec の ```contentFiles``` エントリに ```CopyToOutput``` 値と ```Flatten``` 値を設定する ```<PackageCopyToOutput>``` と ```<PackageFlatten>``` があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="807ea-295">コンテンツ項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="807ea-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="807ea-296">glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="807ea-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="807ea-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="807ea-297">IncludeSymbols</span></span>

<span data-ttu-id="807ea-298">`MSBuild -t:pack -p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="807ea-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="807ea-299">`IncludeSymbols=true` を設定すると、通常のパッケージ *と* シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="807ea-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="807ea-300">IncludeSource</span></span>

<span data-ttu-id="807ea-301">これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。</span><span class="sxs-lookup"><span data-stu-id="807ea-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="807ea-302">種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="807ea-303">`TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。</span><span class="sxs-lookup"><span data-stu-id="807ea-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="807ea-304">種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="807ea-305">ライセンス式またはライセンスファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="807ea-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="807ea-306">ライセンス式を使用する場合は、"パッケージの表示" プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="807ea-307">[ライセンス式のサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="807ea-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="807ea-308">[NuGet.org によって受け付けられるライセンス式とライセンスの詳細については、こちらを参照](nuspec.md#license)してください。</span><span class="sxs-lookup"><span data-stu-id="807ea-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="807ea-309">ライセンスファイルをパッキングする場合は、パッケージのルートを基準としたパッケージパスを指定するために、"パッケージの作成" プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="807ea-310">また、ファイルがパッケージに含まれていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="807ea-311">例:</span><span class="sxs-lookup"><span data-stu-id="807ea-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="807ea-312">[ライセンスファイルのサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="807ea-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="807ea-313">拡張子のないファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="807ea-313">Packing a file without an extension</span></span>

<span data-ttu-id="807ea-314">ライセンスファイルをパッキングする場合など、一部のシナリオでは、拡張子のないファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="807ea-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="807ea-315">履歴の理由により、NuGet & MSBuild では、パスをディレクトリとして拡張せずにパスを扱います。</span><span class="sxs-lookup"><span data-stu-id="807ea-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="807ea-316">[拡張機能サンプルのないファイル](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/)。</span><span class="sxs-lookup"><span data-stu-id="807ea-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="807ea-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="807ea-317">IsTool</span></span>

<span data-ttu-id="807ea-318">`MSBuild -t:pack -p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="807ea-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="807ea-319">これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="807ea-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="807ea-320">.nuspec を使用したパック</span><span class="sxs-lookup"><span data-stu-id="807ea-320">Packing using a .nuspec</span></span>

<span data-ttu-id="807ea-321">通常はファイル内の [すべてのプロパティ](../reference/msbuild-targets.md#pack-target) をプロジェクトファイルに含めることをお勧めし `.nuspec` ますが、プロジェクトを `.nuspec` パックするためにファイルを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="807ea-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="807ea-322">を使用する SDK スタイル以外のプロジェクトでは `PackageReference` 、をインポートして、 `NuGet.Build.Tasks.Pack.targets` パックタスクを実行できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="807ea-323">Nuspec ファイルをパックする前に、プロジェクトを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="807ea-324">(SDK スタイルのプロジェクトには、既定でパックターゲットが含まれています)。</span><span class="sxs-lookup"><span data-stu-id="807ea-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="807ea-325">Nuspec をパッキングする場合、プロジェクトファイルのターゲットフレームワークは無関係であり、使用されません。</span><span class="sxs-lookup"><span data-stu-id="807ea-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="807ea-326">次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="807ea-327">`NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="807ea-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="807ea-328">`NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="807ea-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="807ea-329">MSBuild コマンドラインの解析方法に従い、複数のプロパティは `-p:NuspecProperties="key1=value1;key2=value2"` のように指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="807ea-330">`NuspecBasePath`: `.nuspec` ファイルのベース パス。</span><span class="sxs-lookup"><span data-stu-id="807ea-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="807ea-331">`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="807ea-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="807ea-332">MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="807ea-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="807ea-333">dotnet.exe または msbuild を使用して nuspec をパッキングすると、既定でプロジェクトがビルドされることにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="807ea-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="807ea-334">これは、プロパティを dotnet.exe に渡すことによって回避できます。これは、プロジェクトファイルの ```--no-build``` 設定 ```<NoBuild>true</NoBuild> ``` と共に、プロジェクトファイル内の設定に相当し ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="807ea-335">Nuspec ファイルをパックする .csproj ファイルの例を次に示し *ます。*</span><span class="sxs-lookup"><span data-stu-id="807ea-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="807ea-336">カスタマイズされたパッケージを作成するための高度な拡張ポイント</span><span class="sxs-lookup"><span data-stu-id="807ea-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="807ea-337">ターゲットには、 `pack` ターゲットフレームワーク固有の内部ビルドで実行される2つの拡張ポイントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="807ea-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="807ea-338">拡張ポイントは、ターゲットフレームワーク固有のコンテンツとアセンブリをパッケージに含めることをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="807ea-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="807ea-339">`TargetsForTfmSpecificBuildOutput` ターゲット: フォルダー内のファイル、 `lib` またはを使用して指定されたフォルダー内のファイルに使用し `BuildOutputTargetFolder` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="807ea-340">`TargetsForTfmSpecificContentInPackage` ターゲット: の外部のファイルに対して使用し `BuildOutputTargetFolder` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="807ea-341">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="807ea-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="807ea-342">カスタムターゲットを作成し、プロパティの値として指定し `$(TargetsForTfmSpecificBuildOutput)` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="807ea-343">(既定では lib) に移動する必要があるファイルの場合、 `BuildOutputTargetFolder` ターゲットはこれらのファイルを ItemGroup に書き込み、 `BuildOutputInPackage` 次の2つのメタデータ値を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="807ea-344">`FinalOutputPath`: ファイルの絶対パス。指定されていない場合は、ソースパスの評価に Id が使用されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="807ea-345">`TargetPath`: (省略可能) ファイルが内のサブフォルダーに入る必要があるときに設定し `lib\<TargetFramework>` ます。これは、それぞれのカルチャフォルダーの下にあるサテライトアセンブリのようになります。</span><span class="sxs-lookup"><span data-stu-id="807ea-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="807ea-346">既定値は、ファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="807ea-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="807ea-347">例:</span><span class="sxs-lookup"><span data-stu-id="807ea-347">Example:</span></span>

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="807ea-348">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="807ea-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="807ea-349">カスタムターゲットを作成し、プロパティの値として指定し `$(TargetsForTfmSpecificContentInPackage)` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="807ea-350">パッケージに含めるファイルについては、ターゲットはこれらのファイルを ItemGroup に書き込み、 `TfmSpecificPackageFile` 次のオプションのメタデータを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="807ea-351">`PackagePath`: パッケージでファイルを出力するパス。</span><span class="sxs-lookup"><span data-stu-id="807ea-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="807ea-352">複数のファイルが同じパッケージパスに追加されると、NuGet は警告を発行します。</span><span class="sxs-lookup"><span data-stu-id="807ea-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="807ea-353">`BuildAction`: ファイルに割り当てるビルドアクション。パッケージパスがフォルダー内にある場合にのみ必要です `contentFiles` 。</span><span class="sxs-lookup"><span data-stu-id="807ea-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="807ea-354">既定値は "None" です。</span><span class="sxs-lookup"><span data-stu-id="807ea-354">Defaults to "None".</span></span>

<span data-ttu-id="807ea-355">例:</span><span class="sxs-lookup"><span data-stu-id="807ea-355">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="807ea-356">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="807ea-356">restore target</span></span>

<span data-ttu-id="807ea-357">`MSBuild -t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="807ea-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="807ea-358">すべてのプロジェクト間参照を読み取ります</span><span class="sxs-lookup"><span data-stu-id="807ea-358">Read all project to project references</span></span>
1. <span data-ttu-id="807ea-359">プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します</span><span class="sxs-lookup"><span data-stu-id="807ea-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="807ea-360">MSBuild データを NuGet.Build.Tasks.dll に渡す</span><span class="sxs-lookup"><span data-stu-id="807ea-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="807ea-361">restore を実行します</span><span class="sxs-lookup"><span data-stu-id="807ea-361">Run restore</span></span>
1. <span data-ttu-id="807ea-362">パッケージのダウンロード</span><span class="sxs-lookup"><span data-stu-id="807ea-362">Download packages</span></span>
1. <span data-ttu-id="807ea-363">アセット ファイル、ターゲット、およびプロパティを出力します</span><span class="sxs-lookup"><span data-stu-id="807ea-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="807ea-364">ターゲットは、 `restore` PackageReference 形式を使用するプロジェクトに対して機能します。</span><span class="sxs-lookup"><span data-stu-id="807ea-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="807ea-365">`MSBuild 16.5+` では、形式の [オプトインもサポート](#restoring-packagereference-and-packagesconfig-with-msbuild) されてい `packages.config` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="807ea-366">ターゲットを `restore` ターゲットと組み合わせて [実行することはできません](#restoring-and-building-with-one-msbuild-command) `build` 。</span><span class="sxs-lookup"><span data-stu-id="807ea-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="807ea-367">restore のプロパティ</span><span class="sxs-lookup"><span data-stu-id="807ea-367">Restore properties</span></span>

<span data-ttu-id="807ea-368">追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。</span><span class="sxs-lookup"><span data-stu-id="807ea-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="807ea-369">また、`-p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="807ea-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="807ea-370">プロパティ</span><span class="sxs-lookup"><span data-stu-id="807ea-370">Property</span></span> | <span data-ttu-id="807ea-371">説明</span><span class="sxs-lookup"><span data-stu-id="807ea-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="807ea-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="807ea-372">RestoreSources</span></span> | <span data-ttu-id="807ea-373">パッケージ ソースのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="807ea-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="807ea-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="807ea-374">RestorePackagesPath</span></span> | <span data-ttu-id="807ea-375">ユーザー パッケージ フォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="807ea-375">User packages folder path.</span></span> |
| <span data-ttu-id="807ea-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="807ea-376">RestoreDisableParallel</span></span> | <span data-ttu-id="807ea-377">ダウンロード数を一度に 1 つまでに制限します。</span><span class="sxs-lookup"><span data-stu-id="807ea-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="807ea-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="807ea-378">RestoreConfigFile</span></span> | <span data-ttu-id="807ea-379">適用する `Nuget.Config` ファイルのパス。</span><span class="sxs-lookup"><span data-stu-id="807ea-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="807ea-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="807ea-380">RestoreNoCache</span></span> | <span data-ttu-id="807ea-381">True の場合、キャッシュされたパッケージの使用を回避します。</span><span class="sxs-lookup"><span data-stu-id="807ea-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="807ea-382">「 [グローバルパッケージとキャッシュフォルダーの管理」を](../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="807ea-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="807ea-383">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="807ea-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="807ea-384">true の場合、失敗した、または不足しているパッケージ ソースを無視します。</span><span class="sxs-lookup"><span data-stu-id="807ea-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="807ea-385">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="807ea-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="807ea-386">フォールバックフォルダー。ユーザーパッケージフォルダーを使用する場合と同じ方法で使用されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="807ea-387">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="807ea-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="807ea-388">復元中に使用する追加のソース。</span><span class="sxs-lookup"><span data-stu-id="807ea-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="807ea-389">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="807ea-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="807ea-390">復元中に使用する追加のフォールバックフォルダー。</span><span class="sxs-lookup"><span data-stu-id="807ea-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="807ea-391">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="807ea-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="807ea-392">で指定されたフォールバックフォルダーを除外します。 `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="807ea-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="807ea-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="807ea-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="807ea-394">`NuGet.Build.Tasks.dll` のパス。</span><span class="sxs-lookup"><span data-stu-id="807ea-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="807ea-395">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="807ea-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="807ea-396">復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="807ea-397">Restoreentkipnon存在 Enttargets</span><span class="sxs-lookup"><span data-stu-id="807ea-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="807ea-398">MSBuild を使用してプロジェクトが収集されると、最適化を使用してプロジェクトを収集するかどうかが決定され `SkipNonexistentTargets` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="807ea-399">設定しない場合、の既定値はに `true` なります。</span><span class="sxs-lookup"><span data-stu-id="807ea-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="807ea-400">その結果、プロジェクトのターゲットをインポートできない場合のフェールファースト動作になります。</span><span class="sxs-lookup"><span data-stu-id="807ea-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="807ea-401">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="807ea-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="807ea-402">出力フォルダー。を既定 `BaseIntermediateOutputPath` として、フォルダーをにし `obj` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="807ea-403">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="807ea-403">RestoreForce</span></span> | <span data-ttu-id="807ea-404">PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="807ea-405">このフラグを指定することは、ファイルの削除に似てい `project.assets.json` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="807ea-406">これは、http キャッシュをバイパスしません。</span><span class="sxs-lookup"><span data-stu-id="807ea-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="807ea-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="807ea-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="807ea-408">ロック ファイルの使用をオプトインします。</span><span class="sxs-lookup"><span data-stu-id="807ea-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="807ea-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="807ea-409">RestoreLockedMode</span></span> | <span data-ttu-id="807ea-410">ロックモードで復元を実行します。</span><span class="sxs-lookup"><span data-stu-id="807ea-410">Run restore in locked mode.</span></span> <span data-ttu-id="807ea-411">これは、restore が依存関係を再評価しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="807ea-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="807ea-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="807ea-412">NuGetLockFilePath</span></span> | <span data-ttu-id="807ea-413">ロックファイルのカスタムの場所。</span><span class="sxs-lookup"><span data-stu-id="807ea-413">A custom location for the lock file.</span></span> <span data-ttu-id="807ea-414">既定の場所はプロジェクトの横にあり、という名前が付けられ `packages.lock.json` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="807ea-415">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="807ea-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="807ea-416">復元によって依存関係が再計算され、警告なしでロックファイルが更新されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="807ea-417">Restoreパッケージ構成</span><span class="sxs-lookup"><span data-stu-id="807ea-417">RestorePackagesConfig</span></span> | <span data-ttu-id="807ea-418">packages.config のプロジェクトを復元するオプトインスイッチ。でのみサポートさ `MSBuild -t:restore` れます。</span><span class="sxs-lookup"><span data-stu-id="807ea-418">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="807ea-419">RestoreUseStaticGraphEvaluation</span><span class="sxs-lookup"><span data-stu-id="807ea-419">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="807ea-420">標準評価ではなく、静的なグラフの MSBuild 評価を使用するオプトインスイッチ。</span><span class="sxs-lookup"><span data-stu-id="807ea-420">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="807ea-421">静的グラフの評価は、大規模なリポジトリとソリューションで非常に高速な試験的な機能です。</span><span class="sxs-lookup"><span data-stu-id="807ea-421">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="807ea-422">例</span><span class="sxs-lookup"><span data-stu-id="807ea-422">Examples</span></span>

<span data-ttu-id="807ea-423">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="807ea-423">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="807ea-424">プロジェクト ファイル:</span><span class="sxs-lookup"><span data-stu-id="807ea-424">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="807ea-425">restore の出力</span><span class="sxs-lookup"><span data-stu-id="807ea-425">Restore outputs</span></span>

<span data-ttu-id="807ea-426">restore で、次のファイルがビルドの `obj` フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-426">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="807ea-427">ファイル</span><span class="sxs-lookup"><span data-stu-id="807ea-427">File</span></span> | <span data-ttu-id="807ea-428">説明</span><span class="sxs-lookup"><span data-stu-id="807ea-428">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="807ea-429">すべてのパッケージ参照の依存関係グラフを含みます。</span><span class="sxs-lookup"><span data-stu-id="807ea-429">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="807ea-430">パッケージに含まれる MSBuild プロパティへの参照</span><span class="sxs-lookup"><span data-stu-id="807ea-430">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="807ea-431">パッケージに含まれる MSBuild ターゲットへの参照</span><span class="sxs-lookup"><span data-stu-id="807ea-431">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="807ea-432">1つの MSBuild コマンドを使用した復元とビルド</span><span class="sxs-lookup"><span data-stu-id="807ea-432">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="807ea-433">NuGet では、MSBuild のターゲットとプロパティを表示するパッケージを復元できるため、異なるグローバルプロパティを使用して復元とビルドの評価が実行されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-433">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="807ea-434">これは、次のような場合に予期しない動作が発生する可能性があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="807ea-434">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="807ea-435">代わりに、推奨される方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="807ea-435">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="807ea-436">と同様に、同じロジックが他のターゲットにも適用され `build` ます。</span><span class="sxs-lookup"><span data-stu-id="807ea-436">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="807ea-437">MSBuild を使用した PackageReference と packages.config の復元</span><span class="sxs-lookup"><span data-stu-id="807ea-437">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="807ea-438">MSBuild 16.5 + では、packages.config もサポートされて `msbuild -t:restore` います。</span><span class="sxs-lookup"><span data-stu-id="807ea-438">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="807ea-439">`packages.config` restore は、ではなく、でのみ使用でき `MSBuild 16.5+` ます。 `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="807ea-439">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="807ea-440">MSBuild の静的グラフの評価を使用した復元</span><span class="sxs-lookup"><span data-stu-id="807ea-440">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="807ea-441">MSBuild 16.6 + を使用すると、コマンドラインから静的グラフ評価を使用する実験的な機能が追加されました。これにより、大規模なリポジトリの復元時間が大幅に短縮されます。</span><span class="sxs-lookup"><span data-stu-id="807ea-441">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="807ea-442">または、ディレクトリのプロパティを設定して有効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="807ea-442">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="807ea-443">Visual Studio 2019. x および NuGet 5.x の場合、この機能は試験的でオプトインと見なされます。</span><span class="sxs-lookup"><span data-stu-id="807ea-443">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="807ea-444">この機能が既定で有効になるタイミングの詳細については、 [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) に従ってください。</span><span class="sxs-lookup"><span data-stu-id="807ea-444">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="807ea-445">静的なグラフの復元では、復元の msbuild 部分が変更されますが、プロジェクトの読み取りと評価は復元アルゴリズムではありません。</span><span class="sxs-lookup"><span data-stu-id="807ea-445">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="807ea-446">復元アルゴリズムは、すべての NuGet ツール (NuGet.exe、MSBuild.exe、dotnet.exe、および Visual Studio) で同じです。</span><span class="sxs-lookup"><span data-stu-id="807ea-446">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="807ea-447">ほとんどのシナリオでは、静的なグラフ復元は、現在の復元とは動作が異なる場合があります。また、宣言された特定の PackageReferences または ProjectReferences が見つからない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="807ea-447">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="807ea-448">静的なグラフの復元に移行するときは、次の実行を検討してください。</span><span class="sxs-lookup"><span data-stu-id="807ea-448">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="807ea-449">NuGet は変更を報告し *ません* 。</span><span class="sxs-lookup"><span data-stu-id="807ea-449">NuGet should *not* report any changes.</span></span> <span data-ttu-id="807ea-450">不一致が発生した場合は、 [NuGet/Home](https://github.com/nuget/home/issues/new)で問題を報告してください。</span><span class="sxs-lookup"><span data-stu-id="807ea-450">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="807ea-451">復元グラフの 1 つのライブラリを置き換える</span><span class="sxs-lookup"><span data-stu-id="807ea-451">Replacing one library from a restore graph</span></span>

<span data-ttu-id="807ea-452">復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="807ea-452">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="807ea-453">まず、最上位の `PackageReference` ですべてのアセットを除外します。</span><span class="sxs-lookup"><span data-stu-id="807ea-453">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="807ea-454">次に、DLL の適切なローカル コピーに独自の参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="807ea-454">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
