---
title: NuGet の nuspec ファイルリファレンス
description: .nuspec ファイルには、パッケージを作成するとき、およびパッケージのコンシューマーに情報を提供するために使われる、パッケージのメタデータが含まれています。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6e5107ac05046ea46cc819ebe2a504ba6b030634
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738943"
---
# <a name="nuspec-reference"></a><span data-ttu-id="88811-103">.nuspec リファレンス</span><span class="sxs-lookup"><span data-stu-id="88811-103">.nuspec reference</span></span>

<span data-ttu-id="88811-104">`.nuspec` ファイルは、パッケージのメタデータが含まれている XML マニフェストです。</span><span class="sxs-lookup"><span data-stu-id="88811-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="88811-105">このマニフェストは、パッケージを作成するためと、コンシューマーに情報を提供するための、両方に使われます。</span><span class="sxs-lookup"><span data-stu-id="88811-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="88811-106">パッケージにはマニフェストが常に含まれています。</span><span class="sxs-lookup"><span data-stu-id="88811-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="88811-107">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="88811-107">In this topic:</span></span>

- [<span data-ttu-id="88811-108">一般的な形式とスキーマ</span><span class="sxs-lookup"><span data-stu-id="88811-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="88811-109">[置換トークン](#replacement-tokens) (Visual Studio プロジェクトで使われるとき)</span><span class="sxs-lookup"><span data-stu-id="88811-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="88811-110">依存関係</span><span class="sxs-lookup"><span data-stu-id="88811-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="88811-111">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="88811-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="88811-112">フレームワーク アセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="88811-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="88811-113">アセンブリ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="88811-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="88811-114">コンテンツ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="88811-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="88811-115">Nuspec ファイルの例</span><span class="sxs-lookup"><span data-stu-id="88811-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="88811-116">プロジェクトの種類の互換性</span><span class="sxs-lookup"><span data-stu-id="88811-116">Project type compatibility</span></span>

- <span data-ttu-id="88811-117">を `.nuspec` `nuget.exe pack` 使用する非 SDK 形式のプロジェクトには、を使用し `packages.config` ます。</span><span class="sxs-lookup"><span data-stu-id="88811-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="88811-118">`.nuspec` [Sdk スタイルのプロジェクト](../resources/check-project-format.md)のパッケージを作成するためにファイルは必要ありません (通常、 [sdk 属性](/dotnet/core/tools/csproj#additions)を使用する .net Core および .NET Standard プロジェクト)。</span><span class="sxs-lookup"><span data-stu-id="88811-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="88811-119">( `.nuspec` パッケージの作成時にが生成されることに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="88811-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="88811-120">またはを使用してパッケージを作成する場合は、 `dotnet.exe pack` `msbuild pack target` 通常、ファイル内の [すべてのプロパティ](../reference/msbuild-targets.md#pack-target) をプロジェクトファイルに含めることをお勧め `.nuspec` します。</span><span class="sxs-lookup"><span data-stu-id="88811-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="88811-121">ただし、代わりに[ `.nuspec` `dotnet.exe` また `msbuild pack target` はを使用して、パックするファイルを使用](../reference/msbuild-targets.md#packing-using-a-nuspec)することもできます。</span><span class="sxs-lookup"><span data-stu-id="88811-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="88811-122">から PackageReference に移行されたプロジェクトでは、 `packages.config` パッケージを[PackageReference](../consume-packages/package-references-in-project-files.md) `.nuspec` 作成するためにファイルは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="88811-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="88811-123">代わりに、 [msbuild-{0}](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)を使用します。</span><span class="sxs-lookup"><span data-stu-id="88811-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="88811-124">一般的な形式とスキーマ</span><span class="sxs-lookup"><span data-stu-id="88811-124">General form and schema</span></span>

<span data-ttu-id="88811-125">最新の `nuspec.xsd` スキーマ ファイルは、[NuGet GitHub リポジトリ](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)にあります。</span><span class="sxs-lookup"><span data-stu-id="88811-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="88811-126">このスキーマでの `.nuspec` ファイルの一般的な形式は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="88811-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="88811-127">スキーマの視覚的な表現をはっきり表示したい場合は、Visual Studio のデザイン モードでスキーマ ファイルを開き、**[XML スキーマ エクスプローラー]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="88811-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="88811-128">または、コードとしてファイルを開き、エディター内を右クリックして、**[XML スキーマ エクスプローラーで表示]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="88811-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="88811-129">どちらの方法でも次のように表示されます (ほとんどを展開した場合)。</span><span class="sxs-lookup"><span data-stu-id="88811-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio のスキーマ エクスプローラーで開いた nuspec.xsd](media/SchemaExplorer.png)

<span data-ttu-id="88811-131">一般的な XML の場合と同様に、nuspec ファイル内のすべての XML 要素名で大文字と小文字が区別されます。</span><span class="sxs-lookup"><span data-stu-id="88811-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="88811-132">たとえば、メタデータ要素の使用 `<description>` は正しいので、 `<Description>` 正しくありません。</span><span class="sxs-lookup"><span data-stu-id="88811-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="88811-133">各要素名の適切な大文字と小文字の指定については、以下で説明します。</span><span class="sxs-lookup"><span data-stu-id="88811-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="88811-134">メタデータの必須要素</span><span class="sxs-lookup"><span data-stu-id="88811-134">Required metadata elements</span></span>

<span data-ttu-id="88811-135">以下の要素はパッケージの最低要件であり、[メタデータの省略可能な要素](#optional-metadata-elements)を追加してパッケージに関する開発者の全体的なエクスペリエンスを向上させることを検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="88811-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="88811-136">これらの要素は、`<metadata>` 要素内で指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="88811-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="88811-137">id</span><span class="sxs-lookup"><span data-stu-id="88811-137">id</span></span> 
<span data-ttu-id="88811-138">パッケージの識別子。大文字と小文字が区別されます。nuget.org 全体で、またはパッケージが存在するギャラリー全体で、一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="88811-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="88811-139">ID は、スペースまたは URL で無効な文字を含んでいてはならず、一般に .NET 名前空間の規則に従います。</span><span class="sxs-lookup"><span data-stu-id="88811-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="88811-140">ガイダンスについては、[一意のパッケージ識別子の選択](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="88811-141">パッケージを nuget.org にアップロードする場合、 `id` フィールドの文字数は128文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="88811-142">version</span><span class="sxs-lookup"><span data-stu-id="88811-142">version</span></span>
<span data-ttu-id="88811-143">パッケージのバージョン。*major.minor.patch* のパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="88811-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="88811-144">「[Package versioning](../concepts/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) で説明されているように、バージョン番号にはプレリリースのサフィックスを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="88811-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="88811-145">パッケージを nuget.org にアップロードする場合、 `version` フィールドの文字数は64文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="88811-146">description</span><span class="sxs-lookup"><span data-stu-id="88811-146">description</span></span>
<span data-ttu-id="88811-147">UI 表示用のパッケージの説明。</span><span class="sxs-lookup"><span data-stu-id="88811-147">A description of the package for UI display.</span></span>

<span data-ttu-id="88811-148">パッケージを nuget.org にアップロードする場合、 `description` フィールドの文字数は4000文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="88811-149">作成者</span><span class="sxs-lookup"><span data-stu-id="88811-149">authors</span></span>
<span data-ttu-id="88811-150">Nuget.org のプロファイル名と一致するパッケージ作成者のコンマ区切りのリスト。これらは nuget.org の NuGet ギャラリーに表示され、同じ作成者によってパッケージを相互参照するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="88811-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="88811-151">パッケージを nuget.org にアップロードする場合、 `authors` フィールドの文字数は4000文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="88811-152">メタデータの省略可能な要素</span><span class="sxs-lookup"><span data-stu-id="88811-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="88811-153">owners</span><span class="sxs-lookup"><span data-stu-id="88811-153">owners</span></span>
> [!Important]
> <span data-ttu-id="88811-154">所有者は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="88811-154">owners is deprecated.</span></span> <span data-ttu-id="88811-155">代わりに、作成者を使用してください。</span><span class="sxs-lookup"><span data-stu-id="88811-155">Use authors instead.</span></span>

<span data-ttu-id="88811-156">Nuget.org のプロファイル名を使用して、パッケージ作成者のコンマ区切りのリスト。多くの場合、このリストはと同じです `authors` 。パッケージを nuget.org にアップロードするときには無視されます。「 [Nuget.org でのパッケージ所有者の管理」を](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)参照してください。</span><span class="sxs-lookup"><span data-stu-id="88811-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="88811-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="88811-157">projectUrl</span></span>
<span data-ttu-id="88811-158">パッケージのホーム ページの URL。多くの場合、UI 画面と nuget.org に表示されます。</span><span class="sxs-lookup"><span data-stu-id="88811-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="88811-159">パッケージを nuget.org にアップロードする場合、 `projectUrl` フィールドの文字数は4000文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="88811-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="88811-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="88811-161">licenseUrl は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="88811-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="88811-162">代わりにライセンスを使用してください。</span><span class="sxs-lookup"><span data-stu-id="88811-162">Use license instead.</span></span>

<span data-ttu-id="88811-163">パッケージのライセンスの URL。多くの場合、nuget.org のような Ui に表示されます。</span><span class="sxs-lookup"><span data-stu-id="88811-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="88811-164">パッケージを nuget.org にアップロードする場合、 `licenseUrl` フィールドの文字数は4000文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="88811-165">license</span><span class="sxs-lookup"><span data-stu-id="88811-165">license</span></span>

<span data-ttu-id="88811-166">***NuGet 4.9.0-** 以降でサポートされています*</span><span class="sxs-lookup"><span data-stu-id="88811-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="88811-167">SPDX ライセンス式またはパッケージ内のライセンスファイルへのパス。多くの場合、nuget.org のような Ui に表示されます。MIT や BSD-2 句などの一般的なライセンスでパッケージのライセンスを取得している場合は、関連付けられている [Spdx ライセンス識別子](https://spdx.org/licenses/)を使用します。</span><span class="sxs-lookup"><span data-stu-id="88811-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="88811-168">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="88811-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="88811-169">NuGet.org は、オープンソースイニシアチブまたは無償のソフトウェア基盤によって承認されたライセンス式のみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="88811-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="88811-170">パッケージが複数の一般的なライセンスでライセンスされている場合は、 [Spdx 式の構文バージョン 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)を使用して複合ライセンスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="88811-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="88811-171">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="88811-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="88811-172">ライセンス式でサポートされていないカスタムライセンスを使用する場合は、 `.txt` または `.md` ファイルをライセンスのテキストと共にパッケージ化することができます。</span><span class="sxs-lookup"><span data-stu-id="88811-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="88811-173">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="88811-173">For example:</span></span>

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

<span data-ttu-id="88811-174">同等の MSBuild については、 [ライセンス式またはライセンスファイルのパッキング](msbuild-targets.md#packing-a-license-expression-or-a-license-file)に関する説明を参照してください。</span><span class="sxs-lookup"><span data-stu-id="88811-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="88811-175">NuGet のライセンス式の正確な構文については、 [Abnf](https://tools.ietf.org/html/rfc5234)で説明します。</span><span class="sxs-lookup"><span data-stu-id="88811-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="88811-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="88811-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="88811-177">iconUrl は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="88811-177">iconUrl is deprecated.</span></span> <span data-ttu-id="88811-178">代わりにアイコンを使用してください。</span><span class="sxs-lookup"><span data-stu-id="88811-178">Use icon instead.</span></span>

<span data-ttu-id="88811-179">UI 表示でパッケージのアイコンとして使用される透明な背景を持つ128x128 イメージの URL。</span><span class="sxs-lookup"><span data-stu-id="88811-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="88811-180">この要素の値は、"*画像を直接示す URL*" であり、画像を含む Web ページの URL ではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="88811-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="88811-181">たとえば、GitHub のイメージを使用するには、" <em> https://github.com/ \<username\> / \<repository\> /raw/ \<branch\> / \<logo.png\> </em>" のような raw ファイル URL を使用します。</span><span class="sxs-lookup"><span data-stu-id="88811-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
<span data-ttu-id="88811-182">パッケージを nuget.org にアップロードする場合、 `iconUrl` フィールドの文字数は4000文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="88811-183">icon</span><span class="sxs-lookup"><span data-stu-id="88811-183">icon</span></span>

<span data-ttu-id="88811-184">***NuGet 5.3.0** 以降でサポートされています*</span><span class="sxs-lookup"><span data-stu-id="88811-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="88811-185">これはパッケージ内のイメージファイルへのパスであり、多くの場合、パッケージアイコンとして nuget.org のような Ui に表示されます。</span><span class="sxs-lookup"><span data-stu-id="88811-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="88811-186">イメージファイルのサイズは 1 MB に制限されています。</span><span class="sxs-lookup"><span data-stu-id="88811-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="88811-187">サポートされているファイル形式は、JPEG および PNG です。</span><span class="sxs-lookup"><span data-stu-id="88811-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="88811-188">128x128 のイメージの解像度をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="88811-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="88811-189">たとえば、nuget.exe を使用してパッケージを作成するときに、次のコードを nuspec に追加します。</span><span class="sxs-lookup"><span data-stu-id="88811-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="88811-190">パッケージアイコン nuspec サンプル。</span><span class="sxs-lookup"><span data-stu-id="88811-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="88811-191">同等の MSBuild については、「 [アイコンイメージファイルのパッキング」](msbuild-targets.md#packing-an-icon-image-file)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="88811-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="88811-192">を `icon` `iconUrl` サポートしていないソースとの下位互換性を維持するために、との両方を指定でき `icon` ます。</span><span class="sxs-lookup"><span data-stu-id="88811-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="88811-193">Visual Studio では `icon` 、将来のリリースでフォルダーベースのソースからのパッケージがサポートされるようになります。</span><span class="sxs-lookup"><span data-stu-id="88811-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="88811-194">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="88811-194">requireLicenseAcceptance</span></span>
<span data-ttu-id="88811-195">パッケージをインストールする前にクライアントがユーザーに対してパッケージのライセンスへの同意を求めるプロンプトを表示する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="88811-195">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="88811-196">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="88811-196">developmentDependency</span></span>
<span data-ttu-id="88811-197">*(2.8 以降)* 開発専用の依存関係としてパッケージをマークするかどうかを指定するブール値。指定すると、そのパッケージは他のパッケージに依存関係として含まれなくなります。</span><span class="sxs-lookup"><span data-stu-id="88811-197">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="88811-198">PackageReference (NuGet 4.8 以降) では、このフラグは、コンパイルからコンパイル時アセットを除外することも意味します。</span><span class="sxs-lookup"><span data-stu-id="88811-198">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="88811-199">「 [DevelopmentDependency support For PackageReference」を](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)参照してください。</span><span class="sxs-lookup"><span data-stu-id="88811-199">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="88811-200">まとめ</span><span class="sxs-lookup"><span data-stu-id="88811-200">summary</span></span>
> [!Important]
> <span data-ttu-id="88811-201">`summary` は非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="88811-201">`summary` is being deprecated.</span></span> <span data-ttu-id="88811-202">代わりに、`description` を使用してください。</span><span class="sxs-lookup"><span data-stu-id="88811-202">Use `description` instead.</span></span>

<span data-ttu-id="88811-203">UI 画面用のパッケージの短い説明。</span><span class="sxs-lookup"><span data-stu-id="88811-203">A short description of the package for UI display.</span></span> <span data-ttu-id="88811-204">省略すると、`description` を切り詰めたバージョンが使われます。</span><span class="sxs-lookup"><span data-stu-id="88811-204">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="88811-205">パッケージを nuget.org にアップロードする場合、 `summary` フィールドの文字数は4000文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-205">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="88811-206">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="88811-206">releaseNotes</span></span>
<span data-ttu-id="88811-207">*(1.5 以降)* このリリースのパッケージで行われた変更の説明。Visual Studio パッケージ マネージャーの **[更新]** タブなどの UI で、パッケージの説明の代わりによく使われます。</span><span class="sxs-lookup"><span data-stu-id="88811-207">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="88811-208">パッケージを nuget.org にアップロードする場合、 `releaseNotes` フィールドの文字数は35000文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-208">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="88811-209">著作権</span><span class="sxs-lookup"><span data-stu-id="88811-209">copyright</span></span>
<span data-ttu-id="88811-210">*(1.5 以降)* パッケージの著作権の詳細。</span><span class="sxs-lookup"><span data-stu-id="88811-210">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="88811-211">パッケージを nuget.org にアップロードする場合、 `copyright` フィールドの文字数は4000文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-211">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="88811-212">language</span><span class="sxs-lookup"><span data-stu-id="88811-212">language</span></span>
<span data-ttu-id="88811-213">パッケージのロケール ID。</span><span class="sxs-lookup"><span data-stu-id="88811-213">The locale ID for the package.</span></span> <span data-ttu-id="88811-214">「[ローカライズされたパッケージの作成](../create-packages/creating-localized-packages.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-214">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="88811-215">tags</span><span class="sxs-lookup"><span data-stu-id="88811-215">tags</span></span>
<span data-ttu-id="88811-216">パッケージについて説明し、検索やフィルターでパッケージを見つけやすくするタグやキーワードを、スペースで区切って列記したリスト。</span><span class="sxs-lookup"><span data-stu-id="88811-216">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="88811-217">パッケージを nuget.org にアップロードする場合、 `tags` フィールドの文字数は4000文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-217">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="88811-218">serviceable</span><span class="sxs-lookup"><span data-stu-id="88811-218">serviceable</span></span> 
<span data-ttu-id="88811-219">*(3.3 以降)* NuGet 内部でのみ使われます。</span><span class="sxs-lookup"><span data-stu-id="88811-219">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="88811-220">repository</span><span class="sxs-lookup"><span data-stu-id="88811-220">repository</span></span>
<span data-ttu-id="88811-221">リポジトリメタデータ。4つの省略可能な属性で構成されています: `type` and `url` *(4.0 +)*、and `branch` `commit` *(4.6 +)*。</span><span class="sxs-lookup"><span data-stu-id="88811-221">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="88811-222">これらの属性を使用すると、を構築したリポジトリにをマップすることができ `.nupkg` ます。これにより、パッケージを構築した個々のブランチ名またはコミット sha-1 ハッシュが詳細に表示されます。</span><span class="sxs-lookup"><span data-stu-id="88811-222">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="88811-223">これは、バージョン管理ソフトウェアによって直接呼び出すことができる、一般公開されている url である必要があります。</span><span class="sxs-lookup"><span data-stu-id="88811-223">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="88811-224">これはコンピューター用の html ページである必要はありません。</span><span class="sxs-lookup"><span data-stu-id="88811-224">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="88811-225">[プロジェクトへのリンク] ページでは、代わりにフィールドを使用し `projectUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="88811-225">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="88811-226">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="88811-226">For example:</span></span>
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

<span data-ttu-id="88811-227">パッケージを nuget.org にアップロードする場合、 `type` 属性は100文字に制限され、 `url` 属性は4000文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-227">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="88811-228">title</span><span class="sxs-lookup"><span data-stu-id="88811-228">title</span></span>
<span data-ttu-id="88811-229">UI 表示で使用できる、パッケージのわかりやすいタイトル。</span><span class="sxs-lookup"><span data-stu-id="88811-229">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="88811-230">(Visual Studio の nuget.org とパッケージマネージャーにはタイトルが表示されません)</span><span class="sxs-lookup"><span data-stu-id="88811-230">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="88811-231">パッケージを nuget.org にアップロードする場合、 `title` フィールドは256文字に制限されますが、表示目的では使用されません。</span><span class="sxs-lookup"><span data-stu-id="88811-231">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="88811-232">コレクション要素</span><span class="sxs-lookup"><span data-stu-id="88811-232">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="88811-233">packageTypes</span><span class="sxs-lookup"><span data-stu-id="88811-233">packageTypes</span></span>
<span data-ttu-id="88811-234">*(3.5 以降)* 従来の依存関係パッケージ以外の場合に、パッケージの種類を指定する 0 個以上の `<packageType>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="88811-234">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="88811-235">各 packageType は、*name* 属性と *version* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="88811-235">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="88811-236">「[Setting a package type](../create-packages/set-package-type.md)」(パッケージの種類の設定) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-236">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="88811-237">依存関係</span><span class="sxs-lookup"><span data-stu-id="88811-237">dependencies</span></span>
<span data-ttu-id="88811-238">パッケージの依存関係を指定する 0 個以上の `<dependency>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="88811-238">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="88811-239">各 dependency は、*id*、*version*、*include* (3.x 以降)、*exclude* (3.x 以降) の各属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="88811-239">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="88811-240">後の「[依存関係](#dependencies-element)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-240">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="88811-241">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="88811-241">frameworkAssemblies</span></span>
<span data-ttu-id="88811-242">*(1.2 以降)* このパッケージで必要な .NET Framework アセンブリ参照を示す 0 個以上の `<frameworkAssembly>` 要素のコレクション。パッケージを使うプロジェクトに参照が確実に追加されるようにします。</span><span class="sxs-lookup"><span data-stu-id="88811-242">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="88811-243">各 frameworkAssembly は、*assemblyName* 属性と *targetFramework* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="88811-243">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="88811-244">[フレームワーク アセンブリ参照 GAC の指定](#specifying-framework-assembly-references-gac)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-244">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="88811-245">references</span><span class="sxs-lookup"><span data-stu-id="88811-245">references</span></span>
<span data-ttu-id="88811-246">*(1.5 以降)* パッケージの `lib` フォルダー内のアセンブリのうちプロジェクト参照として追加するものを指定する、0 個以上の `<reference>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="88811-246">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="88811-247">各参照は、*file* 属性を持っています。</span><span class="sxs-lookup"><span data-stu-id="88811-247">Each reference has a *file* attribute.</span></span> <span data-ttu-id="88811-248">`<references>` は `<group>` 要素を含むこともでき、その *targetFramework* 属性に `<reference>` 要素を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="88811-248">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="88811-249">省略すると、`lib` のすべての参照が含まれます。</span><span class="sxs-lookup"><span data-stu-id="88811-249">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="88811-250">[明示的なアセンブリ参照の指定](#specifying-explicit-assembly-references)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-250">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="88811-251">contentFiles</span><span class="sxs-lookup"><span data-stu-id="88811-251">contentFiles</span></span>
<span data-ttu-id="88811-252">*(3.3 以降)* 使用する側のプロジェクトに含めるコンテンツ ファイルを示す `<files>` 要素のコレクション。</span><span class="sxs-lookup"><span data-stu-id="88811-252">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="88811-253">これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。</span><span class="sxs-lookup"><span data-stu-id="88811-253">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="88811-254">[パッケージに含めるファイルの指定](#specifying-files-to-include-in-the-package)に関する後の説明をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-254">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="88811-255">files</span><span class="sxs-lookup"><span data-stu-id="88811-255">files</span></span> 
<span data-ttu-id="88811-256">ノードには `<package>` `<files>` `<metadata>` 、 `<contentFiles>` パッケージに `<metadata>` 含めるアセンブリおよびコンテンツファイルを指定するためのノードが、の兄弟として、およびの子として含まれている場合があります。</span><span class="sxs-lookup"><span data-stu-id="88811-256">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="88811-257">詳しくは、このトピックで後述する「[アセンブリ ファイルを含める](#including-assembly-files)」と「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-257">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="88811-258">メタデータ属性</span><span class="sxs-lookup"><span data-stu-id="88811-258">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="88811-259">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="88811-259">minClientVersion</span></span>
<span data-ttu-id="88811-260">nuget.exe および Visual Studio パッケージ マネージャーで強制する、このパッケージをインストールできる NuGet クライアントの最小バージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="88811-260">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="88811-261">これは、NuGet クライアントの特定のバージョンで追加された `.nuspec` ファイルの特定の機能にパッケージが依存しているときに、常に使われます。</span><span class="sxs-lookup"><span data-stu-id="88811-261">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="88811-262">たとえば、`developmentDependency` 属性を使っているパッケージでは、`minClientVersion` に "2.8" を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="88811-262">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="88811-263">同様に、`contentFiles` 要素 (次のセクションを参照) を使っているパッケージでは、`minClientVersion` を "3.3" に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="88811-263">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="88811-264">また、バージョン 2.5 より前の NuGet クライアントはこのフラグを認識しないので、`minClientVersion` の値が何であっても、"*常に*" パッケージをインストールしないことにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="88811-264">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

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

## <a name="replacement-tokens"></a><span data-ttu-id="88811-265">置換トークン</span><span class="sxs-lookup"><span data-stu-id="88811-265">Replacement tokens</span></span>

<span data-ttu-id="88811-266">パッケージを作成する場合、 [ `nuget pack` コマンド](../reference/cli-reference/cli-ref-pack.md)は、ファイルのノード内の $ で区切られたトークンを、 `.nuspec` `<metadata>` プロジェクトファイルまたはコマンドのスイッチから取得した値に置き換え `pack` `-properties` ます。</span><span class="sxs-lookup"><span data-stu-id="88811-266">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="88811-267">コマンド ラインでは、`nuget pack -properties <name>=<value>;<name>=<value>` でトークンの値を指定します。</span><span class="sxs-lookup"><span data-stu-id="88811-267">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="88811-268">たとえば、`.nuspec` では `$owners$` や `$desc$` などのトークンを使っておき、パッキング時に次のようにして値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="88811-268">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="88811-269">プロジェクトの値を使うには、次の表で説明するトークンを指定します (AssemblyInfo は、`Properties` 内の `AssemblyInfo.cs` や `AssemblyInfo.vb` などのファイルを参照します)。</span><span class="sxs-lookup"><span data-stu-id="88811-269">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="88811-270">これらのトークンを使うには、`nuget pack` を実行するときに、`.nuspec` だけでなくプロジェクト ファイルも指定します。</span><span class="sxs-lookup"><span data-stu-id="88811-270">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="88811-271">たとえば、次のコマンドを使うと、`.nuspec` ファイルの `$id$` および `$version$` トークンが、プロジェクトの `AssemblyName` および `AssemblyVersion` の値に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="88811-271">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="88811-272">通常、プロジェクトがある場合は、最初に `nuget spec MyProject.csproj` を使って `.nuspec` を作成すると、一部の標準的なトークンが自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="88811-272">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="88811-273">ただし、`.nuspec` の必須要素に対する値がプロジェクトにないと、`nuget pack` は失敗します。</span><span class="sxs-lookup"><span data-stu-id="88811-273">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="88811-274">さらに、プロジェクトの値を変更する場合は、パッケージを作成する前に必ずビルドし直してください。これは、pack コマンドの `build` スイッチで簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="88811-274">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="88811-275">例外である `$configuration$` を除き、コマンド ラインの同じトークンに割り当てられている値より、プロジェクトの値の方が優先的に使われます。</span><span class="sxs-lookup"><span data-stu-id="88811-275">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="88811-276">トークン</span><span class="sxs-lookup"><span data-stu-id="88811-276">Token</span></span> | <span data-ttu-id="88811-277">値のソース</span><span class="sxs-lookup"><span data-stu-id="88811-277">Value source</span></span> | <span data-ttu-id="88811-278">値</span><span class="sxs-lookup"><span data-stu-id="88811-278">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="88811-279">**$id $**</span><span class="sxs-lookup"><span data-stu-id="88811-279">**$id$**</span></span> | <span data-ttu-id="88811-280">プロジェクト ファイル</span><span class="sxs-lookup"><span data-stu-id="88811-280">Project file</span></span> | <span data-ttu-id="88811-281">プロジェクトファイルからの AssemblyName (title)</span><span class="sxs-lookup"><span data-stu-id="88811-281">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="88811-282">**$version $**</span><span class="sxs-lookup"><span data-stu-id="88811-282">**$version$**</span></span> | <span data-ttu-id="88811-283">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="88811-283">AssemblyInfo</span></span> | <span data-ttu-id="88811-284">ある場合は AssemblyInformationalVersion、ない場合は AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="88811-284">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="88811-285">**$author $**</span><span class="sxs-lookup"><span data-stu-id="88811-285">**$author$**</span></span> | <span data-ttu-id="88811-286">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="88811-286">AssemblyInfo</span></span> | <span data-ttu-id="88811-287">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="88811-287">AssemblyCompany</span></span> |
| <span data-ttu-id="88811-288">**$title $**</span><span class="sxs-lookup"><span data-stu-id="88811-288">**$title$**</span></span> | <span data-ttu-id="88811-289">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="88811-289">AssemblyInfo</span></span> | <span data-ttu-id="88811-290">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="88811-290">AssemblyTitle</span></span> |
| <span data-ttu-id="88811-291">**$description $**</span><span class="sxs-lookup"><span data-stu-id="88811-291">**$description$**</span></span> | <span data-ttu-id="88811-292">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="88811-292">AssemblyInfo</span></span> | <span data-ttu-id="88811-293">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="88811-293">AssemblyDescription</span></span> |
| <span data-ttu-id="88811-294">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="88811-294">**$copyright$**</span></span> | <span data-ttu-id="88811-295">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="88811-295">AssemblyInfo</span></span> | <span data-ttu-id="88811-296">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="88811-296">AssemblyCopyright</span></span> |
| <span data-ttu-id="88811-297">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="88811-297">**$configuration$**</span></span> | <span data-ttu-id="88811-298">アセンブリ DLL</span><span class="sxs-lookup"><span data-stu-id="88811-298">Assembly DLL</span></span> | <span data-ttu-id="88811-299">アセンブリのビルドに使われる構成。既定値は Debug。</span><span class="sxs-lookup"><span data-stu-id="88811-299">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="88811-300">Release 構成を使ってパッケージを作成するには、常にコマンド ラインで `-properties Configuration=Release` を使うことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="88811-300">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="88811-301">[アセンブリ ファイル](#including-assembly-files)および[コンテンツ ファイル](#including-content-files)を含めるときは、トークンを使ってパスを解決することもできます。</span><span class="sxs-lookup"><span data-stu-id="88811-301">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="88811-302">トークンの名前は MSBuild のプロパティと同じであり、現在のビルド構成に基づいて含めるファイルを選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="88811-302">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="88811-303">たとえば、`.nuspec` ファイルで次のトークンを使うものとします。</span><span class="sxs-lookup"><span data-stu-id="88811-303">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="88811-304">そして、MSBuild で `AssemblyName` が `LoggingLibrary` であるアセンブリを `Release` 構成でビルドすると、パッケージ内の `.nuspec` ファイルの行は結果として次のようになります。</span><span class="sxs-lookup"><span data-stu-id="88811-304">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="88811-305">Dependencies 要素</span><span class="sxs-lookup"><span data-stu-id="88811-305">Dependencies element</span></span>

<span data-ttu-id="88811-306">`<metadata>` 内の `<dependencies>` 要素は、最上位のパッケージが依存している他のパッケージを示す `<dependency>` 要素をいくつでも含むことができます。</span><span class="sxs-lookup"><span data-stu-id="88811-306">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="88811-307">各 `<dependency>` の属性は次にとおりです。</span><span class="sxs-lookup"><span data-stu-id="88811-307">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="88811-308">属性</span><span class="sxs-lookup"><span data-stu-id="88811-308">Attribute</span></span> | <span data-ttu-id="88811-309">説明</span><span class="sxs-lookup"><span data-stu-id="88811-309">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="88811-310">(必須) "EntityFramework" や "NUnit" などの依存関係のパッケージ ID。これはパッケージ ページに表示されるパッケージ nuget.org の名前となります。</span><span class="sxs-lookup"><span data-stu-id="88811-310">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="88811-311">(必須) 依存関係として許容されるバージョンの範囲。</span><span class="sxs-lookup"><span data-stu-id="88811-311">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="88811-312">厳密な構文については、「[Package versioning](../concepts/package-versioning.md#version-ranges)」(パッケージのバージョン管理) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-312">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="88811-313">フローティングバージョンはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="88811-313">Floating versions are not supported.</span></span> |
| <span data-ttu-id="88811-314">include</span><span class="sxs-lookup"><span data-stu-id="88811-314">include</span></span> | <span data-ttu-id="88811-315">最終的なパッケージに含める依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="88811-315">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="88811-316">既定値は `all` です。</span><span class="sxs-lookup"><span data-stu-id="88811-316">The default value is `all`.</span></span> |
| <span data-ttu-id="88811-317">除外</span><span class="sxs-lookup"><span data-stu-id="88811-317">exclude</span></span> | <span data-ttu-id="88811-318">最終的なパッケージから除外する依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。</span><span class="sxs-lookup"><span data-stu-id="88811-318">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="88811-319">既定値は、 `build,analyzers` 上書きすることができます。</span><span class="sxs-lookup"><span data-stu-id="88811-319">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="88811-320">`content/ ContentFiles`また、最終的なパッケージでは、上書きすることはできません。</span><span class="sxs-lookup"><span data-stu-id="88811-320">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="88811-321">`exclude` で指定されているタグの方が、`include` で指定されているタグより優先されます。</span><span class="sxs-lookup"><span data-stu-id="88811-321">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="88811-322">たとえば、`include="runtime, compile" exclude="compile"` は `include="runtime"` と同じです。</span><span class="sxs-lookup"><span data-stu-id="88811-322">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="88811-323">パッケージを nuget.org にアップロードする場合、各依存関係の `id` 属性は128文字に制限され、 `version` 属性は256文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="88811-323">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="88811-324">包含/除外タグ</span><span class="sxs-lookup"><span data-stu-id="88811-324">Include/Exclude tag</span></span> | <span data-ttu-id="88811-325">ターゲットの影響を受けるフォルダー</span><span class="sxs-lookup"><span data-stu-id="88811-325">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="88811-326">contentFiles</span><span class="sxs-lookup"><span data-stu-id="88811-326">contentFiles</span></span> | <span data-ttu-id="88811-327">Content</span><span class="sxs-lookup"><span data-stu-id="88811-327">Content</span></span> |
| <span data-ttu-id="88811-328">ランタイム</span><span class="sxs-lookup"><span data-stu-id="88811-328">runtime</span></span> | <span data-ttu-id="88811-329">Runtime、Resources、FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="88811-329">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="88811-330">compile</span><span class="sxs-lookup"><span data-stu-id="88811-330">compile</span></span> | <span data-ttu-id="88811-331">lib</span><span class="sxs-lookup"><span data-stu-id="88811-331">lib</span></span> |
| <span data-ttu-id="88811-332">build</span><span class="sxs-lookup"><span data-stu-id="88811-332">build</span></span> | <span data-ttu-id="88811-333">build (MSBuild のプロパティとターゲット)</span><span class="sxs-lookup"><span data-stu-id="88811-333">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="88811-334">native</span><span class="sxs-lookup"><span data-stu-id="88811-334">native</span></span> | <span data-ttu-id="88811-335">native</span><span class="sxs-lookup"><span data-stu-id="88811-335">native</span></span> |
| <span data-ttu-id="88811-336">なし</span><span class="sxs-lookup"><span data-stu-id="88811-336">none</span></span> | <span data-ttu-id="88811-337">フォルダーなし</span><span class="sxs-lookup"><span data-stu-id="88811-337">No folders</span></span> |
| <span data-ttu-id="88811-338">all</span><span class="sxs-lookup"><span data-stu-id="88811-338">all</span></span> | <span data-ttu-id="88811-339">すべてのフォルダー</span><span class="sxs-lookup"><span data-stu-id="88811-339">All folders</span></span> |

<span data-ttu-id="88811-340">たとえば、次の行は `PackageA` バージョン 1.1.0 以降および `PackageB` バージョン 1.x での依存関係を示します。</span><span class="sxs-lookup"><span data-stu-id="88811-340">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="88811-341">次の行も同じパッケージでの依存関係を示しますが、`PackageA` の `contentFiles` および `build` フォルダーを含めて、`PackageB` の `native` および `compile` フォルダーを除くすべてを含めることを指定します。</span><span class="sxs-lookup"><span data-stu-id="88811-341">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="88811-342">`.nuspec`を使用してプロジェクトからを作成する場合 `nuget spec` 、そのプロジェクトに存在する依存関係は、結果のファイルに自動的に含まれません `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="88811-342">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="88811-343">代わりに `nuget pack myproject.csproj` 、を使用し、生成された *nupkg* ファイル内から *nuspec* ファイルを取得します。</span><span class="sxs-lookup"><span data-stu-id="88811-343">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="88811-344">この *nuspec* には、依存関係が含まれています。</span><span class="sxs-lookup"><span data-stu-id="88811-344">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="88811-345">依存関係グループ</span><span class="sxs-lookup"><span data-stu-id="88811-345">Dependency groups</span></span>

<span data-ttu-id="88811-346">*バージョン2.0 以降*</span><span class="sxs-lookup"><span data-stu-id="88811-346">*Version 2.0+*</span></span>

<span data-ttu-id="88811-347">1 つのフラット リストの代わりに、`<dependencies>` の `<group>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って依存関係を指定できます。</span><span class="sxs-lookup"><span data-stu-id="88811-347">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="88811-348">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<dependency>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="88811-348">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="88811-349">ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの依存関係が一緒にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="88811-349">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="88811-350">依存関係の既定のリストまたはフォールバック リストとしては、`targetFramework` 属性のない `<group>` 要素が使われます。</span><span class="sxs-lookup"><span data-stu-id="88811-350">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="88811-351">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-351">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="88811-352">グループの形式をフラット リストと併用することはできません。</span><span class="sxs-lookup"><span data-stu-id="88811-352">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="88811-353">フォルダーで使用される [ターゲットフレームワークモニカー (tfm)](../reference/target-frameworks.md) の形式 `lib/ref` は、で使用される tfm と比較して異なり `dependency groups` ます。</span><span class="sxs-lookup"><span data-stu-id="88811-353">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="88811-354">で宣言されたターゲットフレームワーク `dependencies group` とファイルのフォルダーが完全に一致しない場合、 `lib/ref` `.nuspec` `pack` コマンドによって [NuGet 警告 NU5128](../reference/errors-and-warnings/nu5128.md)が生成されます。</span><span class="sxs-lookup"><span data-stu-id="88811-354">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="88811-355">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="88811-355">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="88811-356">明示的なアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="88811-356">Explicit assembly references</span></span>

<span data-ttu-id="88811-357">要素は、 `<references>` を使用してプロジェクトがパッケージを使用するときに、 `packages.config` ターゲットプロジェクトが参照するアセンブリを明示的に指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="88811-357">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="88811-358">明示的な参照は、通常、設計時のみのアセンブリに使われます。</span><span class="sxs-lookup"><span data-stu-id="88811-358">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="88811-359">詳細については、「 [プロジェクトによって参照されるアセンブリの選択](../create-packages/select-assemblies-referenced-by-projects.md) 」のページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="88811-359">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="88811-360">たとえば、次の `<references>` 要素は、パッケージに他のアセンブリがある場合でも、`xunit.dll` と `xunit.extensions.dll` に対する参照だけを追加するよう NuGet に指示します。</span><span class="sxs-lookup"><span data-stu-id="88811-360">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="88811-361">[参照グループ]</span><span class="sxs-lookup"><span data-stu-id="88811-361">Reference groups</span></span>

<span data-ttu-id="88811-362">1 つのフラット リストの代わりに、`<references>` の `<group>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って参照を指定できます。</span><span class="sxs-lookup"><span data-stu-id="88811-362">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="88811-363">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<reference>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="88811-363">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="88811-364">ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの参照はプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="88811-364">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="88811-365">参照の既定のリストまたはフォールバック リストとしては、`targetFramework` 属性のない `<group>` 要素が使われます。</span><span class="sxs-lookup"><span data-stu-id="88811-365">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="88811-366">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-366">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="88811-367">グループの形式をフラット リストと併用することはできません。</span><span class="sxs-lookup"><span data-stu-id="88811-367">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="88811-368">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="88811-368">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="88811-369">フレームワーク アセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="88811-369">Framework assembly references</span></span>

<span data-ttu-id="88811-370">フレームワーク アセンブリは、.NET Framework の一部であり、指定されたコンピューターのグローバル アセンブリ キャッシュ (GAC) に既に存在している必要があります。</span><span class="sxs-lookup"><span data-stu-id="88811-370">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="88811-371">`<frameworkAssemblies>` 要素でこれらのアセンブリを指定することにより、プロジェクトに必要な参照がまだない場合であっても、そのような参照をプロジェクトに確実に追加できます。</span><span class="sxs-lookup"><span data-stu-id="88811-371">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="88811-372">もちろん、そのようなアセンブリがパッケージに直接含まれることはありません。</span><span class="sxs-lookup"><span data-stu-id="88811-372">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="88811-373">`<frameworkAssemblies>` 要素には 0 個以上の `<frameworkAssembly>` 要素を含めることができ、それぞれで次の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="88811-373">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="88811-374">属性</span><span class="sxs-lookup"><span data-stu-id="88811-374">Attribute</span></span> | <span data-ttu-id="88811-375">説明</span><span class="sxs-lookup"><span data-stu-id="88811-375">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88811-376">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="88811-376">**assemblyName**</span></span> | <span data-ttu-id="88811-377">(必須) 完全修飾アセンブリ名。</span><span class="sxs-lookup"><span data-stu-id="88811-377">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="88811-378">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="88811-378">**targetFramework**</span></span> | <span data-ttu-id="88811-379">(省略可能) この参照を適用するターゲット フレームワークを指定します。</span><span class="sxs-lookup"><span data-stu-id="88811-379">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="88811-380">省略した場合は、参照がすべてのフレームワークに適用されることを示します。</span><span class="sxs-lookup"><span data-stu-id="88811-380">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="88811-381">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-381">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="88811-382">次の例は、`System.Net` への参照はすべてのターゲット フレームワークに適用され、`System.ServiceModel` への参照は .NET Framework 4.0 のみに適用されることを示します。</span><span class="sxs-lookup"><span data-stu-id="88811-382">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="88811-383">アセンブリ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="88811-383">Including assembly files</span></span>

<span data-ttu-id="88811-384">「[パッケージを作成する](../create-packages/creating-a-package.md)」で説明されている規則に従う場合、`.nuspec` ファイルでファイルの一覧を明示的に指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="88811-384">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="88811-385">`nuget pack` コマンドが必要なファイルを自動的に選びます。</span><span class="sxs-lookup"><span data-stu-id="88811-385">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="88811-386">プロジェクトにパッケージをインストールするとき、NuGet はパッケージの DLL にアセンブリ参照を自動的に追加します。ただし、指定されている `.resources.dll` は、ローカライズされたサテライト アセンブリであると見なされるため "*除外*" されます。</span><span class="sxs-lookup"><span data-stu-id="88811-386">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="88811-387">そのため、避けなければ不可欠なパッケージ コードが含まれてしまうファイルには `.resources.dll` を使わないようにします。</span><span class="sxs-lookup"><span data-stu-id="88811-387">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="88811-388">この自動動作をバイパスして、パッケージに含めるファイルを明示的に制御するには、`<files>` 要素を `<package>` の子要素 (および `<metadata>` の兄弟要素) として配置し、各ファイルを個別の `<file>` 要素で示します。</span><span class="sxs-lookup"><span data-stu-id="88811-388">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="88811-389">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="88811-389">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="88811-390">NuGet 2.x 以前および `packages.config` を使っているプロジェクトでは、`<files>` 要素はパッケージのインストール時に変更できないコンテンツ ファイルを含めるためにも使われます。</span><span class="sxs-lookup"><span data-stu-id="88811-390">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="88811-391">NuGet 3.3 以降で、PackageReference を使用しているプロジェクトでは、代わりに `<contentFiles>` 要素が使用されます。</span><span class="sxs-lookup"><span data-stu-id="88811-391">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="88811-392">詳しくは、後の「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-392">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="88811-393">File 要素の属性</span><span class="sxs-lookup"><span data-stu-id="88811-393">File element attributes</span></span>

<span data-ttu-id="88811-394">各 `<file>` 要素では、次の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="88811-394">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="88811-395">属性</span><span class="sxs-lookup"><span data-stu-id="88811-395">Attribute</span></span> | <span data-ttu-id="88811-396">説明</span><span class="sxs-lookup"><span data-stu-id="88811-396">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88811-397">**src**</span><span class="sxs-lookup"><span data-stu-id="88811-397">**src**</span></span> | <span data-ttu-id="88811-398">含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。</span><span class="sxs-lookup"><span data-stu-id="88811-398">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="88811-399">絶対パスを指定しない限り、パスは `.nuspec` ファイルが基準になります。</span><span class="sxs-lookup"><span data-stu-id="88811-399">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="88811-400">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="88811-400">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="88811-401">**target**</span><span class="sxs-lookup"><span data-stu-id="88811-401">**target**</span></span> | <span data-ttu-id="88811-402">ソース ファイルが格納されるパッケージ内のフォルダーへの相対パス。`lib`、`content`、`build`、または `tools` で始まっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="88811-402">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="88811-403">[規則に基づく作業ディレクトリからの .nuspec の作成](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="88811-403">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="88811-404">**もの**</span><span class="sxs-lookup"><span data-stu-id="88811-404">**exclude**</span></span> | <span data-ttu-id="88811-405">`src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。</span><span class="sxs-lookup"><span data-stu-id="88811-405">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="88811-406">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="88811-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="88811-407">例</span><span class="sxs-lookup"><span data-stu-id="88811-407">Examples</span></span>

<span data-ttu-id="88811-408">**1 つのアセンブリ**</span><span class="sxs-lookup"><span data-stu-id="88811-408">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="88811-409">**ターゲット フレームワークに固有の 1 つのアセンブリ**</span><span class="sxs-lookup"><span data-stu-id="88811-409">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="88811-410">**ワイルドカードを使った DLL のセット**</span><span class="sxs-lookup"><span data-stu-id="88811-410">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="88811-411">**異なるフレームワークの DLL**</span><span class="sxs-lookup"><span data-stu-id="88811-411">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="88811-412">**ファイルの除外**</span><span class="sxs-lookup"><span data-stu-id="88811-412">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="88811-413">コンテンツ ファイルを含める</span><span class="sxs-lookup"><span data-stu-id="88811-413">Including content files</span></span>

<span data-ttu-id="88811-414">コンテンツ ファイルは、パッケージでプロジェクトに含める必要がある変更できないファイルです。</span><span class="sxs-lookup"><span data-stu-id="88811-414">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="88811-415">変更できないので、それを使うプロジェクトによる変更は意図されていません。</span><span class="sxs-lookup"><span data-stu-id="88811-415">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="88811-416">コンテンツ ファイルの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="88811-416">Example content files include:</span></span>

- <span data-ttu-id="88811-417">リソースとして埋め込まれる画像</span><span class="sxs-lookup"><span data-stu-id="88811-417">Images that are embedded as resources</span></span>
- <span data-ttu-id="88811-418">コンパイル済みのソース ファイル</span><span class="sxs-lookup"><span data-stu-id="88811-418">Source files that are already compiled</span></span>
- <span data-ttu-id="88811-419">プロジェクトのビルド出力と共に含まれる必要があるスクリプト</span><span class="sxs-lookup"><span data-stu-id="88811-419">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="88811-420">プロジェクトに含まれる必要はあるが、プロジェクト固有の変更は必要ない、パッケージの構成ファイル</span><span class="sxs-lookup"><span data-stu-id="88811-420">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="88811-421">コンテンツ ファイルをパッケージに含めるには、`<files>` 要素を使い、`target` 属性で `content` フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="88811-421">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="88811-422">ただし、PackageReference を使用しているプロジェクトにパッケージをインストールする場合、このようなファイルは無視され、代わりに `<contentFiles>` 要素が使用されます。</span><span class="sxs-lookup"><span data-stu-id="88811-422">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="88811-423">使用する側のプロジェクトとの最大限の互換性のため、パッケージでは両方の要素でコンテンツ ファイルを指定するのが理想的です。</span><span class="sxs-lookup"><span data-stu-id="88811-423">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="88811-424">コンテンツ ファイルに対する files 要素の使用</span><span class="sxs-lookup"><span data-stu-id="88811-424">Using the files element for content files</span></span>

<span data-ttu-id="88811-425">コンテンツ ファイルでは、アセンブリ ファイルの場合と同じ形式を使用しますが、次の例のように、`target` 属性で基本フォルダーとして `content` を指定します。</span><span class="sxs-lookup"><span data-stu-id="88811-425">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="88811-426">**基本的なコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="88811-426">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="88811-427">**ディレクトリ構造を持つコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="88811-427">**Content files with directory structure**</span></span>

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

<span data-ttu-id="88811-428">**ターゲット フレームワークに固有のコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="88811-428">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="88811-429">**名前のドットでフォルダーにコピーされるコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="88811-429">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="88811-430">この場合、NuGet は `target` の拡張子が `src` の拡張子と一致しないものと判断し、`target` での名前のその部分をフォルダーとして扱います。</span><span class="sxs-lookup"><span data-stu-id="88811-430">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="88811-431">**拡張子のないコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="88811-431">**Content files without extensions**</span></span>

<span data-ttu-id="88811-432">拡張子のないファイルを含めるには、ワイルドカード `*` または `**` を使います。</span><span class="sxs-lookup"><span data-stu-id="88811-432">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="88811-433">**深いパスと深いターゲットのコンテンツ ファイル**</span><span class="sxs-lookup"><span data-stu-id="88811-433">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="88811-434">この場合、ソースとターゲットのファイル拡張子が一致するので、NuGet はターゲットがフォルダーではなくファイル名であると想定します。</span><span class="sxs-lookup"><span data-stu-id="88811-434">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="88811-435">**パッケージ内のコンテンツ ファイルの名前の変更**</span><span class="sxs-lookup"><span data-stu-id="88811-435">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="88811-436">**ファイルの除外**</span><span class="sxs-lookup"><span data-stu-id="88811-436">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="88811-437">コンテンツ ファイルに対する contentFiles 要素の使用</span><span class="sxs-lookup"><span data-stu-id="88811-437">Using the contentFiles element for content files</span></span>

<span data-ttu-id="88811-438">*NuGet 4.0 以降で、PackageReference を使用している場合*</span><span class="sxs-lookup"><span data-stu-id="88811-438">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="88811-439">既定では、パッケージはコンテンツを `contentFiles` フォルダーに配置し (下記参照)、`nuget pack` は既定の属性を使ってそのフォルダーにすべてのファイルを格納します。</span><span class="sxs-lookup"><span data-stu-id="88811-439">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="88811-440">この場合は、`contentFiles` ノードを `.nuspec` に含める必要はまったくありません。</span><span class="sxs-lookup"><span data-stu-id="88811-440">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="88811-441">含まれるファイルを制御するには、含めるファイルを厳密に示す `<files>` 要素のコレクションである `<contentFiles>` 要素を指定します。</span><span class="sxs-lookup"><span data-stu-id="88811-441">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="88811-442">これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。</span><span class="sxs-lookup"><span data-stu-id="88811-442">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="88811-443">属性</span><span class="sxs-lookup"><span data-stu-id="88811-443">Attribute</span></span> | <span data-ttu-id="88811-444">説明</span><span class="sxs-lookup"><span data-stu-id="88811-444">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88811-445">**用意**</span><span class="sxs-lookup"><span data-stu-id="88811-445">**include**</span></span> | <span data-ttu-id="88811-446">(必須) 含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。</span><span class="sxs-lookup"><span data-stu-id="88811-446">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="88811-447">`contentFiles`絶対パスが指定されていない場合は、フォルダーに対する相対パスになります。</span><span class="sxs-lookup"><span data-stu-id="88811-447">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="88811-448">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="88811-448">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="88811-449">**もの**</span><span class="sxs-lookup"><span data-stu-id="88811-449">**exclude**</span></span> | <span data-ttu-id="88811-450">`src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。</span><span class="sxs-lookup"><span data-stu-id="88811-450">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="88811-451">ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。</span><span class="sxs-lookup"><span data-stu-id="88811-451">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="88811-452">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="88811-452">**buildAction**</span></span> | <span data-ttu-id="88811-453">MSBuild のコンテンツ項目に割り当てるビルドアクション (、、、など) `Content` `None` `Embedded Resource` `Compile` 。既定値は `Compile` です。</span><span class="sxs-lookup"><span data-stu-id="88811-453">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="88811-454">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="88811-454">**copyToOutput**</span></span> | <span data-ttu-id="88811-455">コンテンツ項目をビルド (または発行) 出力フォルダーにコピーするかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="88811-455">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="88811-456">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="88811-456">The default is false.</span></span> |
| <span data-ttu-id="88811-457">**flatten**</span><span class="sxs-lookup"><span data-stu-id="88811-457">**flatten**</span></span> | <span data-ttu-id="88811-458">コンテンツ項目をビルド出力の単一フォルダーにコピーするか (true)、それともパッケージのフォルダー構造を保持するか (false) を示すブール値。</span><span class="sxs-lookup"><span data-stu-id="88811-458">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="88811-459">このフラグは、copyToOutput が true に設定されている場合のみ機能します。</span><span class="sxs-lookup"><span data-stu-id="88811-459">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="88811-460">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="88811-460">The default is false.</span></span> |

<span data-ttu-id="88811-461">パッケージをインストールするとき、NuGet は `<contentFiles>` の子要素を上から下に順番に適用します。</span><span class="sxs-lookup"><span data-stu-id="88811-461">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="88811-462">複数のエントリが同じファイルに一致する場合は、すべてのエントリが適用されます。</span><span class="sxs-lookup"><span data-stu-id="88811-462">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="88811-463">同じ属性に対して競合がある場合は、最上位のエントリが下位のエントリをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="88811-463">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="88811-464">パッケージ フォルダーの構造</span><span class="sxs-lookup"><span data-stu-id="88811-464">Package folder structure</span></span>

<span data-ttu-id="88811-465">パッケージ プロジェクトでは、次のパターンを使ってコンテンツを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="88811-465">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="88811-466">`codeLanguages` には、`cs`、`vb`、`fs`、`any`、または指定された `$(ProjectLanguage)` に相当する小文字表現を指定できます。</span><span class="sxs-lookup"><span data-stu-id="88811-466">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="88811-467">`TxM` は、NuGet がサポートする任意の有効なターゲット フレームワーク モニカーです (「[ターゲット フレームワーク](../reference/target-frameworks.md)」を参照)。</span><span class="sxs-lookup"><span data-stu-id="88811-467">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="88811-468">この構文の末尾に、任意のフォルダー構造を追加できます。</span><span class="sxs-lookup"><span data-stu-id="88811-468">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="88811-469">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="88811-469">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="88811-470">空のフォルダーでは、`.` を使って、言語と TxM の特定の組み合わせにコンテンツを提供しないようにすることができます。次はその例です。</span><span class="sxs-lookup"><span data-stu-id="88811-470">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="88811-471">contentFiles セクションの例</span><span class="sxs-lookup"><span data-stu-id="88811-471">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="88811-472">フレームワーク参照グループ</span><span class="sxs-lookup"><span data-stu-id="88811-472">Framework reference groups</span></span>

<span data-ttu-id="88811-473">*バージョン 5.1 + 追加 PackageReference のみ*</span><span class="sxs-lookup"><span data-stu-id="88811-473">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="88811-474">フレームワーク参照は、WPF や Windows フォームなどの共有フレームワークを表す .NET Core の概念です。</span><span class="sxs-lookup"><span data-stu-id="88811-474">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="88811-475">共有フレームワークを指定することで、パッケージによって、すべてのフレームワークの依存関係が参照元のプロジェクトに含まれるようになります。</span><span class="sxs-lookup"><span data-stu-id="88811-475">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="88811-476">各要素には、1つ `<group>` の `targetFramework` 属性と0個以上の要素が必要 `<frameworkReference>` です。</span><span class="sxs-lookup"><span data-stu-id="88811-476">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="88811-477">次の例は、.NET Core WPF プロジェクト用に生成された nuspec を示しています。</span><span class="sxs-lookup"><span data-stu-id="88811-477">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="88811-478">フレームワーク参照を含む手動作成 nuspecs は推奨されません。</span><span class="sxs-lookup"><span data-stu-id="88811-478">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="88811-479">代わりに、 [ターゲット](msbuild-targets.md) パックを使用することを検討してください。これにより、プロジェクトからそれらが自動的に推論されます。</span><span class="sxs-lookup"><span data-stu-id="88811-479">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="88811-480">Nuspec ファイルの例</span><span class="sxs-lookup"><span data-stu-id="88811-480">Example nuspec files</span></span>

<span data-ttu-id="88811-481">**依存関係またはファイルを指定しない単純な `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="88811-481">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="88811-482">**依存関係を含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="88811-482">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="88811-483">**ファイルを含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="88811-483">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="88811-484">**フレームワーク アセンブリを含む `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="88811-484">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="88811-485">この例では、指定したプロジェクト ターゲットに次のものがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="88811-485">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="88811-486">.NET4 -> `System.Web`、`System.Net`</span><span class="sxs-lookup"><span data-stu-id="88811-486">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="88811-487">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="88811-487">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="88811-488">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="88811-488">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="88811-489">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="88811-489">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
