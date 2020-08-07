---
title: dotnet CLI を使用して NuGet パッケージを作成する
description: NuGet パッケージを設計し、作成する過程を詳しく説明します。ファイルやバージョン管理など、重要な決定ポイントが含まれます。
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 2fcba9dd6bbc7ff4e9b5b8b57250c399f59a1c5e
ms.sourcegitcommit: e02482e15c0cef63153086ed50d14f5b2a38f598
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473845"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>dotnet CLI を使用して NuGet パッケージを作成する

パッケージの動作やそれに含まれているコードに関係なく、CLI ツールのいずれか (`nuget.exe` または `dotnet.exe`) を使用して、他の開発者が何人でも共有して使用できるコンポーネントにその機能をパッケージ化できます。 この記事では、dotnet CLI を使用してパッケージを作成する方法について説明します。 `dotnet` CLI をインストールするには、「[NuGet クライアント ツールのインストール](../install-nuget-client-tools.md)」をご覧ください。 Visual Studio 2017 以降では、dotnet CLI は .NET Core ワークロードに含まれています。

[SDK スタイルの形式](../resources/check-project-format.md)を使用する .NET Core および .NET Standard プロジェクト、またその他の SDK スタイルのあらゆるプロジェクトに対して、NuGet ではプロジェクト ファイルにある情報を直接使ってパッケージが作成されます。 ステップ バイ ステップのチュートリアルについては、「[.NET Standard パッケージの作成 (dotnet CLI)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)」または「[.NET Standard パッケージの作成 (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio.md)」を参照してください。

`msbuild -t:pack` は、`dotnet pack` と同等の機能です。 MSBuild を使用してビルドするには、「[NuGet パッケージの作成 (MSBuild)](creating-a-package-msbuild.md)」を参照してください。

> [!IMPORTANT]
> このトピックは、[SDK スタイル](../resources/check-project-format.md)のプロジェクト (通常は .NET Core および .NET Standard プロジェクト) に適用されます。

## <a name="set-properties"></a>プロパティの設定

次のプロパティは、パッケージを作成するために必要です。

- `PackageId`、パッケージの識別子。パッケージをホストするギャラリー全体で一意にする必要があります。 指定しない場合は、既定値の `AssemblyName` が使用されます。
- `Version`、*Major.Minor.Patch[-Suffix]* という形式の特別なバージョン番号。 *-Suffix* によって[プレリリース版](prerelease-packages.md)を識別します。 指定しない場合は、既定値は 1.0.0 です。
- ホスト (nuget.org など) に表示されるパッケージ タイトル。
- `Authors`、作成者と所有者の情報。 指定しない場合は、既定値の `AssemblyName` が使用されます。
- `Company`、会社名。 指定しない場合は、既定値の `AssemblyName` が使用されます。

Visual Studio では、プロジェクトのプロパティにこれらの値を設定できます (ソリューション エクスプローラー内でプロジェクトを右クリックし、 **[プロパティ]** を選択して、 **[パッケージ]** タブを選択します)。 プロジェクト ファイル (`.csproj`) 内でこれらのプロパティを直接設定することもできます。

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> パッケージには、nuget.org または使用しているパッケージ ソース全体で一意になる識別子を付けてください。

次の例は、これらのプロパティを含む、シンプルかつ完全なプロジェクト ファイルを示しています。 (`dotnet new classlib` コマンドを使用して、新しい既定のプロジェクトを作成できます)。

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
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

## <a name="add-an-optional-description-field"></a>省略可能な説明フィールドを追加する

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>一意のパッケージ識別子を選択してバージョン番号を設定する

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>pack コマンドを実行する

プロジェクトから NuGet パッケージ (`.nupkg` ファイル) を作成するには、`dotnet pack` コマンドを実行します。このコマンドではプロジェクトのビルドも自動的に行われます。

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

出力に、`.nupkg` ファイルへのパスが表示されます。

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>ビルド時に自動的にパッケージを生成する

`dotnet build` の実行時に自動的に `dotnet pack` を実行させるには、プロジェクト ファイルの `<PropertyGroup>` 内に次の行を追加します。

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

ソリューション上で `dotnet pack` を実行した場合、これにより、パック化可能なソリューション内のすべてのプロジェクトがパックされます ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) プロパティは `true` に設定されます)。

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

- [パッケージのバージョン管理](../concepts/package-versioning.md)
- [複数のターゲット フレームワークのサポート](../create-packages/multiple-target-frameworks-project-file.md)
- [パッケージ アイコンの追加](../reference/nuspec.md#icon)
- [ソース ファイルと構成ファイルの変換](../create-packages/source-and-config-file-transformations.md)
- [ローカリゼーション](../create-packages/creating-localized-packages.md)
- [プレリリース バージョン](../create-packages/prerelease-packages.md)
- [パッケージの種類の設定](../create-packages/set-package-type.md)
- [COM 相互運用アセンブリを含むパッケージを作成する](../create-packages/author-packages-with-COM-interop-assemblies.md)

最後になりますが、次のような種類のパッケージもあります。

- [ネイティブ パッケージ](../guides/native-packages.md)
- [シンボル パッケージ](../create-packages/symbol-packages-snupkg.md)
