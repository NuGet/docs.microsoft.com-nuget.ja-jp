---
title: "MSBuild ターゲットとしての NuGet の pack と restore | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。"
keywords: "NuGet と MSBuild, NuGet の pack ターゲット, NuGet の restore ターゲット"
ms.reviewer: karann-msft
ms.openlocfilehash: def01380e5bc3bf878e72dd437f52cd033641ca5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="58fa3-104">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="58fa3-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="58fa3-105">*NuGet 4.0 以降*</span><span class="sxs-lookup"><span data-stu-id="58fa3-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="58fa3-106">NuGet 4.0 以降では、`.csproj` ファイルの情報を直接使用できます。別の `.nuspec` または `project.json` ファイルは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="58fa3-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="58fa3-107">以前はこれらの構成ファイルに格納していたすべてのメタデータは、ここで説明するように `.csproj` ファイルに直接格納できます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="58fa3-108">MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。</span><span class="sxs-lookup"><span data-stu-id="58fa3-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="58fa3-109">これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます </span><span class="sxs-lookup"><span data-stu-id="58fa3-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="58fa3-110">(NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../tools/cli-ref-pack.md) および [restore](../tools/cli-ref-restore.md) コマンドを使用します)。</span><span class="sxs-lookup"><span data-stu-id="58fa3-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="58fa3-111">このトピックの内容</span><span class="sxs-lookup"><span data-stu-id="58fa3-111">In this topic:</span></span>

