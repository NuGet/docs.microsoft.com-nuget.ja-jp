---
title: NuGet でグローバル パッケージ、キャッシュ、一時フォルダーを管理する方法
description: パッケージをインストール、復元、および更新するときに使用される、コンピューター上に存在するグローバル パッケージ インストール フォルダー、パッケージ キャッシュ、および一時フォルダーを管理する方法
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e5585267d4ce2563d77ff30ec5c31e196d98686a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774794"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>グローバル パッケージ、キャッシュ、および一時フォルダーを管理する

NuGet では、パッケージのインストール、更新、または復元を行う場合は常に、プロジェクト構造の外にある複数のフォルダーで、以下のようなパッケージとパッケージ情報を管理します。

| 名前 | 説明および場所 (ユーザーごと)|
| --- | --- |
| global&#8209;packages | "*グローバル パッケージ*" フォルダーは、ダウンロードされた任意のパッケージが NuGet でインストールされる場所です。 各パッケージは、パッケージ ID とバージョン番号と一致するサブフォルダーに完全に展開されます。 [PackageReference](package-references-in-project-files.md) 形式を使用するプロジェクトでは常に、このフォルダーから直接パッケージを使用します。 [packages.config](../reference/packages-config.md) を使用する場合、パッケージは "*グローバル パッケージ*" フォルダーにインストールされ、プロジェクトの `packages` フォルダーにコピーされます。<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>NUGET_PACKAGES 環境変数、`globalPackagesFolder`または `repositoryPath` [構成設定](../reference/nuget-config-file.md#config-section) (それぞれ、PackageReference および `packages.config` を使用している場合)、あるいは `RestorePackagesPath` MSBuild プロパティ (MSBuild のみ) を使用して、オーバーライドします。 環境変数は、構成設定よりも優先されます。</li></ul> |
| http&#8209;cache | Visual Studio パッケージ マネージャー (NuGet 3.x 以降) および `dotnet` ツールでは、ダウンロードしたパッケージのコピーをこのキャッシュに格納し (`.dat` ファイルとして保存)、各パッケージ ソースのサブフォルダーに整理します。 パッケージは展開されず、キャッシュには 30 分の有効期限があります。<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>NUGET_HTTP_CACHE_PATH 環境変数を使用してオーバーライドします。</li></ul> |
| temp | NuGet が、さまざまな操作中に一時ファイルを格納するフォルダーです。<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| plugins-cache **4.8+** | NuGet が、操作要求の結果を格納するフォルダーです。<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>NUGET_PLUGINS_CACHE_PATH 環境変数を使用してオーバーライドします。</li></ul> |

> [!Note]
> NuGet 3.5 以前では、"*HTTP キャッシュ*" ではなく、`%localappdata%\NuGet\Cache` にある "*パッケージ キャッシュ*" を使用していました。

キャッシュと "*グローバル パッケージ*" フォルダーを使用することで、NuGet は多くの場合、コンピューター上に既に存在するパッケージのダウンロードを回避して、インストール、更新、および復元処理のパフォーマンスを改善しました。 また、PackageReference を使用する場合、"*グローバル パッケージ*" フォルダーによって、プロジェクト フォルダー内にダウンロードされたパッケージを保持することを回避できます。プロジェクト フォルダーでは、パッケージがソース コントロールに誤って追加される可能性があります。グローバル パッケージ フォルダーによって、コンピューター ストレージでの NuGet の全体の影響が緩和されます。

パッケージの取得を求められたら、NuGet は最初に "*グローバル パッケージ*" フォルダー内を調べます。 パッケージの正確なバージョンがここになかった場合、NuGet は HTTP 以外のすべてのパッケージ ソースを確認します。 それでもパッケージが見つからない場合、`--no-cache` を付加した `dotnet.exe` コマンドまたは `-NoCache` を付加した `nuget.exe` コマンドを指定していないかぎり、NuGet は "*HTTP キャッシュ*" でパッケージを探します。 パッケージがキャッシュになかった場合、またはキャッシュが使用されていない場合、NuGet は HTTP 経由でパッケージを取得します。

詳細については、「[パッケージ インストールのしくみ](../concepts/package-installation-process.md)」を参照してください。

## <a name="viewing-folder-locations"></a>フォルダーの場所を表示する

次のように [nuget locals コマンド](../reference/cli-reference/cli-ref-locals.md)を使用して場所を表示できます。

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

典型的な出力は次のとおりです (Windows、"user1" は現在のユーザー名)。

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` は NuGet 2.x で使用され、NuGet 3.5 以前で表示されます。)

次のように [dotnet nuget locals コマンド](/dotnet/core/tools/dotnet-nuget-locals)を使用して、フォルダーの場所を表示することもできます。

```dotnetcli
dotnet nuget locals all --list
```

典型的な出力は次のとおりです (Mac/Linux、"user1" は現在のユーザー名)。

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

単一フォルダーの場所を表示するには、`all` ではなく、`http-cache`、`global-packages`、`temp`、または `plugins-cache` を使用します。

## <a name="clearing-local-folders"></a>ローカル フォルダーをクリアする

パッケージのインストールに関する問題が発生した場合、または、リモート ギャラリーからパッケージをインストールしていることを確認する場合は、フォルダーを指定してクリアする `locals --clear` オプションまたは `locals -clear` (nuget.exe) を使用するか、すべてのフォルダーをクリアする `all` を使用します。

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

現在 Visual Studio で開いているプロジェクトで使用されているパッケージはすべて、"*グローバル パッケージ*" フォルダーからクリアされません。

Visual Studio 2017 以降、 **[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー設定]** メニュー コマンドを使用して、 **[すべての NuGet キャッシュをクリア]** を選択します。 キャッシュの管理は現在、パッケージ マネージャー コンソール経由では利用できません。 Visual Studio 2015 では、代わりに CLI コマンドを使用します。

![キャッシュをクリアするための NuGet オプション コマンド](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>エラーのトラブルシューティング

以下のエラーは、`nuget locals` または `dotnet nuget locals`を使用した場合に発生する可能性があります。

- *エラー: 別のプロセスで使用されているため、<package>プロセスはファイルにアクセスできません* または *ローカル リソースをクリアできませんでした。1 つ以上のファイルを削除できません*

    フォルダーにある 1 つまたは複数のファイルが、別のプロセスで使用中です。たとえば、"*グローバル パッケージ*" フォルダー内のパッケージを参照する Visual Studio プロジェクトが開いています。 それらのプロセスを閉じて、もう一度やり直してください。

- *エラー: パスへのアクセスが<path>拒否されます* または *ディレクトリが空ではありません*

    キャッシュのファイルを削除するためのアクセス許可がありません。 可能であれば、フォルダーのアクセス許可を変更して、もう一度やり直してください。 それができない場合は、システム管理者に問い合わせてください。

- *エラー: 指定されたパスかファイル名、またはその両方が長すぎます。完全修飾ファイル名は 260 文字未満で指定し、ディレクトリ名は 248 文字未満で指定してください。* "

    フォルダー名を短くして、もう一度やり直してください。
