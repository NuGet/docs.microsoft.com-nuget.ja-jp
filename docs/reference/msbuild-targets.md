---
title: MSBuild ターゲットとしての NuGet の pack と restore
description: NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 6a49e410617c14e22f0d4a67d8bfe280f64f5505
ms.sourcegitcommit: 8a424829b1f70cf7590e95db61997af6ae2d7a41
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72510795"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="731b4-103">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="731b4-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="731b4-104">*NuGet 4.0 以降*</span><span class="sxs-lookup"><span data-stu-id="731b4-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="731b4-105">[PackageReference](../consume-packages/package-references-in-project-files.md)形式では、NuGet 4.0 以降では、個別の `.nuspec` ファイルを使用するのではなく、すべてのマニフェストメタデータをプロジェクトファイル内に直接格納できます。</span><span class="sxs-lookup"><span data-stu-id="731b4-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="731b4-106">MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。</span><span class="sxs-lookup"><span data-stu-id="731b4-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="731b4-107">これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます</span><span class="sxs-lookup"><span data-stu-id="731b4-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="731b4-108">MSBuild を使用して NuGet パッケージを作成する手順については、「 [msbuild を使用した nuget パッケージの作成](../create-packages/creating-a-package-msbuild.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="731b4-109">(NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../reference/cli-reference/cli-ref-pack.md) および [restore](../reference/cli-reference/cli-ref-restore.md) コマンドを使用します)。</span><span class="sxs-lookup"><span data-stu-id="731b4-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="731b4-110">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="731b4-110">Target build order</span></span>

<span data-ttu-id="731b4-111">`pack` と `restore` は MSBuild のターゲットなので、アクセスするとワークフローを強化できます。</span><span class="sxs-lookup"><span data-stu-id="731b4-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="731b4-112">たとえば、パック後にパッケージをネットワーク共有にコピーするとします。</span><span class="sxs-lookup"><span data-stu-id="731b4-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="731b4-113">この場合、プロジェクト ファイルに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="731b4-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="731b4-114">同様に、MSBuild タスクを記述し、独自のターゲットを記述して、MSBuild タスクで NuGet プロパティを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="731b4-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="731b4-115">`$(OutputPath)` は相対パスであり、プロジェクトのルートからコマンドを実行していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="731b4-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="731b4-116">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="731b4-116">pack target</span></span>

