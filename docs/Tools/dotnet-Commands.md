---
title: dotnet の NuGet コマンド
description: Dotnet コマンド ライン インターフェイスを使用して NuGet に関連するコマンドの短いリファレンスです。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2018
---
# <a name="dotnet-commands"></a>dotnet コマンド

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
