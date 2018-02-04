---
title: "MSBuild ターゲットとしての NuGet の pack と restore | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。"
keywords: "NuGet と MSBuild, NuGet の pack ターゲット, NuGet の restore ターゲット"
ms.reviewer:
- karann-msft
ms.openlocfilehash: 6c488f49e12b014e7bd197d57041745387a4d7b4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="0576d-104">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="0576d-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="0576d-105">*NuGet 4.0 以降*</span><span class="sxs-lookup"><span data-stu-id="0576d-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="0576d-106">PackageReference 形式では、NuGet 4.0 以降が個別を使用するのではなく、プロジェクト ファイル内で直接のすべてのマニフェストのメタデータを格納できます`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="0576d-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="0576d-107">MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。</span><span class="sxs-lookup"><span data-stu-id="0576d-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="0576d-108">これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます </span><span class="sxs-lookup"><span data-stu-id="0576d-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="0576d-109">(NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../tools/cli-ref-pack.md) および [restore](../tools/cli-ref-restore.md) コマンドを使用します)。</span><span class="sxs-lookup"><span data-stu-id="0576d-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="0576d-110">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="0576d-110">Target build order</span></span>

<span data-ttu-id="0576d-111">`pack` と `restore` は MSBuild のターゲットなので、アクセスするとワークフローを強化できます。</span><span class="sxs-lookup"><span data-stu-id="0576d-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="0576d-112">たとえば、パック後にパッケージをネットワーク共有にコピーするとします。</span><span class="sxs-lookup"><span data-stu-id="0576d-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="0576d-113">この場合、プロジェクト ファイルに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="0576d-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="0576d-114">同様に、MSBuild タスクを記述し、独自のターゲットを記述して、MSBuild タスクで NuGet プロパティを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="0576d-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="0576d-115">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="0576d-115">pack target</span></span>

<span data-ttu-id="0576d-116">つまり、パック ターゲットを使用するときに`msbuild /t:pack`MSBuild がプロジェクト ファイルからの入力を描画します。</span><span class="sxs-lookup"><span data-stu-id="0576d-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="0576d-117">次の表は、最初の内のプロジェクト ファイルに追加できる MSBuild プロパティを示します`<PropertyGroup>`ノード。</span><span class="sxs-lookup"><span data-stu-id="0576d-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="0576d-118">Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="0576d-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="0576d-119">便宜上、この表は、[`.nuspec` ファイル](../reference/nuspec.md)の同等のプロパティごとに整理されています。</span><span class="sxs-lookup"><span data-stu-id="0576d-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="0576d-120">`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="0576d-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="0576d-121">属性/NuSpec の値</span><span class="sxs-lookup"><span data-stu-id="0576d-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="0576d-122">MSBuild のプロパティ</span><span class="sxs-lookup"><span data-stu-id="0576d-122">MSBuild Property</span></span> | <span data-ttu-id="0576d-123">既定値</span><span class="sxs-lookup"><span data-stu-id="0576d-123">Default</span></span> | <span data-ttu-id="0576d-124">メモ</span><span class="sxs-lookup"><span data-stu-id="0576d-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="0576d-125">ID</span><span class="sxs-lookup"><span data-stu-id="0576d-125">Id</span></span> | <span data-ttu-id="0576d-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="0576d-126">PackageId</span></span> | <span data-ttu-id="0576d-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="0576d-127">AssemblyName</span></span> | <span data-ttu-id="0576d-128">MSBuild の $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="0576d-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="0576d-129">Version</span><span class="sxs-lookup"><span data-stu-id="0576d-129">Version</span></span> | <span data-ttu-id="0576d-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="0576d-130">PackageVersion</span></span> | <span data-ttu-id="0576d-131">Version</span><span class="sxs-lookup"><span data-stu-id="0576d-131">Version</span></span> | <span data-ttu-id="0576d-132">これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345")</span><span class="sxs-lookup"><span data-stu-id="0576d-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="0576d-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0576d-133">VersionPrefix</span></span> | <span data-ttu-id="0576d-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0576d-134">PackageVersionPrefix</span></span> | <span data-ttu-id="0576d-135">(なし)</span><span class="sxs-lookup"><span data-stu-id="0576d-135">empty</span></span> | <span data-ttu-id="0576d-136">PackageVersionPrefix、PackageVersion の設定が上書きされます。</span><span class="sxs-lookup"><span data-stu-id="0576d-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="0576d-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0576d-137">VersionSuffix</span></span> | <span data-ttu-id="0576d-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0576d-138">PackageVersionSuffix</span></span> | <span data-ttu-id="0576d-139">(なし)</span><span class="sxs-lookup"><span data-stu-id="0576d-139">empty</span></span> | <span data-ttu-id="0576d-140">MSBuild の $(VersionSuffix)</span><span class="sxs-lookup"><span data-stu-id="0576d-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="0576d-141">PackageVersionSuffix、PackageVersion の設定が上書きされます。</span><span class="sxs-lookup"><span data-stu-id="0576d-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="0576d-142">Authors</span><span class="sxs-lookup"><span data-stu-id="0576d-142">Authors</span></span> | <span data-ttu-id="0576d-143">Authors</span><span class="sxs-lookup"><span data-stu-id="0576d-143">Authors</span></span> | <span data-ttu-id="0576d-144">現在のユーザーのユーザー名</span><span class="sxs-lookup"><span data-stu-id="0576d-144">Username of the current user</span></span> | |
| <span data-ttu-id="0576d-145">所有者</span><span class="sxs-lookup"><span data-stu-id="0576d-145">Owners</span></span> | <span data-ttu-id="0576d-146">N/A</span><span class="sxs-lookup"><span data-stu-id="0576d-146">N/A</span></span> | <span data-ttu-id="0576d-147">NuSpec にはありません</span><span class="sxs-lookup"><span data-stu-id="0576d-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="0576d-148">Title</span><span class="sxs-lookup"><span data-stu-id="0576d-148">Title</span></span> | <span data-ttu-id="0576d-149">Title</span><span class="sxs-lookup"><span data-stu-id="0576d-149">Title</span></span> | <span data-ttu-id="0576d-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="0576d-150">The PackageId</span></span>| |
| <span data-ttu-id="0576d-151">説明</span><span class="sxs-lookup"><span data-stu-id="0576d-151">Description</span></span> | <span data-ttu-id="0576d-152">説明</span><span class="sxs-lookup"><span data-stu-id="0576d-152">Description</span></span> | <span data-ttu-id="0576d-153">"パッケージの説明"</span><span class="sxs-lookup"><span data-stu-id="0576d-153">"Package Description"</span></span> | |
| <span data-ttu-id="0576d-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="0576d-154">Copyright</span></span> | <span data-ttu-id="0576d-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="0576d-155">Copyright</span></span> | <span data-ttu-id="0576d-156">(なし)</span><span class="sxs-lookup"><span data-stu-id="0576d-156">empty</span></span> | |
| <span data-ttu-id="0576d-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0576d-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="0576d-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0576d-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="0576d-159">False</span><span class="sxs-lookup"><span data-stu-id="0576d-159">false</span></span> | |
| <span data-ttu-id="0576d-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-160">LicenseUrl</span></span> | <span data-ttu-id="0576d-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-161">PackageLicenseUrl</span></span> | <span data-ttu-id="0576d-162">(なし)</span><span class="sxs-lookup"><span data-stu-id="0576d-162">empty</span></span> | |
| <span data-ttu-id="0576d-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-163">ProjectUrl</span></span> | <span data-ttu-id="0576d-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-164">PackageProjectUrl</span></span> | <span data-ttu-id="0576d-165">(なし)</span><span class="sxs-lookup"><span data-stu-id="0576d-165">empty</span></span> | |
| <span data-ttu-id="0576d-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-166">IconUrl</span></span> | <span data-ttu-id="0576d-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-167">PackageIconUrl</span></span> | <span data-ttu-id="0576d-168">(なし)</span><span class="sxs-lookup"><span data-stu-id="0576d-168">empty</span></span> | |
| <span data-ttu-id="0576d-169">Tags</span><span class="sxs-lookup"><span data-stu-id="0576d-169">Tags</span></span> | <span data-ttu-id="0576d-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="0576d-170">PackageTags</span></span> | <span data-ttu-id="0576d-171">(なし)</span><span class="sxs-lookup"><span data-stu-id="0576d-171">empty</span></span> | <span data-ttu-id="0576d-172">複数のタグはセミコロン (;) で区切られます。</span><span class="sxs-lookup"><span data-stu-id="0576d-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="0576d-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0576d-173">ReleaseNotes</span></span> | <span data-ttu-id="0576d-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0576d-174">PackageReleaseNotes</span></span> | <span data-ttu-id="0576d-175">(なし)</span><span class="sxs-lookup"><span data-stu-id="0576d-175">empty</span></span> | |
| <span data-ttu-id="0576d-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-176">RepositoryUrl</span></span> | <span data-ttu-id="0576d-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-177">RepositoryUrl</span></span> | <span data-ttu-id="0576d-178">(なし)</span><span class="sxs-lookup"><span data-stu-id="0576d-178">empty</span></span> | |
| <span data-ttu-id="0576d-179">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0576d-179">RepositoryType</span></span> | <span data-ttu-id="0576d-180">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0576d-180">RepositoryType</span></span> | <span data-ttu-id="0576d-181">(なし)</span><span class="sxs-lookup"><span data-stu-id="0576d-181">empty</span></span> | |
| <span data-ttu-id="0576d-182">PackageType</span><span class="sxs-lookup"><span data-stu-id="0576d-182">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="0576d-183">まとめ</span><span class="sxs-lookup"><span data-stu-id="0576d-183">Summary</span></span> | <span data-ttu-id="0576d-184">サポートなし</span><span class="sxs-lookup"><span data-stu-id="0576d-184">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="0576d-185">pack ターゲットの入力</span><span class="sxs-lookup"><span data-stu-id="0576d-185">pack target inputs</span></span>

