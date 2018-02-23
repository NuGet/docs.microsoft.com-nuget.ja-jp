---
title: "NuGet の .nuspec ファイル リファレンス | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: ".nuspec ファイルには、パッケージを作成するとき、およびパッケージのコンシューマーに情報を提供するために使われる、パッケージのメタデータが含まれています。"
keywords: "nuspec リファレンス, NuGet パッケージ メタデータ, NuGet パッケージ マニフェスト, nuspec スキーマ"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: c52d0a7c0da507cb9688c8a7b2c4eaf54a8ca5c2
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="nuspec-reference"></a><span data-ttu-id="f471e-104">.nuspec リファレンス</span><span class="sxs-lookup"><span data-stu-id="f471e-104">.nuspec reference</span></span>

<span data-ttu-id="f471e-105">`.nuspec` ファイルは、パッケージのメタデータが含まれている XML マニフェストです。</span><span class="sxs-lookup"><span data-stu-id="f471e-105">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="f471e-106">このマニフェストは、パッケージを作成するためと、コンシューマーに情報を提供するための、両方に使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-106">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="f471e-107">パッケージにはマニフェストが常に含まれています。</span><span class="sxs-lookup"><span data-stu-id="f471e-107">The manifest is always included in a package.</span></span>

<span data-ttu-id="f471e-108">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="f471e-108">In this topic:</span></span>

