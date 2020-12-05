---
title: MSBuild ターゲットとしての NuGet の pack と restore
description: NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 4a04c6dd7993fc47bcf7a6fe46236ed700a0d105
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738930"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="0c739-103">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="0c739-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="0c739-104">*NuGet 4.0 以降*</span><span class="sxs-lookup"><span data-stu-id="0c739-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="0c739-105">[PackageReference](../consume-packages/package-references-in-project-files.md)形式では、NuGet 4.0 以降では、個別のファイルを使用するのではなく、すべてのマニフェストメタデータをプロジェクトファイル内に直接格納でき `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="0c739-106">MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。</span><span class="sxs-lookup"><span data-stu-id="0c739-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="0c739-107">これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます </span><span class="sxs-lookup"><span data-stu-id="0c739-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="0c739-108">MSBuild を使用して NuGet パッケージを作成する手順については、「 [msbuild を使用した nuget パッケージの作成](../create-packages/creating-a-package-msbuild.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c739-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="0c739-109">(NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../reference/cli-reference/cli-ref-pack.md) および [restore](../reference/cli-reference/cli-ref-restore.md) コマンドを使用します)。</span><span class="sxs-lookup"><span data-stu-id="0c739-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="0c739-110">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="0c739-110">Target build order</span></span>

<span data-ttu-id="0c739-111">`pack` と `restore` は MSBuild のターゲットなので、アクセスするとワークフローを強化できます。</span><span class="sxs-lookup"><span data-stu-id="0c739-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="0c739-112">たとえば、パック後にパッケージをネットワーク共有にコピーするとします。</span><span class="sxs-lookup"><span data-stu-id="0c739-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="0c739-113">この場合、プロジェクト ファイルに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="0c739-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="0c739-114">同様に、MSBuild タスクを記述し、独自のターゲットを記述して、MSBuild タスクで NuGet プロパティを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="0c739-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="0c739-115">`$(OutputPath)` は相対であり、プロジェクトのルートからコマンドを実行していることを想定しています。</span><span class="sxs-lookup"><span data-stu-id="0c739-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="0c739-116">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="0c739-116">pack target</span></span>

