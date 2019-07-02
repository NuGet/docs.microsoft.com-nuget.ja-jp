---
title: dotnet CLI NuGet コマンド
description: Dotnet コマンド ライン インターフェイスを使用して NuGet に関連するコマンドの簡単なリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496480"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI コマンド

`dotnet`コマンド ライン インターフェイス (CLI)、Windows、Mac OS X、Linux で実行され、インストール、復元、およびパッケージを公開するなどの重要なコマンドのいくつか提供されます。 Dotnet はニーズを満たしている場合は、使用する必要はありません`nuget.exe`します。

これらのコマンドを使用してパッケージを使用する例については、次を参照してください。[をインストールし、dotnet CLI を使用してパッケージを管理](../consume-packages/install-use-packages-dotnet-cli.md)。 これらのコマンドを使用してパッケージを作成する例については、次を参照してください。[作成 dotnet CLI を使用してパッケージを発行および](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)します。

完全なコマンドのリファレンスで`dotnet`CLI を参照してください[.NET Core コマンド ライン インターフェイス (CLI) ツール](/dotnet/core/tools/?tabs=netcore2x)します。

## <a name="package-consumption"></a>パッケージの使用

- [**dotnet パッケージの追加**](/dotnet/core/tools/dotnet-add-package):プロジェクト ファイルにパッケージ参照を追加し、実行`dotnet restore`パッケージをインストールします。
- [**パッケージを削除して dotnet**](/dotnet/core/tools/dotnet-remove-package):プロジェクト ファイルからパッケージ参照を削除します。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):依存関係とプロジェクトのツールを復元します。 同じコードを実行する時点では NuGet 4.0 では、この`nuget restore`します。
- [**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals):場所を一覧表示、*グローバル パッケージ*、 *http キャッシュ*、および*temp*フォルダーとそれらのフォルダーの内容をクリアします。
- [**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new):作成、 [ `nuget.config` ](../reference/nuget-config-file.md) NuGet の動作を構成するファイル。

## <a name="package-creation"></a>パッケージの作成

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):NuGet パッケージにコードをパックします。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push):パッケージを NuGet サーバーに発行します。 Nuget.org には、Azure の成果物に適用できると[サード パーティの NuGet サーバー](../hosting-packages/overview.md)します。
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete):NuGet サーバーからパッケージを一覧から、または削除します。 Nuget.org には、Azure の成果物に適用できると[サード パーティの NuGet サーバー](../hosting-packages/overview.md)します。
