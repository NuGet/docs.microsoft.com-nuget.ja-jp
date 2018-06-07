---
title: MSBuild ターゲットとしての NuGet の pack と restore
description: NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: f835deabe337236dcabe6654f1963984ab0687ca
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818309"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="b6dfe-103">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="b6dfe-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="b6dfe-104">*NuGet 4.0 以降*</span><span class="sxs-lookup"><span data-stu-id="b6dfe-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="b6dfe-105">NuGet 4.0 以降では、PackageReference 形式を使用することにより、すべてのマニフェスト メタデータを、個別の `.nuspec` ファイルを使用せずにプロジェクト ファイルに直接保存できます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="b6dfe-106">MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="b6dfe-107">これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます </span><span class="sxs-lookup"><span data-stu-id="b6dfe-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="b6dfe-108">(NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../tools/cli-ref-pack.md) および [restore](../tools/cli-ref-restore.md) コマンドを使用します)。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="b6dfe-109">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="b6dfe-109">Target build order</span></span>

<span data-ttu-id="b6dfe-110">`pack` と `restore` は MSBuild のターゲットなので、アクセスするとワークフローを強化できます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="b6dfe-111">たとえば、パック後にパッケージをネットワーク共有にコピーするとします。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="b6dfe-112">この場合、プロジェクト ファイルに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="b6dfe-113">同様に、MSBuild タスクを記述し、独自のターゲットを記述して、MSBuild タスクで NuGet プロパティを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="b6dfe-114">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="b6dfe-114">pack target</span></span>