<span data-ttu-id="0c739-117">PackageReference 形式を使用する .NET Standard プロジェクトでは、を使用して、 `msbuild -t:pack` NuGet パッケージの作成で使用する入力をプロジェクトファイルから描画します。</span><span class="sxs-lookup"><span data-stu-id="0c739-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="0c739-118">以下の表では、最初の `<PropertyGroup>` ノード内のプロジェクト ファイルに追加できる MSBuild のプロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="0c739-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="0c739-119">Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="0c739-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="0c739-120">便宜上、テーブルは[ `.nuspec` ファイル](../reference/nuspec.md)内の同等のプロパティによって整理されています。</span><span class="sxs-lookup"><span data-stu-id="0c739-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="0c739-121">`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="0c739-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="0c739-122">属性/NuSpec の値</span><span class="sxs-lookup"><span data-stu-id="0c739-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="0c739-123">MSBuild のプロパティ</span><span class="sxs-lookup"><span data-stu-id="0c739-123">MSBuild Property</span></span> | <span data-ttu-id="0c739-124">Default</span><span class="sxs-lookup"><span data-stu-id="0c739-124">Default</span></span> | <span data-ttu-id="0c739-125">メモ</span><span class="sxs-lookup"><span data-stu-id="0c739-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="0c739-126">Id</span><span class="sxs-lookup"><span data-stu-id="0c739-126">Id</span></span> | <span data-ttu-id="0c739-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="0c739-127">PackageId</span></span> | <span data-ttu-id="0c739-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="0c739-128">AssemblyName</span></span> | <span data-ttu-id="0c739-129">MSBuild の $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="0c739-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="0c739-130">バージョン</span><span class="sxs-lookup"><span data-stu-id="0c739-130">Version</span></span> | <span data-ttu-id="0c739-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="0c739-131">PackageVersion</span></span> | <span data-ttu-id="0c739-132">バージョン</span><span class="sxs-lookup"><span data-stu-id="0c739-132">Version</span></span> | <span data-ttu-id="0c739-133">これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345")</span><span class="sxs-lookup"><span data-stu-id="0c739-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="0c739-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0c739-134">VersionPrefix</span></span> | <span data-ttu-id="0c739-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0c739-135">PackageVersionPrefix</span></span> | <span data-ttu-id="0c739-136">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-136">empty</span></span> | <span data-ttu-id="0c739-137">PackageVersion を設定すると、PackageVersionPrefix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="0c739-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="0c739-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0c739-138">VersionSuffix</span></span> | <span data-ttu-id="0c739-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0c739-139">PackageVersionSuffix</span></span> | <span data-ttu-id="0c739-140">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-140">empty</span></span> | <span data-ttu-id="0c739-141">MSBuild の $(VersionSuffix)</span><span class="sxs-lookup"><span data-stu-id="0c739-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="0c739-142">PackageVersion を設定すると、PackageVersionSuffix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="0c739-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="0c739-143">Authors</span><span class="sxs-lookup"><span data-stu-id="0c739-143">Authors</span></span> | <span data-ttu-id="0c739-144">Authors</span><span class="sxs-lookup"><span data-stu-id="0c739-144">Authors</span></span> | <span data-ttu-id="0c739-145">現在のユーザーのユーザー名</span><span class="sxs-lookup"><span data-stu-id="0c739-145">Username of the current user</span></span> | |
| <span data-ttu-id="0c739-146">所有者</span><span class="sxs-lookup"><span data-stu-id="0c739-146">Owners</span></span> | <span data-ttu-id="0c739-147">N/A</span><span class="sxs-lookup"><span data-stu-id="0c739-147">N/A</span></span> | <span data-ttu-id="0c739-148">NuSpec にはありません</span><span class="sxs-lookup"><span data-stu-id="0c739-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="0c739-149">タイトル</span><span class="sxs-lookup"><span data-stu-id="0c739-149">Title</span></span> | <span data-ttu-id="0c739-150">タイトル</span><span class="sxs-lookup"><span data-stu-id="0c739-150">Title</span></span> | <span data-ttu-id="0c739-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="0c739-151">The PackageId</span></span>| |
| <span data-ttu-id="0c739-152">説明</span><span class="sxs-lookup"><span data-stu-id="0c739-152">Description</span></span> | <span data-ttu-id="0c739-153">説明</span><span class="sxs-lookup"><span data-stu-id="0c739-153">Description</span></span> | <span data-ttu-id="0c739-154">"パッケージの説明"</span><span class="sxs-lookup"><span data-stu-id="0c739-154">"Package Description"</span></span> | |
| <span data-ttu-id="0c739-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="0c739-155">Copyright</span></span> | <span data-ttu-id="0c739-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="0c739-156">Copyright</span></span> | <span data-ttu-id="0c739-157">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-157">empty</span></span> | |
| <span data-ttu-id="0c739-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0c739-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="0c739-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0c739-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="0c739-160">false</span><span class="sxs-lookup"><span data-stu-id="0c739-160">false</span></span> | |
| <span data-ttu-id="0c739-161">license</span><span class="sxs-lookup"><span data-stu-id="0c739-161">license</span></span> | <span data-ttu-id="0c739-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="0c739-162">PackageLicenseExpression</span></span> | <span data-ttu-id="0c739-163">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-163">empty</span></span> | <span data-ttu-id="0c739-164">`<license type="expression">` に対応します</span><span class="sxs-lookup"><span data-stu-id="0c739-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="0c739-165">license</span><span class="sxs-lookup"><span data-stu-id="0c739-165">license</span></span> | <span data-ttu-id="0c739-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="0c739-166">PackageLicenseFile</span></span> | <span data-ttu-id="0c739-167">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-167">empty</span></span> | <span data-ttu-id="0c739-168">`<license type="file">` に相当します。</span><span class="sxs-lookup"><span data-stu-id="0c739-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="0c739-169">参照されているライセンスファイルを明示的にパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="0c739-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-170">LicenseUrl</span></span> | <span data-ttu-id="0c739-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-171">PackageLicenseUrl</span></span> | <span data-ttu-id="0c739-172">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-172">empty</span></span> | <span data-ttu-id="0c739-173">`PackageLicenseUrl` 非推奨です。パッケージのパッケージを使用して、パッケージのプロパティを</span><span class="sxs-lookup"><span data-stu-id="0c739-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="0c739-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-174">ProjectUrl</span></span> | <span data-ttu-id="0c739-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-175">PackageProjectUrl</span></span> | <span data-ttu-id="0c739-176">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-176">empty</span></span> | |
| <span data-ttu-id="0c739-177">アイコン</span><span class="sxs-lookup"><span data-stu-id="0c739-177">Icon</span></span> | <span data-ttu-id="0c739-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="0c739-178">PackageIcon</span></span> | <span data-ttu-id="0c739-179">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-179">empty</span></span> | <span data-ttu-id="0c739-180">参照されているアイコンイメージファイルを明示的にパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="0c739-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-181">IconUrl</span></span> | <span data-ttu-id="0c739-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-182">PackageIconUrl</span></span> | <span data-ttu-id="0c739-183">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-183">empty</span></span> | <span data-ttu-id="0c739-184">ベストダウンレベルのエクスペリエンスを向上させるには、 `PackageIconUrl` に加えてを指定する必要があり `PackageIcon` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="0c739-185">長期的には `PackageIconUrl` 非推奨となります。</span><span class="sxs-lookup"><span data-stu-id="0c739-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="0c739-186">タグ</span><span class="sxs-lookup"><span data-stu-id="0c739-186">Tags</span></span> | <span data-ttu-id="0c739-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="0c739-187">PackageTags</span></span> | <span data-ttu-id="0c739-188">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-188">empty</span></span> | <span data-ttu-id="0c739-189">複数のタグはセミコロン (;) で区切られます。</span><span class="sxs-lookup"><span data-stu-id="0c739-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="0c739-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0c739-190">ReleaseNotes</span></span> | <span data-ttu-id="0c739-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0c739-191">PackageReleaseNotes</span></span> | <span data-ttu-id="0c739-192">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-192">empty</span></span> | |
| <span data-ttu-id="0c739-193">リポジトリ/Url</span><span class="sxs-lookup"><span data-stu-id="0c739-193">Repository/Url</span></span> | <span data-ttu-id="0c739-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-194">RepositoryUrl</span></span> | <span data-ttu-id="0c739-195">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-195">empty</span></span> | <span data-ttu-id="0c739-196">ソースコードの複製または取得に使用されるリポジトリの URL。</span><span class="sxs-lookup"><span data-stu-id="0c739-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="0c739-197">よう *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="0c739-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="0c739-198">リポジトリ/種類</span><span class="sxs-lookup"><span data-stu-id="0c739-198">Repository/Type</span></span> | <span data-ttu-id="0c739-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0c739-199">RepositoryType</span></span> | <span data-ttu-id="0c739-200">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-200">empty</span></span> | <span data-ttu-id="0c739-201">リポジトリの種類。</span><span class="sxs-lookup"><span data-stu-id="0c739-201">Repository type.</span></span> <span data-ttu-id="0c739-202">例: *git*、 *tfs*。</span><span class="sxs-lookup"><span data-stu-id="0c739-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="0c739-203">リポジトリ/ブランチ</span><span class="sxs-lookup"><span data-stu-id="0c739-203">Repository/Branch</span></span> | <span data-ttu-id="0c739-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="0c739-204">RepositoryBranch</span></span> | <span data-ttu-id="0c739-205">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-205">empty</span></span> | <span data-ttu-id="0c739-206">リポジトリのブランチ情報 (オプション)。</span><span class="sxs-lookup"><span data-stu-id="0c739-206">Optional repository branch information.</span></span> <span data-ttu-id="0c739-207">このプロパティを含めるには、 *RepositoryUrl* も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="0c739-208">例: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="0c739-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="0c739-209">リポジトリ/コミット</span><span class="sxs-lookup"><span data-stu-id="0c739-209">Repository/Commit</span></span> | <span data-ttu-id="0c739-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="0c739-210">RepositoryCommit</span></span> | <span data-ttu-id="0c739-211">empty</span><span class="sxs-lookup"><span data-stu-id="0c739-211">empty</span></span> | <span data-ttu-id="0c739-212">任意のリポジトリ コミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。</span><span class="sxs-lookup"><span data-stu-id="0c739-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="0c739-213">このプロパティを含めるには、 *RepositoryUrl* も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="0c739-214">例: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="0c739-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="0c739-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="0c739-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="0c739-216">まとめ</span><span class="sxs-lookup"><span data-stu-id="0c739-216">Summary</span></span> | <span data-ttu-id="0c739-217">サポートされていません</span><span class="sxs-lookup"><span data-stu-id="0c739-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="0c739-218">pack ターゲットの入力</span><span class="sxs-lookup"><span data-stu-id="0c739-218">pack target inputs</span></span>

- <span data-ttu-id="0c739-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="0c739-219">IsPackable</span></span>
- <span data-ttu-id="0c739-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="0c739-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="0c739-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="0c739-221">PackageVersion</span></span>
- <span data-ttu-id="0c739-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="0c739-222">PackageId</span></span>
- <span data-ttu-id="0c739-223">Authors</span><span class="sxs-lookup"><span data-stu-id="0c739-223">Authors</span></span>
- <span data-ttu-id="0c739-224">Description</span><span class="sxs-lookup"><span data-stu-id="0c739-224">Description</span></span>
- <span data-ttu-id="0c739-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="0c739-225">Copyright</span></span>
- <span data-ttu-id="0c739-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0c739-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="0c739-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="0c739-227">DevelopmentDependency</span></span>
- <span data-ttu-id="0c739-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="0c739-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="0c739-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="0c739-229">PackageLicenseFile</span></span>
- <span data-ttu-id="0c739-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="0c739-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-231">PackageProjectUrl</span></span>
- <span data-ttu-id="0c739-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-232">PackageIconUrl</span></span>
- <span data-ttu-id="0c739-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0c739-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="0c739-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="0c739-234">PackageTags</span></span>
- <span data-ttu-id="0c739-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="0c739-235">PackageOutputPath</span></span>
- <span data-ttu-id="0c739-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="0c739-236">IncludeSymbols</span></span>
- <span data-ttu-id="0c739-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="0c739-237">IncludeSource</span></span>
- <span data-ttu-id="0c739-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="0c739-238">PackageTypes</span></span>
- <span data-ttu-id="0c739-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="0c739-239">IsTool</span></span>
- <span data-ttu-id="0c739-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-240">RepositoryUrl</span></span>
- <span data-ttu-id="0c739-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0c739-241">RepositoryType</span></span>
- <span data-ttu-id="0c739-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="0c739-242">RepositoryBranch</span></span>
- <span data-ttu-id="0c739-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="0c739-243">RepositoryCommit</span></span>
- <span data-ttu-id="0c739-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="0c739-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="0c739-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="0c739-245">MinClientVersion</span></span>
- <span data-ttu-id="0c739-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="0c739-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="0c739-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="0c739-247">IncludeContentInPack</span></span>
- <span data-ttu-id="0c739-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="0c739-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="0c739-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="0c739-249">ContentTargetFolders</span></span>
- <span data-ttu-id="0c739-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="0c739-250">NuspecFile</span></span>
- <span data-ttu-id="0c739-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="0c739-251">NuspecBasePath</span></span>
- <span data-ttu-id="0c739-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="0c739-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="0c739-253">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="0c739-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="0c739-254">依存関係を表示しない</span><span class="sxs-lookup"><span data-stu-id="0c739-254">Suppress dependencies</span></span>

<span data-ttu-id="0c739-255">生成された NuGet パッケージからパッケージの依存関係を抑制するに `SuppressDependenciesWhenPacking` は、をに設定します。これにより、生成された `true` nupkg ファイルからのすべての依存関係がスキップされます。</span><span class="sxs-lookup"><span data-stu-id="0c739-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="0c739-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0c739-256">PackageIconUrl</span></span>

<span data-ttu-id="0c739-257">`PackageIconUrl` は、新しいプロパティを優先するように非推奨とされ [`PackageIcon`](#packageicon) ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="0c739-258">NuGet 5.3 & Visual Studio 2019 バージョン16.3 以降では、 `pack` パッケージメタデータでのみが指定されている場合、 [NU5048](./errors-and-warnings/nu5048.md) warning が発生し `PackageIconUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="0c739-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="0c739-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="0c739-260">を `PackageIcon` `PackageIconUrl` まだサポートしていないクライアントとソースとの下位互換性を維持するには、との両方を指定する必要があり `PackageIcon` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="0c739-261">Visual Studio では `PackageIcon` 、将来のリリースでフォルダーベースのソースからのパッケージがサポートされるようになります。</span><span class="sxs-lookup"><span data-stu-id="0c739-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="0c739-262">アイコンイメージファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="0c739-262">Packing an icon image file</span></span>

