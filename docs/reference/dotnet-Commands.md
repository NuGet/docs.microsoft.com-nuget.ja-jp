---
title: dotnet CLI の NuGet コマンド
description: Dotnet コマンドラインインターフェイスを使用した NuGet 関連のコマンドの短いリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327489"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI コマンド

Windows、Mac OS X、Linux で実行されるコマンドラインインターフェイス(CLI)には、パッケージのインストール、復元、発行など、いくつかの重要なコマンドが用意されています。`dotnet` Dotnet がニーズを満たす場合は、を使用`nuget.exe`する必要はありません。

これらのコマンドを使用してパッケージを使用する例については、[dotnet CLIを使用したパッケージのインストールおよび管理](../consume-packages/install-use-packages-dotnet-cli.md)を参照してください。 これらのコマンドを使用してパッケージを作成する例については、[パッケージの作成と公開 (dotnet CLI)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)を参照してください。

`dotnet`CLIの完全なコマンドリファレンスについては、[.NET Core コマンド ライン インターフェイス (CLI) ツール](/dotnet/core/tools/?tabs=netcore2x)を参照してください。

## <a name="package-consumption"></a>パッケージの使用量

- [**dotnet add package**](/dotnet/core/tools/dotnet-add-package):プロジェクト ファイルにパッケージ参照を追加し、実行`dotnet restore`パッケージをインストールします。
- [**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package):プロジェクト ファイルからパッケージ参照を削除します。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):プロジェクトの依存関係とツールを復元します。 NuGet 4.0 以降、`nuget restore` と同じコードが実行されます。
- [**dotnet nuget ローカル**](/dotnet/core/tools/dotnet-nuget-locals):*グローバルパッケージ*、 *http キャッシュ*、および*一時*フォルダーの場所を一覧表示し、それらのフォルダーの内容をクリアします。
- [**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new):NuGet の[`nuget.config`](../reference/nuget-config-file.md)動作を構成するファイルを作成します。

## <a name="package-creation"></a>パッケージの作成

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):NuGet パッケージにコードをパックします。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push):パッケージを NuGet サーバーに発行します。 Nuget.org、Azure Artifacts、および[サードパーティの nuget サーバー](../hosting-packages/overview.md)に適用されます。
- [**dotnet nuget の削除**](/dotnet/core/tools/dotnet-nuget-delete):NuGet サーバーからパッケージを削除または一覧から削除します。 Nuget.org、Azure Artifacts、および[サードパーティの nuget サーバー](../hosting-packages/overview.md)に適用されます。
