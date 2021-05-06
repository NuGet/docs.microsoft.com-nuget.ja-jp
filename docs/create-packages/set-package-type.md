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
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="15f80-103">NuGet パッケージの種類を設定する</span><span class="sxs-lookup"><span data-stu-id="15f80-103">Set a NuGet package type</span></span>

<span data-ttu-id="15f80-104">パッケージは、使用目的を示すために、1 つ以上の "*パッケージの種類*" でマークすることができます。</span><span class="sxs-lookup"><span data-stu-id="15f80-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="15f80-105">既知のパッケージの種類</span><span class="sxs-lookup"><span data-stu-id="15f80-105">Known package types</span></span>

- <span data-ttu-id="15f80-106">種類が `Dependency` のパッケージでは、ビルド時または実行時アセットがライブラリとアプリケーションに追加されます。(互換性があれば) あらゆる種類のプロジェクトにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="15f80-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="15f80-107">種類が `DotnetTool` のパッケージは、[dotnet CLI](/dotnet/articles/core/tools/index) でインストールできる .NET ツールです。</span><span class="sxs-lookup"><span data-stu-id="15f80-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="15f80-108">`Template` 型パッケージには、アプリ、サービス、ツール、クラス ライブラリなどのファイルまたはプロジェクトの作成に使用できる[カスタム テンプレート](/dotnet/core/tools/custom-templates)があります。</span><span class="sxs-lookup"><span data-stu-id="15f80-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="15f80-109">種類の印が付いていないパッケージ (初期のバージョンの NuGet で作成されたすべてのパッケージが相当) は種類が `Dependency` に初期設定されます。</span><span class="sxs-lookup"><span data-stu-id="15f80-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="15f80-110">パッケージの種類のサポートは、NuGet 3.5 で追加されました。</span><span class="sxs-lookup"><span data-stu-id="15f80-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="15f80-111">カスタム パッケージの種類が必要ない場合は、パッケージの種類を明示的に "*設定しない*" ことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="15f80-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="15f80-112">種類を指定しないと、NuGet によって既定で種類 `Dependency` になります。</span><span class="sxs-lookup"><span data-stu-id="15f80-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="15f80-113">カスタム パッケージの種類</span><span class="sxs-lookup"><span data-stu-id="15f80-113">Custom package types</span></span>

<span data-ttu-id="15f80-114">パッケージの用途が[既知のパッケージの種類](#known-package-types)に合わない場合は、1 つ以上のカスタム パッケージの種類でパッケージをマークできます。</span><span class="sxs-lookup"><span data-stu-id="15f80-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="15f80-115">たとえば、`Contoso` アプリの顧客が拡張機能をインストールできるとします。</span><span class="sxs-lookup"><span data-stu-id="15f80-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="15f80-116">アプリでは、パッケージが必要な規則に従っている適切な拡張機能であることを示すために、カスタム パッケージの種類 `ContosoExtension` を使用するよう、拡張機能の作成者に要求することができます。</span><span class="sxs-lookup"><span data-stu-id="15f80-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="15f80-117">カスタム パッケージの種類が設定されているパッケージは、Visual Studio または nuget.exe ではインストールできません。</span><span class="sxs-lookup"><span data-stu-id="15f80-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="15f80-118">詳細については、[NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="15f80-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="15f80-119">dotnet CLI の使用</span><span class="sxs-lookup"><span data-stu-id="15f80-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="15f80-120">パッケージの種類は、プロジェクト ファイル (`.csproj`) で設定できます。</span><span class="sxs-lookup"><span data-stu-id="15f80-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="15f80-121">複数の用途があるパッケージには、`;` 区切り記号を使用して複数のパッケージの種類を設定できます。</span><span class="sxs-lookup"><span data-stu-id="15f80-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="15f80-122">パッケージの種類とその [`Version`](/dotnet/api/system.version) 文字列の間に区切り記号 `,` を使用することで、パッケージの種類のバージョンを管理できます。</span><span class="sxs-lookup"><span data-stu-id="15f80-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="15f80-123">nuget.exe の使用</span><span class="sxs-lookup"><span data-stu-id="15f80-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="15f80-124">パッケージの種類は、`.nuspec` ファイルの `packageTypes\packageType` ノードの `<metadata>` 要素で設定します。</span><span class="sxs-lookup"><span data-stu-id="15f80-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

<span data-ttu-id="15f80-125">複数の用途を持つパッケージは、複数のパッケージの種類でマークできます。</span><span class="sxs-lookup"><span data-stu-id="15f80-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

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

<span data-ttu-id="15f80-126">パッケージの種類は、文字列 [`Version`](/dotnet/api/system.version) を使用してバージョン管理できます。</span><span class="sxs-lookup"><span data-stu-id="15f80-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

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

<span data-ttu-id="15f80-127">パッケージの種類の文字列の形式は、パッケージ ID とまったく同じです。</span><span class="sxs-lookup"><span data-stu-id="15f80-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="15f80-128">つまり、パッケージの種類は、正規表現 `^\w+([_.-]\w+)*$` と一致する、大文字と小文字が区別されない、1 文字以上 100 文字以下の文字列です。</span><span class="sxs-lookup"><span data-stu-id="15f80-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="15f80-129">パッケージの種類のバージョンを指定する場合は、[`Version`](/dotnet/api/system.version) の文字列になります。</span><span class="sxs-lookup"><span data-stu-id="15f80-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="15f80-130">パッケージの種類のバージョンは省略可能であり、既定値は `0.0` です。</span><span class="sxs-lookup"><span data-stu-id="15f80-130">The package type version is optional and defaults to `0.0`.</span></span>
