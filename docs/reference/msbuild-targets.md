---
title: MSBuild ターゲットとしての NuGet の pack と restore
description: NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: a9427d87f69a2e942a9802fbdae5193eead1c724
ms.sourcegitcommit: af58d59669674c3bc0a230d5764e37020a9a3f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2018
ms.locfileid: "52831021"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="6ba32-103">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="6ba32-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="6ba32-104">*NuGet 4.0 以降*</span><span class="sxs-lookup"><span data-stu-id="6ba32-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="6ba32-105">NuGet 4.0 以降では、PackageReference 形式を使用することにより、すべてのマニフェスト メタデータを、個別の `.nuspec` ファイルを使用せずにプロジェクト ファイルに直接保存できます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="6ba32-106">MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。</span><span class="sxs-lookup"><span data-stu-id="6ba32-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="6ba32-107">これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます </span><span class="sxs-lookup"><span data-stu-id="6ba32-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="6ba32-108">(NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../tools/cli-ref-pack.md) および [restore](../tools/cli-ref-restore.md) コマンドを使用します)。</span><span class="sxs-lookup"><span data-stu-id="6ba32-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="6ba32-109">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="6ba32-109">Target build order</span></span>

<span data-ttu-id="6ba32-110">`pack` と `restore` は MSBuild のターゲットなので、アクセスするとワークフローを強化できます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="6ba32-111">たとえば、パック後にパッケージをネットワーク共有にコピーするとします。</span><span class="sxs-lookup"><span data-stu-id="6ba32-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="6ba32-112">この場合、プロジェクト ファイルに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="6ba32-113">同様に、MSBuild タスクを記述し、独自のターゲットを記述して、MSBuild タスクで NuGet プロパティを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="6ba32-114">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="6ba32-114">pack target</span></span>

