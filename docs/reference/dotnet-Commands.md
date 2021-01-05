---
title: dotnet CLI の NuGet コマンド
description: Dotnet コマンドラインインターフェイスを使用した NuGet 関連のコマンドの短いリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 87cb3c8153931a0917338de9f7001406b5e12dfc
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699829"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="1611b-103">dotnet CLI コマンド</span><span class="sxs-lookup"><span data-stu-id="1611b-103">dotnet CLI commands</span></span>

<span data-ttu-id="1611b-104">`dotnet`Windows、Mac OS X、Linux で実行されるコマンドラインインターフェイス (CLI) には、パッケージのインストール、復元、発行など、いくつかの重要なコマンドが用意されています。</span><span class="sxs-lookup"><span data-stu-id="1611b-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="1611b-105">Dotnet がニーズを満たす場合は、を使用する必要はありません `nuget.exe` 。</span><span class="sxs-lookup"><span data-stu-id="1611b-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="1611b-106">これらのコマンドを使用してパッケージを使用する例については、「 [DOTNET CLI を使用したパッケージのインストールと管理](../consume-packages/install-use-packages-dotnet-cli.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1611b-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="1611b-107">これらのコマンドを使用してパッケージを作成する例については、「 [DOTNET CLI を使用したパッケージの作成と発行](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1611b-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="1611b-108">Cli の完全なコマンドリファレンスについ `dotnet` ては、「 [.net Core コマンドラインインターフェイス (cli) ツール](/dotnet/core/tools/?tabs=netcore2x)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1611b-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="1611b-109">パッケージの使用量</span><span class="sxs-lookup"><span data-stu-id="1611b-109">Package consumption</span></span>

- <span data-ttu-id="1611b-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): プロジェクトファイルにパッケージ参照を追加し、を実行し `dotnet restore` てパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="1611b-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="1611b-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): プロジェクトファイルからパッケージ参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="1611b-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="1611b-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): プロジェクトの依存関係とツールを復元します。</span><span class="sxs-lookup"><span data-stu-id="1611b-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="1611b-113">NuGet 4.0 以降、`nuget restore` と同じコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="1611b-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="1611b-114">[**dotnet nuget ローカル**](/dotnet/core/tools/dotnet-nuget-locals): *グローバルパッケージ*、 *http キャッシュ*、および *一時* フォルダーの場所を一覧表示し、それらのフォルダーの内容を消去します。</span><span class="sxs-lookup"><span data-stu-id="1611b-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="1611b-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): [`nuget.config`](../reference/nuget-config-file.md) NuGet の動作を構成するファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="1611b-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="1611b-116">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="1611b-116">Package creation</span></span>

- <span data-ttu-id="1611b-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet パッケージにコードをパックします。</span><span class="sxs-lookup"><span data-stu-id="1611b-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="1611b-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): nuget サーバーにパッケージを発行します。</span><span class="sxs-lookup"><span data-stu-id="1611b-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="1611b-119">Nuget.org、Azure Artifacts、および [サードパーティの nuget サーバー](../hosting-packages/overview.md)に適用されます。</span><span class="sxs-lookup"><span data-stu-id="1611b-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="1611b-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): nuget サーバーからパッケージを削除または一覧から削除します。</span><span class="sxs-lookup"><span data-stu-id="1611b-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="1611b-121">Nuget.org、Azure Artifacts、および [サードパーティの nuget サーバー](../hosting-packages/overview.md)に適用されます。</span><span class="sxs-lookup"><span data-stu-id="1611b-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="1611b-122">[**dotnet nuget verify**](/dotnet/core/tools/dotnet-nuget-verify): 署名済みの nuget パッケージを検証します。</span><span class="sxs-lookup"><span data-stu-id="1611b-122">[**dotnet nuget verify**](/dotnet/core/tools/dotnet-nuget-verify): Verifies a signed NuGet package.</span></span>