<span data-ttu-id="731b4-117">PackageReference 形式を使用する .NET Standard プロジェクトの場合、`msbuild -t:pack` を使用すると、NuGet パッケージの作成に使用するプロジェクトファイルからの入力を描画します。</span><span class="sxs-lookup"><span data-stu-id="731b4-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="731b4-118">以下の表では、最初の `<PropertyGroup>` ノード内のプロジェクト ファイルに追加できる MSBuild のプロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="731b4-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="731b4-119">Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="731b4-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="731b4-120">便宜上、この表は、[`.nuspec` ファイル](../reference/nuspec.md)の同等のプロパティごとに整理されています。</span><span class="sxs-lookup"><span data-stu-id="731b4-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="731b4-121">`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="731b4-122">属性/NuSpec の値</span><span class="sxs-lookup"><span data-stu-id="731b4-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="731b4-123">MSBuild のプロパティ</span><span class="sxs-lookup"><span data-stu-id="731b4-123">MSBuild Property</span></span> | <span data-ttu-id="731b4-124">既定</span><span class="sxs-lookup"><span data-stu-id="731b4-124">Default</span></span> | <span data-ttu-id="731b4-125">ノート</span><span class="sxs-lookup"><span data-stu-id="731b4-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="731b4-126">ID</span><span class="sxs-lookup"><span data-stu-id="731b4-126">Id</span></span> | <span data-ttu-id="731b4-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="731b4-127">PackageId</span></span> | <span data-ttu-id="731b4-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="731b4-128">AssemblyName</span></span> | <span data-ttu-id="731b4-129">MSBuild の $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="731b4-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="731b4-130">Version</span><span class="sxs-lookup"><span data-stu-id="731b4-130">Version</span></span> | <span data-ttu-id="731b4-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="731b4-131">PackageVersion</span></span> | <span data-ttu-id="731b4-132">Version</span><span class="sxs-lookup"><span data-stu-id="731b4-132">Version</span></span> | <span data-ttu-id="731b4-133">これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345")</span><span class="sxs-lookup"><span data-stu-id="731b4-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="731b4-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="731b4-134">VersionPrefix</span></span> | <span data-ttu-id="731b4-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="731b4-135">PackageVersionPrefix</span></span> | <span data-ttu-id="731b4-136">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-136">empty</span></span> | <span data-ttu-id="731b4-137">PackageVersion を設定すると、PackageVersionPrefix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="731b4-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="731b4-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="731b4-138">VersionSuffix</span></span> | <span data-ttu-id="731b4-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="731b4-139">PackageVersionSuffix</span></span> | <span data-ttu-id="731b4-140">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-140">empty</span></span> | <span data-ttu-id="731b4-141">MSBuild の $(VersionSuffix)</span><span class="sxs-lookup"><span data-stu-id="731b4-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="731b4-142">PackageVersion を設定すると、PackageVersionSuffix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="731b4-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="731b4-143">Authors</span><span class="sxs-lookup"><span data-stu-id="731b4-143">Authors</span></span> | <span data-ttu-id="731b4-144">Authors</span><span class="sxs-lookup"><span data-stu-id="731b4-144">Authors</span></span> | <span data-ttu-id="731b4-145">現在のユーザーのユーザー名</span><span class="sxs-lookup"><span data-stu-id="731b4-145">Username of the current user</span></span> | |
| <span data-ttu-id="731b4-146">所有者</span><span class="sxs-lookup"><span data-stu-id="731b4-146">Owners</span></span> | <span data-ttu-id="731b4-147">N/A</span><span class="sxs-lookup"><span data-stu-id="731b4-147">N/A</span></span> | <span data-ttu-id="731b4-148">NuSpec にはありません</span><span class="sxs-lookup"><span data-stu-id="731b4-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="731b4-149">Title</span><span class="sxs-lookup"><span data-stu-id="731b4-149">Title</span></span> | <span data-ttu-id="731b4-150">Title</span><span class="sxs-lookup"><span data-stu-id="731b4-150">Title</span></span> | <span data-ttu-id="731b4-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="731b4-151">The PackageId</span></span>| |
| <span data-ttu-id="731b4-152">説明</span><span class="sxs-lookup"><span data-stu-id="731b4-152">Description</span></span> | <span data-ttu-id="731b4-153">説明</span><span class="sxs-lookup"><span data-stu-id="731b4-153">Description</span></span> | <span data-ttu-id="731b4-154">"パッケージの説明"</span><span class="sxs-lookup"><span data-stu-id="731b4-154">"Package Description"</span></span> | |
| <span data-ttu-id="731b4-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="731b4-155">Copyright</span></span> | <span data-ttu-id="731b4-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="731b4-156">Copyright</span></span> | <span data-ttu-id="731b4-157">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-157">empty</span></span> | |
| <span data-ttu-id="731b4-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="731b4-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="731b4-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="731b4-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="731b4-160">False</span><span class="sxs-lookup"><span data-stu-id="731b4-160">false</span></span> | |
| <span data-ttu-id="731b4-161">使用</span><span class="sxs-lookup"><span data-stu-id="731b4-161">license</span></span> | <span data-ttu-id="731b4-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="731b4-162">PackageLicenseExpression</span></span> | <span data-ttu-id="731b4-163">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-163">empty</span></span> | <span data-ttu-id="731b4-164">@No__t-0 に対応します。</span><span class="sxs-lookup"><span data-stu-id="731b4-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="731b4-165">使用</span><span class="sxs-lookup"><span data-stu-id="731b4-165">license</span></span> | <span data-ttu-id="731b4-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="731b4-166">PackageLicenseFile</span></span> | <span data-ttu-id="731b4-167">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-167">empty</span></span> | <span data-ttu-id="731b4-168">`<license type="file">` に相当します。</span><span class="sxs-lookup"><span data-stu-id="731b4-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="731b4-169">参照されているライセンスファイルを明示的にパックする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="731b4-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-170">LicenseUrl</span></span> | <span data-ttu-id="731b4-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-171">PackageLicenseUrl</span></span> | <span data-ttu-id="731b4-172">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-172">empty</span></span> | <span data-ttu-id="731b4-173">`PackageLicenseUrl` は推奨されていません。パッケージのパッケージを使用してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="731b4-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-174">ProjectUrl</span></span> | <span data-ttu-id="731b4-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-175">PackageProjectUrl</span></span> | <span data-ttu-id="731b4-176">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-176">empty</span></span> | |
| <span data-ttu-id="731b4-177">アイコン</span><span class="sxs-lookup"><span data-stu-id="731b4-177">Icon</span></span> | <span data-ttu-id="731b4-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="731b4-178">PackageIcon</span></span> | <span data-ttu-id="731b4-179">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-179">empty</span></span> | <span data-ttu-id="731b4-180">参照されているアイコンイメージファイルを明示的にパックする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="731b4-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-181">IconUrl</span></span> | <span data-ttu-id="731b4-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-182">PackageIconUrl</span></span> | <span data-ttu-id="731b4-183">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-183">empty</span></span> | <span data-ttu-id="731b4-184">`PackageIconUrl` は推奨されていません。 PackageIcon プロパティを使用してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="731b4-185">Tags</span><span class="sxs-lookup"><span data-stu-id="731b4-185">Tags</span></span> | <span data-ttu-id="731b4-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="731b4-186">PackageTags</span></span> | <span data-ttu-id="731b4-187">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-187">empty</span></span> | <span data-ttu-id="731b4-188">複数のタグはセミコロン (;) で区切られます。</span><span class="sxs-lookup"><span data-stu-id="731b4-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="731b4-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="731b4-189">ReleaseNotes</span></span> | <span data-ttu-id="731b4-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="731b4-190">PackageReleaseNotes</span></span> | <span data-ttu-id="731b4-191">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-191">empty</span></span> | |
| <span data-ttu-id="731b4-192">リポジトリ/Url</span><span class="sxs-lookup"><span data-stu-id="731b4-192">Repository/Url</span></span> | <span data-ttu-id="731b4-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-193">RepositoryUrl</span></span> | <span data-ttu-id="731b4-194">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-194">empty</span></span> | <span data-ttu-id="731b4-195">ソースコードの複製または取得に使用されるリポジトリの URL。</span><span class="sxs-lookup"><span data-stu-id="731b4-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="731b4-196">例: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="731b4-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="731b4-197">リポジトリ/種類</span><span class="sxs-lookup"><span data-stu-id="731b4-197">Repository/Type</span></span> | <span data-ttu-id="731b4-198">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="731b4-198">RepositoryType</span></span> | <span data-ttu-id="731b4-199">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-199">empty</span></span> | <span data-ttu-id="731b4-200">リポジトリの種類。</span><span class="sxs-lookup"><span data-stu-id="731b4-200">Repository type.</span></span> <span data-ttu-id="731b4-201">例: *git*、 *tfs*。</span><span class="sxs-lookup"><span data-stu-id="731b4-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="731b4-202">リポジトリ/ブランチ</span><span class="sxs-lookup"><span data-stu-id="731b4-202">Repository/Branch</span></span> | <span data-ttu-id="731b4-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="731b4-203">RepositoryBranch</span></span> | <span data-ttu-id="731b4-204">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-204">empty</span></span> | <span data-ttu-id="731b4-205">リポジトリのブランチ情報 (オプション)。</span><span class="sxs-lookup"><span data-stu-id="731b4-205">Optional repository branch information.</span></span> <span data-ttu-id="731b4-206">このプロパティを含めるには、 *RepositoryUrl*も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="731b4-207">例: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="731b4-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="731b4-208">リポジトリ/コミット</span><span class="sxs-lookup"><span data-stu-id="731b4-208">Repository/Commit</span></span> | <span data-ttu-id="731b4-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="731b4-209">RepositoryCommit</span></span> | <span data-ttu-id="731b4-210">(なし)</span><span class="sxs-lookup"><span data-stu-id="731b4-210">empty</span></span> | <span data-ttu-id="731b4-211">任意のリポジトリのコミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。</span><span class="sxs-lookup"><span data-stu-id="731b4-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="731b4-212">このプロパティを含めるには、 *RepositoryUrl*も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="731b4-213">例: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="731b4-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="731b4-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="731b4-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="731b4-215">まとめ</span><span class="sxs-lookup"><span data-stu-id="731b4-215">Summary</span></span> | <span data-ttu-id="731b4-216">サポートなし</span><span class="sxs-lookup"><span data-stu-id="731b4-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="731b4-217">pack ターゲットの入力</span><span class="sxs-lookup"><span data-stu-id="731b4-217">pack target inputs</span></span>

- <span data-ttu-id="731b4-218">IsPackable</span><span class="sxs-lookup"><span data-stu-id="731b4-218">IsPackable</span></span>
- <span data-ttu-id="731b4-219">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="731b4-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="731b4-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="731b4-220">PackageVersion</span></span>
- <span data-ttu-id="731b4-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="731b4-221">PackageId</span></span>
- <span data-ttu-id="731b4-222">Authors</span><span class="sxs-lookup"><span data-stu-id="731b4-222">Authors</span></span>
- <span data-ttu-id="731b4-223">説明</span><span class="sxs-lookup"><span data-stu-id="731b4-223">Description</span></span>
- <span data-ttu-id="731b4-224">Copyright</span><span class="sxs-lookup"><span data-stu-id="731b4-224">Copyright</span></span>
- <span data-ttu-id="731b4-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="731b4-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="731b4-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="731b4-226">DevelopmentDependency</span></span>
- <span data-ttu-id="731b4-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="731b4-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="731b4-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="731b4-228">PackageLicenseFile</span></span>
- <span data-ttu-id="731b4-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="731b4-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-230">PackageProjectUrl</span></span>
- <span data-ttu-id="731b4-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-231">PackageIconUrl</span></span>
- <span data-ttu-id="731b4-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="731b4-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="731b4-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="731b4-233">PackageTags</span></span>
- <span data-ttu-id="731b4-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="731b4-234">PackageOutputPath</span></span>
- <span data-ttu-id="731b4-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="731b4-235">IncludeSymbols</span></span>
- <span data-ttu-id="731b4-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="731b4-236">IncludeSource</span></span>
- <span data-ttu-id="731b4-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="731b4-237">PackageTypes</span></span>
- <span data-ttu-id="731b4-238">IsTool</span><span class="sxs-lookup"><span data-stu-id="731b4-238">IsTool</span></span>
- <span data-ttu-id="731b4-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-239">RepositoryUrl</span></span>
- <span data-ttu-id="731b4-240">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="731b4-240">RepositoryType</span></span>
- <span data-ttu-id="731b4-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="731b4-241">RepositoryBranch</span></span>
- <span data-ttu-id="731b4-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="731b4-242">RepositoryCommit</span></span>
- <span data-ttu-id="731b4-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="731b4-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="731b4-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="731b4-244">MinClientVersion</span></span>
- <span data-ttu-id="731b4-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="731b4-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="731b4-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="731b4-246">IncludeContentInPack</span></span>
- <span data-ttu-id="731b4-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="731b4-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="731b4-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="731b4-248">ContentTargetFolders</span></span>
- <span data-ttu-id="731b4-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="731b4-249">NuspecFile</span></span>
- <span data-ttu-id="731b4-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="731b4-250">NuspecBasePath</span></span>
- <span data-ttu-id="731b4-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="731b4-251">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="731b4-252">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="731b4-252">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="731b4-253">依存関係を表示しない</span><span class="sxs-lookup"><span data-stu-id="731b4-253">Suppress dependencies</span></span>

<span data-ttu-id="731b4-254">生成された NuGet パッケージからのパッケージの依存関係を抑制するには、`SuppressDependenciesWhenPacking` を `true` に設定します。これにより、生成された nupkg ファイルからのすべての依存関係がスキップされます。</span><span class="sxs-lookup"><span data-stu-id="731b4-254">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="731b4-255">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="731b4-255">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="731b4-256">PackageIconUrl は、NuGet 5.3 + & Visual Studio 2019 version 16.3 + では非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="731b4-256">PackageIconUrl is deprecated with NuGet 5.3+ & Visual Studio 2019 version 16.3+.</span></span> <span data-ttu-id="731b4-257">代わりに[Packageicon](#packing-an-icon-image-file)を使用してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-257">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="731b4-258">アイコンイメージファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="731b4-258">Packing an icon image file</span></span>

<span data-ttu-id="731b4-259">アイコンイメージファイルをパッキングする場合は、パッケージのルートに対して相対的なパッケージパスを指定するために PackageIcon プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-259">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="731b4-260">また、ファイルがパッケージに含まれていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-260">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="731b4-261">イメージファイルのサイズは 1 MB に制限されています。</span><span class="sxs-lookup"><span data-stu-id="731b4-261">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="731b4-262">サポートされているファイル形式は、JPEG および PNG です。</span><span class="sxs-lookup"><span data-stu-id="731b4-262">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="731b4-263">64x64 のイメージ解像度をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="731b4-263">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="731b4-264">(例:</span><span class="sxs-lookup"><span data-stu-id="731b4-264">For example:</span></span>

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

<span data-ttu-id="731b4-265">[パッケージアイコンのサンプル](https://github.com/NuGet/Samples/tree/master/PackageIconExample)です。</span><span class="sxs-lookup"><span data-stu-id="731b4-265">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="731b4-266">Nuspec に相当するものについては、「 [nuspec reference for icon」を参照](nuspec.md#icon)してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-266">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="731b4-267">出力アセンブリ</span><span class="sxs-lookup"><span data-stu-id="731b4-267">Output assemblies</span></span>

<span data-ttu-id="731b4-268">`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="731b4-268">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="731b4-269">コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。</span><span class="sxs-lookup"><span data-stu-id="731b4-269">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="731b4-270">出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。</span><span class="sxs-lookup"><span data-stu-id="731b4-270">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="731b4-271">`IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。</span><span class="sxs-lookup"><span data-stu-id="731b4-271">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="731b4-272">`BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="731b4-272">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="731b4-273">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="731b4-273">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="731b4-274">パッケージ参照</span><span class="sxs-lookup"><span data-stu-id="731b4-274">Package references</span></span>

