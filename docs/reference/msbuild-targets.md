---
title: MSBuild ターゲットとしての NuGet の pack と restore
description: NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0c32978baf6146f10c262ba7af94f61fee22272d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777717"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="f6e07-103">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="f6e07-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="f6e07-104">*NuGet 4.0 以降*</span><span class="sxs-lookup"><span data-stu-id="f6e07-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="f6e07-105">[PackageReference](../consume-packages/package-references-in-project-files.md)形式では、NuGet 4.0 以降では、個別のファイルを使用するのではなく、すべてのマニフェストメタデータをプロジェクトファイル内に直接格納でき `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="f6e07-106">MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。</span><span class="sxs-lookup"><span data-stu-id="f6e07-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="f6e07-107">これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます </span><span class="sxs-lookup"><span data-stu-id="f6e07-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="f6e07-108">MSBuild を使用して NuGet パッケージを作成する手順については、「 [msbuild を使用した nuget パッケージの作成](../create-packages/creating-a-package-msbuild.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="f6e07-109">(NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../reference/cli-reference/cli-ref-pack.md) および [restore](../reference/cli-reference/cli-ref-restore.md) コマンドを使用します)。</span><span class="sxs-lookup"><span data-stu-id="f6e07-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="f6e07-110">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="f6e07-110">Target build order</span></span>

<span data-ttu-id="f6e07-111">`pack` と `restore` は MSBuild のターゲットなので、アクセスするとワークフローを強化できます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="f6e07-112">たとえば、パック後にパッケージをネットワーク共有にコピーするとします。</span><span class="sxs-lookup"><span data-stu-id="f6e07-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="f6e07-113">この場合、プロジェクト ファイルに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="f6e07-114">同様に、MSBuild タスクを記述し、独自のターゲットを記述して、MSBuild タスクで NuGet プロパティを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="f6e07-115">`$(OutputPath)` は相対であり、プロジェクトのルートからコマンドを実行していることを想定しています。</span><span class="sxs-lookup"><span data-stu-id="f6e07-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="f6e07-116">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="f6e07-116">pack target</span></span>

