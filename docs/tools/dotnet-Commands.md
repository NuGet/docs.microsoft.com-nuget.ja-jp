---
title: dotnet CLI NuGet コマンド
description: Dotnet コマンド ライン インターフェイスを使用して NuGet に関連するコマンドの簡単なリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426004"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI コマンド

`dotnet`コマンド ライン インターフェイス (CLI)、Windows、Mac OS X、Linux で実行され、インストール、復元、およびパッケージを公開するなどの重要なコマンドのいくつか提供されます。 Dotnet はニーズを満たしている場合は、使用する必要はありません`nuget.exe`します。

これらのコマンドを使用してパッケージを使用する例については、[dotnet CLIを使用したパッケージのインストールおよび管理](../consume-packages/install-use-packages-dotnet-cli.md)を参照してください。 これらのコマンドを使用してパッケージを作成する例については、[パッケージの作成と公開 (dotnet CLI)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)を参照してください。

`dotnet`CLIの完全なコマンドリファレンスについては、[.NET Core コマンド ライン インターフェイス (CLI) ツール](/dotnet/core/tools/?tabs=netcore2x)を参照してください。

## <a name="package-consumption"></a>パッケージの使用

- [**dotnet add package**](/dotnet/core/tools/dotnet-add-package):プロジェクト ファイルにパッケージ参照を追加し、実行`dotnet restore`パッケージをインストールします。
- [**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package):プロジェクト ファイルからパッケージ参照を削除します。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):依存関係とプロジェクトのツールを復元します。 同じコードを実行する時点では NuGet 4.0 では、この`nuget restore`します。
- [**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals):場所を一覧表示、*グローバル パッケージ*、 *http キャッシュ*、および*temp*フォルダーとそれらのフォルダーの内容をクリアします。

## <a name="package-creation"></a>パッケージの作成

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):NuGet パッケージにコードをパックします。 同じコードを実行する時点では NuGet 4.0 では、この`nuget pack`します。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push):サーバーに、パッケージをプッシュし、発行し、nuget.org、Visual Studio Team Services、およびサード パーティの NuGet サーバーに適用します。
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete):Nuget.org、Visual Studio Team Services、およびサード パーティの NuGet サーバーに適用可能なホストからのパッケージを一覧から、または削除します。