<span data-ttu-id="0c739-263">アイコンイメージファイルをパッキングする場合は、パッケージ `PackageIcon` のルートに対して相対的なパッケージパスを指定するために、プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="0c739-264">また、ファイルがパッケージに含まれていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="0c739-265">イメージファイルのサイズは 1 MB に制限されています。</span><span class="sxs-lookup"><span data-stu-id="0c739-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="0c739-266">サポートされているファイル形式は、JPEG および PNG です。</span><span class="sxs-lookup"><span data-stu-id="0c739-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="0c739-267">128x128 のイメージの解像度をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0c739-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="0c739-268">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="0c739-268">For example:</span></span>

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

<span data-ttu-id="0c739-269">[パッケージアイコンのサンプル](https://github.com/NuGet/Samples/tree/master/PackageIconExample)です。</span><span class="sxs-lookup"><span data-stu-id="0c739-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="0c739-270">Nuspec に相当するものについては、「 [nuspec reference for icon」を参照](nuspec.md#icon)してください。</span><span class="sxs-lookup"><span data-stu-id="0c739-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="0c739-271">出力アセンブリ</span><span class="sxs-lookup"><span data-stu-id="0c739-271">Output assemblies</span></span>

<span data-ttu-id="0c739-272">`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="0c739-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="0c739-273">コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。</span><span class="sxs-lookup"><span data-stu-id="0c739-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="0c739-274">出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。</span><span class="sxs-lookup"><span data-stu-id="0c739-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="0c739-275">`IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。</span><span class="sxs-lookup"><span data-stu-id="0c739-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="0c739-276">`BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="0c739-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="0c739-277">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="0c739-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="0c739-278">パッケージ参照</span><span class="sxs-lookup"><span data-stu-id="0c739-278">Package references</span></span>

<span data-ttu-id="0c739-279">「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c739-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="0c739-280">プロジェクト間参照</span><span class="sxs-lookup"><span data-stu-id="0c739-280">Project to project references</span></span>

<span data-ttu-id="0c739-281">プロジェクト間参照は、既定で NuGet パッケージ参照として見なされています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="0c739-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="0c739-282">また、次のメタデータをプロジェクト参照に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="0c739-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="0c739-283">パッケージにコンテンツを含める</span><span class="sxs-lookup"><span data-stu-id="0c739-283">Including content in a package</span></span>

<span data-ttu-id="0c739-284">コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="0c739-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="0c739-285">次のようなエントリでオーバーライドしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="0c739-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="0c739-286">次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="0c739-287">(`content` および `contentFiles` フォルダーの両方ではなく) すべてのコンテンツを特定のルート フォルダーにのみコピーする場合、MSBuild プロパティの `ContentTargetFolders` を使用できます。このプロパティの既定値は "content;contentFiles" ですが、他の任意のフォルダー名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="0c739-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="0c739-288">`ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="0c739-289">`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="0c739-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="0c739-290">空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="0c739-291">たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="0c739-292">また、MSBuild プロパティの `$(IncludeContentInPack)` もあります。既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="0c739-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="0c739-293">これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="0c739-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="0c739-294">上記の任意の項目に設定できる他の pack 固有のメタデータとして、NuSpec の ```contentFiles``` エントリに ```CopyToOutput``` 値と ```Flatten``` 値を設定する ```<PackageCopyToOutput>``` と ```<PackageFlatten>``` があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="0c739-295">コンテンツ項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="0c739-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="0c739-296">glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="0c739-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="0c739-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="0c739-297">IncludeSymbols</span></span>

<span data-ttu-id="0c739-298">`MSBuild -t:pack -p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="0c739-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="0c739-299">`IncludeSymbols=true` を設定すると、通常のパッケージ *と* シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="0c739-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="0c739-300">IncludeSource</span></span>

<span data-ttu-id="0c739-301">これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。</span><span class="sxs-lookup"><span data-stu-id="0c739-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="0c739-302">種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="0c739-303">`TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。</span><span class="sxs-lookup"><span data-stu-id="0c739-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="0c739-304">種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="0c739-305">ライセンス式またはライセンスファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="0c739-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="0c739-306">ライセンス式を使用する場合は、"パッケージの表示" プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="0c739-307">[ライセンス式のサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="0c739-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="0c739-308">[NuGet.org によって受け付けられるライセンス式とライセンスの詳細については、こちらを参照](nuspec.md#license)してください。</span><span class="sxs-lookup"><span data-stu-id="0c739-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="0c739-309">ライセンスファイルをパッキングする場合は、パッケージのルートを基準としたパッケージパスを指定するために、"パッケージの作成" プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="0c739-310">また、ファイルがパッケージに含まれていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="0c739-311">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="0c739-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="0c739-312">[ライセンスファイルのサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="0c739-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="0c739-313">IsTool</span><span class="sxs-lookup"><span data-stu-id="0c739-313">IsTool</span></span>

<span data-ttu-id="0c739-314">`MSBuild -t:pack -p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="0c739-314">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="0c739-315">これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="0c739-315">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="0c739-316">.nuspec を使用したパック</span><span class="sxs-lookup"><span data-stu-id="0c739-316">Packing using a .nuspec</span></span>

<span data-ttu-id="0c739-317">通常はファイル内の [すべてのプロパティ](../reference/msbuild-targets.md#pack-target) をプロジェクトファイルに含めることをお勧めし `.nuspec` ますが、プロジェクトを `.nuspec` パックするためにファイルを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="0c739-317">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="0c739-318">を使用する SDK スタイル以外のプロジェクトでは `PackageReference` 、をインポートして、 `NuGet.Build.Tasks.Pack.targets` パックタスクを実行できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-318">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="0c739-319">Nuspec ファイルをパックする前に、プロジェクトを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-319">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="0c739-320">(SDK スタイルのプロジェクトには、既定でパックターゲットが含まれています)。</span><span class="sxs-lookup"><span data-stu-id="0c739-320">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="0c739-321">Nuspec をパッキングする場合、プロジェクトファイルのターゲットフレームワークは無関係であり、使用されません。</span><span class="sxs-lookup"><span data-stu-id="0c739-321">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="0c739-322">次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-322">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="0c739-323">`NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="0c739-323">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="0c739-324">`NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="0c739-324">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="0c739-325">MSBuild コマンドラインの解析方法に従い、複数のプロパティは `-p:NuspecProperties="key1=value1;key2=value2"` のように指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-325">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="0c739-326">`NuspecBasePath`: `.nuspec` ファイルのベース パス。</span><span class="sxs-lookup"><span data-stu-id="0c739-326">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="0c739-327">`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="0c739-327">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="0c739-328">MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="0c739-328">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="0c739-329">dotnet.exe または msbuild を使用して nuspec をパッキングすると、既定でプロジェクトがビルドされることにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="0c739-329">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="0c739-330">これは、プロパティを dotnet.exe に渡すことによって回避できます。これは、プロジェクトファイルの ```--no-build``` 設定 ```<NoBuild>true</NoBuild> ``` と共に、プロジェクトファイル内の設定に相当し ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-330">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="0c739-331">Nuspec ファイルをパックする .csproj ファイルの例を次に示し *ます。*</span><span class="sxs-lookup"><span data-stu-id="0c739-331">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="0c739-332">カスタマイズされたパッケージを作成するための高度な拡張ポイント</span><span class="sxs-lookup"><span data-stu-id="0c739-332">Advanced extension points to create customized package</span></span>

<span data-ttu-id="0c739-333">ターゲットには、 `pack` ターゲットフレームワーク固有の内部ビルドで実行される2つの拡張ポイントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="0c739-333">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="0c739-334">拡張ポイントは、ターゲットフレームワーク固有のコンテンツとアセンブリをパッケージに含めることをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="0c739-334">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="0c739-335">`TargetsForTfmSpecificBuildOutput` ターゲット: フォルダー内のファイル、 `lib` またはを使用して指定されたフォルダー内のファイルに使用し `BuildOutputTargetFolder` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-335">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="0c739-336">`TargetsForTfmSpecificContentInPackage` ターゲット: の外部のファイルに対して使用し `BuildOutputTargetFolder` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-336">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="0c739-337">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="0c739-337">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="0c739-338">カスタムターゲットを作成し、プロパティの値として指定し `$(TargetsForTfmSpecificBuildOutput)` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-338">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="0c739-339">(既定では lib) に移動する必要があるファイルの場合、 `BuildOutputTargetFolder` ターゲットはこれらのファイルを ItemGroup に書き込み、 `BuildOutputInPackage` 次の2つのメタデータ値を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-339">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="0c739-340">`FinalOutputPath`: ファイルの絶対パス。指定されていない場合は、ソースパスの評価に Id が使用されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-340">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="0c739-341">`TargetPath`: (省略可能) ファイルが内のサブフォルダーに入る必要があるときに設定し `lib\<TargetFramework>` ます。これは、それぞれのカルチャフォルダーの下にあるサテライトアセンブリのようになります。</span><span class="sxs-lookup"><span data-stu-id="0c739-341">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="0c739-342">既定値は、ファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="0c739-342">Defaults to the name of the file.</span></span>

<span data-ttu-id="0c739-343">例:</span><span class="sxs-lookup"><span data-stu-id="0c739-343">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="0c739-344">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="0c739-344">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="0c739-345">カスタムターゲットを作成し、プロパティの値として指定し `$(TargetsForTfmSpecificContentInPackage)` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="0c739-346">パッケージに含めるファイルについては、ターゲットはこれらのファイルを ItemGroup に書き込み、 `TfmSpecificPackageFile` 次のオプションのメタデータを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-346">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="0c739-347">`PackagePath`: パッケージでファイルを出力するパス。</span><span class="sxs-lookup"><span data-stu-id="0c739-347">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="0c739-348">複数のファイルが同じパッケージパスに追加されると、NuGet は警告を発行します。</span><span class="sxs-lookup"><span data-stu-id="0c739-348">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="0c739-349">`BuildAction`: ファイルに割り当てるビルドアクション。パッケージパスがフォルダー内にある場合にのみ必要です `contentFiles` 。</span><span class="sxs-lookup"><span data-stu-id="0c739-349">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="0c739-350">既定値は "None" です。</span><span class="sxs-lookup"><span data-stu-id="0c739-350">Defaults to "None".</span></span>

<span data-ttu-id="0c739-351">例:</span><span class="sxs-lookup"><span data-stu-id="0c739-351">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="0c739-352">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="0c739-352">restore target</span></span>

<span data-ttu-id="0c739-353">`MSBuild -t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="0c739-353">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="0c739-354">すべてのプロジェクト間参照を読み取ります</span><span class="sxs-lookup"><span data-stu-id="0c739-354">Read all project to project references</span></span>
1. <span data-ttu-id="0c739-355">プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します</span><span class="sxs-lookup"><span data-stu-id="0c739-355">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="0c739-356">MSBuild データを NuGet.Build.Tasks.dll に渡す</span><span class="sxs-lookup"><span data-stu-id="0c739-356">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="0c739-357">restore を実行します</span><span class="sxs-lookup"><span data-stu-id="0c739-357">Run restore</span></span>
1. <span data-ttu-id="0c739-358">パッケージのダウンロード</span><span class="sxs-lookup"><span data-stu-id="0c739-358">Download packages</span></span>
1. <span data-ttu-id="0c739-359">アセット ファイル、ターゲット、およびプロパティを出力します</span><span class="sxs-lookup"><span data-stu-id="0c739-359">Write assets file, targets, and props</span></span>

<span data-ttu-id="0c739-360">ターゲットは、 `restore` PackageReference 形式を使用するプロジェクトに対して機能します。</span><span class="sxs-lookup"><span data-stu-id="0c739-360">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="0c739-361">`MSBuild 16.5+` では、形式の [オプトインもサポート](#restoring-packagereference-and-packages.config-with-msbuild) されてい `packages.config` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-361">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packages.config-with-msbuild) for the `packages.config` format.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="0c739-362">restore のプロパティ</span><span class="sxs-lookup"><span data-stu-id="0c739-362">Restore properties</span></span>

<span data-ttu-id="0c739-363">追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。</span><span class="sxs-lookup"><span data-stu-id="0c739-363">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="0c739-364">また、`-p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="0c739-364">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="0c739-365">プロパティ</span><span class="sxs-lookup"><span data-stu-id="0c739-365">Property</span></span> | <span data-ttu-id="0c739-366">Description</span><span class="sxs-lookup"><span data-stu-id="0c739-366">Description</span></span> |
|--------|--------|
| <span data-ttu-id="0c739-367">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="0c739-367">RestoreSources</span></span> | <span data-ttu-id="0c739-368">パッケージ ソースのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="0c739-368">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="0c739-369">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="0c739-369">RestorePackagesPath</span></span> | <span data-ttu-id="0c739-370">ユーザー パッケージ フォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="0c739-370">User packages folder path.</span></span> |
| <span data-ttu-id="0c739-371">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="0c739-371">RestoreDisableParallel</span></span> | <span data-ttu-id="0c739-372">ダウンロード数を一度に 1 つまでに制限します。</span><span class="sxs-lookup"><span data-stu-id="0c739-372">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="0c739-373">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="0c739-373">RestoreConfigFile</span></span> | <span data-ttu-id="0c739-374">適用する `Nuget.Config` ファイルのパス。</span><span class="sxs-lookup"><span data-stu-id="0c739-374">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="0c739-375">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="0c739-375">RestoreNoCache</span></span> | <span data-ttu-id="0c739-376">True の場合、キャッシュされたパッケージの使用を回避します。</span><span class="sxs-lookup"><span data-stu-id="0c739-376">If true, avoids using cached packages.</span></span> <span data-ttu-id="0c739-377">「 [グローバルパッケージとキャッシュフォルダーの管理」を](../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c739-377">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="0c739-378">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="0c739-378">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="0c739-379">true の場合、失敗した、または不足しているパッケージ ソースを無視します。</span><span class="sxs-lookup"><span data-stu-id="0c739-379">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="0c739-380">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="0c739-380">RestoreFallbackFolders</span></span> | <span data-ttu-id="0c739-381">フォールバックフォルダー。ユーザーパッケージフォルダーを使用する場合と同じ方法で使用されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="0c739-382">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="0c739-382">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="0c739-383">復元中に使用する追加のソース。</span><span class="sxs-lookup"><span data-stu-id="0c739-383">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="0c739-384">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="0c739-384">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="0c739-385">復元中に使用する追加のフォールバックフォルダー。</span><span class="sxs-lookup"><span data-stu-id="0c739-385">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="0c739-386">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="0c739-386">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="0c739-387">で指定されたフォールバックフォルダーを除外します。 `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="0c739-387">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="0c739-388">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="0c739-388">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="0c739-389">`NuGet.Build.Tasks.dll` のパス。</span><span class="sxs-lookup"><span data-stu-id="0c739-389">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="0c739-390">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="0c739-390">RestoreGraphProjectInput</span></span> | <span data-ttu-id="0c739-391">復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c739-391">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="0c739-392">Restoreentkipnon存在 Enttargets</span><span class="sxs-lookup"><span data-stu-id="0c739-392">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="0c739-393">MSBuild を使用してプロジェクトが収集されると、最適化を使用してプロジェクトを収集するかどうかが決定され `SkipNonexistentTargets` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-393">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="0c739-394">設定しない場合、の既定値はに `true` なります。</span><span class="sxs-lookup"><span data-stu-id="0c739-394">When not set, defaults to `true`.</span></span> <span data-ttu-id="0c739-395">その結果、プロジェクトのターゲットをインポートできない場合のフェールファースト動作になります。</span><span class="sxs-lookup"><span data-stu-id="0c739-395">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="0c739-396">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="0c739-396">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="0c739-397">出力フォルダー。を既定 `BaseIntermediateOutputPath` として、フォルダーをにし `obj` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-397">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="0c739-398">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="0c739-398">RestoreForce</span></span> | <span data-ttu-id="0c739-399">PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-399">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="0c739-400">このフラグを指定することは、ファイルの削除に似てい `project.assets.json` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-400">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="0c739-401">これは、http キャッシュをバイパスしません。</span><span class="sxs-lookup"><span data-stu-id="0c739-401">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="0c739-402">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="0c739-402">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="0c739-403">ロック ファイルの使用をオプトインします。</span><span class="sxs-lookup"><span data-stu-id="0c739-403">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="0c739-404">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="0c739-404">RestoreLockedMode</span></span> | <span data-ttu-id="0c739-405">ロックモードで復元を実行します。</span><span class="sxs-lookup"><span data-stu-id="0c739-405">Run restore in locked mode.</span></span> <span data-ttu-id="0c739-406">これは、restore が依存関係を再評価しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="0c739-406">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="0c739-407">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="0c739-407">NuGetLockFilePath</span></span> | <span data-ttu-id="0c739-408">ロックファイルのカスタムの場所。</span><span class="sxs-lookup"><span data-stu-id="0c739-408">A custom location for the lock file.</span></span> <span data-ttu-id="0c739-409">既定の場所はプロジェクトの横にあり、という名前が付けられ `packages.lock.json` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-409">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="0c739-410">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="0c739-410">RestoreForceEvaluate</span></span> | <span data-ttu-id="0c739-411">復元によって依存関係が再計算され、警告なしでロックファイルが更新されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-411">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="0c739-412">Restoreパッケージ構成</span><span class="sxs-lookup"><span data-stu-id="0c739-412">RestorePackagesConfig</span></span> | <span data-ttu-id="0c739-413">オプトインスイッチ。 packages.config でプロジェクトを復元します。でのみサポートさ `MSBuild -t:restore` れます。</span><span class="sxs-lookup"><span data-stu-id="0c739-413">An opt in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |

#### <a name="examples"></a><span data-ttu-id="0c739-414">例</span><span class="sxs-lookup"><span data-stu-id="0c739-414">Examples</span></span>

<span data-ttu-id="0c739-415">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="0c739-415">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="0c739-416">プロジェクト ファイル:</span><span class="sxs-lookup"><span data-stu-id="0c739-416">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="0c739-417">restore の出力</span><span class="sxs-lookup"><span data-stu-id="0c739-417">Restore outputs</span></span>

<span data-ttu-id="0c739-418">restore で、次のファイルがビルドの `obj` フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-418">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="0c739-419">ファイル</span><span class="sxs-lookup"><span data-stu-id="0c739-419">File</span></span> | <span data-ttu-id="0c739-420">説明</span><span class="sxs-lookup"><span data-stu-id="0c739-420">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="0c739-421">すべてのパッケージ参照の依存関係グラフを含みます。</span><span class="sxs-lookup"><span data-stu-id="0c739-421">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="0c739-422">パッケージに含まれる MSBuild プロパティへの参照</span><span class="sxs-lookup"><span data-stu-id="0c739-422">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="0c739-423">パッケージに含まれる MSBuild ターゲットへの参照</span><span class="sxs-lookup"><span data-stu-id="0c739-423">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="0c739-424">1つの MSBuild コマンドを使用した復元とビルド</span><span class="sxs-lookup"><span data-stu-id="0c739-424">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="0c739-425">NuGet では、MSBuild のターゲットとプロパティを表示するパッケージを復元できるため、異なるグローバルプロパティを使用して復元とビルドの評価が実行されます。</span><span class="sxs-lookup"><span data-stu-id="0c739-425">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="0c739-426">これは、次のような場合に予期しない動作が発生する可能性があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="0c739-426">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="0c739-427">代わりに、推奨される方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="0c739-427">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="0c739-428">と同様に、同じロジックが他のターゲットにも適用され `build` ます。</span><span class="sxs-lookup"><span data-stu-id="0c739-428">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="0c739-429">MSBuild を使用した PackageReference と packages.config の復元</span><span class="sxs-lookup"><span data-stu-id="0c739-429">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="0c739-430">MSBuild 16.5 + では、packages.config もサポートされて `msbuild -t:restore` います。</span><span class="sxs-lookup"><span data-stu-id="0c739-430">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="0c739-431">`packages.config` restore は、ではなく、でのみ使用でき `MSBuild 16.5+` ます。 `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="0c739-431">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="0c739-432">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="0c739-432">PackageTargetFallback</span></span>

<span data-ttu-id="0c739-433">`PackageTargetFallback` 要素では、パッケージの復元時に使用する、互換性のある一連のターゲットを指定できます。</span><span class="sxs-lookup"><span data-stu-id="0c739-433">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="0c739-434">dotnet [TxM](../reference/target-frameworks.md) を使用するパッケージが、dotnet TxM を宣言していない互換性のあるパッケージと連携できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="0c739-434">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="0c739-435">つまり、プロジェクトで dotnet TxM を使用せず、依存するすべてのパッケージに dotnet TxM を与える必要がある場合、非 dotnet プラットフォームを dotnet 対応にするためにプロジェクトに `<PackageTargetFallback>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="0c739-435">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="0c739-436">たとえば、プロジェクトが `netstandard1.6` TxM を使用し、依存しているパッケージに `lib/net45/a.dll` と `lib/portable-net45+win81/a.dll` のみが含まれている場合、そのプロジェクトはビルドできません。</span><span class="sxs-lookup"><span data-stu-id="0c739-436">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="0c739-437">後者の DLL を構築する予定の場合は、`portable-net45+win81` DLL に互換性を持たせるために、次のように `PackageTargetFallback` を追加します。</span><span class="sxs-lookup"><span data-stu-id="0c739-437">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="0c739-438">プロジェクト内のすべてのターゲットについてフォールバックを宣言するには、`Condition` 属性を省略します。</span><span class="sxs-lookup"><span data-stu-id="0c739-438">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="0c739-439">また、次のように `$(PackageTargetFallback)` を含めて、既存の `PackageTargetFallback` を拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="0c739-439">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="0c739-440">復元グラフの 1 つのライブラリを置き換える</span><span class="sxs-lookup"><span data-stu-id="0c739-440">Replacing one library from a restore graph</span></span>

<span data-ttu-id="0c739-441">復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="0c739-441">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="0c739-442">まず、最上位の `PackageReference` ですべてのアセットを除外します。</span><span class="sxs-lookup"><span data-stu-id="0c739-442">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="0c739-443">次に、DLL の適切なローカル コピーに独自の参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="0c739-443">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
