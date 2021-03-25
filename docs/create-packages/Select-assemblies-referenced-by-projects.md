---
title: プロジェクトによって参照されるアセンブリを選択する
description: 実行時にすべてのアセンブリを利用できるとき、パッケージに含まれるアセンブリのサブセットをコンパイラで利用できるようにします。
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859032"
---
# <a name="select-assemblies-referenced-by-projects"></a>プロジェクトによって参照されるアセンブリを選択する

実行時にすべてのアセンブリを利用できるとき、明示的なアセンブリ参照により、IntelliSense やコンパイルでアセンブリのサブセットを使用できます。 `PackageReference` と `packages.config` では動作が異なるため、パッケージの作成者は両方のプロジェクト タイプと互換性があるパッケージを作成する必要があります。

> [!Note]
> 明示的なアセンブリ参照は .NET アセンブリに関連します。 マネージド アセンブリでプラットフォーム呼び出しされるネイティブ アセンブリを配布するメソッドではありません。

## <a name="packagereference-support"></a>`PackageReference` サポート

あるプロジェクトで `PackageReference` を含むパッケージが使用されるとき、そのパッケージに `ref\<tfm>\` ディレクトリが含まれている場合、NuGet では、それらのアセンブリがコンパイル時アセットとして分類され、`lib\<tfm>\` アセンブリは実行時アセットとして分類されます。 `ref\<tfm>\` のアセンブリは実行時に使用されません。 つまり、`ref\<tfm>\` のあらゆるアセンブリには、`lib\<tfm>\` または関連する `runtime\` ディレクトリに一致するアセンブリがあることが求められます。ない場合、実行時エラーがおそらく発生します。 `ref\<tfm>\` のアセンブリは実行時に使用されないため、パッケージ サイズを減らす[メタデータのみのアセンブリ](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md)になることがあります。

> [!Important]
> あるパッケージに nuspec `<references>` 要素 (`packages.config` で使用、下記) が含まれるが、`ref\<tfm>\` のアセンブリが含まれない場合、NuGet では、コンパイル アセットとランタイム アセットの両方として、nuspec `<references>` 要素に一覧表示されるアセンブリがアドバタイズされます。 つまり、参照されるアセンブリで `lib\<tfm>\` ディレクトリに他のアセンブリを読み込む必要があるとき、ランタイム例外が発生します。

> [!Note]
> パッケージに `runtime\` ディレクトリが含まれる場合、NuGet では `lib\` ディレクトリのアセットが使用されないことがあります。

## <a name="packagesconfig-support"></a>`packages.config` サポート

`packages.config` を使用して NuGet パッケージを管理するプロジェクトでは通常、`lib\<tfm>\` ディレクトリのすべてのアセンブリに参照が追加されます。 `ref\` ディレクトリは `PackageReference` をサポートする目的で追加されており、`packages.config` の使用時には考慮されません。 `packages.config` を使用するプロジェクトで参照されるアセンブリを明示的に設定するには、パッケージで [nuspec ファイルの `<references>` 要素](../reference/nuspec.md#explicit-assembly-references)を使用する必要があります。 次に例を示します。

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config` プロジェクトでは、[ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) というプロセスを使用し、`bin\<configuration>\` 出力ディレクトリにアセンブリをコピーします。 プロジェクトのアセンブリがコピーされると、ビルド システムがアセンブリ マニフェストで参照アセンブリを探し、そのアセンブリをコピーし、すべてのアセンブリに再帰的に繰り返します。 つまり、`lib\<tfm>\` ディレクトリのいずれかのアセンブリが他のアセンブリのマニフェストに依存関係として一覧表示されない場合 (`Assembly.Load`、MEF、またはその他の依存関係挿入フレームワークを利用し、実行時にアセンブリが読み込まれる場合)、`bin\<tfm>\` にあるとしても、プロジェクトの `bin\<configuration>\` 出力ディレクトリにコピーされないことがあります。

## <a name="example"></a>例

パッケージには、.NET Framework 4.7.2 を対象とする 3 つのアセンブリ (`MyLib.dll`、`MyHelpers.dll`、`MyUtilities.dll`) が含まれます。 `MyUtilities.dll` には、他の 2 つのアセンブリでのみ使用されるクラスが含まれます。そのため、IntelliSense やコンパイルで、自分のパッケージを使用するプロジェクトでそれらのクラスを利用できるようにします。 `nuspec` ファイルには、次の XML 要素を含める必要があります。

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

パッケージのファイルは次のようになります。

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