- <span data-ttu-id="0576d-186">IsPackable</span><span class="sxs-lookup"><span data-stu-id="0576d-186">IsPackable</span></span>
- <span data-ttu-id="0576d-187">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="0576d-187">PackageVersion</span></span>
- <span data-ttu-id="0576d-188">PackageId</span><span class="sxs-lookup"><span data-stu-id="0576d-188">PackageId</span></span>
- <span data-ttu-id="0576d-189">Authors</span><span class="sxs-lookup"><span data-stu-id="0576d-189">Authors</span></span>
- <span data-ttu-id="0576d-190">説明</span><span class="sxs-lookup"><span data-stu-id="0576d-190">Description</span></span>
- <span data-ttu-id="0576d-191">Copyright</span><span class="sxs-lookup"><span data-stu-id="0576d-191">Copyright</span></span>
- <span data-ttu-id="0576d-192">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0576d-192">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="0576d-193">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="0576d-193">DevelopmentDependency</span></span>
- <span data-ttu-id="0576d-194">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-194">PackageLicenseUrl</span></span>
- <span data-ttu-id="0576d-195">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-195">PackageProjectUrl</span></span>
- <span data-ttu-id="0576d-196">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-196">PackageIconUrl</span></span>
- <span data-ttu-id="0576d-197">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0576d-197">PackageReleaseNotes</span></span>
- <span data-ttu-id="0576d-198">PackageTags</span><span class="sxs-lookup"><span data-stu-id="0576d-198">PackageTags</span></span>
- <span data-ttu-id="0576d-199">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="0576d-199">PackageOutputPath</span></span>
- <span data-ttu-id="0576d-200">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="0576d-200">IncludeSymbols</span></span>
- <span data-ttu-id="0576d-201">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="0576d-201">IncludeSource</span></span>
- <span data-ttu-id="0576d-202">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="0576d-202">PackageTypes</span></span>
- <span data-ttu-id="0576d-203">IsTool</span><span class="sxs-lookup"><span data-stu-id="0576d-203">IsTool</span></span>
- <span data-ttu-id="0576d-204">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-204">RepositoryUrl</span></span>
- <span data-ttu-id="0576d-205">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0576d-205">RepositoryType</span></span>
- <span data-ttu-id="0576d-206">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="0576d-206">NoPackageAnalysis</span></span>
- <span data-ttu-id="0576d-207">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="0576d-207">MinClientVersion</span></span>
- <span data-ttu-id="0576d-208">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="0576d-208">IncludeBuildOutput</span></span>
- <span data-ttu-id="0576d-209">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="0576d-209">IncludeContentInPack</span></span>
- <span data-ttu-id="0576d-210">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="0576d-210">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="0576d-211">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="0576d-211">ContentTargetFolders</span></span>
- <span data-ttu-id="0576d-212">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="0576d-212">NuspecFile</span></span>
- <span data-ttu-id="0576d-213">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="0576d-213">NuspecBasePath</span></span>
- <span data-ttu-id="0576d-214">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="0576d-214">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="0576d-215">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="0576d-215">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="0576d-216">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0576d-216">PackageIconUrl</span></span>

