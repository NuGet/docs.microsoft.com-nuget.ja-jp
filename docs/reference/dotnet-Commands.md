---
title: dotnet CLI の NuGet コマンド
description: Dotnet コマンドラインインターフェイスを使用した NuGet 関連のコマンドの短いリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 87cb3c8153931a0917338de9f7001406b5e12dfc
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699829"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI コマンド

`dotnet`Windows、Mac OS X、Linux で実行されるコマンドラインインターフェイス (CLI) には、パッケージのインストール、復元、発行など、いくつかの重要なコマンドが用意されています。 Dotnet がニーズを満たす場合は、を使用する必要はありません `nuget.exe` 。

これらのコマンドを使用してパッケージを使用する例については、「 [DOTNET CLI を使用したパッケージのインストールと管理](../consume-packages/install-use-packages-dotnet-cli.md)」を参照してください。 これらのコマンドを使用してパッケージを作成する例については、「 [DOTNET CLI を使用したパッケージの作成と発行](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)」を参照してください。

Cli の完全なコマンドリファレンスについ `dotnet` ては、「 [.net Core コマンドラインインターフェイス (cli) ツール](/dotnet/core/tools/?tabs=netcore2x)」を参照してください。

## <a name="package-consumption"></a>パッケージの使用量

- [**dotnet add package**](/dotnet/core/tools/dotnet-add-package): プロジェクトファイルにパッケージ参照を追加し、を実行し `dotnet restore` てパッケージをインストールします。
- [**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): プロジェクトファイルからパッケージ参照を削除します。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): プロジェクトの依存関係とツールを復元します。 NuGet 4.0 以降、`nuget restore` と同じコードが実行されます。
- [**dotnet nuget ローカル**](/dotnet/core/tools/dotnet-nuget-locals): *グローバルパッケージ*、 *http キャッシュ*、および *一時* フォルダーの場所を一覧表示し、それらのフォルダーの内容を消去します。
- [**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): [`nuget.config`](../reference/nuget-config-file.md) NuGet の動作を構成するファイルを作成します。

## <a name="package-creation"></a>パッケージの作成

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet パッケージにコードをパックします。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): nuget サーバーにパッケージを発行します。 Nuget.org、Azure Artifacts、および [サードパーティの nuget サーバー](../hosting-packages/overview.md)に適用されます。
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): nuget サーバーからパッケージを削除または一覧から削除します。 Nuget.org、Azure Artifacts、および [サードパーティの nuget サーバー](../hosting-packages/overview.md)に適用されます。
- [**dotnet nuget verify**](/dotnet/core/tools/dotnet-nuget-verify): 署名済みの nuget パッケージを検証します。
