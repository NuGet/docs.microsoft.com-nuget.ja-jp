---
title: NuGet project.json のアーカイブ コンテンツ | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet のドキュメントの他の分野から削除された project.json のその他のコンテンツ。
keywords: NuGet project.json ファイル
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 16361fe16d8ecc7064af4b6d636435a31a5663dc
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-archive"></a>project.json のアーカイブ

`project.json` 管理形式は、NuGet 3.x で導入され、特定のプロジェクトの種類に使用されていました。 これは、PackageReference 形式の導入に伴い、使用されなくなりました。PackageReference 形式では、依存関係のリストがプロジェクト ファイルに直接格納されます。

関連項目:

- [project.json のスキーマ](project-json.md)
- [パッケージ作成者に対する project.json の影響](project-json-impact.md)
- [project.json および UWP](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>project.json の管理形式

*"もともとは「[パッケージの復元](../what-is-nuget.md)」内。"*

管理形式の一覧には次が含まれます。

- [`project.json`](project-json.md): *(使用されていない)* プロジェクトの依存関係のリストを保持する JSON ファイルです。全体的なパッケージ グラフは関連ファイル `project.lock.json` に含まれます。 PackageReference が優先され、この形式は使用されていません。

## <a name="nuget-restore-on-mono"></a>Mono での NuGet の復元

*"もともとは「[NuGet クライアント ツールのインストール](../install-nuget-client-tools.md)」内。"*

`project.json` で機能します。

## <a name="constraining-package-versions-with-restore"></a>復元でのパッケージのバージョンの制約

*"もともとは「[パッケージの復元](../consume-packages/package-restore.md#constraining-package-versions-with-restore)」内。"*

- `project.json`: 依存関係のバージョン番号でバージョンの範囲を直接指定します。 例:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>NuGet CLI コマンド

- `project.json`では、`nuget install` は機能しません。
- `nuget restore`: `project.json`を使用するプロジェクトでは、必要に応じて、`project.lock.json` ファイルと `<project>.nuget.props` ファイルを生成します。 (どちらのファイルもソース管理から省略できます)。`<projectPath>` 引数は、`project.json` ファイルを指示することができ、`packages.config` またはプロジェクト ファイルを指示する場合同様に動作します。 パッケージ フォルダーの優先順位では、`project.json` を使用する場合、`%userprofile%\.nuget\packages` が最初に検索されます。
- `nuget update`: Mono の場合、このコマンドは、`project.json` を使用するプロジェクトで機能しません。

## <a name="dependency-resolution-with-packagereference"></a>PackageReference による依存関係の解決

*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)」内。"*

PackageReference の動作は、`project.json` にも適用されます。 nuget restore は、依存関係グラフを、`project.json` と同時に `project.lock.json`にも書き込みます。

## <a name="managing-dependency-assets"></a>依存関係アセットの管理

*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#managing-dependency-assets)」内。"*

`project.json` 形式を使用すると、依存関係から最上位のプロジェクトへの資産のフローを制御できます。 詳細については、「[project.json](project-json.md)」を参照してください。

## <a name="excluding-references"></a>参照の除外

*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#excluding-references)」内。"*

- `project.json`: パッケージ C の依存関係に `"exclude" : "all"` を追加します。

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>互換性のないパッケージのエラーの解決

*"もともとは「[依存関係の解決](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors)」内。"*

エラーを解決するための追加手段:

- **お勧めしません**: パッケージ作成者と作業するときの一時的な解決策として、`netcore`、`netstandard`、および `netcoreapp` を対象とするプロジェクトでは、他のフレームワークを互換性があるものとして指定し、これらの他のフレームワークを対象とするパッケージを使うことができます。 [project.json のインポート](project-json.md#imports)に関するページおよび [MSBuild 復元ターゲットの PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback) に関するページをご覧ください。 この方法では予期しない動作が発生する可能性があるので、繰り返しますが、パッケージ作成者との共同作業または更新によってパッケージの非互換性を解決することをお勧めします。

## <a name="target-frameworks"></a>ターゲット フレームワーク

*"もともとは「[ターゲット フレームワーク](../reference/target-frameworks.md)」内。"*

- [project.json](project-json.md): `frameworks` ノードで、プロジェクトをコンパイルできるフレームワークのバージョンを指定します。

## <a name="creating-a-package"></a>パッケージの作成

*"もともとは「[パッケージの作成](../create-packages/creating-a-package.md)」内"*

### <a name="setting-a-package-type"></a>パッケージの種類の設定

.NET Core 1.x では、DotnetCliTool パッケージがインストールされると、Visual Studio により、`dependencies` ノードではなく、`project.json` `tools` ノードに格納されます。

パッケージの種類は `project.json` で設定されます。

- `project.json`: `packOptions.packageType` プロパティ json 内のパッケージの種類を示します。

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>MSBuild のターゲットとプロパティの追加

*"もともとは「[Visual Studio 2015 での .NET Standard NuGet パッケージの作成](../guides/create-net-standard-packages-vs2015.md)」内。"*

`project.json` を使用する場合、ターゲットはプロジェクトに追加されませんが、`project.lock.json` を通じて使用できます。

### <a name="package-versioning"></a>パッケージのバージョン管理

*"もともとは「[パッケージのバージョン管理](../reference/package-versioning.md)」内。"*

`project.json`形式を使用する場合、NuGet では、メジャー、マイナー、パッチ、およびプレリリースを示す、番号のサフィックス部分にワイルドカード表記 \*を使用できます。

### <a name="nugetconfig-reference"></a>NuGet.Config 参照

*"もともとは「[NuGet.Config 参照](../reference/nuget-config-file.md)」内。"*

`globalPackagesFolder` は、`project.json` にのみ適用されます。 (追加情報: PackageReference にも適用されます。)

### <a name="nuspec-file-reference"></a>nuspec ファイル参照

*"もともとは「[nuspec リファレンス](../reference/nuspec.md)」内。"*

`<contentFiles>` 要素は、`project.json` で `<files>` の代わりに使用されます。

### <a name="package-manager-options-control"></a>パッケージ マネージャーのオプションの制御

*もともとは「[パッケージ マネージャー UI リファレンス](../tools/package-manager-ui.md)」内。*

`project.json` 管理形式を使用するプロジェクトでは、**[プレビュー ウィンドウを表示する]** オプションのみが表示されます。

### <a name="visual-studio-templates"></a>Visual Studio テンプレート

*"もともとは「[Visual Studio テンプレートの NuGet パッケージ](../visual-studio-extensibility/visual-studio-templates.md)」内。"*

ベスト プラクティス: テンプレートに、`project.json` ファイルは含まれません。また、NuGet パッケージがインストールされるときに追加される参照やコンテンツも含まれません。