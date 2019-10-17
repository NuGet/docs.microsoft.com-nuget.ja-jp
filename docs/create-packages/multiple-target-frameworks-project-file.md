---
title: プロジェクト ファイル内での NuGet パッケージの複数バージョン対応
description: 1 つの NuGet パッケージ内から複数の .NET Framework バージョンに対応するためのさまざま方法の説明。
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1d23759433efb405fa5f0035049befced2c43d6b
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380685"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>プロジェクト ファイル内で複数の .NET Framework バージョンをサポートする

プロジェクトを初めて作成するときは、.NET Standard クラス ライブラリを作成することをお勧めします。これにより、幅広い使用元プロジェクトとの互換性が提供されます。 .NET Standard を使用すると、.NET ライブラリへの[クロスプラットフォーム サポート](/dotnet/standard/library-guidance/cross-platform-targeting)が既定で追加されます。 ただし、シナリオによっては、特定のフレームワークを対象とするコードを含める必要がある場合もあります。 この記事では、[SDK スタイル](../resources/check-project-format.md)のプロジェクトでこれを行う方法について説明します。

SDK スタイルのプロジェクトでは、プロジェクト ファイルで複数のターゲット フレームワーク ([TFM](/dotnet/standard/frameworks)) のサポートを構成してから、`dotnet pack` または `msbuild /t:pack` を使用してパッケージを作成できます。

> [!NOTE]
> nuget.exe CLI では、SDK スタイルのプロジェクトのパッキングはサポートされていないため、`dotnet pack` または `msbuild /t:pack` のみを使用してください。 代わりに、通常 `.nuspec` ファイル内にある[すべてのプロパティを、プロジェクト ファイルに含める](../reference/msbuild-targets.md#pack-target)ことをお勧めします。 SDK 形式以外のプロジェクトで複数の .NET Framework バージョンを対象とする場合は、「[複数の .NET Framework バージョンのサポート](supporting-multiple-target-frameworks.md)」を参照してください。

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>複数の .NET Framework バージョンをサポートするプロジェクトを作成する

1. Visual Studio か `dotnet new classlib` を使用して、新しい .NET Standard クラス ライブラリを作成します。

   互換性を最大限に高めるために、.NET Standard クラス ライブラリを作成することをお勧めします。

2. *.csproj* ファイルを編集して、ターゲット フレームワークをサポートします。 たとえば、
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   この行を次のように変更します。
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   XML 要素が単数形から複数形に変更されていることを確認します ("s" を開始タグと終了タグの両方に追加します)。

3. 1 つの TFM でのみ動作するコードがある場合は、`#if NET45` または `#if NETSTANDARD2_0` を使用して、TFM に依存するコードを分離できます。 (詳細については、「[マルチターゲットを設定する方法](/dotnet/core/tutorials/libraries#how-to-multitarget)」を参照してください。)たとえば、次のコードを使用できます。

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. 必要な NuGet メタデータをすべて MSBuild プロパティとして *.csproj* に追加します。

   使用可能なパッケージ メタデータと MSBuild プロパティ名の一覧については、「[pack ターゲット](../reference/msbuild-targets.md#pack-target)」を参照してください。 また、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」も参照してください。

   ビルド関連のプロパティを NuGet メタデータから分離する場合は、別の `PropertyGroup` を使用するか、NuGet プロパティを別のファイルに配置し、MSBuild の `Import` ディレクティブを使用してそれを含めることができます。 `Directory.Build.Props` および `Directory.Build.Targets` は、MSBuild 15.0 以降でもサポートされています。

5. 次に、`dotnet pack` を使用すると、結果の *.nupkg* で .NET Standard 2.0 と .NET Framework 4.5 の両方が対象となります。

前の手順と .NET Core SDK 2.2 を使用して生成された *.csproj* ファイルを次に示します。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>関連項目

* [ターゲット フレームワークを指定する方法](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [クロス プラットフォーム ターゲット](/dotnet/standard/library-guidance/cross-platform-targeting)
