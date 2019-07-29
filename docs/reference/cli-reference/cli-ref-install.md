---
title: NuGet CLI install コマンド
description: Nuget.exe install コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327789"
---
# <a name="install-command-nuget-cli"></a>install コマンド (NuGet CLI)

**適用対象:** パッケージの&bullet;使用量が**サポートされているバージョン:** すべて

パッケージをダウンロードしてプロジェクトにインストールします。指定したパッケージソースを使用して、既定で現在のフォルダーを指定します。

> [!Tip]
> プロジェクトのコンテキストの外部でパッケージを直接ダウンロードするには、 [nuget.org](https://www.nuget.org)のパッケージのページにアクセスし、 **[ダウンロード]** リンクを選択します。

ソースが指定されていない場合は、グローバル構成ファイル`%appdata%\NuGet\NuGet.Config` (Windows) また`~/.nuget/NuGet/NuGet.Config`は (Mac/Linux) に記載されているものが使用されます。 詳細については、「[一般的な NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。

特定のパッケージが指定され`install`ていない場合、は、プロジェクト`packages.config`のファイルに一覧表示さ[`restore`](cli-ref-restore.md)れているすべてのパッケージをインストールして、のようにします。

このコマンドは、プロジェクトファイルまたはを`packages.config`変更しません。この`restore`方法では、パッケージをディスクに追加するだけで、プロジェクトの依存関係は変更しないという点でも同様です。 `install`

依存関係を追加するには、Visual Studio のパッケージマネージャー UI またはコンソールを使用してパッケージ`packages.config`を追加するか`install` 、 `restore`またはを変更して実行します。

## <a name="usage"></a>使用法

```cli
nuget install <packageID | configFilePath> [options]
```

(最新バージョンを使用して) インストールするパッケージの`<configFilePath>` `packages.config` 名前を指定するか、インストールするパッケージの一覧を示すファイルを`<packageID>`指定します。 `-Version`オプションを使用して特定のバージョンを指定できます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| DependencyVersion | *(4.4 以降)* 使用する依存関係パッケージのバージョン。次のいずれかになります。<br/><ul><li>*最低*(既定): 最も低いバージョン</li><li>*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</li><li>*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</li><li>*最高*: 最高バージョン</li></ul> |
| DisableParallelProcessing | 複数のパッケージの並列インストールを無効にします。 |
| ExcludeVersion | パッケージ名がではなく、パッケージ名だけを持つという名前のフォルダーにパッケージをインストールします。 |
| FallbackSource | *(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。 |
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Framework | *(4.4 以降)* 依存関係の選択に使用されるターゲットフレームワーク。 指定しない場合、既定値は ' Any ' になります。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NoCache | NuGet がキャッシュされたパッケージを使用しないようにします。 「[グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| OutputDirectory | パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 |
| PackageSaveMode | パッケージのインストール後に保存するファイルの種類を指定し`nuspec`ます`nupkg`。、 `nuspec;nupkg`、またはのいずれかです。 |
| PreRelease | プレリリースパッケージのインストールを許可します。 このフラグは、を使用してパッケージ`packages.config`を復元する場合には必要ありません。 |
| RequireConsent | パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。 詳細については、「[パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。 |
| SolutionDirectory | パッケージを復元するソリューションのルートフォルダーを指定します。 |
| Source | 使用するパッケージソースの一覧を Url として指定します。 省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [Common NuGet](../../consume-packages/configuring-nuget-behavior.md)configuration」を参照してください。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |
| Version | インストールするパッケージのバージョンを指定します。 |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
