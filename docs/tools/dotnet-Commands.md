---
title: dotnet NuGet コマンド
description: Dotnet コマンド ライン インターフェイスを使用して NuGet に関連するコマンドの簡単なリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546317"
---
# <a name="dotnet-commands"></a>dotnet コマンド

`dotnet`コマンド ライン インターフェイスは、Windows、Mac OS X、Linux で実行されると、次に示すように、多数の重要な nuget.exe コマンドを提供します。 Dotnet はニーズを満たしている場合は、使用する必要はありません`nuget.exe`します。

方法の詳細について`dotnet`を参照してください[.NET Core コマンド ライン インターフェイス (CLI) ツール](/dotnet/core/tools/?tabs=netcore2x)します。

## <a name="package-consumption"></a>パッケージの使用

- [**dotnet パッケージの追加**](/dotnet/core/tools/dotnet-add-package): プロジェクト ファイルにパッケージ参照を追加し、実行`dotnet restore`パッケージをインストールします。
- [**パッケージを削除して dotnet**](/dotnet/core/tools/dotnet-remove-package): プロジェクト ファイルからパッケージ参照を削除します。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 依存関係とプロジェクトのツールを復元します。 同じコードを実行する時点では NuGet 4.0 では、この`nuget restore`します。
- [**dotnet nuget ローカル**](/dotnet/core/tools/dotnet-nuget-locals): の場所を一覧表示、*グローバル パッケージ*、 *http キャッシュ*と*temp*フォルダーの内容をクリアします。これらのフォルダー。

## <a name="package-creation"></a>パッケージの作成

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet パッケージに、コードをパックします。 同じコードを実行する時点では NuGet 4.0 では、この`nuget pack`します。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): サーバーにパッケージをプッシュして発行し、nuget.org、Visual Studio Team Services、およびサード パーティの NuGet サーバーに適用します。
- [**dotnet nuget 削除**](/dotnet/core/tools/dotnet-nuget-delete): nuget.org、Visual Studio Team Services、およびサード パーティの NuGet サーバーに適用可能なホストからのパッケージを一覧から削除または削除します。