<span data-ttu-id="b6dfe-115">PackageReference 形式を使用してを使用して、プロジェクトの標準的な .NET `msbuild /t:pack` NuGet パッケージの作成に使用するプロジェクト ファイルからの入力を描画します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-115">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="b6dfe-116">以下の表では、最初の `<PropertyGroup>` ノード内のプロジェクト ファイルに追加できる MSBuild のプロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="b6dfe-117">Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="b6dfe-118">便宜上、この表は、[`.nuspec` ファイル](../reference/nuspec.md)の同等のプロパティごとに整理されています。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="b6dfe-119">`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="b6dfe-120">属性/NuSpec の値</span><span class="sxs-lookup"><span data-stu-id="b6dfe-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="b6dfe-121">MSBuild のプロパティ</span><span class="sxs-lookup"><span data-stu-id="b6dfe-121">MSBuild Property</span></span> | <span data-ttu-id="b6dfe-122">既定値</span><span class="sxs-lookup"><span data-stu-id="b6dfe-122">Default</span></span> | <span data-ttu-id="b6dfe-123">メモ</span><span class="sxs-lookup"><span data-stu-id="b6dfe-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="b6dfe-124">ID</span><span class="sxs-lookup"><span data-stu-id="b6dfe-124">Id</span></span> | <span data-ttu-id="b6dfe-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="b6dfe-125">PackageId</span></span> | <span data-ttu-id="b6dfe-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="b6dfe-126">AssemblyName</span></span> | <span data-ttu-id="b6dfe-127">MSBuild の $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="b6dfe-128">Version</span><span class="sxs-lookup"><span data-stu-id="b6dfe-128">Version</span></span> | <span data-ttu-id="b6dfe-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="b6dfe-129">PackageVersion</span></span> | <span data-ttu-id="b6dfe-130">Version</span><span class="sxs-lookup"><span data-stu-id="b6dfe-130">Version</span></span> | <span data-ttu-id="b6dfe-131">これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345")</span><span class="sxs-lookup"><span data-stu-id="b6dfe-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="b6dfe-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="b6dfe-132">VersionPrefix</span></span> | <span data-ttu-id="b6dfe-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="b6dfe-133">PackageVersionPrefix</span></span> | <span data-ttu-id="b6dfe-134">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-134">empty</span></span> | <span data-ttu-id="b6dfe-135">PackageVersion を設定すると、PackageVersionPrefix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="b6dfe-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="b6dfe-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="b6dfe-136">VersionSuffix</span></span> | <span data-ttu-id="b6dfe-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="b6dfe-137">PackageVersionSuffix</span></span> | <span data-ttu-id="b6dfe-138">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-138">empty</span></span> | <span data-ttu-id="b6dfe-139">MSBuild の $(VersionSuffix)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="b6dfe-140">PackageVersion を設定すると、PackageVersionSuffix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="b6dfe-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="b6dfe-141">Authors</span><span class="sxs-lookup"><span data-stu-id="b6dfe-141">Authors</span></span> | <span data-ttu-id="b6dfe-142">Authors</span><span class="sxs-lookup"><span data-stu-id="b6dfe-142">Authors</span></span> | <span data-ttu-id="b6dfe-143">現在のユーザーのユーザー名</span><span class="sxs-lookup"><span data-stu-id="b6dfe-143">Username of the current user</span></span> | |
| <span data-ttu-id="b6dfe-144">所有者</span><span class="sxs-lookup"><span data-stu-id="b6dfe-144">Owners</span></span> | <span data-ttu-id="b6dfe-145">N/A</span><span class="sxs-lookup"><span data-stu-id="b6dfe-145">N/A</span></span> | <span data-ttu-id="b6dfe-146">NuSpec にはありません</span><span class="sxs-lookup"><span data-stu-id="b6dfe-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="b6dfe-147">Title</span><span class="sxs-lookup"><span data-stu-id="b6dfe-147">Title</span></span> | <span data-ttu-id="b6dfe-148">Title</span><span class="sxs-lookup"><span data-stu-id="b6dfe-148">Title</span></span> | <span data-ttu-id="b6dfe-149">PackageId</span><span class="sxs-lookup"><span data-stu-id="b6dfe-149">The PackageId</span></span>| |
| <span data-ttu-id="b6dfe-150">説明</span><span class="sxs-lookup"><span data-stu-id="b6dfe-150">Description</span></span> | <span data-ttu-id="b6dfe-151">説明</span><span class="sxs-lookup"><span data-stu-id="b6dfe-151">Description</span></span> | <span data-ttu-id="b6dfe-152">"パッケージの説明"</span><span class="sxs-lookup"><span data-stu-id="b6dfe-152">"Package Description"</span></span> | |
| <span data-ttu-id="b6dfe-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="b6dfe-153">Copyright</span></span> | <span data-ttu-id="b6dfe-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="b6dfe-154">Copyright</span></span> | <span data-ttu-id="b6dfe-155">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-155">empty</span></span> | |
| <span data-ttu-id="b6dfe-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b6dfe-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="b6dfe-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b6dfe-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="b6dfe-158">False</span><span class="sxs-lookup"><span data-stu-id="b6dfe-158">false</span></span> | |
| <span data-ttu-id="b6dfe-159">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-159">LicenseUrl</span></span> | <span data-ttu-id="b6dfe-160">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-160">PackageLicenseUrl</span></span> | <span data-ttu-id="b6dfe-161">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-161">empty</span></span> | |
| <span data-ttu-id="b6dfe-162">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-162">ProjectUrl</span></span> | <span data-ttu-id="b6dfe-163">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-163">PackageProjectUrl</span></span> | <span data-ttu-id="b6dfe-164">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-164">empty</span></span> | |
| <span data-ttu-id="b6dfe-165">IconUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-165">IconUrl</span></span> | <span data-ttu-id="b6dfe-166">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-166">PackageIconUrl</span></span> | <span data-ttu-id="b6dfe-167">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-167">empty</span></span> | |
| <span data-ttu-id="b6dfe-168">Tags</span><span class="sxs-lookup"><span data-stu-id="b6dfe-168">Tags</span></span> | <span data-ttu-id="b6dfe-169">PackageTags</span><span class="sxs-lookup"><span data-stu-id="b6dfe-169">PackageTags</span></span> | <span data-ttu-id="b6dfe-170">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-170">empty</span></span> | <span data-ttu-id="b6dfe-171">複数のタグはセミコロン (;) で区切られます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-171">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="b6dfe-172">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b6dfe-172">ReleaseNotes</span></span> | <span data-ttu-id="b6dfe-173">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b6dfe-173">PackageReleaseNotes</span></span> | <span data-ttu-id="b6dfe-174">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-174">empty</span></span> | |
| <span data-ttu-id="b6dfe-175">リポジトリの Url/</span><span class="sxs-lookup"><span data-stu-id="b6dfe-175">Repository/Url</span></span> | <span data-ttu-id="b6dfe-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-176">RepositoryUrl</span></span> | <span data-ttu-id="b6dfe-177">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-177">empty</span></span> | <span data-ttu-id="b6dfe-178">リポジトリの URL が複製またはソース コードを取得するために使用します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-178">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="b6dfe-179">例: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="b6dfe-179">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="b6dfe-180">リポジトリの種類/</span><span class="sxs-lookup"><span data-stu-id="b6dfe-180">Repository/Type</span></span> | <span data-ttu-id="b6dfe-181">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="b6dfe-181">RepositoryType</span></span> | <span data-ttu-id="b6dfe-182">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-182">empty</span></span> | <span data-ttu-id="b6dfe-183">リポジトリの種類。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-183">Repository type.</span></span> <span data-ttu-id="b6dfe-184">例: *git*、 *tfs*です。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-184">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="b6dfe-185">リポジトリの分岐/</span><span class="sxs-lookup"><span data-stu-id="b6dfe-185">Repository/Branch</span></span> | <span data-ttu-id="b6dfe-186">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="b6dfe-186">RepositoryBranch</span></span> | <span data-ttu-id="b6dfe-187">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-187">empty</span></span> | <span data-ttu-id="b6dfe-188">省略可能なリポジトリのブランチの情報です。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-188">Optional repository branch information.</span></span> <span data-ttu-id="b6dfe-189">*RepositoryUrl*を含めるには、このプロパティにも指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-189">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="b6dfe-190">例:*マスター* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-190">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="b6dfe-191">リポジトリ/コミット</span><span class="sxs-lookup"><span data-stu-id="b6dfe-191">Repository/Commit</span></span> | <span data-ttu-id="b6dfe-192">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="b6dfe-192">RepositoryCommit</span></span> | <span data-ttu-id="b6dfe-193">(なし)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-193">empty</span></span> | <span data-ttu-id="b6dfe-194">省略可能なリポジトリのコミットまたはパッケージをどのソースを示すために変更セットは、に対してビルドされました。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-194">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="b6dfe-195">*RepositoryUrl*を含めるには、このプロパティにも指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-195">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="b6dfe-196">例: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="b6dfe-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="b6dfe-197">PackageType</span><span class="sxs-lookup"><span data-stu-id="b6dfe-197">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="b6dfe-198">まとめ</span><span class="sxs-lookup"><span data-stu-id="b6dfe-198">Summary</span></span> | <span data-ttu-id="b6dfe-199">サポートなし</span><span class="sxs-lookup"><span data-stu-id="b6dfe-199">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="b6dfe-200">pack ターゲットの入力</span><span class="sxs-lookup"><span data-stu-id="b6dfe-200">pack target inputs</span></span>

