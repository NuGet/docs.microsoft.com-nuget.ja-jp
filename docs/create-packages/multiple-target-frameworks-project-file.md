---
title: プロジェクト ファイル内での NuGet パッケージの複数バージョン対応
description: 1 つの NuGet パッケージ内から複数の .NET Framework バージョンに対応するためのさまざま方法の説明。
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: b7870bb6aac39f0865d88efc8c16751fdbecc3a8
ms.sourcegitcommit: cae759ad8518c049575a30ad3bf04fe5d06244fb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2019
ms.locfileid: "68616779"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="ecace-103">プロジェクト ファイル内で複数の .NET Framework バージョンをサポートする</span><span class="sxs-lookup"><span data-stu-id="ecace-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="ecace-104">プロジェクトを初めて作成するときは、.NET Standard クラス ライブラリを作成することをお勧めします。これにより、幅広い使用元プロジェクトとの互換性が提供されます。</span><span class="sxs-lookup"><span data-stu-id="ecace-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="ecace-105">.NET Standard を使用すると、.NET ライブラリへの[クロスプラットフォーム サポート](/dotnet/standard/library-guidance/cross-platform-targeting)が既定で追加されます。</span><span class="sxs-lookup"><span data-stu-id="ecace-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="ecace-106">ただし、シナリオによっては、特定のフレームワークを対象とするコードを含める必要がある場合もあります。</span><span class="sxs-lookup"><span data-stu-id="ecace-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="ecace-107">この記事では、[SDK スタイル](../resources/check-project-format.md)のプロジェクトでこれを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ecace-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="ecace-108">SDK スタイルのプロジェクトでは、プロジェクト ファイルで複数のターゲット フレームワーク ([TFM](/dotnet/standard/frameworks)) のサポートを構成してから、`dotnet pack` または `msbuild /t:pack` を使用してパッケージを作成できます。</span><span class="sxs-lookup"><span data-stu-id="ecace-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="ecace-109">nuget.exe CLI では、SDK スタイルのプロジェクトのパッキングはサポートされていないため、`dotnet pack` または `msbuild /t:pack` のみを使用してください。</span><span class="sxs-lookup"><span data-stu-id="ecace-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="ecace-110">代わりに、通常 `.nuspec` ファイル内にある[すべてのプロパティを、プロジェクト ファイルに含める](../reference/msbuild-targets.md#pack-target)ことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ecace-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="ecace-111">SDK 形式以外のプロジェクトで複数の .NET Framework バージョンを対象とする場合は、「[複数の .NET Framework バージョンのサポート](supporting-multiple-target-frameworks.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ecace-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="ecace-112">複数の .NET Framework バージョンをサポートするプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="ecace-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="ecace-113">Visual Studio か `dotnet new classlib` を使用して、新しい .NET Standard クラス ライブラリを作成します。</span><span class="sxs-lookup"><span data-stu-id="ecace-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="ecace-114">互換性を最大限に高めるために、.NET Standard クラス ライブラリを作成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ecace-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="ecace-115">*.csproj* ファイルを編集して、ターゲット フレームワークをサポートします。</span><span class="sxs-lookup"><span data-stu-id="ecace-115">Edit the *.csproj* file to support the target frameworks.</span></span>

   <span data-ttu-id="ecace-116">たとえば、`<TargetFramework>netstandard2.0</TargetFramework>` を `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>` に変更します。</span><span class="sxs-lookup"><span data-stu-id="ecace-116">For example, change `<TargetFramework>netstandard2.0</TargetFramework>` to `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.</span></span>

   <span data-ttu-id="ecace-117">XML 要素が単数形から複数形に変更されていることを確認します ("s" を開始タグと終了タグの両方に追加します)。</span><span class="sxs-lookup"><span data-stu-id="ecace-117">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="ecace-118">1 つの TFM でのみ動作するコードがある場合は、`#if NET45` または `#if NETSTANDARD20` を使用して、TFM に依存するコードを分離できます。</span><span class="sxs-lookup"><span data-stu-id="ecace-118">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD20` to separate TFM-dependent code.</span></span> <span data-ttu-id="ecace-119">(詳細については、「[マルチターゲットを設定する方法](/dotnet/core/tutorials/libraries#how-to-multitarget)」を参照してください。)たとえば、次のコードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="ecace-119">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

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

4. <span data-ttu-id="ecace-120">必要な NuGet メタデータをすべて MSBuild プロパティとして *.csproj* に追加します。</span><span class="sxs-lookup"><span data-stu-id="ecace-120">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="ecace-121">使用可能なパッケージ メタデータと MSBuild プロパティ名の一覧については、「[pack ターゲット](../reference/msbuild-targets.md#pack-target)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ecace-121">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="ecace-122">また、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="ecace-122">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="ecace-123">ビルド関連のプロパティを NuGet メタデータから分離する場合は、別の `PropertyGroup` を使用するか、NuGet プロパティを別のファイルに配置し、MSBuild の `Import` ディレクティブを使用してそれを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="ecace-123">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="ecace-124">`Directory.Build.Props` および `Directory.Build.Targets` は、MSBuild 15.0 以降でもサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ecace-124">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="ecace-125">次に、`dotnet pack` を使用すると、結果の *.nupkg* で .NET Standard 2.0 と .NET Framework 4.5 の両方が対象となります。</span><span class="sxs-lookup"><span data-stu-id="ecace-125">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="ecace-126">前の手順と .NET Core SDK 2.2 を使用して生成された *.csproj* ファイルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="ecace-126">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="ecace-127">関連項目</span><span class="sxs-lookup"><span data-stu-id="ecace-127">See also</span></span>

* [<span data-ttu-id="ecace-128">ターゲット フレームワークを指定する方法</span><span class="sxs-lookup"><span data-stu-id="ecace-128">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="ecace-129">クロス プラットフォーム ターゲット</span><span class="sxs-lookup"><span data-stu-id="ecace-129">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
