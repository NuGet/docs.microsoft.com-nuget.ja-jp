---
title: NuGet CLI install コマンド
description: Nuget.exe install コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036943"
---
# <a name="install-command-nuget-cli"></a>install コマンド (NuGet CLI)

**適用対象:** パッケージ消費 &bullet;**サポートされているバージョン:** すべて

パッケージをダウンロードしてプロジェクトにインストールします。指定したパッケージソースを使用して、既定で現在のフォルダーを指定します。

> [!Tip]
> プロジェクトのコンテキストの外部でパッケージを直接ダウンロードするには、 [nuget.org](https://www.nuget.org)のパッケージのページにアクセスし、 **[ダウンロード]** リンクを選択します。

ソースが指定されていない場合は、グローバル構成ファイル、`%appdata%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) に記載されているものが使用されます。 詳細については、「[一般的な NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。

特定のパッケージが指定されていない場合は、`install` プロジェクトの `packages.config` ファイルに一覧表示されているすべてのパッケージがインストールされ、 [`restore`](cli-ref-restore.md)のようになります。

`install` コマンドでは、プロジェクトファイルや `packages.config`は変更されません。この方法では、パッケージをディスクに追加するだけで、プロジェクトの依存関係は変更しないという点で `restore` に似ています。

依存関係を追加するには、Visual Studio のパッケージマネージャー UI またはコンソールを使用してパッケージを追加するか、`packages.config` を変更して `install` または `restore`を実行します。

## <a name="usage"></a>使用方法

```cli
nuget install <packageID | configFilePath> [options]
```

インストールするパッケージの `<packageID>` 名前 (最新バージョンを使用)、または `<configFilePath>` インストールするパッケージの一覧を示す `packages.config` ファイルを指定します。 `-Version` オプションを使用して特定のバージョンを指定できます。

## <a name="options"></a>オプション

| オプション | [説明] |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。|
| DependencyVersion | *(4.4 以降)* 使用する依存関係パッケージのバージョン。次のいずれかになります。<br/><ul><li>*最低*(既定): 最も低いバージョンです。</li><li>*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</li><li>*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</li><li>*最高*: 最高バージョン</li><li>*無視*: 依存関係パッケージは使用されません</li></ul> |
| DisableParallelProcessing | 複数のパッケージの並列インストールを無効にします。 |
| ExcludeVersion | パッケージ名がではなく、パッケージ名だけを持つという名前のフォルダーにパッケージをインストールします。 |
| FallbackSource | *(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。 |
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| フレームワーク | *(4.4 以降)* 依存関係の選択に使用されるターゲットフレームワーク。 指定しない場合、既定値は ' Any ' になります。 |
| [Help] | ヘルプのコマンドの情報を表示します。 |
| NoCache | NuGet がキャッシュされたパッケージを使用しないようにします。 「[グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| OutputDirectory | パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 |
| PackageSaveMode | パッケージのインストール後に保存するファイルの種類を指定します。 `nuspec`、`nupkg`、`nuspec;nupkg`のいずれかです。 |
| PreRelease | プレリリースパッケージのインストールを許可します。 `packages.config`でパッケージを復元する場合、このフラグは必要ありません。 |
| RequireConsent | パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。 詳細については、「[パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。 |
| SolutionDirectory | パッケージを復元するソリューションのルートフォルダーを指定します。 |
| [ソース] | 使用するパッケージソースの一覧を Url として指定します。 省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [Common NuGet](../../consume-packages/configuring-nuget-behavior.md)configuration」を参照してください。 |
| 詳細度 | 出力に表示される詳細の量を指定します (*通常*、*非*表示、*詳細*)。 |
| バージョン | インストールするパッケージのバージョンを指定します。 |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
