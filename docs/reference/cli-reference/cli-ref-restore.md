---
title: NuGet CLI の restore コマンド
description: Nuget.exe restore コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8ba61fa87118108c36e9dc73f30d964380d02dab
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380455"
---
# <a name="restore-command-nuget-cli"></a>restore コマンド (NuGet CLI)

**適用対象:** パッケージ消費 &bullet;**サポートされているバージョン:** 2.7 以上

`packages` フォルダーにないパッケージをダウンロードしてインストールします。 NuGet 4.0 + および PackageReference 形式と共に使用すると、必要に応じて `obj` フォルダーに `<project>.nuget.props` ファイルが生成されます。 (ファイルはソース管理から省略できます)。

Mono で CLI を使用している Mac OSX と Linux では、パッケージの復元は PackageReference ではサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget restore <projectPath> [options]
```

ここで `<projectPath>` は、ソリューションまたは `packages.config` ファイルの場所を指定します。 動作の詳細については、以下の[解説](#remarks)を参照してください。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。|
| DirectDownload | *(4.0 以降)* バイナリまたはメタデータを使用してキャッシュを設定せずに、パッケージを直接ダウンロードします。 |
| DisableParallelProcessing | 複数のパッケージの並列復元を無効にします。 |
| FallbackSource | *(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。 リストエントリを区切るには、セミコロンを使用します。 |
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| MSBuildPath | *(4.0 以降)* `-MSBuildVersion`よりも優先される、コマンドで使用する MSBuild のパスを指定します。 |
| MSBuildVersion | *(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。 既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。 |
| NoCache | NuGet がキャッシュされたパッケージを使用しないようにします。 「[グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| OutputDirectory | パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 `PackagesDirectory` または `SolutionDirectory` が使用されていない場合に `packages.config` ファイルで復元するときに必要になります。|
| PackageSaveMode | パッケージのインストール後に保存するファイルの種類を指定します。 `nuspec`、`nupkg`、`nuspec;nupkg`のいずれかです。 |
| PackagesDirectory | `OutputDirectory` と同じ。 `OutputDirectory` または `SolutionDirectory` が使用されていない場合に `packages.config` ファイルで復元するときに必要になります。 |
| Project2ProjectTimeOut | プロジェクト間参照を解決するためのタイムアウト (秒)。 |
| Recursive | *(4.0 以降)* UWP および .NET Core プロジェクトのすべての参照プロジェクトを復元します。 `packages.config`を使用するプロジェクトには適用されません。 |
| RequireConsent | パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。 詳細については、「[パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。 |
| SolutionDirectory | ソリューションフォルダーを指定します。 ソリューションのパッケージを復元するときには無効です。 `PackagesDirectory` または `OutputDirectory` が使用されていない場合に `packages.config` ファイルで復元するときに必要になります。 |
| ソース | 復元に使用するパッケージソースの一覧を Url として指定します。 省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [NuGet の動作の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。 リストエントリを区切るには、セミコロンを使用します。 |
| Force | PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、`project.assets.json` ファイルの削除に似ています。 これは、http キャッシュをバイパスしません。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="remarks"></a>コメント

Restore コマンドは、次の手順を実行します。

1. Restore コマンドの操作モードを決定します。

   | projectPath ファイルの種類 | 動作 |
   | --- | --- |
   | ソリューション (フォルダー) | NuGet は、`.sln` ファイルを検索し、見つかった場合はそれを使用します。それ以外の場合は、エラーが発生します。 `(SolutionDir)\.nuget` は、開始フォルダーとして使用されます。 |
   | `.sln` ファイル | ソリューションによって識別されたパッケージを復元します。`-SolutionDirectory` が使用されている場合は、エラーが発生します。 `$(SolutionDir)\.nuget` は、開始フォルダーとして使用されます。 |
   | `packages.config` またはプロジェクトファイル | ファイルに一覧表示されているパッケージを復元し、依存関係を解決してインストールします。 |
   | その他のファイルの種類 | ファイルは、上記のように `.sln` ファイルであると見なされます。ソリューションでない場合は、NuGet によってエラーが返されます。 |
   | (projectPath が指定されていません) | <ul><li>NuGet は、現在のフォルダーにあるソリューションファイルを検索します。 1つのファイルが見つかった場合は、そのファイルを使用してパッケージを復元します。複数のソリューションが見つかった場合は、NuGet によってエラーが返されます。</li><li>ソリューションファイルがない場合は、NuGet によって `packages.config` が検索され、それを使用してパッケージが復元されます。</li><li>ソリューションまたは `packages.config` ファイルが見つからない場合は、NuGet によってエラーが返されます。</ul> |

2. 次の優先順位を使用して packages フォルダーを特定します (これらのフォルダーが見つからない場合は、NuGet によってエラーが返されます)。

    - `-PackagesDirectory`で指定されたフォルダーです。
    - の `repositoryPath` 値 `Nuget.Config`
    - で指定されたフォルダー `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. ソリューションのパッケージを復元するとき、NuGet は次のことを行います。
    - ソリューションファイルを読み込みます。
    - `$(SolutionDir)\.nuget\packages.config` に一覧表示されているソリューションレベルのパッケージを `packages` フォルダーに復元します。
    - `$(ProjectDir)\packages.config` に一覧表示されているパッケージを `packages` フォルダーに復元します。 指定されたパッケージごとに、`-DisableParallelProcessing` が指定されていない限り、並列でパッケージを復元します。

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
