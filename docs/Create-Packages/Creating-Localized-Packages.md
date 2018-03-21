---
title: "ローカライズされた NuGet パッケージの作成方法 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "すべてのアセンブリを 1 つのパッケージに含めるか個別のアセンブリを公開することによって、ローカライズされた NuGet パッケージを作成する 2 つの方法の詳細について説明します。"
keywords: "NuGet パッケージのローカライズ、NuGet のサテライト アセンブリ、ローカライズされたパッケージの作成、NuGet ローカリゼーション規則"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5946ba6b43d3c418a1624aeb27d12b385d66b2fb
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2018
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="8958e-104">ローカライズされた NuGet パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="8958e-104">Creating localized NuGet packages</span></span>

<span data-ttu-id="8958e-105">ライブラリのローカライズされたバージョンを作成する方法は 2 つあります。</span><span class="sxs-lookup"><span data-stu-id="8958e-105">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="8958e-106">1 つのパッケージにローカライズされたすべてのリソース アセンブリを含めます。</span><span class="sxs-lookup"><span data-stu-id="8958e-106">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="8958e-107">厳密な一連の規則に従って、個別のローカライズされたサテライト パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="8958e-107">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="8958e-108">どちらの方法にも、次のセクションで説明するようなメリットとデメリットがあります。</span><span class="sxs-lookup"><span data-stu-id="8958e-108">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="8958e-109">1 つのパッケージにローカライズされたすべてのリソース アセンブリを含める</span><span class="sxs-lookup"><span data-stu-id="8958e-109">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="8958e-110">ローカライズされたリソース アセンブリを 1 つのパッケージに含めるのが、通常、最も簡単なアプローチです。</span><span class="sxs-lookup"><span data-stu-id="8958e-110">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="8958e-111">これを行うには、パッケージの既定 (en-us と見なされます) 以外のサポートされる言語の `lib` 内にフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="8958e-111">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="8958e-112">これらのフォルダーには、リソース アセンブリおよびローカライズされた IntelliSense XML ファイルを配置できます。</span><span class="sxs-lookup"><span data-stu-id="8958e-112">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="8958e-113">たとえば、次のフォルダー構造は、ドイツ語 (de)、イタリア語 (it)、日本語 (ja)、ロシア語 (ru)、簡体字中国語 (zh-Hans)、および繁体字中国語 (zh-Hant) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="8958e-113">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="8958e-114">すべての言語は `net40` ターゲット フレームワーク フォルダーの下に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="8958e-114">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="8958e-115">[複数のフレームワークをサポートする](../create-packages/supporting-multiple-target-frameworks.md)場合、`lib` の下に各バリアントのフォルダーがあります。</span><span class="sxs-lookup"><span data-stu-id="8958e-115">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="8958e-116">これらのフォルダーを配置して、`.nuspec` 内ですべてのファイルを参照します。</span><span class="sxs-lookup"><span data-stu-id="8958e-116">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="8958e-117">この手法を使用しする 1 つのサンプル パッケージは [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0) です。</span><span class="sxs-lookup"><span data-stu-id="8958e-117">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="8958e-118">メリットとデメリット (ローカライズされたリソース アセンブリ)</span><span class="sxs-lookup"><span data-stu-id="8958e-118">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="8958e-119">1 つのパッケージにすべての言語をビルドすることには、次のようないくつかのデメリットがあります。</span><span class="sxs-lookup"><span data-stu-id="8958e-119">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="8958e-120">**共有メタデータ**: NuGet パッケージは、1 つの `.nuspec` ファイルのみを含めることができるので、1 つの言語のメタデータだけを提供できます。</span><span class="sxs-lookup"><span data-stu-id="8958e-120">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="8958e-121">つまり、NuGet は、ローカライズされたメタデータのサポートを提供しません。</span><span class="sxs-lookup"><span data-stu-id="8958e-121">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="8958e-122">**パッケージのサイズ**: サポートする言語の数によっては、ライブラリがかなり大きくなる可能性があり、パッケージのインストールと復元の速度が低下します。</span><span class="sxs-lookup"><span data-stu-id="8958e-122">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="8958e-123">**同時リリース**: 1 つのパッケージ内にローカライズされたファイルをバンドルするには、そのパッケージ内ですべての資産を同時にリリースする必要があり、個別に各ローカライズをリリースすることはできません。</span><span class="sxs-lookup"><span data-stu-id="8958e-123">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="8958e-124">さらに、1 つのローカライズに何らかの更新があった場合には、パッケージ全体の新しいバージョンが必要です。</span><span class="sxs-lookup"><span data-stu-id="8958e-124">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="8958e-125">ただし、いくつかのメリットもあります。</span><span class="sxs-lookup"><span data-stu-id="8958e-125">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="8958e-126">**シンプル**: パッケージのコンシューマーは、1 つのインストールでサポートされているすべての言語を取得し、各言語を個別にインストールする必要がありません。</span><span class="sxs-lookup"><span data-stu-id="8958e-126">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="8958e-127">1 つのパッケージは、nuget.org で見つけやすくもなります。</span><span class="sxs-lookup"><span data-stu-id="8958e-127">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="8958e-128">**組み合わせたバージョン**: すべてのリソース アセンブリが、プライマリ アセンブリと同じパッケージ内にあるので、それらのすべてが同じバージョン番号を共有し、誤って切り離されるリスクがなくなります。</span><span class="sxs-lookup"><span data-stu-id="8958e-128">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="8958e-129">ローカライズされたサテライト パッケージ</span><span class="sxs-lookup"><span data-stu-id="8958e-129">Localized satellite packages</span></span>

