---
title: NuGet Command-Line Interface (CLI) リファレンス
description: nuget.exe CLI のコマンドラインリファレンスインデックス
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a9a5fc4d3b1e0f19fa3ea249ca7759c8ebc2d12e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777709"
---
# <a name="nuget-cli-reference"></a>NuGet CLI リファレンス

NuGet コマンドラインインターフェイス (CLI) は、 `nuget.exe` プロジェクトファイルを変更することなく、パッケージをインストール、作成、発行、および管理するためのすべての nuget 機能を提供します。

任意のコマンドを使用するには、コマンドウィンドウまたは bash シェルを開き、を実行し `nuget` た後、コマンドと、 `nuget help pack` (パックコマンドのヘルプを表示する) などの適切なオプションを実行します。

このドキュメントには、最新バージョンの NuGet CLI が反映されています。 使用している特定のバージョンの詳細については、目的のコマンドを実行して `nuget help` ください。

`nuget.exe` CLI で基本的なコマンドを使用する方法を学習するには、[nuget.exe CLI を使用したパッケージのインストールと使用](../consume-packages/install-use-packages-nuget-cli.md)に関するページを参照してください。

## <a name="installing-nugetexe"></a>nuget.exe のインストール

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Visual Studio のパッケージマネージャーコンソール内で NuGet CLI を使用できるようにする方法については、「 [コンソールでの nuget.exe CLI の使用](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console)」を参照してください。

## <a name="availability"></a>可用性

詳細については、「 [機能の可用性](../install-nuget-client-tools.md#feature-availability) 」を参照してください。

- Windows では、すべてのコマンドを使用できます。
- 、、およびに対して指定されている場合を除き、すべてのコマンドが Mono で実行される nuget.exe で動作 `pack` `restore` `update` します。
- 、、、 `pack` `restore` 、およびの各 `delete` `locals` `push` コマンドは、dotnet CLI を使用して Mac および Linux でも使用できます。

## <a name="commands-and-applicability"></a>コマンドと適用性

パッケージの作成、パッケージの使用、ホストへのパッケージの発行など、利用可能なコマンドと適用性。

| 一般的なコマンド | 適用可能な役割 | NuGet のバージョン | 説明 |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | 作成 | 2.7 以降 | またはプロジェクトファイルから NuGet パッケージを作成し `.nuspec` ます。 Mono で実行する場合、プロジェクトファイルからパッケージを作成することはサポートされていません。 |
| [push](cli-reference/cli-ref-push.md) | 発行 | すべて | パッケージをパッケージソースに発行します。 |
| [config](cli-reference/cli-ref-config.md) | すべて | すべて | NuGet 構成値を取得または設定します。 |
| [help or ?](cli-reference/cli-ref-help.md) | すべて | すべて | コマンドのヘルプ情報またはヘルプを表示します。 |
| [locals](cli-reference/cli-ref-locals.md) | 従量課金 | 3.3 + | *グローバルパッケージ*、 *http キャッシュ*、および *一時* フォルダーの場所を一覧表示し、それらのフォルダーの内容をクリアします。 |
| [restore](cli-reference/cli-ref-restore.md) | 従量課金 | 2.7 以降 | 使用中のパッケージ管理形式で参照されているすべてのパッケージを復元します。 Mono で実行する場合、PackageReference 形式を使用したパッケージの復元はサポートされていません。 |
| [setapikey](cli-reference/cli-ref-setapikey.md) | 発行、消費 | すべて | パッケージソースがアクセスのためにキーを必要とする場合に、指定されたパッケージソースの API キーを保存します。 |
| [spec](cli-reference/cli-ref-spec.md) | 作成 | すべて | `.nuspec`Visual Studio プロジェクトからファイルを生成する場合、トークンを使用してファイルを生成します。 |

| セカンダリコマンド | 適用可能な役割 | NuGet のバージョン | 説明 |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | 発行 | 3.3 + | 階層レイアウトを使用して、非 HTTP パッケージソースにパッケージを追加します。 HTTP ソースの場合は、 *push* を使用します。 |
| [delete](cli-reference/cli-ref-delete.md) | 発行 | すべて | パッケージソースからパッケージを削除または一覧から削除します。 |
| [init](cli-reference/cli-ref-init.md) | 作成 | 3.3 + | 階層レイアウトを使用して、フォルダーからパッケージソースにパッケージを追加します。 |
| [install](cli-reference/cli-ref-install.md) | 従量課金 | すべて | 現在のプロジェクトにパッケージをインストールしますが、プロジェクトや参照ファイルは変更しません。 |
| [list](cli-reference/cli-ref-list.md) | 消費 (おそらく発行) | すべて | 指定されたソースからのパッケージを表示します。 |
| [mirror](cli-reference/cli-ref-mirror.md) | 発行 | 3.2 + で非推奨 | パッケージとその依存関係をソースからターゲットリポジトリにミラー化します。 |
| [search](cli-reference/cli-ref-search.md) | 従量課金 | 5.8 + | 指定されたクエリ文字列を使用して、指定されたソースを検索します。 |
| [sources](cli-reference/cli-ref-sources.md) | 消費、発行 | すべて | 構成ファイルのパッケージソースを管理します。 |
| [update](cli-reference/cli-ref-update.md) | 従量課金 | すべて | プロジェクトのパッケージを、使用可能な最新バージョンに更新します。 Mono で実行する場合はサポートされません。 |

さまざまなコマンドによって、さまざまな [環境変数](cli-reference/cli-ref-environment-variables.md)が使用できます。

適用可能なロール別の NuGet CLI コマンド:

| Role | コマンド |
| --- | --- |
| 従量課金 | `config`, `help`, `install`, `list`, `locals`, `restore`, `search`, `setapikey`, `sources`, `update` |
| 作成 | `config`, `help`, `init`, `pack`, `spec` |
| 発行 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

たとえば、パッケージの使用のみを懸念している開発者は、NuGet コマンドのサブセットのみを理解する必要があります。

> [!Note]
> コマンドオプション名では大文字と小文字が区別されません。 非推奨のオプションは、この参照には含まれません `NoPrompt` (で置き換えられる `NonInteractive` ) と `Verbose` (によって置き換えられ `Verbosity` ます)。
