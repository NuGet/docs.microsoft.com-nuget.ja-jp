---
title: プロジェクトの形式を特定する
description: プロジェクトの形式を特定する方法について説明します
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843444"
---
# <a name="identify-the-project-format"></a>プロジェクトの形式を特定する

NuGet はすべての .NET プロジェクトに対応しています。 ただし、NuGet パッケージの使用と作成のために使う必要がある一部のツールと方法は、プロジェクトの形式 (SDK スタイルまたは非 SDK スタイル) によって決まります。 SDK スタイルのプロジェクトでは、[SDK 属性](/dotnet/core/tools/csproj#additions)が使用されます。 NuGet パッケージの使用と作成のために使う方法とツールは、プロジェクトの形式によって異なるため、ご自分のプロジェクトの種類を特定することが重要です。 非 SDK スタイルのプロジェクトの場合、その方法とツールは、そのプロジェクトが `PackageReference` 形式に移行されているかどうかにも依存します。

ご自分のプロジェクトが SDK スタイルであるかどうかは、そのプロジェクトの作成に使用した方法によって異なります。 次の表は、Visual Studio 2017 以降のバージョンを使ってプロジェクトを作成した場合の、プロジェクトの既定の形式と、関連付けられている CLI ツールを示しています。

| プロジェクト&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | プロジェクトの既定の形式 | CLI ツール&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | メモ |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK スタイル | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Visual Studio 2017 より前に作成されたプロジェクトは SDK 形式ではありません。 `nuget.exe` CLI をお使いください。 |
| .NET Core | SDK スタイル | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Visual Studio 2017 より前に作成されたプロジェクトは SDK 形式ではありません。 `nuget.exe` CLI をお使いください。 |
| .NET Framework | 非 SDK スタイル | [nuget.exe CLI](../install-nuget-client-tools.md#nugetexe-cli) | 他の方法で作成された .NET Framework プロジェクトは、SDK スタイルのプロジェクトである場合があります。 そのような場合は、代わりに [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) をお使いください。 |
| [移行した](../reference/migrate-packages-config-to-package-reference.md) .NET プロジェクト | 非 SDK スタイル| パッケージを作成する場合は、[msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) を使ってパッケージを作成します。 | パッケージを作成する場合は、`msbuild -t:pack` をお勧めします。 それ以外の場合は、[dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) をお使いください。 移行されたプロジェクトは、SDK スタイルのプロジェクトではありません。 |

## <a name="check-the-project-format"></a>プロジェクトの形式を確認する

プロジェクトが SDK スタイルの形式であるかどうかがわからない場合は、プロジェクト ファイル (C# の場合は *.csproj ファイル) の `<Project>` 要素で SDK 属性を探します。 これが存在する場合、そのプロジェクトは SDK スタイルのプロジェクトです。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>Visual Studio でプロジェクトの形式を確認する

Visual Studio で作業している場合は、次のいずれかの方法を使用して、プロジェクトの形式をすばやく確認できます。

- ソリューション エクスプローラーでプロジェクトを右クリックし、 **[<プロジェクト名>.csproj の編集]** を選択します。

   このオプションは、Visual Studio 2017 以降で、SDK スタイルの属性を使用するプロジェクトに対してのみ使用できます。 それ以外の場合は、他の方法を使用します。

   ![プロジェクト ファイルを編集する](media/edit-project-file.png)

   SDK スタイルのプロジェクトのプロジェクト ファイルには、[SDK 属性](/dotnet/core/tools/csproj#additions)が表示されます。
   
- **[プロジェクト]** メニューから、 **[プロジェクトのアンロード]** を選択します (または、プロジェクトを右クリックして、 **[プロジェクトのアンロード]** を選択します)。

   このプロジェクトのプロジェクト ファイルには、SDK 属性が含まれません。 これは SDK 形式のプロジェクトではありません。

   ![プロジェクトのアンロード](media/unload-project.png)

   次に、アンロードされたプロジェクトを右クリックし、 **[<プロジェクト名>.csproj の編集]** を選択します。

## <a name="see-also"></a>関連項目

- [dotnet CLI を使用して .NET Standard パッケージを作成する](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Visual Studio で .NET Standard パッケージを作成する](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [.NET Framework パッケージの作成と公開 (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [MSBuild ターゲットとしての NuGet の pack と restore](../reference/msbuild-targets.md)