- <span data-ttu-id="b6dfe-201">IsPackable</span><span class="sxs-lookup"><span data-stu-id="b6dfe-201">IsPackable</span></span>
- <span data-ttu-id="b6dfe-202">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="b6dfe-202">PackageVersion</span></span>
- <span data-ttu-id="b6dfe-203">PackageId</span><span class="sxs-lookup"><span data-stu-id="b6dfe-203">PackageId</span></span>
- <span data-ttu-id="b6dfe-204">Authors</span><span class="sxs-lookup"><span data-stu-id="b6dfe-204">Authors</span></span>
- <span data-ttu-id="b6dfe-205">説明</span><span class="sxs-lookup"><span data-stu-id="b6dfe-205">Description</span></span>
- <span data-ttu-id="b6dfe-206">Copyright</span><span class="sxs-lookup"><span data-stu-id="b6dfe-206">Copyright</span></span>
- <span data-ttu-id="b6dfe-207">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b6dfe-207">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="b6dfe-208">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="b6dfe-208">DevelopmentDependency</span></span>
- <span data-ttu-id="b6dfe-209">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-209">PackageLicenseUrl</span></span>
- <span data-ttu-id="b6dfe-210">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-210">PackageProjectUrl</span></span>
- <span data-ttu-id="b6dfe-211">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-211">PackageIconUrl</span></span>
- <span data-ttu-id="b6dfe-212">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b6dfe-212">PackageReleaseNotes</span></span>
- <span data-ttu-id="b6dfe-213">PackageTags</span><span class="sxs-lookup"><span data-stu-id="b6dfe-213">PackageTags</span></span>
- <span data-ttu-id="b6dfe-214">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="b6dfe-214">PackageOutputPath</span></span>
- <span data-ttu-id="b6dfe-215">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="b6dfe-215">IncludeSymbols</span></span>
- <span data-ttu-id="b6dfe-216">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="b6dfe-216">IncludeSource</span></span>
- <span data-ttu-id="b6dfe-217">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="b6dfe-217">PackageTypes</span></span>
- <span data-ttu-id="b6dfe-218">IsTool</span><span class="sxs-lookup"><span data-stu-id="b6dfe-218">IsTool</span></span>
- <span data-ttu-id="b6dfe-219">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-219">RepositoryUrl</span></span>
- <span data-ttu-id="b6dfe-220">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="b6dfe-220">RepositoryType</span></span>
- <span data-ttu-id="b6dfe-221">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="b6dfe-221">RepositoryBranch</span></span>
- <span data-ttu-id="b6dfe-222">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="b6dfe-222">RepositoryCommit</span></span>
- <span data-ttu-id="b6dfe-223">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="b6dfe-223">NoPackageAnalysis</span></span>
- <span data-ttu-id="b6dfe-224">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="b6dfe-224">MinClientVersion</span></span>
- <span data-ttu-id="b6dfe-225">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="b6dfe-225">IncludeBuildOutput</span></span>
- <span data-ttu-id="b6dfe-226">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="b6dfe-226">IncludeContentInPack</span></span>
- <span data-ttu-id="b6dfe-227">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="b6dfe-227">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="b6dfe-228">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="b6dfe-228">ContentTargetFolders</span></span>
- <span data-ttu-id="b6dfe-229">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="b6dfe-229">NuspecFile</span></span>
- <span data-ttu-id="b6dfe-230">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="b6dfe-230">NuspecBasePath</span></span>
- <span data-ttu-id="b6dfe-231">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="b6dfe-231">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="b6dfe-232">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="b6dfe-232">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="b6dfe-233">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b6dfe-233">PackageIconUrl</span></span>

