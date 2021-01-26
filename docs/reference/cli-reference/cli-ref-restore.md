---
title: NuGet CLI の復元コマンド
description: nuget.exe restore コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780035"
---
# <a name="restore-command-nuget-cli"></a>restore コマンド (NuGet CLI)

**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** 2.7 以上

フォルダーにないパッケージをダウンロードしてインストールし `packages` ます。 NuGet 4.0 + および PackageReference 形式と共に使用すると、必要に応じて `<project>.nuget.props` フォルダー内にファイルが生成され `obj` ます。 (ファイルはソース管理から省略できます)。

Mono で CLI を使用している Mac OSX と Linux では、パッケージの復元は PackageReference ではサポートされていません。

## <a name="usage"></a>使用方法

```cli
nuget restore <projectPath> [options]
```

ここ `<projectPath>` では、ソリューションまたはファイルの場所を指定し `packages.config` ます。 動作の詳細については、以下の [解説](#remarks) を参照してください。

## <a name="options"></a>Options

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-DirectDownload`**

  *(4.0 以降)* バイナリまたはメタデータを使用してキャッシュを設定せずに、パッケージを直接ダウンロードします。

- **`-DisableParallelProcessing`**

   複数のパッケージの並列復元を無効にします。

- **`-FallbackSource`**

  *(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。 リストエントリを区切るには、セミコロンを使用します。

- **`-Force`**

  PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、ファイルの削除に似てい `project.assets.json` ます。 これは、http キャッシュをバイパスしません。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-ForceEvaluate`**

  ロック ファイルが既に存在する場合でも、すべての依存関係を再評価するように強制的に復元します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-LockFilePath`**

  プロジェクトのロック ファイルの書き込み先である出力場所。 既定値は `PROJECT_ROOT\packages.lock.json` です。

- **`-LockedMode`**

  プロジェクト ロック ファイルの更新は許可されません。

- **`-MSBuildPath`**

   *(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これはよりも優先さ `-MSBuildVersion` れます。

- **`-MSBuildVersion`**

  *(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。 既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。

- **`-NoCache`**

  NuGet がキャッシュされたパッケージを使用しないようにします。 「 [グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-OutputDirectory`**

  パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 `packages.config` `PackagesDirectory` またはが使用されている場合を除き、ファイルを使用して復元する場合に必要です `SolutionDirectory` 。

- **`-PackageSaveMode`**

  パッケージのインストール後に保存するファイルの種類を指定します。、、またはのいずれか `nuspec` `nupkg` `nuspec;nupkg` です。

- **`-PackagesDirectory`**

  `OutputDirectory` と同じ。 `packages.config` `OutputDirectory` またはが使用されている場合を除き、ファイルを使用して復元する場合に必要です `SolutionDirectory` 。

- **`-Project2ProjectTimeOut`**

  プロジェクト間参照を解決するためのタイムアウト (秒)。

- **`-Recursive`**

  *(4.0 以降)* UWP および .NET Core プロジェクトのすべての参照プロジェクトを復元します。 は、を使用するプロジェクトには適用されません `packages.config` 。

- **`-RequireConsent`**

  パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。 詳細については、「 [パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。

- **`-SolutionDirectory`**

  ソリューションフォルダーを指定します。 ソリューションのパッケージを復元するときには無効です。 `packages.config` `PackagesDirectory` またはが使用されている場合を除き、ファイルを使用して復元する場合に必要です `OutputDirectory` 。

- **`-Source`**

  復元に使用するパッケージソースの一覧を Url として指定します。 省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [NuGet の動作の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。 リストエントリを区切るには、セミコロンを使用します。

- **`-UseLockFile`**

  プロジェクト ロック ファイルを生成して復元で使用できるようにします。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="remarks"></a>解説

Restore コマンドは、次の手順を実行します。

1. Restore コマンドの操作モードを決定します。

   | projectPath ファイルの種類 | 動作 |
   | --- | --- |
   | ソリューション (フォルダー) | NuGet はファイルを検索 `.sln` し、見つかった場合はそれを使用します。それ以外の場合はエラーを返します。 `(SolutionDir)\.nuget` は、開始フォルダーとして使用されます。 |
   | `.sln` ファイル | ソリューションによって識別されたパッケージを復元します。が使用されている場合は、エラーが発生 `-SolutionDirectory` します。 `$(SolutionDir)\.nuget` は、開始フォルダーとして使用されます。 |
   | `packages.config` またはプロジェクトファイル | ファイルに一覧表示されているパッケージを復元し、依存関係を解決してインストールします。 |
   | その他のファイルの種類 | ファイルは上記のファイルと見なされ `.sln` ます。ソリューションでない場合は、NuGet によってエラーが返されます。 |
   | (projectPath が指定されていません) | <ul><li>NuGet は、現在のフォルダーにあるソリューションファイルを検索します。 1つのファイルが見つかった場合は、そのファイルを使用してパッケージを復元します。複数のソリューションが見つかった場合は、NuGet によってエラーが返されます。</li><li>ソリューションファイルがない場合、NuGet はを検索 `packages.config` し、それを使用してパッケージを復元します。</li><li>ソリューションまたは `packages.config` ファイルが見つからない場合は、NuGet によってエラーが返されます。</ul> |

2. 次の優先順位を使用して packages フォルダーを特定します (これらのフォルダーが見つからない場合は、NuGet によってエラーが返されます)。

    - で指定されたフォルダー `-PackagesDirectory` 。
    - `repositoryPath`の値`Nuget.Config`
    - で指定されたフォルダー `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. ソリューションのパッケージを復元するとき、NuGet は次のことを行います。
    - ソリューションファイルを読み込みます。
    - に一覧表示されているソリューションレベル `$(SolutionDir)\.nuget\packages.config` のパッケージをフォルダーに復元 `packages` します。
    - に一覧表示されているパッケージ `$(ProjectDir)\packages.config` をフォルダーに復元 `packages` します。 が指定されている場合を除き、指定したパッケージごとに、並列でパッケージを復元し `-DisableParallelProcessing` ます。

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
