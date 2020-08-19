---
title: NuGet CLI のインストールコマンド
description: nuget.exe install コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 23856728d07d07183b5aedcd6218a56a444c410b
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623098"
---
# <a name="install-command-nuget-cli"></a>install コマンド (NuGet CLI)

**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** すべて

パッケージをダウンロードしてプロジェクトにインストールします。指定したパッケージソースを使用して、既定で現在のフォルダーを指定します。

> [!Tip]
> プロジェクトのコンテキストの外部でパッケージを直接ダウンロードするには、 [nuget.org](https://www.nuget.org) のパッケージのページにアクセスし、[ **ダウンロード** ] リンクを選択します。

ソースが指定されていない場合は、グローバル構成ファイル `%appdata%\NuGet\NuGet.Config` (Windows) または (Mac/Linux) に記載されているもの `~/.nuget/NuGet/NuGet.Config` が使用されます。 詳細については、「 [一般的な NuGet の構成](../../consume-packages/configuring-nuget-behavior.md) 」を参照してください。

特定のパッケージが指定されていない場合、は、 `install` プロジェクトのファイルに一覧表示されているすべてのパッケージをインストールして、の `packages.config` ように [`restore`](cli-ref-restore.md) します。

`install`このコマンドは、プロジェクトファイルまたはを変更しません `packages.config` 。この方法では、 `restore` パッケージをディスクに追加するだけで、プロジェクトの依存関係は変更しないという点でも同様です。

依存関係を追加するには、Visual Studio のパッケージマネージャー UI またはコンソールを使用してパッケージを追加するか、 `packages.config` またはを変更して実行し `install` `restore` ます。

## <a name="usage"></a>使用法

```cli
nuget install <packageID | configFilePath> [options]
```

`<packageID>`(最新バージョンを使用して) インストールするパッケージの名前を `<configFilePath>` 指定するか、 `packages.config` インストールするパッケージの一覧を示すファイルを指定します。 オプションを使用して特定のバージョンを指定でき `-Version` ます。

## <a name="options"></a>Options

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-DependencyVersion`**

  *(4.4 以降)* 使用する依存関係パッケージのバージョン。次のいずれかになります。<br/><ul><li>*最低* (既定): 最も低いバージョンです。</li><li>*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</li><li>*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</li><li>*最高*: 最高バージョン</li><li>*無視*: 依存関係パッケージは使用されません</li></ul>

- **`-DirectDownload`**

  メタデータまたはバイナリを含むキャッシュを作成せずに、直接ダウンロードします。

- **`-DisableParallelProcessing`**

  複数のパッケージの並列インストールを無効にします。

- **`-x|-ExcludeVersion`**

  パッケージ名がではなく、パッケージ名だけを持つという名前のフォルダーにパッケージをインストールします。

- **`-FallbackSource`**

  *(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-Framework`**

  *(4.4 以降)* 依存関係の選択に使用されるターゲットフレームワーク。 指定しない場合、既定値は ' Any ' になります。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-NoCache`**

  NuGet がキャッシュされたパッケージを使用しないようにします。 「 [グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-OutputDirectory`**

  パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。

- **`-PackageSaveMode`**

  パッケージのインストール後に保存するファイルの種類を指定します。、、またはのいずれか `nuspec` `nupkg` `nuspec;nupkg` です。

- **`-PreRelease`**

  プレリリースパッケージのインストールを許可します。 このフラグは、を使用してパッケージを復元する場合には必要ありません `packages.config` 。

- **`-RequireConsent`**

  パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。 詳細については、「 [パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。

- **`-SolutionDirectory`**

  パッケージを復元するソリューションのルートフォルダーを指定します。

- **`-Source`**

   使用するパッケージソースの一覧を Url として指定します。 省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [Common NuGet](../../consume-packages/configuring-nuget-behavior.md)configuration」を参照してください。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

- **`-Version`**

  インストールするパッケージのバージョンを指定します。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
