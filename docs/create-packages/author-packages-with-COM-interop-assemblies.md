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
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>COM 相互運用アセンブリを含む NuGet パッケージを作成する

COM 相互運用アセンブリを含むパッケージには、PackageReference 形式を利用して正しい `EmbedInteropTypes` メタデータがプロジェクトに追加されるように、適切な [targets ファイル](creating-a-package.md#include-msbuild-props-and-targets-in-a-package)が含まれる必要があります。 既定では、PackageReference が使用されるとき、`EmbedInteropTypes` メタデータは常にすべてのアセンブリに対して false になります。それにより、targets ファイルでこのメタデータが明示的に追加されます。 競合を回避するために、ターゲット名を一意にする必要があります。理想的には、パッケージ名と組み込むアセンブリの組み合わせを使用します。下の例の `{InteropAssemblyName}` をその値で置換します。 (例については、[NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) もご覧ください。)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

`packages.config` 管理形式を利用するとき、パッケージからアセンブリの参照を追加すると、NuGet と Visual Studio は COM 相互運用アセンブリがないか調べ、プロジェクト ファイルで `EmbedInteropTypes` を true に設定します。 この場合、ターゲットはオーバーライドされます。

また、既定では、[ビルド アセットの推移的なフローはありません](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。 ここで説明したように作成したパッケージの動作は、プロジェクトからプロジェクト参照に推移的依存関係として引き出されたときとは異なります。 パッケージの利用者は、ビルドを含めないように PrivateAssets の既定値を変更することでそれをフローさせることができます。

<a name="creating-the-package"></a>