- [<span data-ttu-id="f471e-109">一般的な形式とスキーマ</span><span class="sxs-lookup"><span data-stu-id="f471e-109">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="f471e-110">[置換トークン](#replacement-tokens) (Visual Studio プロジェクトで使われるとき)</span><span class="sxs-lookup"><span data-stu-id="f471e-110">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="f471e-111">依存関係</span><span class="sxs-lookup"><span data-stu-id="f471e-111">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="f471e-112">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="f471e-112">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="f471e-113">フレームワーク アセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="f471e-113">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="f471e-114">アセンブリ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="f471e-114">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="f471e-115">コンテンツ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="f471e-115">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="f471e-116">例</span><span class="sxs-lookup"><span data-stu-id="f471e-116">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="f471e-117">一般的な形式とスキーマ</span><span class="sxs-lookup"><span data-stu-id="f471e-117">General form and schema</span></span>

<span data-ttu-id="f471e-118">最新の `nuspec.xsd` スキーマ ファイルは、[NuGet GitHub リポジトリ](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)にあります。</span><span class="sxs-lookup"><span data-stu-id="f471e-118">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="f471e-119">このスキーマでの `.nuspec` ファイルの一般的な形式は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="f471e-119">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="f471e-120">スキーマの視覚的な表現をはっきり表示したい場合は、Visual Studio のデザイン モードでスキーマ ファイルを開き、**[XML スキーマ エクスプローラー]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f471e-120">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="f471e-121">または、コードとしてファイルを開き、エディター内を右クリックして、**[XML スキーマ エクスプローラーで表示]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="f471e-121">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="f471e-122">どちらの方法でも次のように表示されます (ほとんどを展開した場合)。</span><span class="sxs-lookup"><span data-stu-id="f471e-122">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio のスキーマ エクスプローラーで開いた nuspec.xsd](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="f471e-124">メタデータの属性</span><span class="sxs-lookup"><span data-stu-id="f471e-124">Metadata attributes</span></span>

<span data-ttu-id="f471e-125">`<metadata>` 要素では、次の表で説明する属性を指定できます。</span><span class="sxs-lookup"><span data-stu-id="f471e-125">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="f471e-126">属性</span><span class="sxs-lookup"><span data-stu-id="f471e-126">Attribute</span></span> | <span data-ttu-id="f471e-127">必須</span><span class="sxs-lookup"><span data-stu-id="f471e-127">Required</span></span> | <span data-ttu-id="f471e-128">説明</span><span class="sxs-lookup"><span data-stu-id="f471e-128">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="f471e-129">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="f471e-129">**minClientVersion**</span></span> | <span data-ttu-id="f471e-130">×</span><span class="sxs-lookup"><span data-stu-id="f471e-130">No</span></span> | <span data-ttu-id="f471e-131">nuget.exe および Visual Studio パッケージ マネージャーで強制する、このパッケージをインストールできる NuGet クライアントの最小バージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-131">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="f471e-132">これは、NuGet クライアントの特定のバージョンで追加された `.nuspec` ファイルの特定の機能にパッケージが依存しているときに、常に使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-132">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="f471e-133">たとえば、`developmentDependency` 属性を使っているパッケージでは、`minClientVersion` に "2.8" を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f471e-133">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="f471e-134">同様に、`contentFiles` 要素 (次のセクションを参照) を使っているパッケージでは、`minClientVersion` を "3.3" に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f471e-134">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="f471e-135">また、バージョン 2.5 より前の NuGet クライアントはこのフラグを認識しないので、`minClientVersion` の値が何であっても、"*常に*" パッケージをインストールしないことにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="f471e-135">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="f471e-136">メタデータの必須要素</span><span class="sxs-lookup"><span data-stu-id="f471e-136">Required metadata elements</span></span>

<span data-ttu-id="f471e-137">以下の要素はパッケージの最低要件であり、[メタデータの省略可能な要素](#optional-metadata-elements)を追加してパッケージに関する開発者の全体的なエクスペリエンスを向上させることを検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f471e-137">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="f471e-138">これらの要素は、`<metadata>` 要素内で指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f471e-138">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="f471e-139">要素</span><span class="sxs-lookup"><span data-stu-id="f471e-139">Element</span></span> | <span data-ttu-id="f471e-140">説明</span><span class="sxs-lookup"><span data-stu-id="f471e-140">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f471e-141">**ID**</span><span class="sxs-lookup"><span data-stu-id="f471e-141">**id**</span></span> | <span data-ttu-id="f471e-142">パッケージの識別子。大文字と小文字が区別されます。nuget.org 全体で、またはパッケージが存在するギャラリー全体で、一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="f471e-142">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="f471e-143">ID は、スペースまたは URL で無効な文字を含んでいてはならず、一般に .NET 名前空間の規則に従います。</span><span class="sxs-lookup"><span data-stu-id="f471e-143">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="f471e-144">ガイダンスについては、[一意のパッケージ識別子の選択](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-144">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="f471e-145">**version**</span><span class="sxs-lookup"><span data-stu-id="f471e-145">**version**</span></span> | <span data-ttu-id="f471e-146">パッケージのバージョン。*major.minor.patch* のパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="f471e-146">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="f471e-147">「[Package versioning](../reference/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) で説明されているように、バージョン番号にはプレリリースのサフィックスを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="f471e-147">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="f471e-148">**description**</span><span class="sxs-lookup"><span data-stu-id="f471e-148">**description**</span></span> | <span data-ttu-id="f471e-149">UI 画面用のパッケージの長い説明。</span><span class="sxs-lookup"><span data-stu-id="f471e-149">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="f471e-150">**authors**</span><span class="sxs-lookup"><span data-stu-id="f471e-150">**authors**</span></span> | <span data-ttu-id="f471e-151">パッケージ作成者の一覧。コンマで区切られています。nuget.org のプロファイル名と一致します。これらは nuget.org の NuGet ギャラリーに表示され、同じ作成者によるパッケージの相互参照に使用されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-151">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="f471e-152">メタデータの省略可能な要素</span><span class="sxs-lookup"><span data-stu-id="f471e-152">Optional metadata elements</span></span>

<span data-ttu-id="f471e-153">これらの要素は、`<metadata>` 要素内に表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="f471e-153">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="f471e-154">単一要素</span><span class="sxs-lookup"><span data-stu-id="f471e-154">Single elements</span></span>

| <span data-ttu-id="f471e-155">要素</span><span class="sxs-lookup"><span data-stu-id="f471e-155">Element</span></span> | <span data-ttu-id="f471e-156">説明</span><span class="sxs-lookup"><span data-stu-id="f471e-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f471e-157">**title**</span><span class="sxs-lookup"><span data-stu-id="f471e-157">**title**</span></span> | <span data-ttu-id="f471e-158">人が読みやすいパッケージのタイトル。通常、nuget.org と、Visual Studio のパッケージ マネージャーの UI 画面で使用されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-158">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="f471e-159">指定しないと、パッケージ ID が使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-159">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="f471e-160">**owners**</span><span class="sxs-lookup"><span data-stu-id="f471e-160">**owners**</span></span> | <span data-ttu-id="f471e-161">コンマで区切って指定したパッケージ作成者の一覧。nuget.org でのプロファイル名です。多くの場合は `authors` と同じ一覧であり、nuget.org にパッケージをアップロードするときは無視されます。「[nuget.org でパッケージ所有者を管理する](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-161">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="f471e-162">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="f471e-162">**projectUrl**</span></span> | <span data-ttu-id="f471e-163">パッケージのホーム ページの URL。多くの場合、UI 画面と nuget.org に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-163">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="f471e-164">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="f471e-164">**licenseUrl**</span></span> | <span data-ttu-id="f471e-165">パッケージのライセンスの URL。通常、UI 画面および nuget.org に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-165">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="f471e-166">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="f471e-166">**iconUrl**</span></span> | <span data-ttu-id="f471e-167">UI 表示でパッケージのアイコンとして使われる、背景が透明な 64 x 64 の画像の URL。</span><span class="sxs-lookup"><span data-stu-id="f471e-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="f471e-168">この要素の値は、"*画像を直接示す URL*" であり、画像を含む Web ページの URL ではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f471e-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="f471e-169">たとえば、GitHub からイメージを使用する URL と同様に、raw ファイルを使用して*https://github.com/\<username\>/\<リポジトリ\>/raw/\<ブランチ\>/ \<logo.png\>*です。</span><span class="sxs-lookup"><span data-stu-id="f471e-169">For example, to use an image from GitHub, use the raw file URL like *https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\>*.</span></span> |
| <span data-ttu-id="f471e-170">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="f471e-170">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="f471e-171">パッケージをインストールする前にクライアントがユーザーに対してパッケージのライセンスへの同意を求めるプロンプトを表示する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="f471e-171">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="f471e-172">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="f471e-172">**developmentDependency**</span></span> | <span data-ttu-id="f471e-173">*(2.8 以降)* 開発専用の依存関係としてパッケージをマークするかどうかを指定するブール値。指定すると、そのパッケージは他のパッケージに依存関係として含まれなくなります。</span><span class="sxs-lookup"><span data-stu-id="f471e-173">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="f471e-174">**summary**</span><span class="sxs-lookup"><span data-stu-id="f471e-174">**summary**</span></span> | <span data-ttu-id="f471e-175">UI 画面用のパッケージの短い説明。</span><span class="sxs-lookup"><span data-stu-id="f471e-175">A short description of the package for UI display.</span></span> <span data-ttu-id="f471e-176">省略すると、`description` を切り詰めたバージョンが使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-176">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="f471e-177">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="f471e-177">**releaseNotes**</span></span> | <span data-ttu-id="f471e-178">*(1.5 以降)* このリリースのパッケージで行われた変更の説明。Visual Studio パッケージ マネージャーの **[更新]** タブなどの UI で、パッケージの説明の代わりによく使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="f471e-179">**copyright**</span><span class="sxs-lookup"><span data-stu-id="f471e-179">**copyright**</span></span> | <span data-ttu-id="f471e-180">*(1.5 以降)* パッケージの著作権の詳細。</span><span class="sxs-lookup"><span data-stu-id="f471e-180">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="f471e-181">**language**</span><span class="sxs-lookup"><span data-stu-id="f471e-181">**language**</span></span> | <span data-ttu-id="f471e-182">パッケージのロケール ID。</span><span class="sxs-lookup"><span data-stu-id="f471e-182">The locale ID for the package.</span></span> <span data-ttu-id="f471e-183">「[ローカライズされたパッケージの作成](../create-packages/creating-localized-packages.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="f471e-184">**tags**</span><span class="sxs-lookup"><span data-stu-id="f471e-184">**tags**</span></span> | <span data-ttu-id="f471e-185">パッケージについて説明し、検索やフィルターでパッケージを見つけやすくするタグやキーワードを、スペースで区切って列記したリスト。</span><span class="sxs-lookup"><span data-stu-id="f471e-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="f471e-186">**serviceable**</span><span class="sxs-lookup"><span data-stu-id="f471e-186">**serviceable**</span></span> | <span data-ttu-id="f471e-187">*(3.3 以降)* NuGet 内部でのみ使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-187">*(3.3+)* For internal NuGet use only.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="f471e-188">コレクション要素</span><span class="sxs-lookup"><span data-stu-id="f471e-188">Collection elements</span></span>

| <span data-ttu-id="f471e-189">要素</span><span class="sxs-lookup"><span data-stu-id="f471e-189">Element</span></span> | <span data-ttu-id="f471e-190">説明</span><span class="sxs-lookup"><span data-stu-id="f471e-190">Description</span></span> |
| --- | --- |
<span data-ttu-id="f471e-191">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="f471e-191">**packageTypes**</span></span> | <span data-ttu-id="f471e-192">*(3.5 以降)* 従来の依存関係パッケージ以外の場合に、パッケージの種類を指定する 0 個以上の `<packageType>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="f471e-192">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="f471e-193">各 packageType は、*name* 属性と *version* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="f471e-193">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="f471e-194">「[Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type)」(パッケージの種類の設定) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-194">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="f471e-195">**dependencies**</span><span class="sxs-lookup"><span data-stu-id="f471e-195">**dependencies**</span></span> | <span data-ttu-id="f471e-196">パッケージの依存関係を指定する 0 個以上の `<dependency>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="f471e-196">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="f471e-197">各 dependency は、*id*、*version*、*include* (3.x 以降)、*exclude* (3.x 以降) の各属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="f471e-197">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="f471e-198">後の「[依存関係](#dependencies)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-198">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="f471e-199">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="f471e-199">**frameworkAssemblies**</span></span> | <span data-ttu-id="f471e-200">*(1.2 以降)* このパッケージで必要な .NET Framework アセンブリ参照を示す 0 個以上の `<frameworkAssembly>` 要素のコレクション。パッケージを使うプロジェクトに参照が確実に追加されるようにします。</span><span class="sxs-lookup"><span data-stu-id="f471e-200">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="f471e-201">各 frameworkAssembly は、*assemblyName* 属性と *targetFramework* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="f471e-201">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="f471e-202">[フレームワーク アセンブリ参照 GAC の指定](#specifying-framework-assembly-references-gac)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-202">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="f471e-203">**references**</span><span class="sxs-lookup"><span data-stu-id="f471e-203">**references**</span></span> | <span data-ttu-id="f471e-204">*(1.5 以降)* パッケージの `lib` フォルダー内のアセンブリのうちプロジェクト参照として追加するものを指定する、0 個以上の `<reference>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="f471e-204">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="f471e-205">各参照は、*file* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="f471e-205">Each reference has a *file* attribute.</span></span> <span data-ttu-id="f471e-206">`<references>` は `<group>` 要素を含むこともでき、その *targetFramework* 属性に `<reference>` 要素を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="f471e-206">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="f471e-207">省略すると、`lib` のすべての参照が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f471e-207">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="f471e-208">[明示的なアセンブリ参照の指定](#specifying-explicit-assembly-references)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-208">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="f471e-209">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="f471e-209">**contentFiles**</span></span> | <span data-ttu-id="f471e-210">*(3.3 以降)* 使用する側のプロジェクトに含めるコンテンツ ファイルを示す `<files>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="f471e-210">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="f471e-211">これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-211">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="f471e-212">[パッケージに含めるファイルの指定](#specifying-files-to-include-in-the-package)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-212">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="f471e-213">Files 要素</span><span class="sxs-lookup"><span data-stu-id="f471e-213">Files element</span></span>

<span data-ttu-id="f471e-214">`<package>` ノードでは、`<metadata>` の兄弟として `<files>` ノードを追加するか、または `<metadata>` の子として `<contentFiles>` を追加して、パッケージに含めるアセンブリとコンテンツ ファイルを指定できます。</span><span class="sxs-lookup"><span data-stu-id="f471e-214">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="f471e-215">詳しくは、このトピックで後述する「[アセンブリ ファイルを含める](#including-assembly-files)」と「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-215">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="f471e-216">置換トークン</span><span class="sxs-lookup"><span data-stu-id="f471e-216">Replacement tokens</span></span>

<span data-ttu-id="f471e-217">パッケージを作成するとき、[`nuget pack` コマンド](../tools/cli-ref-pack.md)は、`.nuspec` ファイルの `<metadata>` ノード内の $ で区切られたトークンを、プロジェクト ファイルまたは `pack` コマンドの `-properties` スイッチで指定されている値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f471e-217">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="f471e-218">コマンド ラインでは、`nuget pack -properties <name>=<value>;<name>=<value>` でトークンの値を指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-218">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="f471e-219">たとえば、`.nuspec` では `$owners$` や `$desc$` などのトークンを使っておき、パッキング時に次のようにして値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="f471e-219">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="f471e-220">プロジェクトの値を使うには、次の表で説明するトークンを指定します (AssemblyInfo は、`Properties` 内の `AssemblyInfo.cs` や `AssemblyInfo.vb` などのファイルを参照します)。</span><span class="sxs-lookup"><span data-stu-id="f471e-220">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="f471e-221">これらのトークンを使うには、`nuget pack` を実行するときに、`.nuspec` だけでなくプロジェクト ファイルも指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-221">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="f471e-222">たとえば、次のコマンドを使うと、`.nuspec` ファイルの `$id$` および `$version$` トークンが、プロジェクトの `AssemblyName` および `AssemblyVersion` の値に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="f471e-222">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="f471e-223">通常、プロジェクトがある場合は、最初に `nuget spec MyProject.csproj` を使って `.nuspec` を作成すると、一部の標準的なトークンが自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-223">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="f471e-224">ただし、`.nuspec` の必須要素に対する値がプロジェクトにないと、`nuget pack` は失敗します。</span><span class="sxs-lookup"><span data-stu-id="f471e-224">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="f471e-225">さらに、プロジェクトの値を変更する場合は、パッケージを作成する前に必ずビルドし直してください。これは、pack コマンドの `build` スイッチで簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f471e-225">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="f471e-226">例外である `$configuration$` を除き、コマンド ラインの同じトークンに割り当てられている値より、プロジェクトの値の方が優先的に使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-226">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="f471e-227">トークン</span><span class="sxs-lookup"><span data-stu-id="f471e-227">Token</span></span> | <span data-ttu-id="f471e-228">値のソース</span><span class="sxs-lookup"><span data-stu-id="f471e-228">Value source</span></span> | <span data-ttu-id="f471e-229">[値]</span><span class="sxs-lookup"><span data-stu-id="f471e-229">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="f471e-230">**$id$**</span><span class="sxs-lookup"><span data-stu-id="f471e-230">**$id$**</span></span> | <span data-ttu-id="f471e-231">プロジェクト ファイル</span><span class="sxs-lookup"><span data-stu-id="f471e-231">Project file</span></span> | <span data-ttu-id="f471e-232">プロジェクト ファイルの AssemblyName</span><span class="sxs-lookup"><span data-stu-id="f471e-232">AssemblyName from the project file</span></span> |
| <span data-ttu-id="f471e-233">**$version$**</span><span class="sxs-lookup"><span data-stu-id="f471e-233">**$version$**</span></span> | <span data-ttu-id="f471e-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f471e-234">AssemblyInfo</span></span> | <span data-ttu-id="f471e-235">ある場合は AssemblyInformationalVersion、ない場合は AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="f471e-235">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="f471e-236">**$author$**</span><span class="sxs-lookup"><span data-stu-id="f471e-236">**$author$**</span></span> | <span data-ttu-id="f471e-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f471e-237">AssemblyInfo</span></span> | <span data-ttu-id="f471e-238">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="f471e-238">AssemblyCompany</span></span> |
| <span data-ttu-id="f471e-239">**$description$**</span><span class="sxs-lookup"><span data-stu-id="f471e-239">**$description$**</span></span> | <span data-ttu-id="f471e-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f471e-240">AssemblyInfo</span></span> | <span data-ttu-id="f471e-241">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="f471e-241">AssemblyDescription</span></span> |
| <span data-ttu-id="f471e-242">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="f471e-242">**$copyright$**</span></span> | <span data-ttu-id="f471e-243">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f471e-243">AssemblyInfo</span></span> | <span data-ttu-id="f471e-244">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="f471e-244">AssemblyCopyright</span></span> |
| <span data-ttu-id="f471e-245">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="f471e-245">**$configuration$**</span></span> | <span data-ttu-id="f471e-246">アセンブリ DLL</span><span class="sxs-lookup"><span data-stu-id="f471e-246">Assembly DLL</span></span> | <span data-ttu-id="f471e-247">アセンブリのビルドに使われる構成。既定値は Debug。</span><span class="sxs-lookup"><span data-stu-id="f471e-247">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="f471e-248">Release 構成を使ってパッケージを作成するには、常にコマンド ラインで `-properties Configuration=Release` を使うことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f471e-248">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="f471e-249">[アセンブリ ファイル](#including-assembly-files)および[コンテンツ ファイル](#including-content-files)を含めるときは、トークンを使ってパスを解決することもできます。</span><span class="sxs-lookup"><span data-stu-id="f471e-249">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="f471e-250">トークンの名前は MSBuild のプロパティと同じであり、現在のビルド構成に基づいて含めるファイルを選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="f471e-250">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="f471e-251">たとえば、`.nuspec` ファイルで次のトークンを使うものとします。</span><span class="sxs-lookup"><span data-stu-id="f471e-251">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="f471e-252">そして、MSBuild で `AssemblyName` が `LoggingLibrary` であるアセンブリを `Release` 構成でビルドすると、パッケージ内の `.nuspec` ファイルの行は結果として次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f471e-252">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="f471e-253">依存関係</span><span class="sxs-lookup"><span data-stu-id="f471e-253">Dependencies</span></span>

<span data-ttu-id="f471e-254">`<metadata>` 内の `<dependencies>` 要素は、最上位のパッケージが依存している他のパッケージを示す `<dependency>` 要素をいくつでも含むことができます。</span><span class="sxs-lookup"><span data-stu-id="f471e-254">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="f471e-255">各 `<dependency>` の属性は次にとおりです。</span><span class="sxs-lookup"><span data-stu-id="f471e-255">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="f471e-256">属性</span><span class="sxs-lookup"><span data-stu-id="f471e-256">Attribute</span></span> | <span data-ttu-id="f471e-257">説明</span><span class="sxs-lookup"><span data-stu-id="f471e-257">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="f471e-258">(必須) "EntityFramework" や "NUnit" などの依存関係のパッケージ ID。これはパッケージ ページに表示されるパッケージ nuget.org の名前となります。</span><span class="sxs-lookup"><span data-stu-id="f471e-258">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="f471e-259">(必須) 依存関係として許容されるバージョンの範囲。</span><span class="sxs-lookup"><span data-stu-id="f471e-259">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="f471e-260">厳密な構文については、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」(パッケージのバージョン管理) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-260">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="f471e-261">include</span><span class="sxs-lookup"><span data-stu-id="f471e-261">include</span></span> | <span data-ttu-id="f471e-262">最終的なパッケージに含める依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="f471e-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="f471e-263">既定値は `none` です。</span><span class="sxs-lookup"><span data-stu-id="f471e-263">The default value is `none`.</span></span> |
| <span data-ttu-id="f471e-264">exclude</span><span class="sxs-lookup"><span data-stu-id="f471e-264">exclude</span></span> | <span data-ttu-id="f471e-265">最終的なパッケージから除外する依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="f471e-265">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="f471e-266">既定値は `all` です。</span><span class="sxs-lookup"><span data-stu-id="f471e-266">The  default value is `all`.</span></span> <span data-ttu-id="f471e-267">`exclude` で指定されているタグの方が、`include` で指定されているタグより優先されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-267">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="f471e-268">たとえば、`include="runtime, compile" exclude="compile"` は `include="runtime"` と同じです。</span><span class="sxs-lookup"><span data-stu-id="f471e-268">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="f471e-269">包含/除外タグ</span><span class="sxs-lookup"><span data-stu-id="f471e-269">Include/Exclude tag</span></span> | <span data-ttu-id="f471e-270">ターゲットの影響を受けるフォルダー</span><span class="sxs-lookup"><span data-stu-id="f471e-270">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="f471e-271">contentFiles</span><span class="sxs-lookup"><span data-stu-id="f471e-271">contentFiles</span></span> | <span data-ttu-id="f471e-272">Content</span><span class="sxs-lookup"><span data-stu-id="f471e-272">Content</span></span>  |
| <span data-ttu-id="f471e-273">ランタイム</span><span class="sxs-lookup"><span data-stu-id="f471e-273">runtime</span></span> | <span data-ttu-id="f471e-274">Runtime、Resources、FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="f471e-274">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="f471e-275">compile</span><span class="sxs-lookup"><span data-stu-id="f471e-275">compile</span></span> | <span data-ttu-id="f471e-276">lib</span><span class="sxs-lookup"><span data-stu-id="f471e-276">lib</span></span> |
| <span data-ttu-id="f471e-277">ビルド</span><span class="sxs-lookup"><span data-stu-id="f471e-277">build</span></span> | <span data-ttu-id="f471e-278">build (MSBuild のプロパティとターゲット)</span><span class="sxs-lookup"><span data-stu-id="f471e-278">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="f471e-279">native</span><span class="sxs-lookup"><span data-stu-id="f471e-279">native</span></span> | <span data-ttu-id="f471e-280">native</span><span class="sxs-lookup"><span data-stu-id="f471e-280">native</span></span> |
| <span data-ttu-id="f471e-281">none</span><span class="sxs-lookup"><span data-stu-id="f471e-281">none</span></span> | <span data-ttu-id="f471e-282">フォルダーなし</span><span class="sxs-lookup"><span data-stu-id="f471e-282">No folders</span></span> |
| <span data-ttu-id="f471e-283">すべて</span><span class="sxs-lookup"><span data-stu-id="f471e-283">all</span></span> | <span data-ttu-id="f471e-284">すべてのフォルダー</span><span class="sxs-lookup"><span data-stu-id="f471e-284">All folders</span></span> |

<span data-ttu-id="f471e-285">たとえば、次の行は `PackageA` バージョン 1.1.0 以降および `PackageB` バージョン 1.x での依存関係を示します。</span><span class="sxs-lookup"><span data-stu-id="f471e-285">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="f471e-286">次の行も同じパッケージでの依存関係を示しますが、`PackageA` の `contentFiles` および `build` フォルダーを含めて、`PackageB` の `native` および `compile` フォルダーを除くすべてを含めることを指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-286">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="f471e-287">注: `nuget spec` を使ってプロジェクトから `.nuspec` を作成すると、そのプロジェクトに存在する依存関係が結果の `.nuspec` ファイルに自動的に含まれます。</span><span class="sxs-lookup"><span data-stu-id="f471e-287">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="f471e-288">依存関係グループ</span><span class="sxs-lookup"><span data-stu-id="f471e-288">Dependency groups</span></span>

<span data-ttu-id="f471e-289">*バージョン 2.0 以降*</span><span class="sxs-lookup"><span data-stu-id="f471e-289">*Version 2.0+*</span></span>

<span data-ttu-id="f471e-290">1 つのフラット リストの代わりに、`<dependencies>` の `<group>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って依存関係を指定できます。</span><span class="sxs-lookup"><span data-stu-id="f471e-290">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="f471e-291">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<dependency>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f471e-291">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="f471e-292">ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの依存関係が一緒にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="f471e-292">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="f471e-293">依存関係の既定のリストまたはフォールバック リストとしては、`targetFramework` 属性のない `<group>` 要素が使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-293">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="f471e-294">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-294">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="f471e-295">グループの形式をフラット リストと併用することはできません。</span><span class="sxs-lookup"><span data-stu-id="f471e-295">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="f471e-296">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="f471e-296">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="f471e-297">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="f471e-297">Explicit assembly references</span></span>

<span data-ttu-id="f471e-298">`<references>` 要素は、パッケージを使うときにターゲット プロジェクトが参照する必要のあるアセンブリを明示的に指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-298">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="f471e-299">この要素がある場合、NuGet は一覧で指定されているアセンブリのみへの参照を追加します。パッケージの `lib` フォルダーに含まれる他のアセンブリに対する参照は追加されません。</span><span class="sxs-lookup"><span data-stu-id="f471e-299">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="f471e-300">たとえば、次の `<references>` 要素は、パッケージに他のアセンブリがある場合でも、`xunit.dll` と `xunit.extensions.dll` に対する参照だけを追加するよう NuGet に指示します。</span><span class="sxs-lookup"><span data-stu-id="f471e-300">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="f471e-301">明示的な参照は、通常、設計時のみのアセンブリに使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-301">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="f471e-302">たとえば、[コード コントラクト](/dotnet/framework/debug-trace-profile/code-contracts)を使うときは、Visual Studio がコントラクト アセンブリを検出できるように、コントラクト アセンブリはそれが拡張するランタイム アセンブリの隣に存在する必要がありますが、プロジェクトでコントラクト アセンブリを参照したり、プロジェクトの `bin` フォルダーにコントラクト アセンブリをコピーしたりする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f471e-302">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="f471e-303">同様に、明示的な参照は XUnit などの単体テスト フレームワークに使うことができ、その場合、ツール アセンブリはランタイム アセンブリの隣に存在する必要がありますが、プロジェクト参照として含まれる必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f471e-303">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="f471e-304">[参照グループ]</span><span class="sxs-lookup"><span data-stu-id="f471e-304">Reference groups</span></span>

<span data-ttu-id="f471e-305">1 つのフラット リストの代わりに、`<references>` の `<group>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って参照を指定できます。</span><span class="sxs-lookup"><span data-stu-id="f471e-305">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="f471e-306">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<reference>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f471e-306">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="f471e-307">ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの参照はプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-307">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="f471e-308">参照の既定のリストまたはフォールバック リストとしては、`targetFramework` 属性のない `<group>` 要素が使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-308">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="f471e-309">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-309">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="f471e-310">グループの形式をフラット リストと併用することはできません。</span><span class="sxs-lookup"><span data-stu-id="f471e-310">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="f471e-311">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="f471e-311">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="f471e-312">フレームワーク アセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="f471e-312">Framework assembly references</span></span>

<span data-ttu-id="f471e-313">フレームワーク アセンブリは、.NET Framework の一部であり、指定されたコンピューターのグローバル アセンブリ キャッシュ (GAC) に既に存在している必要があります。</span><span class="sxs-lookup"><span data-stu-id="f471e-313">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="f471e-314">`<frameworkAssemblies>` 要素でこれらのアセンブリを指定することにより、プロジェクトに必要な参照がまだない場合であっても、そのような参照をプロジェクトに確実に追加できます。</span><span class="sxs-lookup"><span data-stu-id="f471e-314">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="f471e-315">もちろん、そのようなアセンブリがパッケージに直接含まれることはありません。</span><span class="sxs-lookup"><span data-stu-id="f471e-315">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="f471e-316">`<frameworkAssemblies>` 要素には 0 個以上の `<frameworkAssembly>` 要素を含めることができ、それぞれで次の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-316">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="f471e-317">属性</span><span class="sxs-lookup"><span data-stu-id="f471e-317">Attribute</span></span> | <span data-ttu-id="f471e-318">説明</span><span class="sxs-lookup"><span data-stu-id="f471e-318">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f471e-319">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="f471e-319">**assemblyName**</span></span> | <span data-ttu-id="f471e-320">(必須) 完全修飾アセンブリ名。</span><span class="sxs-lookup"><span data-stu-id="f471e-320">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="f471e-321">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="f471e-321">**targetFramework**</span></span> | <span data-ttu-id="f471e-322">(省略可能) この参照を適用するターゲット フレームワークを指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-322">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="f471e-323">省略した場合は、参照がすべてのフレームワークに適用されることを示します。</span><span class="sxs-lookup"><span data-stu-id="f471e-323">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="f471e-324">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-324">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="f471e-325">次の例は、`System.Net` への参照はすべてのターゲット フレームワークに適用され、`System.ServiceModel` への参照は .NET Framework 4.0 のみに適用されることを示します。</span><span class="sxs-lookup"><span data-stu-id="f471e-325">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="f471e-326">アセンブリ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="f471e-326">Including assembly files</span></span>

<span data-ttu-id="f471e-327">「[パッケージを作成する](../create-packages/creating-a-package.md)」で説明されている規則に従う場合、`.nuspec` ファイルでファイルの一覧を明示的に指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f471e-327">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="f471e-328">`nuget pack` コマンドが必要なファイルを自動的に選びます。</span><span class="sxs-lookup"><span data-stu-id="f471e-328">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="f471e-329">プロジェクトにパッケージをインストールするとき、NuGet はパッケージの DLL にアセンブリ参照を自動的に追加します。ただし、指定されている `.resources.dll` は、ローカライズされたサテライト アセンブリであると見なされるため "*除外*" されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-329">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="f471e-330">そのため、避けなければ不可欠なパッケージ コードが含まれてしまうファイルには `.resources.dll` を使わないようにします。</span><span class="sxs-lookup"><span data-stu-id="f471e-330">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="f471e-331">この自動動作をバイパスして、パッケージに含めるファイルを明示的に制御するには、`<files>` 要素を `<package>` の子要素 (および `<metadata>` の兄弟要素) として配置し、各ファイルを個別の `<file>` 要素で示します。</span><span class="sxs-lookup"><span data-stu-id="f471e-331">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="f471e-332">例:</span><span class="sxs-lookup"><span data-stu-id="f471e-332">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="f471e-333">NuGet 2.x 以前および `packages.config` を使っているプロジェクトでは、`<files>` 要素はパッケージのインストール時に変更できないコンテンツ ファイルを含めるためにも使われます。</span><span class="sxs-lookup"><span data-stu-id="f471e-333">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="f471e-334">NuGet 3.3 以降で、PackageReference を使用しているプロジェクトでは、代わりに `<contentFiles>` 要素が使用されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-334">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="f471e-335">詳しくは、後の「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-335">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="f471e-336">File 要素の属性</span><span class="sxs-lookup"><span data-stu-id="f471e-336">File element attributes</span></span>

<span data-ttu-id="f471e-337">各 `<file>` 要素では、次の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-337">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="f471e-338">属性</span><span class="sxs-lookup"><span data-stu-id="f471e-338">Attribute</span></span> | <span data-ttu-id="f471e-339">説明</span><span class="sxs-lookup"><span data-stu-id="f471e-339">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f471e-340">**src**</span><span class="sxs-lookup"><span data-stu-id="f471e-340">**src**</span></span> | <span data-ttu-id="f471e-341">含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。</span><span class="sxs-lookup"><span data-stu-id="f471e-341">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="f471e-342">絶対パスを指定しない限り、パスは `.nuspec` ファイルが基準になります。</span><span class="sxs-lookup"><span data-stu-id="f471e-342">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="f471e-343">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="f471e-343">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="f471e-344">**target**</span><span class="sxs-lookup"><span data-stu-id="f471e-344">**target**</span></span> | <span data-ttu-id="f471e-345">ソース ファイルが格納されるパッケージ内のフォルダーへの相対パス。`lib`、`content`、`build`、または `tools` で始まっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f471e-345">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="f471e-346">[規則に基づく作業ディレクトリからの .nuspec の作成](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f471e-346">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="f471e-347">**exclude**</span><span class="sxs-lookup"><span data-stu-id="f471e-347">**exclude**</span></span> | <span data-ttu-id="f471e-348">`src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。</span><span class="sxs-lookup"><span data-stu-id="f471e-348">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="f471e-349">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="f471e-349">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="f471e-350">使用例</span><span class="sxs-lookup"><span data-stu-id="f471e-350">Examples</span></span>

<span data-ttu-id="f471e-351">**1 つのアセンブリ**</span><span class="sxs-lookup"><span data-stu-id="f471e-351">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="f471e-352">**ターゲット フレームワークに固有の 1 つのアセンブリ**</span><span class="sxs-lookup"><span data-stu-id="f471e-352">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="f471e-353">**ワイルドカードを使った DLL のセット**</span><span class="sxs-lookup"><span data-stu-id="f471e-353">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="f471e-354">**異なるフレームワークの DLL**</span><span class="sxs-lookup"><span data-stu-id="f471e-354">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="f471e-355">**ファイルの除外**</span><span class="sxs-lookup"><span data-stu-id="f471e-355">**Excluding files**</span></span>

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="f471e-356">コンテンツ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="f471e-356">Including content files</span></span>

<span data-ttu-id="f471e-357">コンテンツ ファイルは、パッケージでプロジェクトに含める必要がある変更できないファイルです。</span><span class="sxs-lookup"><span data-stu-id="f471e-357">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="f471e-358">変更できないので、それを使うプロジェクトによる変更は意図されていません。</span><span class="sxs-lookup"><span data-stu-id="f471e-358">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="f471e-359">コンテンツ ファイルの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="f471e-359">Example content files include:</span></span>

- <span data-ttu-id="f471e-360">リソースとして埋め込まれる画像</span><span class="sxs-lookup"><span data-stu-id="f471e-360">Images that are embedded as resources</span></span>
- <span data-ttu-id="f471e-361">コンパイル済みのソース ファイル</span><span class="sxs-lookup"><span data-stu-id="f471e-361">Source files that are already compiled</span></span>
- <span data-ttu-id="f471e-362">プロジェクトのビルド出力と共に含まれる必要があるスクリプト</span><span class="sxs-lookup"><span data-stu-id="f471e-362">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="f471e-363">プロジェクトに含まれる必要はあるが、プロジェクト固有の変更は必要ない、パッケージの構成ファイル</span><span class="sxs-lookup"><span data-stu-id="f471e-363">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="f471e-364">コンテンツ ファイルをパッケージに含めるには、`<files>` 要素を使い、`target` 属性で `content` フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-364">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="f471e-365">ただし、PackageReference を使用しているプロジェクトにパッケージをインストールする場合、このようなファイルは無視され、代わりに `<contentFiles>` 要素が使用されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-365">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="f471e-366">使用する側のプロジェクトとの最大限の互換性のため、パッケージでは両方の要素でコンテンツ ファイルを指定するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="f471e-366">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="f471e-367">コンテンツ ファイルに対する files 要素の使用</span><span class="sxs-lookup"><span data-stu-id="f471e-367">Using the files element for content files</span></span>

<span data-ttu-id="f471e-368">コンテンツ ファイルでは、アセンブリ ファイルの場合と同じ形式を使用しますが、次の例のように、`target` 属性で基本フォルダーとして `content` を指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-368">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="f471e-369">**基本的なコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="f471e-369">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="f471e-370">**ディレクトリ構造を持つコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="f471e-370">**Content files with directory structure**</span></span>

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

<span data-ttu-id="f471e-371">**ターゲット フレームワークに固有のコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="f471e-371">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="f471e-372">**名前のドットでフォルダーにコピーされるコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="f471e-372">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="f471e-373">この場合、NuGet は `target` の拡張子が `src` の拡張子と一致しないものと判断し、`target` での名前のその部分をフォルダーとして扱います。</span><span class="sxs-lookup"><span data-stu-id="f471e-373">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="f471e-374">**拡張子のないコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="f471e-374">**Content files without extensions**</span></span>

<span data-ttu-id="f471e-375">拡張子のないファイルを含めるには、ワイルドカード `*` または `**` を使います。</span><span class="sxs-lookup"><span data-stu-id="f471e-375">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="f471e-376">**深いパスと深いターゲットのコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="f471e-376">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="f471e-377">この場合、ソースとターゲットのファイル拡張子が一致するので、NuGet はターゲットがフォルダーではなくファイル名であると想定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-377">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="f471e-378">**パッケージ内のコンテンツ ファイルの名前の変更**</span><span class="sxs-lookup"><span data-stu-id="f471e-378">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="f471e-379">**ファイルの除外**</span><span class="sxs-lookup"><span data-stu-id="f471e-379">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="f471e-380">コンテンツ ファイルに対する contentFiles 要素の使用</span><span class="sxs-lookup"><span data-stu-id="f471e-380">Using the contentFiles element for content files</span></span>

<span data-ttu-id="f471e-381">*NuGet 4.0 以降で、PackageReference を使用している場合*</span><span class="sxs-lookup"><span data-stu-id="f471e-381">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="f471e-382">既定では、パッケージはコンテンツを `contentFiles` フォルダーに配置し (下記参照)、`nuget pack` は既定の属性を使ってそのフォルダーにすべてのファイルを格納します。</span><span class="sxs-lookup"><span data-stu-id="f471e-382">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="f471e-383">この場合は、`contentFiles` ノードを `.nuspec` に含める必要はまったくありません。</span><span class="sxs-lookup"><span data-stu-id="f471e-383">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="f471e-384">含まれるファイルを制御するには、含めるファイルを厳密に示す `<files>` 要素のコレクションである `<contentFiles>` 要素を指定します。</span><span class="sxs-lookup"><span data-stu-id="f471e-384">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="f471e-385">これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-385">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="f471e-386">属性</span><span class="sxs-lookup"><span data-stu-id="f471e-386">Attribute</span></span> | <span data-ttu-id="f471e-387">説明</span><span class="sxs-lookup"><span data-stu-id="f471e-387">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f471e-388">**include**</span><span class="sxs-lookup"><span data-stu-id="f471e-388">**include**</span></span> | <span data-ttu-id="f471e-389">(必須) 含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。</span><span class="sxs-lookup"><span data-stu-id="f471e-389">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="f471e-390">絶対パスを指定しない限り、パスは `.nuspec` ファイルが基準になります。</span><span class="sxs-lookup"><span data-stu-id="f471e-390">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="f471e-391">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="f471e-391">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="f471e-392">**exclude**</span><span class="sxs-lookup"><span data-stu-id="f471e-392">**exclude**</span></span> | <span data-ttu-id="f471e-393">`src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。</span><span class="sxs-lookup"><span data-stu-id="f471e-393">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="f471e-394">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="f471e-394">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="f471e-395">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="f471e-395">**buildAction**</span></span> | <span data-ttu-id="f471e-396">MSBuild のコンテンツ項目に割り当てるビルド アクション。`Content`、`None`、`Embedded Resource`、`Compile` などです。既定値は、`Compile` です。</span><span class="sxs-lookup"><span data-stu-id="f471e-396">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="f471e-397">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="f471e-397">**copyToOutput**</span></span> | <span data-ttu-id="f471e-398">ビルド出力フォルダーにコンテンツ項目をコピーするかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="f471e-398">A Boolean indicating whether to copy content items to the build output folder.</span></span> <span data-ttu-id="f471e-399">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="f471e-399">The default is false.</span></span> |
| <span data-ttu-id="f471e-400">**flatten**</span><span class="sxs-lookup"><span data-stu-id="f471e-400">**flatten**</span></span> | <span data-ttu-id="f471e-401">コンテンツ項目をビルド出力の単一フォルダーにコピーするか (true)、それともパッケージのフォルダー構造を保持するか (false) を示すブール値。</span><span class="sxs-lookup"><span data-stu-id="f471e-401">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="f471e-402">このフラグは、copyToOutput が true に設定されている場合のみ機能します。</span><span class="sxs-lookup"><span data-stu-id="f471e-402">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="f471e-403">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="f471e-403">The default is false.</span></span> |

<span data-ttu-id="f471e-404">パッケージをインストールするとき、NuGet は `<contentFiles>` の子要素を上から下に順番に適用します。</span><span class="sxs-lookup"><span data-stu-id="f471e-404">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="f471e-405">複数のエントリが同じファイルに一致する場合は、すべてのエントリが適用されます。</span><span class="sxs-lookup"><span data-stu-id="f471e-405">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="f471e-406">同じ属性に対して競合がある場合は、最上位のエントリが下位のエントリを上書きします。</span><span class="sxs-lookup"><span data-stu-id="f471e-406">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="f471e-407">パッケージ フォルダーの構造</span><span class="sxs-lookup"><span data-stu-id="f471e-407">Package folder structure</span></span>

<span data-ttu-id="f471e-408">パッケージ プロジェクトでは、次のパターンを使ってコンテンツを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f471e-408">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="f471e-409">`codeLanguages` には、`cs`、`vb`、`fs`、`any`、または指定された `$(ProjectLanguage)` に相当する小文字表現を指定できます。</span><span class="sxs-lookup"><span data-stu-id="f471e-409">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="f471e-410">`TxM` は、NuGet がサポートする任意の有効なターゲット フレームワーク モニカーです (「[ターゲット フレームワーク](../reference/target-frameworks.md)」を参照)。</span><span class="sxs-lookup"><span data-stu-id="f471e-410">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="f471e-411">この構文の末尾に、任意のフォルダー構造を追加できます。</span><span class="sxs-lookup"><span data-stu-id="f471e-411">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="f471e-412">例:</span><span class="sxs-lookup"><span data-stu-id="f471e-412">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="f471e-413">空のフォルダーでは、`.` を使って、言語と TxM の特定の組み合わせにコンテンツを提供しないようにすることができます。次はその例です。</span><span class="sxs-lookup"><span data-stu-id="f471e-413">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="f471e-414">contentFiles セクションの例</span><span class="sxs-lookup"><span data-stu-id="f471e-414">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="f471e-415">.nuspec ファイルの例</span><span class="sxs-lookup"><span data-stu-id="f471e-415">Example .nuspec files</span></span>

<span data-ttu-id="f471e-416">**依存関係またはファイルを指定しない単純な `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="f471e-416">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="f471e-417">**依存関係を含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="f471e-417">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="f471e-418">**ファイルを含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="f471e-418">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="f471e-419">**フレームワーク アセンブリを含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="f471e-419">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="f471e-420">この例では、指定したプロジェクト ターゲットに次のものがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="f471e-420">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="f471e-421">.NET4 -> `System.Web`、`System.Net`</span><span class="sxs-lookup"><span data-stu-id="f471e-421">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="f471e-422">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="f471e-422">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="f471e-423">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="f471e-423">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="f471e-424">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="f471e-424">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="f471e-425">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="f471e-425">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
