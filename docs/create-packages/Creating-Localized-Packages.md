---
title: ローカライズされた NuGet パッケージの作成方法
description: すべてのアセンブリを 1 つのパッケージに含めるか個別のアセンブリを公開することによって、ローカライズされた NuGet パッケージを作成する 2 つの方法の詳細について説明します。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 83414a824676844f9e44eab874e5eac788d50583
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610936"
---
# <a name="creating-localized-nuget-packages"></a>ローカライズされた NuGet パッケージを作成する

ライブラリのローカライズされたバージョンを作成する方法は 2 つあります。

1. 1 つのパッケージにローカライズされたすべてのリソース アセンブリを含めます。
1. 厳密な一連の規則に従って、個別のローカライズされたサテライト パッケージを作成します。

どちらの方法にも、次のセクションで説明するようなメリットとデメリットがあります。

## <a name="localized-resource-assemblies-in-a-single-package"></a>1 つのパッケージにローカライズされたすべてのリソース アセンブリを含める

ローカライズされたリソース アセンブリを 1 つのパッケージに含めるのが、通常、最も簡単なアプローチです。 これを行うには、パッケージの既定 (en-us と見なされます) 以外のサポートされる言語の `lib` 内にフォルダーを作成します。 これらのフォルダーには、リソース アセンブリおよびローカライズされた IntelliSense XML ファイルを配置できます。

たとえば、次のフォルダー構造は、ドイツ語 (de)、イタリア語 (it)、日本語 (ja)、ロシア語 (ru)、簡体中国語 (zh-Hans)、および繁体中国語 (zh-Hant) をサポートします。

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

すべての言語は `net40` ターゲット フレームワーク フォルダーの下に一覧表示されます。 [複数のフレームワークをサポートする](../create-packages/supporting-multiple-target-frameworks.md)場合、`lib` の下に各バリアントのフォルダーがあります。

これらのフォルダーを配置して、`.nuspec` 内ですべてのファイルを参照します。

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

この手法を使用しする 1 つのサンプル パッケージは [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0) です。

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>メリットとデメリット (ローカライズされたリソース アセンブリ)

1 つのパッケージにすべての言語をビルドすることには、次のようないくつかのデメリットがあります。

1. **共有メタデータ**:NuGet パッケージは、1 つの `.nuspec` ファイルのみを含めることができるので、1 つの言語のメタデータだけを提供できます。 つまり、NuGet は、ローカライズされたメタデータのサポートを提供しません。
1. **パッケージのサイズ**:サポートする言語の数によっては、ライブラリがかなり大きくなる可能性があり、パッケージのインストールと復元の速度が低下します。
1. **同時リリース**:1 つのパッケージ内にローカライズされたファイルをバンドルするには、そのパッケージ内ですべてのアセットを同時にリリースする必要があり、個別に各ローカライズをリリースすることはできません。 さらに、1 つのローカライズに何らかの更新があった場合には、パッケージ全体の新しいバージョンが必要です。

ただし、いくつかのメリットもあります。

1. **シンプル**:パッケージのコンシューマーは、1 つのインストールでサポートされているすべての言語を取得し、各言語を個別にインストールする必要がありません。 1 つのパッケージは、nuget.org で見つけやすくもなります。
1. **組み合わせたバージョン**:すべてのリソース アセンブリが、プライマリ アセンブリと同じパッケージ内にあるので、それらのすべてが同じバージョン番号を共有し、誤って切り離されるリスクがなくなります。

## <a name="localized-satellite-packages"></a>ローカライズされたサテライト パッケージ

.NET Framework でのサテライト アセンブリのサポート方法と同様に、この方法では、ローカライズされたリソースと IntelliSense XML ファイルをサテライト パッケージに分割します。

これを行うには、プライマリ パッケージで、名前付け規則 `{identifier}.{version}.nupkg` を使用し、既定の言語 (en-US など) などのアセンブリを含めます。 たとえば、`ContosoUtilities.1.0.0.nupkg` には、次の構造が含まれます。

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

サテライト アセンブリは、`ContosoUtilities.de.1.0.0.nupkg` などのように名前付け規則 `{identifier}.{language}.{version}.nupkg`を使用します。 識別子は、プライマリ パッケージと完全に一致している**必要があります**。