<span data-ttu-id="731b4-275">「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-275">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="731b4-276">プロジェクト間参照</span><span class="sxs-lookup"><span data-stu-id="731b4-276">Project to project references</span></span>

<span data-ttu-id="731b4-277">プロジェクト間参照は、既定で NuGet パッケージ参照として見なされています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="731b4-277">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="731b4-278">また、次のメタデータをプロジェクト参照に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="731b4-278">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="731b4-279">パッケージにコンテンツを含める</span><span class="sxs-lookup"><span data-stu-id="731b4-279">Including content in a package</span></span>

<span data-ttu-id="731b4-280">コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="731b4-280">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="731b4-281">次のようなエントリでオーバーライドしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="731b4-281">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="731b4-282">次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-282">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="731b4-283">(`content` および `contentFiles` フォルダーの両方ではなく) すべてのコンテンツを特定のルート フォルダーにのみコピーする場合、MSBuild プロパティの `ContentTargetFolders` を使用できます。このプロパティの既定値は "content;contentFiles" ですが、他の任意のフォルダー名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="731b4-283">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="731b4-284">`ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-284">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="731b4-285">`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="731b4-285">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="731b4-286">空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-286">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="731b4-287">たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-287">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="731b4-288">また、MSBuild プロパティの `$(IncludeContentInPack)` もあります。既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="731b4-288">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="731b4-289">これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="731b4-289">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="731b4-290">上記の任意の項目に設定できる他の pack 固有のメタデータとして、NuSpec の ```contentFiles``` エントリに ```CopyToOutput``` 値と ```Flatten``` 値を設定する ```<PackageCopyToOutput>``` と ```<PackageFlatten>``` があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-290">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="731b4-291">コンテンツ項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="731b4-291">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="731b4-292">glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="731b4-292">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="731b4-293">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="731b4-293">IncludeSymbols</span></span>

<span data-ttu-id="731b4-294">`MSBuild -t:pack -p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="731b4-294">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="731b4-295">`IncludeSymbols=true` を設定すると、通常のパッケージ*と*シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-295">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="731b4-296">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="731b4-296">IncludeSource</span></span>

