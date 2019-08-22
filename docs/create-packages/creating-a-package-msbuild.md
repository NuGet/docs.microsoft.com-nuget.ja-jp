---
title: MSBuild を使用して NuGet パッケージを作成する
description: NuGet パッケージを設計し、作成する過程を詳しく説明します。ファイルやバージョン管理など、重要な決定ポイントが含まれます。
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: a965a3049f46af59efcfad2ecf19e0923fda413b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488946"
---
# <a name="create-a-nuget-package-using-msbuild"></a>MSBuild を使用して NuGet パッケージを作成する

自分のコードで NuGet パッケージを作成する場合、その機能をコンポーネントにパッケージ化し、数を問わず他の開発者と共有し、使用することができます。 この記事では、MSBuild を使用してパッケージを作成する方法について説明します。 MSBuild は、NuGet を含むすべての Visual Studio ワークロードにプレインストールされています。 また、dotnet CLI と [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild) を使用して MSBuild を使用することもできます。

[SDK スタイルの形式](../resources/check-project-format.md)を使用する .NET Core および .NET Standard プロジェクト、またその他の SDK スタイルのあらゆるプロジェクトに対して、NuGet ではプロジェクト ファイルにある情報を直接使ってパッケージが作成されます。  `<PackageReference>` を使用する SDK スタイル以外のプロジェクトの場合、NuGet ではプロジェクト ファイルを使用してパッケージを作成することもできます。

SDK スタイルのプロジェクトには、既定でパック機能を利用できます。 SDK スタイル以外の PackageReference プロジェクトでは、プロジェクトの依存関係に NuGet.Build.Tasks.Pack パッケージを追加する必要があります。 MSBuild パック ターゲットの詳細については、「[MSBuild ターゲットとしての NuGet の pack と restore](../reference/msbuild-targets.md)」を参照してください。

パッケージ (`msbuild -t:pack`) を作成するコマンドは、`dotnet pack` と同等の機能です。

> [!IMPORTANT]
> このトピックは、[SDK スタイル](../resources/check-project-format.md)のプロジェクト (通常は、.NET Core プロジェクトと .NET Standard プロジェクト)、および PackageReference を使った SDK スタイル以外のプロジェクトを対象としています。

## <a name="set-properties"></a>プロパティの設定

次のプロパティは、パッケージを作成するために必要です。

- `PackageId`、パッケージの識別子。パッケージをホストするギャラリー全体で一意にする必要があります。 指定しない場合は、既定値の `AssemblyName` が使用されます。
- `Version`、*Major.Minor.Patch[-Suffix]* という形式の特別なバージョン番号。 *-Suffix* によって[プレリリース版](prerelease-packages.md)を識別します。 指定しない場合は、既定値は 1.0.0 です。
- ホスト (nuget.org など) に表示されるパッケージ タイトル。
- `Authors`、作成者と所有者の情報。 指定しない場合は、既定値の `AssemblyName` が使用されます。
- `Company`、会社名。 指定しない場合は、既定値の `AssemblyName` が使用されます。

Visual Studio では、プロジェクトのプロパティにこれらの値を設定できます (ソリューション エクスプローラー内でプロジェクトを右クリックし、 **[プロパティ]** を選択して、 **[パッケージ]** タブを選択します)。 プロジェクト ファイル ( *.csproj*) 内でこれらのプロパティを直接設定することもできます。

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> パッケージには、nuget.org または使用しているパッケージ ソース全体で一意になる識別子を付けてください。

次の例は、これらのプロパティを含む、シンプルかつ完全なプロジェクト ファイルを示しています。

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

