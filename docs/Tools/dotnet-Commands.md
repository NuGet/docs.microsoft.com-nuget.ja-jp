---
title: "dotNet の NuGet コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Dotnet コマンド ライン インターフェイスを使用して NuGet に関連するコマンドの短いリファレンスです。"
keywords: "dotnet の NuGet コマンド、dotnet パック、dotnet 復元、dotnet nuget ローカル変数、dotnet nuget プッシュ、dotnet nuget の削除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d06e4590ab87b68e7846a13b2eba0f59eb9529d6
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="dotnet-commands"></a>dotNet commands

Windows、Mac OS X、Linux で実行され、DotNet コマンド ライン インターフェイスは、次に示すように不可欠な nuget.exe コマンドの数を提供します。 Dotnet の必要なコマンドを提供、場所、nuget.exe をダウンロードする必要はありません。

- [**dotnet パック**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet パッケージに、コードをパックします。 NuGet 4.0 の時点でと同じコードが実行されて`nuget pack`です。
- [**dotnet 復元**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 依存関係およびプロジェクトのツールを復元します。 NuGet 4.0 の時点でと同じコードが実行されて`nuget restore`です。
- [**dotnet nuget ローカル**](/dotnet/core/tools/dotnet-nuget-locals): http などのローカルの NuGet リソースは、要求を一覧表示をオフまたはキャッシュ、一時的なキャッシュ、またはコンピューター全体のグローバル packages フォルダーです。
- [**dotnet nuget プッシュ**](/dotnet/core/tools/dotnet-nuget-push): サーバーにパッケージをプッシュし、公開、nuget.org、Visual Studio Team Services、または任意のサードパーティ NuGet サーバーに適用します。
- [**dotnet nuget 削除**](/dotnet/core/tools/dotnet-nuget-delete): unlists nuget.org、Visual Studio Team Services、または任意のサードパーティ製 NuGet サーバーに適用できる、サーバーからパッケージを削除するか。
