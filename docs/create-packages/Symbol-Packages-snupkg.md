---
title: 新しいシンボル パッケージ形式 '.snupkg' を使用して NuGet シンボル パッケージを公開する方法 | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet シンボル パッケージ (snupkg) の作成方法。
keywords: NuGet シンボル パッケージ, NuGet パッケージ デバッグ, NuGet デバッグ対応, パッケージ シンボル, シンボル パッケージ規則
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 9f9cdd188cf2ec678bc9047604e618f1af9124ae
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842465"
---
# <a name="creating-symbol-packages-snupkg"></a>シンボル パッケージ (.snupkg) の作成

シンボル パッケージを利用すると、NuGet パッケージのデバッグがしやすくなります。

## <a name="prerequisites"></a>必須コンポーネント

必要な [NuGet プロトコル](../api/nuget-protocols.md)を実装する、[nuget.exe v4.9.0 以上](https://www.nuget.org/downloads)または [dotnet.exe v2.2.0 以上](https://www.microsoft.com/net/download/dotnet-core/2.2)。

## <a name="creating-a-symbol-package"></a>シンボル パッケージを作成する

snupkg シンボル パッケージを作成するには、dotnet.exe、NuGet.exe、または MSBuild を使用します。 NuGet.exe を使用する場合は、次のコマンドを使用すると .nupkg ファイルに加えて .snupkg ファイルを作成できます。

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

dotnet.exe または MSBuild を使用する場合は、次の手順で .nupkg ファイルに加えて .snupkg ファイルを作成します。

1. 次に示すプロパティを .csproj ファイルに追加します。

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. `dotnet pack MyPackage.csproj` または `msbuild -t:pack MyPackage.csproj` を使用してプロジェクトをパックします。

[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) プロパティには、`symbols.nupkg` (既定値) または `snupkg` の 2 つの値のいずれかを指定できます。 [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) プロパティが指定されていない場合は、レガシ シンボル パッケージが作成されます。

> [!Note]
> 従来の形式 `.symbols.nupkg` は引き続きサポートされますが、これは互換性のみを目的としています ([レガシ シンボル パッケージ](Symbol-Packages.md)に関する記事を参照)。 NuGet.org のシンボル サーバーは、新しいシンボル パッケージ形式 `.snupkg` のみを受け入れます。

## <a name="publishing-a-symbol-package"></a>シンボル パッケージを公開する

1. 便宜上、最初に NuGet で API キーを保存してください (「[パッケージを公開する](../nuget-org/publish-a-package.md)」を参照)。

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. nuget.org にプライマリ パッケージを公開した後は、次のようにしてシンボル パッケージをプッシュします。

    ```cli
    nuget push MyPackage.snupkg
    ```

1. 以下のコマンドを使用して、プライマリ パッケージとシンボル パッケージの両方を同時にプッシュすることもできます。 .nupkg および .snupkg ファイルの両方が、現在のフォルダーに存在する必要があります。

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet では、両方のパッケージが nuget.org に公開されます。最初に `MyPackage.nupkg` が、次に `MyPackage.snupkg` が公開されます。

> [!Note]
> シンボル パッケージが公開されていない場合は、NuGet.org のソースを `https://api.nuget.org/v3/index.json` として構成したことを確認します。 シンボル パッケージの公開は、[NuGet V3 API](../api/overview.md#versioning) によってのみサポートされています。

## <a name="nugetorg-symbol-server"></a>NuGet.org のシンボル サーバー

NuGet.org は独自のシンボル サーバー リポジトリをサポートし、新しいシンボル パッケージ形式 `.snupkg` のみを受け入れます。 パッケージ コンシューマーは Visual Studio で自分のシンボル ソースに `https://symbols.nuget.org/download/symbols` を追加することで、nuget.org シンボル サーバーに公開されたシンボルを使用できます。それにより、Visual Studio デバッガーでパッケージ コードに入ることができます。 このプロセスの詳細については、「[Visual Studio デバッガーでのシンボル (.pdb) ファイルとソース ファイルの指定](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017)」を参照してください。

### <a name="nugetorg-symbol-package-constraints"></a>Nuget.org シンボル パッケージの制約

nuget.org でサポートされているシンボル パッケージには、次の 2 つの制約があります

- 次のファイル拡張子のみをシンボル パッケージに追加できます。 ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- nuget シンボル サーバーでは管理対象の[ポータブル PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) のみが現在サポートされています。
- PDB と関連付けられている nupkg dll は、Visual studio バージョン 15.9 以上のコンパイラでビルドする必要があります ([pdb 暗号化ハッシュ](https://github.com/dotnet/roslyn/issues/24429)に関する記事を参照)

それ以外のファイルの種類が .snupkg に含まれていると、nuget.org でのシンボル パッケージの公開は失敗します。

### <a name="symbol-package-validation-and-indexing"></a>シンボル パッケージの検証とインデックスの作成

[NuGet.org](https://www.nuget.org/) にプッシュされたパッケージは、ウイルス チェックなど、いくつかの検証を受けます。

パッケージがすべての検証チェックに合格してから、シンボルのインデックスを作成し、NuGet.org シンボル サーバーで使用できるようになるまでには少し時間がかかります。 パッケージが検証チェックで不合格になった場合、.nupkg のパッケージの詳細ページが更新され、関連エラーが表示されます。それに関する電子メールも届きます。

パッケージの検証とインデックスの作成は、通常、15 以内で完了します。 パッケージ公開に予想以上の時間がかかる場合、[status.nuget.org](https://status.nuget.org/) にアクセスし、nuget.org に中断が発生していないか確認してください。 すべてのシステムが動作しているとき、1 時間以内にパッケージが正常に公開されない場合、nuget.org にログインし、パッケージの詳細ページの [Contact Support] リンクからお問い合わせください。

## <a name="symbol-package-structure"></a>シンボル パッケージ構造

.nupkg ファイルは全く変わりませんが、.snupkg ファイルには次の特性が含まれます。

1) .snupkg の ID とバージョンは、対応する .nupkg と同じになります。
2) .snupkg のファイル構造は DLL や EXE ファイルの nupkg と全く同じですが、区別されています。対応する PDB が同じフォルダ構造に含まれています。 PDB 以外の拡張子のファイルとフォルダーは snupkg から除外されたままになります。
3) .snupkg の .nuspec ファイルでは次に示すように新しい PackageType も指定されます。 指定される PackageType は 1 つだけです。 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) 作成者が nupkg と snupkg のビルドにカスタムの nuspec を使用した場合、snupkg には 2) で説明したものと同じフォルダ階層とファイルが含まれます。
5) ```authors``` と ```owners``` のフィールドは snupkg の nuspec から除外されます。

## <a name="see-also"></a>関連項目

[NuGet パッケージのデバッグとシンボルの改善](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