<span data-ttu-id="0576d-217">[NuGet の問題 2582](https://github.com/NuGet/Home/issues/2582) への変更の一部として、最終的に `PackageIconUrl` は `PackageIconUri` に変更され、結果のパッケージのルートに含まれるアイコン ファイルへの相対パスを使用できるようになる予定です。</span><span class="sxs-lookup"><span data-stu-id="0576d-217">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="0576d-218">出力アセンブリ</span><span class="sxs-lookup"><span data-stu-id="0576d-218">Output assemblies</span></span>

<span data-ttu-id="0576d-219">`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="0576d-219">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="0576d-220">コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。</span><span class="sxs-lookup"><span data-stu-id="0576d-220">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="0576d-221">出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。</span><span class="sxs-lookup"><span data-stu-id="0576d-221">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="0576d-222">`IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。</span><span class="sxs-lookup"><span data-stu-id="0576d-222">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="0576d-223">`BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="0576d-223">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="0576d-224">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="0576d-224">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="0576d-225">パッケージ参照</span><span class="sxs-lookup"><span data-stu-id="0576d-225">Package references</span></span>

<span data-ttu-id="0576d-226">「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0576d-226">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="0576d-227">プロジェクト間参照</span><span class="sxs-lookup"><span data-stu-id="0576d-227">Project to project references</span></span>

<span data-ttu-id="0576d-228">プロジェクト間参照は、既定で NuGet パッケージ参照として見なされています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="0576d-228">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="0576d-229">また、次のメタデータをプロジェクト参照に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="0576d-229">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="0576d-230">パッケージにコンテンツを含める</span><span class="sxs-lookup"><span data-stu-id="0576d-230">Including content in a package</span></span>

<span data-ttu-id="0576d-231">コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="0576d-231">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="0576d-232">次のようなエントリで上書きしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="0576d-232">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="0576d-233">次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="0576d-233">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="0576d-234">(`content` および `contentFiles` フォルダーの両方ではなく) すべてのコンテンツを特定のルート フォルダーにのみコピーする場合、MSBuild プロパティの `ContentTargetFolders` を使用できます。このプロパティの既定値は "content;contentFiles" ですが、他の任意のフォルダー名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="0576d-234">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="0576d-235">`ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="0576d-235">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="0576d-236">`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="0576d-236">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="0576d-237">空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="0576d-237">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="0576d-238">たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="0576d-238">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="0576d-239">また、MSBuild プロパティの `$(IncludeContentInPack)` もあります。既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="0576d-239">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="0576d-240">これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="0576d-240">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="0576d-241">上記の任意の項目に設定できる他の pack 固有のメタデータとして、NuSpec の ```contentFiles``` エントリに ```CopyToOutput``` 値と ```Flatten``` 値を設定する ```<PackageCopyToOutput>``` と ```<PackageFlatten>``` があります。</span><span class="sxs-lookup"><span data-stu-id="0576d-241">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="0576d-242">コンテンツ項目とは別に、`<Pack>`と`<PackagePath>`メタデータを内のファイルのコンパイル、埋め込まれたリソース、ApplicationDefinition、ページ、リソース、スプラッシュ スクリーン、DesignData、DesignDataWithDesignTimeCreateableTypes ビルド アクションを設定することもできます。、、、CodeAnalysisDictionary、AndroidAsset、AndroidResource BundleResource または None です。</span><span class="sxs-lookup"><span data-stu-id="0576d-242">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="0576d-243">glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="0576d-243">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="0576d-244">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="0576d-244">IncludeSymbols</span></span>

<span data-ttu-id="0576d-245">`MSBuild /t:pack /p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="0576d-245">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="0576d-246">`IncludeSymbols=true` を設定すると、通常のパッケージ*と*シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="0576d-246">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="0576d-247">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="0576d-247">IncludeSource</span></span>

<span data-ttu-id="0576d-248">これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。</span><span class="sxs-lookup"><span data-stu-id="0576d-248">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="0576d-249">種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="0576d-249">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="0576d-250">`TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。</span><span class="sxs-lookup"><span data-stu-id="0576d-250">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="0576d-251">種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="0576d-251">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="0576d-252">IsTool</span><span class="sxs-lookup"><span data-stu-id="0576d-252">IsTool</span></span>

<span data-ttu-id="0576d-253">`MSBuild /t:pack /p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="0576d-253">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="0576d-254">これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="0576d-254">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="0576d-255">.nuspec を使用したパック</span><span class="sxs-lookup"><span data-stu-id="0576d-255">Packing using a .nuspec</span></span>

<span data-ttu-id="0576d-256">パック タスクを実行するために `NuGet.Build.Tasks.Pack.targets` をインポートするプロジェクト ファイルがある場合、`.nuspec` ファイルを使用してプロジェクトをパックできます。</span><span class="sxs-lookup"><span data-stu-id="0576d-256">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="0576d-257">次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。</span><span class="sxs-lookup"><span data-stu-id="0576d-257">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="0576d-258">`NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="0576d-258">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="0576d-259">`NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="0576d-259">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="0576d-260">MSBuild コマンドラインの解析方法に従い、複数のプロパティは `/p:NuspecProperties=\"key1=value1;key2=value2\"` のように指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0576d-260">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="0576d-261">`NuspecBasePath`: `.nuspec` ファイルのベース パス。</span><span class="sxs-lookup"><span data-stu-id="0576d-261">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="0576d-262">`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="0576d-262">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="0576d-263">MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="0576d-263">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="0576d-264">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="0576d-264">restore target</span></span>

<span data-ttu-id="0576d-265">`MSBuild /t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="0576d-265">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="0576d-266">すべてのプロジェクト間参照を読み取ります</span><span class="sxs-lookup"><span data-stu-id="0576d-266">Read all project to project references</span></span>
1. <span data-ttu-id="0576d-267">プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します</span><span class="sxs-lookup"><span data-stu-id="0576d-267">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="0576d-268">MSBuild データを NuGet.Build.Tasks.dll に渡します</span><span class="sxs-lookup"><span data-stu-id="0576d-268">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="0576d-269">restore を実行します</span><span class="sxs-lookup"><span data-stu-id="0576d-269">Run restore</span></span>
1. <span data-ttu-id="0576d-270">パッケージをダウンロードします</span><span class="sxs-lookup"><span data-stu-id="0576d-270">Download packages</span></span>
1. <span data-ttu-id="0576d-271">アセット ファイル、ターゲット、およびプロパティを出力します</span><span class="sxs-lookup"><span data-stu-id="0576d-271">Write assets file, targets, and props</span></span>

### <a name="restore-properties"></a><span data-ttu-id="0576d-272">restore のプロパティ</span><span class="sxs-lookup"><span data-stu-id="0576d-272">Restore properties</span></span>

<span data-ttu-id="0576d-273">追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。</span><span class="sxs-lookup"><span data-stu-id="0576d-273">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="0576d-274">また、`/p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="0576d-274">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="0576d-275">プロパティ</span><span class="sxs-lookup"><span data-stu-id="0576d-275">Property</span></span> | <span data-ttu-id="0576d-276">説明</span><span class="sxs-lookup"><span data-stu-id="0576d-276">Description</span></span> |
|--------|--------|
| <span data-ttu-id="0576d-277">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="0576d-277">RestoreSources</span></span> | <span data-ttu-id="0576d-278">パッケージ ソースのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="0576d-278">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="0576d-279">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="0576d-279">RestorePackagesPath</span></span> | <span data-ttu-id="0576d-280">ユーザー パッケージ フォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="0576d-280">User packages folder path.</span></span> |
| <span data-ttu-id="0576d-281">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="0576d-281">RestoreDisableParallel</span></span> | <span data-ttu-id="0576d-282">ダウンロード数を一度に 1 つまでに制限します。</span><span class="sxs-lookup"><span data-stu-id="0576d-282">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="0576d-283">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="0576d-283">RestoreConfigFile</span></span> | <span data-ttu-id="0576d-284">適用する `Nuget.Config` ファイルのパス。</span><span class="sxs-lookup"><span data-stu-id="0576d-284">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="0576d-285">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="0576d-285">RestoreNoCache</span></span> | <span data-ttu-id="0576d-286">true の場合、Web キャッシュを使用しません。</span><span class="sxs-lookup"><span data-stu-id="0576d-286">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="0576d-287">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="0576d-287">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="0576d-288">true の場合、失敗した、または不足しているパッケージ ソースを無視します。</span><span class="sxs-lookup"><span data-stu-id="0576d-288">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="0576d-289">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="0576d-289">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="0576d-290">`NuGet.Build.Tasks.dll` のパス。</span><span class="sxs-lookup"><span data-stu-id="0576d-290">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="0576d-291">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="0576d-291">RestoreGraphProjectInput</span></span> | <span data-ttu-id="0576d-292">復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0576d-292">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="0576d-293">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="0576d-293">RestoreOutputPath</span></span> | <span data-ttu-id="0576d-294">出力フォルダー。既定値は `obj` フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="0576d-294">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="0576d-295">使用例</span><span class="sxs-lookup"><span data-stu-id="0576d-295">Examples</span></span>

<span data-ttu-id="0576d-296">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="0576d-296">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="0576d-297">プロジェクト ファイル:</span><span class="sxs-lookup"><span data-stu-id="0576d-297">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="0576d-298">restore の出力</span><span class="sxs-lookup"><span data-stu-id="0576d-298">Restore outputs</span></span>

<span data-ttu-id="0576d-299">restore で、次のファイルがビルドの `obj` フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="0576d-299">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="0576d-300">ファイル</span><span class="sxs-lookup"><span data-stu-id="0576d-300">File</span></span> | <span data-ttu-id="0576d-301">説明</span><span class="sxs-lookup"><span data-stu-id="0576d-301">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="0576d-302">以前の `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="0576d-302">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="0576d-303">パッケージに含まれる MSBuild プロパティへの参照</span><span class="sxs-lookup"><span data-stu-id="0576d-303">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="0576d-304">パッケージに含まれる MSBuild ターゲットへの参照</span><span class="sxs-lookup"><span data-stu-id="0576d-304">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="0576d-305">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="0576d-305">PackageTargetFallback</span></span>

<span data-ttu-id="0576d-306">`PackageTargetFallback` 要素では、パッケージの復元時に使用する、互換性のある一連のターゲットを指定できます。</span><span class="sxs-lookup"><span data-stu-id="0576d-306">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="0576d-307">dotnet [TxM](../reference/target-frameworks.md) を使用するパッケージが、dotnet TxM を宣言していない互換性のあるパッケージと連携できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="0576d-307">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="0576d-308">つまり、プロジェクトで dotnet TxM を使用せず、依存するすべてのパッケージに dotnet TxM を与える必要がある場合、非 dotnet プラットフォームを dotnet 対応にするためにプロジェクトに `<PackageTargetFallback>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="0576d-308">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="0576d-309">たとえば、プロジェクトが `netstandard1.6` TxM を使用し、依存しているパッケージに `lib/net45/a.dll` と `lib/portable-net45+win81/a.dll` のみが含まれている場合、そのプロジェクトはビルドできません。</span><span class="sxs-lookup"><span data-stu-id="0576d-309">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="0576d-310">後者の DLL を構築する予定の場合は、`portable-net45+win81` DLL に互換性を持たせるために、次のように `PackageTargetFallback` を追加します。</span><span class="sxs-lookup"><span data-stu-id="0576d-310">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="0576d-311">プロジェクト内のすべてのターゲットについてフォールバックを宣言するには、`Condition` 属性を省略します。</span><span class="sxs-lookup"><span data-stu-id="0576d-311">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="0576d-312">また、次のように `$(PackageTargetFallback)` を含めて、既存の `PackageTargetFallback` を拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="0576d-312">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="0576d-313">復元グラフの 1 つのライブラリを置き換える</span><span class="sxs-lookup"><span data-stu-id="0576d-313">Replacing one library from a restore graph</span></span>

<span data-ttu-id="0576d-314">復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="0576d-314">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="0576d-315">まず、最上位の `PackageReference` ですべてのアセットを除外します。</span><span class="sxs-lookup"><span data-stu-id="0576d-315">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="0576d-316">次に、DLL の適切なローカル コピーに独自の参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="0576d-316">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
