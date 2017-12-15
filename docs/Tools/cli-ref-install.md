---
title: "NuGet CLI コマンドをインストールする |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Nuget.exe-install コマンドのリファレンス"
keywords: "nuget の参照をパッケージのコマンドをインストールします。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a>コマンド (NuGet CLI) をインストールします。

**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:**すべて

ダウンロードし、指定したパッケージ ソースを使用して、現在のフォルダーには、既定のプロジェクトにパッケージをインストールします。

> [!Tip]
> プロジェクトのコンテキスト外で直接パッケージをダウンロードするには、ページにアクセスして、パッケージの[nuget.org](https://www.nuget.org)を選択し、**ダウンロード**リンクします。 

ソースが指定されていない場合、グローバル構成ファイルに一覧表示`%APPDATA%\NuGet\NuGet.Config`、使用されます。 参照してください[NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)さらに詳細です。

特定のパッケージが指定されていない場合`install`プロジェクトの表示されているすべてのパッケージをインストール`packages.config`ようなファイル[ `restore`](#restore)です。 (、`install`コマンドでは機能しません`project.json`)。

`install`コマンドは、プロジェクト ファイルを変更していないまたは`packages.config`; に似ていますが、この方法で`restore`のみにパッケージをディスクに追加、プロジェクトの依存関係を変更することはできません。

依存関係を追加するか、Visual Studio で、パッケージ マネージャー UI またはコンソール経由で、プロジェクトを追加または変更`packages.config`いずれかを実行および`install`または`restore`です。 使用してプロジェクトの`project.json`、そのファイルを変更して実行し、`restore`です。

## <a name="usage"></a>使用方法

```
nuget install <packageID | configFilePath> [options]
```

ここで`<packageID>`(最新バージョンを使用) をインストールするパッケージの名前または`<configFilePath>`を識別、`packages.config`ファイルをインストールするパッケージを一覧表示します。 特定のバージョンを指定することができます、`-Version`オプション。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | *(2.5 +)* NuGet 構成ファイルを適用します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| DisableParallelProcessing | 複数のパッケージを並列でインストールを無効にします。 |
| ExcludeVersion | パッケージ名のみとバージョン番号ではないという名前のフォルダーにパッケージをインストールします。 |
| FallbackSource | *(3.2 +)*プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| フレームワーク | *(4.4 +)*ターゲット フレームワークの依存関係を選択するために使用します。 'Any' に指定されていない場合の既定値です。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NoCache | NuGet がローカル コンピューターのキャッシュからパッケージを使用するを防ぎます。 |
| 非対話型 | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| OutputDirectory | パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 |
| PackageSaveMode | パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`です。 |
| プレリリース版 | インストールするプレリリースのパッケージを使用できます。 このフラグは、使用してパッケージを復元するときに必要ありません`packages.config`です。 |
| RequireConsent | ダウンロードして、パッケージをインストールする前にパッケージを復元が有効になっていることを確認します。 詳細については、「[パッケージの復元](../consume-packages/package-restore.md)です。 |
| SolutionDirectory | パッケージを復元するためのソリューションのルート フォルダーを指定します。 |
| ソース | (Url) として使用するパッケージ ソースの一覧を指定します。 コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../Consume-Packages/Configuring-NuGet-Behavior.md)です。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。 |
| Version | インストールするパッケージのバージョンを指定します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>例

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