<span data-ttu-id="b6dfe-234">変更の一環として[NuGet 問題 352](https://github.com/NuGet/Home/issues/352)、`PackageIconUrl`に最終的に変更されます`PackageIconUri`は、作成したパッケージのルートに含まれているアイコン ファイルへの相対パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-234">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="b6dfe-235">出力アセンブリ</span><span class="sxs-lookup"><span data-stu-id="b6dfe-235">Output assemblies</span></span>

<span data-ttu-id="b6dfe-236">`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-236">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="b6dfe-237">コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-237">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="b6dfe-238">出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-238">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="b6dfe-239">`IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-239">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="b6dfe-240">`BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-240">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="b6dfe-241">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-241">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="b6dfe-242">パッケージ参照</span><span class="sxs-lookup"><span data-stu-id="b6dfe-242">Package references</span></span>

<span data-ttu-id="b6dfe-243">「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-243">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="b6dfe-244">プロジェクト間参照</span><span class="sxs-lookup"><span data-stu-id="b6dfe-244">Project to project references</span></span>

<span data-ttu-id="b6dfe-245">プロジェクト間参照は、既定で NuGet パッケージ参照として見なされています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-245">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="b6dfe-246">また、次のメタデータをプロジェクト参照に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-246">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="b6dfe-247">パッケージにコンテンツを含める</span><span class="sxs-lookup"><span data-stu-id="b6dfe-247">Including content in a package</span></span>

<span data-ttu-id="b6dfe-248">コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-248">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="b6dfe-249">次のようなエントリで上書きしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-249">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="b6dfe-250">次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-250">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="b6dfe-251">(`content` および `contentFiles` フォルダーの両方ではなく) すべてのコンテンツを特定のルート フォルダーにのみコピーする場合、MSBuild プロパティの `ContentTargetFolders` を使用できます。このプロパティの既定値は "content;contentFiles" ですが、他の任意のフォルダー名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-251">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="b6dfe-252">`ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-252">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="b6dfe-253">`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-253">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="b6dfe-254">空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-254">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="b6dfe-255">たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-255">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="b6dfe-256">また、MSBuild プロパティの `$(IncludeContentInPack)` もあります。既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-256">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="b6dfe-257">これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-257">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="b6dfe-258">上記の任意の項目に設定できる他の pack 固有のメタデータとして、NuSpec の ```contentFiles``` エントリに ```CopyToOutput``` 値と ```Flatten``` 値を設定する ```<PackageCopyToOutput>``` と ```<PackageFlatten>``` があります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-258">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="b6dfe-259">コンテンツ項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-259">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="b6dfe-260">glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-260">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="b6dfe-261">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="b6dfe-261">IncludeSymbols</span></span>

<span data-ttu-id="b6dfe-262">`MSBuild /t:pack /p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-262">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="b6dfe-263">`IncludeSymbols=true` を設定すると、通常のパッケージ*と*シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-263">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="b6dfe-264">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="b6dfe-264">IncludeSource</span></span>

<span data-ttu-id="b6dfe-265">これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-265">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="b6dfe-266">種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-266">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="b6dfe-267">`TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-267">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="b6dfe-268">種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-268">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="b6dfe-269">IsTool</span><span class="sxs-lookup"><span data-stu-id="b6dfe-269">IsTool</span></span>

<span data-ttu-id="b6dfe-270">`MSBuild /t:pack /p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-270">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="b6dfe-271">これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-271">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="b6dfe-272">.nuspec を使用したパック</span><span class="sxs-lookup"><span data-stu-id="b6dfe-272">Packing using a .nuspec</span></span>

<span data-ttu-id="b6dfe-273">使用することができます、 `.nuspec` SDK プロジェクト ファイルをインポートする場合は、プロジェクトをパッケージ ファイル`NuGet.Build.Tasks.Pack.targets`パックのタスクを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-273">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="b6dfe-274">Nuspec ファイルをパックする前に、プロジェクトを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-274">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="b6dfe-275">プロジェクト ファイルのターゲット フレームワークは使用されませんし、梱包、nuspec ときは使用されません。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-275">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="b6dfe-276">次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-276">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="b6dfe-277">`NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-277">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="b6dfe-278">`NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-278">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="b6dfe-279">MSBuild コマンドラインの解析方法に従い、複数のプロパティは `/p:NuspecProperties=\"key1=value1;key2=value2\"` のように指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-279">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="b6dfe-280">`NuspecBasePath`: `.nuspec` ファイルのベース パス。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-280">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="b6dfe-281">`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-281">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="b6dfe-282">MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-282">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="b6dfe-283">既定では、プロジェクトのビルドにパッキングする nuspec dotnet.exe または msbuild を使用して潜在顧客もことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-283">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="b6dfe-284">渡すことによってこれを回避する```--no-build```プロパティ設定の相当する dotnet.exe を```<NoBuild>true</NoBuild> ```設定と共に、プロジェクト ファイルで```<IncludeBuildOutput>false</IncludeBuildOutput> ```プロジェクト ファイル</span><span class="sxs-lookup"><span data-stu-id="b6dfe-284">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="b6dfe-285">Nuspec ファイルをパック csproj ファイルの例を示します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-285">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="b6dfe-286">カスタマイズされたパッケージを作成する拡張ポイントの詳細</span><span class="sxs-lookup"><span data-stu-id="b6dfe-286">Advanced extension points to create customized package</span></span>

<span data-ttu-id="b6dfe-287">`pack`ターゲットは、内部のターゲット フレームワーク固有のビルドで実行されている 2 つの拡張ポイントを提供します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-287">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="b6dfe-288">拡張ポイントは、ターゲット フレームワークの特定のコンテンツとパッケージにアセンブリを含むサポートします。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-288">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="b6dfe-289">`TargetsForTfmSpecificBuildOutput` ターゲット: 内のファイルの使用、`lib`フォルダー、またはフォルダーを使用して指定`BuildOutputTargetFolder`です。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-289">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="b6dfe-290">`TargetsForTfmSpecificContentInPackage` ターゲット: 外でファイルを使用して、`BuildOutputTargetFolder`です。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-290">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="b6dfe-291">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="b6dfe-291">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="b6dfe-292">カスタムのターゲットを作成しの値として指定する、`$(TargetsForTfmSpecificBuildOutput)`プロパティです。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-292">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="b6dfe-293">移動する必要があるすべてのファイルについて、 `BuildOutputTargetFolder` (既定では lib)、ターゲットは、ItemGroup にそれらのファイルを書き込む必要があります`BuildOutputInPackage`し、次の 2 つのメタデータ値を設定します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-293">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="b6dfe-294">`FinalOutputPath`: ファイルの絶対パス指定しないと、ソース パスを評価する、Id が使用されます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-294">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="b6dfe-295">`TargetPath`: (省略可能) ファイルは、内のサブフォルダーに移動する必要があるときに設定`lib\<TargetFramework>`サテライト アセンブリを、それぞれのカルチャ フォルダーの下には、その移動と同じように、します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-295">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="b6dfe-296">既定値は、ファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-296">Defaults to the name of the file.</span></span>

<span data-ttu-id="b6dfe-297">例:</span><span class="sxs-lookup"><span data-stu-id="b6dfe-297">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="b6dfe-298">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="b6dfe-298">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="b6dfe-299">カスタムのターゲットを作成しの値として指定する、`$(TargetsForTfmSpecificContentInPackage)`プロパティです。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-299">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="b6dfe-300">パッケージに含めるすべてのファイルについて、ターゲットは、ItemGroup にそれらのファイルを書き込む必要があります`TfmSpecificPackageFile`し、次のオプションのメタデータを設定します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-300">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="b6dfe-301">`PackagePath`: パス、ファイルがパッケージの出力をする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-301">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="b6dfe-302">NuGet は、複数のファイルが同じパッケージのパスに追加された場合に警告を発行します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-302">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="b6dfe-303">`BuildAction`: ビルドのアクションをファイルに割り当てるために必要なだけかどうかに、パッケージのパスが、`contentFiles`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-303">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="b6dfe-304">既定値は"None"です。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-304">Defaults to "None".</span></span>

<span data-ttu-id="b6dfe-305">例:</span><span class="sxs-lookup"><span data-stu-id="b6dfe-305">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
  <ItemGroup>
    <TfmSpecificPackageFile Include=""abc.txt"">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="b6dfe-306">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="b6dfe-306">restore target</span></span>

<span data-ttu-id="b6dfe-307">`MSBuild /t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-307">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="b6dfe-308">すべてのプロジェクト間参照を読み取ります</span><span class="sxs-lookup"><span data-stu-id="b6dfe-308">Read all project to project references</span></span>
1. <span data-ttu-id="b6dfe-309">プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します</span><span class="sxs-lookup"><span data-stu-id="b6dfe-309">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="b6dfe-310">MSBuild データを NuGet.Build.Tasks.dll に渡します</span><span class="sxs-lookup"><span data-stu-id="b6dfe-310">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="b6dfe-311">restore を実行します</span><span class="sxs-lookup"><span data-stu-id="b6dfe-311">Run restore</span></span>
1. <span data-ttu-id="b6dfe-312">パッケージをダウンロードします</span><span class="sxs-lookup"><span data-stu-id="b6dfe-312">Download packages</span></span>
1. <span data-ttu-id="b6dfe-313">アセット ファイル、ターゲット、およびプロパティを出力します</span><span class="sxs-lookup"><span data-stu-id="b6dfe-313">Write assets file, targets, and props</span></span>

<span data-ttu-id="b6dfe-314">`restore`対象 works**のみ**PackageReference 形式を使用してプロジェクトのです。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-314">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="b6dfe-315">**いない**を使用してプロジェクトの作業、`packages.config`を書式設定。 を使用して[nuget 復元](../tools/cli-ref-restore.md)代わりにします。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-315">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="b6dfe-316">restore のプロパティ</span><span class="sxs-lookup"><span data-stu-id="b6dfe-316">Restore properties</span></span>

<span data-ttu-id="b6dfe-317">追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-317">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="b6dfe-318">また、`/p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-318">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="b6dfe-319">プロパティ</span><span class="sxs-lookup"><span data-stu-id="b6dfe-319">Property</span></span> | <span data-ttu-id="b6dfe-320">説明</span><span class="sxs-lookup"><span data-stu-id="b6dfe-320">Description</span></span> |
|--------|--------|
| <span data-ttu-id="b6dfe-321">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="b6dfe-321">RestoreSources</span></span> | <span data-ttu-id="b6dfe-322">パッケージ ソースのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-322">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="b6dfe-323">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="b6dfe-323">RestorePackagesPath</span></span> | <span data-ttu-id="b6dfe-324">ユーザー パッケージ フォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-324">User packages folder path.</span></span> |
| <span data-ttu-id="b6dfe-325">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="b6dfe-325">RestoreDisableParallel</span></span> | <span data-ttu-id="b6dfe-326">ダウンロード数を一度に 1 つまでに制限します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-326">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="b6dfe-327">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="b6dfe-327">RestoreConfigFile</span></span> | <span data-ttu-id="b6dfe-328">適用する `Nuget.Config` ファイルのパス。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-328">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="b6dfe-329">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="b6dfe-329">RestoreNoCache</span></span> | <span data-ttu-id="b6dfe-330">True の場合は、キャッシュされているパッケージを使用して回避できます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-330">If true, avoids using cached packages.</span></span> <span data-ttu-id="b6dfe-331">参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-331">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="b6dfe-332">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="b6dfe-332">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="b6dfe-333">true の場合、失敗した、または不足しているパッケージ ソースを無視します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-333">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="b6dfe-334">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="b6dfe-334">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="b6dfe-335">`NuGet.Build.Tasks.dll` のパス。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-335">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="b6dfe-336">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="b6dfe-336">RestoreGraphProjectInput</span></span> | <span data-ttu-id="b6dfe-337">復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-337">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="b6dfe-338">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="b6dfe-338">RestoreOutputPath</span></span> | <span data-ttu-id="b6dfe-339">出力フォルダー。既定値は `obj` フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-339">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="b6dfe-340">使用例</span><span class="sxs-lookup"><span data-stu-id="b6dfe-340">Examples</span></span>

<span data-ttu-id="b6dfe-341">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="b6dfe-341">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="b6dfe-342">プロジェクト ファイル:</span><span class="sxs-lookup"><span data-stu-id="b6dfe-342">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="b6dfe-343">restore の出力</span><span class="sxs-lookup"><span data-stu-id="b6dfe-343">Restore outputs</span></span>

<span data-ttu-id="b6dfe-344">restore で、次のファイルがビルドの `obj` フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-344">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="b6dfe-345">ファイル</span><span class="sxs-lookup"><span data-stu-id="b6dfe-345">File</span></span> | <span data-ttu-id="b6dfe-346">説明</span><span class="sxs-lookup"><span data-stu-id="b6dfe-346">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="b6dfe-347">すべてのパッケージ参照の依存関係グラフが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-347">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="b6dfe-348">パッケージに含まれる MSBuild プロパティへの参照</span><span class="sxs-lookup"><span data-stu-id="b6dfe-348">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="b6dfe-349">パッケージに含まれる MSBuild ターゲットへの参照</span><span class="sxs-lookup"><span data-stu-id="b6dfe-349">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="b6dfe-350">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="b6dfe-350">PackageTargetFallback</span></span>

<span data-ttu-id="b6dfe-351">`PackageTargetFallback` 要素では、パッケージの復元時に使用する、互換性のある一連のターゲットを指定できます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-351">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="b6dfe-352">dotnet [TxM](../reference/target-frameworks.md) を使用するパッケージが、dotnet TxM を宣言していない互換性のあるパッケージと連携できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-352">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="b6dfe-353">つまり、プロジェクトで dotnet TxM を使用せず、依存するすべてのパッケージに dotnet TxM を与える必要がある場合、非 dotnet プラットフォームを dotnet 対応にするためにプロジェクトに `<PackageTargetFallback>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-353">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="b6dfe-354">たとえば、プロジェクトが `netstandard1.6` TxM を使用し、依存しているパッケージに `lib/net45/a.dll` と `lib/portable-net45+win81/a.dll` のみが含まれている場合、そのプロジェクトはビルドできません。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-354">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="b6dfe-355">後者の DLL を構築する予定の場合は、`portable-net45+win81` DLL に互換性を持たせるために、次のように `PackageTargetFallback` を追加します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-355">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="b6dfe-356">プロジェクト内のすべてのターゲットについてフォールバックを宣言するには、`Condition` 属性を省略します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-356">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="b6dfe-357">また、次のように `$(PackageTargetFallback)` を含めて、既存の `PackageTargetFallback` を拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-357">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="b6dfe-358">復元グラフの 1 つのライブラリを置き換える</span><span class="sxs-lookup"><span data-stu-id="b6dfe-358">Replacing one library from a restore graph</span></span>

<span data-ttu-id="b6dfe-359">復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-359">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="b6dfe-360">まず、最上位の `PackageReference` ですべてのアセットを除外します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-360">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="b6dfe-361">次に、DLL の適切なローカル コピーに独自の参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="b6dfe-361">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
