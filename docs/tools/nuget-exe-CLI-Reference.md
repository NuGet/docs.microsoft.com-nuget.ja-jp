---
title: NuGet コマンド ライン インターフェイス (CLI) のリファレンス
description: Nuget.exe CLI のコマンド ライン リファレンスのインデックス
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a257dbbd9d56b5989e050ed4096d096cd1036184
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426019"
---
# <a name="nuget-cli-reference"></a>NuGet CLI リファレンス

NuGet コマンド ライン インターフェイス (CLI)、 `nuget.exe`、インストール、作成、発行、およびプロジェクト ファイルに変更を加えずにパッケージの管理に NuGet の機能のすべての範囲を提供します。

任意のコマンドを使用するコマンド ウィンドウを開き、または bash シェルを実行`nuget`などによって、コマンドと適切なオプションは、その後に`nuget help pack`(pack コマンドのヘルプを表示) にします。

このドキュメントでは、NuGet CLI の最新バージョンが反映されます。 使用している任意のバージョンに対して正確な詳細については、次のように実行します。`nuget help`の目的のコマンド。

基本的なコマンドを使用する方法については、 `nuget.exe` CLI を参照してください[インストール nuget.exe CLI を使用してパッケージを使用して](../consume-packages/install-use-packages-nuget-cli.md)します。

## <a name="installing-nugetexe"></a>Nuget.exe をインストールします。

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> NuGet CLI で使用できるように、パッケージ マネージャー コンソール内で Visual Studio で、次を参照してください。[コンソールで nuget.exe CLI を使用して](package-manager-console.md#using-the-nugetexe-cli-in-the-console)します。

## <a name="availability"></a>可用性

参照してください[機能の可用性](../install-nuget-client-tools.md#feature-availability)詳細については正確です。

- すべてのコマンドは、Windows で使用できます。
- Nuget.exe に対して指定された場所を除く、Mono で実行されているすべてのコマンドを使用`pack`、 `restore`、および`update`します。
- `pack`、 `restore`、 `delete`、 `locals`、および`push`コマンドも dotnet CLI を使って Mac および Linux で使用します。

## <a name="commands-and-applicability"></a>コマンドと適用性

使用可能なコマンドとパッケージの作成、パッケージの使用、またはパッケージのホストに公開する適用性:

| 一般的なコマンド | 適用可能なロール | NuGet のバージョン | 説明 |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | 作成 | 2.7+ | NuGet パッケージを作成、`.nuspec`またはプロジェクト ファイル。 Mono で実行するときに、プロジェクト ファイルからパッケージの作成はサポートされていません。 |
| [push](cli-ref-push.md) | 置換 | すべて | パッケージ ソースへのパッケージを発行します。 |
| [config](cli-ref-config.md) | すべて | すべて | 取得または NuGet の構成値を設定します。 |
| [help or ?](cli-ref-help.md) | すべて | すべて | ヘルプ情報またはコマンドのヘルプを表示します。 |
| [locals](cli-ref-locals.md) | 利用 | 3.3+ | 場所を一覧表示、*グローバル パッケージ*、 *http キャッシュ*、および*temp*フォルダーとそれらのフォルダーの内容をクリアします。 |
| [restore](cli-ref-restore.md) | 利用 | 2.7+ | 使用中のパッケージ管理形式によって参照されるすべてのパッケージを復元します。 Mono で実行するときに、PackageReference 形式を使用してパッケージの復元はサポートされていません。 |
| [setapikey](cli-ref-setapikey.md) | 発行に使用量 | すべて | パッケージ ソースへのアクセス キーが必要な場合は、特定のパッケージ ソースの API キーを保存します。 |
| [spec](cli-ref-spec.md) | 作成 | すべて | 生成、`.nuspec`ファイルを Visual Studio プロジェクトからファイルを生成する場合は、トークンを使用します。 |

| セカンダリ コマンド | 適用可能なロール | NuGet のバージョン | 説明 |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | 置換 | 3.3+ | 階層構造を使用して、HTTP 以外のパッケージ ソースには、パッケージを追加します。 HTTP ソース、使用*プッシュ*します。 |
| [delete](cli-ref-delete.md) | 置換 | すべて | パッケージ ソースからパッケージを一覧から削除するか。 |
| [init](cli-ref-init.md) | 作成 | 3.3+ | 階層構造を使用して、パッケージ ソースには、フォルダーからパッケージを追加します。 |
| [install](cli-ref-install.md) | 利用 | すべて | インストール パッケージを現在プロジェクトしますが、プロジェクトを変更したりしないファイルを参照します。 |
| [list](cli-ref-list.md) | おそらく発行の消費量 | すべて | 特定のソースからパッケージを表示します。 |
| [mirror](cli-ref-mirror.md) | 置換 | 3\.2 + で非推奨とされます。 | パッケージをターゲットのリポジトリにソースからその依存関係をミラー化します。 |
| [sources](cli-ref-sources.md) | 使用量、発行 | すべて | 構成ファイルでパッケージ ソースを管理します。 |
| [update](cli-ref-update.md) | 利用 | すべて | プロジェクトのパッケージを最新のバージョンに更新します。 Mono で実行されているときに、サポートされていません。 |

さまざまなコマンドのために使用して、さまざまな[環境変数](cli-ref-environment-variables.md)します。

適用可能なロールで NuGet CLI コマンド:

| ロール | コマンド |
| --- | --- |
| 利用 | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| 作成 | `config`, `help`, `init`, `pack`, `spec` |
| 置換 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

たとえば、開発者は、パッケージの使用のみは、NuGet コマンドのサブセットを理解する必要がありますのみ。

> [!Note]
> コマンド オプション名は大文字です。 非推奨のオプションはなど、この参照に含まれません`NoPrompt`(置き換え`NonInteractive`) と`Verbose`(置き換え`Verbosity`)。
