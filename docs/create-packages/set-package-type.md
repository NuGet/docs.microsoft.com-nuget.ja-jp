---
title: NuGet パッケージの種類を設定する
description: パッケージの使用目的を示すパッケージの種類について説明します。
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067280"
---
# <a name="set-a-nuget-package-type"></a>NuGet パッケージの種類を設定する

パッケージは、使用目的を示すために、1 つ以上の "*パッケージの種類*" でマークすることができます。

## <a name="known-package-types"></a>既知のパッケージの種類

- 種類が `Dependency` のパッケージでは、ビルド時または実行時アセットがライブラリとアプリケーションに追加されます。(互換性があれば) あらゆる種類のプロジェクトにインストールできます。

- 種類が `DotnetTool` のパッケージは、[dotnet CLI](/dotnet/articles/core/tools/index) でインストールできる .NET ツールです。

- `Template` 型パッケージには、アプリ、サービス、ツール、クラス ライブラリなどのファイルまたはプロジェクトの作成に使用できる[カスタム テンプレート](/dotnet/core/tools/custom-templates)があります。

種類の印が付いていないパッケージ (初期のバージョンの NuGet で作成されたすべてのパッケージが相当) は種類が `Dependency` に初期設定されます。

> [!NOTE]
> パッケージの種類のサポートは、NuGet 3.5 で追加されました。
> カスタム パッケージの種類が必要ない場合は、パッケージの種類を明示的に "*設定しない*" ことをお勧めします。
> 種類を指定しないと、NuGet によって既定で種類 `Dependency` になります。

## <a name="custom-package-types"></a>カスタム パッケージの種類

パッケージの用途が[既知のパッケージの種類](#known-package-types)に合わない場合は、1 つ以上のカスタム パッケージの種類でパッケージをマークできます。

たとえば、`Contoso` アプリの顧客が拡張機能をインストールできるとします。 アプリでは、パッケージが必要な規則に従っている適切な拡張機能であることを示すために、カスタム パッケージの種類 `ContosoExtension` を使用するよう、拡張機能の作成者に要求することができます。

> [!WARNING]
> カスタム パッケージの種類が設定されているパッケージは、Visual Studio または nuget.exe ではインストールできません。 詳細については、[NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) を参照してください。

# <a name="using-dotnet-cli"></a>[dotnet CLI の使用](#tab/dotnet)

パッケージの種類は、プロジェクト ファイル (`.csproj`) で設定できます。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

複数の用途があるパッケージには、`;` 区切り記号を使用して複数のパッケージの種類を設定できます。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

パッケージの種類とその [`Version`](/dotnet/api/system.version) 文字列の間に区切り記号 `,` を使用することで、パッケージの種類のバージョンを管理できます。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[nuget.exe の使用](#tab/nugetexe)

パッケージの種類は、`.nuspec` ファイルの `packageTypes\packageType` ノードの `<metadata>` 要素で設定します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

複数の用途を持つパッケージは、複数のパッケージの種類でマークできます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

パッケージの種類は、文字列 [`Version`](/dotnet/api/system.version) を使用してバージョン管理できます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

パッケージの種類の文字列の形式は、パッケージ ID とまったく同じです。 つまり、パッケージの種類は、正規表現 `^\w+([_.-]\w+)*$` と一致する、大文字と小文字が区別されない、1 文字以上 100 文字以下の文字列です。

パッケージの種類のバージョンを指定する場合は、[`Version`](/dotnet/api/system.version) の文字列になります。 パッケージの種類のバージョンは省略可能であり、既定値は `0.0` です。
