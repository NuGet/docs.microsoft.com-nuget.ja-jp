---
title: "NuGet クライアント ツールのインストール | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Visual Studio 用にクライアント ツール、コマンド ライン インターフェイス (CLI)、およびパッケージ マネージャーをインストールするためのガイダンス。"
keywords: "nuget.exe CLI、NuGet クライアント ツール、NuGet パッケージ マネージャー、NuGet パッケージ マネージャー コンソール、Visual Studio 用 NuGet、NuGet ベータ チャネル"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="8a7df-104">NuGet クライアント ツールのインストール</span><span class="sxs-lookup"><span data-stu-id="8a7df-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="8a7df-105"> **パッケージをインストールする場合は、[クイック スタート: パッケージを使用する](../Quickstart/Use-a-Package.md)をご覧ください。**</span><span class="sxs-lookup"><span data-stu-id="8a7df-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="8a7df-106">NuGet パッケージの構築、公開、使用に使用できる次の 2 つの主要なツールがあります。</span><span class="sxs-lookup"><span data-stu-id="8a7df-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="8a7df-107">[**NuGet CLI**](#nuget-cli) は、すべての NuGet 機能を提供する Windows 用のコマンド ライン ユーティリティです。Mono を使用、または .NET Core CLI (`dotnet`) を通じて、Mac OSX および Linux でも実行できます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="8a7df-108">[**Visual Studio での NuGet パッケージ マネージャー**](#nuget-package-manager-in-visual-studio) (Windows のみ) は、パッケージを管理するための GUI ツールで、PowerShell コンソールが含まれており、これを通じて Visual Studio 内で直接、特定の NuGet コマンドを使用できます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="8a7df-109">パッケージ マネージャーの UI とコンソールはどちらも Visual Studio (Windows) 2012 以降に含まれており、それより前のバージョンには手動でインストールできます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="8a7df-110">Visual Studio for Mac には、NuGet の機能が直接、組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="8a7df-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="8a7df-111">チュートリアルについては、「[プロジェクトに NuGet パッケージを含める](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="8a7df-111">See [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="8a7df-112">現時点では Visual Studio Code には組み込みの NuGet のサポートはありません。</span><span class="sxs-lookup"><span data-stu-id="8a7df-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="8a7df-113">NuGet CLI または [dotnet CLI](../Tools/dotnet-Commands.md) を使用してください。</span><span class="sxs-lookup"><span data-stu-id="8a7df-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="8a7df-114">NuGet CLI とパッケージ マネージャーは、どちらも次の操作をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="8a7df-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="8a7df-115">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="8a7df-115">Search packages</span></span>
- <span data-ttu-id="8a7df-116">パッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="8a7df-116">Install packages</span></span>
- <span data-ttu-id="8a7df-117">パッケージの更新</span><span class="sxs-lookup"><span data-stu-id="8a7df-117">Update packages</span></span>
- <span data-ttu-id="8a7df-118">パッケージのアンインストール</span><span class="sxs-lookup"><span data-stu-id="8a7df-118">Uninstall packages</span></span>
- <span data-ttu-id="8a7df-119">パッケージの復元 (パッケージ マネージャーの UI のみ)</span><span class="sxs-lookup"><span data-stu-id="8a7df-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="8a7df-120">NuGet ソースの管理</span><span class="sxs-lookup"><span data-stu-id="8a7df-120">Manage NuGet sources</span></span>

<span data-ttu-id="8a7df-121">次の機能は、NuGet CLI でのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="8a7df-122">パッケージの管理 (nuget.org またはプライベート フィード)</span><span class="sxs-lookup"><span data-stu-id="8a7df-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="8a7df-123">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="8a7df-123">Create packages</span></span> 
- <span data-ttu-id="8a7df-124">パッケージの公開</span><span class="sxs-lookup"><span data-stu-id="8a7df-124">Publish packages</span></span>
- <span data-ttu-id="8a7df-125">Nuget.Config の管理</span><span class="sxs-lookup"><span data-stu-id="8a7df-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="8a7df-126">NuGet のキャッシュの管理</span><span class="sxs-lookup"><span data-stu-id="8a7df-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="8a7df-127">パッケージのレプリケート</span><span class="sxs-lookup"><span data-stu-id="8a7df-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="8a7df-128">もう 1 つの優れたツールは、[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)です。NuGet パッケージを視覚的に調査、作成、および編集する、オープン ソースのスタンドアロン ツールです。</span><span class="sxs-lookup"><span data-stu-id="8a7df-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="8a7df-129">このツールを使用すると、たとえば、パッケージ構造に実験的な変更を加えるたびに、パッケージをリビルドする必要がないため、非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="8a7df-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="8a7df-130">.NET Core アプリケーションの開発に使用されるクロス プラットフォーム [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) ツールチェーンは、delete、locals、push、pack、および restore など、複数の NuGet コマンドをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="8a7df-130">The cross-platform [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="8a7df-131">NuGet CLI</span><span class="sxs-lookup"><span data-stu-id="8a7df-131">NuGet CLI</span></span>

<span data-ttu-id="8a7df-132">NuGet コマンド ライン インターフェイスは、すべての NuGet 機能へのアクセスを提供し、以降のセクションで説明するように、Windows、Mac OSX および Linux で実行できます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="8a7df-133">Windows</span><span class="sxs-lookup"><span data-stu-id="8a7df-133">Windows</span></span>

<span data-ttu-id="8a7df-134">**直接ダウンロード:**</span><span class="sxs-lookup"><span data-stu-id="8a7df-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="8a7df-135">NuGet 1.4 以降では、`nuget update -self` を使用して既存の nuget.exe を最新バージョンに更新できます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="8a7df-136">**その他のメソッド:**</span><span class="sxs-lookup"><span data-stu-id="8a7df-136">**Other methods:**</span></span>

- <span data-ttu-id="8a7df-137">**Chocolatey**: [Chocolatey](http://chocolatey.org) クライアントを使用して、[NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="8a7df-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="8a7df-138">**Visual Studio**: Visual Studio のパッケージ マネージャー コンソールから [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="8a7df-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="8a7df-139">**NuGet 2.x ユーザーの場合**: NuGet 3.2 で導入された互換性に影響する変更点により、継続的なインテグレーション システムが中断される可能性を防止するため、[https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) は最新の安定した NuGet 2.x リリースをポイントします。</span><span class="sxs-lookup"><span data-stu-id="8a7df-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="8a7df-140">Mac OSX および Linux</span><span class="sxs-lookup"><span data-stu-id="8a7df-140">Mac OSX and Linux</span></span>

<span data-ttu-id="8a7df-141">Mac OSX および Linux では、次の 2 つの方法で NuGet CLI を実行できます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="8a7df-142">NuGet のコア機能を含む [.NET Core SDK](https://www.microsoft.com/net/download/core) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="8a7df-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="8a7df-143">ダウンロードが [github.com/dotnet/cli](https://github.com/dotnet/cli) にも一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="8a7df-144">より多くの機能が必要な場合は、次の 2 番目のオプションを使用して、Mono で `nuget.exe` を使用します。</span><span class="sxs-lookup"><span data-stu-id="8a7df-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="8a7df-145">[Mono](http://www.mono-project.com/docs/getting-started/install/) をインストールし、[nuget.org/downloads](https://nuget.org/downloads) から、Windows の `nuget.exe` コマンドライン実行可能ファイル (バージョン 3.2 以降) を使用します。</span><span class="sxs-lookup"><span data-stu-id="8a7df-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="8a7df-146">Mono で NuGet を実行する場合、次の制限があります。</span><span class="sxs-lookup"><span data-stu-id="8a7df-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="8a7df-147">テスト済みのコマンド:</span><span class="sxs-lookup"><span data-stu-id="8a7df-147">Commands tested to work:</span></span>
        - <span data-ttu-id="8a7df-148">.config</span><span class="sxs-lookup"><span data-stu-id="8a7df-148">config</span></span>
        - <span data-ttu-id="8a7df-149">削除</span><span class="sxs-lookup"><span data-stu-id="8a7df-149">delete</span></span>
        - <span data-ttu-id="8a7df-150">help</span><span class="sxs-lookup"><span data-stu-id="8a7df-150">help</span></span>
        - <span data-ttu-id="8a7df-151">install</span><span class="sxs-lookup"><span data-stu-id="8a7df-151">install</span></span>
        - <span data-ttu-id="8a7df-152">リスト</span><span class="sxs-lookup"><span data-stu-id="8a7df-152">list</span></span>
        - <span data-ttu-id="8a7df-153">push</span><span class="sxs-lookup"><span data-stu-id="8a7df-153">push</span></span>
        - <span data-ttu-id="8a7df-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="8a7df-154">setApiKey</span></span>
        - <span data-ttu-id="8a7df-155">sources</span><span class="sxs-lookup"><span data-stu-id="8a7df-155">sources</span></span>
        - <span data-ttu-id="8a7df-156">spec</span><span class="sxs-lookup"><span data-stu-id="8a7df-156">spec</span></span>

    - <span data-ttu-id="8a7df-157">部分的に機能するコマンド:</span><span class="sxs-lookup"><span data-stu-id="8a7df-157">Partially-working commands:</span></span>
        - <span data-ttu-id="8a7df-158">pack: `.nuspec` ファイルでは機能しますが、プロジェクト ファイルでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="8a7df-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="8a7df-159">restore: `packages.config` ファイルと `project.json` ファイルでは機能しますが、ソリューション (`.sln`) ファイルでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="8a7df-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="8a7df-160">機能しないコマンド:</span><span class="sxs-lookup"><span data-stu-id="8a7df-160">Commands that do not work:</span></span>
        - <span data-ttu-id="8a7df-161">更新</span><span class="sxs-lookup"><span data-stu-id="8a7df-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="8a7df-162">関連トピック</span><span class="sxs-lookup"><span data-stu-id="8a7df-162">Related topics</span></span>

- [<span data-ttu-id="8a7df-163">NuGet CLI リファレンス</span><span class="sxs-lookup"><span data-stu-id="8a7df-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="8a7df-164">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="8a7df-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="8a7df-165">パッケージの公開</span><span class="sxs-lookup"><span data-stu-id="8a7df-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="8a7df-166">Visual Studio の NuGet パッケージ マネージャー</span><span class="sxs-lookup"><span data-stu-id="8a7df-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="8a7df-167">NuGet パッケージ マネージャーは、Windows の Visual Studio 2012 以降のすべてのエディションに含まれます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="8a7df-168">これにはパッケージ マネージャー UI ([参照](../tools/package-manager-ui.md)) と、特定のパッケージに付属するツールにアクセスできるパッケージ マネージャー コンソール ([参照](../tools/package-manager-console.md)) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8a7df-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="8a7df-169">Visual Studio 2017 インストーラーには、NuGet パッケージ マネージャーと .NET を使用するすべてのワークロードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="8a7df-170">個別にインストール、またはパッケージ マネージャーがインストールされていることを確認するには、Visual Studio 2017 インストーラーを実行し、**[個別のコンポーネント] > [コード ツール] > [NuGet パッケージ マネージャー]** の下でオプションを確認します。</span><span class="sxs-lookup"><span data-stu-id="8a7df-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="8a7df-171">コンソールには [PowerShell 2.0](http://support.microsoft.com/kb/968929) が必要です。これは、Windows 7 以降と Windows Server 2008 R2 以降では既にインストールされています。</span><span class="sxs-lookup"><span data-stu-id="8a7df-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="8a7df-172">パッケージ マネージャー コンソールのコマンドも、Windows の Visual Studio 内でのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="8a7df-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="8a7df-173">Visual Studio for Mac および Visual Studio Code を含む、その環境の外部で NuGet CLI を使用します。</span><span class="sxs-lookup"><span data-stu-id="8a7df-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="8a7df-174">Visual Studio 2010 以前のパッケージ マネージャーのインストール</span><span class="sxs-lookup"><span data-stu-id="8a7df-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="8a7df-175">*この手順は、パッケージ マネージャーが既に含まれている Visual Studio 2012 以降では必要ありません。*</span><span class="sxs-lookup"><span data-stu-id="8a7df-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="8a7df-176">Visual Studio 2010 以前では、**[ツール] > [拡張機能と更新プログラム]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="8a7df-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="8a7df-177">**[オンライン]** に移動し、"Visual Studio 用 NuGet パッケージ マネージャー" を検索し、**[ダウンロード]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8a7df-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="8a7df-178">[インストーラー] ダイアログ ボックスで、**[インストール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8a7df-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="8a7df-179">インストールが完了したら、Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="8a7df-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="8a7df-180">Visual Studio で **[拡張機能と更新プログラム]** ダイアログが使用できない (たとえばプロキシによってブロックされている) 場合は、[https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) で Visual Studio 2013 および 2015 の拡張機能を直接、ダウンロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="8a7df-181">パッケージ マネージャーの更新</span><span class="sxs-lookup"><span data-stu-id="8a7df-181">Updating the Package Manager</span></span>

<span data-ttu-id="8a7df-182">Visual Studio 2015 Update 2 以降では、パッケージ マネージャーが最新の安定版リリースに自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="8a7df-183">Visual Studio 2015 Update 1 以前では、**[ツール] > [拡張機能と更新プログラム]** コマンドを選択し、**[更新]** タブをクリックして、パッケージ マネージャーの新しいバージョンが使用可能かどうかを確認してください。</span><span class="sxs-lookup"><span data-stu-id="8a7df-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="8a7df-184">NuGet のプレビュー</span><span class="sxs-lookup"><span data-stu-id="8a7df-184">NuGet previews</span></span>

<span data-ttu-id="8a7df-185">リリース予定の NuGet の機能をプレビューしたい場合は、[Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/) をインストールします。これは、Visual Studio の安定版リリースと同時に実行できます。</span><span class="sxs-lookup"><span data-stu-id="8a7df-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="8a7df-186">Visual Studio 2015 用の以前の NuGet のベータ チャネル (`https://dotnet.myget.org/F/nuget-beta/vsix/`) は、使用されていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8a7df-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="8a7df-187">NuGet の任意のリリースの問題を報告したり、アイデアを共有するには、[NuGet GitHub リポジトリ](https://github.com/Nuget/Home)で懸案事項を作成します。</span><span class="sxs-lookup"><span data-stu-id="8a7df-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="8a7df-188">関連トピック</span><span class="sxs-lookup"><span data-stu-id="8a7df-188">Related topics</span></span>

- [<span data-ttu-id="8a7df-189">パッケージ マネージャー UI のリファレンス</span><span class="sxs-lookup"><span data-stu-id="8a7df-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="8a7df-190">パッケージ マネージャー コンソールのリファレンス</span><span class="sxs-lookup"><span data-stu-id="8a7df-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="8a7df-191">パッケージ マネージャー コンソール PowerShell のリファレンス</span><span class="sxs-lookup"><span data-stu-id="8a7df-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)