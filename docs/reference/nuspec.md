---
title: NuGet の .nuspec ファイル リファレンス
description: .nuspec ファイルには、パッケージを作成するとき、およびパッケージのコンシューマーに情報を提供するために使われる、パッケージのメタデータが含まれています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6d190d9fdb26d76fa8e46b7d283c1857cfab26e9
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508037"
---
# <a name="nuspec-reference"></a><span data-ttu-id="4860f-103">.nuspec リファレンス</span><span class="sxs-lookup"><span data-stu-id="4860f-103">.nuspec reference</span></span>

<span data-ttu-id="4860f-104">`.nuspec` ファイルは、パッケージのメタデータが含まれている XML マニフェストです。</span><span class="sxs-lookup"><span data-stu-id="4860f-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="4860f-105">このマニフェストは、パッケージを作成するためと、コンシューマーに情報を提供するための、両方に使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="4860f-106">パッケージにはマニフェストが常に含まれています。</span><span class="sxs-lookup"><span data-stu-id="4860f-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="4860f-107">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="4860f-107">In this topic:</span></span>

- [<span data-ttu-id="4860f-108">一般的な形式とスキーマ</span><span class="sxs-lookup"><span data-stu-id="4860f-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="4860f-109">[置換トークン](#replacement-tokens) (Visual Studio プロジェクトで使われるとき)</span><span class="sxs-lookup"><span data-stu-id="4860f-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="4860f-110">依存関係</span><span class="sxs-lookup"><span data-stu-id="4860f-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="4860f-111">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="4860f-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="4860f-112">フレームワーク アセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="4860f-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="4860f-113">アセンブリ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="4860f-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="4860f-114">コンテンツ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="4860f-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="4860f-115">Nuspec ファイルの例</span><span class="sxs-lookup"><span data-stu-id="4860f-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="4860f-116">一般的な形式とスキーマ</span><span class="sxs-lookup"><span data-stu-id="4860f-116">General form and schema</span></span>

<span data-ttu-id="4860f-117">最新の `nuspec.xsd` スキーマ ファイルは、[NuGet GitHub リポジトリ](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)にあります。</span><span class="sxs-lookup"><span data-stu-id="4860f-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="4860f-118">このスキーマでの `.nuspec` ファイルの一般的な形式は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="4860f-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="4860f-119">スキーマの視覚的な表現をはっきり表示したい場合は、Visual Studio のデザイン モードでスキーマ ファイルを開き、**[XML スキーマ エクスプローラー]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4860f-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="4860f-120">または、コードとしてファイルを開き、エディター内を右クリックして、**[XML スキーマ エクスプローラーで表示]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="4860f-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="4860f-121">どちらの方法でも次のように表示されます (ほとんどを展開した場合)。</span><span class="sxs-lookup"><span data-stu-id="4860f-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio のスキーマ エクスプローラーで開いた nuspec.xsd](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="4860f-123">メタデータの属性</span><span class="sxs-lookup"><span data-stu-id="4860f-123">Metadata attributes</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="4860f-124">メタデータの必須要素</span><span class="sxs-lookup"><span data-stu-id="4860f-124">Required metadata elements</span></span>

<span data-ttu-id="4860f-125">以下の要素はパッケージの最低要件であり、[メタデータの省略可能な要素](#optional-metadata-elements)を追加してパッケージに関する開発者の全体的なエクスペリエンスを向上させることを検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4860f-125">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="4860f-126">これらの要素は、`<metadata>` 要素内で指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4860f-126">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="4860f-127">要素</span><span class="sxs-lookup"><span data-stu-id="4860f-127">Element</span></span> | <span data-ttu-id="4860f-128">説明</span><span class="sxs-lookup"><span data-stu-id="4860f-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4860f-129">**ID**</span><span class="sxs-lookup"><span data-stu-id="4860f-129">**id**</span></span> | <span data-ttu-id="4860f-130">パッケージの識別子。大文字と小文字が区別されます。nuget.org 全体で、またはパッケージが存在するギャラリー全体で、一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="4860f-130">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="4860f-131">ID は、スペースまたは URL で無効な文字を含んでいてはならず、一般に .NET 名前空間の規則に従います。</span><span class="sxs-lookup"><span data-stu-id="4860f-131">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="4860f-132">ガイダンスについては、[一意のパッケージ識別子の選択](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-132">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="4860f-133">**version**</span><span class="sxs-lookup"><span data-stu-id="4860f-133">**version**</span></span> | <span data-ttu-id="4860f-134">パッケージのバージョン。*major.minor.patch* のパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="4860f-134">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="4860f-135">「[Package versioning](../reference/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) で説明されているように、バージョン番号にはプレリリースのサフィックスを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="4860f-135">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="4860f-136">**description**</span><span class="sxs-lookup"><span data-stu-id="4860f-136">**description**</span></span> | <span data-ttu-id="4860f-137">UI 画面用のパッケージの長い説明。</span><span class="sxs-lookup"><span data-stu-id="4860f-137">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="4860f-138">**authors**</span><span class="sxs-lookup"><span data-stu-id="4860f-138">**authors**</span></span> | <span data-ttu-id="4860f-139">パッケージ作成者の一覧。コンマで区切られています。nuget.org のプロファイル名と一致します。これらは nuget.org の NuGet ギャラリーに表示され、同じ作成者によるパッケージの相互参照に使用されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-139">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="4860f-140">メタデータの省略可能な要素</span><span class="sxs-lookup"><span data-stu-id="4860f-140">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="4860f-141">タイトル</span><span class="sxs-lookup"><span data-stu-id="4860f-141">title</span></span>
<span data-ttu-id="4860f-142">人が読みやすいパッケージのタイトル。通常、nuget.org と、Visual Studio のパッケージ マネージャーの UI 画面で使用されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-142">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="4860f-143">指定しないと、パッケージ ID が使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-143">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="4860f-144">owners</span><span class="sxs-lookup"><span data-stu-id="4860f-144">owners</span></span>
<span data-ttu-id="4860f-145">コンマで区切って指定したパッケージ作成者の一覧。nuget.org でのプロファイル名です。多くの場合は `authors` と同じ一覧であり、nuget.org にパッケージをアップロードするときは無視されます。「[nuget.org でパッケージ所有者を管理する](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-145">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="4860f-146">projectUrl</span><span class="sxs-lookup"><span data-stu-id="4860f-146">projectUrl</span></span>
<span data-ttu-id="4860f-147">パッケージのホーム ページの URL。多くの場合、UI 画面と nuget.org に表示されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-147">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="4860f-148">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="4860f-148">licenseUrl</span></span>
<span data-ttu-id="4860f-149">パッケージのライセンスの URL。通常、UI 画面および nuget.org に表示されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-149">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="iconurl"></a><span data-ttu-id="4860f-150">iconUrl</span><span class="sxs-lookup"><span data-stu-id="4860f-150">iconUrl</span></span>
<span data-ttu-id="4860f-151">UI 表示でパッケージのアイコンとして使われる、背景が透明な 64 x 64 の画像の URL。</span><span class="sxs-lookup"><span data-stu-id="4860f-151">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="4860f-152">この要素の値は、"*画像を直接示す URL*" であり、画像を含む Web ページの URL ではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4860f-152">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="4860f-153">たとえば、GitHub からのイメージを使用する URL などの生ファイルを使用して <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>します。</span><span class="sxs-lookup"><span data-stu-id="4860f-153">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="4860f-154">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="4860f-154">requireLicenseAcceptance</span></span>
<span data-ttu-id="4860f-155">パッケージをインストールする前にクライアントがユーザーに対してパッケージのライセンスへの同意を求めるプロンプトを表示する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="4860f-155">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="4860f-156">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="4860f-156">developmentDependency</span></span>
<span data-ttu-id="4860f-157">*(2.8 以降)* 開発専用の依存関係としてパッケージをマークするかどうかを指定するブール値。指定すると、そのパッケージは他のパッケージに依存関係として含まれなくなります。</span><span class="sxs-lookup"><span data-stu-id="4860f-157">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span>
#### <a name="summary"></a><span data-ttu-id="4860f-158">概要</span><span class="sxs-lookup"><span data-stu-id="4860f-158">summary</span></span>
<span data-ttu-id="4860f-159">UI 画面用のパッケージの短い説明。</span><span class="sxs-lookup"><span data-stu-id="4860f-159">A short description of the package for UI display.</span></span> <span data-ttu-id="4860f-160">省略すると、`description` を切り詰めたバージョンが使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-160">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="4860f-161">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="4860f-161">releaseNotes</span></span>
<span data-ttu-id="4860f-162">*(1.5 以降)* このリリースのパッケージで行われた変更の説明。Visual Studio パッケージ マネージャーの **[更新]** タブなどの UI で、パッケージの説明の代わりによく使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-162">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="4860f-163">著作権</span><span class="sxs-lookup"><span data-stu-id="4860f-163">copyright</span></span>
<span data-ttu-id="4860f-164">*(1.5 以降)* パッケージの著作権の詳細。</span><span class="sxs-lookup"><span data-stu-id="4860f-164">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="4860f-165">language</span><span class="sxs-lookup"><span data-stu-id="4860f-165">language</span></span>
<span data-ttu-id="4860f-166">パッケージのロケール ID。</span><span class="sxs-lookup"><span data-stu-id="4860f-166">The locale ID for the package.</span></span> <span data-ttu-id="4860f-167">「[ローカライズされたパッケージの作成](../create-packages/creating-localized-packages.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-167">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="4860f-168">タグ</span><span class="sxs-lookup"><span data-stu-id="4860f-168">tags</span></span>
<span data-ttu-id="4860f-169">パッケージについて説明し、検索やフィルターでパッケージを見つけやすくするタグやキーワードを、スペースで区切って列記したリスト。</span><span class="sxs-lookup"><span data-stu-id="4860f-169">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="4860f-170">処理できます。</span><span class="sxs-lookup"><span data-stu-id="4860f-170">serviceable</span></span> 
<span data-ttu-id="4860f-171">*(3.3 以降)* NuGet 内部でのみ使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-171">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="4860f-172">リポジトリ</span><span class="sxs-lookup"><span data-stu-id="4860f-172">repository</span></span>
<span data-ttu-id="4860f-173">4 つの省略可能な属性で構成される、リポジトリ メタデータ:*型*と*url* *(4.0 以降)*、および*ブランチ*と*コミット* *(4.6 以降)* します。</span><span class="sxs-lookup"><span data-stu-id="4860f-173">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="4860f-174">これらの属性を取得する可能性がありますが、組み込まれているリポジトリへの .nupkg をマップできます。 個々 の分岐またはパッケージの構築コミットとして説明されています。</span><span class="sxs-lookup"><span data-stu-id="4860f-174">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="4860f-175">バージョン管理のソフトウェアを直接呼び出すことができる公開されている url があります。</span><span class="sxs-lookup"><span data-stu-id="4860f-175">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="4860f-176">これは、コンピューターのように html ページをことがいません。</span><span class="sxs-lookup"><span data-stu-id="4860f-176">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="4860f-177">プロジェクトのページへのリンクを使用して、`projectUrl`フィールドに、代わりにします |。</span><span class="sxs-lookup"><span data-stu-id="4860f-177">For linking to project page, use the `projectUrl` field, instead.|</span></span>
#### <a name="minclientversion"></a><span data-ttu-id="4860f-178">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="4860f-178">minClientVersion</span></span>
<span data-ttu-id="4860f-179">nuget.exe および Visual Studio パッケージ マネージャーで強制する、このパッケージをインストールできる NuGet クライアントの最小バージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-179">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="4860f-180">これは、NuGet クライアントの特定のバージョンで追加された `.nuspec` ファイルの特定の機能にパッケージが依存しているときに、常に使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-180">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="4860f-181">たとえば、`developmentDependency` 属性を使っているパッケージでは、`minClientVersion` に "2.8" を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4860f-181">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="4860f-182">同様に、`contentFiles` 要素 (次のセクションを参照) を使っているパッケージでは、`minClientVersion` を "3.3" に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4860f-182">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="4860f-183">また、バージョン 2.5 より前の NuGet クライアントはこのフラグを認識しないので、`minClientVersion` の値が何であっても、"*常に*" パッケージをインストールしないことにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="4860f-183">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="4860f-184">コレクション要素</span><span class="sxs-lookup"><span data-stu-id="4860f-184">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="4860f-185">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="4860f-185">packageTypes</span></span>
<span data-ttu-id="4860f-186">*(3.5 以降)* 従来の依存関係パッケージ以外の場合に、パッケージの種類を指定する 0 個以上の `<packageType>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="4860f-186">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="4860f-187">各 packageType は、*name* 属性と *version* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="4860f-187">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="4860f-188">「[Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type)」(パッケージの種類の設定) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-188">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="4860f-189">依存関係</span><span class="sxs-lookup"><span data-stu-id="4860f-189">dependencies</span></span>
<span data-ttu-id="4860f-190">パッケージの依存関係を指定する 0 個以上の `<dependency>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="4860f-190">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="4860f-191">各 dependency は、*id*、*version*、*include* (3.x 以降)、*exclude* (3.x 以降) の各属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="4860f-191">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="4860f-192">後の「[依存関係](#dependencies-element)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-192">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="4860f-193">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="4860f-193">frameworkAssemblies</span></span>
<span data-ttu-id="4860f-194">*(1.2 以降)* このパッケージで必要な .NET Framework アセンブリ参照を示す 0 個以上の `<frameworkAssembly>` 要素のコレクション。パッケージを使うプロジェクトに参照が確実に追加されるようにします。</span><span class="sxs-lookup"><span data-stu-id="4860f-194">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="4860f-195">各 frameworkAssembly は、*assemblyName* 属性と *targetFramework* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="4860f-195">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="4860f-196">[フレームワーク アセンブリ参照 GAC の指定](#specifying-framework-assembly-references-gac)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-196">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="4860f-197">参照</span><span class="sxs-lookup"><span data-stu-id="4860f-197">references</span></span>
<span data-ttu-id="4860f-198">*(1.5 以降)* パッケージの `lib` フォルダー内のアセンブリのうちプロジェクト参照として追加するものを指定する、0 個以上の `<reference>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="4860f-198">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="4860f-199">各参照は、*file* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="4860f-199">Each reference has a *file* attribute.</span></span> <span data-ttu-id="4860f-200">`<references>` は `<group>` 要素を含むこともでき、その *targetFramework* 属性に `<reference>` 要素を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="4860f-200">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="4860f-201">省略すると、`lib` のすべての参照が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4860f-201">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="4860f-202">[明示的なアセンブリ参照の指定](#specifying-explicit-assembly-references)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-202">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="4860f-203">contentFiles</span><span class="sxs-lookup"><span data-stu-id="4860f-203">contentFiles</span></span>
<span data-ttu-id="4860f-204">*(3.3 以降)* 使用する側のプロジェクトに含めるコンテンツ ファイルを示す `<files>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="4860f-204">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="4860f-205">これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-205">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="4860f-206">[パッケージに含めるファイルの指定](#specifying-files-to-include-in-the-package)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-206">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="4860f-207">ファイル</span><span class="sxs-lookup"><span data-stu-id="4860f-207">files</span></span> 
<span data-ttu-id="4860f-208">`<package>` ノードでは、`<metadata>` の兄弟として `<files>` ノードを追加するか、または `<metadata>` の子として `<contentFiles>` を追加して、パッケージに含めるアセンブリとコンテンツ ファイルを指定できます。</span><span class="sxs-lookup"><span data-stu-id="4860f-208">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="4860f-209">詳しくは、このトピックで後述する「[アセンブリ ファイルを含める](#including-assembly-files)」と「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-209">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="4860f-210">置換トークン</span><span class="sxs-lookup"><span data-stu-id="4860f-210">Replacement tokens</span></span>

<span data-ttu-id="4860f-211">パッケージを作成するとき、[`nuget pack` コマンド](../tools/cli-ref-pack.md)は、`.nuspec` ファイルの `<metadata>` ノード内の $ で区切られたトークンを、プロジェクト ファイルまたは `pack` コマンドの `-properties` スイッチで指定されている値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4860f-211">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="4860f-212">コマンド ラインでは、`nuget pack -properties <name>=<value>;<name>=<value>` でトークンの値を指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-212">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="4860f-213">たとえば、`.nuspec` では `$owners$` や `$desc$` などのトークンを使っておき、パッキング時に次のようにして値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="4860f-213">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="4860f-214">プロジェクトの値を使うには、次の表で説明するトークンを指定します (AssemblyInfo は、`Properties` 内の `AssemblyInfo.cs` や `AssemblyInfo.vb` などのファイルを参照します)。</span><span class="sxs-lookup"><span data-stu-id="4860f-214">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="4860f-215">これらのトークンを使うには、`nuget pack` を実行するときに、`.nuspec` だけでなくプロジェクト ファイルも指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-215">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="4860f-216">たとえば、次のコマンドを使うと、`.nuspec` ファイルの `$id$` および `$version$` トークンが、プロジェクトの `AssemblyName` および `AssemblyVersion` の値に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="4860f-216">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="4860f-217">通常、プロジェクトがある場合は、最初に `nuget spec MyProject.csproj` を使って `.nuspec` を作成すると、一部の標準的なトークンが自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-217">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="4860f-218">ただし、`.nuspec` の必須要素に対する値がプロジェクトにないと、`nuget pack` は失敗します。</span><span class="sxs-lookup"><span data-stu-id="4860f-218">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="4860f-219">さらに、プロジェクトの値を変更する場合は、パッケージを作成する前に必ずビルドし直してください。これは、pack コマンドの `build` スイッチで簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="4860f-219">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="4860f-220">例外である `$configuration$` を除き、コマンド ラインの同じトークンに割り当てられている値より、プロジェクトの値の方が優先的に使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-220">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="4860f-221">トークン</span><span class="sxs-lookup"><span data-stu-id="4860f-221">Token</span></span> | <span data-ttu-id="4860f-222">値のソース</span><span class="sxs-lookup"><span data-stu-id="4860f-222">Value source</span></span> | <span data-ttu-id="4860f-223">[値]</span><span class="sxs-lookup"><span data-stu-id="4860f-223">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="4860f-224">**$id$**</span><span class="sxs-lookup"><span data-stu-id="4860f-224">**$id$**</span></span> | <span data-ttu-id="4860f-225">プロジェクト ファイル</span><span class="sxs-lookup"><span data-stu-id="4860f-225">Project file</span></span> | <span data-ttu-id="4860f-226">プロジェクト ファイルの AssemblyName (タイトル)</span><span class="sxs-lookup"><span data-stu-id="4860f-226">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="4860f-227">**$version$**</span><span class="sxs-lookup"><span data-stu-id="4860f-227">**$version$**</span></span> | <span data-ttu-id="4860f-228">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="4860f-228">AssemblyInfo</span></span> | <span data-ttu-id="4860f-229">ある場合は AssemblyInformationalVersion、ない場合は AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="4860f-229">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="4860f-230">**$author$**</span><span class="sxs-lookup"><span data-stu-id="4860f-230">**$author$**</span></span> | <span data-ttu-id="4860f-231">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="4860f-231">AssemblyInfo</span></span> | <span data-ttu-id="4860f-232">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="4860f-232">AssemblyCompany</span></span> |
| <span data-ttu-id="4860f-233">**$title$**</span><span class="sxs-lookup"><span data-stu-id="4860f-233">**$title$**</span></span> | <span data-ttu-id="4860f-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="4860f-234">AssemblyInfo</span></span> | <span data-ttu-id="4860f-235">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="4860f-235">AssemblyTitle</span></span> |
| <span data-ttu-id="4860f-236">**$description$**</span><span class="sxs-lookup"><span data-stu-id="4860f-236">**$description$**</span></span> | <span data-ttu-id="4860f-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="4860f-237">AssemblyInfo</span></span> | <span data-ttu-id="4860f-238">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="4860f-238">AssemblyDescription</span></span> |
| <span data-ttu-id="4860f-239">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="4860f-239">**$copyright$**</span></span> | <span data-ttu-id="4860f-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="4860f-240">AssemblyInfo</span></span> | <span data-ttu-id="4860f-241">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="4860f-241">AssemblyCopyright</span></span> |
| <span data-ttu-id="4860f-242">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="4860f-242">**$configuration$**</span></span> | <span data-ttu-id="4860f-243">アセンブリ DLL</span><span class="sxs-lookup"><span data-stu-id="4860f-243">Assembly DLL</span></span> | <span data-ttu-id="4860f-244">アセンブリのビルドに使われる構成。既定値は Debug。</span><span class="sxs-lookup"><span data-stu-id="4860f-244">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="4860f-245">Release 構成を使ってパッケージを作成するには、常にコマンド ラインで `-properties Configuration=Release` を使うことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4860f-245">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="4860f-246">[アセンブリ ファイル](#including-assembly-files)および[コンテンツ ファイル](#including-content-files)を含めるときは、トークンを使ってパスを解決することもできます。</span><span class="sxs-lookup"><span data-stu-id="4860f-246">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="4860f-247">トークンの名前は MSBuild のプロパティと同じであり、現在のビルド構成に基づいて含めるファイルを選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="4860f-247">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="4860f-248">たとえば、`.nuspec` ファイルで次のトークンを使うものとします。</span><span class="sxs-lookup"><span data-stu-id="4860f-248">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="4860f-249">そして、MSBuild で `AssemblyName` が `LoggingLibrary` であるアセンブリを `Release` 構成でビルドすると、パッケージ内の `.nuspec` ファイルの行は結果として次のようになります。</span><span class="sxs-lookup"><span data-stu-id="4860f-249">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="4860f-250">依存関係要素</span><span class="sxs-lookup"><span data-stu-id="4860f-250">Dependencies element</span></span>

<span data-ttu-id="4860f-251">`<metadata>` 内の `<dependencies>` 要素は、最上位のパッケージが依存している他のパッケージを示す `<dependency>` 要素をいくつでも含むことができます。</span><span class="sxs-lookup"><span data-stu-id="4860f-251">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="4860f-252">各 `<dependency>` の属性は次にとおりです。</span><span class="sxs-lookup"><span data-stu-id="4860f-252">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="4860f-253">属性</span><span class="sxs-lookup"><span data-stu-id="4860f-253">Attribute</span></span> | <span data-ttu-id="4860f-254">説明</span><span class="sxs-lookup"><span data-stu-id="4860f-254">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="4860f-255">(必須) "EntityFramework" や "NUnit" などの依存関係のパッケージ ID。これはパッケージ ページに表示されるパッケージ nuget.org の名前となります。</span><span class="sxs-lookup"><span data-stu-id="4860f-255">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="4860f-256">(必須) 依存関係として許容されるバージョンの範囲。</span><span class="sxs-lookup"><span data-stu-id="4860f-256">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="4860f-257">厳密な構文については、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」(パッケージのバージョン管理) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-257">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="4860f-258">include</span><span class="sxs-lookup"><span data-stu-id="4860f-258">include</span></span> | <span data-ttu-id="4860f-259">最終的なパッケージに含める依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="4860f-259">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="4860f-260">既定値は `none` です。</span><span class="sxs-lookup"><span data-stu-id="4860f-260">The default value is `none`.</span></span> |
| <span data-ttu-id="4860f-261">exclude</span><span class="sxs-lookup"><span data-stu-id="4860f-261">exclude</span></span> | <span data-ttu-id="4860f-262">最終的なパッケージから除外する依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="4860f-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="4860f-263">既定値は `all` です。</span><span class="sxs-lookup"><span data-stu-id="4860f-263">The  default value is `all`.</span></span> <span data-ttu-id="4860f-264">`exclude` で指定されているタグの方が、`include` で指定されているタグより優先されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-264">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="4860f-265">たとえば、`include="runtime, compile" exclude="compile"` は `include="runtime"` と同じです。</span><span class="sxs-lookup"><span data-stu-id="4860f-265">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="4860f-266">包含/除外タグ</span><span class="sxs-lookup"><span data-stu-id="4860f-266">Include/Exclude tag</span></span> | <span data-ttu-id="4860f-267">ターゲットの影響を受けるフォルダー</span><span class="sxs-lookup"><span data-stu-id="4860f-267">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="4860f-268">contentFiles</span><span class="sxs-lookup"><span data-stu-id="4860f-268">contentFiles</span></span> | <span data-ttu-id="4860f-269">Content</span><span class="sxs-lookup"><span data-stu-id="4860f-269">Content</span></span> |
| <span data-ttu-id="4860f-270">ランタイム</span><span class="sxs-lookup"><span data-stu-id="4860f-270">runtime</span></span> | <span data-ttu-id="4860f-271">Runtime、Resources、FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="4860f-271">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="4860f-272">compile</span><span class="sxs-lookup"><span data-stu-id="4860f-272">compile</span></span> | <span data-ttu-id="4860f-273">lib</span><span class="sxs-lookup"><span data-stu-id="4860f-273">lib</span></span> |
| <span data-ttu-id="4860f-274">ビルド</span><span class="sxs-lookup"><span data-stu-id="4860f-274">build</span></span> | <span data-ttu-id="4860f-275">build (MSBuild のプロパティとターゲット)</span><span class="sxs-lookup"><span data-stu-id="4860f-275">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="4860f-276">native</span><span class="sxs-lookup"><span data-stu-id="4860f-276">native</span></span> | <span data-ttu-id="4860f-277">native</span><span class="sxs-lookup"><span data-stu-id="4860f-277">native</span></span> |
| <span data-ttu-id="4860f-278">none</span><span class="sxs-lookup"><span data-stu-id="4860f-278">none</span></span> | <span data-ttu-id="4860f-279">フォルダーなし</span><span class="sxs-lookup"><span data-stu-id="4860f-279">No folders</span></span> |
| <span data-ttu-id="4860f-280">すべて</span><span class="sxs-lookup"><span data-stu-id="4860f-280">all</span></span> | <span data-ttu-id="4860f-281">すべてのフォルダー</span><span class="sxs-lookup"><span data-stu-id="4860f-281">All folders</span></span> |

<span data-ttu-id="4860f-282">たとえば、次の行は `PackageA` バージョン 1.1.0 以降および `PackageB` バージョン 1.x での依存関係を示します。</span><span class="sxs-lookup"><span data-stu-id="4860f-282">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="4860f-283">次の行も同じパッケージでの依存関係を示しますが、`PackageA` の `contentFiles` および `build` フォルダーを含めて、`PackageB` の `native` および `compile` フォルダーを除くすべてを含めることを指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-283">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="4860f-284">注: `nuget spec` を使ってプロジェクトから `.nuspec` を作成すると、そのプロジェクトに存在する依存関係が結果の `.nuspec` ファイルに自動的に含まれます。</span><span class="sxs-lookup"><span data-stu-id="4860f-284">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="4860f-285">依存関係グループ</span><span class="sxs-lookup"><span data-stu-id="4860f-285">Dependency groups</span></span>

<span data-ttu-id="4860f-286">*バージョン 2.0 以降*</span><span class="sxs-lookup"><span data-stu-id="4860f-286">*Version 2.0+*</span></span>

<span data-ttu-id="4860f-287">1 つのフラット リストの代わりに、`<dependencies>` の `<group>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って依存関係を指定できます。</span><span class="sxs-lookup"><span data-stu-id="4860f-287">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="4860f-288">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<dependency>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4860f-288">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="4860f-289">ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの依存関係が一緒にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="4860f-289">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="4860f-290">依存関係の既定のリストまたはフォールバック リストとしては、`targetFramework` 属性のない `<group>` 要素が使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-290">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="4860f-291">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-291">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="4860f-292">グループの形式をフラット リストと併用することはできません。</span><span class="sxs-lookup"><span data-stu-id="4860f-292">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="4860f-293">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="4860f-293">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="4860f-294">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="4860f-294">Explicit assembly references</span></span>

<span data-ttu-id="4860f-295">`<references>` 要素は、パッケージを使うときにターゲット プロジェクトが参照する必要のあるアセンブリを明示的に指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-295">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="4860f-296">この要素がある場合、NuGet は一覧で指定されているアセンブリのみへの参照を追加します。パッケージの `lib` フォルダーに含まれる他のアセンブリに対する参照は追加されません。</span><span class="sxs-lookup"><span data-stu-id="4860f-296">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="4860f-297">たとえば、次の `<references>` 要素は、パッケージに他のアセンブリがある場合でも、`xunit.dll` と `xunit.extensions.dll` に対する参照だけを追加するよう NuGet に指示します。</span><span class="sxs-lookup"><span data-stu-id="4860f-297">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="4860f-298">明示的な参照は、通常、設計時のみのアセンブリに使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-298">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="4860f-299">たとえば、[コード コントラクト](/dotnet/framework/debug-trace-profile/code-contracts)を使うときは、Visual Studio がコントラクト アセンブリを検出できるように、コントラクト アセンブリはそれが拡張するランタイム アセンブリの隣に存在する必要がありますが、プロジェクトでコントラクト アセンブリを参照したり、プロジェクトの `bin` フォルダーにコントラクト アセンブリをコピーしたりする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4860f-299">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="4860f-300">同様に、明示的な参照は XUnit などの単体テスト フレームワークに使うことができ、その場合、ツール アセンブリはランタイム アセンブリの隣に存在する必要がありますが、プロジェクト参照として含まれる必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4860f-300">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="4860f-301">[参照グループ]</span><span class="sxs-lookup"><span data-stu-id="4860f-301">Reference groups</span></span>

<span data-ttu-id="4860f-302">1 つのフラット リストの代わりに、`<references>` の `<group>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って参照を指定できます。</span><span class="sxs-lookup"><span data-stu-id="4860f-302">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="4860f-303">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<reference>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4860f-303">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="4860f-304">ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの参照はプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-304">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="4860f-305">参照の既定のリストまたはフォールバック リストとしては、`targetFramework` 属性のない `<group>` 要素が使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-305">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="4860f-306">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-306">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="4860f-307">グループの形式をフラット リストと併用することはできません。</span><span class="sxs-lookup"><span data-stu-id="4860f-307">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="4860f-308">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="4860f-308">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="4860f-309">フレームワーク アセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="4860f-309">Framework assembly references</span></span>

<span data-ttu-id="4860f-310">フレームワーク アセンブリは、.NET Framework の一部であり、指定されたコンピューターのグローバル アセンブリ キャッシュ (GAC) に既に存在している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4860f-310">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="4860f-311">`<frameworkAssemblies>` 要素でこれらのアセンブリを指定することにより、プロジェクトに必要な参照がまだない場合であっても、そのような参照をプロジェクトに確実に追加できます。</span><span class="sxs-lookup"><span data-stu-id="4860f-311">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="4860f-312">もちろん、そのようなアセンブリがパッケージに直接含まれることはありません。</span><span class="sxs-lookup"><span data-stu-id="4860f-312">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="4860f-313">`<frameworkAssemblies>` 要素には 0 個以上の `<frameworkAssembly>` 要素を含めることができ、それぞれで次の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-313">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="4860f-314">属性</span><span class="sxs-lookup"><span data-stu-id="4860f-314">Attribute</span></span> | <span data-ttu-id="4860f-315">説明</span><span class="sxs-lookup"><span data-stu-id="4860f-315">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4860f-316">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="4860f-316">**assemblyName**</span></span> | <span data-ttu-id="4860f-317">(必須) 完全修飾アセンブリ名。</span><span class="sxs-lookup"><span data-stu-id="4860f-317">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="4860f-318">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="4860f-318">**targetFramework**</span></span> | <span data-ttu-id="4860f-319">(省略可能) この参照を適用するターゲット フレームワークを指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-319">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="4860f-320">省略した場合は、参照がすべてのフレームワークに適用されることを示します。</span><span class="sxs-lookup"><span data-stu-id="4860f-320">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="4860f-321">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-321">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="4860f-322">次の例は、`System.Net` への参照はすべてのターゲット フレームワークに適用され、`System.ServiceModel` への参照は .NET Framework 4.0 のみに適用されることを示します。</span><span class="sxs-lookup"><span data-stu-id="4860f-322">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="4860f-323">アセンブリ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="4860f-323">Including assembly files</span></span>

<span data-ttu-id="4860f-324">「[パッケージを作成する](../create-packages/creating-a-package.md)」で説明されている規則に従う場合、`.nuspec` ファイルでファイルの一覧を明示的に指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4860f-324">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="4860f-325">`nuget pack` コマンドが必要なファイルを自動的に選びます。</span><span class="sxs-lookup"><span data-stu-id="4860f-325">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="4860f-326">プロジェクトにパッケージをインストールするとき、NuGet はパッケージの DLL にアセンブリ参照を自動的に追加します。ただし、指定されている `.resources.dll` は、ローカライズされたサテライト アセンブリであると見なされるため "*除外*" されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-326">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="4860f-327">そのため、避けなければ不可欠なパッケージ コードが含まれてしまうファイルには `.resources.dll` を使わないようにします。</span><span class="sxs-lookup"><span data-stu-id="4860f-327">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="4860f-328">この自動動作をバイパスして、パッケージに含めるファイルを明示的に制御するには、`<files>` 要素を `<package>` の子要素 (および `<metadata>` の兄弟要素) として配置し、各ファイルを個別の `<file>` 要素で示します。</span><span class="sxs-lookup"><span data-stu-id="4860f-328">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="4860f-329">例えば:</span><span class="sxs-lookup"><span data-stu-id="4860f-329">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="4860f-330">NuGet 2.x 以前および `packages.config` を使っているプロジェクトでは、`<files>` 要素はパッケージのインストール時に変更できないコンテンツ ファイルを含めるためにも使われます。</span><span class="sxs-lookup"><span data-stu-id="4860f-330">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="4860f-331">NuGet 3.3 以降で、PackageReference を使用しているプロジェクトでは、代わりに `<contentFiles>` 要素が使用されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-331">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="4860f-332">詳しくは、後の「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-332">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="4860f-333">File 要素の属性</span><span class="sxs-lookup"><span data-stu-id="4860f-333">File element attributes</span></span>

<span data-ttu-id="4860f-334">各 `<file>` 要素では、次の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-334">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="4860f-335">属性</span><span class="sxs-lookup"><span data-stu-id="4860f-335">Attribute</span></span> | <span data-ttu-id="4860f-336">説明</span><span class="sxs-lookup"><span data-stu-id="4860f-336">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4860f-337">**src**</span><span class="sxs-lookup"><span data-stu-id="4860f-337">**src**</span></span> | <span data-ttu-id="4860f-338">含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。</span><span class="sxs-lookup"><span data-stu-id="4860f-338">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="4860f-339">絶対パスを指定しない限り、パスは `.nuspec` ファイルが基準になります。</span><span class="sxs-lookup"><span data-stu-id="4860f-339">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="4860f-340">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="4860f-340">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="4860f-341">**target**</span><span class="sxs-lookup"><span data-stu-id="4860f-341">**target**</span></span> | <span data-ttu-id="4860f-342">ソース ファイルが格納されるパッケージ内のフォルダーへの相対パス。`lib`、`content`、`build`、または `tools` で始まっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="4860f-342">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="4860f-343">[規則に基づく作業ディレクトリからの .nuspec の作成](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4860f-343">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="4860f-344">**exclude**</span><span class="sxs-lookup"><span data-stu-id="4860f-344">**exclude**</span></span> | <span data-ttu-id="4860f-345">`src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。</span><span class="sxs-lookup"><span data-stu-id="4860f-345">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="4860f-346">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="4860f-346">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="4860f-347">使用例</span><span class="sxs-lookup"><span data-stu-id="4860f-347">Examples</span></span>

<span data-ttu-id="4860f-348">**1 つのアセンブリ**</span><span class="sxs-lookup"><span data-stu-id="4860f-348">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="4860f-349">**ターゲット フレームワークに固有の 1 つのアセンブリ**</span><span class="sxs-lookup"><span data-stu-id="4860f-349">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="4860f-350">**ワイルドカードを使った DLL のセット**</span><span class="sxs-lookup"><span data-stu-id="4860f-350">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="4860f-351">**異なるフレームワークの DLL**</span><span class="sxs-lookup"><span data-stu-id="4860f-351">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="4860f-352">**ファイルの除外**</span><span class="sxs-lookup"><span data-stu-id="4860f-352">**Excluding files**</span></span>

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="4860f-353">コンテンツ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="4860f-353">Including content files</span></span>

<span data-ttu-id="4860f-354">コンテンツ ファイルは、パッケージでプロジェクトに含める必要がある変更できないファイルです。</span><span class="sxs-lookup"><span data-stu-id="4860f-354">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="4860f-355">変更できないので、それを使うプロジェクトによる変更は意図されていません。</span><span class="sxs-lookup"><span data-stu-id="4860f-355">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="4860f-356">コンテンツ ファイルの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4860f-356">Example content files include:</span></span>

- <span data-ttu-id="4860f-357">リソースとして埋め込まれる画像</span><span class="sxs-lookup"><span data-stu-id="4860f-357">Images that are embedded as resources</span></span>
- <span data-ttu-id="4860f-358">コンパイル済みのソース ファイル</span><span class="sxs-lookup"><span data-stu-id="4860f-358">Source files that are already compiled</span></span>
- <span data-ttu-id="4860f-359">プロジェクトのビルド出力と共に含まれる必要があるスクリプト</span><span class="sxs-lookup"><span data-stu-id="4860f-359">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="4860f-360">プロジェクトに含まれる必要はあるが、プロジェクト固有の変更は必要ない、パッケージの構成ファイル</span><span class="sxs-lookup"><span data-stu-id="4860f-360">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="4860f-361">コンテンツ ファイルをパッケージに含めるには、`<files>` 要素を使い、`target` 属性で `content` フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-361">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="4860f-362">ただし、PackageReference を使用しているプロジェクトにパッケージをインストールする場合、このようなファイルは無視され、代わりに `<contentFiles>` 要素が使用されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-362">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="4860f-363">使用する側のプロジェクトとの最大限の互換性のため、パッケージでは両方の要素でコンテンツ ファイルを指定するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="4860f-363">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="4860f-364">コンテンツ ファイルに対する files 要素の使用</span><span class="sxs-lookup"><span data-stu-id="4860f-364">Using the files element for content files</span></span>

<span data-ttu-id="4860f-365">コンテンツ ファイルでは、アセンブリ ファイルの場合と同じ形式を使用しますが、次の例のように、`target` 属性で基本フォルダーとして `content` を指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-365">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="4860f-366">**基本的なコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="4860f-366">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="4860f-367">**ディレクトリ構造を持つコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="4860f-367">**Content files with directory structure**</span></span>

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

<span data-ttu-id="4860f-368">**ターゲット フレームワークに固有のコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="4860f-368">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="4860f-369">**名前のドットでフォルダーにコピーされるコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="4860f-369">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="4860f-370">この場合、NuGet は `target` の拡張子が `src` の拡張子と一致しないものと判断し、`target` での名前のその部分をフォルダーとして扱います。</span><span class="sxs-lookup"><span data-stu-id="4860f-370">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="4860f-371">**拡張子のないコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="4860f-371">**Content files without extensions**</span></span>

<span data-ttu-id="4860f-372">拡張子のないファイルを含めるには、ワイルドカード `*` または `**` を使います。</span><span class="sxs-lookup"><span data-stu-id="4860f-372">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="4860f-373">**深いパスと深いターゲットのコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="4860f-373">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="4860f-374">この場合、ソースとターゲットのファイル拡張子が一致するので、NuGet はターゲットがフォルダーではなくファイル名であると想定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-374">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="4860f-375">**パッケージ内のコンテンツ ファイルの名前の変更**</span><span class="sxs-lookup"><span data-stu-id="4860f-375">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="4860f-376">**ファイルの除外**</span><span class="sxs-lookup"><span data-stu-id="4860f-376">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="4860f-377">コンテンツ ファイルに対する contentFiles 要素の使用</span><span class="sxs-lookup"><span data-stu-id="4860f-377">Using the contentFiles element for content files</span></span>

<span data-ttu-id="4860f-378">*NuGet 4.0 以降で、PackageReference を使用している場合*</span><span class="sxs-lookup"><span data-stu-id="4860f-378">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="4860f-379">既定では、パッケージはコンテンツを `contentFiles` フォルダーに配置し (下記参照)、`nuget pack` は既定の属性を使ってそのフォルダーにすべてのファイルを格納します。</span><span class="sxs-lookup"><span data-stu-id="4860f-379">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="4860f-380">この場合は、`contentFiles` ノードを `.nuspec` に含める必要はまったくありません。</span><span class="sxs-lookup"><span data-stu-id="4860f-380">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="4860f-381">含まれるファイルを制御するには、含めるファイルを厳密に示す `<files>` 要素のコレクションである `<contentFiles>` 要素を指定します。</span><span class="sxs-lookup"><span data-stu-id="4860f-381">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="4860f-382">これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-382">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="4860f-383">属性</span><span class="sxs-lookup"><span data-stu-id="4860f-383">Attribute</span></span> | <span data-ttu-id="4860f-384">説明</span><span class="sxs-lookup"><span data-stu-id="4860f-384">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4860f-385">**include**</span><span class="sxs-lookup"><span data-stu-id="4860f-385">**include**</span></span> | <span data-ttu-id="4860f-386">(必須) 含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。</span><span class="sxs-lookup"><span data-stu-id="4860f-386">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="4860f-387">絶対パスを指定しない限り、パスは `.nuspec` ファイルが基準になります。</span><span class="sxs-lookup"><span data-stu-id="4860f-387">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="4860f-388">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="4860f-388">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="4860f-389">**exclude**</span><span class="sxs-lookup"><span data-stu-id="4860f-389">**exclude**</span></span> | <span data-ttu-id="4860f-390">`src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。</span><span class="sxs-lookup"><span data-stu-id="4860f-390">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="4860f-391">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="4860f-391">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="4860f-392">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="4860f-392">**buildAction**</span></span> | <span data-ttu-id="4860f-393">MSBuild のコンテンツ項目に割り当てるビルド アクション。`Content`、`None`、`Embedded Resource`、`Compile` などです。既定値は、`Compile` です。</span><span class="sxs-lookup"><span data-stu-id="4860f-393">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="4860f-394">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="4860f-394">**copyToOutput**</span></span> | <span data-ttu-id="4860f-395">出力フォルダーをビルドするコンテンツ項目をコピー (またはパブリッシュ) するかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="4860f-395">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="4860f-396">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="4860f-396">The default is false.</span></span> |
| <span data-ttu-id="4860f-397">**flatten**</span><span class="sxs-lookup"><span data-stu-id="4860f-397">**flatten**</span></span> | <span data-ttu-id="4860f-398">コンテンツ項目をビルド出力の単一フォルダーにコピーするか (true)、それともパッケージのフォルダー構造を保持するか (false) を示すブール値。</span><span class="sxs-lookup"><span data-stu-id="4860f-398">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="4860f-399">このフラグは、copyToOutput が true に設定されている場合のみ機能します。</span><span class="sxs-lookup"><span data-stu-id="4860f-399">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="4860f-400">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="4860f-400">The default is false.</span></span> |

<span data-ttu-id="4860f-401">パッケージをインストールするとき、NuGet は `<contentFiles>` の子要素を上から下に順番に適用します。</span><span class="sxs-lookup"><span data-stu-id="4860f-401">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="4860f-402">複数のエントリが同じファイルに一致する場合は、すべてのエントリが適用されます。</span><span class="sxs-lookup"><span data-stu-id="4860f-402">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="4860f-403">同じ属性に対して競合がある場合は、最上位のエントリが下位のエントリをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="4860f-403">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="4860f-404">パッケージ フォルダーの構造</span><span class="sxs-lookup"><span data-stu-id="4860f-404">Package folder structure</span></span>

<span data-ttu-id="4860f-405">パッケージ プロジェクトでは、次のパターンを使ってコンテンツを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4860f-405">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="4860f-406">`codeLanguages` には、`cs`、`vb`、`fs`、`any`、または指定された `$(ProjectLanguage)` に相当する小文字表現を指定できます。</span><span class="sxs-lookup"><span data-stu-id="4860f-406">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="4860f-407">`TxM` は、NuGet がサポートする任意の有効なターゲット フレームワーク モニカーです (「[ターゲット フレームワーク](../reference/target-frameworks.md)」を参照)。</span><span class="sxs-lookup"><span data-stu-id="4860f-407">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="4860f-408">この構文の末尾に、任意のフォルダー構造を追加できます。</span><span class="sxs-lookup"><span data-stu-id="4860f-408">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="4860f-409">例えば:</span><span class="sxs-lookup"><span data-stu-id="4860f-409">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="4860f-410">空のフォルダーでは、`.` を使って、言語と TxM の特定の組み合わせにコンテンツを提供しないようにすることができます。次はその例です。</span><span class="sxs-lookup"><span data-stu-id="4860f-410">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="4860f-411">contentFiles セクションの例</span><span class="sxs-lookup"><span data-stu-id="4860f-411">Example contentFiles section</span></span>

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="4860f-412">Nuspec ファイルの例</span><span class="sxs-lookup"><span data-stu-id="4860f-412">Example nuspec files</span></span>

<span data-ttu-id="4860f-413">**依存関係またはファイルを指定しない単純な `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="4860f-413">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="4860f-414">**依存関係を含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="4860f-414">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="4860f-415">**ファイルを含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="4860f-415">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="4860f-416">**フレームワーク アセンブリを含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="4860f-416">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="4860f-417">この例では、指定したプロジェクト ターゲットに次のものがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="4860f-417">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="4860f-418">.NET4 -> `System.Web`、`System.Net`</span><span class="sxs-lookup"><span data-stu-id="4860f-418">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="4860f-419">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="4860f-419">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="4860f-420">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="4860f-420">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="4860f-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="4860f-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="4860f-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="4860f-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
