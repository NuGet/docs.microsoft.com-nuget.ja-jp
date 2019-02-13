---
title: NuGet CLI restore コマンド
description: Nuget.exe の復元コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: adf97196f50f2a55d6b8ceed93d53ff12b67657b
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145632"
---
# <a name="restore-command-nuget-cli"></a>restore (NuGet CLI) コマンド

**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン。** 2.7+

ダウンロードしてから不足しているすべてのパッケージをインストール、`packages`フォルダー。 NuGet 4.0 以降と PackageReference 形式を併用すると生成、`<project>.nuget.props`ファイルの場合は、必要に応じて、`obj`フォルダー。 (ファイルをソース管理から省略できます)。

Mac OSX および Mono で CLI を使用した Linux の場合は、パッケージの復元はサポートされていません packagereference の場合。

## <a name="usage"></a>使用法

```cli
nuget restore <projectPath> [options]
```

場所`<projectPath>`ソリューションの場所を指定しますまたは、`packages.config`ファイル。 参照してください[解説](#remarks)以下詳細については動作します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| DirectDownload | *(4.0 以降)* 任意のバイナリとメタデータのキャッシュを設定せずに直接パッケージをダウンロードします。 |
| DisableParallelProcessing | 並列で複数のパッケージの復元を無効にします。 |
| FallbackSource | *(3.2 以降)* プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。 |
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| MSBuildPath | *(4.0 以降)* よりも優先、コマンドで使用する MSBuild のパスを示す`-MSBuildVersion`します。 |
| MSBuildVersion | *(3.2 以降)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされている値とは、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。 パスに MSBuild が取得される、既定でそれ以外の場合、既定値 MSBuild の最上位のインストールされているバージョンです。 |
| NoCache | NuGet がキャッシュされたパッケージを使用するを防ぎます。 参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| OutputDirectory | パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 復元するときに必要な`packages.config`ファイル`PackagesDirectory`または`SolutionDirectory`使用されます。|
| PackageSaveMode | パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`します。 |
| パッケージファイル | `OutputDirectory` と同じ。 復元するときに必要な`packages.config`ファイル`OutputDirectory`または`SolutionDirectory`使用されます。 |
| Project2ProjectTimeOut | タイムアウト (秒) プロジェクト間参照を解決します。 |
| 再帰 | *(4.0 以降)* UWP と .NET Core プロジェクトのすべての参照プロジェクトを復元します。 使用してプロジェクトには適用されません`packages.config`します。 |
| RequireConsent | ダウンロードして、パッケージをインストールする前にパッケージの復元が有効になっていることを確認します。 詳細については、次を参照してください。[パッケージの復元](../consume-packages/package-restore.md)します。 |
| SolutionDirectory | ソリューション フォルダーを指定します。 ソリューションのパッケージを復元するときに無効です。 復元するときに必要な`packages.config`ファイル`PackagesDirectory`または`OutputDirectory`使用されます。 |
| ソース | (Url) として、復元に使用するパッケージ ソースの一覧を指定します。 コマンドを省略すると、構成ファイルで提供されるソースを使用して、参照してください[NuGet の構成の動作を](../consume-packages/configuring-nuget-behavior.md)します。 |
| 詳細度 |> の出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="remarks"></a>Remarks

Restore コマンドでは、次の手順を実行します。

1. Restore コマンドの操作モードを決定します。

   | projectPath ファイルの種類 | 動作 |
   | --- | --- |
   | ソリューション (フォルダー) | NuGet 検索、`.sln`ファイルとそれ以外の場合は、エラーが使用されます。 `(SolutionDir)\.nuget` 開始フォルダーとして使用されます。 |
   | `.sln` ファイル | ソリューションで識別されるパッケージを復元します。エラーを示します`-SolutionDirectory`使用されます。 `$(SolutionDir)\.nuget` 開始フォルダーとして使用されます。 |
   | `packages.config` ファイルまたはプロジェクト ファイル | 解決して、依存関係のインストール ファイルで示されているパッケージを復元します。 |
   | その他のファイルの種類 | ファイルがあると見なされます、`.sln`ソリューション、NuGet はエラーがない場合に、上記; ファイルします。 |
   | (指定されていない projectPath) | <ul><li>NuGet は、現在のフォルダーにソリューション ファイルを検索します。 は、パッケージを復元する 1 つが使用される 1 つのファイルが見つかった場合複数のソリューションが見つかった場合、NuGet はエラーを示します。</li><li>NuGet 検索ソリューション ファイルがない場合、`packages.config`はパッケージの復元を使用しているとします。</li><li>ソリューションがない場合または`packages.config`ファイルが見つかると、NuGet はエラーを示します。</ul> |

2. 次の優先順位 (NuGet は、これらのフォルダーが見つからない場合にエラーを提供) を使用して、パッケージ フォルダーを確認します。

    - 指定されたフォルダー`-PackagesDirectory`します。
    - `repositoryPath`の値 `Nuget.Config`
    - 指定されたフォルダー `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. ソリューションのパッケージを復元するには、NuGet は、次を行います。
    - ソリューション ファイルを読み込みます。
    - 記載ソリューション レベル パッケージを復元`$(SolutionDir)\.nuget\packages.config`に、`packages`フォルダー。
    - 示されているパッケージを復元`$(ProjectDir)\packages.config`に、`packages`フォルダー。 指定されたパッケージごとに、必要ない限り、並列でパッケージを復元`-DisableParallelProcessing`を指定します。

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