<span data-ttu-id="6ba32-115">PackageReference 形式を使用して、使用して .NET Standard プロジェクトの`msbuild -t:pack`NuGet パッケージの作成に使用するプロジェクト ファイルからの入力を描画します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="6ba32-116">以下の表では、最初の `<PropertyGroup>` ノード内のプロジェクト ファイルに追加できる MSBuild のプロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="6ba32-117">Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="6ba32-118">便宜上、この表は、[`.nuspec` ファイル](../reference/nuspec.md)の同等のプロパティごとに整理されています。</span><span class="sxs-lookup"><span data-stu-id="6ba32-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="6ba32-119">`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="6ba32-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="6ba32-120">属性/NuSpec の値</span><span class="sxs-lookup"><span data-stu-id="6ba32-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="6ba32-121">MSBuild のプロパティ</span><span class="sxs-lookup"><span data-stu-id="6ba32-121">MSBuild Property</span></span> | <span data-ttu-id="6ba32-122">既定値</span><span class="sxs-lookup"><span data-stu-id="6ba32-122">Default</span></span> | <span data-ttu-id="6ba32-123">メモ</span><span class="sxs-lookup"><span data-stu-id="6ba32-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="6ba32-124">ID</span><span class="sxs-lookup"><span data-stu-id="6ba32-124">Id</span></span> | <span data-ttu-id="6ba32-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="6ba32-125">PackageId</span></span> | <span data-ttu-id="6ba32-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="6ba32-126">AssemblyName</span></span> | <span data-ttu-id="6ba32-127">MSBuild の $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="6ba32-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="6ba32-128">Version</span><span class="sxs-lookup"><span data-stu-id="6ba32-128">Version</span></span> | <span data-ttu-id="6ba32-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="6ba32-129">PackageVersion</span></span> | <span data-ttu-id="6ba32-130">Version</span><span class="sxs-lookup"><span data-stu-id="6ba32-130">Version</span></span> | <span data-ttu-id="6ba32-131">これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345")</span><span class="sxs-lookup"><span data-stu-id="6ba32-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="6ba32-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="6ba32-132">VersionPrefix</span></span> | <span data-ttu-id="6ba32-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="6ba32-133">PackageVersionPrefix</span></span> | <span data-ttu-id="6ba32-134">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-134">empty</span></span> | <span data-ttu-id="6ba32-135">PackageVersion を設定すると、PackageVersionPrefix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="6ba32-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="6ba32-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="6ba32-136">VersionSuffix</span></span> | <span data-ttu-id="6ba32-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="6ba32-137">PackageVersionSuffix</span></span> | <span data-ttu-id="6ba32-138">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-138">empty</span></span> | <span data-ttu-id="6ba32-139">MSBuild の $(VersionSuffix)</span><span class="sxs-lookup"><span data-stu-id="6ba32-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="6ba32-140">PackageVersion を設定すると、PackageVersionSuffix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="6ba32-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="6ba32-141">Authors</span><span class="sxs-lookup"><span data-stu-id="6ba32-141">Authors</span></span> | <span data-ttu-id="6ba32-142">Authors</span><span class="sxs-lookup"><span data-stu-id="6ba32-142">Authors</span></span> | <span data-ttu-id="6ba32-143">現在のユーザーのユーザー名</span><span class="sxs-lookup"><span data-stu-id="6ba32-143">Username of the current user</span></span> | |
| <span data-ttu-id="6ba32-144">所有者</span><span class="sxs-lookup"><span data-stu-id="6ba32-144">Owners</span></span> | <span data-ttu-id="6ba32-145">N/A</span><span class="sxs-lookup"><span data-stu-id="6ba32-145">N/A</span></span> | <span data-ttu-id="6ba32-146">NuSpec にはありません</span><span class="sxs-lookup"><span data-stu-id="6ba32-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="6ba32-147">Title</span><span class="sxs-lookup"><span data-stu-id="6ba32-147">Title</span></span> | <span data-ttu-id="6ba32-148">Title</span><span class="sxs-lookup"><span data-stu-id="6ba32-148">Title</span></span> | <span data-ttu-id="6ba32-149">PackageId</span><span class="sxs-lookup"><span data-stu-id="6ba32-149">The PackageId</span></span>| |
| <span data-ttu-id="6ba32-150">説明</span><span class="sxs-lookup"><span data-stu-id="6ba32-150">Description</span></span> | <span data-ttu-id="6ba32-151">説明</span><span class="sxs-lookup"><span data-stu-id="6ba32-151">Description</span></span> | <span data-ttu-id="6ba32-152">"パッケージの説明"</span><span class="sxs-lookup"><span data-stu-id="6ba32-152">"Package Description"</span></span> | |
| <span data-ttu-id="6ba32-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="6ba32-153">Copyright</span></span> | <span data-ttu-id="6ba32-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="6ba32-154">Copyright</span></span> | <span data-ttu-id="6ba32-155">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-155">empty</span></span> | |
| <span data-ttu-id="6ba32-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="6ba32-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="6ba32-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="6ba32-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="6ba32-158">False</span><span class="sxs-lookup"><span data-stu-id="6ba32-158">false</span></span> | |
| <span data-ttu-id="6ba32-159">ライセンス</span><span class="sxs-lookup"><span data-stu-id="6ba32-159">license</span></span> | <span data-ttu-id="6ba32-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="6ba32-160">PackageLicenseExpression</span></span> | <span data-ttu-id="6ba32-161">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-161">empty</span></span> | <span data-ttu-id="6ba32-162">対応しています `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="6ba32-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="6ba32-163">ライセンス</span><span class="sxs-lookup"><span data-stu-id="6ba32-163">license</span></span> | <span data-ttu-id="6ba32-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="6ba32-164">PackageLicenseFile</span></span> | <span data-ttu-id="6ba32-165">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-165">empty</span></span> | <span data-ttu-id="6ba32-166">`<license type="file">` に相当します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="6ba32-167">明示的に参照先のライセンス ファイルをパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="6ba32-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-168">LicenseUrl</span></span> | <span data-ttu-id="6ba32-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-169">PackageLicenseUrl</span></span> | <span data-ttu-id="6ba32-170">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-170">empty</span></span> | <span data-ttu-id="6ba32-171">`licenseUrl` PackageLicenseExpression または PackageLicenseFile プロパティを使用して、非推奨とされています。</span><span class="sxs-lookup"><span data-stu-id="6ba32-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="6ba32-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-172">ProjectUrl</span></span> | <span data-ttu-id="6ba32-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-173">PackageProjectUrl</span></span> | <span data-ttu-id="6ba32-174">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-174">empty</span></span> | |
| <span data-ttu-id="6ba32-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-175">IconUrl</span></span> | <span data-ttu-id="6ba32-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-176">PackageIconUrl</span></span> | <span data-ttu-id="6ba32-177">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-177">empty</span></span> | |
| <span data-ttu-id="6ba32-178">Tags</span><span class="sxs-lookup"><span data-stu-id="6ba32-178">Tags</span></span> | <span data-ttu-id="6ba32-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="6ba32-179">PackageTags</span></span> | <span data-ttu-id="6ba32-180">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-180">empty</span></span> | <span data-ttu-id="6ba32-181">複数のタグはセミコロン (;) で区切られます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="6ba32-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="6ba32-182">ReleaseNotes</span></span> | <span data-ttu-id="6ba32-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="6ba32-183">PackageReleaseNotes</span></span> | <span data-ttu-id="6ba32-184">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-184">empty</span></span> | |
| <span data-ttu-id="6ba32-185">リポジトリの Url/</span><span class="sxs-lookup"><span data-stu-id="6ba32-185">Repository/Url</span></span> | <span data-ttu-id="6ba32-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-186">RepositoryUrl</span></span> | <span data-ttu-id="6ba32-187">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-187">empty</span></span> | <span data-ttu-id="6ba32-188">リポジトリの URL を複製するか、ソース コードを取得するために使用します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="6ba32-189">例: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="6ba32-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="6ba32-190">リポジトリの種類/</span><span class="sxs-lookup"><span data-stu-id="6ba32-190">Repository/Type</span></span> | <span data-ttu-id="6ba32-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="6ba32-191">RepositoryType</span></span> | <span data-ttu-id="6ba32-192">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-192">empty</span></span> | <span data-ttu-id="6ba32-193">リポジトリの種類。</span><span class="sxs-lookup"><span data-stu-id="6ba32-193">Repository type.</span></span> <span data-ttu-id="6ba32-194">例: *git*、 *tfs*します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="6ba32-195">リポジトリとブランチ</span><span class="sxs-lookup"><span data-stu-id="6ba32-195">Repository/Branch</span></span> | <span data-ttu-id="6ba32-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="6ba32-196">RepositoryBranch</span></span> | <span data-ttu-id="6ba32-197">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-197">empty</span></span> | <span data-ttu-id="6ba32-198">省略可能なリポジトリのブランチの情報。</span><span class="sxs-lookup"><span data-stu-id="6ba32-198">Optional repository branch information.</span></span> <span data-ttu-id="6ba32-199">*RepositoryUrl*にインクルードするには、このプロパティも指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="6ba32-200">例:*マスター* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="6ba32-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="6ba32-201">コミットあたりのリポジトリ</span><span class="sxs-lookup"><span data-stu-id="6ba32-201">Repository/Commit</span></span> | <span data-ttu-id="6ba32-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="6ba32-202">RepositoryCommit</span></span> | <span data-ttu-id="6ba32-203">(なし)</span><span class="sxs-lookup"><span data-stu-id="6ba32-203">empty</span></span> | <span data-ttu-id="6ba32-204">省略可能なリポジトリのコミットまたは変更セットをパッケージ ソースを示すためには、に対して構築されました。</span><span class="sxs-lookup"><span data-stu-id="6ba32-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="6ba32-205">*RepositoryUrl*にインクルードするには、このプロパティも指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="6ba32-206">例: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="6ba32-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="6ba32-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="6ba32-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="6ba32-208">まとめ</span><span class="sxs-lookup"><span data-stu-id="6ba32-208">Summary</span></span> | <span data-ttu-id="6ba32-209">サポートなし</span><span class="sxs-lookup"><span data-stu-id="6ba32-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="6ba32-210">pack ターゲットの入力</span><span class="sxs-lookup"><span data-stu-id="6ba32-210">pack target inputs</span></span>

- <span data-ttu-id="6ba32-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="6ba32-211">IsPackable</span></span>
- <span data-ttu-id="6ba32-212">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="6ba32-212">PackageVersion</span></span>
- <span data-ttu-id="6ba32-213">PackageId</span><span class="sxs-lookup"><span data-stu-id="6ba32-213">PackageId</span></span>
- <span data-ttu-id="6ba32-214">Authors</span><span class="sxs-lookup"><span data-stu-id="6ba32-214">Authors</span></span>
- <span data-ttu-id="6ba32-215">説明</span><span class="sxs-lookup"><span data-stu-id="6ba32-215">Description</span></span>
- <span data-ttu-id="6ba32-216">Copyright</span><span class="sxs-lookup"><span data-stu-id="6ba32-216">Copyright</span></span>
- <span data-ttu-id="6ba32-217">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="6ba32-217">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="6ba32-218">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="6ba32-218">DevelopmentDependency</span></span>
- <span data-ttu-id="6ba32-219">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="6ba32-219">PackageLicenseExpression</span></span>
- <span data-ttu-id="6ba32-220">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="6ba32-220">PackageLicenseFile</span></span>
- <span data-ttu-id="6ba32-221">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-221">PackageLicenseUrl</span></span>
- <span data-ttu-id="6ba32-222">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-222">PackageProjectUrl</span></span>
- <span data-ttu-id="6ba32-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-223">PackageIconUrl</span></span>
- <span data-ttu-id="6ba32-224">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="6ba32-224">PackageReleaseNotes</span></span>
- <span data-ttu-id="6ba32-225">PackageTags</span><span class="sxs-lookup"><span data-stu-id="6ba32-225">PackageTags</span></span>
- <span data-ttu-id="6ba32-226">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="6ba32-226">PackageOutputPath</span></span>
- <span data-ttu-id="6ba32-227">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="6ba32-227">IncludeSymbols</span></span>
- <span data-ttu-id="6ba32-228">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="6ba32-228">IncludeSource</span></span>
- <span data-ttu-id="6ba32-229">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="6ba32-229">PackageTypes</span></span>
- <span data-ttu-id="6ba32-230">IsTool</span><span class="sxs-lookup"><span data-stu-id="6ba32-230">IsTool</span></span>
- <span data-ttu-id="6ba32-231">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-231">RepositoryUrl</span></span>
- <span data-ttu-id="6ba32-232">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="6ba32-232">RepositoryType</span></span>
- <span data-ttu-id="6ba32-233">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="6ba32-233">RepositoryBranch</span></span>
- <span data-ttu-id="6ba32-234">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="6ba32-234">RepositoryCommit</span></span>
- <span data-ttu-id="6ba32-235">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="6ba32-235">NoPackageAnalysis</span></span>
- <span data-ttu-id="6ba32-236">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="6ba32-236">MinClientVersion</span></span>
- <span data-ttu-id="6ba32-237">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="6ba32-237">IncludeBuildOutput</span></span>
- <span data-ttu-id="6ba32-238">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="6ba32-238">IncludeContentInPack</span></span>
- <span data-ttu-id="6ba32-239">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="6ba32-239">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="6ba32-240">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="6ba32-240">ContentTargetFolders</span></span>
- <span data-ttu-id="6ba32-241">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="6ba32-241">NuspecFile</span></span>
- <span data-ttu-id="6ba32-242">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="6ba32-242">NuspecBasePath</span></span>
- <span data-ttu-id="6ba32-243">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="6ba32-243">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="6ba32-244">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="6ba32-244">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="6ba32-245">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="6ba32-245">PackageIconUrl</span></span>

<span data-ttu-id="6ba32-246">変更の一環として[NuGet 問題 352](https://github.com/NuGet/Home/issues/352)、`PackageIconUrl`に最終的に変更されます`PackageIconUri`結果のパッケージのルートに含まれるアイコン ファイルへの相対パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-246">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="6ba32-247">出力アセンブリ</span><span class="sxs-lookup"><span data-stu-id="6ba32-247">Output assemblies</span></span>

<span data-ttu-id="6ba32-248">`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="6ba32-248">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="6ba32-249">コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-249">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="6ba32-250">出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-250">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="6ba32-251">`IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。</span><span class="sxs-lookup"><span data-stu-id="6ba32-251">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="6ba32-252">`BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-252">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="6ba32-253">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-253">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="6ba32-254">パッケージ参照</span><span class="sxs-lookup"><span data-stu-id="6ba32-254">Package references</span></span>

