---
title: NuGet の nuspec ファイルリファレンス
description: .nuspec ファイルには、パッケージを作成するとき、およびパッケージのコンシューマーに情報を提供するために使われる、パッケージのメタデータが含まれています。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 19e7934e2f249056c532369fa5e8ee6e35cc8086
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428379"
---
# <a name="nuspec-reference"></a><span data-ttu-id="a747a-103">.nuspec リファレンス</span><span class="sxs-lookup"><span data-stu-id="a747a-103">.nuspec reference</span></span>

<span data-ttu-id="a747a-104">`.nuspec` ファイルは、パッケージのメタデータが含まれている XML マニフェストです。</span><span class="sxs-lookup"><span data-stu-id="a747a-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="a747a-105">このマニフェストは、パッケージを作成するためと、コンシューマーに情報を提供するための、両方に使われます。</span><span class="sxs-lookup"><span data-stu-id="a747a-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="a747a-106">パッケージにはマニフェストが常に含まれています。</span><span class="sxs-lookup"><span data-stu-id="a747a-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="a747a-107">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="a747a-107">In this topic:</span></span>

- [<span data-ttu-id="a747a-108">一般的な形式とスキーマ</span><span class="sxs-lookup"><span data-stu-id="a747a-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="a747a-109">[置換トークン](#replacement-tokens) (Visual Studio プロジェクトで使われるとき)</span><span class="sxs-lookup"><span data-stu-id="a747a-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="a747a-110">依存関係</span><span class="sxs-lookup"><span data-stu-id="a747a-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="a747a-111">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="a747a-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="a747a-112">フレームワーク アセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="a747a-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="a747a-113">アセンブリ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="a747a-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="a747a-114">コンテンツ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="a747a-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="a747a-115">Nuspec ファイルの例</span><span class="sxs-lookup"><span data-stu-id="a747a-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="a747a-116">プロジェクトの種類の互換性</span><span class="sxs-lookup"><span data-stu-id="a747a-116">Project type compatibility</span></span>

- <span data-ttu-id="a747a-117">`packages.config`を使用する非 SDK 形式のプロジェクトには、`nuget.exe pack` と共に `.nuspec` を使用します。</span><span class="sxs-lookup"><span data-stu-id="a747a-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="a747a-118">[Sdk スタイルのプロジェクト](../resources/check-project-format.md)(通常、 [sdk 属性](/dotnet/core/tools/csproj#additions)を使用する .net Core および .NET Standard プロジェクト) のパッケージを作成するために `.nuspec` ファイルは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="a747a-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="a747a-119">(パッケージの作成時に `.nuspec` が生成されることに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="a747a-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="a747a-120">`dotnet.exe pack` または `msbuild pack target`を使用してパッケージを作成する場合は、通常は `.nuspec` ファイルに含まれる[すべてのプロパティ](../reference/msbuild-targets.md#pack-target)をプロジェクトファイルに含めることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a747a-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="a747a-121">ただし、代わりに、 [`dotnet.exe` または `msbuild pack target`を使用してパックするために `.nuspec` ファイルを使用](../reference/msbuild-targets.md#packing-using-a-nuspec)することもできます。</span><span class="sxs-lookup"><span data-stu-id="a747a-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="a747a-122">`packages.config` から[PackageReference](../consume-packages/package-references-in-project-files.md)に移行されたプロジェクトの場合、パッケージの作成に `.nuspec` ファイルは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="a747a-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="a747a-123">代わりに、 [msbuild-](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)を使用します。</span><span class="sxs-lookup"><span data-stu-id="a747a-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="a747a-124">一般的な形式とスキーマ</span><span class="sxs-lookup"><span data-stu-id="a747a-124">General form and schema</span></span>

<span data-ttu-id="a747a-125">最新の `nuspec.xsd` スキーマ ファイルは、[NuGet GitHub リポジトリ](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)にあります。</span><span class="sxs-lookup"><span data-stu-id="a747a-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="a747a-126">このスキーマでの `.nuspec` ファイルの一般的な形式は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a747a-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="a747a-127">スキーマの視覚的な表現をはっきり表示したい場合は、Visual Studio のデザイン モードでスキーマ ファイルを開き、 **[XML スキーマ エクスプローラー]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a747a-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="a747a-128">または、コードとしてファイルを開き、エディター内を右クリックして、 **[XML スキーマ エクスプローラーで表示]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="a747a-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="a747a-129">どちらの方法でも次のように表示されます (ほとんどを展開した場合)。</span><span class="sxs-lookup"><span data-stu-id="a747a-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio のスキーマ エクスプローラーで開いた nuspec.xsd](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="a747a-131">メタデータの必須要素</span><span class="sxs-lookup"><span data-stu-id="a747a-131">Required metadata elements</span></span>

<span data-ttu-id="a747a-132">以下の要素はパッケージの最低要件であり、[メタデータの省略可能な要素](#optional-metadata-elements)を追加してパッケージに関する開発者の全体的なエクスペリエンスを向上させることを検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a747a-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="a747a-133">これらの要素は、`<metadata>` 要素内で指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a747a-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="a747a-134">id</span><span class="sxs-lookup"><span data-stu-id="a747a-134">id</span></span> 
<span data-ttu-id="a747a-135">パッケージの識別子。大文字と小文字が区別されます。nuget.org 全体で、またはパッケージが存在するギャラリー全体で、一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="a747a-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="a747a-136">ID は、スペースまたは URL で無効な文字を含んでいてはならず、一般に .NET 名前空間の規則に従います。</span><span class="sxs-lookup"><span data-stu-id="a747a-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="a747a-137">ガイダンスについては、[一意のパッケージ識別子の選択](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="a747a-138">バージョン</span><span class="sxs-lookup"><span data-stu-id="a747a-138">version</span></span>
<span data-ttu-id="a747a-139">パッケージのバージョン。*major.minor.patch* のパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="a747a-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="a747a-140">「[Package versioning](../concepts/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) で説明されているように、バージョン番号にはプレリリースのサフィックスを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a747a-140">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="a747a-141">description</span><span class="sxs-lookup"><span data-stu-id="a747a-141">description</span></span>
<span data-ttu-id="a747a-142">UI 表示用のパッケージの説明。</span><span class="sxs-lookup"><span data-stu-id="a747a-142">A description of the package for UI display.</span></span>
#### <a name="authors"></a><span data-ttu-id="a747a-143">authors</span><span class="sxs-lookup"><span data-stu-id="a747a-143">authors</span></span>
<span data-ttu-id="a747a-144">Nuget.org のプロファイル名と一致するパッケージ作成者のコンマ区切りのリスト。これらは nuget.org の NuGet ギャラリーに表示され、同じ作成者によってパッケージを相互参照するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="a747a-145">メタデータの省略可能な要素</span><span class="sxs-lookup"><span data-stu-id="a747a-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="a747a-146">owners</span><span class="sxs-lookup"><span data-stu-id="a747a-146">owners</span></span>
<span data-ttu-id="a747a-147">Nuget.org のプロファイル名を使用して、パッケージ作成者のコンマ区切りのリスト。これは、多くの場合 `authors`と同じリストであり、パッケージを nuget.org にアップロードするときには無視されます。「 [Nuget.org でのパッケージ所有者の管理」を](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)参照してください。</span><span class="sxs-lookup"><span data-stu-id="a747a-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="a747a-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="a747a-148">projectUrl</span></span>
<span data-ttu-id="a747a-149">パッケージのホーム ページの URL。多くの場合、UI 画面と nuget.org に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="a747a-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="a747a-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="a747a-151">licenseUrl は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="a747a-151">licenseUrl is deprecated.</span></span> <span data-ttu-id="a747a-152">代わりにライセンスを使用してください。</span><span class="sxs-lookup"><span data-stu-id="a747a-152">Use license instead.</span></span>

<span data-ttu-id="a747a-153">パッケージのライセンスの URL。多くの場合、nuget.org のような Ui に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="a747a-154">ライセンス●らいせんす○</span><span class="sxs-lookup"><span data-stu-id="a747a-154">license</span></span>
<span data-ttu-id="a747a-155">SPDX ライセンス式またはパッケージ内のライセンスファイルへのパス。多くの場合、nuget.org のような Ui に表示されます。MIT や BSD-2 句などの一般的なライセンスでパッケージのライセンスを取得している場合は、関連付けられている[Spdx ライセンス識別子](https://spdx.org/licenses/)を使用します。</span><span class="sxs-lookup"><span data-stu-id="a747a-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="a747a-156">例 :</span><span class="sxs-lookup"><span data-stu-id="a747a-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="a747a-157">NuGet.org は、オープンソースイニシアチブまたは無償のソフトウェア基盤によって承認されたライセンス式のみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="a747a-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="a747a-158">パッケージが複数の一般的なライセンスでライセンスされている場合は、 [Spdx 式の構文バージョン 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)を使用して複合ライセンスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="a747a-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="a747a-159">例 :</span><span class="sxs-lookup"><span data-stu-id="a747a-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="a747a-160">ライセンス式でサポートされていないカスタムライセンスを使用する場合は、`.txt` または `.md` ファイルをライセンスのテキストと共にパッケージ化することができます。</span><span class="sxs-lookup"><span data-stu-id="a747a-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="a747a-161">例 :</span><span class="sxs-lookup"><span data-stu-id="a747a-161">For example:</span></span>

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

<span data-ttu-id="a747a-162">同等の MSBuild については、[ライセンス式またはライセンスファイルのパッキング](msbuild-targets.md#packing-a-license-expression-or-a-license-file)に関する説明を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a747a-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="a747a-163">NuGet のライセンス式の正確な構文については、 [Abnf](https://tools.ietf.org/html/rfc5234)で説明します。</span><span class="sxs-lookup"><span data-stu-id="a747a-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="a747a-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="a747a-164">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="a747a-165">iconUrl は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="a747a-165">iconUrl is deprecated.</span></span> <span data-ttu-id="a747a-166">代わりにアイコンを使用してください。</span><span class="sxs-lookup"><span data-stu-id="a747a-166">Use icon instead.</span></span>

<span data-ttu-id="a747a-167">UI 表示でパッケージのアイコンとして使用される透明な背景を持つ128x128 イメージの URL。</span><span class="sxs-lookup"><span data-stu-id="a747a-167">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="a747a-168">この要素の値は、"*画像を直接示す URL*" であり、画像を含む Web ページの URL ではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a747a-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="a747a-169">たとえば、GitHub のイメージを使用するには、 <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>のような RAW ファイル URL を使用します。</span><span class="sxs-lookup"><span data-stu-id="a747a-169">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
#### <a name="icon"></a><span data-ttu-id="a747a-170">アイコン●あいこん○</span><span class="sxs-lookup"><span data-stu-id="a747a-170">icon</span></span>

<span data-ttu-id="a747a-171">これはパッケージ内のイメージファイルへのパスであり、多くの場合、パッケージアイコンとして nuget.org のような Ui に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-171">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="a747a-172">イメージファイルのサイズは 1 MB に制限されています。</span><span class="sxs-lookup"><span data-stu-id="a747a-172">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="a747a-173">サポートされているファイル形式は、JPEG および PNG です。</span><span class="sxs-lookup"><span data-stu-id="a747a-173">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="a747a-174">128x128 のイメージの解像度をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a747a-174">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="a747a-175">たとえば、nuget.exe を使用してパッケージを作成するときに、nuspec に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="a747a-175">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="a747a-176">パッケージアイコン nuspec サンプル。</span><span class="sxs-lookup"><span data-stu-id="a747a-176">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="a747a-177">同等の MSBuild については、「[アイコンイメージファイルのパッキング」](msbuild-targets.md#packing-an-icon-image-file)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a747a-177">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="a747a-178">`icon`をサポートしていないソースとの下位互換性を維持するために、`icon` と `iconUrl` の両方を指定できます。</span><span class="sxs-lookup"><span data-stu-id="a747a-178">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="a747a-179">Visual Studio は、今後のリリースでフォルダーベースのソースからのパッケージの `icon` をサポートします。</span><span class="sxs-lookup"><span data-stu-id="a747a-179">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="a747a-180">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="a747a-180">requireLicenseAcceptance</span></span>
<span data-ttu-id="a747a-181">パッケージをインストールする前にクライアントがユーザーに対してパッケージのライセンスへの同意を求めるプロンプトを表示する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="a747a-181">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="a747a-182">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="a747a-182">developmentDependency</span></span>
<span data-ttu-id="a747a-183">*(2.8 以降)* 開発専用の依存関係としてパッケージをマークするかどうかを指定するブール値。指定すると、そのパッケージは他のパッケージに依存関係として含まれなくなります。</span><span class="sxs-lookup"><span data-stu-id="a747a-183">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="a747a-184">PackageReference (NuGet 4.8 以降) では、このフラグは、コンパイル時のアセットをコンパイルから除外することも意味します。</span><span class="sxs-lookup"><span data-stu-id="a747a-184">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="a747a-185">「 [DevelopmentDependency support For PackageReference」を](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)参照してください。</span><span class="sxs-lookup"><span data-stu-id="a747a-185">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="a747a-186">summary</span><span class="sxs-lookup"><span data-stu-id="a747a-186">summary</span></span>
> [!Important]
> <span data-ttu-id="a747a-187">`summary` は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="a747a-187">`summary` is being deprecated.</span></span> <span data-ttu-id="a747a-188">代わりに `description` を使用してください</span><span class="sxs-lookup"><span data-stu-id="a747a-188">Use `description` instead.</span></span>

<span data-ttu-id="a747a-189">UI 画面用のパッケージの短い説明。</span><span class="sxs-lookup"><span data-stu-id="a747a-189">A short description of the package for UI display.</span></span> <span data-ttu-id="a747a-190">省略すると、`description` を切り詰めたバージョンが使われます。</span><span class="sxs-lookup"><span data-stu-id="a747a-190">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="a747a-191">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="a747a-191">releaseNotes</span></span>
<span data-ttu-id="a747a-192">*(1.5 以降)* このリリースのパッケージで行われた変更の説明。Visual Studio パッケージ マネージャーの **[更新]** タブなどの UI で、パッケージの説明の代わりによく使われます。</span><span class="sxs-lookup"><span data-stu-id="a747a-192">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="a747a-193">著作権</span><span class="sxs-lookup"><span data-stu-id="a747a-193">copyright</span></span>
<span data-ttu-id="a747a-194">*(1.5 以降)* パッケージの著作権の詳細。</span><span class="sxs-lookup"><span data-stu-id="a747a-194">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="a747a-195">language</span><span class="sxs-lookup"><span data-stu-id="a747a-195">language</span></span>
<span data-ttu-id="a747a-196">パッケージのロケール ID。</span><span class="sxs-lookup"><span data-stu-id="a747a-196">The locale ID for the package.</span></span> <span data-ttu-id="a747a-197">「[ローカライズされたパッケージの作成](../create-packages/creating-localized-packages.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-197">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="a747a-198">tags</span><span class="sxs-lookup"><span data-stu-id="a747a-198">tags</span></span>
<span data-ttu-id="a747a-199">パッケージについて説明し、検索やフィルターでパッケージを見つけやすくするタグやキーワードを、スペースで区切って列記したリスト。</span><span class="sxs-lookup"><span data-stu-id="a747a-199">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="a747a-200">保守</span><span class="sxs-lookup"><span data-stu-id="a747a-200">serviceable</span></span> 
<span data-ttu-id="a747a-201">*(3.3 以降)* NuGet 内部でのみ使われます。</span><span class="sxs-lookup"><span data-stu-id="a747a-201">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="a747a-202">repository</span><span class="sxs-lookup"><span data-stu-id="a747a-202">repository</span></span>
<span data-ttu-id="a747a-203">`type` と `url` *(4.0 +)* 、および `branch` と `commit` *(4.6 +)* の4つの省略可能な属性で構成されるリポジトリメタデータ。</span><span class="sxs-lookup"><span data-stu-id="a747a-203">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="a747a-204">これらの属性を使用すると、`.nupkg` を構築したリポジトリにマップすることができます。これにより、パッケージを構築した個々のブランチ名またはコミット SHA-1 ハッシュが詳細に表示される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a747a-204">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="a747a-205">これは、バージョン管理ソフトウェアによって直接呼び出すことができる、一般公開されている url である必要があります。</span><span class="sxs-lookup"><span data-stu-id="a747a-205">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="a747a-206">これはコンピューター用の html ページである必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a747a-206">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="a747a-207">[プロジェクトへのリンク] ページでは、代わりに `projectUrl` フィールドを使用します。</span><span class="sxs-lookup"><span data-stu-id="a747a-207">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="a747a-208">例 :</span><span class="sxs-lookup"><span data-stu-id="a747a-208">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a><span data-ttu-id="a747a-209">title</span><span class="sxs-lookup"><span data-stu-id="a747a-209">title</span></span>
<span data-ttu-id="a747a-210">UI 表示で使用できる、パッケージのわかりやすいタイトル。</span><span class="sxs-lookup"><span data-stu-id="a747a-210">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="a747a-211">(Visual Studio の nuget.org とパッケージマネージャーにはタイトルが表示されません)</span><span class="sxs-lookup"><span data-stu-id="a747a-211">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="a747a-212">コレクション要素</span><span class="sxs-lookup"><span data-stu-id="a747a-212">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="a747a-213">packageTypes</span><span class="sxs-lookup"><span data-stu-id="a747a-213">packageTypes</span></span>
<span data-ttu-id="a747a-214">*(3.5 以降)* 従来の依存関係パッケージ以外の場合に、パッケージの種類を指定する 0 個以上の `<packageType>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="a747a-214">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="a747a-215">各 packageType は、*name* 属性と *version* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="a747a-215">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="a747a-216">「[Setting a package type](../create-packages/set-package-type.md)」(パッケージの種類の設定) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-216">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="a747a-217">依存関係</span><span class="sxs-lookup"><span data-stu-id="a747a-217">dependencies</span></span>
<span data-ttu-id="a747a-218">パッケージの依存関係を指定する 0 個以上の `<dependency>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="a747a-218">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="a747a-219">各 dependency は、*id*、*version*、*include* (3.x 以降)、*exclude* (3.x 以降) の各属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="a747a-219">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="a747a-220">後の「[依存関係](#dependencies-element)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-220">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="a747a-221">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="a747a-221">frameworkAssemblies</span></span>
<span data-ttu-id="a747a-222">*(1.2 以降)* このパッケージで必要な .NET Framework アセンブリ参照を示す 0 個以上の `<frameworkAssembly>` 要素のコレクション。パッケージを使うプロジェクトに参照が確実に追加されるようにします。</span><span class="sxs-lookup"><span data-stu-id="a747a-222">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="a747a-223">各 frameworkAssembly は、*assemblyName* 属性と *targetFramework* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="a747a-223">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="a747a-224">[フレームワーク アセンブリ参照 GAC の指定](#specifying-framework-assembly-references-gac)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-224">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="a747a-225">参照</span><span class="sxs-lookup"><span data-stu-id="a747a-225">references</span></span>
<span data-ttu-id="a747a-226">*(1.5 以降)* パッケージの `<reference>` フォルダー内のアセンブリのうちプロジェクト参照として追加するものを指定する、0 個以上の `lib` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="a747a-226">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="a747a-227">各参照は、*file* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="a747a-227">Each reference has a *file* attribute.</span></span> <span data-ttu-id="a747a-228">`<references>` は `<group>` 要素を含むこともでき、その *targetFramework* 属性に `<reference>` 要素を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a747a-228">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="a747a-229">省略すると、`lib` のすべての参照が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a747a-229">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="a747a-230">[明示的なアセンブリ参照の指定](#specifying-explicit-assembly-references)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-230">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="a747a-231">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a747a-231">contentFiles</span></span>
<span data-ttu-id="a747a-232">*(3.3 以降)* 使用する側のプロジェクトに含めるコンテンツ ファイルを示す `<files>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="a747a-232">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="a747a-233">これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-233">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="a747a-234">[パッケージに含めるファイルの指定](#specifying-files-to-include-in-the-package)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-234">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="a747a-235">files</span><span class="sxs-lookup"><span data-stu-id="a747a-235">files</span></span> 
<span data-ttu-id="a747a-236">`<package>` ノードには、`<metadata>`の兄弟として `<files>` ノードが含まれている場合があります。また、`<metadata>`に `<contentFiles>` 子として、パッケージに含めるアセンブリおよびコンテンツファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-236">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="a747a-237">詳しくは、このトピックで後述する「[アセンブリ ファイルを含める](#including-assembly-files)」と「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-237">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="a747a-238">メタデータ属性</span><span class="sxs-lookup"><span data-stu-id="a747a-238">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="a747a-239">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="a747a-239">minClientVersion</span></span>
<span data-ttu-id="a747a-240">nuget.exe および Visual Studio パッケージ マネージャーで強制する、このパッケージをインストールできる NuGet クライアントの最小バージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-240">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="a747a-241">これは、NuGet クライアントの特定のバージョンで追加された `.nuspec` ファイルの特定の機能にパッケージが依存しているときに、常に使われます。</span><span class="sxs-lookup"><span data-stu-id="a747a-241">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="a747a-242">たとえば、`developmentDependency` 属性を使っているパッケージでは、`minClientVersion` に "2.8" を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a747a-242">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="a747a-243">同様に、`contentFiles` 要素 (次のセクションを参照) を使っているパッケージでは、`minClientVersion` を "3.3" に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a747a-243">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="a747a-244">また、バージョン 2.5 より前の NuGet クライアントはこのフラグを認識しないので、 *の値が何であっても、"* 常に`minClientVersion`" パッケージをインストールしないことにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="a747a-244">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="a747a-245">置換トークン</span><span class="sxs-lookup"><span data-stu-id="a747a-245">Replacement tokens</span></span>

<span data-ttu-id="a747a-246">パッケージを作成するとき、[`nuget pack` コマンド](../reference/cli-reference/cli-ref-pack.md)は、`.nuspec` ファイルの `<metadata>` ノード内の $ で区切られたトークンを、プロジェクト ファイルまたは `pack` コマンドの `-properties` スイッチで指定されている値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a747a-246">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="a747a-247">コマンド ラインでは、`nuget pack -properties <name>=<value>;<name>=<value>` でトークンの値を指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-247">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="a747a-248">たとえば、`$owners$` では `$desc$` や `.nuspec` などのトークンを使っておき、パッキング時に次のようにして値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="a747a-248">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="a747a-249">プロジェクトの値を使うには、次の表で説明するトークンを指定します (AssemblyInfo は、`Properties` 内の `AssemblyInfo.cs` や `AssemblyInfo.vb` などのファイルを参照します)。</span><span class="sxs-lookup"><span data-stu-id="a747a-249">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="a747a-250">これらのトークンを使うには、`nuget pack` を実行するときに、`.nuspec` だけでなくプロジェクト ファイルも指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-250">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="a747a-251">たとえば、次のコマンドを使うと、`$id$` ファイルの `$version$` および `.nuspec` トークンが、プロジェクトの `AssemblyName` および `AssemblyVersion` の値に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="a747a-251">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="a747a-252">通常、プロジェクトがある場合は、最初に `.nuspec` を使って `nuget spec MyProject.csproj` を作成すると、一部の標準的なトークンが自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-252">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="a747a-253">ただし、`.nuspec` の必須要素に対する値がプロジェクトにないと、`nuget pack` は失敗します。</span><span class="sxs-lookup"><span data-stu-id="a747a-253">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="a747a-254">さらに、プロジェクトの値を変更する場合は、パッケージを作成する前に必ずビルドし直してください。これは、pack コマンドの `build` スイッチで簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a747a-254">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="a747a-255">例外である `$configuration$` を除き、コマンド ラインの同じトークンに割り当てられている値より、プロジェクトの値の方が優先的に使われます。</span><span class="sxs-lookup"><span data-stu-id="a747a-255">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="a747a-256">トークン</span><span class="sxs-lookup"><span data-stu-id="a747a-256">Token</span></span> | <span data-ttu-id="a747a-257">値のソース</span><span class="sxs-lookup"><span data-stu-id="a747a-257">Value source</span></span> | <span data-ttu-id="a747a-258">値</span><span class="sxs-lookup"><span data-stu-id="a747a-258">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="a747a-259">**$id$**</span><span class="sxs-lookup"><span data-stu-id="a747a-259">**$id$**</span></span> | <span data-ttu-id="a747a-260">プロジェクト ファイル</span><span class="sxs-lookup"><span data-stu-id="a747a-260">Project file</span></span> | <span data-ttu-id="a747a-261">プロジェクトファイルからの AssemblyName (title)</span><span class="sxs-lookup"><span data-stu-id="a747a-261">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="a747a-262">**$version$**</span><span class="sxs-lookup"><span data-stu-id="a747a-262">**$version$**</span></span> | <span data-ttu-id="a747a-263">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a747a-263">AssemblyInfo</span></span> | <span data-ttu-id="a747a-264">ある場合は AssemblyInformationalVersion、ない場合は AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="a747a-264">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="a747a-265">**$author$**</span><span class="sxs-lookup"><span data-stu-id="a747a-265">**$author$**</span></span> | <span data-ttu-id="a747a-266">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a747a-266">AssemblyInfo</span></span> | <span data-ttu-id="a747a-267">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="a747a-267">AssemblyCompany</span></span> |
| <span data-ttu-id="a747a-268">**$title $**</span><span class="sxs-lookup"><span data-stu-id="a747a-268">**$title$**</span></span> | <span data-ttu-id="a747a-269">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a747a-269">AssemblyInfo</span></span> | <span data-ttu-id="a747a-270">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="a747a-270">AssemblyTitle</span></span> |
| <span data-ttu-id="a747a-271">**$description$**</span><span class="sxs-lookup"><span data-stu-id="a747a-271">**$description$**</span></span> | <span data-ttu-id="a747a-272">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a747a-272">AssemblyInfo</span></span> | <span data-ttu-id="a747a-273">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="a747a-273">AssemblyDescription</span></span> |
| <span data-ttu-id="a747a-274">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="a747a-274">**$copyright$**</span></span> | <span data-ttu-id="a747a-275">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a747a-275">AssemblyInfo</span></span> | <span data-ttu-id="a747a-276">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="a747a-276">AssemblyCopyright</span></span> |
| <span data-ttu-id="a747a-277">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="a747a-277">**$configuration$**</span></span> | <span data-ttu-id="a747a-278">アセンブリ DLL</span><span class="sxs-lookup"><span data-stu-id="a747a-278">Assembly DLL</span></span> | <span data-ttu-id="a747a-279">アセンブリのビルドに使われる構成。既定値は Debug。</span><span class="sxs-lookup"><span data-stu-id="a747a-279">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="a747a-280">Release 構成を使ってパッケージを作成するには、常にコマンド ラインで `-properties Configuration=Release` を使うことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a747a-280">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="a747a-281">[アセンブリ ファイル](#including-assembly-files)および[コンテンツ ファイル](#including-content-files)を含めるときは、トークンを使ってパスを解決することもできます。</span><span class="sxs-lookup"><span data-stu-id="a747a-281">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="a747a-282">トークンの名前は MSBuild のプロパティと同じであり、現在のビルド構成に基づいて含めるファイルを選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="a747a-282">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="a747a-283">たとえば、`.nuspec` ファイルで次のトークンを使うものとします。</span><span class="sxs-lookup"><span data-stu-id="a747a-283">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="a747a-284">そして、MSBuild で `AssemblyName` が `LoggingLibrary` であるアセンブリを `Release` 構成でビルドすると、パッケージ内の `.nuspec` ファイルの行は結果として次のようになります。</span><span class="sxs-lookup"><span data-stu-id="a747a-284">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="a747a-285">Dependencies 要素</span><span class="sxs-lookup"><span data-stu-id="a747a-285">Dependencies element</span></span>

<span data-ttu-id="a747a-286">`<dependencies>` 内の `<metadata>` 要素は、最上位のパッケージが依存している他のパッケージを示す `<dependency>` 要素をいくつでも含むことができます。</span><span class="sxs-lookup"><span data-stu-id="a747a-286">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="a747a-287">各 `<dependency>` の属性は次にとおりです。</span><span class="sxs-lookup"><span data-stu-id="a747a-287">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="a747a-288">属性</span><span class="sxs-lookup"><span data-stu-id="a747a-288">Attribute</span></span> | <span data-ttu-id="a747a-289">説明</span><span class="sxs-lookup"><span data-stu-id="a747a-289">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="a747a-290">(必須) "EntityFramework" や "NUnit" などの依存関係のパッケージ ID。これはパッケージ ページに表示されるパッケージ nuget.org の名前となります。</span><span class="sxs-lookup"><span data-stu-id="a747a-290">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="a747a-291">(必須) 依存関係として許容されるバージョンの範囲。</span><span class="sxs-lookup"><span data-stu-id="a747a-291">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="a747a-292">厳密な構文については、「[Package versioning](../concepts/package-versioning.md#version-ranges)」(パッケージのバージョン管理) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-292">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="a747a-293">フローティングバージョンはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a747a-293">Floating versions are not supported.</span></span> |
| <span data-ttu-id="a747a-294">include</span><span class="sxs-lookup"><span data-stu-id="a747a-294">include</span></span> | <span data-ttu-id="a747a-295">最終的なパッケージに含める依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="a747a-295">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="a747a-296">既定値は `all` です。</span><span class="sxs-lookup"><span data-stu-id="a747a-296">The default value is `all`.</span></span> |
| <span data-ttu-id="a747a-297">exclude</span><span class="sxs-lookup"><span data-stu-id="a747a-297">exclude</span></span> | <span data-ttu-id="a747a-298">最終的なパッケージから除外する依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="a747a-298">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="a747a-299">既定値は `build,analyzers` を上書きすることができます。</span><span class="sxs-lookup"><span data-stu-id="a747a-299">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="a747a-300">ただし、`content/ ContentFiles` は、上書きできない最終的なパッケージでも暗黙的に除外されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-300">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="a747a-301">`exclude` で指定されているタグの方が、`include` で指定されているタグより優先されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-301">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="a747a-302">たとえば、`include="runtime, compile" exclude="compile"` は `include="runtime"` と同じです。</span><span class="sxs-lookup"><span data-stu-id="a747a-302">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="a747a-303">包含/除外タグ</span><span class="sxs-lookup"><span data-stu-id="a747a-303">Include/Exclude tag</span></span> | <span data-ttu-id="a747a-304">ターゲットの影響を受けるフォルダー</span><span class="sxs-lookup"><span data-stu-id="a747a-304">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="a747a-305">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a747a-305">contentFiles</span></span> | <span data-ttu-id="a747a-306">コンテンツ</span><span class="sxs-lookup"><span data-stu-id="a747a-306">Content</span></span> |
| <span data-ttu-id="a747a-307">runtime</span><span class="sxs-lookup"><span data-stu-id="a747a-307">runtime</span></span> | <span data-ttu-id="a747a-308">Runtime、Resources、FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="a747a-308">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="a747a-309">コンパイル</span><span class="sxs-lookup"><span data-stu-id="a747a-309">compile</span></span> | <span data-ttu-id="a747a-310">lib</span><span class="sxs-lookup"><span data-stu-id="a747a-310">lib</span></span> |
| <span data-ttu-id="a747a-311">build</span><span class="sxs-lookup"><span data-stu-id="a747a-311">build</span></span> | <span data-ttu-id="a747a-312">build (MSBuild のプロパティとターゲット)</span><span class="sxs-lookup"><span data-stu-id="a747a-312">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="a747a-313">native</span><span class="sxs-lookup"><span data-stu-id="a747a-313">native</span></span> | <span data-ttu-id="a747a-314">native</span><span class="sxs-lookup"><span data-stu-id="a747a-314">native</span></span> |
| <span data-ttu-id="a747a-315">なし</span><span class="sxs-lookup"><span data-stu-id="a747a-315">none</span></span> | <span data-ttu-id="a747a-316">フォルダーなし</span><span class="sxs-lookup"><span data-stu-id="a747a-316">No folders</span></span> |
| <span data-ttu-id="a747a-317">すべて</span><span class="sxs-lookup"><span data-stu-id="a747a-317">all</span></span> | <span data-ttu-id="a747a-318">すべてのフォルダー</span><span class="sxs-lookup"><span data-stu-id="a747a-318">All folders</span></span> |

<span data-ttu-id="a747a-319">たとえば、次の行は `PackageA` バージョン 1.1.0 以降および `PackageB` バージョン 1.x での依存関係を示します。</span><span class="sxs-lookup"><span data-stu-id="a747a-319">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="a747a-320">次の行も同じパッケージでの依存関係を示しますが、`contentFiles` の `build` および `PackageA` フォルダーを含めて、`native` の `compile` および `PackageB` フォルダーを除くすべてを含めることを指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-320">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="a747a-321">`nuget spec`を使用してプロジェクトから `.nuspec` を作成する場合、そのプロジェクトに存在する依存関係は、結果の `.nuspec` ファイルに自動的に含まれません。</span><span class="sxs-lookup"><span data-stu-id="a747a-321">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="a747a-322">代わりに、`nuget pack myproject.csproj`を使用し、生成された*nupkg*ファイル内から*nuspec*ファイルを取得します。</span><span class="sxs-lookup"><span data-stu-id="a747a-322">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="a747a-323">この*nuspec*には、依存関係が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a747a-323">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="a747a-324">依存関係グループ</span><span class="sxs-lookup"><span data-stu-id="a747a-324">Dependency groups</span></span>

<span data-ttu-id="a747a-325">*バージョン 2.0 以降*</span><span class="sxs-lookup"><span data-stu-id="a747a-325">*Version 2.0+*</span></span>

<span data-ttu-id="a747a-326">1 つのフラット リストの代わりに、`<group>` の `<dependencies>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って依存関係を指定できます。</span><span class="sxs-lookup"><span data-stu-id="a747a-326">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="a747a-327">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<dependency>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a747a-327">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="a747a-328">ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの依存関係が一緒にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a747a-328">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="a747a-329">依存関係の既定のリストまたはフォールバック リストとしては、`<group>` 属性のない `targetFramework` 要素が使われます。</span><span class="sxs-lookup"><span data-stu-id="a747a-329">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="a747a-330">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-330">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="a747a-331">グループの形式をフラット リストと併用することはできません。</span><span class="sxs-lookup"><span data-stu-id="a747a-331">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="a747a-332">`lib/ref` フォルダーで使用される[ターゲットフレームワークモニカー (tfm)](../reference/target-frameworks.md)の形式は、`dependency groups`で使用される tfm と比較して異なります。</span><span class="sxs-lookup"><span data-stu-id="a747a-332">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="a747a-333">`dependencies group` で宣言されたターゲットフレームワークと `.nuspec` ファイルの `lib/ref` フォルダーに完全に一致するものがない場合は、`pack` コマンドによって[NuGet 警告 NU5128](../reference/errors-and-warnings/nu5128.md)が発生します。</span><span class="sxs-lookup"><span data-stu-id="a747a-333">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="a747a-334">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="a747a-334">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="a747a-335">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="a747a-335">Explicit assembly references</span></span>

<span data-ttu-id="a747a-336">`<references>` 要素は、パッケージを使用するときにターゲットプロジェクトが参照するアセンブリを明示的に指定するために `packages.config` を使用するプロジェクトによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-336">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="a747a-337">明示的な参照は、通常、設計時のみのアセンブリに使われます。</span><span class="sxs-lookup"><span data-stu-id="a747a-337">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="a747a-338">詳細については、「[プロジェクトによって参照されるアセンブリの選択](../create-packages/select-assemblies-referenced-by-projects.md)」のページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="a747a-338">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="a747a-339">たとえば、次の `<references>` 要素は、パッケージに他のアセンブリがある場合でも、`xunit.dll` と `xunit.extensions.dll` に対する参照だけを追加するよう NuGet に指示します。</span><span class="sxs-lookup"><span data-stu-id="a747a-339">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="a747a-340">[参照グループ]</span><span class="sxs-lookup"><span data-stu-id="a747a-340">Reference groups</span></span>

<span data-ttu-id="a747a-341">1 つのフラット リストの代わりに、`<group>` の `<references>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って参照を指定できます。</span><span class="sxs-lookup"><span data-stu-id="a747a-341">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="a747a-342">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<reference>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a747a-342">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="a747a-343">ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの参照はプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-343">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="a747a-344">参照の既定のリストまたはフォールバック リストとしては、`<group>` 属性のない `targetFramework` 要素が使われます。</span><span class="sxs-lookup"><span data-stu-id="a747a-344">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="a747a-345">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-345">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="a747a-346">グループの形式をフラット リストと併用することはできません。</span><span class="sxs-lookup"><span data-stu-id="a747a-346">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="a747a-347">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="a747a-347">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="a747a-348">フレームワーク アセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="a747a-348">Framework assembly references</span></span>

<span data-ttu-id="a747a-349">フレームワーク アセンブリは、.NET Framework の一部であり、指定されたコンピューターのグローバル アセンブリ キャッシュ (GAC) に既に存在している必要があります。</span><span class="sxs-lookup"><span data-stu-id="a747a-349">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="a747a-350">`<frameworkAssemblies>` 要素でこれらのアセンブリを指定することにより、プロジェクトに必要な参照がまだない場合であっても、そのような参照をプロジェクトに確実に追加できます。</span><span class="sxs-lookup"><span data-stu-id="a747a-350">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="a747a-351">もちろん、そのようなアセンブリがパッケージに直接含まれることはありません。</span><span class="sxs-lookup"><span data-stu-id="a747a-351">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="a747a-352">`<frameworkAssemblies>` 要素には 0 個以上の `<frameworkAssembly>` 要素を含めることができ、それぞれで次の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-352">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="a747a-353">属性</span><span class="sxs-lookup"><span data-stu-id="a747a-353">Attribute</span></span> | <span data-ttu-id="a747a-354">説明</span><span class="sxs-lookup"><span data-stu-id="a747a-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a747a-355">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="a747a-355">**assemblyName**</span></span> | <span data-ttu-id="a747a-356">(必須) 完全修飾アセンブリ名。</span><span class="sxs-lookup"><span data-stu-id="a747a-356">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="a747a-357">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="a747a-357">**targetFramework**</span></span> | <span data-ttu-id="a747a-358">(省略可能) この参照を適用するターゲット フレームワークを指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-358">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="a747a-359">省略した場合は、参照がすべてのフレームワークに適用されることを示します。</span><span class="sxs-lookup"><span data-stu-id="a747a-359">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="a747a-360">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-360">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="a747a-361">次の例は、`System.Net` への参照はすべてのターゲット フレームワークに適用され、`System.ServiceModel` への参照は .NET Framework 4.0 のみに適用されることを示します。</span><span class="sxs-lookup"><span data-stu-id="a747a-361">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="a747a-362">アセンブリ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="a747a-362">Including assembly files</span></span>

<span data-ttu-id="a747a-363">「[パッケージを作成する](../create-packages/creating-a-package.md)」で説明されている規則に従う場合、`.nuspec` ファイルでファイルの一覧を明示的に指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a747a-363">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="a747a-364">`nuget pack` コマンドが必要なファイルを自動的に選びます。</span><span class="sxs-lookup"><span data-stu-id="a747a-364">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="a747a-365">プロジェクトにパッケージをインストールするとき、NuGet はパッケージの DLL にアセンブリ参照を自動的に追加します。ただし、指定されている  *は、ローカライズされたサテライト アセンブリであると見なされるため "* 除外`.resources.dll`" されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-365">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="a747a-366">そのため、避けなければ不可欠なパッケージ コードが含まれてしまうファイルには `.resources.dll` を使わないようにします。</span><span class="sxs-lookup"><span data-stu-id="a747a-366">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="a747a-367">この自動動作をバイパスして、パッケージに含めるファイルを明示的に制御するには、`<files>` 要素を `<package>` の子要素 (および `<metadata>` の兄弟要素) として配置し、各ファイルを個別の `<file>` 要素で示します。</span><span class="sxs-lookup"><span data-stu-id="a747a-367">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="a747a-368">例 :</span><span class="sxs-lookup"><span data-stu-id="a747a-368">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="a747a-369">NuGet 2.x 以前および `packages.config` を使っているプロジェクトでは、`<files>` 要素はパッケージのインストール時に変更できないコンテンツ ファイルを含めるためにも使われます。</span><span class="sxs-lookup"><span data-stu-id="a747a-369">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="a747a-370">NuGet 3.3 以降で、PackageReference を使用しているプロジェクトでは、代わりに `<contentFiles>` 要素が使用されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-370">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="a747a-371">詳しくは、後の「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-371">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="a747a-372">File 要素の属性</span><span class="sxs-lookup"><span data-stu-id="a747a-372">File element attributes</span></span>

<span data-ttu-id="a747a-373">各 `<file>` 要素では、次の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-373">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="a747a-374">属性</span><span class="sxs-lookup"><span data-stu-id="a747a-374">Attribute</span></span> | <span data-ttu-id="a747a-375">説明</span><span class="sxs-lookup"><span data-stu-id="a747a-375">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a747a-376">**src**</span><span class="sxs-lookup"><span data-stu-id="a747a-376">**src**</span></span> | <span data-ttu-id="a747a-377">含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。</span><span class="sxs-lookup"><span data-stu-id="a747a-377">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="a747a-378">絶対パスを指定しない限り、パスは `.nuspec` ファイルが基準になります。</span><span class="sxs-lookup"><span data-stu-id="a747a-378">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="a747a-379">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="a747a-379">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a747a-380">**target**</span><span class="sxs-lookup"><span data-stu-id="a747a-380">**target**</span></span> | <span data-ttu-id="a747a-381">ソース ファイルが格納されるパッケージ内のフォルダーへの相対パス。`lib`、`content`、`build`、または `tools` で始まっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a747a-381">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="a747a-382">[規則に基づく作業ディレクトリからの .nuspec の作成](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a747a-382">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="a747a-383">**exclude**</span><span class="sxs-lookup"><span data-stu-id="a747a-383">**exclude**</span></span> | <span data-ttu-id="a747a-384">`src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。</span><span class="sxs-lookup"><span data-stu-id="a747a-384">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="a747a-385">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="a747a-385">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="a747a-386">例</span><span class="sxs-lookup"><span data-stu-id="a747a-386">Examples</span></span>

<span data-ttu-id="a747a-387">**1 つのアセンブリ**</span><span class="sxs-lookup"><span data-stu-id="a747a-387">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="a747a-388">**ターゲット フレームワークに固有の 1 つのアセンブリ**</span><span class="sxs-lookup"><span data-stu-id="a747a-388">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="a747a-389">**ワイルドカードを使った DLL のセット**</span><span class="sxs-lookup"><span data-stu-id="a747a-389">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="a747a-390">**異なるフレームワークの DLL**</span><span class="sxs-lookup"><span data-stu-id="a747a-390">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="a747a-391">**ファイルの除外**</span><span class="sxs-lookup"><span data-stu-id="a747a-391">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="a747a-392">コンテンツ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="a747a-392">Including content files</span></span>

<span data-ttu-id="a747a-393">コンテンツ ファイルは、パッケージでプロジェクトに含める必要がある変更できないファイルです。</span><span class="sxs-lookup"><span data-stu-id="a747a-393">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="a747a-394">変更できないので、それを使うプロジェクトによる変更は意図されていません。</span><span class="sxs-lookup"><span data-stu-id="a747a-394">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="a747a-395">コンテンツ ファイルの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a747a-395">Example content files include:</span></span>

- <span data-ttu-id="a747a-396">リソースとして埋め込まれる画像</span><span class="sxs-lookup"><span data-stu-id="a747a-396">Images that are embedded as resources</span></span>
- <span data-ttu-id="a747a-397">コンパイル済みのソース ファイル</span><span class="sxs-lookup"><span data-stu-id="a747a-397">Source files that are already compiled</span></span>
- <span data-ttu-id="a747a-398">プロジェクトのビルド出力と共に含まれる必要があるスクリプト</span><span class="sxs-lookup"><span data-stu-id="a747a-398">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="a747a-399">プロジェクトに含まれる必要はあるが、プロジェクト固有の変更は必要ない、パッケージの構成ファイル</span><span class="sxs-lookup"><span data-stu-id="a747a-399">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="a747a-400">コンテンツ ファイルをパッケージに含めるには、`<files>` 要素を使い、`content` 属性で `target` フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-400">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="a747a-401">ただし、PackageReference を使用しているプロジェクトにパッケージをインストールする場合、このようなファイルは無視され、代わりに `<contentFiles>` 要素が使用されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-401">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="a747a-402">使用する側のプロジェクトとの最大限の互換性のため、パッケージでは両方の要素でコンテンツ ファイルを指定するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="a747a-402">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="a747a-403">コンテンツ ファイルに対する files 要素の使用</span><span class="sxs-lookup"><span data-stu-id="a747a-403">Using the files element for content files</span></span>

<span data-ttu-id="a747a-404">コンテンツ ファイルでは、アセンブリ ファイルの場合と同じ形式を使用しますが、次の例のように、`content` 属性で基本フォルダーとして `target` を指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-404">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="a747a-405">**基本的なコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="a747a-405">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="a747a-406">**ディレクトリ構造を持つコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="a747a-406">**Content files with directory structure**</span></span>

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

<span data-ttu-id="a747a-407">**ターゲット フレームワークに固有のコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="a747a-407">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="a747a-408">**名前のドットでフォルダーにコピーされるコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="a747a-408">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="a747a-409">この場合、NuGet は `target` の拡張子が `src` の拡張子と一致しないものと判断し、`target` での名前のその部分をフォルダーとして扱います。</span><span class="sxs-lookup"><span data-stu-id="a747a-409">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="a747a-410">**拡張子のないコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="a747a-410">**Content files without extensions**</span></span>

<span data-ttu-id="a747a-411">拡張子のないファイルを含めるには、ワイルドカード `*` または `**` を使います。</span><span class="sxs-lookup"><span data-stu-id="a747a-411">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="a747a-412">**深いパスと深いターゲットのコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="a747a-412">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="a747a-413">この場合、ソースとターゲットのファイル拡張子が一致するので、NuGet はターゲットがフォルダーではなくファイル名であると想定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-413">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="a747a-414">**パッケージ内のコンテンツ ファイルの名前の変更**</span><span class="sxs-lookup"><span data-stu-id="a747a-414">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="a747a-415">**ファイルの除外**</span><span class="sxs-lookup"><span data-stu-id="a747a-415">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="a747a-416">コンテンツ ファイルに対する contentFiles 要素の使用</span><span class="sxs-lookup"><span data-stu-id="a747a-416">Using the contentFiles element for content files</span></span>

<span data-ttu-id="a747a-417">*NuGet 4.0 以降で、PackageReference を使用している場合*</span><span class="sxs-lookup"><span data-stu-id="a747a-417">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="a747a-418">既定では、パッケージはコンテンツを `contentFiles` フォルダーに配置し (下記参照)、`nuget pack` は既定の属性を使ってそのフォルダーにすべてのファイルを格納します。</span><span class="sxs-lookup"><span data-stu-id="a747a-418">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="a747a-419">この場合は、`contentFiles` ノードを `.nuspec` に含める必要はまったくありません。</span><span class="sxs-lookup"><span data-stu-id="a747a-419">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="a747a-420">含まれるファイルを制御するには、含めるファイルを厳密に示す `<contentFiles>` 要素のコレクションである `<files>` 要素を指定します。</span><span class="sxs-lookup"><span data-stu-id="a747a-420">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="a747a-421">これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-421">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="a747a-422">属性</span><span class="sxs-lookup"><span data-stu-id="a747a-422">Attribute</span></span> | <span data-ttu-id="a747a-423">説明</span><span class="sxs-lookup"><span data-stu-id="a747a-423">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a747a-424">**include**</span><span class="sxs-lookup"><span data-stu-id="a747a-424">**include**</span></span> | <span data-ttu-id="a747a-425">(必須) 含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。</span><span class="sxs-lookup"><span data-stu-id="a747a-425">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="a747a-426">絶対パスが指定されていない場合、パスは `contentFiles` フォルダーの相対パスになります。</span><span class="sxs-lookup"><span data-stu-id="a747a-426">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="a747a-427">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="a747a-427">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a747a-428">**exclude**</span><span class="sxs-lookup"><span data-stu-id="a747a-428">**exclude**</span></span> | <span data-ttu-id="a747a-429">`src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。</span><span class="sxs-lookup"><span data-stu-id="a747a-429">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="a747a-430">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="a747a-430">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a747a-431">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="a747a-431">**buildAction**</span></span> | <span data-ttu-id="a747a-432">MSBuild のコンテンツ項目に割り当てるビルドアクション (`Content`、`None`、`Embedded Resource`、`Compile`など)。既定値は `Compile`です。</span><span class="sxs-lookup"><span data-stu-id="a747a-432">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="a747a-433">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="a747a-433">**copyToOutput**</span></span> | <span data-ttu-id="a747a-434">コンテンツ項目をビルド (または発行) 出力フォルダーにコピーするかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="a747a-434">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="a747a-435">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="a747a-435">The default is false.</span></span> |
| <span data-ttu-id="a747a-436">**flatten**</span><span class="sxs-lookup"><span data-stu-id="a747a-436">**flatten**</span></span> | <span data-ttu-id="a747a-437">コンテンツ項目をビルド出力の単一フォルダーにコピーするか (true)、それともパッケージのフォルダー構造を保持するか (false) を示すブール値。</span><span class="sxs-lookup"><span data-stu-id="a747a-437">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="a747a-438">このフラグは、copyToOutput が true に設定されている場合のみ機能します。</span><span class="sxs-lookup"><span data-stu-id="a747a-438">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="a747a-439">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="a747a-439">The default is false.</span></span> |

<span data-ttu-id="a747a-440">パッケージをインストールするとき、NuGet は `<contentFiles>` の子要素を上から下に順番に適用します。</span><span class="sxs-lookup"><span data-stu-id="a747a-440">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="a747a-441">複数のエントリが同じファイルに一致する場合は、すべてのエントリが適用されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-441">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="a747a-442">同じ属性に対して競合がある場合は、最上位のエントリが下位のエントリをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="a747a-442">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="a747a-443">パッケージ フォルダーの構造</span><span class="sxs-lookup"><span data-stu-id="a747a-443">Package folder structure</span></span>

<span data-ttu-id="a747a-444">パッケージ プロジェクトでは、次のパターンを使ってコンテンツを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a747a-444">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="a747a-445">`codeLanguages` には、`cs`、`vb`、`fs`、`any`、または指定された `$(ProjectLanguage)` に相当する小文字表現を指定できます。</span><span class="sxs-lookup"><span data-stu-id="a747a-445">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="a747a-446">`TxM` は、NuGet がサポートする任意の有効なターゲット フレームワーク モニカーです (「[ターゲット フレームワーク](../reference/target-frameworks.md)」を参照)。</span><span class="sxs-lookup"><span data-stu-id="a747a-446">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="a747a-447">この構文の末尾に、任意のフォルダー構造を追加できます。</span><span class="sxs-lookup"><span data-stu-id="a747a-447">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="a747a-448">例 :</span><span class="sxs-lookup"><span data-stu-id="a747a-448">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="a747a-449">空のフォルダーでは、`.` を使って、言語と TxM の特定の組み合わせにコンテンツを提供しないようにすることができます。次はその例です。</span><span class="sxs-lookup"><span data-stu-id="a747a-449">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="a747a-450">contentFiles セクションの例</span><span class="sxs-lookup"><span data-stu-id="a747a-450">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
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
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a><span data-ttu-id="a747a-451">フレームワーク参照グループ</span><span class="sxs-lookup"><span data-stu-id="a747a-451">Framework reference groups</span></span>

<span data-ttu-id="a747a-452">*バージョン 5.1 + 追加 PackageReference のみ*</span><span class="sxs-lookup"><span data-stu-id="a747a-452">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="a747a-453">フレームワーク参照は、WPF や Windows フォームなどの共有フレームワークを表す .NET Core の概念です。</span><span class="sxs-lookup"><span data-stu-id="a747a-453">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="a747a-454">共有フレームワークを指定することで、パッケージによって、すべてのフレームワークの依存関係が参照元のプロジェクトに含まれるようになります。</span><span class="sxs-lookup"><span data-stu-id="a747a-454">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="a747a-455">各 `<group>` 要素には、`targetFramework` 属性と0個以上の `<frameworkReference>` 要素が必要です。</span><span class="sxs-lookup"><span data-stu-id="a747a-455">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="a747a-456">次の例は、.NET Core WPF プロジェクト用に生成された nuspec を示しています。</span><span class="sxs-lookup"><span data-stu-id="a747a-456">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="a747a-457">フレームワーク参照を含む手動作成 nuspecs は推奨されません。</span><span class="sxs-lookup"><span data-stu-id="a747a-457">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="a747a-458">代わりに、[ターゲット](msbuild-targets.md)パックを使用することを検討してください。これにより、プロジェクトからそれらが自動的に推論されます。</span><span class="sxs-lookup"><span data-stu-id="a747a-458">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="a747a-459">Nuspec ファイルの例</span><span class="sxs-lookup"><span data-stu-id="a747a-459">Example nuspec files</span></span>

<span data-ttu-id="a747a-460">**依存関係またはファイルを指定しない単純な `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="a747a-460">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="a747a-461">**依存関係を含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="a747a-461">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="a747a-462">**ファイルを含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="a747a-462">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="a747a-463">**フレームワーク アセンブリを含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="a747a-463">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="a747a-464">この例では、指定したプロジェクト ターゲットに次のものがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a747a-464">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="a747a-465">.NET4 -> `System.Web`、`System.Net`</span><span class="sxs-lookup"><span data-stu-id="a747a-465">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="a747a-466">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="a747a-466">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="a747a-467">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="a747a-467">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="a747a-468">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="a747a-468">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
