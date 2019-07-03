---
title: dotnet CLI NuGet コマンド
description: Dotnet コマンド ライン インターフェイスを使用して NuGet に関連するコマンドの簡単なリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496480"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="a1980-103">dotnet CLI コマンド</span><span class="sxs-lookup"><span data-stu-id="a1980-103">dotnet CLI commands</span></span>

<span data-ttu-id="a1980-104">`dotnet`コマンド ライン インターフェイス (CLI)、Windows、Mac OS X、Linux で実行され、インストール、復元、およびパッケージを公開するなどの重要なコマンドのいくつか提供されます。</span><span class="sxs-lookup"><span data-stu-id="a1980-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="a1980-105">Dotnet はニーズを満たしている場合は、使用する必要はありません`nuget.exe`します。</span><span class="sxs-lookup"><span data-stu-id="a1980-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="a1980-106">これらのコマンドを使用してパッケージを使用する例については、[dotnet CLIを使用したパッケージのインストールおよび管理](../consume-packages/install-use-packages-dotnet-cli.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a1980-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="a1980-107">これらのコマンドを使用してパッケージを作成する例については、[パッケージの作成と公開 (dotnet CLI)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a1980-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="a1980-108">`dotnet`CLIの完全なコマンドリファレンスについては、[.NET Core コマンド ライン インターフェイス (CLI) ツール](/dotnet/core/tools/?tabs=netcore2x)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a1980-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="a1980-109">パッケージの使用</span><span class="sxs-lookup"><span data-stu-id="a1980-109">Package consumption</span></span>

- <span data-ttu-id="a1980-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package):プロジェクト ファイルにパッケージ参照を追加し、実行`dotnet restore`パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="a1980-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="a1980-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package):プロジェクト ファイルからパッケージ参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="a1980-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="a1980-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):依存関係とプロジェクトのツールを復元します。</span><span class="sxs-lookup"><span data-stu-id="a1980-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="a1980-113">同じコードを実行する時点では NuGet 4.0 では、この`nuget restore`します。</span><span class="sxs-lookup"><span data-stu-id="a1980-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="a1980-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals):場所を一覧表示、*グローバル パッケージ*、 *http キャッシュ*、および*temp*フォルダーとそれらのフォルダーの内容をクリアします。</span><span class="sxs-lookup"><span data-stu-id="a1980-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="a1980-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new):作成、 [ `nuget.config` ](../reference/nuget-config-file.md) NuGet の動作を構成するファイル。</span><span class="sxs-lookup"><span data-stu-id="a1980-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="a1980-116">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="a1980-116">Package creation</span></span>

- <span data-ttu-id="a1980-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):NuGet パッケージにコードをパックします。</span><span class="sxs-lookup"><span data-stu-id="a1980-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="a1980-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push):パッケージを NuGet サーバーに発行します。</span><span class="sxs-lookup"><span data-stu-id="a1980-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="a1980-119">Nuget.org には、Azure の成果物に適用できると[サード パーティの NuGet サーバー](../hosting-packages/overview.md)します。</span><span class="sxs-lookup"><span data-stu-id="a1980-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="a1980-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete):NuGet サーバーからパッケージを一覧から、または削除します。</span><span class="sxs-lookup"><span data-stu-id="a1980-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="a1980-121">Nuget.org には、Azure の成果物に適用できると[サード パーティの NuGet サーバー](../hosting-packages/overview.md)します。</span><span class="sxs-lookup"><span data-stu-id="a1980-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