<span data-ttu-id="6ba32-255">「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6ba32-255">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="6ba32-256">プロジェクト間参照</span><span class="sxs-lookup"><span data-stu-id="6ba32-256">Project to project references</span></span>

<span data-ttu-id="6ba32-257">プロジェクト間参照は、既定で NuGet パッケージ参照として見なされています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-257">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="6ba32-258">また、次のメタデータをプロジェクト参照に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-258">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="6ba32-259">パッケージにコンテンツを含める</span><span class="sxs-lookup"><span data-stu-id="6ba32-259">Including content in a package</span></span>

<span data-ttu-id="6ba32-260">コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-260">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="6ba32-261">次のようなエントリでオーバーライドしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-261">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="6ba32-262">次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-262">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="6ba32-263">(`content` および `contentFiles` フォルダーの両方ではなく) すべてのコンテンツを特定のルート フォルダーにのみコピーする場合、MSBuild プロパティの `ContentTargetFolders` を使用できます。このプロパティの既定値は "content;contentFiles" ですが、他の任意のフォルダー名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-263">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="6ba32-264">`ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-264">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="6ba32-265">`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-265">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="6ba32-266">空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-266">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="6ba32-267">たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-267">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="6ba32-268">また、MSBuild プロパティの `$(IncludeContentInPack)` もあります。既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="6ba32-268">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="6ba32-269">これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="6ba32-269">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="6ba32-270">上記の任意の項目に設定できる他の pack 固有のメタデータとして、NuSpec の ```contentFiles``` エントリに ```CopyToOutput``` 値と ```Flatten``` 値を設定する ```<PackageCopyToOutput>``` と ```<PackageFlatten>``` があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-270">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="6ba32-271">コンテンツ項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-271">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="6ba32-272">glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-272">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="6ba32-273">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="6ba32-273">IncludeSymbols</span></span>

