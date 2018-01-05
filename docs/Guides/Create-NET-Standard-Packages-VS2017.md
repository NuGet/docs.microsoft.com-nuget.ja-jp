---
title: "Visual Studio 2017 での .NET Standard 2.0 NuGet パッケージの作成 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "NuGet 4.x と Visual Studio 2017 を使用して、.NET Standard 2.0 NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。"
keywords: "パッケージを作成する, .NET Standard パッケージ, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Visual Studio 2017 での .NET Standard 2.0 パッケージの作成

*Visual Studio 2017 Update 3 で提供される NuGet 4.x 以降および MSBuild 15.3 以降に適用されます。Visual Studio 2017 の以前のバージョンについては、これらの手順は \<TargetFramework\> プロパティを変更した .NET Standard 1.4 から 1.6 に当てはまります。NuGet 3.x 以降を使用して作業を行う場合は、「[Visual Studio 2015 での .NET Standard パッケージの作成](../guides/create-net-standard-packages-vs2015.md)」も参照してください。*

[.NET Standard ライブラリ](https://docs.microsoft.com/dotnet/articles/standard/library)は、すべての .NET ランタイムで使用できるようにすることを目的とした .NET API の正式な仕様です。したがって、.NET エコシステムでより高い統一性が確立されます。 .NET Standard Library は、ワークロードに関係なく、すべての .NET プラットフォーム用に統一された BCL (基本クラス ライブラリ) API のセットを定義して実装します。 これにより、開発者はすべての .NET ランタイム間で使用可能な PCL を生成でき、共有コードでプラットフォーム固有の条件付きコンパイル ディレクティブを除去するまでとはいかないまでも減らすことはできます。

このガイドでは、Visual Studio 2017 Update 3 と NuGet 4.0 を使用した .NET Standard Library 2.0 をターゲットとする nuget パッケージの作成について説明します。

1. [前提条件](#pre-requisites)
1. [クラス ライブラリ プロジェクトを作成する](#create-the-netstandard-class-library-project)
1. [.csproj ファイル内のメタデータを編集する](#edit-metadata-in-the-csproj-file)
1. [コンポーネントをパッケージ化する](#package-the-component)
1. [関連トピック](#related-topics)

## <a name="pre-requisites"></a>前提条件

このチュートリアルでは、Visual Studio 2017 Update 3 と **.NET Core クロスプラットフォーム開発**ワークロードが必要です。 [visualstudio.com](https://www.visualstudio.com/) から無料の Community Edition をインストールします。Professional Edition と Enterprise Edition も使用できます。

Visual Studio のインストーラーで、必要なワークロードは次のように表示されます。

![Visual Studio インストーラーの [.NET Core クロスプラット フォーム開発] ワークロード](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>.NET Standard クラス ライブラリ プロジェクトの作成

1. Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に移動し、**[Visual C#]、[.NET Standard]** ノードの順に展開して、**[Class Library (Net Standard)]\(クラス ライブラリ (.Net Standard)\)** を選択し、名前を AppLogger に変更してから [OK] をクリックします。

    ![新しいクラス ライブラリ プロジェクトを作成する](media/NuGet4-02-NewProject.png)

1. ビルド構成を **[リリース]** に変更します。
1. ソリューション エクスプローラーで `AppLogger` プロジェクトを右クリックし、**[プロパティ]** を選択し、**[ビルド]** タブを選択し、**[XML ドキュメント ファイル]** のチェック ボックスをオンにし、ファイル名を単に `AppLogger.xml` に設定します。 次いでプロジェクトを保存します。

1. 次のように、コンポーネントにコードを追加します (ここではコンソールにメッセージが明確に出力されるのみです)。

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. プロジェクト (Release 構成の) をビルドし、DLL および XML ファイルが `bin\Release\netstandard2.0` フォルダー内に生成されていることを確認します。

## <a name="edit-metadata-in-the-csproj-file"></a>.csproj ファイルでメタデータを編集する

NuGet 4.0 と .NET Core のプロジェクトでは、パッケージのメタデータは、`.nuspec` などの外部ファイルではなく `.csproj` ファイルに直接含まれます。 そのメタデータの完全な説明については、「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target)」 (NuGet パックと MSBuild のターゲットとしての復元) を参照してください。

1. ソリューション エクスプローラーでプロジェクトを右クリックし、**[Edit AppLogger.csproj]\(AppLogger.csproj の編集\)** を選択し、最初のプロパティ グループを編集して次のようにパッケージ情報が含まれるようにします。

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. プロジェクトを保存し、ソリューションを右クリックし、**[ソリューションのビルド]** を選択し、パッケージのすべてのファイルをここでは正しいメタデータで生成します。


## <a name="package-the-component"></a>コンポーネントをパッケージ化する

NuGet 4.0 は、前のセクションで追加したように、プロジェクトに必要なパッケージ メタデータが含まれる場合、MSBuild バージョン 15.1 以降を使用したパック ターゲット (Visual Studio 2017 Update 3 の一部として MSBuild 15.3 を含む) をサポートします。 この方法で MSBuild を呼び出すには、`.csproj` ファイルと同じフォルダーに、コマンド ラインで単純にパック ターゲットを指定します。

    msbuild /t:pack /p:Configuration=Release

コンテンツ ファイル、シンボル、ソース コードなどを含める `msbuild /t:pack` のその他のオプションについては、「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target)」 (NuGet パックと MSBuild のターゲットとしての復元) を参照してください。

いずれの場合も、上記のコマンドは、その構成をビルドする際に、既定で `bin\Release` フォルダーに `AppLogger.YOUR_NAME.1.0.0.nupkg` が生成されます。 `/p` スイッチを省略した場合、既定の構成は `Debug` になります。 

[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。

![AppLogger パッケージが表示された NuGet パッケージ エクスプローラー](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> `.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。 したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。

パッケージを他の開発者が使用できるようにする場合は、「[パッケージの公開](../create-packages/publish-a-package.md)」の手順に従ってください。

## <a name="related-topics"></a>関連トピック

- 「[Package References in Project Files](../consume-packages/package-references-in-project-files.md)」 (プロジェクト ファイル内のパッケージ参照) では、プロジェクト ファイルに直接パッケージを記述する場合の詳細がすべて説明されています。
- 「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md)」 (NuGet パックと MSBuild のターゲットとしての復元) では、パッケージを作成するために `msbuild /t:pack` を使用するすべてのオプションが説明されています。
- [.NET Standard ライブラリのドキュメント](https://docs.microsoft.com/dotnet/articles/standard/library)
- [.NET Framework から .NET Core への移植](https://docs.microsoft.com/dotnet/articles/core/porting/index)
