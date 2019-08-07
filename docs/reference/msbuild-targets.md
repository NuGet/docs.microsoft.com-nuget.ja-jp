---
title: MSBuild ターゲットとしての NuGet の pack と restore
description: NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8403ae38b5d2e907c6f06b162a18cdcd5425565b
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817525"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="56cc8-103">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="56cc8-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="56cc8-104">*NuGet 4.0 以降*</span><span class="sxs-lookup"><span data-stu-id="56cc8-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="56cc8-105">[PackageReference](../consume-packages/package-references-in-project-files.md)形式では、NuGet 4.0 以降では、個別`.nuspec`のファイルを使用するのではなく、すべてのマニフェストメタデータをプロジェクトファイル内に直接格納できます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="56cc8-106">MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。</span><span class="sxs-lookup"><span data-stu-id="56cc8-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="56cc8-107">これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます</span><span class="sxs-lookup"><span data-stu-id="56cc8-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="56cc8-108">MSBuild を使用して NuGet パッケージを作成する手順については、「 [msbuild を使用した nuget パッケージの作成](../create-packages/creating-a-package-msbuild.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="56cc8-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="56cc8-109">(NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../reference/cli-reference/cli-ref-pack.md) および [restore](../reference/cli-reference/cli-ref-restore.md) コマンドを使用します)。</span><span class="sxs-lookup"><span data-stu-id="56cc8-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="56cc8-110">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="56cc8-110">Target build order</span></span>

<span data-ttu-id="56cc8-111">`pack` と `restore` は MSBuild のターゲットなので、アクセスするとワークフローを強化できます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="56cc8-112">たとえば、パック後にパッケージをネットワーク共有にコピーするとします。</span><span class="sxs-lookup"><span data-stu-id="56cc8-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="56cc8-113">この場合、プロジェクト ファイルに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="56cc8-114">同様に、MSBuild タスクを記述し、独自のターゲットを記述して、MSBuild タスクで NuGet プロパティを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="56cc8-115">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="56cc8-115">pack target</span></span>

