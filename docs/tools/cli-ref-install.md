---
title: NuGet CLI のインストール コマンド
description: Nuget.exe install コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8261cdb83af72d9d9379124f4c446c7cd2a50299
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549137"
---
# <a name="install-command-nuget-cli"></a>Install コマンド (NuGet CLI)

**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン:** すべて

ダウンロードし、既定では、現在のフォルダーを指定したパッケージ ソースを使用して、プロジェクトにパッケージをインストールします。

> [!Tip]
> プロジェクトのコンテキスト外で直接パッケージをダウンロードするには、パッケージのページを参照してください。 [nuget.org](https://www.nuget.org)を選択し、**ダウンロード**リンク。

ソースが指定されていない場合、グローバル構成ファイルに一覧表示`%appdata%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) 使用されます。 参照してください[NuGet の構成の動作を](../consume-packages/configuring-nuget-behavior.md)詳細。

特定のパッケージが指定されていない場合`install`プロジェクトの一覧にあるすべてのパッケージをインストール`packages.config`ようなファイル[ `restore`](cli-ref-restore.md)します。

`install`コマンドでは、プロジェクト ファイルは変更しませんまたは`packages.config`; に似ていますが、この方法で`restore`のみにパッケージをディスクに追加しますが、プロジェクトの依存関係を変更することはできません。

依存関係を追加するか、Visual Studio でパッケージ マネージャー UI またはコンソールを使用してパッケージを追加または変更`packages.config`いずれかを実行および`install`または`restore`します。

## <a name="usage"></a>使用法

```cli
nuget install <packageID | configFilePath> [options]
```

場所`<packageID>`(最新バージョンを使用) をインストールするパッケージの名前または`<configFilePath>`を識別、`packages.config`ファイルをインストールするパッケージを一覧表示します。 特定のバージョンを示すことができます、`-Version`オプション。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| DependencyVersion | *(4.4 以降)* 次のいずれかの値を使用する依存関係パッケージのバージョン。<br/><ul><li>*最も低い*(既定値): 最小バージョン</li><li>*HighestPatch*: 最高レベルの最も大きなを最低軽微な修正プログラムのバージョン</li><li>*HighestMinor*: 主要な最小のバージョン、マイナー、最高の最高の修正プログラム</li><li>*最も高い*: 最上位のバージョン</li></ul> |
| DisableParallelProcessing | 複数のパッケージを並列でインストールを無効にします。 |
| ExcludeVersion | パッケージ名のみとバージョン番号ではないという名前のフォルダーにパッケージをインストールします。 |
| FallbackSource | *(3.2 以降)* プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。 |
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| フレームワーク | *(4.4 以降)* ターゲット フレームワークの依存関係を選択するために使用します。 'に指定されていない場合の既定値です。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| NoCache | NuGet がキャッシュされたパッケージを使用するを防ぎます。 参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| OutputDirectory | パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 |
| PackageSaveMode | パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`します。 |
| プレリリース版 | インストールするプレリリース パッケージを使用できます。 このフラグを使用してパッケージを復元するときに必要ありません`packages.config`します。 |
| RequireConsent | ダウンロードして、パッケージをインストールする前にパッケージの復元が有効になっていることを確認します。 詳細については、[パッケージの復元](../consume-packages/package-restore.md)を参照してください。 |
| SolutionDirectory | パッケージを復元する対象のソリューションのルート フォルダーを指定します。 |
| ソース | パッケージ ソースの一覧を使用する (Url) として指定します。 コマンドを省略すると、構成ファイルで提供されるソースを使用して、参照してください[NuGet の構成の動作を](../consume-packages/configuring-nuget-behavior.md)します。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |
| Version | インストールするパッケージのバージョンを指定します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
