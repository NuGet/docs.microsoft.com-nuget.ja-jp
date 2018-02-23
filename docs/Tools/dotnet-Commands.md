---
title: "dotNet の NuGet コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Dotnet コマンド ライン インターフェイスを使用して NuGet に関連するコマンドの短いリファレンスです。"
keywords: "dotnet の NuGet コマンド、dotnet パック、dotnet 復元、dotnet nuget ローカル変数、dotnet nuget プッシュ、dotnet nuget の削除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="b1b59-104">dotNet commands</span><span class="sxs-lookup"><span data-stu-id="b1b59-104">dotNet commands</span></span>

<span data-ttu-id="b1b59-105">`dotnet` Windows、Mac OS X、Linux 上で実行されるコマンド ライン インターフェイスは、次に示すように不可欠 nuget.exe コマンドの数を提供します。</span><span class="sxs-lookup"><span data-stu-id="b1b59-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="b1b59-106">Dotnet がニーズを満たす場合は、使用する必要はありません`nuget.exe`です。</span><span class="sxs-lookup"><span data-stu-id="b1b59-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="b1b59-107">詳細については`dotnet`を参照してください[.NET Core コマンド ライン インターフェイス (CLI) ツール](/dotnet/core/tools/?tabs=netcore2x)です。</span><span class="sxs-lookup"><span data-stu-id="b1b59-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="b1b59-108">パッケージの消費量</span><span class="sxs-lookup"><span data-stu-id="b1b59-108">Package consumption</span></span>

- <span data-ttu-id="b1b59-109">[**dotnet パッケージに追加**](/dotnet/core/tools/dotnet-add-package): プロジェクト ファイルへのパッケージ参照を追加し、実行`dotnet restore`パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="b1b59-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="b1b59-110">[**パッケージを削除して dotnet**](/dotnet/core/tools/dotnet-remove-package): パッケージ参照をプロジェクト ファイルから削除します。</span><span class="sxs-lookup"><span data-stu-id="b1b59-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="b1b59-111">[**dotnet 復元**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 依存関係およびプロジェクトのツールを復元します。</span><span class="sxs-lookup"><span data-stu-id="b1b59-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="b1b59-112">NuGet 4.0 の時点でと同じコードが実行されて`nuget restore`です。</span><span class="sxs-lookup"><span data-stu-id="b1b59-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="b1b59-113">[**dotnet nuget ローカル**](/dotnet/core/tools/dotnet-nuget-locals): を消去または http 要求のキャッシュ、一時のキャッシュでは、コンピューター全体のグローバル packages フォルダーなどのローカルの NuGet リソースを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b1b59-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as the http-request cache, the temporary cache, and the machine-wide global packages folder.</span></span>

## <a name="package-creation"></a><span data-ttu-id="b1b59-114">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="b1b59-114">Package creation</span></span>

- <span data-ttu-id="b1b59-115">[**dotnet パック**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet パッケージに、コードをパックします。</span><span class="sxs-lookup"><span data-stu-id="b1b59-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="b1b59-116">NuGet 4.0 の時点でと同じコードが実行されて`nuget pack`です。</span><span class="sxs-lookup"><span data-stu-id="b1b59-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="b1b59-117">[**dotnet nuget プッシュ**](/dotnet/core/tools/dotnet-nuget-push): サーバーにパッケージをプッシュし、公開、nuget.org、Visual Studio Team Services、およびサードパーティの NuGet のサーバーに適用します。</span><span class="sxs-lookup"><span data-stu-id="b1b59-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="b1b59-118">[**dotnet nuget 削除**](/dotnet/core/tools/dotnet-nuget-delete): unlists nuget.org、Visual Studio Team Services、およびサードパーティの NuGet のサーバーに適用可能なホストからパッケージを削除するか。</span><span class="sxs-lookup"><span data-stu-id="b1b59-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