これは、個別のパッケージに独自の `.nuspec` ファイルがあり、それがローカライズされたメタデータを含んでいるためです。 `.nuspec` の言語は、ファイル名で使用されるものと一致している**必要があります**。

サテライト アセンブリは、[] バージョン表記を使用して (「[Package versioning](../concepts/package-versioning.md)」(パッケージのバージョン管理) を参照してください)、プライマリ パッケージの正確なバージョンを宣言する**必要もあります**。 たとえば、`ContosoUtilities.de.1.0.0.nupkg` は、`[1.0.0]` 表記を使用して `ContosoUtilities.1.0.0.nupkg` で依存関係を宣言する必要があります。 サテライト パッケージでは、当然ながら、プライマリ パッケージと別のバージョン番号を付けることができます。

サテライト パッケージの構造で、パッケージ ファイル名の `{language}` と一致するサブフォルダーにリソース アセンブリと XML IntelliSense ファイルを含める必要があります。

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**注**: `ja-JP` などの特定のサブカルチャが必要な場合を除いて、`ja` のような高レベルの言語識別子を常に使用してください。

サテライト アセンブリで、NuGet は、ファイル名の `{language}` と一致するフォルダー内のファイル**のみ**を認識します。 他の属性はすべて無視されます。

これらのすべての規則が満たされたら、NuGet は、サテライト パッケージとしてパッケージを認識し、プライマリ パッケージの `lib` フォルダーにローカライズされたファイルをインストールします。それらがもともとバンドルされている場合と同様です。 サテライト パッケージをアンインストールすると、その同じフォルダーからそのファイルが削除されます。

サポートされている言語ごとに同じ方法で、追加のサテライト アセンブリを作成します。 例については、ASP.NET MVC のパッケージのセットを確認してください。

- [Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (英語のプライマリ)
- [Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (ドイツ語)
- [Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (日本語)
- [Microsoft.AspNet.Mvc.zh Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (簡体中国語)
- [Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (繁体中国語)

### <a name="summary-of-required-conventions"></a>必要な規則の概要

- プライマリ パッケージの名前を指定する必要があります。`{identifier}.{version}.nupkg`
- サテライト パッケージの名前を指定する必要があります。`{identifier}.{language}.{version}.nupkg`
- サテライト パッケージの `.nuspec` でファイル名に一致する言語を指定する必要があります。
- サテライト パッケージは、`.nuspec` ファイルで [] 表記を使用して、プライマリの正確なバージョンで依存関係を宣言する必要があります。 範囲はサポートされていません。
- サテライト パッケージは、ファイルの `{language}` と正確に一致する `lib\[{framework}\]{language}` フォルダー内にファイルを配置する必要があります。

### <a name="advantages-and-disadvantages-satellite-packages"></a>メリットとデメリット (サテライトのパッケージ)

サテライトのパッケージを使用すると、いくつかのメリットがあります。

1. **パッケージのサイズ**:プライマリ パッケージの全体的な大きさが最小限に抑えられ、コンシューマーには、使用する各言語のコストのみが発生します。
1. **個別のメタデータ**:各サテライト パッケージには、専用の `.nuspec` ファイルがあり、そのため、専用のローカライズされたメタデータがあります。 これにより、一部のコンシューマーが、ローカライズされた用語で nuget.org を検索することで、より簡単にパッケージを検索できます。
1. **切り離されたリリース**:サテライト アセンブリは、すべて一度にではなく時間の経過と共にリリースできるので、ローカライズ作業を分散することができます。

ただし、サテライト パッケージには、次の固有の一連のデメリットがあります。

1. **煩雑さ**:1 つのパッケージの代わりに、多くのパッケージがあるので、nuget.org で検索結果が煩雑になり、Visual Studio プロジェクト内で参照の一覧が長くなる可能性があります。
1. **厳密な規則**。 サテライト パッケージは、規則に厳密に従う必要があります。そうしないと、ローカライズされたバージョンは正しく取得されません。
1. **バージョン管理**:各サテライト パッケージは、プライマリ パッケージと正確なバージョンの依存関係を持っている必要があります。 つまり、プライマリ パッケージを更新した場合、リソースを変更しない場合でもすべてのサテライト パッケージも更新する必要があります。
