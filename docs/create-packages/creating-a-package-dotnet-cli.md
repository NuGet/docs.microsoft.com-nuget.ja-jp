---
title: dotnet CLI を使用して NuGet パッケージを作成する
description: NuGet パッケージを設計し、作成する過程を詳しく説明します。ファイルやバージョン管理など、重要な決定ポイントが含まれます。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: da5dbc8b1659cef66e8439b9a3c3bb2c9205cbe6
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462464"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>dotnet CLI を使用して NuGet パッケージを作成する

パッケージの動作やそれに含まれているコードに関係なく、CLI ツールのいずれか (`nuget.exe` または `dotnet.exe`) を使用して、他の開発者が何人でも共有して使用できるコンポーネントにその機能をパッケージ化できます。 この記事では、dotnet CLI を使用してパッケージを作成する方法について説明します。 `dotnet` CLI をインストールするには、「[NuGet クライアント ツールのインストール](../install-nuget-client-tools.md)」をご覧ください。 Visual Studio 2017 以降では、dotnet CLI は .NET Core ワークロードに含まれています。

[SDK スタイルの形式](../resources/check-project-format.md)を使用する .NET Core および .NET Standard プロジェクト、またその他の SDK スタイルのあらゆるプロジェクトに対して、NuGet ではプロジェクト ファイルにある情報を直接使ってパッケージが作成されます。 ステップバイステップのチュートリアルについては、[dotnet CLI を使用した .NET Standard パッケージの作成](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)に関するページ、[Visual Studio を使用した .NET Standard パッケージの作成](../quickstart/create-and-publish-a-package-using-visual-studio.md)に関するページをご覧ください。

`msbuild -t:pack` は、`dotnet pack` と同等の機能です。 MSBuild を使用してビルドする場合、その概念はこの記事の説明と同じですが、コマンド ラインのコマンドが少し異なります。 同様に、非 SDK スタイルのプロジェクトおよび `<PackageReference>` では、`msbuild /t:pack` を使用できます。 これらのシナリオでは、依存関係に NuGet.Build.Tasks.Pack パッケージを追加する必要があります。 「[MSBuild ターゲットとしての NuGet の pack と restore](../reference/msbuild-targets.md)」をご覧ください。

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
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> パッケージには、nuget.org または使用しているパッケージ ソース全体で一意になる識別子を付けてください。

また、[MSBuild pack ターゲット](../reference/msbuild-targets.md#pack-target)に関するセクション、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」、「[NuGet メタデータ プロパティ](/dotnet/core/tools/csproj#nuget-metadata-properties)」に説明されているように、`Title`、`PackageDescription`、`PackageTags` などのオプションのプロパティを設定することもできます。

> [!NOTE]
> 公開用にビルドされたパッケージの場合は、**PackageTags**プロパティに特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。

依存関係の宣言とバージョン番号の指定については、「[パッケージのバージョン管理](../reference/package-versioning.md)」を参照してください。 `<IncludeAssets>` および `<ExcludeAssets>` 属性を使用して、パッケージ内で直接、依存関係からアセットを表面化させることもできます。 詳しくは、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」をご覧ください。

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>一意のパッケージ識別子を選択してバージョン番号を設定する

パッケージ識別子とバージョン番号は、パッケージに含まれる正確なコードを一意に識別するため、プロジェクトの中で最も重要な 2 つの値です。

**パッケージ識別子のベスト プラクティス:**

- **一意性**:この識別子は、nuget.org 全体で、あるいはパッケージをホストするギャラリー全体で一意になる必要があります。 識別子を決める前に、該当するギャラリーを検索し、その名前が既に使用されていないか確認してください。 競合を避けるために、`Contoso.` のように、識別子の最初の部分に会社の名前を使用することが適しているパターンです。
- **名前空間のような名前**:.NET の名前空間に似たパターンに従います。ハイフンの代わりにドット表記を使います。 たとえば、`Contoso-Utility-UsefulStuff` や `Contoso_Utility_UsefulStuff` ではなく `Contoso.Utility.UsefulStuff` を使用します。 パッケージ識別子がコードで使用される名前空間と一致すれば、利用者にとっても便利です。
- **サンプル パッケージ**:別のパッケージの使用方法を示すサンプル コードのパッケージを生成する場合、`Contoso.Utility.UsefulStuff.Sample` のように、識別子にサフィックスとして `.Sample` を付けます。 (サンプル パッケージは、もちろん、他のパッケージに依存します。)サンプル パッケージを作成する場合は、`<IncludeAssets>` 内で `contentFiles` 値を使用します。 `content` フォルダーで、`\Samples\Contoso.Utility.UsefulStuff.Sample` のように、`\Samples\<identifier>` という名前のフォルダーにサンプル コードを配置します。

**パッケージ バージョンのベスト プラクティス:**

- これは厳密には必須ではありませんが、一般的にはプロジェクト (またはアセンブリ) と一致するようにパッケージのバージョンを設定します。 パッケージを単一のアセンブリに限定する場合に、これはシンプルな方法です。 概して、NuGet 自体は依存関係の解決時、パッケージ バージョンを使います。アセンブリ バージョンではありません。
- 非標準のバージョン スキーマを使用するとき、「[パッケージのバージョン管理](../reference/package-versioning.md)」で説明するように、NuGet バージョン管理ルールを検討してください。 NuGet は、ほぼ [semver 2 に準拠](../reference/package-versioning.md#semantic-versioning-200)しています。

> 依存関係の解決については、「[PackageReference による依存関係の解決](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)」をご覧ください。 バージョン管理の理解を深めるためにも役立つ可能性がある旧情報については、こちらの一連のブログ投稿を確認してください。
>
> - [第 1 部: DLL 地獄](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [第 2 部: コア アルゴリズム](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [第 3 部:バインド リダイレクトによる統合](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="run-the-pack-command"></a>pack コマンドを実行する

プロジェクトから NuGet パッケージ (`.nupkg` ファイル) を作成するには、`dotnet pack` コマンドを実行します。このコマンドではプロジェクトのビルドも自動的に行われます。

```cli
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

- [パッケージのバージョン管理](../reference/package-versioning.md)
- [複数のターゲット フレームワークのサポート](../create-packages/multiple-target-frameworks-project-file.md)
- [ソース ファイルと構成ファイルの変換](../create-packages/source-and-config-file-transformations.md)
- [ローカリゼーション](../create-packages/creating-localized-packages.md)
- [プレリリース バージョン](../create-packages/prerelease-packages.md)
- [パッケージの種類の設定](../create-packages/set-package-type.md)
- [COM 相互運用アセンブリを含むパッケージを作成する](../create-packages/author-packages-with-COM-interop-assemblies.md)

最後になりますが、次のような種類のパッケージもあります。

- [ネイティブ パッケージ](../create-packages/native-packages.md)
- [シンボル パッケージ](../create-packages/symbol-packages.md)