<span data-ttu-id="8958e-130">.NET Framework でのサテライト アセンブリのサポート方法と同様に、この方法では、ローカライズされたリソースと IntelliSense XML ファイルをサテライト パッケージに分割します。</span><span class="sxs-lookup"><span data-stu-id="8958e-130">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="8958e-131">これを行うには、プライマリ パッケージで、名前付け規則 `{identifier}.{version}.nupkg` を使用し、既定の言語 (en-US など) などのアセンブリを含めます。</span><span class="sxs-lookup"><span data-stu-id="8958e-131">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="8958e-132">たとえば、`ContosoUtilities.1.0.0.nupkg` には、次の構造が含まれます。</span><span class="sxs-lookup"><span data-stu-id="8958e-132">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="8958e-133">サテライト アセンブリは、`ContosoUtilities.de.1.0.0.nupkg` などのように名前付け規則 `{identifier}.{language}.{version}.nupkg`を使用します。</span><span class="sxs-lookup"><span data-stu-id="8958e-133">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="8958e-134">識別子は、プライマリ パッケージと完全に一致している**必要があります**。</span><span class="sxs-lookup"><span data-stu-id="8958e-134">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="8958e-135">これは、個別のパッケージに独自の `.nuspec` ファイルがあり、それがローカライズされたメタデータを含んでいるためです。</span><span class="sxs-lookup"><span data-stu-id="8958e-135">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="8958e-136">`.nuspec` の言語は、ファイル名で使用されるものと一致している**必要があります**。</span><span class="sxs-lookup"><span data-stu-id="8958e-136">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="8958e-137">サテライト アセンブリは、[] バージョン表記を使用して (「[Package versioning](../reference/package-versioning.md)」(パッケージのバージョン管理) を参照してください)、プライマリ パッケージの正確なバージョンを宣言する**必要もあります**。</span><span class="sxs-lookup"><span data-stu-id="8958e-137">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="8958e-138">たとえば、`ContosoUtilities.de.1.0.0.nupkg` は、`[1.0.0]` 表記を使用して `ContosoUtilities.1.0.0.nupkg` で依存関係を宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8958e-138">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="8958e-139">サテライト パッケージでは、当然ながら、プライマリ パッケージと別のバージョン番号を付けることができます。</span><span class="sxs-lookup"><span data-stu-id="8958e-139">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="8958e-140">サテライト パッケージの構造で、パッケージ ファイル名の `{language}` と一致するサブフォルダーにリソース アセンブリと XML IntelliSense ファイルを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="8958e-140">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="8958e-141">**注**: `ja-JP` などの特定のサブカルチャが必要な場合を除いて、`ja` のような高レベルの言語識別子を常に使用してください。</span><span class="sxs-lookup"><span data-stu-id="8958e-141">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="8958e-142">サテライト アセンブリで、NuGet は、ファイル名の `{language}` と一致するフォルダー内のファイル**のみ**を認識します。</span><span class="sxs-lookup"><span data-stu-id="8958e-142">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="8958e-143">他の属性はすべて無視されます。</span><span class="sxs-lookup"><span data-stu-id="8958e-143">All others are ignored.</span></span>

