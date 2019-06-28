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
# <a name="dotnet-cli-commands"></a><span data-ttu-id="47859-103">dotnet CLI コマンド</span><span class="sxs-lookup"><span data-stu-id="47859-103">dotnet CLI commands</span></span>

<span data-ttu-id="47859-104">`dotnet`コマンド ライン インターフェイス (CLI)、Windows、Mac OS X、Linux で実行され、インストール、復元、およびパッケージを公開するなどの重要なコマンドのいくつか提供されます。</span><span class="sxs-lookup"><span data-stu-id="47859-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="47859-105">Dotnet はニーズを満たしている場合は、使用する必要はありません`nuget.exe`します。</span><span class="sxs-lookup"><span data-stu-id="47859-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="47859-106">これらのコマンドを使用してパッケージを使用する例については、次を参照してください。[をインストールし、dotnet CLI を使用してパッケージを管理](../consume-packages/install-use-packages-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="47859-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="47859-107">これらのコマンドを使用してパッケージを作成する例については、次を参照してください [作成と dotnet CLI を使用してパッケージを発行する].。/quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="47859-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI]../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="47859-108">完全なコマンドのリファレンスで`dotnet`CLI を参照してください[.NET Core コマンド ライン インターフェイス (CLI) ツール](/dotnet/core/tools/?tabs=netcore2x)します。</span><span class="sxs-lookup"><span data-stu-id="47859-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="47859-109">パッケージの使用</span><span class="sxs-lookup"><span data-stu-id="47859-109">Package consumption</span></span>

- <span data-ttu-id="47859-110">[**dotnet パッケージの追加**](/dotnet/core/tools/dotnet-add-package):プロジェクト ファイルにパッケージ参照を追加し、実行`dotnet restore`パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="47859-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="47859-111">[**パッケージを削除して dotnet**](/dotnet/core/tools/dotnet-remove-package):プロジェクト ファイルからパッケージ参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="47859-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="47859-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):依存関係とプロジェクトのツールを復元します。</span><span class="sxs-lookup"><span data-stu-id="47859-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="47859-113">同じコードを実行する時点では NuGet 4.0 では、この`nuget restore`します。</span><span class="sxs-lookup"><span data-stu-id="47859-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="47859-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals):場所を一覧表示、*グローバル パッケージ*、 *http キャッシュ*、および*temp*フォルダーとそれらのフォルダーの内容をクリアします。</span><span class="sxs-lookup"><span data-stu-id="47859-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="47859-115">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="47859-115">Package creation</span></span>

- <span data-ttu-id="47859-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):NuGet パッケージにコードをパックします。</span><span class="sxs-lookup"><span data-stu-id="47859-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="47859-117">同じコードを実行する時点では NuGet 4.0 では、この`nuget pack`します。</span><span class="sxs-lookup"><span data-stu-id="47859-117">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="47859-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push):サーバーに、パッケージをプッシュし、発行し、nuget.org、Visual Studio Team Services、およびサード パーティの NuGet サーバーに適用します。</span><span class="sxs-lookup"><span data-stu-id="47859-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="47859-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete):Nuget.org、Visual Studio Team Services、およびサード パーティの NuGet サーバーに適用可能なホストからのパッケージを一覧から、または削除します。</span><span class="sxs-lookup"><span data-stu-id="47859-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