また、[MSBuild pack ターゲット](../reference/msbuild-targets.md#pack-target)に関するセクション、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」、「[NuGet メタデータ プロパティ](/dotnet/core/tools/csproj#nuget-metadata-properties)」に説明されているように、`Title`、`PackageDescription`、`PackageTags` などのオプションのプロパティを設定することもできます。

> [!NOTE]
> 公開用にビルドされたパッケージの場合は、**PackageTags**プロパティに特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。

依存関係の宣言とバージョン番号の指定の詳細については、「[プロジェクト ファイルのパッケージ参照 (PackageReference)](../consume-packages/package-references-in-project-files.md)」と「[パッケージのバージョン管理](../concepts/package-versioning.md)」を参照してください。 `<IncludeAssets>` および `<ExcludeAssets>` 属性を使用して、パッケージ内で直接、依存関係からアセットを表面化させることもできます。 詳しくは、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」をご覧ください。

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>一意のパッケージ識別子を選択してバージョン番号を設定する

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>NuGet.Build.Tasks.Pack パッケージを追加する

SDK スタイル以外のプロジェクトと PackageReference で MSBuild を使用している場合は、プロジェクトに NuGet.Build.Tasks.Pack パッケージを追加します。

1. プロジェクト ファイルを開き、以下を `<PropertyGroup>` 要素の後に追加します。

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. 開発者コマンド プロンプトを開きます (**検索**ボックスに「**開発者コマンド プロンプト**」と入力します)。

   MSBuild に必要なすべてのパスが構成されるため、通常は **[スタート]** メニューから Visual Studio 用開発者コマンド プロンプトを使用します。

3. プロジェクト ファイルが含まれているフォルダーに切り替え、次のコマンドを入力して、NuGet.Build.Tasks.Pack パッケージをインストールします。

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   MSBuild の出力にビルドが正常に完了したことが示されていることを確認します。

## <a name="run-the-msbuild--tpack-command"></a>msbuild -t:pack コマンドを実行する

プロジェクトから NuGet パッケージ (`.nupkg` ファイル) を作成するには、`msbuild -t:pack` コマンドを実行します。このコマンドではプロジェクトのビルドも自動的に行われます。

Visual Studio 用開発者コマンド プロンプトで次のコマンドを入力します。

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

出力に、`.nupkg` ファイルへのパスが表示されます。

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>ビルド時に自動的にパッケージを生成する

プロジェクトのビルドまたは復元時に自動的に `msbuild -t:pack` を実行させるには、プロジェクト ファイルの `<PropertyGroup>` 内に次の行を追加します。

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

ソリューション上で `msbuild -t:pack` を実行した場合、これにより、パック化可能なソリューション内のすべてのプロジェクトがパックされます ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) プロパティは `true` に設定されます)。

> [!NOTE]
> パッケージを自動的に生成する場合、パックする時間によってプロジェクトのビルド時間が長くなります。

### <a name="test-package-installation"></a>パッケージ インストールのテスト

パッケージを公開する前に、通常、パッケージをプロジェクトにインストールするプロセスをテストします。 このテストにより、必要なファイルがすべて、プロジェクト内の適切な場所に入ります。

インストールは Visual Studio またはコマンド ラインで手動テストできます。通常の[パッケージ インストール手順](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)を利用します。

> [!IMPORTANT]
> パッケージは不変です。 問題を修正する場合は、パッケージ内容を変更して、もう一度パックしてください。再テスト時に、[グローバル パッケージのフォルダーをクリアする](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)までは、古いバージョンのパッケージを引き続き使用することになります。 どのビルド時でも、一意のプレリリース ラベルを使用しないパッケージをテストする場合に、これは特に該当します。

## <a name="next-steps"></a>次の手順

`.nupkg` ファイルとなるパッケージを作成したら、「[パッケージの公開](../nuget-org/publish-a-package.md)」の説明にあるように、選択したギャラリーにパッケージを公開できます。

パッケージの機能を拡張したり、次のトピックで説明するように、その他の方法で他のシナリオをサポートしたりすると便利な場合があります。

- [MSBuild ターゲットとしての NuGet の pack と restore](../reference/msbuild-targets.md)
- [パッケージのバージョン管理](../concepts/package-versioning.md)
- [複数のターゲット フレームワークのサポート](../create-packages/multiple-target-frameworks-project-file.md)
- [ソース ファイルと構成ファイルの変換](../create-packages/source-and-config-file-transformations.md)
- [ローカリゼーション](../create-packages/creating-localized-packages.md)
- [プレリリース バージョン](../create-packages/prerelease-packages.md)
- [パッケージの種類の設定](../create-packages/set-package-type.md)
- [COM 相互運用アセンブリを含むパッケージを作成する](../create-packages/author-packages-with-COM-interop-assemblies.md)

最後になりますが、次のような種類のパッケージもあります。

- [ネイティブ パッケージ](../guides/native-packages.md)
- [シンボル パッケージ](../create-packages/symbol-packages.md)
