---
title: NuGet の .nuspec ファイル リファレンス
description: .nuspec ファイルには、パッケージを作成するとき、およびパッケージのコンシューマーに情報を提供するために使われる、パッケージのメタデータが含まれています。
author: karann-msft
ms.author: karann
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 009be99a1c6623a00b4bdbe6db3164ca70782212
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324904"
---
# <a name="nuspec-reference"></a><span data-ttu-id="29e5a-103">.nuspec リファレンス</span><span class="sxs-lookup"><span data-stu-id="29e5a-103">.nuspec reference</span></span>

<span data-ttu-id="29e5a-104">`.nuspec` ファイルは、パッケージのメタデータが含まれている XML マニフェストです。</span><span class="sxs-lookup"><span data-stu-id="29e5a-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="29e5a-105">このマニフェストは、パッケージを作成するためと、コンシューマーに情報を提供するための、両方に使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="29e5a-106">パッケージにはマニフェストが常に含まれています。</span><span class="sxs-lookup"><span data-stu-id="29e5a-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="29e5a-107">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="29e5a-107">In this topic:</span></span>

- [<span data-ttu-id="29e5a-108">一般的な形式とスキーマ</span><span class="sxs-lookup"><span data-stu-id="29e5a-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="29e5a-109">[置換トークン](#replacement-tokens) (Visual Studio プロジェクトで使われるとき)</span><span class="sxs-lookup"><span data-stu-id="29e5a-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="29e5a-110">依存関係</span><span class="sxs-lookup"><span data-stu-id="29e5a-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="29e5a-111">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="29e5a-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="29e5a-112">フレームワーク アセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="29e5a-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="29e5a-113">アセンブリ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="29e5a-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="29e5a-114">コンテンツ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="29e5a-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="29e5a-115">Nuspec ファイルの例</span><span class="sxs-lookup"><span data-stu-id="29e5a-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="29e5a-116">一般的な形式とスキーマ</span><span class="sxs-lookup"><span data-stu-id="29e5a-116">General form and schema</span></span>

<span data-ttu-id="29e5a-117">最新の `nuspec.xsd` スキーマ ファイルは、[NuGet GitHub リポジトリ](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)にあります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="29e5a-118">このスキーマでの `.nuspec` ファイルの一般的な形式は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="29e5a-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="29e5a-119">スキーマの視覚的な表現をはっきり表示したい場合は、Visual Studio のデザイン モードでスキーマ ファイルを開き、**[XML スキーマ エクスプローラー]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="29e5a-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="29e5a-120">または、コードとしてファイルを開き、エディター内を右クリックして、**[XML スキーマ エクスプローラーで表示]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="29e5a-121">どちらの方法でも次のように表示されます (ほとんどを展開した場合)。</span><span class="sxs-lookup"><span data-stu-id="29e5a-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio のスキーマ エクスプローラーで開いた nuspec.xsd](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="29e5a-123">メタデータの必須要素</span><span class="sxs-lookup"><span data-stu-id="29e5a-123">Required metadata elements</span></span>

<span data-ttu-id="29e5a-124">以下の要素はパッケージの最低要件であり、[メタデータの省略可能な要素](#optional-metadata-elements)を追加してパッケージに関する開発者の全体的なエクスペリエンスを向上させることを検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-124">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="29e5a-125">これらの要素は、`<metadata>` 要素内で指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-125">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="29e5a-126">ID</span><span class="sxs-lookup"><span data-stu-id="29e5a-126">id</span></span> 
<span data-ttu-id="29e5a-127">パッケージの識別子。大文字と小文字が区別されます。nuget.org 全体で、またはパッケージが存在するギャラリー全体で、一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-127">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="29e5a-128">ID は、スペースまたは URL で無効な文字を含んでいてはならず、一般に .NET 名前空間の規則に従います。</span><span class="sxs-lookup"><span data-stu-id="29e5a-128">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="29e5a-129">ガイダンスについては、[一意のパッケージ識別子の選択](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-129">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="29e5a-130">version</span><span class="sxs-lookup"><span data-stu-id="29e5a-130">version</span></span>
<span data-ttu-id="29e5a-131">パッケージのバージョン。*major.minor.patch* のパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="29e5a-131">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="29e5a-132">「[Package versioning](../reference/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) で説明されているように、バージョン番号にはプレリリースのサフィックスを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-132">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="29e5a-133">説明</span><span class="sxs-lookup"><span data-stu-id="29e5a-133">description</span></span>
<span data-ttu-id="29e5a-134">UI 画面用のパッケージの長い説明。</span><span class="sxs-lookup"><span data-stu-id="29e5a-134">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="29e5a-135">作成者</span><span class="sxs-lookup"><span data-stu-id="29e5a-135">authors</span></span>
<span data-ttu-id="29e5a-136">パッケージ作成者の一覧。コンマで区切られています。nuget.org のプロファイル名と一致します。これらは nuget.org の NuGet ギャラリーに表示され、同じ作成者によるパッケージの相互参照に使用されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-136">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="29e5a-137">メタデータの省略可能な要素</span><span class="sxs-lookup"><span data-stu-id="29e5a-137">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="29e5a-138">タイトル</span><span class="sxs-lookup"><span data-stu-id="29e5a-138">title</span></span>
<span data-ttu-id="29e5a-139">人が読みやすいパッケージのタイトル。通常、nuget.org と、Visual Studio のパッケージ マネージャーの UI 画面で使用されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="29e5a-140">指定しないと、パッケージ ID が使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-140">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="29e5a-141">owners</span><span class="sxs-lookup"><span data-stu-id="29e5a-141">owners</span></span>
<span data-ttu-id="29e5a-142">コンマで区切って指定したパッケージ作成者の一覧。nuget.org でのプロファイル名です。多くの場合は `authors` と同じ一覧であり、nuget.org にパッケージをアップロードするときは無視されます。「[nuget.org でパッケージ所有者を管理する](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-142">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="29e5a-143">projectUrl</span><span class="sxs-lookup"><span data-stu-id="29e5a-143">projectUrl</span></span>
<span data-ttu-id="29e5a-144">パッケージのホーム ページの URL。多くの場合、UI 画面と nuget.org に表示されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-144">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="29e5a-145">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="29e5a-145">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="29e5a-146">licenseUrl は非推奨とされています。</span><span class="sxs-lookup"><span data-stu-id="29e5a-146">licenseUrl is being deprecated.</span></span> <span data-ttu-id="29e5a-147">ライセンスを使用してください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-147">Use license instead.</span></span>

<span data-ttu-id="29e5a-148">パッケージのライセンスの URL。通常、UI 画面および nuget.org に表示されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-148">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="license"></a><span data-ttu-id="29e5a-149">ライセンス</span><span class="sxs-lookup"><span data-stu-id="29e5a-149">license</span></span>
<span data-ttu-id="29e5a-150">SPDX ライセンス式、または UI 表示や nuget.org によく表示されるパッケージ内でのライセンス ファイルのパスを指定します。BSD-2-句または MIT などの一般的なライセンスの下でパッケージをライセンスする場合は、関連付けられている SPDX ライセンス識別子を使用します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-150">An SPDX license expression or path to a license file within the package, often shown in UI displays as well as nuget.org. If you’re licensing the package under a common license such as BSD-2-Clause or MIT, use the associated SPDX license identifier.</span></span><br><span data-ttu-id="29e5a-151">例: `<license type="expression">MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="29e5a-151">For example: `<license type="expression">MIT</license>`</span></span>

<span data-ttu-id="29e5a-152">完全な一覧を次に示します[SPDX ライセンス識別子](https://spdx.org/licenses/)します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-152">Here is the complete list of [SPDX license identifiers](https://spdx.org/licenses/).</span></span> <span data-ttu-id="29e5a-153">NuGet.org は OSI のみを受け入れるか、承認 FSF ライセンスを使用する場合のライセンスの種類を示す。</span><span class="sxs-lookup"><span data-stu-id="29e5a-153">NuGet.org accepts only OSI or FSF approved licenses when using license type expression.</span></span>

<span data-ttu-id="29e5a-154">複合のライセンスを使用して、指定するには、パッケージは、複数の一般的なライセンス下でライセンスが場合、 [SPDX 式構文のバージョン 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-154">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span><br><span data-ttu-id="29e5a-155">例: `<license type="expression">BSD-2-Clause OR MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="29e5a-155">For example: `<license type="expression">BSD-2-Clause OR MIT</license>`</span></span>

<span data-ttu-id="29e5a-156">SPDX 識別子が割り当てられていないライセンスを使用している、またはカスタムのライセンスは、ライセンスのテキストを持つファイルをパッケージ化できます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-156">If you are using a license that hasn’t been assigned an SPDX identifier, or it is a custom license, you can package a file with the license text.</span></span> <span data-ttu-id="29e5a-157">例:</span><span class="sxs-lookup"><span data-stu-id="29e5a-157">For example:</span></span>
```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="29e5a-158">MSBuild と同じを参照してください[ライセンス式またはライセンス ファイルをパッキング](msbuild-targets.md#packing-a-license-expression-or-a-license-file)します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-158">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="29e5a-159">NuGet のライセンスの式の正確な構文は以下の説明で[ABNF](https://tools.ietf.org/html/rfc5234)します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-159">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="29e5a-160">iconUrl</span><span class="sxs-lookup"><span data-stu-id="29e5a-160">iconUrl</span></span>
<span data-ttu-id="29e5a-161">UI 表示でパッケージのアイコンとして使われる、背景が透明な 64 x 64 の画像の URL。</span><span class="sxs-lookup"><span data-stu-id="29e5a-161">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="29e5a-162">この要素の値は、"*画像を直接示す URL*" であり、画像を含む Web ページの URL ではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-162">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="29e5a-163">たとえば、GitHub からのイメージを使用する URL などの生ファイルを使用して <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-163">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="29e5a-164">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="29e5a-164">requireLicenseAcceptance</span></span>
<span data-ttu-id="29e5a-165">パッケージをインストールする前にクライアントがユーザーに対してパッケージのライセンスへの同意を求めるプロンプトを表示する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="29e5a-165">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="29e5a-166">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="29e5a-166">developmentDependency</span></span>
<span data-ttu-id="29e5a-167">*(2.8 以降)* 開発専用の依存関係としてパッケージをマークするかどうかを指定するブール値。指定すると、そのパッケージは他のパッケージに依存関係として含まれなくなります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-167">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="29e5a-168">Packagereference (NuGet 4.8 以降) の場合、コンパイルからコンパイル アセットを除外することをこのフラグも意味します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-168">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="29e5a-169">参照してください[DevelopmentDependency PackageReference のサポート](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="29e5a-169">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>
#### <a name="summary"></a><span data-ttu-id="29e5a-170">概要</span><span class="sxs-lookup"><span data-stu-id="29e5a-170">summary</span></span>
<span data-ttu-id="29e5a-171">UI 画面用のパッケージの短い説明。</span><span class="sxs-lookup"><span data-stu-id="29e5a-171">A short description of the package for UI display.</span></span> <span data-ttu-id="29e5a-172">省略すると、`description` を切り詰めたバージョンが使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-172">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="29e5a-173">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="29e5a-173">releaseNotes</span></span>
<span data-ttu-id="29e5a-174">*(1.5 以降)* このリリースのパッケージで行われた変更の説明。Visual Studio パッケージ マネージャーの **[更新]** タブなどの UI で、パッケージの説明の代わりによく使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-174">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="29e5a-175">著作権</span><span class="sxs-lookup"><span data-stu-id="29e5a-175">copyright</span></span>
<span data-ttu-id="29e5a-176">*(1.5 以降)* パッケージの著作権の詳細。</span><span class="sxs-lookup"><span data-stu-id="29e5a-176">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="29e5a-177">language</span><span class="sxs-lookup"><span data-stu-id="29e5a-177">language</span></span>
<span data-ttu-id="29e5a-178">パッケージのロケール ID。</span><span class="sxs-lookup"><span data-stu-id="29e5a-178">The locale ID for the package.</span></span> <span data-ttu-id="29e5a-179">「[ローカライズされたパッケージの作成](../create-packages/creating-localized-packages.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-179">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="29e5a-180">タグ</span><span class="sxs-lookup"><span data-stu-id="29e5a-180">tags</span></span>
<span data-ttu-id="29e5a-181">パッケージについて説明し、検索やフィルターでパッケージを見つけやすくするタグやキーワードを、スペースで区切って列記したリスト。</span><span class="sxs-lookup"><span data-stu-id="29e5a-181">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="29e5a-182">処理できます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-182">serviceable</span></span> 
<span data-ttu-id="29e5a-183">*(3.3 以降)* NuGet 内部でのみ使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-183">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="29e5a-184">リポジトリ</span><span class="sxs-lookup"><span data-stu-id="29e5a-184">repository</span></span>
<span data-ttu-id="29e5a-185">4 つの省略可能な属性で構成される、リポジトリ メタデータ:*型*と*url* *(4.0 以降)*、および*ブランチ*と*コミット* *(4.6 以降)* します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-185">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="29e5a-186">これらの属性を取得する可能性がありますが、組み込まれているリポジトリへの .nupkg をマップできます。 個々 の分岐またはパッケージの構築コミットとして説明されています。</span><span class="sxs-lookup"><span data-stu-id="29e5a-186">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="29e5a-187">バージョン管理のソフトウェアを直接呼び出すことができる公開されている url があります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-187">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="29e5a-188">これは、コンピューターのように html ページをことがいません。</span><span class="sxs-lookup"><span data-stu-id="29e5a-188">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="29e5a-189">プロジェクトのページへのリンクを使用して、`projectUrl`フィールドに、代わりにします。</span><span class="sxs-lookup"><span data-stu-id="29e5a-189">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="29e5a-190">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="29e5a-190">minClientVersion</span></span>
<span data-ttu-id="29e5a-191">nuget.exe および Visual Studio パッケージ マネージャーで強制する、このパッケージをインストールできる NuGet クライアントの最小バージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-191">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="29e5a-192">これは、NuGet クライアントの特定のバージョンで追加された `.nuspec` ファイルの特定の機能にパッケージが依存しているときに、常に使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-192">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="29e5a-193">たとえば、`developmentDependency` 属性を使っているパッケージでは、`minClientVersion` に "2.8" を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-193">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="29e5a-194">同様に、`contentFiles` 要素 (次のセクションを参照) を使っているパッケージでは、`minClientVersion` を "3.3" に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-194">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="29e5a-195">また、バージョン 2.5 より前の NuGet クライアントはこのフラグを認識しないので、`minClientVersion` の値が何であっても、"*常に*" パッケージをインストールしないことにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-195">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="29e5a-196">コレクション要素</span><span class="sxs-lookup"><span data-stu-id="29e5a-196">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="29e5a-197">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="29e5a-197">packageTypes</span></span>
<span data-ttu-id="29e5a-198">*(3.5 以降)* 従来の依存関係パッケージ以外の場合に、パッケージの種類を指定する 0 個以上の `<packageType>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="29e5a-198">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="29e5a-199">各 packageType は、*name* 属性と *version* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="29e5a-199">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="29e5a-200">「[Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type)」(パッケージの種類の設定) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-200">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="29e5a-201">依存関係</span><span class="sxs-lookup"><span data-stu-id="29e5a-201">dependencies</span></span>
<span data-ttu-id="29e5a-202">パッケージの依存関係を指定する 0 個以上の `<dependency>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="29e5a-202">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="29e5a-203">各 dependency は、*id*、*version*、*include* (3.x 以降)、*exclude* (3.x 以降) の各属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="29e5a-203">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="29e5a-204">後の「[依存関係](#dependencies-element)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-204">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="29e5a-205">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="29e5a-205">frameworkAssemblies</span></span>
<span data-ttu-id="29e5a-206">*(1.2 以降)* このパッケージで必要な .NET Framework アセンブリ参照を示す 0 個以上の `<frameworkAssembly>` 要素のコレクション。パッケージを使うプロジェクトに参照が確実に追加されるようにします。</span><span class="sxs-lookup"><span data-stu-id="29e5a-206">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="29e5a-207">各 frameworkAssembly は、*assemblyName* 属性と *targetFramework* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="29e5a-207">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="29e5a-208">[フレームワーク アセンブリ参照 GAC の指定](#specifying-framework-assembly-references-gac)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-208">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="29e5a-209">参照</span><span class="sxs-lookup"><span data-stu-id="29e5a-209">references</span></span>
<span data-ttu-id="29e5a-210">*(1.5 以降)* パッケージの `lib` フォルダー内のアセンブリのうちプロジェクト参照として追加するものを指定する、0 個以上の `<reference>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="29e5a-210">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="29e5a-211">各参照は、*file* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="29e5a-211">Each reference has a *file* attribute.</span></span> <span data-ttu-id="29e5a-212">`<references>` は `<group>` 要素を含むこともでき、その *targetFramework* 属性に `<reference>` 要素を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-212">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="29e5a-213">省略すると、`lib` のすべての参照が含まれます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-213">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="29e5a-214">[明示的なアセンブリ参照の指定](#specifying-explicit-assembly-references)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-214">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="29e5a-215">contentFiles</span><span class="sxs-lookup"><span data-stu-id="29e5a-215">contentFiles</span></span>
<span data-ttu-id="29e5a-216">*(3.3 以降)* 使用する側のプロジェクトに含めるコンテンツ ファイルを示す `<files>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="29e5a-216">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="29e5a-217">これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-217">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="29e5a-218">[パッケージに含めるファイルの指定](#specifying-files-to-include-in-the-package)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-218">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="29e5a-219">ファイル</span><span class="sxs-lookup"><span data-stu-id="29e5a-219">files</span></span> 
<span data-ttu-id="29e5a-220">`<package>`ノードを含めることができます、`<files>`ノードを兄弟として`<metadata>`、および`<contentFiles>`下の子`<metadata>`パッケージに含めるアセンブリとコンテンツ ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-220">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="29e5a-221">詳しくは、このトピックで後述する「[アセンブリ ファイルを含める](#including-assembly-files)」と「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-221">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="29e5a-222">置換トークン</span><span class="sxs-lookup"><span data-stu-id="29e5a-222">Replacement tokens</span></span>

<span data-ttu-id="29e5a-223">パッケージを作成するとき、[`nuget pack` コマンド](../tools/cli-ref-pack.md)は、`.nuspec` ファイルの `<metadata>` ノード内の $ で区切られたトークンを、プロジェクト ファイルまたは `pack` コマンドの `-properties` スイッチで指定されている値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-223">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="29e5a-224">コマンド ラインでは、`nuget pack -properties <name>=<value>;<name>=<value>` でトークンの値を指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-224">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="29e5a-225">たとえば、`.nuspec` では `$owners$` や `$desc$` などのトークンを使っておき、パッキング時に次のようにして値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-225">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="29e5a-226">プロジェクトの値を使うには、次の表で説明するトークンを指定します (AssemblyInfo は、`Properties` 内の `AssemblyInfo.cs` や `AssemblyInfo.vb` などのファイルを参照します)。</span><span class="sxs-lookup"><span data-stu-id="29e5a-226">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="29e5a-227">これらのトークンを使うには、`nuget pack` を実行するときに、`.nuspec` だけでなくプロジェクト ファイルも指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-227">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="29e5a-228">たとえば、次のコマンドを使うと、`.nuspec` ファイルの `$id$` および `$version$` トークンが、プロジェクトの `AssemblyName` および `AssemblyVersion` の値に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-228">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="29e5a-229">通常、プロジェクトがある場合は、最初に `nuget spec MyProject.csproj` を使って `.nuspec` を作成すると、一部の標準的なトークンが自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-229">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="29e5a-230">ただし、`.nuspec` の必須要素に対する値がプロジェクトにないと、`nuget pack` は失敗します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-230">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="29e5a-231">さらに、プロジェクトの値を変更する場合は、パッケージを作成する前に必ずビルドし直してください。これは、pack コマンドの `build` スイッチで簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-231">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="29e5a-232">例外である `$configuration$` を除き、コマンド ラインの同じトークンに割り当てられている値より、プロジェクトの値の方が優先的に使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-232">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="29e5a-233">トークン</span><span class="sxs-lookup"><span data-stu-id="29e5a-233">Token</span></span> | <span data-ttu-id="29e5a-234">値のソース</span><span class="sxs-lookup"><span data-stu-id="29e5a-234">Value source</span></span> | <span data-ttu-id="29e5a-235">[値]</span><span class="sxs-lookup"><span data-stu-id="29e5a-235">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="29e5a-236">**$id$**</span><span class="sxs-lookup"><span data-stu-id="29e5a-236">**$id$**</span></span> | <span data-ttu-id="29e5a-237">プロジェクト ファイル</span><span class="sxs-lookup"><span data-stu-id="29e5a-237">Project file</span></span> | <span data-ttu-id="29e5a-238">プロジェクト ファイルの AssemblyName (タイトル)</span><span class="sxs-lookup"><span data-stu-id="29e5a-238">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="29e5a-239">**$version$**</span><span class="sxs-lookup"><span data-stu-id="29e5a-239">**$version$**</span></span> | <span data-ttu-id="29e5a-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="29e5a-240">AssemblyInfo</span></span> | <span data-ttu-id="29e5a-241">ある場合は AssemblyInformationalVersion、ない場合は AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="29e5a-241">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="29e5a-242">**$authors $**</span><span class="sxs-lookup"><span data-stu-id="29e5a-242">**$authors$**</span></span> | <span data-ttu-id="29e5a-243">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="29e5a-243">AssemblyInfo</span></span> | <span data-ttu-id="29e5a-244">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="29e5a-244">AssemblyCompany</span></span> |
| <span data-ttu-id="29e5a-245">**$title$**</span><span class="sxs-lookup"><span data-stu-id="29e5a-245">**$title$**</span></span> | <span data-ttu-id="29e5a-246">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="29e5a-246">AssemblyInfo</span></span> | <span data-ttu-id="29e5a-247">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="29e5a-247">AssemblyTitle</span></span> |
| <span data-ttu-id="29e5a-248">**$description$**</span><span class="sxs-lookup"><span data-stu-id="29e5a-248">**$description$**</span></span> | <span data-ttu-id="29e5a-249">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="29e5a-249">AssemblyInfo</span></span> | <span data-ttu-id="29e5a-250">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="29e5a-250">AssemblyDescription</span></span> |
| <span data-ttu-id="29e5a-251">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="29e5a-251">**$copyright$**</span></span> | <span data-ttu-id="29e5a-252">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="29e5a-252">AssemblyInfo</span></span> | <span data-ttu-id="29e5a-253">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="29e5a-253">AssemblyCopyright</span></span> |
| <span data-ttu-id="29e5a-254">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="29e5a-254">**$configuration$**</span></span> | <span data-ttu-id="29e5a-255">アセンブリ DLL</span><span class="sxs-lookup"><span data-stu-id="29e5a-255">Assembly DLL</span></span> | <span data-ttu-id="29e5a-256">アセンブリのビルドに使われる構成。既定値は Debug。</span><span class="sxs-lookup"><span data-stu-id="29e5a-256">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="29e5a-257">Release 構成を使ってパッケージを作成するには、常にコマンド ラインで `-properties Configuration=Release` を使うことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-257">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="29e5a-258">[アセンブリ ファイル](#including-assembly-files)および[コンテンツ ファイル](#including-content-files)を含めるときは、トークンを使ってパスを解決することもできます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-258">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="29e5a-259">トークンの名前は MSBuild のプロパティと同じであり、現在のビルド構成に基づいて含めるファイルを選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-259">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="29e5a-260">たとえば、`.nuspec` ファイルで次のトークンを使うものとします。</span><span class="sxs-lookup"><span data-stu-id="29e5a-260">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="29e5a-261">そして、MSBuild で `AssemblyName` が `LoggingLibrary` であるアセンブリを `Release` 構成でビルドすると、パッケージ内の `.nuspec` ファイルの行は結果として次のようになります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-261">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="29e5a-262">依存関係要素</span><span class="sxs-lookup"><span data-stu-id="29e5a-262">Dependencies element</span></span>

<span data-ttu-id="29e5a-263">`<metadata>` 内の `<dependencies>` 要素は、最上位のパッケージが依存している他のパッケージを示す `<dependency>` 要素をいくつでも含むことができます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-263">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="29e5a-264">各 `<dependency>` の属性は次にとおりです。</span><span class="sxs-lookup"><span data-stu-id="29e5a-264">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="29e5a-265">属性</span><span class="sxs-lookup"><span data-stu-id="29e5a-265">Attribute</span></span> | <span data-ttu-id="29e5a-266">説明</span><span class="sxs-lookup"><span data-stu-id="29e5a-266">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="29e5a-267">(必須) "EntityFramework" や "NUnit" などの依存関係のパッケージ ID。これはパッケージ ページに表示されるパッケージ nuget.org の名前となります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-267">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="29e5a-268">(必須) 依存関係として許容されるバージョンの範囲。</span><span class="sxs-lookup"><span data-stu-id="29e5a-268">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="29e5a-269">厳密な構文については、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」(パッケージのバージョン管理) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-269">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="29e5a-270">include</span><span class="sxs-lookup"><span data-stu-id="29e5a-270">include</span></span> | <span data-ttu-id="29e5a-271">最終的なパッケージに含める依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="29e5a-271">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="29e5a-272">既定値は `all` です。</span><span class="sxs-lookup"><span data-stu-id="29e5a-272">The default value is `all`.</span></span> |
| <span data-ttu-id="29e5a-273">exclude</span><span class="sxs-lookup"><span data-stu-id="29e5a-273">exclude</span></span> | <span data-ttu-id="29e5a-274">最終的なパッケージから除外する依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="29e5a-274">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="29e5a-275">既定値は`build,analyzers`上書きすることができます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-275">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="29e5a-276">`content/ ContentFiles`上書きすることはできませんが、最終的なパッケージも暗黙的にから除外されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-276">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="29e5a-277">`exclude` で指定されているタグの方が、`include` で指定されているタグより優先されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-277">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="29e5a-278">たとえば、`include="runtime, compile" exclude="compile"` は `include="runtime"` と同じです。</span><span class="sxs-lookup"><span data-stu-id="29e5a-278">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="29e5a-279">包含/除外タグ</span><span class="sxs-lookup"><span data-stu-id="29e5a-279">Include/Exclude tag</span></span> | <span data-ttu-id="29e5a-280">ターゲットの影響を受けるフォルダー</span><span class="sxs-lookup"><span data-stu-id="29e5a-280">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="29e5a-281">contentFiles</span><span class="sxs-lookup"><span data-stu-id="29e5a-281">contentFiles</span></span> | <span data-ttu-id="29e5a-282">Content</span><span class="sxs-lookup"><span data-stu-id="29e5a-282">Content</span></span> |
| <span data-ttu-id="29e5a-283">ランタイム</span><span class="sxs-lookup"><span data-stu-id="29e5a-283">runtime</span></span> | <span data-ttu-id="29e5a-284">Runtime、Resources、FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="29e5a-284">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="29e5a-285">compile</span><span class="sxs-lookup"><span data-stu-id="29e5a-285">compile</span></span> | <span data-ttu-id="29e5a-286">lib</span><span class="sxs-lookup"><span data-stu-id="29e5a-286">lib</span></span> |
| <span data-ttu-id="29e5a-287">ビルド</span><span class="sxs-lookup"><span data-stu-id="29e5a-287">build</span></span> | <span data-ttu-id="29e5a-288">build (MSBuild のプロパティとターゲット)</span><span class="sxs-lookup"><span data-stu-id="29e5a-288">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="29e5a-289">native</span><span class="sxs-lookup"><span data-stu-id="29e5a-289">native</span></span> | <span data-ttu-id="29e5a-290">native</span><span class="sxs-lookup"><span data-stu-id="29e5a-290">native</span></span> |
| <span data-ttu-id="29e5a-291">none</span><span class="sxs-lookup"><span data-stu-id="29e5a-291">none</span></span> | <span data-ttu-id="29e5a-292">フォルダーなし</span><span class="sxs-lookup"><span data-stu-id="29e5a-292">No folders</span></span> |
| <span data-ttu-id="29e5a-293">all</span><span class="sxs-lookup"><span data-stu-id="29e5a-293">all</span></span> | <span data-ttu-id="29e5a-294">すべてのフォルダー</span><span class="sxs-lookup"><span data-stu-id="29e5a-294">All folders</span></span> |

<span data-ttu-id="29e5a-295">たとえば、次の行は `PackageA` バージョン 1.1.0 以降および `PackageB` バージョン 1.x での依存関係を示します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-295">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="29e5a-296">次の行も同じパッケージでの依存関係を示しますが、`PackageA` の `contentFiles` および `build` フォルダーを含めて、`PackageB` の `native` および `compile` フォルダーを除くすべてを含めることを指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-296">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="29e5a-297">メモ:作成するときに、`.nuspec`を使用してプロジェクトから`nuget spec`、そのプロジェクト内に存在する依存関係が、最終的な自動的に含まれている`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="29e5a-297">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="29e5a-298">依存関係グループ</span><span class="sxs-lookup"><span data-stu-id="29e5a-298">Dependency groups</span></span>

<span data-ttu-id="29e5a-299">*バージョン 2.0 以降*</span><span class="sxs-lookup"><span data-stu-id="29e5a-299">*Version 2.0+*</span></span>

<span data-ttu-id="29e5a-300">1 つのフラット リストの代わりに、`<dependencies>` の `<group>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って依存関係を指定できます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-300">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="29e5a-301">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<dependency>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-301">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="29e5a-302">ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの依存関係が一緒にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-302">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="29e5a-303">依存関係の既定のリストまたはフォールバック リストとしては、`targetFramework` 属性のない `<group>` 要素が使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-303">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="29e5a-304">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-304">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="29e5a-305">グループの形式をフラット リストと併用することはできません。</span><span class="sxs-lookup"><span data-stu-id="29e5a-305">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="29e5a-306">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-306">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="29e5a-307">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="29e5a-307">Explicit assembly references</span></span>

<span data-ttu-id="29e5a-308">`<references>` 要素は、パッケージを使うときにターゲット プロジェクトが参照する必要のあるアセンブリを明示的に指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-308">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="29e5a-309">この要素がある場合、NuGet は一覧で指定されているアセンブリのみへの参照を追加します。パッケージの `lib` フォルダーに含まれる他のアセンブリに対する参照は追加されません。</span><span class="sxs-lookup"><span data-stu-id="29e5a-309">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="29e5a-310">たとえば、次の `<references>` 要素は、パッケージに他のアセンブリがある場合でも、`xunit.dll` と `xunit.extensions.dll` に対する参照だけを追加するよう NuGet に指示します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-310">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="29e5a-311">明示的な参照は、通常、設計時のみのアセンブリに使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-311">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="29e5a-312">たとえば、[コード コントラクト](/dotnet/framework/debug-trace-profile/code-contracts)を使うときは、Visual Studio がコントラクト アセンブリを検出できるように、コントラクト アセンブリはそれが拡張するランタイム アセンブリの隣に存在する必要がありますが、プロジェクトでコントラクト アセンブリを参照したり、プロジェクトの `bin` フォルダーにコントラクト アセンブリをコピーしたりする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="29e5a-312">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="29e5a-313">同様に、明示的な参照は XUnit などの単体テスト フレームワークに使うことができ、その場合、ツール アセンブリはランタイム アセンブリの隣に存在する必要がありますが、プロジェクト参照として含まれる必要はありません。</span><span class="sxs-lookup"><span data-stu-id="29e5a-313">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="29e5a-314">[参照グループ]</span><span class="sxs-lookup"><span data-stu-id="29e5a-314">Reference groups</span></span>

<span data-ttu-id="29e5a-315">1 つのフラット リストの代わりに、`<references>` の `<group>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って参照を指定できます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-315">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="29e5a-316">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<reference>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-316">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="29e5a-317">ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの参照はプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-317">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="29e5a-318">参照の既定のリストまたはフォールバック リストとしては、`targetFramework` 属性のない `<group>` 要素が使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-318">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="29e5a-319">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-319">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="29e5a-320">グループの形式をフラット リストと併用することはできません。</span><span class="sxs-lookup"><span data-stu-id="29e5a-320">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="29e5a-321">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-321">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="29e5a-322">フレームワーク アセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="29e5a-322">Framework assembly references</span></span>

<span data-ttu-id="29e5a-323">フレームワーク アセンブリは、.NET Framework の一部であり、指定されたコンピューターのグローバル アセンブリ キャッシュ (GAC) に既に存在している必要があります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-323">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="29e5a-324">`<frameworkAssemblies>` 要素でこれらのアセンブリを指定することにより、プロジェクトに必要な参照がまだない場合であっても、そのような参照をプロジェクトに確実に追加できます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-324">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="29e5a-325">もちろん、そのようなアセンブリがパッケージに直接含まれることはありません。</span><span class="sxs-lookup"><span data-stu-id="29e5a-325">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="29e5a-326">`<frameworkAssemblies>` 要素には 0 個以上の `<frameworkAssembly>` 要素を含めることができ、それぞれで次の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-326">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="29e5a-327">属性</span><span class="sxs-lookup"><span data-stu-id="29e5a-327">Attribute</span></span> | <span data-ttu-id="29e5a-328">説明</span><span class="sxs-lookup"><span data-stu-id="29e5a-328">Description</span></span> |
| --- | --- |
| <span data-ttu-id="29e5a-329">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="29e5a-329">**assemblyName**</span></span> | <span data-ttu-id="29e5a-330">(必須) 完全修飾アセンブリ名。</span><span class="sxs-lookup"><span data-stu-id="29e5a-330">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="29e5a-331">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="29e5a-331">**targetFramework**</span></span> | <span data-ttu-id="29e5a-332">(省略可能) この参照を適用するターゲット フレームワークを指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-332">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="29e5a-333">省略した場合は、参照がすべてのフレームワークに適用されることを示します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-333">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="29e5a-334">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-334">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="29e5a-335">次の例は、`System.Net` への参照はすべてのターゲット フレームワークに適用され、`System.ServiceModel` への参照は .NET Framework 4.0 のみに適用されることを示します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-335">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="29e5a-336">アセンブリ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="29e5a-336">Including assembly files</span></span>

<span data-ttu-id="29e5a-337">「[パッケージを作成する](../create-packages/creating-a-package.md)」で説明されている規則に従う場合、`.nuspec` ファイルでファイルの一覧を明示的に指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="29e5a-337">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="29e5a-338">`nuget pack` コマンドが必要なファイルを自動的に選びます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-338">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="29e5a-339">プロジェクトにパッケージをインストールするとき、NuGet はパッケージの DLL にアセンブリ参照を自動的に追加します。ただし、指定されている `.resources.dll` は、ローカライズされたサテライト アセンブリであると見なされるため "*除外*" されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-339">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="29e5a-340">そのため、避けなければ不可欠なパッケージ コードが含まれてしまうファイルには `.resources.dll` を使わないようにします。</span><span class="sxs-lookup"><span data-stu-id="29e5a-340">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="29e5a-341">この自動動作をバイパスして、パッケージに含めるファイルを明示的に制御するには、`<files>` 要素を `<package>` の子要素 (および `<metadata>` の兄弟要素) として配置し、各ファイルを個別の `<file>` 要素で示します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-341">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="29e5a-342">例:</span><span class="sxs-lookup"><span data-stu-id="29e5a-342">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="29e5a-343">NuGet 2.x 以前および `packages.config` を使っているプロジェクトでは、`<files>` 要素はパッケージのインストール時に変更できないコンテンツ ファイルを含めるためにも使われます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-343">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="29e5a-344">NuGet 3.3 以降で、PackageReference を使用しているプロジェクトでは、代わりに `<contentFiles>` 要素が使用されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-344">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="29e5a-345">詳しくは、後の「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-345">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="29e5a-346">File 要素の属性</span><span class="sxs-lookup"><span data-stu-id="29e5a-346">File element attributes</span></span>

<span data-ttu-id="29e5a-347">各 `<file>` 要素では、次の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-347">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="29e5a-348">属性</span><span class="sxs-lookup"><span data-stu-id="29e5a-348">Attribute</span></span> | <span data-ttu-id="29e5a-349">説明</span><span class="sxs-lookup"><span data-stu-id="29e5a-349">Description</span></span> |
| --- | --- |
| <span data-ttu-id="29e5a-350">**src**</span><span class="sxs-lookup"><span data-stu-id="29e5a-350">**src**</span></span> | <span data-ttu-id="29e5a-351">含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-351">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="29e5a-352">絶対パスを指定しない限り、パスは `.nuspec` ファイルが基準になります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-352">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="29e5a-353">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-353">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="29e5a-354">**target**</span><span class="sxs-lookup"><span data-stu-id="29e5a-354">**target**</span></span> | <span data-ttu-id="29e5a-355">ソース ファイルが格納されるパッケージ内のフォルダーへの相対パス。`lib`、`content`、`build`、または `tools` で始まっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-355">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="29e5a-356">[規則に基づく作業ディレクトリからの .nuspec の作成](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29e5a-356">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="29e5a-357">**exclude**</span><span class="sxs-lookup"><span data-stu-id="29e5a-357">**exclude**</span></span> | <span data-ttu-id="29e5a-358">`src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。</span><span class="sxs-lookup"><span data-stu-id="29e5a-358">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="29e5a-359">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-359">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="29e5a-360">使用例</span><span class="sxs-lookup"><span data-stu-id="29e5a-360">Examples</span></span>

<span data-ttu-id="29e5a-361">**1 つのアセンブリ**</span><span class="sxs-lookup"><span data-stu-id="29e5a-361">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="29e5a-362">**ターゲット フレームワークに固有の 1 つのアセンブリ**</span><span class="sxs-lookup"><span data-stu-id="29e5a-362">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="29e5a-363">**ワイルドカードを使った DLL のセット**</span><span class="sxs-lookup"><span data-stu-id="29e5a-363">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="29e5a-364">**異なるフレームワークの DLL**</span><span class="sxs-lookup"><span data-stu-id="29e5a-364">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="29e5a-365">**ファイルの除外**</span><span class="sxs-lookup"><span data-stu-id="29e5a-365">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="29e5a-366">コンテンツ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="29e5a-366">Including content files</span></span>

<span data-ttu-id="29e5a-367">コンテンツ ファイルは、パッケージでプロジェクトに含める必要がある変更できないファイルです。</span><span class="sxs-lookup"><span data-stu-id="29e5a-367">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="29e5a-368">変更できないので、それを使うプロジェクトによる変更は意図されていません。</span><span class="sxs-lookup"><span data-stu-id="29e5a-368">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="29e5a-369">コンテンツ ファイルの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-369">Example content files include:</span></span>

- <span data-ttu-id="29e5a-370">リソースとして埋め込まれる画像</span><span class="sxs-lookup"><span data-stu-id="29e5a-370">Images that are embedded as resources</span></span>
- <span data-ttu-id="29e5a-371">コンパイル済みのソース ファイル</span><span class="sxs-lookup"><span data-stu-id="29e5a-371">Source files that are already compiled</span></span>
- <span data-ttu-id="29e5a-372">プロジェクトのビルド出力と共に含まれる必要があるスクリプト</span><span class="sxs-lookup"><span data-stu-id="29e5a-372">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="29e5a-373">プロジェクトに含まれる必要はあるが、プロジェクト固有の変更は必要ない、パッケージの構成ファイル</span><span class="sxs-lookup"><span data-stu-id="29e5a-373">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="29e5a-374">コンテンツ ファイルをパッケージに含めるには、`<files>` 要素を使い、`target` 属性で `content` フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-374">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="29e5a-375">ただし、PackageReference を使用しているプロジェクトにパッケージをインストールする場合、このようなファイルは無視され、代わりに `<contentFiles>` 要素が使用されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-375">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="29e5a-376">使用する側のプロジェクトとの最大限の互換性のため、パッケージでは両方の要素でコンテンツ ファイルを指定するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="29e5a-376">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="29e5a-377">コンテンツ ファイルに対する files 要素の使用</span><span class="sxs-lookup"><span data-stu-id="29e5a-377">Using the files element for content files</span></span>

<span data-ttu-id="29e5a-378">コンテンツ ファイルでは、アセンブリ ファイルの場合と同じ形式を使用しますが、次の例のように、`target` 属性で基本フォルダーとして `content` を指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-378">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="29e5a-379">**基本的なコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="29e5a-379">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="29e5a-380">**ディレクトリ構造を持つコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="29e5a-380">**Content files with directory structure**</span></span>

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

<span data-ttu-id="29e5a-381">**ターゲット フレームワークに固有のコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="29e5a-381">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="29e5a-382">**名前のドットでフォルダーにコピーされるコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="29e5a-382">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="29e5a-383">この場合、NuGet は `target` の拡張子が `src` の拡張子と一致しないものと判断し、`target` での名前のその部分をフォルダーとして扱います。</span><span class="sxs-lookup"><span data-stu-id="29e5a-383">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="29e5a-384">**拡張子のないコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="29e5a-384">**Content files without extensions**</span></span>

<span data-ttu-id="29e5a-385">拡張子のないファイルを含めるには、ワイルドカード `*` または `**` を使います。</span><span class="sxs-lookup"><span data-stu-id="29e5a-385">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="29e5a-386">**深いパスと深いターゲットのコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="29e5a-386">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="29e5a-387">この場合、ソースとターゲットのファイル拡張子が一致するので、NuGet はターゲットがフォルダーではなくファイル名であると想定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-387">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="29e5a-388">**パッケージ内のコンテンツ ファイルの名前の変更**</span><span class="sxs-lookup"><span data-stu-id="29e5a-388">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="29e5a-389">**ファイルの除外**</span><span class="sxs-lookup"><span data-stu-id="29e5a-389">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="29e5a-390">コンテンツ ファイルに対する contentFiles 要素の使用</span><span class="sxs-lookup"><span data-stu-id="29e5a-390">Using the contentFiles element for content files</span></span>

<span data-ttu-id="29e5a-391">*NuGet 4.0 以降で、PackageReference を使用している場合*</span><span class="sxs-lookup"><span data-stu-id="29e5a-391">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="29e5a-392">既定では、パッケージはコンテンツを `contentFiles` フォルダーに配置し (下記参照)、`nuget pack` は既定の属性を使ってそのフォルダーにすべてのファイルを格納します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-392">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="29e5a-393">この場合は、`contentFiles` ノードを `.nuspec` に含める必要はまったくありません。</span><span class="sxs-lookup"><span data-stu-id="29e5a-393">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="29e5a-394">含まれるファイルを制御するには、含めるファイルを厳密に示す `<files>` 要素のコレクションである `<contentFiles>` 要素を指定します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-394">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="29e5a-395">これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-395">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="29e5a-396">属性</span><span class="sxs-lookup"><span data-stu-id="29e5a-396">Attribute</span></span> | <span data-ttu-id="29e5a-397">説明</span><span class="sxs-lookup"><span data-stu-id="29e5a-397">Description</span></span> |
| --- | --- |
| <span data-ttu-id="29e5a-398">**include**</span><span class="sxs-lookup"><span data-stu-id="29e5a-398">**include**</span></span> | <span data-ttu-id="29e5a-399">(必須) 含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-399">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="29e5a-400">絶対パスを指定しない限り、パスは `.nuspec` ファイルが基準になります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-400">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="29e5a-401">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-401">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="29e5a-402">**exclude**</span><span class="sxs-lookup"><span data-stu-id="29e5a-402">**exclude**</span></span> | <span data-ttu-id="29e5a-403">`src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。</span><span class="sxs-lookup"><span data-stu-id="29e5a-403">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="29e5a-404">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-404">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="29e5a-405">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="29e5a-405">**buildAction**</span></span> | <span data-ttu-id="29e5a-406">MSBuild のコンテンツ項目に割り当てるビルド アクション。`Content`、`None`、`Embedded Resource`、`Compile` などです。既定値は、`Compile` です。</span><span class="sxs-lookup"><span data-stu-id="29e5a-406">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="29e5a-407">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="29e5a-407">**copyToOutput**</span></span> | <span data-ttu-id="29e5a-408">出力フォルダーをビルドするコンテンツ項目をコピー (またはパブリッシュ) するかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="29e5a-408">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="29e5a-409">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="29e5a-409">The default is false.</span></span> |
| <span data-ttu-id="29e5a-410">**flatten**</span><span class="sxs-lookup"><span data-stu-id="29e5a-410">**flatten**</span></span> | <span data-ttu-id="29e5a-411">コンテンツ項目をビルド出力の単一フォルダーにコピーするか (true)、それともパッケージのフォルダー構造を保持するか (false) を示すブール値。</span><span class="sxs-lookup"><span data-stu-id="29e5a-411">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="29e5a-412">このフラグは、copyToOutput が true に設定されている場合のみ機能します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-412">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="29e5a-413">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="29e5a-413">The default is false.</span></span> |

<span data-ttu-id="29e5a-414">パッケージをインストールするとき、NuGet は `<contentFiles>` の子要素を上から下に順番に適用します。</span><span class="sxs-lookup"><span data-stu-id="29e5a-414">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="29e5a-415">複数のエントリが同じファイルに一致する場合は、すべてのエントリが適用されます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-415">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="29e5a-416">同じ属性に対して競合がある場合は、最上位のエントリが下位のエントリをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="29e5a-416">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="29e5a-417">パッケージ フォルダーの構造</span><span class="sxs-lookup"><span data-stu-id="29e5a-417">Package folder structure</span></span>

<span data-ttu-id="29e5a-418">パッケージ プロジェクトでは、次のパターンを使ってコンテンツを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="29e5a-418">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="29e5a-419">`codeLanguages` には、`cs`、`vb`、`fs`、`any`、または指定された `$(ProjectLanguage)` に相当する小文字表現を指定できます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-419">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="29e5a-420">`TxM` は、NuGet がサポートする任意の有効なターゲット フレームワーク モニカーです (「[ターゲット フレームワーク](../reference/target-frameworks.md)」を参照)。</span><span class="sxs-lookup"><span data-stu-id="29e5a-420">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="29e5a-421">この構文の末尾に、任意のフォルダー構造を追加できます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-421">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="29e5a-422">例:</span><span class="sxs-lookup"><span data-stu-id="29e5a-422">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="29e5a-423">空のフォルダーでは、`.` を使って、言語と TxM の特定の組み合わせにコンテンツを提供しないようにすることができます。次はその例です。</span><span class="sxs-lookup"><span data-stu-id="29e5a-423">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="29e5a-424">contentFiles セクションの例</span><span class="sxs-lookup"><span data-stu-id="29e5a-424">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="29e5a-425">Nuspec ファイルの例</span><span class="sxs-lookup"><span data-stu-id="29e5a-425">Example nuspec files</span></span>

<span data-ttu-id="29e5a-426">**依存関係またはファイルを指定しない単純な `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="29e5a-426">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="29e5a-427">**依存関係を含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="29e5a-427">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="29e5a-428">**ファイルを含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="29e5a-428">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="29e5a-429">**フレームワーク アセンブリを含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="29e5a-429">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="29e5a-430">この例では、指定したプロジェクト ターゲットに次のものがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="29e5a-430">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="29e5a-431">.NET4 -> `System.Web`、`System.Net`</span><span class="sxs-lookup"><span data-stu-id="29e5a-431">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="29e5a-432">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="29e5a-432">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="29e5a-433">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="29e5a-433">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="29e5a-434">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="29e5a-434">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="29e5a-435">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="29e5a-435">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
