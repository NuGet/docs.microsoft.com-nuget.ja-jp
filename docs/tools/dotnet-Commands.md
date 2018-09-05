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
# <a name="dotnet-commands"></a><span data-ttu-id="d216c-103">dotnet コマンド</span><span class="sxs-lookup"><span data-stu-id="d216c-103">dotnet commands</span></span>

<span data-ttu-id="d216c-104">`dotnet`コマンド ライン インターフェイスは、Windows、Mac OS X、Linux で実行されると、次に示すように、多数の重要な nuget.exe コマンドを提供します。</span><span class="sxs-lookup"><span data-stu-id="d216c-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="d216c-105">Dotnet はニーズを満たしている場合は、使用する必要はありません`nuget.exe`します。</span><span class="sxs-lookup"><span data-stu-id="d216c-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="d216c-106">方法の詳細について`dotnet`を参照してください[.NET Core コマンド ライン インターフェイス (CLI) ツール](/dotnet/core/tools/?tabs=netcore2x)します。</span><span class="sxs-lookup"><span data-stu-id="d216c-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="d216c-107">パッケージの使用</span><span class="sxs-lookup"><span data-stu-id="d216c-107">Package consumption</span></span>

- <span data-ttu-id="d216c-108">[**dotnet パッケージの追加**](/dotnet/core/tools/dotnet-add-package): プロジェクト ファイルにパッケージ参照を追加し、実行`dotnet restore`パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="d216c-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="d216c-109">[**パッケージを削除して dotnet**](/dotnet/core/tools/dotnet-remove-package): プロジェクト ファイルからパッケージ参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="d216c-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="d216c-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 依存関係とプロジェクトのツールを復元します。</span><span class="sxs-lookup"><span data-stu-id="d216c-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="d216c-111">同じコードを実行する時点では NuGet 4.0 では、この`nuget restore`します。</span><span class="sxs-lookup"><span data-stu-id="d216c-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="d216c-112">[**dotnet nuget ローカル**](/dotnet/core/tools/dotnet-nuget-locals): の場所を一覧表示、*グローバル パッケージ*、 *http キャッシュ*と*temp*フォルダーの内容をクリアします。これらのフォルダー。</span><span class="sxs-lookup"><span data-stu-id="d216c-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="d216c-113">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="d216c-113">Package creation</span></span>

- <span data-ttu-id="d216c-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet パッケージに、コードをパックします。</span><span class="sxs-lookup"><span data-stu-id="d216c-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="d216c-115">同じコードを実行する時点では NuGet 4.0 では、この`nuget pack`します。</span><span class="sxs-lookup"><span data-stu-id="d216c-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="d216c-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): サーバーにパッケージをプッシュして発行し、nuget.org、Visual Studio Team Services、およびサード パーティの NuGet サーバーに適用します。</span><span class="sxs-lookup"><span data-stu-id="d216c-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="d216c-117">[**dotnet nuget 削除**](/dotnet/core/tools/dotnet-nuget-delete): nuget.org、Visual Studio Team Services、およびサード パーティの NuGet サーバーに適用可能なホストからのパッケージを一覧から削除または削除します。</span><span class="sxs-lookup"><span data-stu-id="d216c-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