<span data-ttu-id="56cc8-116">PackageReference 形式を使用する .NET Standard プロジェクトでは`msbuild -t:pack` 、を使用して、NuGet パッケージの作成で使用する入力をプロジェクトファイルから描画します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-116">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="56cc8-117">以下の表では、最初の `<PropertyGroup>` ノード内のプロジェクト ファイルに追加できる MSBuild のプロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="56cc8-118">Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="56cc8-119">便宜上、この表は、[`.nuspec` ファイル](../reference/nuspec.md)の同等のプロパティごとに整理されています。</span><span class="sxs-lookup"><span data-stu-id="56cc8-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="56cc8-120">`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="56cc8-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="56cc8-121">属性/NuSpec の値</span><span class="sxs-lookup"><span data-stu-id="56cc8-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="56cc8-122">MSBuild のプロパティ</span><span class="sxs-lookup"><span data-stu-id="56cc8-122">MSBuild Property</span></span> | <span data-ttu-id="56cc8-123">既定値</span><span class="sxs-lookup"><span data-stu-id="56cc8-123">Default</span></span> | <span data-ttu-id="56cc8-124">メモ</span><span class="sxs-lookup"><span data-stu-id="56cc8-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="56cc8-125">ID</span><span class="sxs-lookup"><span data-stu-id="56cc8-125">Id</span></span> | <span data-ttu-id="56cc8-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="56cc8-126">PackageId</span></span> | <span data-ttu-id="56cc8-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="56cc8-127">AssemblyName</span></span> | <span data-ttu-id="56cc8-128">MSBuild の $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="56cc8-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="56cc8-129">Version</span><span class="sxs-lookup"><span data-stu-id="56cc8-129">Version</span></span> | <span data-ttu-id="56cc8-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="56cc8-130">PackageVersion</span></span> | <span data-ttu-id="56cc8-131">Version</span><span class="sxs-lookup"><span data-stu-id="56cc8-131">Version</span></span> | <span data-ttu-id="56cc8-132">これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345")</span><span class="sxs-lookup"><span data-stu-id="56cc8-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="56cc8-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="56cc8-133">VersionPrefix</span></span> | <span data-ttu-id="56cc8-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="56cc8-134">PackageVersionPrefix</span></span> | <span data-ttu-id="56cc8-135">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-135">empty</span></span> | <span data-ttu-id="56cc8-136">PackageVersion を設定すると、PackageVersionPrefix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="56cc8-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="56cc8-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="56cc8-137">VersionSuffix</span></span> | <span data-ttu-id="56cc8-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="56cc8-138">PackageVersionSuffix</span></span> | <span data-ttu-id="56cc8-139">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-139">empty</span></span> | <span data-ttu-id="56cc8-140">MSBuild の $(VersionSuffix)</span><span class="sxs-lookup"><span data-stu-id="56cc8-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="56cc8-141">PackageVersion を設定すると、PackageVersionSuffix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="56cc8-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="56cc8-142">Authors</span><span class="sxs-lookup"><span data-stu-id="56cc8-142">Authors</span></span> | <span data-ttu-id="56cc8-143">Authors</span><span class="sxs-lookup"><span data-stu-id="56cc8-143">Authors</span></span> | <span data-ttu-id="56cc8-144">現在のユーザーのユーザー名</span><span class="sxs-lookup"><span data-stu-id="56cc8-144">Username of the current user</span></span> | |
| <span data-ttu-id="56cc8-145">Owners</span><span class="sxs-lookup"><span data-stu-id="56cc8-145">Owners</span></span> | <span data-ttu-id="56cc8-146">N/A</span><span class="sxs-lookup"><span data-stu-id="56cc8-146">N/A</span></span> | <span data-ttu-id="56cc8-147">NuSpec にはありません</span><span class="sxs-lookup"><span data-stu-id="56cc8-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="56cc8-148">Title</span><span class="sxs-lookup"><span data-stu-id="56cc8-148">Title</span></span> | <span data-ttu-id="56cc8-149">Title</span><span class="sxs-lookup"><span data-stu-id="56cc8-149">Title</span></span> | <span data-ttu-id="56cc8-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="56cc8-150">The PackageId</span></span>| |
| <span data-ttu-id="56cc8-151">Description</span><span class="sxs-lookup"><span data-stu-id="56cc8-151">Description</span></span> | <span data-ttu-id="56cc8-152">Description</span><span class="sxs-lookup"><span data-stu-id="56cc8-152">Description</span></span> | <span data-ttu-id="56cc8-153">"パッケージの説明"</span><span class="sxs-lookup"><span data-stu-id="56cc8-153">"Package Description"</span></span> | |
| <span data-ttu-id="56cc8-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="56cc8-154">Copyright</span></span> | <span data-ttu-id="56cc8-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="56cc8-155">Copyright</span></span> | <span data-ttu-id="56cc8-156">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-156">empty</span></span> | |
| <span data-ttu-id="56cc8-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="56cc8-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="56cc8-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="56cc8-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="56cc8-159">False</span><span class="sxs-lookup"><span data-stu-id="56cc8-159">false</span></span> | |
| <span data-ttu-id="56cc8-160">license</span><span class="sxs-lookup"><span data-stu-id="56cc8-160">license</span></span> | <span data-ttu-id="56cc8-161">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="56cc8-161">PackageLicenseExpression</span></span> | <span data-ttu-id="56cc8-162">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-162">empty</span></span> | <span data-ttu-id="56cc8-163">対応しています `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="56cc8-163">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="56cc8-164">license</span><span class="sxs-lookup"><span data-stu-id="56cc8-164">license</span></span> | <span data-ttu-id="56cc8-165">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="56cc8-165">PackageLicenseFile</span></span> | <span data-ttu-id="56cc8-166">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-166">empty</span></span> | <span data-ttu-id="56cc8-167">`<license type="file">` に相当します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-167">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="56cc8-168">明示的に参照先のライセンス ファイルをパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-168">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="56cc8-169">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-169">LicenseUrl</span></span> | <span data-ttu-id="56cc8-170">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-170">PackageLicenseUrl</span></span> | <span data-ttu-id="56cc8-171">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-171">empty</span></span> | <span data-ttu-id="56cc8-172">`licenseUrl`は非推奨とされます。パッケージ化 Elicenseexpression または "パッケージの表示" プロパティを使用してください。</span><span class="sxs-lookup"><span data-stu-id="56cc8-172">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="56cc8-173">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-173">ProjectUrl</span></span> | <span data-ttu-id="56cc8-174">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-174">PackageProjectUrl</span></span> | <span data-ttu-id="56cc8-175">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-175">empty</span></span> | |
| <span data-ttu-id="56cc8-176">IconUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-176">IconUrl</span></span> | <span data-ttu-id="56cc8-177">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-177">PackageIconUrl</span></span> | <span data-ttu-id="56cc8-178">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-178">empty</span></span> | |
| <span data-ttu-id="56cc8-179">Tags</span><span class="sxs-lookup"><span data-stu-id="56cc8-179">Tags</span></span> | <span data-ttu-id="56cc8-180">PackageTags</span><span class="sxs-lookup"><span data-stu-id="56cc8-180">PackageTags</span></span> | <span data-ttu-id="56cc8-181">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-181">empty</span></span> | <span data-ttu-id="56cc8-182">複数のタグはセミコロン (;) で区切られます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-182">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="56cc8-183">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="56cc8-183">ReleaseNotes</span></span> | <span data-ttu-id="56cc8-184">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="56cc8-184">PackageReleaseNotes</span></span> | <span data-ttu-id="56cc8-185">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-185">empty</span></span> | |
| <span data-ttu-id="56cc8-186">Repository/Url</span><span class="sxs-lookup"><span data-stu-id="56cc8-186">Repository/Url</span></span> | <span data-ttu-id="56cc8-187">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-187">RepositoryUrl</span></span> | <span data-ttu-id="56cc8-188">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-188">empty</span></span> | <span data-ttu-id="56cc8-189">ソースコードの複製または取得に使用されるリポジトリの URL。</span><span class="sxs-lookup"><span data-stu-id="56cc8-189">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="56cc8-190">よう *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="56cc8-190">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="56cc8-191">Repository/Type</span><span class="sxs-lookup"><span data-stu-id="56cc8-191">Repository/Type</span></span> | <span data-ttu-id="56cc8-192">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="56cc8-192">RepositoryType</span></span> | <span data-ttu-id="56cc8-193">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-193">empty</span></span> | <span data-ttu-id="56cc8-194">リポジトリの種類。</span><span class="sxs-lookup"><span data-stu-id="56cc8-194">Repository type.</span></span> <span data-ttu-id="56cc8-195">例: *git*、 *tfs*。</span><span class="sxs-lookup"><span data-stu-id="56cc8-195">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="56cc8-196">Repository/Branch</span><span class="sxs-lookup"><span data-stu-id="56cc8-196">Repository/Branch</span></span> | <span data-ttu-id="56cc8-197">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="56cc8-197">RepositoryBranch</span></span> | <span data-ttu-id="56cc8-198">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-198">empty</span></span> | <span data-ttu-id="56cc8-199">リポジトリのブランチ情報 (オプション)。</span><span class="sxs-lookup"><span data-stu-id="56cc8-199">Optional repository branch information.</span></span> <span data-ttu-id="56cc8-200">このプロパティを含めるには、 *RepositoryUrl*も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-200">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="56cc8-201">例: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="56cc8-201">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="56cc8-202">Repository/Commit</span><span class="sxs-lookup"><span data-stu-id="56cc8-202">Repository/Commit</span></span> | <span data-ttu-id="56cc8-203">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="56cc8-203">RepositoryCommit</span></span> | <span data-ttu-id="56cc8-204">(なし)</span><span class="sxs-lookup"><span data-stu-id="56cc8-204">empty</span></span> | <span data-ttu-id="56cc8-205">任意のリポジトリのコミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-205">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="56cc8-206">このプロパティを含めるには、 *RepositoryUrl*も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="56cc8-207">例:*0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="56cc8-207">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="56cc8-208">PackageType</span><span class="sxs-lookup"><span data-stu-id="56cc8-208">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="56cc8-209">Summary</span><span class="sxs-lookup"><span data-stu-id="56cc8-209">Summary</span></span> | <span data-ttu-id="56cc8-210">サポートなし</span><span class="sxs-lookup"><span data-stu-id="56cc8-210">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="56cc8-211">pack ターゲットの入力</span><span class="sxs-lookup"><span data-stu-id="56cc8-211">pack target inputs</span></span>

