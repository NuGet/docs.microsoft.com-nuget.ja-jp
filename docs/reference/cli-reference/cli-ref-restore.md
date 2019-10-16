---
title: NuGet CLI の復元コマンド
description: Nuget.exe 復元コマンドのリファレンス
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

**適用対象:** パッケージ消費 &bullet;**サポートされているバージョン:** 2.7 以降

@No__t-0 フォルダーにないパッケージをダウンロードしてインストールします。 NuGet 4.0 + および PackageReference 形式と共に使用すると、必要に応じて `obj` フォルダーに @no__t 0 ファイルが生成されます。 (ファイルはソース管理から省略できます)。

Mono で CLI を使用している Mac OSX と Linux では、パッケージの復元は PackageReference ではサポートされていません。

## <a name="usage"></a>使用方法

```cli
nuget restore <projectPath> [options]
```

ここで `<projectPath>` は、ソリューションまたは @no__t 1 ファイルの場所を指定します。 動作の詳細については、以下の[解説](#remarks)を参照してください。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。|
| DirectDownload | *(4.0 以降)* バイナリまたはメタデータを使用してキャッシュを設定せずに、パッケージを直接ダウンロードします。 |
| DisableParallelProcessing | 複数のパッケージの並列復元を無効にします。 |
| FallbackSource | *(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。 リストエントリを区切るには、セミコロンを使用します。 |
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| [Help] | コマンドのヘルプ情報を表示します。 |
| MSBuildPath | *(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。 `-MSBuildVersion` よりも優先されます。 |
| MSBuildVersion | *(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。 既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。 |
| NoCache | NuGet がキャッシュされたパッケージを使用しないようにします。 「[グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。 |
| 非対話型 | ユーザーの入力または確認のプロンプトを表示しません。 |
| OutputDirectory | パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 @No__t-1 または `SolutionDirectory` が使用されていない場合は、@no__t 0 のファイルで復元するときに必要になります。|
| パッケージ Avemode | パッケージのインストール後に保存するファイルの種類を指定します。 `nuspec`、`nupkg`、`nuspec;nupkg` のいずれかです。 |
| パッケージディレクトリ | `OutputDirectory` と同じ。 @No__t-1 または `SolutionDirectory` が使用されていない場合は、@no__t 0 のファイルで復元するときに必要になります。 |
| Project2ProjectTimeOut | プロジェクト間参照を解決するためのタイムアウト (秒)。 |
| 繰り返し | *(4.0 以降)* UWP および .NET Core プロジェクトのすべての参照プロジェクトを復元します。 @No__t-0 を使用するプロジェクトには適用されません。 |
| RequireConsent | パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。 詳細については、「[パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。 |
| SolutionDirectory | ソリューションフォルダーを指定します。 ソリューションのパッケージを復元するときには無効です。 @No__t-1 または `OutputDirectory` が使用されていない場合は、@no__t 0 のファイルで復元するときに必要になります。 |
| [ソース] | 復元に使用するパッケージソースの一覧を Url として指定します。 省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [NuGet の動作の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。 リストエントリを区切るには、セミコロンを使用します。 |
| 必ず | PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、`project.assets.json` ファイルの削除に似ています。 これは、http キャッシュをバイパスしません。 |
| 詳細度 | 出力に表示される詳細の量を指定します (*通常*、*非*表示、*詳細*)。 |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="remarks"></a>Remarks

Restore コマンドは、次の手順を実行します。

1. Restore コマンドの操作モードを決定します。

   | projectPath ファイルの種類 | 動作 |
   | --- | --- |
   | ソリューション (フォルダー) | NuGet は @no__t 0 のファイルを検索し、見つかった場合はそれを使用します。それ以外の場合は、エラーが発生します。 `(SolutionDir)\.nuget` が開始フォルダーとして使用されます。 |
   | `.sln` ファイル | ソリューションによって識別されたパッケージを復元します。`-SolutionDirectory` が使用されている場合は、エラーが発生します。 `$(SolutionDir)\.nuget` が開始フォルダーとして使用されます。 |
   | `packages.config` またはプロジェクトファイル | ファイルに一覧表示されているパッケージを復元し、依存関係を解決してインストールします。 |
   | その他のファイルの種類 | ファイルは、上記の @no__t 0 ファイルと想定されます。ソリューションでない場合は、NuGet によってエラーが返されます。 |
   | (projectPath が指定されていません) | <ul><li>NuGet は、現在のフォルダーにあるソリューションファイルを検索します。 1つのファイルが見つかった場合は、そのファイルを使用してパッケージを復元します。複数のソリューションが見つかった場合は、NuGet によってエラーが返されます。</li><li>ソリューションファイルがない場合、NuGet は @no__t 0 を検索し、それを使用してパッケージを復元します。</li><li>ソリューションまたは `packages.config` ファイルが見つからない場合は、NuGet によってエラーが返されます。</ul> |

2. 次の優先順位を使用して packages フォルダーを特定します (これらのフォルダーが見つからない場合は、NuGet によってエラーが返されます)。

    - @No__t-0 で指定されたフォルダーです。
    - @No__t-1 の @no__t 0 の値
    - @No__t-0 で指定されたフォルダー
    - `$(SolutionDir)\packages`

3. ソリューションのパッケージを復元するとき、NuGet は次のことを行います。
    - ソリューションファイルを読み込みます。
    - @No__t-0 に一覧表示されているソリューションレベルのパッケージを `packages` フォルダーに復元します。
    - @No__t-0 に一覧表示されているパッケージを `packages` フォルダーに復元します。 指定されたパッケージごとに、`-DisableParallelProcessing` が指定されていない限り、並列でパッケージを復元します。

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
