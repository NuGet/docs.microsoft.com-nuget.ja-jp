---
title: dotNet の NuGet コマンド |Microsoft ドキュメント
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Dotnet コマンド ライン インターフェイスを使用して NuGet に関連するコマンドの短いリファレンスです。
keywords: dotnet の NuGet コマンド、dotnet パック、dotnet 復元、dotnet nuget ローカル変数、dotnet nuget プッシュ、dotnet nuget の削除
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 352145701fba509e21e774a429d227e7427a1f0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="dotnet-commands"></a>dotNet commands

`dotnet` Windows、Mac OS X、Linux 上で実行されるコマンド ライン インターフェイスは、次に示すように不可欠 nuget.exe コマンドの数を提供します。 Dotnet がニーズを満たす場合は、使用する必要はありません`nuget.exe`です。

詳細については`dotnet`を参照してください[.NET Core コマンド ライン インターフェイス (CLI) ツール](/dotnet/core/tools/?tabs=netcore2x)です。

## <a name="package-consumption"></a>パッケージの消費量

- [**dotnet パッケージに追加**](/dotnet/core/tools/dotnet-add-package): プロジェクト ファイルへのパッケージ参照を追加し、実行`dotnet restore`パッケージをインストールします。
- [**パッケージを削除して dotnet**](/dotnet/core/tools/dotnet-remove-package): パッケージ参照をプロジェクト ファイルから削除します。
- [**dotnet 復元**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 依存関係およびプロジェクトのツールを復元します。 NuGet 4.0 の時点でと同じコードが実行されて`nuget restore`です。
- [**dotnet nuget ローカル**](/dotnet/core/tools/dotnet-nuget-locals): の場所を一覧表示、*グローバル パッケージ*、 *http キャッシュ*、および*temp*フォルダーの内容を消去し、これらのフォルダーです。

## <a name="package-creation"></a>パッケージの作成

- [**dotnet パック**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet パッケージに、コードをパックします。 NuGet 4.0 の時点でと同じコードが実行されて`nuget pack`です。
- [**dotnet nuget プッシュ**](/dotnet/core/tools/dotnet-nuget-push): サーバーにパッケージをプッシュし、公開、nuget.org、Visual Studio Team Services、およびサードパーティの NuGet のサーバーに適用します。
- [**dotnet nuget 削除**](/dotnet/core/tools/dotnet-nuget-delete): unlists nuget.org、Visual Studio Team Services、およびサードパーティの NuGet のサーバーに適用可能なホストからパッケージを削除するか。