- <span data-ttu-id="56cc8-212">IsPackable</span><span class="sxs-lookup"><span data-stu-id="56cc8-212">IsPackable</span></span>
- <span data-ttu-id="56cc8-213">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="56cc8-213">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="56cc8-214">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="56cc8-214">PackageVersion</span></span>
- <span data-ttu-id="56cc8-215">PackageId</span><span class="sxs-lookup"><span data-stu-id="56cc8-215">PackageId</span></span>
- <span data-ttu-id="56cc8-216">Authors</span><span class="sxs-lookup"><span data-stu-id="56cc8-216">Authors</span></span>
- <span data-ttu-id="56cc8-217">Description</span><span class="sxs-lookup"><span data-stu-id="56cc8-217">Description</span></span>
- <span data-ttu-id="56cc8-218">Copyright</span><span class="sxs-lookup"><span data-stu-id="56cc8-218">Copyright</span></span>
- <span data-ttu-id="56cc8-219">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="56cc8-219">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="56cc8-220">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="56cc8-220">DevelopmentDependency</span></span>
- <span data-ttu-id="56cc8-221">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="56cc8-221">PackageLicenseExpression</span></span>
- <span data-ttu-id="56cc8-222">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="56cc8-222">PackageLicenseFile</span></span>
- <span data-ttu-id="56cc8-223">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-223">PackageLicenseUrl</span></span>
- <span data-ttu-id="56cc8-224">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-224">PackageProjectUrl</span></span>
- <span data-ttu-id="56cc8-225">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-225">PackageIconUrl</span></span>
- <span data-ttu-id="56cc8-226">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="56cc8-226">PackageReleaseNotes</span></span>
- <span data-ttu-id="56cc8-227">PackageTags</span><span class="sxs-lookup"><span data-stu-id="56cc8-227">PackageTags</span></span>
- <span data-ttu-id="56cc8-228">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="56cc8-228">PackageOutputPath</span></span>
- <span data-ttu-id="56cc8-229">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="56cc8-229">IncludeSymbols</span></span>
- <span data-ttu-id="56cc8-230">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="56cc8-230">IncludeSource</span></span>
- <span data-ttu-id="56cc8-231">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="56cc8-231">PackageTypes</span></span>
- <span data-ttu-id="56cc8-232">IsTool</span><span class="sxs-lookup"><span data-stu-id="56cc8-232">IsTool</span></span>
- <span data-ttu-id="56cc8-233">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-233">RepositoryUrl</span></span>
- <span data-ttu-id="56cc8-234">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="56cc8-234">RepositoryType</span></span>
- <span data-ttu-id="56cc8-235">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="56cc8-235">RepositoryBranch</span></span>
- <span data-ttu-id="56cc8-236">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="56cc8-236">RepositoryCommit</span></span>
- <span data-ttu-id="56cc8-237">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="56cc8-237">NoPackageAnalysis</span></span>
- <span data-ttu-id="56cc8-238">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="56cc8-238">MinClientVersion</span></span>
- <span data-ttu-id="56cc8-239">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="56cc8-239">IncludeBuildOutput</span></span>
- <span data-ttu-id="56cc8-240">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="56cc8-240">IncludeContentInPack</span></span>
- <span data-ttu-id="56cc8-241">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="56cc8-241">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="56cc8-242">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="56cc8-242">ContentTargetFolders</span></span>
- <span data-ttu-id="56cc8-243">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="56cc8-243">NuspecFile</span></span>
- <span data-ttu-id="56cc8-244">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="56cc8-244">NuspecBasePath</span></span>
- <span data-ttu-id="56cc8-245">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="56cc8-245">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="56cc8-246">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="56cc8-246">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="56cc8-247">依存関係を表示しない</span><span class="sxs-lookup"><span data-stu-id="56cc8-247">Suppress dependencies</span></span>

