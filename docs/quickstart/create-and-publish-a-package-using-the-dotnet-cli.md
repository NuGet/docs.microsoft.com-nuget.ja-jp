---
title: dotnet CLI を使用した NuGet パッケージの作成と公開
description: .NET Core CLI (dotnet) を使用した NuGet パッケージの作成と公開に関するチュートリアル。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 4e96d9969c8b4570ee69501d6529986f891ea4dc
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842602"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>クイック スタート: パッケージの作成と公開 (dotnet CLI)

これは、`dotnet`コマンド ライン インターフェイス (CLI) を使用して、.NET クラス ライブラリから NuGet パッケージを作成し、nuget.org に公開する簡単なプロセスです。

## <a name="prerequisites"></a>必須コンポーネント

1. `dotnet` CLI を含む [.NET Core SDK](https://www.microsoft.com/net/download/) をインストールします。 Visual Studio 2017 以降、dotnet CLI は .NET Core 関連のワークロードで自動的にインストールされます。

1. まだ持っていない場合は、[nuget.org で無料アカウントを登録](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)します。 新しいアカウントを作成すると、確認メールが送信されます。 パッケージをアップロードするには、その前にアカウントを確認する必要があります。

## <a name="create-a-class-library-project"></a>クラス ライブラリ プロジェクトを作成する

パッケージ化するコードに既存の .NET クラス ライブラリ プロジェクトを使用することも、次の手順に従って単純なプロジェクトを作成することもできます。

1. `AppLogger`という名前のフォルダーを作成し、そこに変更します。

1. `dotnet new classlib`を使用してプロジェクトを作成します。プロジェクト名には現在のフォルダーの名前が使用されます。

## <a name="add-package-metadata-to-the-project-file"></a>パッケージのメタデータをプロジェクト ファイルに追加する

すべての NuGet パッケージには、その内容と依存関係を説明するマニフェストが必要です。 最終的なパッケージでは、マニフェストは、プロジェクト ファイルに含まれる NuGet メタデータのプロパティから生成される `.nuspec` ファイルです。

1. プロジェクト ファイル (`.csproj`) を開いて、既存の `<PropertyGroup>` タグ内に次の最小限のプロパティを追加し、必要に応じて値を変更します。

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > パッケージに、nuget.org または使用しているホスト全体で一意の識別子を付けます。 このチュートリアルでは、以降の公開手順でパッケージを一般公開するので (ただし、誰かが実際に使用する可能性はありません)、名前に "Sample" または "Test" を含めることをお勧めします。

1. 「[NuGet メタデータ プロパティ](/dotnet/core/tools/csproj#nuget-metadata-properties)」で説明する省略可能なプロパティを追加します。

    > [!Note]
    > 公開用にビルドされたパッケージの場合は、**PackageTags**プロパティに特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。

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

## <a name="publish-the-package"></a>パッケージを公開する

`.nupkg` ファイルを作成したら、`dotnet nuget push` コマンドと、nuget.org から取得した API キーを使用して、そのファイルを nuget.org に公開します。

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API キーを取得する

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>dotnet nuget push を使用して公開する

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>公開エラー

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>公開済みパッケージを管理する

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>関連トピック

- [パッケージの作成](../create-packages/creating-a-package.md)
- [パッケージの公開](../nuget-org/publish-a-package.md)
- [プレリリース パッケージ](../create-packages/Prerelease-Packages.md)
- [複数のターゲット フレームワークのサポート](../create-packages/supporting-multiple-target-frameworks.md)
- [パッケージのバージョン管理](../reference/package-versioning.md)
- [ローカライズされたパッケージを作成する](../create-packages/creating-localized-packages.md)
- [シンボル パッケージを作成する](../create-packages/symbol-packages-snupkg.md)
- [署名パッケージ](../create-packages/Sign-a-package.md)