<span data-ttu-id="8958e-144">これらのすべての規則が満たされたら、NuGet は、サテライト パッケージとしてパッケージを認識し、プライマリ パッケージの `lib` フォルダーにローカライズされたファイルをインストールします。それらがもともとバンドルされている場合と同様です。</span><span class="sxs-lookup"><span data-stu-id="8958e-144">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="8958e-145">サテライト パッケージをアンインストールすると、その同じフォルダーからそのファイルが削除されます。</span><span class="sxs-lookup"><span data-stu-id="8958e-145">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="8958e-146">サポートされている言語ごとに同じ方法で、追加のサテライト アセンブリを作成します。</span><span class="sxs-lookup"><span data-stu-id="8958e-146">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="8958e-147">例については、ASP.NET MVC のパッケージのセットを確認してください。</span><span class="sxs-lookup"><span data-stu-id="8958e-147">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="8958e-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (英語のプライマリ)</span><span class="sxs-lookup"><span data-stu-id="8958e-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="8958e-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (ドイツ語)</span><span class="sxs-lookup"><span data-stu-id="8958e-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="8958e-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (日本語)</span><span class="sxs-lookup"><span data-stu-id="8958e-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="8958e-151">[Microsoft.AspNet.Mvc.zh Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (簡体字中国語)</span><span class="sxs-lookup"><span data-stu-id="8958e-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="8958e-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (繁体字中国語)</span><span class="sxs-lookup"><span data-stu-id="8958e-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="8958e-153">必要な規則の概要</span><span class="sxs-lookup"><span data-stu-id="8958e-153">Summary of required conventions</span></span>

- <span data-ttu-id="8958e-154">プライマリ パッケージの名前を指定する必要があります。`{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="8958e-154">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="8958e-155">サテライト パッケージの名前を指定する必要があります。`{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="8958e-155">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="8958e-156">サテライト パッケージの `.nuspec` でファイル名に一致する言語を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8958e-156">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="8958e-157">サテライト パッケージは、`.nuspec` ファイルで [] 表記を使用して、プライマリの正確なバージョンで依存関係を宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8958e-157">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="8958e-158">範囲はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="8958e-158">Ranges are not supported.</span></span>
- <span data-ttu-id="8958e-159">サテライト パッケージは、ファイルの `{language}` と正確に一致する `lib\[{framework}\]{language}` フォルダー内にファイルを配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8958e-159">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="8958e-160">メリットとデメリット (サテライトのパッケージ)</span><span class="sxs-lookup"><span data-stu-id="8958e-160">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="8958e-161">サテライトのパッケージを使用すると、いくつかのメリットがあります。</span><span class="sxs-lookup"><span data-stu-id="8958e-161">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="8958e-162">**パッケージのサイズ**: プライマリ パッケージの全体的な大きさが最小限に抑えられ、コンシューマーには、使用する各言語のコストのみが発生します。</span><span class="sxs-lookup"><span data-stu-id="8958e-162">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="8958e-163">**個別のメタデータ**: 各サテライト パッケージには、専用の `.nuspec` ファイルがあり、そのため、専用のローカライズされたメタデータがあります。</span><span class="sxs-lookup"><span data-stu-id="8958e-163">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="8958e-164">これにより、一部のコンシューマーが、ローカライズされた用語で nuget.org を検索することで、より簡単にパッケージを検索できます。</span><span class="sxs-lookup"><span data-stu-id="8958e-164">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="8958e-165">**切り離されたリリース**: サテライト アセンブリは、すべて一度にではなく時間の経過と共にリリースできるので、ローカライズ作業を分散することができます。</span><span class="sxs-lookup"><span data-stu-id="8958e-165">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="8958e-166">ただし、サテライト パッケージには、次の固有の一連のデメリットがあります。</span><span class="sxs-lookup"><span data-stu-id="8958e-166">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="8958e-167">**煩雑さ**: 1 つのパッケージの代わりに、多くのパッケージがあるので、nuget.org で検索結果が煩雑になり、Visual Studio プロジェクト内で参照の一覧が長くなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8958e-167">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="8958e-168">**厳密な規則**。</span><span class="sxs-lookup"><span data-stu-id="8958e-168">**Strict conventions**.</span></span> <span data-ttu-id="8958e-169">サテライト パッケージは、規則に厳密に従う必要があります。そうしないと、ローカライズされたバージョンは正しく取得されません。</span><span class="sxs-lookup"><span data-stu-id="8958e-169">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="8958e-170">**バージョン管理**: 各サテライト パッケージは、プライマリ パッケージと正確なバージョンの依存関係を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="8958e-170">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="8958e-171">つまり、プライマリ パッケージを更新した場合、リソースを変更しない場合でもすべてのサテライト パッケージも更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8958e-171">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