<span data-ttu-id="6ba32-274">`MSBuild -t:pack -p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-274">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="6ba32-275">`IncludeSymbols=true` を設定すると、通常のパッケージ*と*シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-275">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="6ba32-276">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="6ba32-276">IncludeSource</span></span>

<span data-ttu-id="6ba32-277">これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。</span><span class="sxs-lookup"><span data-stu-id="6ba32-277">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="6ba32-278">種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-278">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="6ba32-279">`TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-279">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="6ba32-280">種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-280">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="6ba32-281">梱包ライセンス式またはライセンス ファイル</span><span class="sxs-lookup"><span data-stu-id="6ba32-281">Packing a license expression or a license file</span></span>

<span data-ttu-id="6ba32-282">ライセンスの式を使用する場合は、PackageLicenseExpression プロパティを使用してください。</span><span class="sxs-lookup"><span data-stu-id="6ba32-282">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="6ba32-283">[ライセンスの式のサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-283">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

<span data-ttu-id="6ba32-284">ライセンス ファイルをパックするときに、PackageLicenseFile プロパティを使用して、パッケージのルートを基準とした、パッケージのパスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-284">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="6ba32-285">さらに、ファイルをパッケージに含まれるかどうかを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-285">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="6ba32-286">例:</span><span class="sxs-lookup"><span data-stu-id="6ba32-286">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```
<span data-ttu-id="6ba32-287">[ライセンス ファイルのサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-287">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="6ba32-288">IsTool</span><span class="sxs-lookup"><span data-stu-id="6ba32-288">IsTool</span></span>

<span data-ttu-id="6ba32-289">`MSBuild -t:pack -p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-289">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="6ba32-290">これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-290">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="6ba32-291">.nuspec を使用したパック</span><span class="sxs-lookup"><span data-stu-id="6ba32-291">Packing using a .nuspec</span></span>

<span data-ttu-id="6ba32-292">使用することができます、`.nuspec`ファイルをインポートする SDK のプロジェクト ファイルがある場合に、プロジェクトをパック`NuGet.Build.Tasks.Pack.targets`パック タスクを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="6ba32-292">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="6ba32-293">Nuspec ファイルをパックする前に、プロジェクトを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-293">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="6ba32-294">プロジェクト ファイルのターゲット フレームワークは関係ありませんされ、nuspec をパックするときに使用されません。</span><span class="sxs-lookup"><span data-stu-id="6ba32-294">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="6ba32-295">次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-295">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="6ba32-296">`NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="6ba32-296">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="6ba32-297">`NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="6ba32-297">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="6ba32-298">MSBuild コマンドラインの解析方法に従い、複数のプロパティは `-p:NuspecProperties=\"key1=value1;key2=value2\"` のように指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-298">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="6ba32-299">`NuspecBasePath`: `.nuspec` ファイルのベース パス。</span><span class="sxs-lookup"><span data-stu-id="6ba32-299">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="6ba32-300">`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-300">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="6ba32-301">MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-301">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="6ba32-302">既定では、プロジェクトを構築するために nuspec を梱包 dotnet.exe または msbuild を使用して潜在顧客もことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6ba32-302">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="6ba32-303">これを渡すことによって回避できます```--no-build```プロパティの設定に相当する、dotnet.exe を```<NoBuild>true</NoBuild> ```設定と共に、プロジェクト ファイルで```<IncludeBuildOutput>false</IncludeBuildOutput> ```プロジェクト ファイル</span><span class="sxs-lookup"><span data-stu-id="6ba32-303">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="6ba32-304">Nuspec ファイルをパックする csproj ファイルの例を示します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-304">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="6ba32-305">カスタマイズされたパッケージを作成する拡張ポイントの詳細</span><span class="sxs-lookup"><span data-stu-id="6ba32-305">Advanced extension points to create customized package</span></span>

<span data-ttu-id="6ba32-306">`pack`ターゲットは、内部のターゲット フレームワーク固有のビルドで実行している 2 つの拡張機能ポイントを提供します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-306">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="6ba32-307">拡張機能ポイントは、ターゲット フレームワークの特定のコンテンツなど、パッケージにアセンブリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="6ba32-307">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="6ba32-308">`TargetsForTfmSpecificBuildOutput` ターゲット: 内のファイルの使用、`lib`フォルダー、またはフォルダーを使用して指定`BuildOutputTargetFolder`します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-308">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="6ba32-309">`TargetsForTfmSpecificContentInPackage` ターゲット: 外にファイルを使用して、`BuildOutputTargetFolder`します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-309">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="6ba32-310">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="6ba32-310">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="6ba32-311">カスタムのターゲットを作成しの値として指定する、`$(TargetsForTfmSpecificBuildOutput)`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="6ba32-311">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="6ba32-312">移動する必要があるすべてのファイルに対して、 `BuildOutputTargetFolder` (既定では lib)、ターゲットは、ItemGroup にそれらのファイルを書き込む必要があります`BuildOutputInPackage`し、次の 2 つのメタデータ値の設定。</span><span class="sxs-lookup"><span data-stu-id="6ba32-312">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="6ba32-313">`FinalOutputPath`: ファイルの絶対パス指定しない場合、ソース パスを評価する Id が使用します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-313">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="6ba32-314">`TargetPath`: (省略可能) ファイルがサブフォルダー内にする必要があるときに設定`lib\<TargetFramework>`サテライト アセンブリのそれぞれのカルチャ フォルダーの下には、その移動など、します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-314">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="6ba32-315">既定値は、ファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="6ba32-315">Defaults to the name of the file.</span></span>

<span data-ttu-id="6ba32-316">例:</span><span class="sxs-lookup"><span data-stu-id="6ba32-316">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="6ba32-317">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="6ba32-317">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="6ba32-318">カスタムのターゲットを作成しの値として指定する、`$(TargetsForTfmSpecificContentInPackage)`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="6ba32-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="6ba32-319">パッケージに含める任意のファイルのターゲットは、ItemGroup にそれらのファイルを書き込む必要があります`TfmSpecificPackageFile`し、次の省略可能なメタデータを設定します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-319">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="6ba32-320">`PackagePath`: パス、ファイルがパッケージの出力をする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-320">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="6ba32-321">NuGet は、1 つ以上のファイルが同じパッケージのパスに追加された場合に警告を発行します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-321">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="6ba32-322">`BuildAction`: かどうかは、パッケージ パスでは、ファイルに割り当てるには、ビルド アクションにのみ必要な`contentFiles`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="6ba32-322">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="6ba32-323">"None"に既定値です。</span><span class="sxs-lookup"><span data-stu-id="6ba32-323">Defaults to "None".</span></span>

<span data-ttu-id="6ba32-324">例:</span><span class="sxs-lookup"><span data-stu-id="6ba32-324">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="6ba32-325">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="6ba32-325">restore target</span></span>

<span data-ttu-id="6ba32-326">`MSBuild -t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-326">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="6ba32-327">すべてのプロジェクト間参照を読み取ります</span><span class="sxs-lookup"><span data-stu-id="6ba32-327">Read all project to project references</span></span>
1. <span data-ttu-id="6ba32-328">プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します</span><span class="sxs-lookup"><span data-stu-id="6ba32-328">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="6ba32-329">MSBuild データを NuGet.Build.Tasks.dll に渡します</span><span class="sxs-lookup"><span data-stu-id="6ba32-329">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="6ba32-330">restore を実行します</span><span class="sxs-lookup"><span data-stu-id="6ba32-330">Run restore</span></span>
1. <span data-ttu-id="6ba32-331">パッケージをダウンロードします</span><span class="sxs-lookup"><span data-stu-id="6ba32-331">Download packages</span></span>
1. <span data-ttu-id="6ba32-332">アセット ファイル、ターゲット、およびプロパティを出力します</span><span class="sxs-lookup"><span data-stu-id="6ba32-332">Write assets file, targets, and props</span></span>

<span data-ttu-id="6ba32-333">`restore`対象 works**のみ**PackageReference 形式を使用してプロジェクトの。</span><span class="sxs-lookup"><span data-stu-id="6ba32-333">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="6ba32-334">**いない**を使用するプロジェクトの作業、`packages.config`は書式指定を使用して、 [nuget 復元](../tools/cli-ref-restore.md)代わりにします。</span><span class="sxs-lookup"><span data-stu-id="6ba32-334">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="6ba32-335">restore のプロパティ</span><span class="sxs-lookup"><span data-stu-id="6ba32-335">Restore properties</span></span>

<span data-ttu-id="6ba32-336">追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-336">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="6ba32-337">また、`-p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="6ba32-337">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="6ba32-338">プロパティ</span><span class="sxs-lookup"><span data-stu-id="6ba32-338">Property</span></span> | <span data-ttu-id="6ba32-339">説明</span><span class="sxs-lookup"><span data-stu-id="6ba32-339">Description</span></span> |
|--------|--------|
| <span data-ttu-id="6ba32-340">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="6ba32-340">RestoreSources</span></span> | <span data-ttu-id="6ba32-341">パッケージ ソースのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="6ba32-341">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="6ba32-342">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="6ba32-342">RestorePackagesPath</span></span> | <span data-ttu-id="6ba32-343">ユーザー パッケージ フォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="6ba32-343">User packages folder path.</span></span> |
| <span data-ttu-id="6ba32-344">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="6ba32-344">RestoreDisableParallel</span></span> | <span data-ttu-id="6ba32-345">ダウンロード数を一度に 1 つまでに制限します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-345">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="6ba32-346">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="6ba32-346">RestoreConfigFile</span></span> | <span data-ttu-id="6ba32-347">適用する `Nuget.Config` ファイルのパス。</span><span class="sxs-lookup"><span data-stu-id="6ba32-347">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="6ba32-348">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="6ba32-348">RestoreNoCache</span></span> | <span data-ttu-id="6ba32-349">True の場合は、キャッシュされたパッケージを使用して回避できます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-349">If true, avoids using cached packages.</span></span> <span data-ttu-id="6ba32-350">参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-350">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="6ba32-351">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="6ba32-351">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="6ba32-352">true の場合、失敗した、または不足しているパッケージ ソースを無視します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-352">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="6ba32-353">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="6ba32-353">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="6ba32-354">`NuGet.Build.Tasks.dll` のパス。</span><span class="sxs-lookup"><span data-stu-id="6ba32-354">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="6ba32-355">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="6ba32-355">RestoreGraphProjectInput</span></span> | <span data-ttu-id="6ba32-356">復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ba32-356">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="6ba32-357">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="6ba32-357">RestoreOutputPath</span></span> | <span data-ttu-id="6ba32-358">出力フォルダー。既定値は `obj` フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6ba32-358">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="6ba32-359">使用例</span><span class="sxs-lookup"><span data-stu-id="6ba32-359">Examples</span></span>

<span data-ttu-id="6ba32-360">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="6ba32-360">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="6ba32-361">プロジェクト ファイル:</span><span class="sxs-lookup"><span data-stu-id="6ba32-361">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="6ba32-362">restore の出力</span><span class="sxs-lookup"><span data-stu-id="6ba32-362">Restore outputs</span></span>

<span data-ttu-id="6ba32-363">restore で、次のファイルがビルドの `obj` フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-363">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="6ba32-364">ファイル</span><span class="sxs-lookup"><span data-stu-id="6ba32-364">File</span></span> | <span data-ttu-id="6ba32-365">説明</span><span class="sxs-lookup"><span data-stu-id="6ba32-365">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="6ba32-366">すべてのパッケージ参照の依存関係グラフが含まれています。</span><span class="sxs-lookup"><span data-stu-id="6ba32-366">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="6ba32-367">パッケージに含まれる MSBuild プロパティへの参照</span><span class="sxs-lookup"><span data-stu-id="6ba32-367">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="6ba32-368">パッケージに含まれる MSBuild ターゲットへの参照</span><span class="sxs-lookup"><span data-stu-id="6ba32-368">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="6ba32-369">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="6ba32-369">PackageTargetFallback</span></span>

<span data-ttu-id="6ba32-370">`PackageTargetFallback` 要素では、パッケージの復元時に使用する、互換性のある一連のターゲットを指定できます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-370">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="6ba32-371">dotnet [TxM](../reference/target-frameworks.md) を使用するパッケージが、dotnet TxM を宣言していない互換性のあるパッケージと連携できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="6ba32-371">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="6ba32-372">つまり、プロジェクトで dotnet TxM を使用せず、依存するすべてのパッケージに dotnet TxM を与える必要がある場合、非 dotnet プラットフォームを dotnet 対応にするためにプロジェクトに `<PackageTargetFallback>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-372">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="6ba32-373">たとえば、プロジェクトが `netstandard1.6` TxM を使用し、依存しているパッケージに `lib/net45/a.dll` と `lib/portable-net45+win81/a.dll` のみが含まれている場合、そのプロジェクトはビルドできません。</span><span class="sxs-lookup"><span data-stu-id="6ba32-373">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="6ba32-374">後者の DLL を構築する予定の場合は、`portable-net45+win81` DLL に互換性を持たせるために、次のように `PackageTargetFallback` を追加します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-374">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="6ba32-375">プロジェクト内のすべてのターゲットについてフォールバックを宣言するには、`Condition` 属性を省略します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-375">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="6ba32-376">また、次のように `$(PackageTargetFallback)` を含めて、既存の `PackageTargetFallback` を拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-376">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="6ba32-377">復元グラフの 1 つのライブラリを置き換える</span><span class="sxs-lookup"><span data-stu-id="6ba32-377">Replacing one library from a restore graph</span></span>

<span data-ttu-id="6ba32-378">復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="6ba32-378">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="6ba32-379">まず、最上位の `PackageReference` ですべてのアセットを除外します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-379">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="6ba32-380">次に、DLL の適切なローカル コピーに独自の参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="6ba32-380">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