<span data-ttu-id="731b4-297">これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。</span><span class="sxs-lookup"><span data-stu-id="731b4-297">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="731b4-298">種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-298">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="731b4-299">`TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。</span><span class="sxs-lookup"><span data-stu-id="731b4-299">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="731b4-300">種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-300">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="731b4-301">ライセンス式またはライセンスファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="731b4-301">Packing a license expression or a license file</span></span>

<span data-ttu-id="731b4-302">ライセンス式を使用する場合は、"パッケージの表示" プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-302">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="731b4-303">[ライセンス式のサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="731b4-303">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="731b4-304">[NuGet.org によって受け付けられるライセンス式とライセンスの詳細については、こちらを参照](nuspec.md#license)してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-304">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="731b4-305">ライセンスファイルをパッキングする場合は、パッケージのルートを基準としたパッケージパスを指定するために、"パッケージの作成" プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-305">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="731b4-306">また、ファイルがパッケージに含まれていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-306">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="731b4-307">(例:</span><span class="sxs-lookup"><span data-stu-id="731b4-307">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="731b4-308">[ライセンスファイルのサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="731b4-308">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="731b4-309">IsTool</span><span class="sxs-lookup"><span data-stu-id="731b4-309">IsTool</span></span>

<span data-ttu-id="731b4-310">`MSBuild -t:pack -p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="731b4-310">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="731b4-311">これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="731b4-311">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="731b4-312">.nuspec を使用したパック</span><span class="sxs-lookup"><span data-stu-id="731b4-312">Packing using a .nuspec</span></span>

<span data-ttu-id="731b4-313">通常はプロジェクトファイルの `.nuspec` ファイルにある[すべてのプロパティを含める](../reference/msbuild-targets.md#pack-target)ことをお勧めしますが、@no__t 2 ファイルを使用してプロジェクトをパックすることもできます。</span><span class="sxs-lookup"><span data-stu-id="731b4-313">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="731b4-314">@No__t-0 を使用する SDK 形式以外のプロジェクトの場合は、パックタスクを実行できるように `NuGet.Build.Tasks.Pack.targets` をインポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-314">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="731b4-315">Nuspec ファイルをパックする前に、プロジェクトを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-315">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="731b4-316">(SDK スタイルのプロジェクトには、既定でパックターゲットが含まれています)。</span><span class="sxs-lookup"><span data-stu-id="731b4-316">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="731b4-317">Nuspec をパッキングする場合、プロジェクトファイルのターゲットフレームワークは無関係であり、使用されません。</span><span class="sxs-lookup"><span data-stu-id="731b4-317">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="731b4-318">次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-318">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="731b4-319">`NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="731b4-319">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="731b4-320">`NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="731b4-320">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="731b4-321">MSBuild コマンドラインの解析方法に従い、複数のプロパティは `-p:NuspecProperties=\"key1=value1;key2=value2\"` のように指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-321">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="731b4-322">`NuspecBasePath`: `.nuspec` ファイルのベース パス。</span><span class="sxs-lookup"><span data-stu-id="731b4-322">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="731b4-323">`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="731b4-323">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="731b4-324">MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="731b4-324">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="731b4-325">Dotnet または msbuild を使用して nuspec をパッキングすると、既定でプロジェクトのビルドも実行されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-325">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="731b4-326">これを回避するには ```--no-build``` プロパティを dotnet に渡します。これは、プロジェクトファイル内の ```<NoBuild>true</NoBuild> ``` を設定した場合と同じです。また、プロジェクトファイルに ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` を設定した場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="731b4-326">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="731b4-327">Nuspec ファイルをパックする .csproj ファイルの例を次に示し*ます。*</span><span class="sxs-lookup"><span data-stu-id="731b4-327">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="731b4-328">カスタマイズしたパッケージを作成するための高度な拡張機能ポイント</span><span class="sxs-lookup"><span data-stu-id="731b4-328">Advanced extension points to create customized package</span></span>

<span data-ttu-id="731b4-329">@No__t-0 ターゲットには、ターゲットフレームワーク固有の内部ビルドで実行される2つの拡張ポイントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="731b4-329">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="731b4-330">拡張ポイントは、ターゲットフレームワーク固有のコンテンツとアセンブリをパッケージに含めることをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="731b4-330">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="731b4-331">`TargetsForTfmSpecificBuildOutput` target: `lib` フォルダー内のファイル、または `BuildOutputTargetFolder` を使用して指定されたフォルダー内のファイルに使用します。</span><span class="sxs-lookup"><span data-stu-id="731b4-331">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="731b4-332">`TargetsForTfmSpecificContentInPackage` ターゲット: `BuildOutputTargetFolder` 以外のファイルに使用します。</span><span class="sxs-lookup"><span data-stu-id="731b4-332">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="731b4-333">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="731b4-333">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="731b4-334">カスタムターゲットを作成し、`$(TargetsForTfmSpecificBuildOutput)` プロパティの値として指定します。</span><span class="sxs-lookup"><span data-stu-id="731b4-334">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="731b4-335">@No__t-0 (既定では lib) に入る必要があるファイルの場合、ターゲットはこれらのファイルを ItemGroup `BuildOutputInPackage` に書き込み、次の2つのメタデータ値を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-335">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="731b4-336">`FinalOutputPath`: ファイルの絶対パス。指定されていない場合は、ソースパスの評価に Id が使用されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-336">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="731b4-337">`TargetPath`: (省略可能) ファイルが `lib\<TargetFramework>` 内のサブフォルダーに入る必要がある場合に設定されます。これは、それぞれのカルチャフォルダーの下にあるサテライトアセンブリのようになります。</span><span class="sxs-lookup"><span data-stu-id="731b4-337">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="731b4-338">既定値は、ファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="731b4-338">Defaults to the name of the file.</span></span>

<span data-ttu-id="731b4-339">例:</span><span class="sxs-lookup"><span data-stu-id="731b4-339">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="731b4-340">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="731b4-340">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="731b4-341">カスタムターゲットを作成し、`$(TargetsForTfmSpecificContentInPackage)` プロパティの値として指定します。</span><span class="sxs-lookup"><span data-stu-id="731b4-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="731b4-342">パッケージに含めるファイルについては、ターゲットはこれらのファイルを ItemGroup `TfmSpecificPackageFile` に書き込み、次のオプションのメタデータを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-342">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="731b4-343">`PackagePath`: パッケージ内でファイルが出力されるパス。</span><span class="sxs-lookup"><span data-stu-id="731b4-343">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="731b4-344">複数のファイルが同じパッケージパスに追加されると、NuGet は警告を発行します。</span><span class="sxs-lookup"><span data-stu-id="731b4-344">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="731b4-345">`BuildAction`: パッケージパスが `contentFiles` フォルダー内にある場合にのみ必要な、ファイルに割り当てるビルドアクション。</span><span class="sxs-lookup"><span data-stu-id="731b4-345">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="731b4-346">既定値は "None" です。</span><span class="sxs-lookup"><span data-stu-id="731b4-346">Defaults to "None".</span></span>

<span data-ttu-id="731b4-347">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="731b4-347">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="731b4-348">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="731b4-348">restore target</span></span>

<span data-ttu-id="731b4-349">`MSBuild -t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="731b4-349">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="731b4-350">すべてのプロジェクト間参照を読み取ります</span><span class="sxs-lookup"><span data-stu-id="731b4-350">Read all project to project references</span></span>
1. <span data-ttu-id="731b4-351">プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します</span><span class="sxs-lookup"><span data-stu-id="731b4-351">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="731b4-352">MSBuild データを NuGet に渡します。</span><span class="sxs-lookup"><span data-stu-id="731b4-352">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="731b4-353">restore を実行します</span><span class="sxs-lookup"><span data-stu-id="731b4-353">Run restore</span></span>
1. <span data-ttu-id="731b4-354">パッケージをダウンロードします</span><span class="sxs-lookup"><span data-stu-id="731b4-354">Download packages</span></span>
1. <span data-ttu-id="731b4-355">アセット ファイル、ターゲット、およびプロパティを出力します</span><span class="sxs-lookup"><span data-stu-id="731b4-355">Write assets file, targets, and props</span></span>

<span data-ttu-id="731b4-356">@No__t-0 ターゲットは、PackageReference 形式を使用するプロジェクトに対して**のみ**機能します。</span><span class="sxs-lookup"><span data-stu-id="731b4-356">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="731b4-357">@No__t-1 形式を使用するプロジェクトでは機能し**ません**。代わりに[nuget restore](../reference/cli-reference/cli-ref-restore.md)を使用してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-357">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="731b4-358">restore のプロパティ</span><span class="sxs-lookup"><span data-stu-id="731b4-358">Restore properties</span></span>

<span data-ttu-id="731b4-359">追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。</span><span class="sxs-lookup"><span data-stu-id="731b4-359">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="731b4-360">また、`-p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="731b4-360">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="731b4-361">property</span><span class="sxs-lookup"><span data-stu-id="731b4-361">Property</span></span> | <span data-ttu-id="731b4-362">説明</span><span class="sxs-lookup"><span data-stu-id="731b4-362">Description</span></span> |
|--------|--------|
| <span data-ttu-id="731b4-363">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="731b4-363">RestoreSources</span></span> | <span data-ttu-id="731b4-364">パッケージ ソースのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="731b4-364">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="731b4-365">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="731b4-365">RestorePackagesPath</span></span> | <span data-ttu-id="731b4-366">ユーザー パッケージ フォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="731b4-366">User packages folder path.</span></span> |
| <span data-ttu-id="731b4-367">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="731b4-367">RestoreDisableParallel</span></span> | <span data-ttu-id="731b4-368">ダウンロード数を一度に 1 つまでに制限します。</span><span class="sxs-lookup"><span data-stu-id="731b4-368">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="731b4-369">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="731b4-369">RestoreConfigFile</span></span> | <span data-ttu-id="731b4-370">適用する `Nuget.Config` ファイルのパス。</span><span class="sxs-lookup"><span data-stu-id="731b4-370">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="731b4-371">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="731b4-371">RestoreNoCache</span></span> | <span data-ttu-id="731b4-372">True の場合、キャッシュされたパッケージの使用を回避します。</span><span class="sxs-lookup"><span data-stu-id="731b4-372">If true, avoids using cached packages.</span></span> <span data-ttu-id="731b4-373">「[グローバルパッケージとキャッシュフォルダーの管理」を](../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="731b4-373">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="731b4-374">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="731b4-374">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="731b4-375">true の場合、失敗した、または不足しているパッケージ ソースを無視します。</span><span class="sxs-lookup"><span data-stu-id="731b4-375">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="731b4-376">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="731b4-376">RestoreFallbackFolders</span></span> | <span data-ttu-id="731b4-377">フォールバックフォルダー。ユーザーパッケージフォルダーを使用する場合と同じ方法で使用されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-377">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="731b4-378">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="731b4-378">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="731b4-379">復元中に使用する追加のソース。</span><span class="sxs-lookup"><span data-stu-id="731b4-379">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="731b4-380">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="731b4-380">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="731b4-381">復元中に使用する追加のフォールバックフォルダー。</span><span class="sxs-lookup"><span data-stu-id="731b4-381">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="731b4-382">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="731b4-382">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="731b4-383">@No__t-0 で指定されたフォールバックフォルダーを除外します。</span><span class="sxs-lookup"><span data-stu-id="731b4-383">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="731b4-384">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="731b4-384">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="731b4-385">`NuGet.Build.Tasks.dll` のパス。</span><span class="sxs-lookup"><span data-stu-id="731b4-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="731b4-386">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="731b4-386">RestoreGraphProjectInput</span></span> | <span data-ttu-id="731b4-387">復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="731b4-387">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="731b4-388">Restoreentkipnon存在 Enttargets</span><span class="sxs-lookup"><span data-stu-id="731b4-388">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="731b4-389">MSBuild を使用してプロジェクトが収集されると、`SkipNonexistentTargets` の最適化を使用してプロジェクトを収集するかどうかが決定されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-389">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="731b4-390">設定しない場合、既定値は `true` になります。</span><span class="sxs-lookup"><span data-stu-id="731b4-390">When not set, defaults to `true`.</span></span> <span data-ttu-id="731b4-391">その結果、プロジェクトのターゲットをインポートできない場合のフェールファースト動作になります。</span><span class="sxs-lookup"><span data-stu-id="731b4-391">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="731b4-392">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="731b4-392">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="731b4-393">出力フォルダー。 `BaseIntermediateOutputPath` および `obj` フォルダーを既定とします。</span><span class="sxs-lookup"><span data-stu-id="731b4-393">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="731b4-394">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="731b4-394">RestoreForce</span></span> | <span data-ttu-id="731b4-395">PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-395">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="731b4-396">このフラグを指定することは、`project.assets.json` ファイルの削除に似ています。</span><span class="sxs-lookup"><span data-stu-id="731b4-396">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="731b4-397">これは、http キャッシュをバイパスしません。</span><span class="sxs-lookup"><span data-stu-id="731b4-397">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="731b4-398">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="731b4-398">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="731b4-399">ロックファイルの使用を解除します。</span><span class="sxs-lookup"><span data-stu-id="731b4-399">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="731b4-400">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="731b4-400">RestoreLockedMode</span></span> | <span data-ttu-id="731b4-401">ロックモードで復元を実行します。</span><span class="sxs-lookup"><span data-stu-id="731b4-401">Run restore in locked mode.</span></span> <span data-ttu-id="731b4-402">これは、restore が依存関係を再評価しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="731b4-402">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="731b4-403">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="731b4-403">NuGetLockFilePath</span></span> | <span data-ttu-id="731b4-404">ロックファイルのカスタムの場所。</span><span class="sxs-lookup"><span data-stu-id="731b4-404">A custom location for the lock file.</span></span> <span data-ttu-id="731b4-405">既定の場所はプロジェクトの横にあり、には `packages.lock.json` という名前が付けられます。</span><span class="sxs-lookup"><span data-stu-id="731b4-405">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="731b4-406">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="731b4-406">RestoreForceEvaluate</span></span> | <span data-ttu-id="731b4-407">復元によって依存関係が再計算され、警告なしでロックファイルが更新されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-407">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> | 

#### <a name="examples"></a><span data-ttu-id="731b4-408">使用例</span><span class="sxs-lookup"><span data-stu-id="731b4-408">Examples</span></span>

<span data-ttu-id="731b4-409">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="731b4-409">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="731b4-410">プロジェクト ファイル:</span><span class="sxs-lookup"><span data-stu-id="731b4-410">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="731b4-411">restore の出力</span><span class="sxs-lookup"><span data-stu-id="731b4-411">Restore outputs</span></span>

<span data-ttu-id="731b4-412">restore で、次のファイルがビルドの `obj` フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-412">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="731b4-413">ファイル</span><span class="sxs-lookup"><span data-stu-id="731b4-413">File</span></span> | <span data-ttu-id="731b4-414">説明</span><span class="sxs-lookup"><span data-stu-id="731b4-414">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="731b4-415">すべてのパッケージ参照の依存関係グラフを含みます。</span><span class="sxs-lookup"><span data-stu-id="731b4-415">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="731b4-416">パッケージに含まれる MSBuild プロパティへの参照</span><span class="sxs-lookup"><span data-stu-id="731b4-416">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="731b4-417">パッケージに含まれる MSBuild ターゲットへの参照</span><span class="sxs-lookup"><span data-stu-id="731b4-417">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="731b4-418">1つの MSBuild コマンドを使用した復元とビルド</span><span class="sxs-lookup"><span data-stu-id="731b4-418">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="731b4-419">NuGet では、MSBuild のターゲットとプロパティを表示するパッケージを復元できるため、異なるグローバルプロパティを使用して復元とビルドの評価が実行されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-419">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="731b4-420">これは、次のような場合に予期しない動作が発生する可能性があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="731b4-420">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="731b4-421">代わりに、推奨される方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="731b4-421">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="731b4-422">@No__t-0 に似た他のターゲットにも同じロジックが適用されます。</span><span class="sxs-lookup"><span data-stu-id="731b4-422">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="731b4-423">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="731b4-423">PackageTargetFallback</span></span>

<span data-ttu-id="731b4-424">`PackageTargetFallback` 要素では、パッケージの復元時に使用する、互換性のある一連のターゲットを指定できます。</span><span class="sxs-lookup"><span data-stu-id="731b4-424">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="731b4-425">dotnet [TxM](../reference/target-frameworks.md) を使用するパッケージが、dotnet TxM を宣言していない互換性のあるパッケージと連携できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="731b4-425">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="731b4-426">つまり、プロジェクトで dotnet TxM を使用せず、依存するすべてのパッケージに dotnet TxM を与える必要がある場合、非 dotnet プラットフォームを dotnet 対応にするためにプロジェクトに `<PackageTargetFallback>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="731b4-426">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="731b4-427">たとえば、プロジェクトが `netstandard1.6` TxM を使用し、依存しているパッケージに `lib/net45/a.dll` と `lib/portable-net45+win81/a.dll` のみが含まれている場合、そのプロジェクトはビルドできません。</span><span class="sxs-lookup"><span data-stu-id="731b4-427">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="731b4-428">後者の DLL を構築する予定の場合は、`portable-net45+win81` DLL に互換性を持たせるために、次のように `PackageTargetFallback` を追加します。</span><span class="sxs-lookup"><span data-stu-id="731b4-428">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="731b4-429">プロジェクト内のすべてのターゲットについてフォールバックを宣言するには、`Condition` 属性を省略します。</span><span class="sxs-lookup"><span data-stu-id="731b4-429">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="731b4-430">また、次のように `$(PackageTargetFallback)` を含めて、既存の `PackageTargetFallback` を拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="731b4-430">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="731b4-431">復元グラフの 1 つのライブラリを置き換える</span><span class="sxs-lookup"><span data-stu-id="731b4-431">Replacing one library from a restore graph</span></span>

<span data-ttu-id="731b4-432">復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="731b4-432">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="731b4-433">まず、最上位の `PackageReference` ですべてのアセットを除外します。</span><span class="sxs-lookup"><span data-stu-id="731b4-433">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="731b4-434">次に、DLL の適切なローカル コピーに独自の参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="731b4-434">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
