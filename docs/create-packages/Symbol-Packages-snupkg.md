---
title: 新しいシンボル パッケージ形式 '.snupkg' を使用して NuGet シンボル パッケージを公開する方法 | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
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
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380419"
---
# <a name="creating-symbol-packages-snupkg"></a>シンボル パッケージ (.snupkg) の作成

きちんとデバッグできるには、コンパイルされたコードとソースコードの間の関連付け、ローカル変数の名前、スタック トレースなどの重要な情報を提供するデバッグ シンボルが必要です。 シンボル パッケージ (snupkg) を使用すると、これらのシンボルを配布して、お使いの NuGet パッケージのデバッグ エクスペリエンスを向上させることができます。

## <a name="prerequisites"></a>前提条件

必要な [NuGet プロトコル](https://www.nuget.org/downloads)を実装する [nuget.exe v4.9.0 以上](https://www.microsoft.com/net/download/dotnet-core/2.2) または [dotnet CLI v2.2.0 以上](../api/nuget-protocols.md)。

## <a name="creating-a-symbol-package"></a>シンボル パッケージを作成する

dotnet CLI または MSBuild を使用する場合は、`IncludeSymbols` プロパティと `SymbolPackageFormat` プロパティを設定し、.nupkg ファイルに加えて .snupkg ファイルを作成します。

* 次のプロパティを .csproj ファイルに追加するか:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* または、コマンド ラインで次のプロパティを指定します:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  or

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

NuGet.exe を使用する場合は、次のコマンドを使用すると .nupkg ファイルに加えて .snupkg ファイルを作成できます。

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) プロパティには、`symbols.nupkg` (既定値) または `snupkg` の 2 つの値のいずれかを指定できます。 このプロパティが指定されていない場合は、レガシ シンボル パッケージが作成されます。

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

NuGet.org は独自のシンボル サーバー リポジトリをサポートし、新しいシンボル パッケージ形式 `.snupkg` のみを受け入れます。 パッケージ コンシューマーは Visual Studio で自分のシンボル ソースに `https://symbols.nuget.org/download/symbols` を追加することで、nuget.org シンボル サーバーに公開されたシンボルを使用できます。それにより、Visual Studio デバッガーでパッケージ コードに入ることができます。 このプロセスの詳細については、「[Visual Studio デバッガーでのシンボル (.pdb) ファイルとソース ファイルの指定](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)」を参照してください。

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org シンボル パッケージの制約

NuGet.org には、シンボル パッケージに対して次の制約があります。

- シンボル パッケージでは、次のファイル拡張子のみが許可されます: `.pdb`、`.nuspec`、`.xml`、`.psmdcp`、`.rels`、`.p7s`
- NuGet.org のシンボル サーバーでは管理対象の[ポータブル PDB](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) のみがサポートされています。
- PDB と関連付けられている .nupkg DLL は、Visual Studio バージョン 15.9 以上のコンパイラでビルドする必要があります (「[PDB 暗号化ハッシュ](https://github.com/dotnet/roslyn/issues/24429)」を参照)

これらの制約が満たされない場合、NuGet.org に発行されたシンボル パッケージは検証に失敗します。 

### <a name="symbol-package-validation-and-indexing"></a>シンボル パッケージの検証とインデックスの作成

[NuGet.org](https://www.nuget.org/) に発行されたシンボル パッケージは、マルウェアのスキャンなど、いくつかの検証を受けます。 パッケージが検証チェックに失敗した場合、そのパッケージの詳細ページにエラー メッセージが表示されます。 さらに、パッケージの所有者は、特定された問題の修正方法を示す電子メールを受信します。

シンボル パッケージがすべての検証に合格すると、そのシンボルは NuGet. org のシンボル サーバーによってインデックス付けされ、使用可能になります。

パッケージの検証とインデックスの作成は、通常、15 以内で完了します。 パッケージの公開に予想以上の時間がかかる場合、[status.nuget.org](https://status.nuget.org/) にアクセスし、Nuget.org に中断が発生していないか確認してください。 すべてのシステムが動作しているとき、1 時間以内にパッケージが正常に公開されない場合、nuget.org にログインし、パッケージの詳細ページの [Contact Support] リンクからお問い合わせください。

## <a name="symbol-package-structure"></a>シンボル パッケージ構造

シンボル パッケージ (.snupkg) には、次の特徴があります。

1) .snupkg の ID とバージョンは、対応する NuGet パッケージ (.nupkg) のものと同じです。
2) .snupkg のすべての DLL や EXE ファイルのファイル構造は、DLL および EXE ではなくそれに対応する PDB が同じフォルダ構造に含まれることを除き、それと対応する nupkg と全く同じです。 PDB 以外の拡張子のファイルとフォルダーは snupkg から除外されたままになります。
3) シンボル パッケージの .nuspec ファイルのパッケージの種類は、`SymbolsPackage` です。

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) 作成者が nupkg と snupkg のビルドにカスタムの nuspec を使用した場合、snupkg には 2) で説明したものと同じフォルダ階層とファイルが含まれます。
5) 次のフィールドは snupkg の nuspec から除外されます: ```authors```、```owners```、```requireLicenseAcceptance```、```license type```、```licenseUrl```、```icon```。
6) ```<license>``` 要素は使用しないでください。 .snupkg には、対応する .nupkg と同じライセンスが適用されます。

## <a name="see-also"></a>参照

ソース リンクを使用して、.NET アセンブリのソース コードのデバッグを有効にすることを検討してください。 詳細については、「[ソース リンクのガイダンス](/dotnet/standard/library-guidance/sourcelink)」を参照してください。

シンボル パッケージの詳細については、「[NuGet パッケージのデバッグとシンボルの機能強化](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)」の設計仕様を参照してください。
