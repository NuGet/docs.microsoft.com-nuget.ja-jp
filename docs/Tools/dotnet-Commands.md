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
# <a name="dotnet-commands"></a><span data-ttu-id="c20b2-104">dotNet コマンド</span><span class="sxs-lookup"><span data-stu-id="c20b2-104">dotNet commands</span></span>

<span data-ttu-id="c20b2-105">Windows、Mac OS X、Linux で実行され、DotNet コマンド ライン インターフェイスは、次に示すように不可欠な nuget.exe コマンドの数を提供します。</span><span class="sxs-lookup"><span data-stu-id="c20b2-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="c20b2-106">Dotnet の必要なコマンドを提供、場所、nuget.exe をダウンロードする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="c20b2-106">Where dotnet provides the desired commands, it is not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="c20b2-107">[**dotnet パック**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NETCore SDK 用のコードをプロジェクト パック NuGet パッケージにします。</span><span class="sxs-lookup"><span data-stu-id="c20b2-107">[**dotnet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs code for NETCore SDK projects into a NuGet package.</span></span> <span data-ttu-id="c20b2-108">その他のすべてのプロジェクトの種類を使用する必要があります。[`nuget pack`](cli-ref-pack.md)</span><span class="sxs-lookup"><span data-stu-id="c20b2-108">All other project types should use [`nuget pack`](cli-ref-pack.md)</span></span>
- <span data-ttu-id="c20b2-109">[**dotnet 復元**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 依存関係およびプロジェクトのツールを復元します。</span><span class="sxs-lookup"><span data-stu-id="c20b2-109">[**dotnet restore**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="c20b2-110">NuGet 4.0 の時点でと同じコードが実行されて`nuget restore`です。</span><span class="sxs-lookup"><span data-stu-id="c20b2-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="c20b2-111">[**dotnet nuget ローカル**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): http などのローカルの NuGet リソースは、要求を一覧表示をオフまたはキャッシュ、一時的なキャッシュ、またはコンピューター全体のグローバル packages フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="c20b2-111">[**dotnet nuget locals**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="c20b2-112">[**dotnet nuget プッシュ**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): サーバーにパッケージをプッシュし、公開、nuget.org、Visual Studio Team Services、または任意のサードパーティ NuGet サーバーに適用します。</span><span class="sxs-lookup"><span data-stu-id="c20b2-112">[**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="c20b2-113">[**dotnet nuget 削除**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): unlists nuget.org、Visual Studio Team Services、または任意のサードパーティ製 NuGet サーバーに適用できる、サーバーからパッケージを削除するか。</span><span class="sxs-lookup"><span data-stu-id="c20b2-113">[**dotnet nuget delete**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