<span data-ttu-id="56cc8-248">生成された NuGet パッケージからパッケージの依存`SuppressDependenciesWhenPacking`関係`true`を抑制するには、をに設定します。これにより、生成された nupkg ファイルからのすべての依存関係がスキップされます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-248">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="56cc8-249">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="56cc8-249">PackageIconUrl</span></span>

<span data-ttu-id="56cc8-250">[NuGet の問題 352](https://github.com/NuGet/Home/issues/352)の変更の一環とし`PackageIconUrl`て、は最終的に`PackageIconUri`に変更され、結果のパッケージのルートに含まれるアイコンファイルへの相対パスにすることができます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-250">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="56cc8-251">出力アセンブリ</span><span class="sxs-lookup"><span data-stu-id="56cc8-251">Output assemblies</span></span>

<span data-ttu-id="56cc8-252">`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="56cc8-252">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="56cc8-253">コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-253">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="56cc8-254">出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-254">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="56cc8-255">`IncludeBuildOutput`:ビルド出力アセンブリをパッケージに含める必要があるかどうかを決定するブール値。</span><span class="sxs-lookup"><span data-stu-id="56cc8-255">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="56cc8-256">`BuildOutputTargetFolder`:出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-256">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="56cc8-257">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-257">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="56cc8-258">パッケージ参照</span><span class="sxs-lookup"><span data-stu-id="56cc8-258">Package references</span></span>

<span data-ttu-id="56cc8-259">「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="56cc8-259">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="56cc8-260">プロジェクト間参照</span><span class="sxs-lookup"><span data-stu-id="56cc8-260">Project to project references</span></span>

<span data-ttu-id="56cc8-261">プロジェクト間参照は、既定で NuGet パッケージ参照として見なされています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-261">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="56cc8-262">また、次のメタデータをプロジェクト参照に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-262">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="56cc8-263">パッケージにコンテンツを含める</span><span class="sxs-lookup"><span data-stu-id="56cc8-263">Including content in a package</span></span>

<span data-ttu-id="56cc8-264">コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-264">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="56cc8-265">次のようなエントリでオーバーライドしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-265">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="56cc8-266">次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-266">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="56cc8-267">(`content` および `contentFiles` フォルダーの両方ではなく) すべてのコンテンツを特定のルート フォルダーにのみコピーする場合、MSBuild プロパティの `ContentTargetFolders` を使用できます。このプロパティの既定値は "content;contentFiles" ですが、他の任意のフォルダー名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-267">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="56cc8-268">`ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-268">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="56cc8-269">`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-269">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="56cc8-270">空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-270">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="56cc8-271">たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-271">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="56cc8-272">また、MSBuild プロパティの `$(IncludeContentInPack)` もあります。既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="56cc8-272">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="56cc8-273">これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="56cc8-273">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="56cc8-274">上記の任意の項目に設定できる他の pack 固有のメタデータとして、NuSpec の ```contentFiles``` エントリに ```CopyToOutput``` 値と ```Flatten``` 値を設定する ```<PackageCopyToOutput>``` と ```<PackageFlatten>``` があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-274">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="56cc8-275">コンテンツ項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-275">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="56cc8-276">glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-276">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="56cc8-277">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="56cc8-277">IncludeSymbols</span></span>

<span data-ttu-id="56cc8-278">`MSBuild -t:pack -p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-278">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="56cc8-279">`IncludeSymbols=true` を設定すると、通常のパッケージ*と*シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-279">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="56cc8-280">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="56cc8-280">IncludeSource</span></span>

<span data-ttu-id="56cc8-281">これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。</span><span class="sxs-lookup"><span data-stu-id="56cc8-281">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="56cc8-282">種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-282">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="56cc8-283">`TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-283">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="56cc8-284">種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-284">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="56cc8-285">ライセンス式またはライセンスファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="56cc8-285">Packing a license expression or a license file</span></span>

<span data-ttu-id="56cc8-286">ライセンス式を使用する場合は、"パッケージの表示" プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-286">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="56cc8-287">[ライセンス式のサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="56cc8-287">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="56cc8-288">[NuGet.org によって受け付けられるライセンス式とライセンスの詳細については、こちらを参照](nuspec.md#license)してください。</span><span class="sxs-lookup"><span data-stu-id="56cc8-288">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="56cc8-289">ライセンスファイルをパッキングする場合は、パッケージのルートを基準としたパッケージパスを指定するために、"パッケージの作成" プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-289">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="56cc8-290">また、ファイルがパッケージに含まれていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-290">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="56cc8-291">例えば:</span><span class="sxs-lookup"><span data-stu-id="56cc8-291">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="56cc8-292">[ライセンスファイルのサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="56cc8-292">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="56cc8-293">IsTool</span><span class="sxs-lookup"><span data-stu-id="56cc8-293">IsTool</span></span>

<span data-ttu-id="56cc8-294">`MSBuild -t:pack -p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-294">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="56cc8-295">これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-295">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="56cc8-296">.nuspec を使用したパック</span><span class="sxs-lookup"><span data-stu-id="56cc8-296">Packing using a .nuspec</span></span>

<span data-ttu-id="56cc8-297">通常は`.nuspec`ファイル内の[すべてのプロパティ](../reference/msbuild-targets.md#pack-target)をプロジェクトファイルに含めることをお勧めしますが、プロジェクトをパックするためにファイルを`.nuspec`使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-297">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="56cc8-298">を使用`PackageReference`する SDK スタイル以外のプロジェクトでは、をインポート`NuGet.Build.Tasks.Pack.targets`して、パックタスクを実行できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-298">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="56cc8-299">Nuspec ファイルをパックする前に、プロジェクトを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-299">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="56cc8-300">(SDK スタイルのプロジェクトには、既定でパックターゲットが含まれています)。</span><span class="sxs-lookup"><span data-stu-id="56cc8-300">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="56cc8-301">Nuspec をパッキングする場合、プロジェクトファイルのターゲットフレームワークは無関係であり、使用されません。</span><span class="sxs-lookup"><span data-stu-id="56cc8-301">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="56cc8-302">次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-302">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="56cc8-303">`NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="56cc8-303">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="56cc8-304">`NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="56cc8-304">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="56cc8-305">MSBuild コマンドラインの解析方法に従い、複数のプロパティは `-p:NuspecProperties=\"key1=value1;key2=value2\"` のように指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-305">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="56cc8-306">`NuspecBasePath`:`.nuspec`ファイルのベースパス。</span><span class="sxs-lookup"><span data-stu-id="56cc8-306">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="56cc8-307">`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-307">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="56cc8-308">MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-308">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="56cc8-309">Dotnet または msbuild を使用して nuspec をパッキングすると、既定でプロジェクトのビルドも実行されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="56cc8-309">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="56cc8-310">これを回避するには```--no-build``` 、プロパティを dotnet に渡します。これは、プロジェクト```<NoBuild>true</NoBuild> ```ファイルの設定と共に、プロジェクト```<IncludeBuildOutput>false</IncludeBuildOutput> ```ファイル内の設定に相当します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-310">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="56cc8-311">Nuspec ファイルをパックする .csproj ファイルの例を次に示し*ます。*</span><span class="sxs-lookup"><span data-stu-id="56cc8-311">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="56cc8-312">カスタマイズしたパッケージを作成するための高度な拡張機能ポイント</span><span class="sxs-lookup"><span data-stu-id="56cc8-312">Advanced extension points to create customized package</span></span>

<span data-ttu-id="56cc8-313">`pack`ターゲットには、ターゲットフレームワーク固有の内部ビルドで実行される2つの拡張ポイントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="56cc8-313">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="56cc8-314">拡張ポイントは、ターゲットフレームワーク固有のコンテンツとアセンブリをパッケージに含めることをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="56cc8-314">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="56cc8-315">`TargetsForTfmSpecificBuildOutput`接続`lib`フォルダー内のファイル、またはを使用して`BuildOutputTargetFolder`指定したフォルダー内のファイルに対して使用します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-315">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="56cc8-316">`TargetsForTfmSpecificContentInPackage`接続の`BuildOutputTargetFolder`外部のファイルに対して使用します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-316">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="56cc8-317">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="56cc8-317">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="56cc8-318">カスタムターゲットを作成し、 `$(TargetsForTfmSpecificBuildOutput)`プロパティの値として指定します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="56cc8-319">(既定では`BuildOutputTargetFolder` lib) に移動する必要があるファイルの場合、ターゲットはこれらのファイルを ItemGroup `BuildOutputInPackage`に書き込み、次の2つのメタデータ値を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-319">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="56cc8-320">`FinalOutputPath`:ファイルの絶対パス。指定されていない場合は、ソースパスの評価に Id が使用されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-320">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="56cc8-321">`TargetPath`:Optionalファイルが内`lib\<TargetFramework>`のサブフォルダーに入る必要があるときに、それぞれのカルチャフォルダーの下にあるサテライトアセンブリのように設定します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-321">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="56cc8-322">既定値は、ファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="56cc8-322">Defaults to the name of the file.</span></span>

<span data-ttu-id="56cc8-323">例:</span><span class="sxs-lookup"><span data-stu-id="56cc8-323">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="56cc8-324">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="56cc8-324">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="56cc8-325">カスタムターゲットを作成し、 `$(TargetsForTfmSpecificContentInPackage)`プロパティの値として指定します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-325">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="56cc8-326">パッケージに含めるファイルについては、ターゲットはこれらのファイルを ItemGroup `TfmSpecificPackageFile`に書き込み、次のオプションのメタデータを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-326">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="56cc8-327">`PackagePath`:パッケージ内でファイルが出力されるパス。</span><span class="sxs-lookup"><span data-stu-id="56cc8-327">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="56cc8-328">複数のファイルが同じパッケージパスに追加されると、NuGet は警告を発行します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-328">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="56cc8-329">`BuildAction`:ファイルに割り当てるビルドアクション。パッケージパスが`contentFiles`フォルダー内にある場合にのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="56cc8-329">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="56cc8-330">既定値は "None" です。</span><span class="sxs-lookup"><span data-stu-id="56cc8-330">Defaults to "None".</span></span>

<span data-ttu-id="56cc8-331">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-331">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="56cc8-332">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="56cc8-332">restore target</span></span>

<span data-ttu-id="56cc8-333">`MSBuild -t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-333">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="56cc8-334">すべてのプロジェクト間参照を読み取ります</span><span class="sxs-lookup"><span data-stu-id="56cc8-334">Read all project to project references</span></span>
1. <span data-ttu-id="56cc8-335">プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します</span><span class="sxs-lookup"><span data-stu-id="56cc8-335">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="56cc8-336">MSBuild データを NuGet に渡します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-336">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="56cc8-337">restore を実行します</span><span class="sxs-lookup"><span data-stu-id="56cc8-337">Run restore</span></span>
1. <span data-ttu-id="56cc8-338">パッケージをダウンロードします</span><span class="sxs-lookup"><span data-stu-id="56cc8-338">Download packages</span></span>
1. <span data-ttu-id="56cc8-339">アセット ファイル、ターゲット、およびプロパティを出力します</span><span class="sxs-lookup"><span data-stu-id="56cc8-339">Write assets file, targets, and props</span></span>

<span data-ttu-id="56cc8-340">ターゲット`restore`は、PackageReference 形式を使用するプロジェクトに対して**のみ**機能します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-340">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="56cc8-341">`packages.config`形式を使用するプロジェクトでは機能し**ません**。代わりに[nuget restore](../reference/cli-reference/cli-ref-restore.md)を使用してください。</span><span class="sxs-lookup"><span data-stu-id="56cc8-341">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="56cc8-342">restore のプロパティ</span><span class="sxs-lookup"><span data-stu-id="56cc8-342">Restore properties</span></span>

<span data-ttu-id="56cc8-343">追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-343">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="56cc8-344">また、`-p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="56cc8-344">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="56cc8-345">プロパティ</span><span class="sxs-lookup"><span data-stu-id="56cc8-345">Property</span></span> | <span data-ttu-id="56cc8-346">Description</span><span class="sxs-lookup"><span data-stu-id="56cc8-346">Description</span></span> |
|--------|--------|
| <span data-ttu-id="56cc8-347">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="56cc8-347">RestoreSources</span></span> | <span data-ttu-id="56cc8-348">パッケージ ソースのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="56cc8-348">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="56cc8-349">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="56cc8-349">RestorePackagesPath</span></span> | <span data-ttu-id="56cc8-350">ユーザー パッケージ フォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="56cc8-350">User packages folder path.</span></span> |
| <span data-ttu-id="56cc8-351">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="56cc8-351">RestoreDisableParallel</span></span> | <span data-ttu-id="56cc8-352">ダウンロード数を一度に 1 つまでに制限します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-352">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="56cc8-353">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="56cc8-353">RestoreConfigFile</span></span> | <span data-ttu-id="56cc8-354">適用する `Nuget.Config` ファイルのパス。</span><span class="sxs-lookup"><span data-stu-id="56cc8-354">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="56cc8-355">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="56cc8-355">RestoreNoCache</span></span> | <span data-ttu-id="56cc8-356">True の場合、キャッシュされたパッケージの使用を回避します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-356">If true, avoids using cached packages.</span></span> <span data-ttu-id="56cc8-357">「[グローバルパッケージとキャッシュフォルダーの管理」を](../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="56cc8-357">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="56cc8-358">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="56cc8-358">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="56cc8-359">true の場合、失敗した、または不足しているパッケージ ソースを無視します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-359">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="56cc8-360">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="56cc8-360">RestoreFallbackFolders</span></span> | <span data-ttu-id="56cc8-361">フォールバックフォルダー。ユーザーパッケージフォルダーを使用する場合と同じ方法で使用されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-361">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="56cc8-362">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="56cc8-362">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="56cc8-363">復元中に使用する追加のソース。</span><span class="sxs-lookup"><span data-stu-id="56cc8-363">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="56cc8-364">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="56cc8-364">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="56cc8-365">復元中に使用する追加のフォールバックフォルダー。</span><span class="sxs-lookup"><span data-stu-id="56cc8-365">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="56cc8-366">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="56cc8-366">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="56cc8-367">で指定されたフォールバックフォルダーを除外します。`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="56cc8-367">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="56cc8-368">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="56cc8-368">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="56cc8-369">`NuGet.Build.Tasks.dll` のパス。</span><span class="sxs-lookup"><span data-stu-id="56cc8-369">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="56cc8-370">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="56cc8-370">RestoreGraphProjectInput</span></span> | <span data-ttu-id="56cc8-371">復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-371">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="56cc8-372">Restoreentkipnon存在 Enttargets</span><span class="sxs-lookup"><span data-stu-id="56cc8-372">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="56cc8-373">MSBuild を使用してプロジェクトが収集されると、 `SkipNonexistentTargets`最適化を使用してプロジェクトを収集するかどうかが決定されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-373">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="56cc8-374">設定しない場合、の`true`既定値はになります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-374">When not set, defaults to `true`.</span></span> <span data-ttu-id="56cc8-375">その結果、プロジェクトのターゲットをインポートできない場合のフェールファースト動作になります。</span><span class="sxs-lookup"><span data-stu-id="56cc8-375">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="56cc8-376">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="56cc8-376">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="56cc8-377">出力フォルダー。を既定`BaseIntermediateOutputPath` `obj`として、フォルダーをにします。</span><span class="sxs-lookup"><span data-stu-id="56cc8-377">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="56cc8-378">使用例</span><span class="sxs-lookup"><span data-stu-id="56cc8-378">Examples</span></span>

<span data-ttu-id="56cc8-379">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="56cc8-379">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="56cc8-380">プロジェクト ファイル:</span><span class="sxs-lookup"><span data-stu-id="56cc8-380">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="56cc8-381">restore の出力</span><span class="sxs-lookup"><span data-stu-id="56cc8-381">Restore outputs</span></span>

<span data-ttu-id="56cc8-382">restore で、次のファイルがビルドの `obj` フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-382">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="56cc8-383">ファイル</span><span class="sxs-lookup"><span data-stu-id="56cc8-383">File</span></span> | <span data-ttu-id="56cc8-384">Description</span><span class="sxs-lookup"><span data-stu-id="56cc8-384">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="56cc8-385">すべてのパッケージ参照の依存関係グラフを含みます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-385">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="56cc8-386">パッケージに含まれる MSBuild プロパティへの参照</span><span class="sxs-lookup"><span data-stu-id="56cc8-386">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="56cc8-387">パッケージに含まれる MSBuild ターゲットへの参照</span><span class="sxs-lookup"><span data-stu-id="56cc8-387">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="56cc8-388">1つの MSBuild コマンドを使用した復元とビルド</span><span class="sxs-lookup"><span data-stu-id="56cc8-388">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="56cc8-389">NuGet では、MSBuild のターゲットとプロパティを表示するパッケージを復元できるため、異なるグローバルプロパティを使用して復元とビルドの評価が実行されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-389">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="56cc8-390">これは、次のような場合に予期しない動作が発生する可能性があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-390">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="56cc8-391">代わりに、推奨される方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="56cc8-391">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="56cc8-392">と同様に`build`、同じロジックが他のターゲットにも適用されます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-392">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="56cc8-393">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="56cc8-393">PackageTargetFallback</span></span>

<span data-ttu-id="56cc8-394">`PackageTargetFallback` 要素では、パッケージの復元時に使用する、互換性のある一連のターゲットを指定できます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-394">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="56cc8-395">dotnet [TxM](../reference/target-frameworks.md) を使用するパッケージが、dotnet TxM を宣言していない互換性のあるパッケージと連携できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="56cc8-395">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="56cc8-396">つまり、プロジェクトで dotnet TxM を使用せず、依存するすべてのパッケージに dotnet TxM を与える必要がある場合、非 dotnet プラットフォームを dotnet 対応にするためにプロジェクトに `<PackageTargetFallback>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-396">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="56cc8-397">たとえば、プロジェクトが `netstandard1.6` TxM を使用し、依存しているパッケージに `lib/net45/a.dll` と `lib/portable-net45+win81/a.dll` のみが含まれている場合、そのプロジェクトはビルドできません。</span><span class="sxs-lookup"><span data-stu-id="56cc8-397">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="56cc8-398">後者の DLL を構築する予定の場合は、`portable-net45+win81` DLL に互換性を持たせるために、次のように `PackageTargetFallback` を追加します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-398">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="56cc8-399">プロジェクト内のすべてのターゲットについてフォールバックを宣言するには、`Condition` 属性を省略します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-399">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="56cc8-400">また、次のように `$(PackageTargetFallback)` を含めて、既存の `PackageTargetFallback` を拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-400">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="56cc8-401">復元グラフの 1 つのライブラリを置き換える</span><span class="sxs-lookup"><span data-stu-id="56cc8-401">Replacing one library from a restore graph</span></span>

<span data-ttu-id="56cc8-402">復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="56cc8-402">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="56cc8-403">まず、最上位の `PackageReference` ですべてのアセットを除外します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-403">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="56cc8-404">次に、DLL の適切なローカル コピーに独自の参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="56cc8-404">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
