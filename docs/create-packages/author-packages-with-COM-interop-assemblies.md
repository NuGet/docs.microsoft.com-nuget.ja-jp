---
title: COM 相互運用アセンブリを含むパッケージを作成する
description: COM 相互運用アセンブリを含むパッケージを作成する方法について説明します
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b12672e81a974e113ffbda80560c9d3eede9c69d
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859123"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="b4808-103">COM 相互運用アセンブリを含む NuGet パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="b4808-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="b4808-104">COM 相互運用アセンブリを含むパッケージには、PackageReference 形式を利用して正しい `EmbedInteropTypes` メタデータがプロジェクトに追加されるように、適切な [targets ファイル](creating-a-package.md#include-msbuild-props-and-targets-in-a-package)が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="b4808-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="b4808-105">既定では、PackageReference が使用されるとき、`EmbedInteropTypes` メタデータは常にすべてのアセンブリに対して false になります。それにより、targets ファイルでこのメタデータが明示的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="b4808-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="b4808-106">競合を回避するために、ターゲット名を一意にする必要があります。理想的には、パッケージ名と組み込むアセンブリの組み合わせを使用します。下の例の `{InteropAssemblyName}` をその値で置換します。</span><span class="sxs-lookup"><span data-stu-id="b4808-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="b4808-107">(例については、[NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) もご覧ください。)</span><span class="sxs-lookup"><span data-stu-id="b4808-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="b4808-108">`packages.config` 管理形式を利用するとき、パッケージからアセンブリの参照を追加すると、NuGet と Visual Studio は COM 相互運用アセンブリがないか調べ、プロジェクト ファイルで `EmbedInteropTypes` を true に設定します。</span><span class="sxs-lookup"><span data-stu-id="b4808-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="b4808-109">この場合、ターゲットはオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="b4808-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="b4808-110">また、既定では、[ビルド アセットの推移的なフローはありません](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="b4808-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="b4808-111">ここで説明したように作成したパッケージの動作は、プロジェクトからプロジェクト参照に推移的依存関係として引き出されたときとは異なります。</span><span class="sxs-lookup"><span data-stu-id="b4808-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="b4808-112">パッケージの利用者は、ビルドを含めないように PrivateAssets の既定値を変更することでそれをフローさせることができます。</span><span class="sxs-lookup"><span data-stu-id="b4808-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>