- [<span data-ttu-id="58fa3-112">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="58fa3-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="58fa3-113">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="58fa3-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="58fa3-114">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="58fa3-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="58fa3-115">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="58fa3-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="58fa3-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="58fa3-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="58fa3-117">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="58fa3-117">Target build order</span></span>

<span data-ttu-id="58fa3-118">`pack` と `restore` は MSBuild のターゲットなので、アクセスするとワークフローを強化できます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="58fa3-119">たとえば、パック後にパッケージをネットワーク共有にコピーするとします。</span><span class="sxs-lookup"><span data-stu-id="58fa3-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="58fa3-120">この場合、プロジェクト ファイルに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="58fa3-121">同様に、MSBuild タスクを記述し、独自のターゲットを記述して、MSBuild タスクで NuGet プロパティを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="58fa3-122">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="58fa3-122">pack target</span></span>

<span data-ttu-id="58fa3-123">pack ターゲット (つまり `msbuild /t:pack`) を使用すると、MSBuild は `project.json` または `.nuspec` ファイルではなく `.csproj` ファイルからの入力を描画します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="58fa3-124">以下の表は、最初の `<PropertyGroup>` ノード内の `.csproj` ファイルに追加できる MSBuild のプロパティを説明したものです。</span><span class="sxs-lookup"><span data-stu-id="58fa3-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="58fa3-125">Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="58fa3-126">便宜上、この表は、[`.nuspec` ファイル](../schema/nuspec.md)の同等のプロパティごとに整理されています。</span><span class="sxs-lookup"><span data-stu-id="58fa3-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="58fa3-127">`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="58fa3-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="58fa3-128">属性/NuSpec の値</span><span class="sxs-lookup"><span data-stu-id="58fa3-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="58fa3-129">MSBuild のプロパティ</span><span class="sxs-lookup"><span data-stu-id="58fa3-129">MSBuild Property</span></span> | <span data-ttu-id="58fa3-130">既定値</span><span class="sxs-lookup"><span data-stu-id="58fa3-130">Default</span></span> | <span data-ttu-id="58fa3-131">メモ</span><span class="sxs-lookup"><span data-stu-id="58fa3-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="58fa3-132">ID</span><span class="sxs-lookup"><span data-stu-id="58fa3-132">Id</span></span> | <span data-ttu-id="58fa3-133">PackageId</span><span class="sxs-lookup"><span data-stu-id="58fa3-133">PackageId</span></span> | <span data-ttu-id="58fa3-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="58fa3-134">AssemblyName</span></span> | <span data-ttu-id="58fa3-135">MSBuild の $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="58fa3-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="58fa3-136">Version</span><span class="sxs-lookup"><span data-stu-id="58fa3-136">Version</span></span> | <span data-ttu-id="58fa3-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="58fa3-137">PackageVersion</span></span> | <span data-ttu-id="58fa3-138">Version</span><span class="sxs-lookup"><span data-stu-id="58fa3-138">Version</span></span> | <span data-ttu-id="58fa3-139">これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345")</span><span class="sxs-lookup"><span data-stu-id="58fa3-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="58fa3-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="58fa3-140">VersionPrefix</span></span> | <span data-ttu-id="58fa3-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="58fa3-141">PackageVersionPrefix</span></span> | <span data-ttu-id="58fa3-142">(なし)</span><span class="sxs-lookup"><span data-stu-id="58fa3-142">empty</span></span> | <span data-ttu-id="58fa3-143">PackageVersion を設定すると、PackageVersionPrefix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="58fa3-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="58fa3-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="58fa3-144">VersionSuffix</span></span> | <span data-ttu-id="58fa3-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="58fa3-145">PackageVersionSuffix</span></span> | <span data-ttu-id="58fa3-146">(なし)</span><span class="sxs-lookup"><span data-stu-id="58fa3-146">empty</span></span> | <span data-ttu-id="58fa3-147">MSBuild の $(VersionSuffix)</span><span class="sxs-lookup"><span data-stu-id="58fa3-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="58fa3-148">PackageVersion を設定すると、PackageVersionSuffix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="58fa3-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="58fa3-149">作成者</span><span class="sxs-lookup"><span data-stu-id="58fa3-149">Authors</span></span> | <span data-ttu-id="58fa3-150">作成者</span><span class="sxs-lookup"><span data-stu-id="58fa3-150">Authors</span></span> | <span data-ttu-id="58fa3-151">現在のユーザーのユーザー名</span><span class="sxs-lookup"><span data-stu-id="58fa3-151">Username of the current user</span></span> | |
| <span data-ttu-id="58fa3-152">所有者</span><span class="sxs-lookup"><span data-stu-id="58fa3-152">Owners</span></span> | <span data-ttu-id="58fa3-153">N/A</span><span class="sxs-lookup"><span data-stu-id="58fa3-153">N/A</span></span> | <span data-ttu-id="58fa3-154">NuSpec にはありません</span><span class="sxs-lookup"><span data-stu-id="58fa3-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="58fa3-155">タイトル</span><span class="sxs-lookup"><span data-stu-id="58fa3-155">Title</span></span> | <span data-ttu-id="58fa3-156">タイトル</span><span class="sxs-lookup"><span data-stu-id="58fa3-156">Title</span></span> | <span data-ttu-id="58fa3-157">PackageId</span><span class="sxs-lookup"><span data-stu-id="58fa3-157">The PackageId</span></span>| |
| <span data-ttu-id="58fa3-158">説明</span><span class="sxs-lookup"><span data-stu-id="58fa3-158">Description</span></span> | <span data-ttu-id="58fa3-159">説明</span><span class="sxs-lookup"><span data-stu-id="58fa3-159">Description</span></span> | <span data-ttu-id="58fa3-160">"パッケージの説明"</span><span class="sxs-lookup"><span data-stu-id="58fa3-160">"Package Description"</span></span> | |
| <span data-ttu-id="58fa3-161">Copyright</span><span class="sxs-lookup"><span data-stu-id="58fa3-161">Copyright</span></span> | <span data-ttu-id="58fa3-162">Copyright</span><span class="sxs-lookup"><span data-stu-id="58fa3-162">Copyright</span></span> | <span data-ttu-id="58fa3-163">(なし)</span><span class="sxs-lookup"><span data-stu-id="58fa3-163">empty</span></span> | |
| <span data-ttu-id="58fa3-164">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="58fa3-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="58fa3-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="58fa3-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="58fa3-166">False</span><span class="sxs-lookup"><span data-stu-id="58fa3-166">false</span></span> | |
| <span data-ttu-id="58fa3-167">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-167">LicenseUrl</span></span> | <span data-ttu-id="58fa3-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-168">PackageLicenseUrl</span></span> | <span data-ttu-id="58fa3-169">(なし)</span><span class="sxs-lookup"><span data-stu-id="58fa3-169">empty</span></span> | |
| <span data-ttu-id="58fa3-170">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-170">ProjectUrl</span></span> | <span data-ttu-id="58fa3-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-171">PackageProjectUrl</span></span> | <span data-ttu-id="58fa3-172">(なし)</span><span class="sxs-lookup"><span data-stu-id="58fa3-172">empty</span></span> | |
| <span data-ttu-id="58fa3-173">IconUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-173">IconUrl</span></span> | <span data-ttu-id="58fa3-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-174">PackageIconUrl</span></span> | <span data-ttu-id="58fa3-175">(なし)</span><span class="sxs-lookup"><span data-stu-id="58fa3-175">empty</span></span> | |
| <span data-ttu-id="58fa3-176">Tags</span><span class="sxs-lookup"><span data-stu-id="58fa3-176">Tags</span></span> | <span data-ttu-id="58fa3-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="58fa3-177">PackageTags</span></span> | <span data-ttu-id="58fa3-178">(なし)</span><span class="sxs-lookup"><span data-stu-id="58fa3-178">empty</span></span> | <span data-ttu-id="58fa3-179">複数のタグはセミコロン (;) で区切られます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="58fa3-180">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="58fa3-180">ReleaseNotes</span></span> | <span data-ttu-id="58fa3-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="58fa3-181">PackageReleaseNotes</span></span> | <span data-ttu-id="58fa3-182">(なし)</span><span class="sxs-lookup"><span data-stu-id="58fa3-182">empty</span></span> | |
| <span data-ttu-id="58fa3-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-183">RepositoryUrl</span></span> | <span data-ttu-id="58fa3-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-184">RepositoryUrl</span></span> | <span data-ttu-id="58fa3-185">(なし)</span><span class="sxs-lookup"><span data-stu-id="58fa3-185">empty</span></span> | |
| <span data-ttu-id="58fa3-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="58fa3-186">RepositoryType</span></span> | <span data-ttu-id="58fa3-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="58fa3-187">RepositoryType</span></span> | <span data-ttu-id="58fa3-188">(なし)</span><span class="sxs-lookup"><span data-stu-id="58fa3-188">empty</span></span> | |
| <span data-ttu-id="58fa3-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="58fa3-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="58fa3-190">概要</span><span class="sxs-lookup"><span data-stu-id="58fa3-190">Summary</span></span> | <span data-ttu-id="58fa3-191">サポートなし</span><span class="sxs-lookup"><span data-stu-id="58fa3-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="58fa3-192">pack ターゲットの入力</span><span class="sxs-lookup"><span data-stu-id="58fa3-192">pack target inputs</span></span>

- <span data-ttu-id="58fa3-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="58fa3-193">IsPackable</span></span>
- <span data-ttu-id="58fa3-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="58fa3-194">PackageVersion</span></span>
- <span data-ttu-id="58fa3-195">PackageId</span><span class="sxs-lookup"><span data-stu-id="58fa3-195">PackageId</span></span>
- <span data-ttu-id="58fa3-196">作成者</span><span class="sxs-lookup"><span data-stu-id="58fa3-196">Authors</span></span>
- <span data-ttu-id="58fa3-197">説明</span><span class="sxs-lookup"><span data-stu-id="58fa3-197">Description</span></span>
- <span data-ttu-id="58fa3-198">Copyright</span><span class="sxs-lookup"><span data-stu-id="58fa3-198">Copyright</span></span>
- <span data-ttu-id="58fa3-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="58fa3-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="58fa3-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="58fa3-200">DevelopmentDependency</span></span>
- <span data-ttu-id="58fa3-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="58fa3-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-202">PackageProjectUrl</span></span>
- <span data-ttu-id="58fa3-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-203">PackageIconUrl</span></span>
- <span data-ttu-id="58fa3-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="58fa3-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="58fa3-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="58fa3-205">PackageTags</span></span>
- <span data-ttu-id="58fa3-206">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="58fa3-206">PackageOutputPath</span></span>
- <span data-ttu-id="58fa3-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="58fa3-207">IncludeSymbols</span></span>
- <span data-ttu-id="58fa3-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="58fa3-208">IncludeSource</span></span>
- <span data-ttu-id="58fa3-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="58fa3-209">PackageTypes</span></span>
- <span data-ttu-id="58fa3-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="58fa3-210">IsTool</span></span>
- <span data-ttu-id="58fa3-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-211">RepositoryUrl</span></span>
- <span data-ttu-id="58fa3-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="58fa3-212">RepositoryType</span></span>
- <span data-ttu-id="58fa3-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="58fa3-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="58fa3-214">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="58fa3-214">MinClientVersion</span></span>
- <span data-ttu-id="58fa3-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="58fa3-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="58fa3-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="58fa3-216">IncludeContentInPack</span></span>
- <span data-ttu-id="58fa3-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="58fa3-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="58fa3-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="58fa3-218">ContentTargetFolders</span></span>
- <span data-ttu-id="58fa3-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="58fa3-219">NuspecFile</span></span>
- <span data-ttu-id="58fa3-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="58fa3-220">NuspecBasePath</span></span>
- <span data-ttu-id="58fa3-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="58fa3-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="58fa3-222">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="58fa3-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="58fa3-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="58fa3-223">PackageIconUrl</span></span>

<span data-ttu-id="58fa3-224">[NuGet の問題 2582](https://github.com/NuGet/Home/issues/2582) への変更の一部として、最終的に `PackageIconUrl` は `PackageIconUri` に変更され、結果のパッケージのルートに含まれるアイコン ファイルへの相対パスを使用できるようになる予定です。</span><span class="sxs-lookup"><span data-stu-id="58fa3-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="58fa3-225">出力アセンブリ</span><span class="sxs-lookup"><span data-stu-id="58fa3-225">Output assemblies</span></span>

<span data-ttu-id="58fa3-226">`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="58fa3-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="58fa3-227">コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。</span><span class="sxs-lookup"><span data-stu-id="58fa3-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="58fa3-228">出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="58fa3-229">`IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。</span><span class="sxs-lookup"><span data-stu-id="58fa3-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="58fa3-230">`BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="58fa3-231">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="58fa3-232">パッケージ参照</span><span class="sxs-lookup"><span data-stu-id="58fa3-232">Package references</span></span>

<span data-ttu-id="58fa3-233">「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="58fa3-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="58fa3-234">プロジェクト間参照</span><span class="sxs-lookup"><span data-stu-id="58fa3-234">Project to project references</span></span>

<span data-ttu-id="58fa3-235">プロジェクト間参照は、既定で NuGet パッケージ参照として見なされています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="58fa3-236">また、次のメタデータをプロジェクト参照に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="58fa3-237">パッケージにコンテンツを含める</span><span class="sxs-lookup"><span data-stu-id="58fa3-237">Including content in a package</span></span>

<span data-ttu-id="58fa3-238">コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="58fa3-239">次のようなエントリで上書きしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="58fa3-240">次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="58fa3-241">(`content` および `contentFiles` フォルダーの両方ではなく) すべてのコンテンツを特定のルート フォルダーにのみコピーする場合、MSBuild プロパティの `ContentTargetFolders` を使用できます。このプロパティの既定値は "content;contentFiles" ですが、他の任意のフォルダー名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="58fa3-242">`ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="58fa3-243">`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="58fa3-244">空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="58fa3-245">たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="58fa3-246">また、MSBuild プロパティの `$(IncludeContentInPack)` もあります。既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="58fa3-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="58fa3-247">これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="58fa3-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="58fa3-248">上記の任意の項目に設定できる他の pack 固有のメタデータとして、NuSpec の ```contentFiles``` エントリに ```CopyToOutput``` 値と ```Flatten``` 値を設定する ```<PackageCopyToOutput>``` と ```<PackageFlatten>``` があります。</span><span class="sxs-lookup"><span data-stu-id="58fa3-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="58fa3-249">Content 項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="58fa3-250">glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="58fa3-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="58fa3-251">IncludeSymbols</span></span>

<span data-ttu-id="58fa3-252">`MSBuild /t:pack /p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="58fa3-253">`IncludeSymbols=true` を設定すると、通常のパッケージ*と*シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="58fa3-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="58fa3-254">IncludeSource</span></span>

<span data-ttu-id="58fa3-255">これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。</span><span class="sxs-lookup"><span data-stu-id="58fa3-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="58fa3-256">種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="58fa3-257">`TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。</span><span class="sxs-lookup"><span data-stu-id="58fa3-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="58fa3-258">種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-258">If a file of type Compile, is outside the project folder, then it is just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="58fa3-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="58fa3-259">IsTool</span></span>

<span data-ttu-id="58fa3-260">`MSBuild /t:pack /p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="58fa3-261">これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="58fa3-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="58fa3-262">.nuspec を使用したパック</span><span class="sxs-lookup"><span data-stu-id="58fa3-262">Packing using a .nuspec</span></span>

<span data-ttu-id="58fa3-263">パック タスクを実行するために `NuGet.Build.Tasks.Pack.targets` をインポートするプロジェクト ファイルがある場合、`.nuspec` ファイルを使用してプロジェクトをパックできます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="58fa3-264">次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。</span><span class="sxs-lookup"><span data-stu-id="58fa3-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="58fa3-265">`NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="58fa3-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="58fa3-266">`NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="58fa3-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="58fa3-267">MSBuild コマンドラインの解析方法に従い、複数のプロパティは `/p:NuspecProperties=\"key1=value1;key2=value2\"` のように指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="58fa3-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="58fa3-268">`NuspecBasePath`: `.nuspec` ファイルのベース パス。</span><span class="sxs-lookup"><span data-stu-id="58fa3-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="58fa3-269">`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="58fa3-270">MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="58fa3-271">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="58fa3-271">restore target</span></span>

<span data-ttu-id="58fa3-272">`MSBuild /t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="58fa3-273">すべてのプロジェクト間参照を読み取ります</span><span class="sxs-lookup"><span data-stu-id="58fa3-273">Read all project to project references</span></span>
1. <span data-ttu-id="58fa3-274">プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します</span><span class="sxs-lookup"><span data-stu-id="58fa3-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="58fa3-275">MSBuild データを NuGet.Build.Tasks.dll に渡します</span><span class="sxs-lookup"><span data-stu-id="58fa3-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="58fa3-276">restore を実行します</span><span class="sxs-lookup"><span data-stu-id="58fa3-276">Run restore</span></span>
1. <span data-ttu-id="58fa3-277">パッケージをダウンロードします</span><span class="sxs-lookup"><span data-stu-id="58fa3-277">Download packages</span></span>
1. <span data-ttu-id="58fa3-278">アセット ファイル、ターゲット、およびプロパティを出力します</span><span class="sxs-lookup"><span data-stu-id="58fa3-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="58fa3-279">restore のプロパティ</span><span class="sxs-lookup"><span data-stu-id="58fa3-279">Restore properties</span></span>

<span data-ttu-id="58fa3-280">追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="58fa3-281">また、`/p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="58fa3-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="58fa3-282">プロパティ</span><span class="sxs-lookup"><span data-stu-id="58fa3-282">Property</span></span> | <span data-ttu-id="58fa3-283">説明</span><span class="sxs-lookup"><span data-stu-id="58fa3-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="58fa3-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="58fa3-284">RestoreSources</span></span> | <span data-ttu-id="58fa3-285">パッケージ ソースのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="58fa3-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="58fa3-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="58fa3-286">RestorePackagesPath</span></span> | <span data-ttu-id="58fa3-287">ユーザー パッケージ フォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="58fa3-287">User packages folder path.</span></span> |
| <span data-ttu-id="58fa3-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="58fa3-288">RestoreDisableParallel</span></span> | <span data-ttu-id="58fa3-289">ダウンロード数を一度に 1 つまでに制限します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="58fa3-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="58fa3-290">RestoreConfigFile</span></span> | <span data-ttu-id="58fa3-291">適用する `Nuget.Config` ファイルのパス。</span><span class="sxs-lookup"><span data-stu-id="58fa3-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="58fa3-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="58fa3-292">RestoreNoCache</span></span> | <span data-ttu-id="58fa3-293">true の場合、Web キャッシュを使用しません。</span><span class="sxs-lookup"><span data-stu-id="58fa3-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="58fa3-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="58fa3-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="58fa3-295">true の場合、失敗した、または不足しているパッケージ ソースを無視します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="58fa3-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="58fa3-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="58fa3-297">`NuGet.Build.Tasks.dll` のパス。</span><span class="sxs-lookup"><span data-stu-id="58fa3-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="58fa3-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="58fa3-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="58fa3-299">復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="58fa3-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="58fa3-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="58fa3-300">RestoreOutputPath</span></span> | <span data-ttu-id="58fa3-301">出力フォルダー。既定値は `obj` フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="58fa3-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="58fa3-302">**例**</span><span class="sxs-lookup"><span data-stu-id="58fa3-302">**Examples**</span></span>

<span data-ttu-id="58fa3-303">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="58fa3-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="58fa3-304">プロジェクト ファイル:</span><span class="sxs-lookup"><span data-stu-id="58fa3-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="58fa3-305">restore の出力</span><span class="sxs-lookup"><span data-stu-id="58fa3-305">Restore outputs</span></span>

<span data-ttu-id="58fa3-306">restore で、次のファイルがビルドの `obj` フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="58fa3-307">ファイル</span><span class="sxs-lookup"><span data-stu-id="58fa3-307">File</span></span> | <span data-ttu-id="58fa3-308">説明</span><span class="sxs-lookup"><span data-stu-id="58fa3-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="58fa3-309">以前の `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="58fa3-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="58fa3-310">パッケージに含まれる MSBuild プロパティへの参照</span><span class="sxs-lookup"><span data-stu-id="58fa3-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="58fa3-311">パッケージに含まれる MSBuild ターゲットへの参照</span><span class="sxs-lookup"><span data-stu-id="58fa3-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="58fa3-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="58fa3-312">PackageTargetFallback</span></span> 

<span data-ttu-id="58fa3-313">`PackageTargetFallback` 要素では、パッケージの復元時に使用する、互換性のある一連のターゲットを指定できます ([`project.json` の `imports`](../schema/project-json.md#imports) に相当)。</span><span class="sxs-lookup"><span data-stu-id="58fa3-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="58fa3-314">dotnet [TxM](../schema/target-frameworks.md) を使用するパッケージが、dotnet TxM を宣言していない互換性のあるパッケージと連携できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="58fa3-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="58fa3-315">つまり、プロジェクトで dotnet TxM を使用せず、依存するすべてのパッケージに dotnet TxM を与える必要がある場合、非 dotnet プラットフォームを dotnet 対応にするためにプロジェクトに `<PackageTargetFallback>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="58fa3-316">たとえば、プロジェクトが `netstandard1.6` TxM を使用し、依存しているパッケージに `lib/net45/a.dll` と `lib/portable-net45+win81/a.dll` のみが含まれている場合、そのプロジェクトはビルドできません。</span><span class="sxs-lookup"><span data-stu-id="58fa3-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="58fa3-317">後者の DLL を構築する予定の場合は、`portable-net45+win81` DLL に互換性を持たせるために、次のように `PackageTargetFallback` を追加します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="58fa3-318">プロジェクト内のすべてのターゲットについてフォールバックを宣言するには、`Condition` 属性を省略します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="58fa3-319">また、次のように `$(PackageTargetFallback)` を含めて、既存の `PackageTargetFallback` を拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="58fa3-320">復元グラフの 1 つのライブラリを置き換える</span><span class="sxs-lookup"><span data-stu-id="58fa3-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="58fa3-321">復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="58fa3-321">If a restore is bringing the wrong assembly, it is possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="58fa3-322">まず、最上位の `PackageReference` ですべてのアセットを除外します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="58fa3-323">次に、DLL の適切なローカル コピーに独自の参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="58fa3-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
