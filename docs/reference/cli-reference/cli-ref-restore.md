---
title: NuGet CLI の restore コマンド
description: Nuget.exe restore コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 82113d460f7f5ff467b0a0552cc49283de95de25
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327639"
---
# <a name="restore-command-nuget-cli"></a>restore コマンド (NuGet CLI)

**適用対象:** パッケージ消費&bullet;が**サポートされているバージョン:** 2.7+

フォルダーに`packages`ないパッケージをダウンロードしてインストールします。 NuGet 4.0 + および PackageReference 形式と共に使用すると、 `<project>.nuget.props`必要に応じて`obj`フォルダー内にファイルが生成されます。 (ファイルはソース管理から省略できます)。

Mono で CLI を使用している Mac OSX と Linux では、パッケージの復元は PackageReference ではサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget restore <projectPath> [options]
```

ここ`<projectPath>` で`packages.config`は、ソリューションまたはファイルの場所を指定します。 動作の詳細については、以下の[解説](#remarks)を参照してください。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| DirectDownload | *(4.0 以降)* バイナリまたはメタデータを使用してキャッシュを設定せずに、パッケージを直接ダウンロードします。 |
| DisableParallelProcessing | 複数のパッケージの並列復元を無効にします。 |
| FallbackSource | *(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。 |
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| MSBuildPath | *(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これは`-MSBuildVersion`よりも優先されます。 |
| MSBuildVersion | *(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。 既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。 |
| NoCache | NuGet がキャッシュされたパッケージを使用しないようにします。 「[グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| OutputDirectory | パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 または`packages.config` `PackagesDirectory` が使用されている場合を除き、ファイルを使用して復元する場合`SolutionDirectory`に必要です。|
| PackageSaveMode | パッケージのインストール後に保存するファイルの種類を指定し`nuspec`ます`nupkg`。、 `nuspec;nupkg`、またはのいずれかです。 |
| PackagesDirectory | `OutputDirectory` と同じ。 または`packages.config` `OutputDirectory` が使用されている場合を除き、ファイルを使用して復元する場合`SolutionDirectory`に必要です。 |
| Project2ProjectTimeOut | プロジェクト間参照を解決するためのタイムアウト (秒)。 |
| Recursive | *(4.0 以降)* UWP および .NET Core プロジェクトのすべての参照プロジェクトを復元します。 は、を使用`packages.config`するプロジェクトには適用されません。 |
| RequireConsent | パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。 詳細については、「[パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。 |
| SolutionDirectory | ソリューションフォルダーを指定します。 ソリューションのパッケージを復元するときには無効です。 または`packages.config` `PackagesDirectory` が使用されている場合を除き、ファイルを使用して復元する場合`OutputDirectory`に必要です。 |
| Source | 復元に使用するパッケージソースの一覧を Url として指定します。 省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [NuGet の動作の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="remarks"></a>Remarks

Restore コマンドは、次の手順を実行します。

1. Restore コマンドの操作モードを決定します。

   | projectPath ファイルの種類 | 動作 |
   | --- | --- |
   | ソリューション (フォルダー) | NuGet は`.sln`ファイルを検索し、見つかった場合はそれを使用します。それ以外の場合はエラーを返します。 `(SolutionDir)\.nuget`は、開始フォルダーとして使用されます。 |
   | `.sln`拡張子 | ソリューションによって識別されたパッケージを復元します。が使用され`-SolutionDirectory`ている場合は、エラーが発生します。 `$(SolutionDir)\.nuget`は、開始フォルダーとして使用されます。 |
   | `packages.config`またはプロジェクトファイル | ファイルに一覧表示されているパッケージを復元し、依存関係を解決してインストールします。 |
   | その他のファイルの種類 | ファイルは上記の`.sln`ファイルと見なされます。ソリューションでない場合は、NuGet によってエラーが返されます。 |
   | (projectPath が指定されていません) | <ul><li>NuGet は、現在のフォルダーにあるソリューションファイルを検索します。 1つのファイルが見つかった場合は、そのファイルを使用してパッケージを復元します。複数のソリューションが見つかった場合は、NuGet によってエラーが返されます。</li><li>ソリューションファイルがない場合、NuGet はを検索`packages.config`し、それを使用してパッケージを復元します。</li><li>ソリューションまたは`packages.config`ファイルが見つからない場合は、NuGet によってエラーが返されます。</ul> |

2. 次の優先順位を使用して packages フォルダーを特定します (これらのフォルダーが見つからない場合は、NuGet によってエラーが返されます)。

    - で`-PackagesDirectory`指定されたフォルダー。
    - の`repositoryPath`値`Nuget.Config`
    - で指定されたフォルダー`-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. ソリューションのパッケージを復元するとき、NuGet は次のことを行います。
    - ソリューションファイルを読み込みます。
    - に`$(SolutionDir)\.nuget\packages.config`一覧表示されているソリューション`packages`レベルのパッケージをフォルダーに復元します。
    - に`$(ProjectDir)\packages.config`一覧表示されて`packages`いるパッケージをフォルダーに復元します。 が指定されている場合を除き`-DisableParallelProcessing` 、指定したパッケージごとに、並列でパッケージを復元します。

## <a name="examples"></a>使用例

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
