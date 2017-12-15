---
title: "dotNet の NuGet コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Dotnet コマンド ライン インターフェイスを使用して NuGet に関連するコマンドの短いリファレンスです。"
keywords: "dotnet の NuGet コマンド、dotnet パック、dotnet 復元、dotnet nuget ローカル変数、dotnet nuget プッシュ、dotnet nuget の削除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a>dotNet コマンド

Windows、Mac OS X、Linux で実行され、DotNet コマンド ライン インターフェイスは、次に示すように不可欠な nuget.exe コマンドの数を提供します。 Dotnet の必要なコマンドを提供、場所、nuget.exe をダウンロードする必要はありません。

- [**dotnet パック**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NETCore SDK 用のコードをプロジェクト パック NuGet パッケージにします。 その他のすべてのプロジェクトの種類を使用する必要があります。[`nuget pack`](cli-ref-pack.md)
- [**dotnet 復元**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 依存関係およびプロジェクトのツールを復元します。 NuGet 4.0 の時点でと同じコードが実行されて`nuget restore`です。
- [**dotnet nuget ローカル**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): http などのローカルの NuGet リソースは、要求を一覧表示をオフまたはキャッシュ、一時的なキャッシュ、またはコンピューター全体のグローバル packages フォルダーです。
- [**dotnet nuget プッシュ**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): サーバーにパッケージをプッシュし、公開、nuget.org、Visual Studio Team Services、または任意のサードパーティ NuGet サーバーに適用します。
- [**dotnet nuget 削除**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): unlists nuget.org、Visual Studio Team Services、または任意のサードパーティ製 NuGet サーバーに適用できる、サーバーからパッケージを削除するか。
