---
title: NuGetターゲットとしてのパックと復元 MSBuild
description: NuGet パックと復元は、4.0 以降のターゲットとして直接使用でき MSBuild NuGet ます。
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 8ebf0329f9dc7af09a59f1498a934754842df365
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067311"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="2d94f-103">NuGetターゲットとしてのパックと復元 MSBuild</span><span class="sxs-lookup"><span data-stu-id="2d94f-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="2d94f-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="2d94f-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="2d94f-105">[PackageReference](../consume-packages/package-references-in-project-files.md)形式では、 NuGet 4.0 以降では、個別のファイルを使用するのではなく、プロジェクトファイル内に直接すべてのマニフェストメタデータを格納でき `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="2d94f-106">MSBuild15.1 + で NuGet は、次に示すように、とのターゲットを持つファーストクラスの市民でもあり MSBuild `pack` `restore` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="2d94f-107">これらのターゲットを使用すると、 NuGet 他のタスクやターゲットと同様にを操作でき MSBuild ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="2d94f-108">を使用したパッケージの作成手順については NuGet MSBuild 、「 [ NuGet を使用 MSBuild したパッケージの作成](../create-packages/creating-a-package-msbuild.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="2d94f-109">(の場合 NuGet )3.x 以前のバージョンでは、CLI を使用して、 [パック](../reference/cli-reference/cli-ref-pack.md) と [復元](../reference/cli-reference/cli-ref-restore.md) コマンドを使用して NuGet います)。</span><span class="sxs-lookup"><span data-stu-id="2d94f-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="2d94f-110">ターゲットのビルド順序</span><span class="sxs-lookup"><span data-stu-id="2d94f-110">Target build order</span></span>

<span data-ttu-id="2d94f-111">`pack`と `restore` はターゲットであるため MSBuild 、それらにアクセスしてワークフローを拡張できます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="2d94f-112">たとえば、パッキング後にパッケージをネットワーク共有にコピーするとします。</span><span class="sxs-lookup"><span data-stu-id="2d94f-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="2d94f-113">この場合、プロジェクト ファイルに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="2d94f-114">同様に、タスクを作成 MSBuild し、独自のターゲットを作成して、タスクのプロパティを使用することもでき NuGet MSBuild ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="2d94f-115">`$(OutputPath)` は相対であり、プロジェクトのルートからコマンドを実行していることを想定しています。</span><span class="sxs-lookup"><span data-stu-id="2d94f-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="2d94f-116">pack ターゲット</span><span class="sxs-lookup"><span data-stu-id="2d94f-116">pack target</span></span>

<span data-ttu-id="2d94f-117">形式を使用する .NET プロジェクトでは `PackageReference` 、を使用して、 `msbuild -t:pack` パッケージの作成に使用するプロジェクトファイルからの入力を描画し NuGet ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="2d94f-118">次の表では、 MSBuild 最初のノード内のプロジェクトファイルに追加できるプロパティについて説明し `<PropertyGroup>` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="2d94f-119">Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="2d94f-120">便宜上、テーブルは[ `.nuspec` ファイル](../reference/nuspec.md)内の同等のプロパティによって整理されています。</span><span class="sxs-lookup"><span data-stu-id="2d94f-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2d94f-121">`Owners` およびの `Summary` プロパティ `.nuspec` は、ではサポートされていません MSBuild 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="2d94f-122">属性/ nuspec 値</span><span class="sxs-lookup"><span data-stu-id="2d94f-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="2d94f-123">MSBuild プロパティ</span><span class="sxs-lookup"><span data-stu-id="2d94f-123">MSBuild Property</span></span> | <span data-ttu-id="2d94f-124">Default</span><span class="sxs-lookup"><span data-stu-id="2d94f-124">Default</span></span> | <span data-ttu-id="2d94f-125">メモ</span><span class="sxs-lookup"><span data-stu-id="2d94f-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="2d94f-126">MSBuild からの `$(AssemblyName)`</span><span class="sxs-lookup"><span data-stu-id="2d94f-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="2d94f-127">Version</span><span class="sxs-lookup"><span data-stu-id="2d94f-127">Version</span></span> | <span data-ttu-id="2d94f-128">これは semver と互換性があります `1.0.0` 。たとえば、、などです。 `1.0.0-beta``1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="2d94f-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="2d94f-129">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-129">empty</span></span> | <span data-ttu-id="2d94f-130">上書きの設定 `PackageVersion``PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="2d94f-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="2d94f-131">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-131">empty</span></span> | <span data-ttu-id="2d94f-132">`$(VersionSuffix)` から MSBuild 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="2d94f-133">上書きの設定 `PackageVersion``PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="2d94f-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="2d94f-134">現在のユーザーのユーザー名</span><span class="sxs-lookup"><span data-stu-id="2d94f-134">Username of the current user</span></span> | <span data-ttu-id="2d94f-135">Nuget.org のプロファイル名と一致するパッケージ作成者のセミコロン区切りのリスト。これらは nuget.org のギャラリーに表示され、 NuGet 同じ作成者によってパッケージを相互参照するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="2d94f-136">該当なし</span><span class="sxs-lookup"><span data-stu-id="2d94f-136">N/A</span></span> | <span data-ttu-id="2d94f-137">存在しない nuspec</span><span class="sxs-lookup"><span data-stu-id="2d94f-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="2d94f-138">`PackageId`</span><span class="sxs-lookup"><span data-stu-id="2d94f-138">The `PackageId`</span></span> | <span data-ttu-id="2d94f-139">人が読みやすいパッケージのタイトル。通常、nuget.org と、Visual Studio のパッケージ マネージャーの UI 画面で使用されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="2d94f-140">"パッケージの説明"</span><span class="sxs-lookup"><span data-stu-id="2d94f-140">"Package Description"</span></span> | <span data-ttu-id="2d94f-141">アセンブリの長い説明。</span><span class="sxs-lookup"><span data-stu-id="2d94f-141">A long description for the assembly.</span></span> <span data-ttu-id="2d94f-142">`PackageDescription` が指定されていない場合、このプロパティはパッケージの説明としても使用されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="2d94f-143">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-143">empty</span></span> | <span data-ttu-id="2d94f-144">パッケージの著作権の詳細。</span><span class="sxs-lookup"><span data-stu-id="2d94f-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="2d94f-145">クライアントがユーザーに対して、パッケージのインストール前にパッケージ ライセンスに同意することを必須にするかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="2d94f-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="2d94f-146">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-146">empty</span></span> | <span data-ttu-id="2d94f-147">`<license type="expression">` に相当します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="2d94f-148">「 [ライセンス式またはライセンスファイルのパッキング](#packing-a-license-expression-or-a-license-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="2d94f-149">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-149">empty</span></span> | <span data-ttu-id="2d94f-150">カスタムライセンスまたは SPDX 識別子が割り当てられていないライセンスを使用している場合の、パッケージ内のライセンスファイルへのパス。</span><span class="sxs-lookup"><span data-stu-id="2d94f-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="2d94f-151">参照されているライセンスファイルを明示的にパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="2d94f-152">`<license type="file">` に相当します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="2d94f-153">「 [ライセンス式またはライセンスファイルのパッキング](#packing-a-license-expression-or-a-license-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="2d94f-154">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-154">empty</span></span> | <span data-ttu-id="2d94f-155">`PackageLicenseUrl` は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="2d94f-156">代わりに、`PackageLicenseExpression` タグまたは `PackageLicenseFile` タグを使用してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="2d94f-157">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="2d94f-158">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-158">empty</span></span> | <span data-ttu-id="2d94f-159">パッケージ アイコンとして使用するパッケージ内の画像へのパス。</span><span class="sxs-lookup"><span data-stu-id="2d94f-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="2d94f-160">参照されているアイコンイメージファイルを明示的にパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="2d94f-161">詳細については、「[アイコンイメージファイル](#packing-an-icon-image-file)と[ `icon` メタデータ](./nuspec.md#icon)のパッキング」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="2d94f-162">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-162">empty</span></span> | <span data-ttu-id="2d94f-163">`PackageIconUrl` は、を優先するために非推奨とされ `PackageIcon` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="2d94f-164">ただし、最も高いダウンレベルエクスペリエンスを実現するには、に加えてを指定する必要があり `PackageIconUrl` `PackageIcon` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="2d94f-165">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-165">empty</span></span> | <span data-ttu-id="2d94f-166">参照されている readme ファイルを明示的にパックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="2d94f-167">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-167">empty</span></span> | <span data-ttu-id="2d94f-168">パッケージを指定するタグのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="2d94f-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="2d94f-169">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-169">empty</span></span> | <span data-ttu-id="2d94f-170">パッケージのリリース ノート。</span><span class="sxs-lookup"><span data-stu-id="2d94f-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="2d94f-171">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-171">empty</span></span> | <span data-ttu-id="2d94f-172">ソースコードの複製または取得に使用されるリポジトリの URL。</span><span class="sxs-lookup"><span data-stu-id="2d94f-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="2d94f-173">例: *https://github.com/ NuGet / NuGet 。クライアント. git*。</span><span class="sxs-lookup"><span data-stu-id="2d94f-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="2d94f-174">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-174">empty</span></span> | <span data-ttu-id="2d94f-175">リポジトリの種類。</span><span class="sxs-lookup"><span data-stu-id="2d94f-175">Repository type.</span></span> <span data-ttu-id="2d94f-176">例: `git` (既定値)、 `tfs` 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="2d94f-177">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-177">empty</span></span> | <span data-ttu-id="2d94f-178">リポジトリのブランチ情報 (オプション)。</span><span class="sxs-lookup"><span data-stu-id="2d94f-178">Optional repository branch information.</span></span> <span data-ttu-id="2d94f-179">このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="2d94f-180">例: *master* ( NuGet 4.7.0 +)。</span><span class="sxs-lookup"><span data-stu-id="2d94f-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="2d94f-181">空</span><span class="sxs-lookup"><span data-stu-id="2d94f-181">empty</span></span> | <span data-ttu-id="2d94f-182">任意のリポジトリ コミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="2d94f-183">このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="2d94f-184">例: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +)。</span><span class="sxs-lookup"><span data-stu-id="2d94f-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>CustomType1, 1.0.0.0;CustomType2</PackageType>` | | <span data-ttu-id="2d94f-185">パッケージの使用目的を示します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-185">Indicates the package's intended use.</span></span> <span data-ttu-id="2d94f-186">パッケージの種類は、パッケージ Id と同じ形式を使用し、によって区切られ `;` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-186">Package types use the same format as package IDs and are delimited by `;`.</span></span> <span data-ttu-id="2d94f-187">パッケージの種類は、と文字列を追加することによってバージョン管理でき `,` [`Version`](/dotnet/api/system.version) ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-187">Package types may be versioned by appending a `,` and a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="2d94f-188">「 [パッケージの NuGet 種類を設定する](../create-packages/set-package-type.md) (3.5.0 +)」を参照してください NuGet 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-188">See [Set a NuGet package type](../create-packages/set-package-type.md) (NuGet 3.5.0+).</span></span> |
| `Summary` | <span data-ttu-id="2d94f-189">サポートされていません</span><span class="sxs-lookup"><span data-stu-id="2d94f-189">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="2d94f-190">pack ターゲットの入力</span><span class="sxs-lookup"><span data-stu-id="2d94f-190">pack target inputs</span></span>

| <span data-ttu-id="2d94f-191">プロパティ</span><span class="sxs-lookup"><span data-stu-id="2d94f-191">Property</span></span> | <span data-ttu-id="2d94f-192">説明</span><span class="sxs-lookup"><span data-stu-id="2d94f-192">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="2d94f-193">プロジェクトをパックできるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="2d94f-193">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="2d94f-194">既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-194">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="2d94f-195">`true`生成されたパッケージからのパッケージの依存関係を抑制するには、に設定し NuGet ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-195">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="2d94f-196">結果のパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-196">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="2d94f-197">すべての形式の NuGet バージョン文字列を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-197">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="2d94f-198">既定値は `$(Version)` です。つまり、プロジェクトのプロパティ `Version` の値です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-198">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="2d94f-199">結果のパッケージの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-199">Specifies the name for the resulting package.</span></span> <span data-ttu-id="2d94f-200">指定しない場合、`pack` 操作の既定では、`AssemblyName` またはディレクトリ名をパッケージ名として使用します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-200">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="2d94f-201">UI 画面用のパッケージの長い説明。</span><span class="sxs-lookup"><span data-stu-id="2d94f-201">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="2d94f-202">Nuget.org のプロファイル名と一致するパッケージ作成者のセミコロン区切りのリスト。これらは nuget.org のギャラリーに表示され、 NuGet 同じ作成者によってパッケージを相互参照するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-202">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="2d94f-203">アセンブリの長い説明。</span><span class="sxs-lookup"><span data-stu-id="2d94f-203">A long description for the assembly.</span></span> <span data-ttu-id="2d94f-204">`PackageDescription` が指定されていない場合、このプロパティはパッケージの説明としても使用されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-204">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="2d94f-205">パッケージの著作権の詳細。</span><span class="sxs-lookup"><span data-stu-id="2d94f-205">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="2d94f-206">クライアントがユーザーに対して、パッケージのインストール前にパッケージ ライセンスに同意することを必須にするかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="2d94f-206">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="2d94f-207">既定値は、`false` です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-207">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="2d94f-208">開発専用の依存関係としてパッケージをマークするかどうかを指定するブール値。指定すると、そのパッケージは他のパッケージに依存関係として含まれなくなります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-208">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="2d94f-209">`PackageReference`( NuGet 4.8 以降) では、このフラグはコンパイル時のアセットがコンパイルから除外されることも意味します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-209">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="2d94f-210">詳しくは、「[DevelopmentDependency support for PackageReference (PackageReference に対する DevelopmentDependency のサポート)](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-210">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="2d94f-211">[Spdx ライセンス識別子](https://spdx.org/licenses/)または式 (など) `Apache-2.0` 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-211">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="2d94f-212">詳細については、「 [ライセンス式またはライセンスファイルのパッキング](#packing-a-license-expression-or-a-license-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-212">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="2d94f-213">カスタムライセンスまたは SPDX 識別子が割り当てられていないライセンスを使用している場合の、パッケージ内のライセンスファイルへのパス。</span><span class="sxs-lookup"><span data-stu-id="2d94f-213">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="2d94f-214">`PackageLicenseUrl` は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-214">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="2d94f-215">代わりに、`PackageLicenseExpression` タグまたは `PackageLicenseFile` タグを使用してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-215">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="2d94f-216">パッケージのルートに対して相対的なパッケージアイコンパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-216">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="2d94f-217">詳細については、「 [アイコンイメージファイルのパッキング](#packing-an-icon-image-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-217">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="2d94f-218">パッケージのリリース ノート。</span><span class="sxs-lookup"><span data-stu-id="2d94f-218">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="2d94f-219">パッケージの Readme。</span><span class="sxs-lookup"><span data-stu-id="2d94f-219">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="2d94f-220">パッケージを指定するタグのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="2d94f-220">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="2d94f-221">パックされたパッケージをドロップする出力パスを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-221">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="2d94f-222">既定値は `$(OutputPath)` です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-222">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="2d94f-223">このブール値は、プロジェクトをパックするときに、パッケージが追加のシンボル パッケージを作成するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-223">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="2d94f-224">シンボル パッケージの形式は、`SymbolPackageFormat` プロパティで制御します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-224">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="2d94f-225">詳細については、「 [IncludeSymbols](#includesymbols)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-225">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="2d94f-226">このブール値は、パック プロセスでソース パッケージを作成するかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-226">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="2d94f-227">ソース パッケージには、ライブラリのソース コードと PDB ファイルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-227">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="2d94f-228">ソース ファイルは、結果のパッケージ ファイルの `src/ProjectName` ディレクトリに置かれます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-228">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="2d94f-229">詳細については、「データの追加」を[参照してください。](#includesource)</span><span class="sxs-lookup"><span data-stu-id="2d94f-229">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="2d94f-230">すべての出力ファイルを *lib* フォルダーではなく *tools* フォルダーにコピーするかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-230">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="2d94f-231">詳細については、「 [IsTool](#istool)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-231">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="2d94f-232">ソースコードの複製または取得に使用されるリポジトリの URL。</span><span class="sxs-lookup"><span data-stu-id="2d94f-232">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="2d94f-233">例: *https://github.com/ NuGet / NuGet 。クライアント. git*。</span><span class="sxs-lookup"><span data-stu-id="2d94f-233">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="2d94f-234">リポジトリの種類。</span><span class="sxs-lookup"><span data-stu-id="2d94f-234">Repository type.</span></span> <span data-ttu-id="2d94f-235">例: `git` (既定値)、 `tfs` 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-235">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="2d94f-236">リポジトリのブランチ情報 (オプション)。</span><span class="sxs-lookup"><span data-stu-id="2d94f-236">Optional repository branch information.</span></span> <span data-ttu-id="2d94f-237">このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-237">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="2d94f-238">例: *master* ( NuGet 4.7.0 +)。</span><span class="sxs-lookup"><span data-stu-id="2d94f-238">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="2d94f-239">任意のリポジトリ コミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-239">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="2d94f-240">このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-240">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="2d94f-241">例: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +)。</span><span class="sxs-lookup"><span data-stu-id="2d94f-241">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="2d94f-242">シンボル パッケージの形式を指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-242">Specifies the format of the symbols package.</span></span> <span data-ttu-id="2d94f-243">"Symbols. nupkg" の場合、従来のシンボルパッケージは、Pdb、Dll、およびその他の出力ファイルを含む、 *シンボル* が含まれた拡張子が付いて作成されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-243">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="2d94f-244">"Snupkg" の場合、ポータブル Pdb を含む snupkg シンボルパッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-244">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="2d94f-245">既定値は "symbols. nupkg" です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-245">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="2d94f-246">`pack`パッケージのビルド後にパッケージ分析を実行しないことを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-246">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="2d94f-247">NuGetnuget.exe と Visual Studio パッケージマネージャーによって適用される、このパッケージをインストールできるクライアントの最小バージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-247">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="2d94f-248">このブール値は、ビルド出力アセンブリを *.nupkg* ファイルにパッケージ化するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-248">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="2d94f-249">このブール値は、の型を持つ項目 `Content` が、結果のパッケージに自動的に含まれるかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-249">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="2d94f-250">既定では、 `true`です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-250">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="2d94f-251">出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-251">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="2d94f-252">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-252">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="2d94f-253">詳細については、「 [出力アセンブリ](#output-assemblies)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-253">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="2d94f-254">が指定されていない場合に、すべてのコンテンツファイルの移動先となる既定の場所を指定し `PackagePath` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-254">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="2d94f-255">既定値は "content;contentFiles" です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-255">The default value is "content;contentFiles".</span></span> <span data-ttu-id="2d94f-256">詳細については、「[Including content in a package](#including-content-in-a-package)」 (パッケージにコンテンツを追加する) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-256">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="2d94f-257">*.nuspec* パッキングに使用されるファイルへの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="2d94f-257">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="2d94f-258">指定した場合、パッケージ化情報 **専用** に使用され、プロジェクト内の情報は使用されません。</span><span class="sxs-lookup"><span data-stu-id="2d94f-258">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="2d94f-259">詳細については、「を[使用した .nuspec パッキング](#packing-using-a-nuspec-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="2d94f-260">ファイルのベースパス *.nuspec* 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-260">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="2d94f-261">詳細については、「を[使用した .nuspec パッキング](#packing-using-a-nuspec-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-261">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="2d94f-262">キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="2d94f-262">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="2d94f-263">詳細については、「を[使用した .nuspec パッキング](#packing-using-a-nuspec-file)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-263">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="2d94f-264">pack のシナリオ</span><span class="sxs-lookup"><span data-stu-id="2d94f-264">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="2d94f-265">依存関係の抑制</span><span class="sxs-lookup"><span data-stu-id="2d94f-265">Suppressing dependencies</span></span>

<span data-ttu-id="2d94f-266">生成されたパッケージからパッケージの依存関係を抑制するに NuGet `SuppressDependenciesWhenPacking` は、をに設定し `true` ます。これにより、生成された nupkg ファイルからのすべての依存関係をスキップできます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-266">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="2d94f-267">`PackageIconUrl` は、プロパティを優先するために非推奨とされ [`PackageIcon`](#packageicon) ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-267">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="2d94f-268">NuGet5.3 および Visual Studio 2019 バージョン16.3 以降では、 `pack` パッケージメタデータでのみが指定されている場合、は[NU5048](./errors-and-warnings/nu5048.md) warning を発生させ `PackageIconUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-268">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="2d94f-269">まだサポートされていないクライアントおよびソースとの下位互換性を維持するに `PackageIcon` は、との両方を指定し `PackageIcon` `PackageIconUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-269">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="2d94f-270">Visual Studio で `PackageIcon` は、フォルダーベースのソースからのパッケージがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="2d94f-270">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="2d94f-271">アイコンイメージファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="2d94f-271">Packing an icon image file</span></span>

<span data-ttu-id="2d94f-272">アイコンイメージファイルをパッキングする場合は、プロパティを使用して、 `PackageIcon` パッケージのルートを基準としたアイコンファイルのパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-272">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="2d94f-273">また、ファイルがパッケージに含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-273">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="2d94f-274">イメージファイルのサイズは 1 MB に制限されています。</span><span class="sxs-lookup"><span data-stu-id="2d94f-274">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="2d94f-275">サポートされているファイル形式は、JPEG および PNG です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-275">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="2d94f-276">128x128 のイメージの解像度をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2d94f-276">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="2d94f-277">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-277">For example:</span></span>

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

<span data-ttu-id="2d94f-278">[パッケージアイコンのサンプル](https://github.com/NuGet/Samples/tree/main/PackageIconExample)です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-278">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="2d94f-279">同等のものについては、 nuspec [ nuspec アイコンの参照](nuspec.md#icon)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-279">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="2d94f-280">パッケージファイル</span><span class="sxs-lookup"><span data-stu-id="2d94f-280">PackageReadmeFile</span></span>

<span data-ttu-id="2d94f-281">***NuGet 5.10.0 preview 2**  /  **.net SDK 5.0.300** 以降でサポートされています*</span><span class="sxs-lookup"><span data-stu-id="2d94f-281">*Supported with **NuGet 5.10.0 preview 2** / **.NET SDK 5.0.300** and above*</span></span>

<span data-ttu-id="2d94f-282">Readme ファイルをパッキングする場合は、パッケージ `PackageReadmeFile` のルートに対して相対的なパッケージパスを指定するために、プロパティを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-282">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="2d94f-283">これに加えて、ファイルがパッケージに含まれていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-283">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="2d94f-284">サポートされるファイル形式には、Markdown (*md*) のみが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-284">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="2d94f-285">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-285">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="2d94f-286">同等のものについては nuspec 、 [ nuspec readme のリファレンス](nuspec.md#readme)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-286">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="2d94f-287">出力アセンブリ</span><span class="sxs-lookup"><span data-stu-id="2d94f-287">Output assemblies</span></span>

<span data-ttu-id="2d94f-288">`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="2d94f-288">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="2d94f-289">コピーされる出力ファイルは、ターゲットのによって提供される内容によって異なり MSBuild `BuiltOutputProjectGroup` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-289">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="2d94f-290">MSBuildプロジェクトファイルまたはコマンドラインでは、出力アセンブリの移動先を制御するために使用できるプロパティが2つあります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-290">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="2d94f-291">`IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。</span><span class="sxs-lookup"><span data-stu-id="2d94f-291">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="2d94f-292">`BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-292">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="2d94f-293">出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-293">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="2d94f-294">パッケージ参照</span><span class="sxs-lookup"><span data-stu-id="2d94f-294">Package references</span></span>

<span data-ttu-id="2d94f-295">「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-295">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="2d94f-296">プロジェクト間参照</span><span class="sxs-lookup"><span data-stu-id="2d94f-296">Project to project references</span></span>

<span data-ttu-id="2d94f-297">プロジェクト間参照は、既定ではパッケージ参照と見なされ NuGet ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-297">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="2d94f-298">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-298">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="2d94f-299">また、次のメタデータをプロジェクト参照に追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-299">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="2d94f-300">パッケージにコンテンツを含める</span><span class="sxs-lookup"><span data-stu-id="2d94f-300">Including content in a package</span></span>

<span data-ttu-id="2d94f-301">コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-301">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="2d94f-302">次のようなエントリでオーバーライドしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-302">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="2d94f-303">次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-303">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="2d94f-304">すべてのコンテンツを (およびの代わりに) 特定のルートフォルダーにのみコピーする場合は `content` 、 `contentFiles` プロパティを使用できます MSBuild `ContentTargetFolders` 。既定値は "content; contentfiles" ですが、他のフォルダー名に設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-304">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="2d94f-305">`ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-305">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="2d94f-306">`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-306">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="2d94f-307">空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-307">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="2d94f-308">たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-308">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="2d94f-309">プロパティもあり MSBuild `$(IncludeContentInPack)` ます。既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-309">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="2d94f-310">これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="2d94f-310">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="2d94f-311">上記のいずれかの項目に設定できるその他のパック固有のメタデータには、 ```<PackageCopyToOutput>``` ```<PackageFlatten>``` 出力のエントリのセットと値が含まれ ```CopyToOutput``` ```Flatten``` ```contentFiles``` nuspec ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-311">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="2d94f-312">コンテンツ項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-312">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="2d94f-313">glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-313">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="2d94f-314">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="2d94f-314">IncludeSymbols</span></span>

<span data-ttu-id="2d94f-315">`MSBuild -t:pack -p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-315">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="2d94f-316">`IncludeSymbols=true` を設定すると、通常のパッケージ *と* シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-316">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="2d94f-317">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="2d94f-317">IncludeSource</span></span>

<span data-ttu-id="2d94f-318">これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。</span><span class="sxs-lookup"><span data-stu-id="2d94f-318">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="2d94f-319">種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-319">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="2d94f-320">`TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-320">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="2d94f-321">種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-321">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="2d94f-322">ライセンス式またはライセンスファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="2d94f-322">Packing a license expression or a license file</span></span>

<span data-ttu-id="2d94f-323">ライセンス式を使用する場合は、プロパティを使用し `PackageLicenseExpression` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-323">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="2d94f-324">サンプルについては、「 [ライセンス式のサンプル](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-324">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="2d94f-325">組織で受け入れられるライセンス式とライセンスの詳細については NuGet 、「 [ライセンスメタデータ](nuspec.md#license)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-325">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="2d94f-326">ライセンスファイルをパッキングする場合は、パッケージ `PackageLicenseFile` のルートに対して相対的なパッケージパスをプロパティを使用して指定します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-326">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="2d94f-327">また、ファイルがパッケージに含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-327">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="2d94f-328">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-328">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="2d94f-329">サンプルについては、「 [ライセンスファイルのサンプル](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-329">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="2d94f-330">、、およびのいずれか1つだけを `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` 同時に指定できます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-330">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="2d94f-331">拡張子のないファイルのパッキング</span><span class="sxs-lookup"><span data-stu-id="2d94f-331">Packing a file without an extension</span></span>

<span data-ttu-id="2d94f-332">ライセンスファイルをパッキングする場合など、一部のシナリオでは、拡張子のないファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-332">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="2d94f-333">履歴上の理由により、 NuGet  &  MSBuild パスをディレクトリとして拡張せずに扱います。</span><span class="sxs-lookup"><span data-stu-id="2d94f-333">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="2d94f-334">[拡張機能サンプルのないファイル](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/)。</span><span class="sxs-lookup"><span data-stu-id="2d94f-334">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="2d94f-335">IsTool</span><span class="sxs-lookup"><span data-stu-id="2d94f-335">IsTool</span></span>

<span data-ttu-id="2d94f-336">`MSBuild -t:pack -p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-336">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="2d94f-337">これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-337">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="2d94f-338">ファイルを使用したパッキング `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="2d94f-338">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="2d94f-339">通常はファイル内の [すべてのプロパティ](../reference/msbuild-targets.md#pack-target) をプロジェクトファイルに含めることをお勧めし `.nuspec` ますが、プロジェクトを `.nuspec` パックするためにファイルを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-339">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="2d94f-340">を使用する SDK スタイル以外のプロジェクトでは `PackageReference` 、をインポートして、 `NuGet.Build.Tasks.Pack.targets` パックタスクを実行できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-340">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="2d94f-341">ただし、ファイルをパックする前に、プロジェクトを復元する必要があり nuspec ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-341">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="2d94f-342">(SDK スタイルのプロジェクトには、既定でパックターゲットが含まれています)。</span><span class="sxs-lookup"><span data-stu-id="2d94f-342">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="2d94f-343">プロジェクトファイルのターゲットフレームワークは無関係であり、をパッキングするときには使用されません nuspec 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-343">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="2d94f-344">次の3つの MSBuild プロパティは、を使用したパッキングに関連してい `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-344">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="2d94f-345">`NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。</span><span class="sxs-lookup"><span data-stu-id="2d94f-345">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="2d94f-346">`NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="2d94f-346">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="2d94f-347">コマンドラインの解析方法によっては、次のように MSBuild 複数のプロパティを指定する必要があり `-p:NuspecProperties="key1=value1;key2=value2"` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-347">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="2d94f-348">`NuspecBasePath`: `.nuspec` ファイルのベース パス。</span><span class="sxs-lookup"><span data-stu-id="2d94f-348">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="2d94f-349">`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-349">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="2d94f-350">MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-350">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="2d94f-351">nuspecdotnet.exe または msbuild を使用してをパッキングすると、既定でプロジェクトがビルドされることにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-351">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="2d94f-352">これは、プロパティを dotnet.exe に渡すことによって回避できます。これは、プロジェクトファイルの ```--no-build``` 設定 ```<NoBuild>true</NoBuild> ``` と共に、プロジェクトファイル内の設定に相当し ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-352">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="2d94f-353">ファイルをパックする .csproj ファイルの例を次に示し *ます。* nuspec</span><span class="sxs-lookup"><span data-stu-id="2d94f-353">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="2d94f-354">カスタマイズされたパッケージを作成するための高度な拡張ポイント</span><span class="sxs-lookup"><span data-stu-id="2d94f-354">Advanced extension points to create customized package</span></span>

<span data-ttu-id="2d94f-355">ターゲットには、 `pack` ターゲットフレームワーク固有の内部ビルドで実行される2つの拡張ポイントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="2d94f-355">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="2d94f-356">拡張ポイントは、ターゲットフレームワーク固有のコンテンツとアセンブリをパッケージに含めることをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="2d94f-356">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="2d94f-357">`TargetsForTfmSpecificBuildOutput` ターゲット: フォルダー内のファイル、 `lib` またはを使用して指定されたフォルダー内のファイルに使用し `BuildOutputTargetFolder` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-357">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="2d94f-358">`TargetsForTfmSpecificContentInPackage` ターゲット: の外部のファイルに対して使用し `BuildOutputTargetFolder` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-358">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="2d94f-359">カスタムターゲットを作成し、プロパティの値として指定し `$(TargetsForTfmSpecificBuildOutput)` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-359">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="2d94f-360">(既定では lib) に移動する必要があるファイルの場合、 `BuildOutputTargetFolder` ターゲットはこれらのファイルを ItemGroup に書き込み、 `BuildOutputInPackage` 次の2つのメタデータ値を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-360">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="2d94f-361">`FinalOutputPath`: ファイルの絶対パス。指定されていない場合は、ソースパスの評価に Id が使用されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-361">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="2d94f-362">`TargetPath`: (省略可能) ファイルが内のサブフォルダーに入る必要があるときに設定し `lib\<TargetFramework>` ます。これは、それぞれのカルチャフォルダーの下にあるサテライトアセンブリのようになります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-362">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="2d94f-363">既定値は、ファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-363">Defaults to the name of the file.</span></span>

<span data-ttu-id="2d94f-364">例:</span><span class="sxs-lookup"><span data-stu-id="2d94f-364">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="2d94f-365">カスタムターゲットを作成し、プロパティの値として指定し `$(TargetsForTfmSpecificContentInPackage)` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-365">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="2d94f-366">パッケージに含めるファイルについては、ターゲットはこれらのファイルを ItemGroup に書き込み、 `TfmSpecificPackageFile` 次のオプションのメタデータを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-366">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="2d94f-367">`PackagePath`: パッケージでファイルを出力するパス。</span><span class="sxs-lookup"><span data-stu-id="2d94f-367">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="2d94f-368">NuGet 複数のファイルが同じパッケージパスに追加された場合に、警告を発行します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-368">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="2d94f-369">`BuildAction`: ファイルに割り当てるビルドアクション。パッケージパスがフォルダー内にある場合にのみ必要です `contentFiles` 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-369">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="2d94f-370">既定値は "None" です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-370">Defaults to "None".</span></span>

<span data-ttu-id="2d94f-371">例:</span><span class="sxs-lookup"><span data-stu-id="2d94f-371">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="2d94f-372">restore ターゲット</span><span class="sxs-lookup"><span data-stu-id="2d94f-372">restore target</span></span>

<span data-ttu-id="2d94f-373">`MSBuild -t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-373">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="2d94f-374">すべてのプロジェクト間参照を読み取ります</span><span class="sxs-lookup"><span data-stu-id="2d94f-374">Read all project to project references</span></span>
1. <span data-ttu-id="2d94f-375">プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します</span><span class="sxs-lookup"><span data-stu-id="2d94f-375">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="2d94f-376">MSBuild.Build.Tasks.dll にデータを渡す NuGet</span><span class="sxs-lookup"><span data-stu-id="2d94f-376">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="2d94f-377">restore を実行します</span><span class="sxs-lookup"><span data-stu-id="2d94f-377">Run restore</span></span>
1. <span data-ttu-id="2d94f-378">パッケージのダウンロード</span><span class="sxs-lookup"><span data-stu-id="2d94f-378">Download packages</span></span>
1. <span data-ttu-id="2d94f-379">アセット ファイル、ターゲット、およびプロパティを出力します</span><span class="sxs-lookup"><span data-stu-id="2d94f-379">Write assets file, targets, and props</span></span>

<span data-ttu-id="2d94f-380">ターゲットは、 `restore` PackageReference 形式を使用するプロジェクトに対して機能します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-380">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="2d94f-381">`MSBuild 16.5+` では、形式の [オプトインもサポート](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) されてい `packages.config` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-381">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="2d94f-382">ターゲットを `restore` ターゲットと組み合わせて [実行することはできません](#restoring-and-building-with-one-msbuild-command) `build` 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-382">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="2d94f-383">restore のプロパティ</span><span class="sxs-lookup"><span data-stu-id="2d94f-383">Restore properties</span></span>

<span data-ttu-id="2d94f-384">その他の復元設定は MSBuild 、プロジェクトファイルのプロパティから取得できます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-384">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="2d94f-385">また、`-p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="2d94f-385">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="2d94f-386">プロパティ</span><span class="sxs-lookup"><span data-stu-id="2d94f-386">Property</span></span> | <span data-ttu-id="2d94f-387">説明</span><span class="sxs-lookup"><span data-stu-id="2d94f-387">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="2d94f-388">パッケージ ソースのセミコロン区切りの一覧。</span><span class="sxs-lookup"><span data-stu-id="2d94f-388">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="2d94f-389">ユーザー パッケージ フォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="2d94f-389">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="2d94f-390">ダウンロード数を一度に 1 つまでに制限します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-390">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="2d94f-391">適用する `Nuget.Config` ファイルのパス。</span><span class="sxs-lookup"><span data-stu-id="2d94f-391">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="2d94f-392">True の場合、キャッシュされたパッケージの使用を回避します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-392">If true, avoids using cached packages.</span></span> <span data-ttu-id="2d94f-393">「 [グローバルパッケージとキャッシュフォルダーの管理」を](../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-393">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="2d94f-394">true の場合、失敗した、または不足しているパッケージ ソースを無視します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-394">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="2d94f-395">フォールバックフォルダー。ユーザーパッケージフォルダーを使用する場合と同じ方法で使用されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-395">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="2d94f-396">復元中に使用する追加のソース。</span><span class="sxs-lookup"><span data-stu-id="2d94f-396">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="2d94f-397">復元中に使用する追加のフォールバックフォルダー。</span><span class="sxs-lookup"><span data-stu-id="2d94f-397">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="2d94f-398">で指定されたフォールバックフォルダーを除外します。 `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="2d94f-398">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="2d94f-399">`NuGet.Build.Tasks.dll` のパス。</span><span class="sxs-lookup"><span data-stu-id="2d94f-399">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="2d94f-400">復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-400">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="2d94f-401">プロジェクトをで収集すると、そのプロジェクトが MSBuild 最適化を使用して収集されるかどうかが決まり `SkipNonexistentTargets` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-401">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="2d94f-402">設定しない場合、の既定値はに `true` なります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-402">When not set, defaults to `true`.</span></span> <span data-ttu-id="2d94f-403">その結果、プロジェクトのターゲットをインポートできない場合のフェールファースト動作になります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-403">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="2d94f-404">出力フォルダー。を既定 `BaseIntermediateOutputPath` として、フォルダーをにし `obj` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-404">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="2d94f-405">PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-405">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="2d94f-406">このフラグを指定することは、ファイルの削除に似てい `project.assets.json` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-406">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="2d94f-407">これは、http キャッシュをバイパスしません。</span><span class="sxs-lookup"><span data-stu-id="2d94f-407">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="2d94f-408">ロック ファイルの使用をオプトインします。</span><span class="sxs-lookup"><span data-stu-id="2d94f-408">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="2d94f-409">ロックモードで復元を実行します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-409">Run restore in locked mode.</span></span> <span data-ttu-id="2d94f-410">これは、restore が依存関係を再評価しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-410">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="2d94f-411">ロックファイルのカスタムの場所。</span><span class="sxs-lookup"><span data-stu-id="2d94f-411">A custom location for the lock file.</span></span> <span data-ttu-id="2d94f-412">既定の場所はプロジェクトの横にあり、という名前が付けられ `packages.lock.json` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-412">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="2d94f-413">復元によって依存関係が再計算され、警告なしでロックファイルが更新されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-413">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="2d94f-414">packages.config のプロジェクトを復元するオプトインスイッチ。でのみサポートさ `MSBuild -t:restore` れます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-414">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="2d94f-415">標準評価ではなく、静的なグラフの評価を使用するオプトインスイッチ MSBuild 。</span><span class="sxs-lookup"><span data-stu-id="2d94f-415">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="2d94f-416">静的グラフの評価は、大規模なリポジトリとソリューションで非常に高速な試験的な機能です。</span><span class="sxs-lookup"><span data-stu-id="2d94f-416">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="2d94f-417">例</span><span class="sxs-lookup"><span data-stu-id="2d94f-417">Examples</span></span>

<span data-ttu-id="2d94f-418">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="2d94f-418">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="2d94f-419">プロジェクト ファイル:</span><span class="sxs-lookup"><span data-stu-id="2d94f-419">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="2d94f-420">restore の出力</span><span class="sxs-lookup"><span data-stu-id="2d94f-420">Restore outputs</span></span>

<span data-ttu-id="2d94f-421">restore で、次のファイルがビルドの `obj` フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-421">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="2d94f-422">ファイル</span><span class="sxs-lookup"><span data-stu-id="2d94f-422">File</span></span> | <span data-ttu-id="2d94f-423">説明</span><span class="sxs-lookup"><span data-stu-id="2d94f-423">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="2d94f-424">すべてのパッケージ参照の依存関係グラフを含みます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-424">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="2d94f-425">MSBuildパッケージに含まれる props への参照</span><span class="sxs-lookup"><span data-stu-id="2d94f-425">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="2d94f-426">MSBuildパッケージに含まれているターゲットへの参照</span><span class="sxs-lookup"><span data-stu-id="2d94f-426">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="2d94f-427">1つのコマンドを使用した復元とビルド MSBuild</span><span class="sxs-lookup"><span data-stu-id="2d94f-427">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="2d94f-428">NuGetターゲットと props をダウンするパッケージを復元できるという事実により MSBuild 、復元とビルドの評価は異なるグローバルプロパティを使用して実行されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-428">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="2d94f-429">これは、次のような場合に予期しない動作が発生する可能性があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-429">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="2d94f-430">代わりに、推奨される方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2d94f-430">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="2d94f-431">と同様に、同じロジックが他のターゲットにも適用され `build` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-431">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="2d94f-432">を使用した PackageReference および packages.config プロジェクトの復元 MSBuild</span><span class="sxs-lookup"><span data-stu-id="2d94f-432">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="2d94f-433">MSBuild16.5 + では、の packages.config もサポートされてい `msbuild -t:restore` ます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-433">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="2d94f-434">`packages.config` restore は、ではなく、でのみ使用でき `MSBuild 16.5+` ます。 `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="2d94f-434">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="2d94f-435">静的グラフの評価を使用した復元 MSBuild</span><span class="sxs-lookup"><span data-stu-id="2d94f-435">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="2d94f-436">MSBuild16.6 + で NuGet は、コマンドラインからの静的なグラフ評価を使用する実験的な機能が追加されました。これにより、大規模なリポジトリの復元時間が大幅に短縮されます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-436">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="2d94f-437">または、ディレクトリのプロパティを設定して有効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-437">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="2d94f-438">Visual Studio 2019. x と5.x の NuGet 場合、この機能は試験的でオプトインと見なされます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-438">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="2d94f-439">この機能が既定で有効になるタイミングの詳細については、「 [ NuGet /home # 9803](https://github.com/NuGet/Home/issues/9803) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-439">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="2d94f-440">静的なグラフの復元では、復元の msbuild 部分が変更されますが、プロジェクトの読み取りと評価は復元アルゴリズムではありません。</span><span class="sxs-lookup"><span data-stu-id="2d94f-440">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="2d94f-441">復元アルゴリズムは、すべての NuGet ツール ( NuGet .exe、 MSBuild .exe、dotnet.exe、および Visual Studio) で同じです。</span><span class="sxs-lookup"><span data-stu-id="2d94f-441">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="2d94f-442">ほとんどのシナリオでは、静的なグラフ復元は、現在の復元とは動作が異なる場合があります。また、宣言された特定の PackageReferences または ProjectReferences が見つからない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2d94f-442">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="2d94f-443">静的なグラフの復元に移行するときは、次の実行を検討してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-443">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="2d94f-444">NuGet 変更を報告 *しない* でください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-444">NuGet should *not* report any changes.</span></span> <span data-ttu-id="2d94f-445">不一致が発生した場合は、 [ NuGet /home](https://github.com/nuget/home/issues/new)で問題を報告してください。</span><span class="sxs-lookup"><span data-stu-id="2d94f-445">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="2d94f-446">復元グラフの 1 つのライブラリを置き換える</span><span class="sxs-lookup"><span data-stu-id="2d94f-446">Replacing one library from a restore graph</span></span>

<span data-ttu-id="2d94f-447">復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="2d94f-447">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="2d94f-448">まず、最上位の `PackageReference` ですべてのアセットを除外します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-448">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="2d94f-449">次に、DLL の適切なローカル コピーに独自の参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="2d94f-449">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