<span data-ttu-id="f6e07-117">形式を使用する .NET プロジェクトでは `PackageReference` 、を使用して、 `msbuild -t:pack` NuGet パッケージの作成に使用するプロジェクトファイルからの入力を描画します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="f6e07-118">次の表では、最初のノード内のプロジェクトファイルに追加できる MSBuild のプロパティについて説明し `<PropertyGroup>` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="f6e07-119">Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="f6e07-120">便宜上、テーブルは[ `.nuspec` ファイル](../reference/nuspec.md)内の同等のプロパティによって整理されています。</span><span class="sxs-lookup"><span data-stu-id="f6e07-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="f6e07-121">`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="f6e07-122">属性/NuSpec の値</span><span class="sxs-lookup"><span data-stu-id="f6e07-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="f6e07-123">MSBuild のプロパティ</span><span class="sxs-lookup"><span data-stu-id="f6e07-123">MSBuild Property</span></span> | <span data-ttu-id="f6e07-124">Default</span><span class="sxs-lookup"><span data-stu-id="f6e07-124">Default</span></span> | <span data-ttu-id="f6e07-125">Notes</span><span class="sxs-lookup"><span data-stu-id="f6e07-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="f6e07-126">Id</span><span class="sxs-lookup"><span data-stu-id="f6e07-126">Id</span></span> | <span data-ttu-id="f6e07-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="f6e07-127">PackageId</span></span> | <span data-ttu-id="f6e07-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="f6e07-128">AssemblyName</span></span> | <span data-ttu-id="f6e07-129">MSBuild の $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="f6e07-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="f6e07-130">Version</span><span class="sxs-lookup"><span data-stu-id="f6e07-130">Version</span></span> | <span data-ttu-id="f6e07-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="f6e07-131">PackageVersion</span></span> | <span data-ttu-id="f6e07-132">Version</span><span class="sxs-lookup"><span data-stu-id="f6e07-132">Version</span></span> | <span data-ttu-id="f6e07-133">これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345")</span><span class="sxs-lookup"><span data-stu-id="f6e07-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="f6e07-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="f6e07-134">VersionPrefix</span></span> | <span data-ttu-id="f6e07-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="f6e07-135">PackageVersionPrefix</span></span> | <span data-ttu-id="f6e07-136">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-136">empty</span></span> | <span data-ttu-id="f6e07-137">PackageVersion を設定すると、PackageVersionPrefix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="f6e07-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="f6e07-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="f6e07-138">VersionSuffix</span></span> | <span data-ttu-id="f6e07-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="f6e07-139">PackageVersionSuffix</span></span> | <span data-ttu-id="f6e07-140">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-140">empty</span></span> | <span data-ttu-id="f6e07-141">MSBuild の $(VersionSuffix)</span><span class="sxs-lookup"><span data-stu-id="f6e07-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="f6e07-142">PackageVersion を設定すると、PackageVersionSuffix は上書きされます</span><span class="sxs-lookup"><span data-stu-id="f6e07-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="f6e07-143">Authors</span><span class="sxs-lookup"><span data-stu-id="f6e07-143">Authors</span></span> | <span data-ttu-id="f6e07-144">Authors</span><span class="sxs-lookup"><span data-stu-id="f6e07-144">Authors</span></span> | <span data-ttu-id="f6e07-145">現在のユーザーのユーザー名</span><span class="sxs-lookup"><span data-stu-id="f6e07-145">Username of the current user</span></span> | <span data-ttu-id="f6e07-146">nuget.org のプロファイル名と一致するパッケージ作成者をセミコロンで区切った一覧。これらは nuget.org の NuGet ギャラリーに表示され、同じ作成者によるパッケージの相互参照に使用されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-146">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| <span data-ttu-id="f6e07-147">所有者</span><span class="sxs-lookup"><span data-stu-id="f6e07-147">Owners</span></span> | <span data-ttu-id="f6e07-148">該当なし</span><span class="sxs-lookup"><span data-stu-id="f6e07-148">N/A</span></span> | <span data-ttu-id="f6e07-149">NuSpec にはありません</span><span class="sxs-lookup"><span data-stu-id="f6e07-149">Not present in NuSpec</span></span> | |
| <span data-ttu-id="f6e07-150">タイトル</span><span class="sxs-lookup"><span data-stu-id="f6e07-150">Title</span></span> | <span data-ttu-id="f6e07-151">タイトル</span><span class="sxs-lookup"><span data-stu-id="f6e07-151">Title</span></span> | <span data-ttu-id="f6e07-152">PackageId</span><span class="sxs-lookup"><span data-stu-id="f6e07-152">The PackageId</span></span>| <span data-ttu-id="f6e07-153">人が読みやすいパッケージのタイトル。通常、nuget.org と、Visual Studio のパッケージ マネージャーの UI 画面で使用されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-153">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| <span data-ttu-id="f6e07-154">説明</span><span class="sxs-lookup"><span data-stu-id="f6e07-154">Description</span></span> | <span data-ttu-id="f6e07-155">説明</span><span class="sxs-lookup"><span data-stu-id="f6e07-155">Description</span></span> | <span data-ttu-id="f6e07-156">"パッケージの説明"</span><span class="sxs-lookup"><span data-stu-id="f6e07-156">"Package Description"</span></span> | <span data-ttu-id="f6e07-157">アセンブリの長い説明。</span><span class="sxs-lookup"><span data-stu-id="f6e07-157">A long description for the assembly.</span></span> <span data-ttu-id="f6e07-158">`PackageDescription` が指定されていない場合、このプロパティはパッケージの説明としても使用されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-158">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| <span data-ttu-id="f6e07-159">Copyright</span><span class="sxs-lookup"><span data-stu-id="f6e07-159">Copyright</span></span> | <span data-ttu-id="f6e07-160">Copyright</span><span class="sxs-lookup"><span data-stu-id="f6e07-160">Copyright</span></span> | <span data-ttu-id="f6e07-161">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-161">empty</span></span> | <span data-ttu-id="f6e07-162">パッケージの著作権の詳細。</span><span class="sxs-lookup"><span data-stu-id="f6e07-162">Copyright details for the package.</span></span> |
| <span data-ttu-id="f6e07-163">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f6e07-163">RequireLicenseAcceptance</span></span> | <span data-ttu-id="f6e07-164">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f6e07-164">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="f6e07-165">false</span><span class="sxs-lookup"><span data-stu-id="f6e07-165">false</span></span> | <span data-ttu-id="f6e07-166">クライアントがユーザーに対して、パッケージのインストール前にパッケージ ライセンスに同意することを必須にするかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="f6e07-166">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="f6e07-167">license</span><span class="sxs-lookup"><span data-stu-id="f6e07-167">license</span></span> | <span data-ttu-id="f6e07-168">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="f6e07-168">PackageLicenseExpression</span></span> | <span data-ttu-id="f6e07-169">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-169">empty</span></span> | <span data-ttu-id="f6e07-170">`<license type="expression">` に相当します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-170">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="f6e07-171">「 [ライセンス式またはライセンスファイルのパッキング](#packing-a-license-expression-or-a-license-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-171">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="f6e07-172">license</span><span class="sxs-lookup"><span data-stu-id="f6e07-172">license</span></span> | <span data-ttu-id="f6e07-173">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="f6e07-173">PackageLicenseFile</span></span> | <span data-ttu-id="f6e07-174">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-174">empty</span></span> | <span data-ttu-id="f6e07-175">カスタムライセンスまたは SPDX 識別子が割り当てられていないライセンスを使用している場合の、パッケージ内のライセンスファイルへのパス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-175">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="f6e07-176">参照されているライセンスファイルを明示的にパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-176">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="f6e07-177">`<license type="file">` に相当します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-177">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="f6e07-178">「 [ライセンス式またはライセンスファイルのパッキング](#packing-a-license-expression-or-a-license-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-178">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="f6e07-179">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-179">LicenseUrl</span></span> | <span data-ttu-id="f6e07-180">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-180">PackageLicenseUrl</span></span> | <span data-ttu-id="f6e07-181">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-181">empty</span></span> | <span data-ttu-id="f6e07-182">`PackageLicenseUrl` は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-182">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="f6e07-183">代わりに、`PackageLicenseExpression` タグまたは `PackageLicenseFile` タグを使用してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-183">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| <span data-ttu-id="f6e07-184">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-184">ProjectUrl</span></span> | <span data-ttu-id="f6e07-185">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-185">PackageProjectUrl</span></span> | <span data-ttu-id="f6e07-186">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-186">empty</span></span> | |
| <span data-ttu-id="f6e07-187">アイコン</span><span class="sxs-lookup"><span data-stu-id="f6e07-187">Icon</span></span> | <span data-ttu-id="f6e07-188">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="f6e07-188">PackageIcon</span></span> | <span data-ttu-id="f6e07-189">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-189">empty</span></span> | <span data-ttu-id="f6e07-190">パッケージ アイコンとして使用するパッケージ内の画像へのパス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-190">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="f6e07-191">参照されているアイコンイメージファイルを明示的にパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-191">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="f6e07-192">詳細については、「[アイコンイメージファイル](#packing-an-icon-image-file)と[ `icon` メタデータ](/nuget/reference/nuspec#icon)のパッキング」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-192">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](/nuget/reference/nuspec#icon).</span></span> |
| <span data-ttu-id="f6e07-193">IconUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-193">IconUrl</span></span> | <span data-ttu-id="f6e07-194">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-194">PackageIconUrl</span></span> | <span data-ttu-id="f6e07-195">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-195">empty</span></span> | <span data-ttu-id="f6e07-196">`PackageIconUrl` は、を優先するために非推奨とされ `PackageIcon` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-196">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="f6e07-197">ただし、最も高いダウンレベルエクスペリエンスを実現するには、に加えてを指定する必要があり `PackageIconUrl` `PackageIcon` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-197">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| <span data-ttu-id="f6e07-198">Tags</span><span class="sxs-lookup"><span data-stu-id="f6e07-198">Tags</span></span> | <span data-ttu-id="f6e07-199">PackageTags</span><span class="sxs-lookup"><span data-stu-id="f6e07-199">PackageTags</span></span> | <span data-ttu-id="f6e07-200">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-200">empty</span></span> | <span data-ttu-id="f6e07-201">パッケージを指定するタグのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="f6e07-201">A semicolon-delimited list of tags that designates the package.</span></span> |
| <span data-ttu-id="f6e07-202">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f6e07-202">ReleaseNotes</span></span> | <span data-ttu-id="f6e07-203">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f6e07-203">PackageReleaseNotes</span></span> | <span data-ttu-id="f6e07-204">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-204">empty</span></span> | <span data-ttu-id="f6e07-205">パッケージのリリース ノート。</span><span class="sxs-lookup"><span data-stu-id="f6e07-205">Release notes for the package.</span></span> |
| <span data-ttu-id="f6e07-206">リポジトリ/Url</span><span class="sxs-lookup"><span data-stu-id="f6e07-206">Repository/Url</span></span> | <span data-ttu-id="f6e07-207">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-207">RepositoryUrl</span></span> | <span data-ttu-id="f6e07-208">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-208">empty</span></span> | <span data-ttu-id="f6e07-209">ソースコードの複製または取得に使用されるリポジトリの URL。</span><span class="sxs-lookup"><span data-stu-id="f6e07-209">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="f6e07-210">例: *https://github.com/NuGet/NuGet.Client.git* 。</span><span class="sxs-lookup"><span data-stu-id="f6e07-210">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| <span data-ttu-id="f6e07-211">リポジトリ/種類</span><span class="sxs-lookup"><span data-stu-id="f6e07-211">Repository/Type</span></span> | <span data-ttu-id="f6e07-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="f6e07-212">RepositoryType</span></span> | <span data-ttu-id="f6e07-213">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-213">empty</span></span> | <span data-ttu-id="f6e07-214">リポジトリの種類。</span><span class="sxs-lookup"><span data-stu-id="f6e07-214">Repository type.</span></span> <span data-ttu-id="f6e07-215">例: `git` (既定値)、 `tfs` 。</span><span class="sxs-lookup"><span data-stu-id="f6e07-215">Examples: `git` (default), `tfs`.</span></span> |
| <span data-ttu-id="f6e07-216">リポジトリ/ブランチ</span><span class="sxs-lookup"><span data-stu-id="f6e07-216">Repository/Branch</span></span> | <span data-ttu-id="f6e07-217">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="f6e07-217">RepositoryBranch</span></span> | <span data-ttu-id="f6e07-218">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-218">empty</span></span> | <span data-ttu-id="f6e07-219">リポジトリのブランチ情報 (オプション)。</span><span class="sxs-lookup"><span data-stu-id="f6e07-219">Optional repository branch information.</span></span> <span data-ttu-id="f6e07-220">このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-220">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="f6e07-221">例: *master* (NuGet 4.7.0 +)。</span><span class="sxs-lookup"><span data-stu-id="f6e07-221">Example: *master* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="f6e07-222">リポジトリ/コミット</span><span class="sxs-lookup"><span data-stu-id="f6e07-222">Repository/Commit</span></span> | <span data-ttu-id="f6e07-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="f6e07-223">RepositoryCommit</span></span> | <span data-ttu-id="f6e07-224">empty</span><span class="sxs-lookup"><span data-stu-id="f6e07-224">empty</span></span> | <span data-ttu-id="f6e07-225">任意のリポジトリ コミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-225">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="f6e07-226">このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-226">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="f6e07-227">例: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)。</span><span class="sxs-lookup"><span data-stu-id="f6e07-227">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="f6e07-228">PackageType</span><span class="sxs-lookup"><span data-stu-id="f6e07-228">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="f6e07-229">まとめ</span><span class="sxs-lookup"><span data-stu-id="f6e07-229">Summary</span></span> | <span data-ttu-id="f6e07-230">サポートされていません</span><span class="sxs-lookup"><span data-stu-id="f6e07-230">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="f6e07-231">pack ターゲットの入力</span><span class="sxs-lookup"><span data-stu-id="f6e07-231">pack target inputs</span></span>

| <span data-ttu-id="f6e07-232">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f6e07-232">Property</span></span> | <span data-ttu-id="f6e07-233">説明</span><span class="sxs-lookup"><span data-stu-id="f6e07-233">Description</span></span> |
| - | - |
| <span data-ttu-id="f6e07-234">IsPackable</span><span class="sxs-lookup"><span data-stu-id="f6e07-234">IsPackable</span></span> | <span data-ttu-id="f6e07-235">プロジェクトをパックできるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="f6e07-235">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="f6e07-236">既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-236">The default value is `true`.</span></span> |
| <span data-ttu-id="f6e07-237">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="f6e07-237">SuppressDependenciesWhenPacking</span></span> | <span data-ttu-id="f6e07-238">`true`生成された NuGet パッケージからのパッケージの依存関係を抑制するには、に設定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-238">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| <span data-ttu-id="f6e07-239">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="f6e07-239">PackageVersion</span></span> | <span data-ttu-id="f6e07-240">結果のパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-240">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="f6e07-241">すべてのフォームの NuGet バージョン文字列を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-241">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="f6e07-242">既定値は `$(Version)` です。つまり、プロジェクトのプロパティ `Version` の値です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-242">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| <span data-ttu-id="f6e07-243">PackageId</span><span class="sxs-lookup"><span data-stu-id="f6e07-243">PackageId</span></span> | <span data-ttu-id="f6e07-244">結果のパッケージの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-244">Specifies the name for the resulting package.</span></span> <span data-ttu-id="f6e07-245">指定しない場合、`pack` 操作の既定では、`AssemblyName` またはディレクトリ名をパッケージ名として使用します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-245">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| <span data-ttu-id="f6e07-246">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="f6e07-246">PackageDescription</span></span> | <span data-ttu-id="f6e07-247">UI 画面用のパッケージの長い説明。</span><span class="sxs-lookup"><span data-stu-id="f6e07-247">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="f6e07-248">Authors</span><span class="sxs-lookup"><span data-stu-id="f6e07-248">Authors</span></span> | <span data-ttu-id="f6e07-249">nuget.org のプロファイル名と一致するパッケージ作成者をセミコロンで区切った一覧。これらは nuget.org の NuGet ギャラリーに表示され、同じ作成者によるパッケージの相互参照に使用されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-249">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| <span data-ttu-id="f6e07-250">説明</span><span class="sxs-lookup"><span data-stu-id="f6e07-250">Description</span></span> | <span data-ttu-id="f6e07-251">アセンブリの長い説明。</span><span class="sxs-lookup"><span data-stu-id="f6e07-251">A long description for the assembly.</span></span> <span data-ttu-id="f6e07-252">`PackageDescription` が指定されていない場合、このプロパティはパッケージの説明としても使用されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-252">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| <span data-ttu-id="f6e07-253">Copyright</span><span class="sxs-lookup"><span data-stu-id="f6e07-253">Copyright</span></span> | <span data-ttu-id="f6e07-254">パッケージの著作権の詳細。</span><span class="sxs-lookup"><span data-stu-id="f6e07-254">Copyright details for the package.</span></span> |
| <span data-ttu-id="f6e07-255">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f6e07-255">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="f6e07-256">クライアントがユーザーに対して、パッケージのインストール前にパッケージ ライセンスに同意することを必須にするかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="f6e07-256">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="f6e07-257">既定値は、`false` です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-257">The default is `false`.</span></span> |
| <span data-ttu-id="f6e07-258">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="f6e07-258">DevelopmentDependency</span></span> | <span data-ttu-id="f6e07-259">開発専用の依存関係としてパッケージをマークするかどうかを指定するブール値。指定すると、そのパッケージは他のパッケージに依存関係として含まれなくなります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-259">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="f6e07-260">`PackageReference`(NuGet 4.8 以降) では、このフラグはコンパイル時のアセットがコンパイルから除外されることも意味します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-260">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="f6e07-261">詳しくは、「[DevelopmentDependency support for PackageReference (PackageReference に対する DevelopmentDependency のサポート)](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-261">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| <span data-ttu-id="f6e07-262">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="f6e07-262">PackageLicenseExpression</span></span> | <span data-ttu-id="f6e07-263">[Spdx ライセンス識別子](https://spdx.org/licenses/)または式 (など) `Apache-2.0` 。</span><span class="sxs-lookup"><span data-stu-id="f6e07-263">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="f6e07-264">詳細については、「 [ライセンス式またはライセンスファイルのパッキング](#packing-a-license-expression-or-a-license-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-264">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="f6e07-265">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="f6e07-265">PackageLicenseFile</span></span> | <span data-ttu-id="f6e07-266">カスタムライセンスまたは SPDX 識別子が割り当てられていないライセンスを使用している場合の、パッケージ内のライセンスファイルへのパス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-266">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| <span data-ttu-id="f6e07-267">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-267">PackageLicenseUrl</span></span> | <span data-ttu-id="f6e07-268">`PackageLicenseUrl` は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-268">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="f6e07-269">代わりに、`PackageLicenseExpression` タグまたは `PackageLicenseFile` タグを使用してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-269">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| <span data-ttu-id="f6e07-270">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-270">PackageProjectUrl</span></span> | |
| <span data-ttu-id="f6e07-271">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="f6e07-271">PackageIcon</span></span> | <span data-ttu-id="f6e07-272">パッケージのルートに対して相対的なパッケージアイコンパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-272">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="f6e07-273">詳細については、「 [アイコンイメージファイルのパッキング](#packing-an-icon-image-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-273">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| <span data-ttu-id="f6e07-274">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f6e07-274">PackageReleaseNotes</span></span>| <span data-ttu-id="f6e07-275">パッケージのリリース ノート。</span><span class="sxs-lookup"><span data-stu-id="f6e07-275">Release notes for the package.</span></span> |
| <span data-ttu-id="f6e07-276">PackageTags</span><span class="sxs-lookup"><span data-stu-id="f6e07-276">PackageTags</span></span> | <span data-ttu-id="f6e07-277">パッケージを指定するタグのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="f6e07-277">A semicolon-delimited list of tags that designates the package.</span></span> |
| <span data-ttu-id="f6e07-278">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="f6e07-278">PackageOutputPath</span></span> | <span data-ttu-id="f6e07-279">パックされたパッケージをドロップする出力パスを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-279">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="f6e07-280">既定値は `$(OutputPath)` です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-280">Default is `$(OutputPath)`.</span></span> |
| <span data-ttu-id="f6e07-281">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="f6e07-281">IncludeSymbols</span></span> | <span data-ttu-id="f6e07-282">このブール値は、プロジェクトをパックするときに、パッケージが追加のシンボル パッケージを作成するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-282">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="f6e07-283">シンボル パッケージの形式は、`SymbolPackageFormat` プロパティで制御します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-283">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="f6e07-284">詳細については、「 [IncludeSymbols](#includesymbols)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-284">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| <span data-ttu-id="f6e07-285">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="f6e07-285">IncludeSource</span></span> | <span data-ttu-id="f6e07-286">このブール値は、パック プロセスでソース パッケージを作成するかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-286">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="f6e07-287">ソース パッケージには、ライブラリのソース コードと PDB ファイルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-287">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="f6e07-288">ソース ファイルは、結果のパッケージ ファイルの `src/ProjectName` ディレクトリに置かれます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-288">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="f6e07-289">詳細については、「データの追加」を[参照してください。](#includesource)</span><span class="sxs-lookup"><span data-stu-id="f6e07-289">For more information, see [IncludeSource](#includesource).</span></span> |
| <span data-ttu-id="f6e07-290">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="f6e07-290">PackageTypes</span></span>
| <span data-ttu-id="f6e07-291">IsTool</span><span class="sxs-lookup"><span data-stu-id="f6e07-291">IsTool</span></span> | <span data-ttu-id="f6e07-292">すべての出力ファイルを *lib* フォルダーではなく *tools* フォルダーにコピーするかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-292">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="f6e07-293">詳細については、「 [IsTool](#istool)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-293">For more information, see [IsTool](#istool).</span></span> |
| <span data-ttu-id="f6e07-294">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-294">RepositoryUrl</span></span> | <span data-ttu-id="f6e07-295">ソースコードの複製または取得に使用されるリポジトリの URL。</span><span class="sxs-lookup"><span data-stu-id="f6e07-295">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="f6e07-296">例: *https://github.com/NuGet/NuGet.Client.git* 。</span><span class="sxs-lookup"><span data-stu-id="f6e07-296">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| <span data-ttu-id="f6e07-297">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="f6e07-297">RepositoryType</span></span> | <span data-ttu-id="f6e07-298">リポジトリの種類。</span><span class="sxs-lookup"><span data-stu-id="f6e07-298">Repository type.</span></span> <span data-ttu-id="f6e07-299">例: `git` (既定値)、 `tfs` 。</span><span class="sxs-lookup"><span data-stu-id="f6e07-299">Examples: `git` (default), `tfs`.</span></span> |
| <span data-ttu-id="f6e07-300">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="f6e07-300">RepositoryBranch</span></span> | <span data-ttu-id="f6e07-301">リポジトリのブランチ情報 (オプション)。</span><span class="sxs-lookup"><span data-stu-id="f6e07-301">Optional repository branch information.</span></span> <span data-ttu-id="f6e07-302">このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-302">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="f6e07-303">例: *master* (NuGet 4.7.0 +)。</span><span class="sxs-lookup"><span data-stu-id="f6e07-303">Example: *master* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="f6e07-304">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="f6e07-304">RepositoryCommit</span></span> | <span data-ttu-id="f6e07-305">任意のリポジトリ コミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-305">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="f6e07-306">このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-306">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="f6e07-307">例: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)。</span><span class="sxs-lookup"><span data-stu-id="f6e07-307">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="f6e07-308">SymbolPackageFormat</span><span class="sxs-lookup"><span data-stu-id="f6e07-308">SymbolPackageFormat</span></span> | <span data-ttu-id="f6e07-309">シンボル パッケージの形式を指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-309">Specifies the format of the symbols package.</span></span> <span data-ttu-id="f6e07-310">"Symbols. nupkg" の場合、従来のシンボルパッケージは、Pdb、Dll、およびその他の出力ファイルを含む、 *シンボル* が含まれた拡張子が付いて作成されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-310">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="f6e07-311">"Snupkg" の場合、ポータブル Pdb を含む snupkg シンボルパッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-311">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="f6e07-312">既定値は "symbols. nupkg" です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-312">The default is "symbols.nupkg".</span></span> |
| <span data-ttu-id="f6e07-313">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="f6e07-313">NoPackageAnalysis</span></span> | <span data-ttu-id="f6e07-314">`pack`パッケージのビルド後にパッケージ分析を実行しないことを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-314">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="f6e07-315">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="f6e07-315">MinClientVersion</span></span> | <span data-ttu-id="f6e07-316">nuget.exe および Visual Studio パッケージ マネージャーで強制する、このパッケージをインストールできる NuGet クライアントの最小バージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-316">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| <span data-ttu-id="f6e07-317">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="f6e07-317">IncludeBuildOutput</span></span> | <span data-ttu-id="f6e07-318">このブール値は、ビルド出力アセンブリを *.nupkg* ファイルにパッケージ化するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-318">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| <span data-ttu-id="f6e07-319">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="f6e07-319">IncludeContentInPack</span></span> | <span data-ttu-id="f6e07-320">このブール値は、の型を持つ項目 `Content` が、結果のパッケージに自動的に含まれるかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-320">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="f6e07-321">既定値は、`true` です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-321">The default is `true`.</span></span> |
| <span data-ttu-id="f6e07-322">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="f6e07-322">BuildOutputTargetFolder</span></span> | <span data-ttu-id="f6e07-323">出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-323">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="f6e07-324">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-324">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="f6e07-325">詳細については、「 [出力アセンブリ](#output-assemblies)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-325">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| <span data-ttu-id="f6e07-326">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="f6e07-326">ContentTargetFolders</span></span> | <span data-ttu-id="f6e07-327">が指定されていない場合に、すべてのコンテンツファイルの移動先となる既定の場所を指定し `PackagePath` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-327">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="f6e07-328">既定値は "content;contentFiles" です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-328">The default value is "content;contentFiles".</span></span> <span data-ttu-id="f6e07-329">詳細については、「[Including content in a package](#including-content-in-a-package)」 (パッケージにコンテンツを追加する) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-329">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| <span data-ttu-id="f6e07-330">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="f6e07-330">NuspecFile</span></span> | <span data-ttu-id="f6e07-331">パックに使用する *.nuspec* ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-331">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="f6e07-332">指定した場合、パッケージ化情報 **専用** に使用され、プロジェクト内の情報は使用されません。</span><span class="sxs-lookup"><span data-stu-id="f6e07-332">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="f6e07-333">詳細については、「 [nuspec を使用したパッキング](#packing-using-a-nuspec)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-333">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |
| <span data-ttu-id="f6e07-334">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="f6e07-334">NuspecBasePath</span></span> | <span data-ttu-id="f6e07-335">*.nuspec* ファイルのベース パス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-335">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="f6e07-336">詳細については、「 [nuspec を使用したパッキング](#packing-using-a-nuspec)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-336">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |
| <span data-ttu-id="f6e07-337">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="f6e07-337">NuspecProperties</span></span> | <span data-ttu-id="f6e07-338">キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="f6e07-338">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="f6e07-339">詳細については、「 [nuspec を使用したパッキング](#packing-using-a-nuspec)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-339">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="f6e07-340">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f6e07-340">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="f6e07-341">依存関係を表示しない</span><span class="sxs-lookup"><span data-stu-id="f6e07-341">Suppress dependencies</span></span>

<span data-ttu-id="f6e07-342">生成された NuGet パッケージからパッケージの依存関係を抑制するに `SuppressDependenciesWhenPacking` は、をに設定します。これにより、生成された `true` nupkg ファイルからのすべての依存関係がスキップされます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-342">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="f6e07-343">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f6e07-343">PackageIconUrl</span></span>

<span data-ttu-id="f6e07-344">`PackageIconUrl` は、プロパティを優先するために非推奨とされ [`PackageIcon`](#packageicon) ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-344">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="f6e07-345">NuGet 5.3 および Visual Studio 2019 バージョン16.3 以降では、 `pack` パッケージメタデータでのみが指定されている場合、は [NU5048](./errors-and-warnings/nu5048.md) warning を発生させ `PackageIconUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-345">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="f6e07-346">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="f6e07-346">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="f6e07-347">まだサポートされていないクライアントおよびソースとの下位互換性を維持するに `PackageIcon` は、との両方を指定し `PackageIcon` `PackageIconUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-347">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="f6e07-348">Visual Studio で `PackageIcon` は、フォルダーベースのソースからのパッケージがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f6e07-348">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="f6e07-349">アイコンイメージファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="f6e07-349">Packing an icon image file</span></span>

<span data-ttu-id="f6e07-350">アイコンイメージファイルをパッキングする場合は、プロパティを使用して、 `PackageIcon` パッケージのルートを基準としたアイコンファイルのパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-350">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="f6e07-351">また、ファイルがパッケージに含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-351">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="f6e07-352">イメージファイルのサイズは 1 MB に制限されています。</span><span class="sxs-lookup"><span data-stu-id="f6e07-352">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="f6e07-353">サポートされているファイル形式は、JPEG および PNG です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-353">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="f6e07-354">128x128 のイメージの解像度をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f6e07-354">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="f6e07-355">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-355">For example:</span></span>

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

<span data-ttu-id="f6e07-356">[パッケージアイコンのサンプル](https://github.com/NuGet/Samples/tree/master/PackageIconExample)です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-356">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="f6e07-357">Nuspec に相当するものについては、「 [nuspec reference for icon」を参照](nuspec.md#icon)してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-357">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="f6e07-358">出力アセンブリ</span><span class="sxs-lookup"><span data-stu-id="f6e07-358">Output assemblies</span></span>

<span data-ttu-id="f6e07-359">`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="f6e07-359">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="f6e07-360">コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-360">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="f6e07-361">出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-361">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="f6e07-362">`IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。</span><span class="sxs-lookup"><span data-stu-id="f6e07-362">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="f6e07-363">`BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-363">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="f6e07-364">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-364">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="f6e07-365">パッケージ参照</span><span class="sxs-lookup"><span data-stu-id="f6e07-365">Package references</span></span>

<span data-ttu-id="f6e07-366">「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-366">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="f6e07-367">プロジェクト間参照</span><span class="sxs-lookup"><span data-stu-id="f6e07-367">Project to project references</span></span>

<span data-ttu-id="f6e07-368">プロジェクト間参照は、既定で NuGet パッケージ参照として見なされています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-368">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="f6e07-369">また、次のメタデータをプロジェクト参照に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-369">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="f6e07-370">パッケージにコンテンツを含める</span><span class="sxs-lookup"><span data-stu-id="f6e07-370">Including content in a package</span></span>

<span data-ttu-id="f6e07-371">コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-371">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="f6e07-372">次のようなエントリでオーバーライドしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-372">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="f6e07-373">次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-373">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="f6e07-374">(`content` および `contentFiles` フォルダーの両方ではなく) すべてのコンテンツを特定のルート フォルダーにのみコピーする場合、MSBuild プロパティの `ContentTargetFolders` を使用できます。このプロパティの既定値は "content;contentFiles" ですが、他の任意のフォルダー名に設定できます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-374">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="f6e07-375">`ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-375">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="f6e07-376">`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-376">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="f6e07-377">空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-377">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="f6e07-378">たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-378">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="f6e07-379">また、MSBuild プロパティの `$(IncludeContentInPack)` もあります。既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-379">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="f6e07-380">これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="f6e07-380">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="f6e07-381">上記の任意の項目に設定できる他の pack 固有のメタデータとして、NuSpec の ```contentFiles``` エントリに ```CopyToOutput``` 値と ```Flatten``` 値を設定する ```<PackageCopyToOutput>``` と ```<PackageFlatten>``` があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-381">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="f6e07-382">コンテンツ項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-382">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="f6e07-383">glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-383">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="f6e07-384">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="f6e07-384">IncludeSymbols</span></span>

<span data-ttu-id="f6e07-385">`MSBuild -t:pack -p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-385">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="f6e07-386">`IncludeSymbols=true` を設定すると、通常のパッケージ *と* シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-386">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="f6e07-387">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="f6e07-387">IncludeSource</span></span>

<span data-ttu-id="f6e07-388">これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。</span><span class="sxs-lookup"><span data-stu-id="f6e07-388">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="f6e07-389">種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-389">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="f6e07-390">`TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-390">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="f6e07-391">種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-391">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="f6e07-392">ライセンス式またはライセンスファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="f6e07-392">Packing a license expression or a license file</span></span>

<span data-ttu-id="f6e07-393">ライセンス式を使用する場合は、プロパティを使用し `PackageLicenseExpression` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-393">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="f6e07-394">サンプルについては、「 [ライセンス式のサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-394">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="f6e07-395">NuGet.org で受け入れられるライセンス式とライセンスの詳細については、「 [ライセンスメタデータ](nuspec.md#license)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-395">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="f6e07-396">ライセンスファイルをパッキングする場合は、パッケージ `PackageLicenseFile` のルートに対して相対的なパッケージパスをプロパティを使用して指定します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-396">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="f6e07-397">また、ファイルがパッケージに含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-397">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="f6e07-398">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-398">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="f6e07-399">サンプルについては、「 [ライセンスファイルのサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-399">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="f6e07-400">、、およびのいずれか1つだけを `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` 同時に指定できます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-400">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="f6e07-401">拡張子のないファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="f6e07-401">Packing a file without an extension</span></span>

<span data-ttu-id="f6e07-402">ライセンスファイルをパッキングする場合など、一部のシナリオでは、拡張子のないファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-402">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="f6e07-403">履歴の理由により、NuGet & MSBuild では、パスをディレクトリとして拡張せずにパスを扱います。</span><span class="sxs-lookup"><span data-stu-id="f6e07-403">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="f6e07-404">[拡張機能サンプルのないファイル](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/)。</span><span class="sxs-lookup"><span data-stu-id="f6e07-404">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="f6e07-405">IsTool</span><span class="sxs-lookup"><span data-stu-id="f6e07-405">IsTool</span></span>

<span data-ttu-id="f6e07-406">`MSBuild -t:pack -p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-406">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="f6e07-407">これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-407">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="f6e07-408">.nuspec を使用したパック</span><span class="sxs-lookup"><span data-stu-id="f6e07-408">Packing using a .nuspec</span></span>

<span data-ttu-id="f6e07-409">通常はファイル内の [すべてのプロパティ](../reference/msbuild-targets.md#pack-target) をプロジェクトファイルに含めることをお勧めし `.nuspec` ますが、プロジェクトを `.nuspec` パックするためにファイルを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-409">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="f6e07-410">を使用する SDK スタイル以外のプロジェクトでは `PackageReference` 、をインポートして、 `NuGet.Build.Tasks.Pack.targets` パックタスクを実行できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-410">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="f6e07-411">Nuspec ファイルをパックする前に、プロジェクトを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-411">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="f6e07-412">(SDK スタイルのプロジェクトには、既定でパックターゲットが含まれています)。</span><span class="sxs-lookup"><span data-stu-id="f6e07-412">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="f6e07-413">Nuspec をパッキングする場合、プロジェクトファイルのターゲットフレームワークは無関係であり、使用されません。</span><span class="sxs-lookup"><span data-stu-id="f6e07-413">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="f6e07-414">次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-414">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="f6e07-415">`NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-415">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="f6e07-416">`NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="f6e07-416">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="f6e07-417">MSBuild コマンドラインの解析方法に従い、複数のプロパティは `-p:NuspecProperties="key1=value1;key2=value2"` のように指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-417">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="f6e07-418">`NuspecBasePath`: `.nuspec` ファイルのベース パス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-418">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="f6e07-419">`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-419">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="f6e07-420">MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-420">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="f6e07-421">dotnet.exe または msbuild を使用して nuspec をパッキングすると、既定でプロジェクトがビルドされることにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-421">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="f6e07-422">これは、プロパティを dotnet.exe に渡すことによって回避できます。これは、プロジェクトファイルの ```--no-build``` 設定 ```<NoBuild>true</NoBuild> ``` と共に、プロジェクトファイル内の設定に相当し ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-422">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="f6e07-423">Nuspec ファイルをパックする .csproj ファイルの例を次に示し *ます。*</span><span class="sxs-lookup"><span data-stu-id="f6e07-423">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="f6e07-424">カスタマイズされたパッケージを作成するための高度な拡張ポイント</span><span class="sxs-lookup"><span data-stu-id="f6e07-424">Advanced extension points to create customized package</span></span>

<span data-ttu-id="f6e07-425">ターゲットには、 `pack` ターゲットフレームワーク固有の内部ビルドで実行される2つの拡張ポイントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="f6e07-425">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="f6e07-426">拡張ポイントは、ターゲットフレームワーク固有のコンテンツとアセンブリをパッケージに含めることをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="f6e07-426">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="f6e07-427">`TargetsForTfmSpecificBuildOutput` ターゲット: フォルダー内のファイル、 `lib` またはを使用して指定されたフォルダー内のファイルに使用し `BuildOutputTargetFolder` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-427">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="f6e07-428">`TargetsForTfmSpecificContentInPackage` ターゲット: の外部のファイルに対して使用し `BuildOutputTargetFolder` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-428">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="f6e07-429">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="f6e07-429">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="f6e07-430">カスタムターゲットを作成し、プロパティの値として指定し `$(TargetsForTfmSpecificBuildOutput)` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-430">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="f6e07-431">(既定では lib) に移動する必要があるファイルの場合、 `BuildOutputTargetFolder` ターゲットはこれらのファイルを ItemGroup に書き込み、 `BuildOutputInPackage` 次の2つのメタデータ値を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-431">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="f6e07-432">`FinalOutputPath`: ファイルの絶対パス。指定されていない場合は、ソースパスの評価に Id が使用されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-432">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="f6e07-433">`TargetPath`: (省略可能) ファイルが内のサブフォルダーに入る必要があるときに設定し `lib\<TargetFramework>` ます。これは、それぞれのカルチャフォルダーの下にあるサテライトアセンブリのようになります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-433">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="f6e07-434">既定値は、ファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-434">Defaults to the name of the file.</span></span>

<span data-ttu-id="f6e07-435">例:</span><span class="sxs-lookup"><span data-stu-id="f6e07-435">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="f6e07-436">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="f6e07-436">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="f6e07-437">カスタムターゲットを作成し、プロパティの値として指定し `$(TargetsForTfmSpecificContentInPackage)` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-437">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="f6e07-438">パッケージに含めるファイルについては、ターゲットはこれらのファイルを ItemGroup に書き込み、 `TfmSpecificPackageFile` 次のオプションのメタデータを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-438">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="f6e07-439">`PackagePath`: パッケージでファイルを出力するパス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-439">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="f6e07-440">複数のファイルが同じパッケージパスに追加されると、NuGet は警告を発行します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-440">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="f6e07-441">`BuildAction`: ファイルに割り当てるビルドアクション。パッケージパスがフォルダー内にある場合にのみ必要です `contentFiles` 。</span><span class="sxs-lookup"><span data-stu-id="f6e07-441">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="f6e07-442">既定値は "None" です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-442">Defaults to "None".</span></span>

<span data-ttu-id="f6e07-443">例:</span><span class="sxs-lookup"><span data-stu-id="f6e07-443">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="f6e07-444">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="f6e07-444">restore target</span></span>

<span data-ttu-id="f6e07-445">`MSBuild -t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-445">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="f6e07-446">すべてのプロジェクト間参照を読み取ります</span><span class="sxs-lookup"><span data-stu-id="f6e07-446">Read all project to project references</span></span>
1. <span data-ttu-id="f6e07-447">プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します</span><span class="sxs-lookup"><span data-stu-id="f6e07-447">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="f6e07-448">MSBuild データを NuGet.Build.Tasks.dll に渡す</span><span class="sxs-lookup"><span data-stu-id="f6e07-448">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="f6e07-449">restore を実行します</span><span class="sxs-lookup"><span data-stu-id="f6e07-449">Run restore</span></span>
1. <span data-ttu-id="f6e07-450">パッケージのダウンロード</span><span class="sxs-lookup"><span data-stu-id="f6e07-450">Download packages</span></span>
1. <span data-ttu-id="f6e07-451">アセット ファイル、ターゲット、およびプロパティを出力します</span><span class="sxs-lookup"><span data-stu-id="f6e07-451">Write assets file, targets, and props</span></span>

<span data-ttu-id="f6e07-452">ターゲットは、 `restore` PackageReference 形式を使用するプロジェクトに対して機能します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-452">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="f6e07-453">`MSBuild 16.5+` では、形式の [オプトインもサポート](#restoring-packagereference-and-packagesconfig-with-msbuild) されてい `packages.config` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-453">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="f6e07-454">ターゲットを `restore` ターゲットと組み合わせて [実行することはできません](#restoring-and-building-with-one-msbuild-command) `build` 。</span><span class="sxs-lookup"><span data-stu-id="f6e07-454">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="f6e07-455">restore のプロパティ</span><span class="sxs-lookup"><span data-stu-id="f6e07-455">Restore properties</span></span>

<span data-ttu-id="f6e07-456">追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-456">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="f6e07-457">また、`-p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="f6e07-457">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="f6e07-458">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f6e07-458">Property</span></span> | <span data-ttu-id="f6e07-459">説明</span><span class="sxs-lookup"><span data-stu-id="f6e07-459">Description</span></span> |
|--------|--------|
| <span data-ttu-id="f6e07-460">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="f6e07-460">RestoreSources</span></span> | <span data-ttu-id="f6e07-461">パッケージ ソースのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="f6e07-461">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="f6e07-462">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="f6e07-462">RestorePackagesPath</span></span> | <span data-ttu-id="f6e07-463">ユーザー パッケージ フォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-463">User packages folder path.</span></span> |
| <span data-ttu-id="f6e07-464">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="f6e07-464">RestoreDisableParallel</span></span> | <span data-ttu-id="f6e07-465">ダウンロード数を一度に 1 つまでに制限します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-465">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="f6e07-466">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="f6e07-466">RestoreConfigFile</span></span> | <span data-ttu-id="f6e07-467">適用する `Nuget.Config` ファイルのパス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-467">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="f6e07-468">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="f6e07-468">RestoreNoCache</span></span> | <span data-ttu-id="f6e07-469">True の場合、キャッシュされたパッケージの使用を回避します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-469">If true, avoids using cached packages.</span></span> <span data-ttu-id="f6e07-470">「 [グローバルパッケージとキャッシュフォルダーの管理」を](../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-470">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="f6e07-471">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="f6e07-471">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="f6e07-472">true の場合、失敗した、または不足しているパッケージ ソースを無視します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-472">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="f6e07-473">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="f6e07-473">RestoreFallbackFolders</span></span> | <span data-ttu-id="f6e07-474">フォールバックフォルダー。ユーザーパッケージフォルダーを使用する場合と同じ方法で使用されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-474">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="f6e07-475">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="f6e07-475">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="f6e07-476">復元中に使用する追加のソース。</span><span class="sxs-lookup"><span data-stu-id="f6e07-476">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="f6e07-477">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="f6e07-477">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="f6e07-478">復元中に使用する追加のフォールバックフォルダー。</span><span class="sxs-lookup"><span data-stu-id="f6e07-478">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="f6e07-479">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="f6e07-479">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="f6e07-480">で指定されたフォールバックフォルダーを除外します。 `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="f6e07-480">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="f6e07-481">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="f6e07-481">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="f6e07-482">`NuGet.Build.Tasks.dll` のパス。</span><span class="sxs-lookup"><span data-stu-id="f6e07-482">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="f6e07-483">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="f6e07-483">RestoreGraphProjectInput</span></span> | <span data-ttu-id="f6e07-484">復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-484">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="f6e07-485">Restoreentkipnon存在 Enttargets</span><span class="sxs-lookup"><span data-stu-id="f6e07-485">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="f6e07-486">MSBuild を使用してプロジェクトが収集されると、最適化を使用してプロジェクトを収集するかどうかが決定され `SkipNonexistentTargets` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-486">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="f6e07-487">設定しない場合、の既定値はに `true` なります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-487">When not set, defaults to `true`.</span></span> <span data-ttu-id="f6e07-488">その結果、プロジェクトのターゲットをインポートできない場合のフェールファースト動作になります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-488">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="f6e07-489">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="f6e07-489">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="f6e07-490">出力フォルダー。を既定 `BaseIntermediateOutputPath` として、フォルダーをにし `obj` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-490">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="f6e07-491">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="f6e07-491">RestoreForce</span></span> | <span data-ttu-id="f6e07-492">PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-492">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="f6e07-493">このフラグを指定することは、ファイルの削除に似てい `project.assets.json` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-493">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="f6e07-494">これは、http キャッシュをバイパスしません。</span><span class="sxs-lookup"><span data-stu-id="f6e07-494">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="f6e07-495">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="f6e07-495">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="f6e07-496">ロック ファイルの使用をオプトインします。</span><span class="sxs-lookup"><span data-stu-id="f6e07-496">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="f6e07-497">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="f6e07-497">RestoreLockedMode</span></span> | <span data-ttu-id="f6e07-498">ロックモードで復元を実行します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-498">Run restore in locked mode.</span></span> <span data-ttu-id="f6e07-499">これは、restore が依存関係を再評価しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-499">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="f6e07-500">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="f6e07-500">NuGetLockFilePath</span></span> | <span data-ttu-id="f6e07-501">ロックファイルのカスタムの場所。</span><span class="sxs-lookup"><span data-stu-id="f6e07-501">A custom location for the lock file.</span></span> <span data-ttu-id="f6e07-502">既定の場所はプロジェクトの横にあり、という名前が付けられ `packages.lock.json` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-502">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="f6e07-503">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="f6e07-503">RestoreForceEvaluate</span></span> | <span data-ttu-id="f6e07-504">復元によって依存関係が再計算され、警告なしでロックファイルが更新されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-504">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="f6e07-505">Restoreパッケージ構成</span><span class="sxs-lookup"><span data-stu-id="f6e07-505">RestorePackagesConfig</span></span> | <span data-ttu-id="f6e07-506">packages.config のプロジェクトを復元するオプトインスイッチ。でのみサポートさ `MSBuild -t:restore` れます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-506">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="f6e07-507">RestoreUseStaticGraphEvaluation</span><span class="sxs-lookup"><span data-stu-id="f6e07-507">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="f6e07-508">標準評価ではなく、静的なグラフの MSBuild 評価を使用するオプトインスイッチ。</span><span class="sxs-lookup"><span data-stu-id="f6e07-508">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="f6e07-509">静的グラフの評価は、大規模なリポジトリとソリューションで非常に高速な試験的な機能です。</span><span class="sxs-lookup"><span data-stu-id="f6e07-509">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="f6e07-510">例</span><span class="sxs-lookup"><span data-stu-id="f6e07-510">Examples</span></span>

<span data-ttu-id="f6e07-511">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="f6e07-511">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="f6e07-512">プロジェクト ファイル:</span><span class="sxs-lookup"><span data-stu-id="f6e07-512">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="f6e07-513">restore の出力</span><span class="sxs-lookup"><span data-stu-id="f6e07-513">Restore outputs</span></span>

<span data-ttu-id="f6e07-514">restore で、次のファイルがビルドの `obj` フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-514">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="f6e07-515">ファイル</span><span class="sxs-lookup"><span data-stu-id="f6e07-515">File</span></span> | <span data-ttu-id="f6e07-516">説明</span><span class="sxs-lookup"><span data-stu-id="f6e07-516">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="f6e07-517">すべてのパッケージ参照の依存関係グラフを含みます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-517">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="f6e07-518">パッケージに含まれる MSBuild プロパティへの参照</span><span class="sxs-lookup"><span data-stu-id="f6e07-518">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="f6e07-519">パッケージに含まれる MSBuild ターゲットへの参照</span><span class="sxs-lookup"><span data-stu-id="f6e07-519">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="f6e07-520">1つの MSBuild コマンドを使用した復元とビルド</span><span class="sxs-lookup"><span data-stu-id="f6e07-520">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="f6e07-521">NuGet では、MSBuild のターゲットとプロパティを表示するパッケージを復元できるため、異なるグローバルプロパティを使用して復元とビルドの評価が実行されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-521">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="f6e07-522">これは、次のような場合に予期しない動作が発生する可能性があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-522">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="f6e07-523">代わりに、推奨される方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="f6e07-523">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="f6e07-524">と同様に、同じロジックが他のターゲットにも適用され `build` ます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-524">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="f6e07-525">MSBuild を使用した PackageReference と packages.config の復元</span><span class="sxs-lookup"><span data-stu-id="f6e07-525">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="f6e07-526">MSBuild 16.5 + では、packages.config もサポートされて `msbuild -t:restore` います。</span><span class="sxs-lookup"><span data-stu-id="f6e07-526">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="f6e07-527">`packages.config` restore は、ではなく、でのみ使用でき `MSBuild 16.5+` ます。 `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="f6e07-527">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="f6e07-528">MSBuild の静的グラフの評価を使用した復元</span><span class="sxs-lookup"><span data-stu-id="f6e07-528">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="f6e07-529">MSBuild 16.6 + を使用すると、コマンドラインから静的グラフ評価を使用する実験的な機能が追加されました。これにより、大規模なリポジトリの復元時間が大幅に短縮されます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-529">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="f6e07-530">または、ディレクトリのプロパティを設定して有効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-530">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="f6e07-531">Visual Studio 2019. x および NuGet 5.x の場合、この機能は試験的でオプトインと見なされます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-531">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="f6e07-532">この機能が既定で有効になるタイミングの詳細については、 [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) に従ってください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-532">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="f6e07-533">静的なグラフの復元では、復元の msbuild 部分が変更されますが、プロジェクトの読み取りと評価は復元アルゴリズムではありません。</span><span class="sxs-lookup"><span data-stu-id="f6e07-533">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="f6e07-534">復元アルゴリズムは、すべての NuGet ツール (NuGet.exe、MSBuild.exe、dotnet.exe、および Visual Studio) で同じです。</span><span class="sxs-lookup"><span data-stu-id="f6e07-534">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="f6e07-535">ほとんどのシナリオでは、静的なグラフ復元は、現在の復元とは動作が異なる場合があります。また、宣言された特定の PackageReferences または ProjectReferences が見つからない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f6e07-535">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="f6e07-536">静的なグラフの復元に移行するときは、次の実行を検討してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-536">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="f6e07-537">NuGet は変更を報告し *ません* 。</span><span class="sxs-lookup"><span data-stu-id="f6e07-537">NuGet should *not* report any changes.</span></span> <span data-ttu-id="f6e07-538">不一致が発生した場合は、 [NuGet/Home](https://github.com/nuget/home/issues/new)で問題を報告してください。</span><span class="sxs-lookup"><span data-stu-id="f6e07-538">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="f6e07-539">復元グラフの 1 つのライブラリを置き換える</span><span class="sxs-lookup"><span data-stu-id="f6e07-539">Replacing one library from a restore graph</span></span>

<span data-ttu-id="f6e07-540">復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="f6e07-540">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="f6e07-541">まず、最上位の `PackageReference` ですべてのアセットを除外します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-541">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="f6e07-542">次に、DLL の適切なローカル コピーに独自の参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="f6e07-542">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
