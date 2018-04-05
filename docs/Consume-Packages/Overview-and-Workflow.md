---
title: NuGet パッケージの使用の概要とワークフロー | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/22/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: プロジェクトで NuGet パッケージを利用する場合のプロセスの概要と、プロセスの他の特定の部分へのリンク。
keywords: NuGet パッケージの利用, NuGet 利用の概要, NuGet 利用のワークフロー, パッケージ利用のワークフロー, パッケージ利用の概要
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e79b09fe8131f25c6bbed650e1927425dcc5d409
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="package-consumption-workflow"></a><span data-ttu-id="b4834-104">パッケージ利用のワークフロー</span><span class="sxs-lookup"><span data-stu-id="b4834-104">Package consumption workflow</span></span>

<span data-ttu-id="b4834-105">nuget.org と組織が確立する可能性のあるプライベート パッケージ ギャラリーの間で、アプリとサービスで使用する数万の非常に有用なパッケージを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="b4834-105">Between nuget.org and private package galleries that your organization might establish, you can find tens of thousands of highly useful packages to use in your apps and services.</span></span> <span data-ttu-id="b4834-106">ただし、ソースに関係なく、パッケージを利用する場合は一般的なワークフローに従います。</span><span class="sxs-lookup"><span data-stu-id="b4834-106">But regardless of the source, consuming a package follows the same general workflow.</span></span>

![パッケージ ソースへの移動、パッケージの検索、プロジェクトへのインストール、パッケージ API への using ステートメントと呼び出しの追加を示すフロー](media/Overview-01-GeneralFlow.png)

<span data-ttu-id="b4834-108">"\* _Visual Studio および dotnet.ex\` のみ。nuget インストール コマンドは、プロジェクト ファイルまたは packages.config を変更しません。エントリは、手動で管理する必要があります。_"</span><span class="sxs-lookup"><span data-stu-id="b4834-108">\* _Visual Studio and dotnet.ex\` only. The nuget install command does not modify project files or packages.config; entries must be managed manually._</span></span>

<span data-ttu-id="b4834-109">詳細については、「[プロジェクトの NuGet パッケージの検索と評価](../consume-packages/finding-and-choosing-packages.md)」および「[Different ways to install a NuGet package](ways-to-install-a-package.md)」(NuGet パッケージをインストールするためのさまざまな方法) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b4834-109">For further details, see [Finding and Choosing Packages](../consume-packages/finding-and-choosing-packages.md) and [Different ways to install a NuGet package](ways-to-install-a-package.md).</span></span>

<span data-ttu-id="b4834-110">NuGet は、インストールされている各パッケージの ID とバージョン番号を記憶し、プロジェクトの種類と使用している NuGet のバージョンに応じて、[`packages.config`](../reference/packages-config.md) またはプロジェクト ファイル ([PackageReference](../consume-packages/package-references-in-project-files.md) を使用) のいずれかに記録します。</span><span class="sxs-lookup"><span data-stu-id="b4834-110">NuGet remembers the identity and version number of each installed package, recording it in either [`packages.config`](../reference/packages-config.md) or the project file (using [PackageReference](../consume-packages/package-references-in-project-files.md)), depending on project type and your version of NuGet.</span></span> <span data-ttu-id="b4834-111">PackageReference は [パッケージ マネージャーの UI オプション](../tools/package-manager-ui.md)を利用して Visual Studio で構成できますが、NuGet 4.0 以降では、PackageReference をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b4834-111">With NuGet 4.0+, PackageReference is preferred, although this is configurable in Visual Studio through the [Package Manager UI options](../tools/package-manager-ui.md).</span></span> <span data-ttu-id="b4834-112">いずれの場合も、適切なファイルでいつでもプロジェクトの依存関係の完全なリストを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="b4834-112">In any case, you can look in the appropriate file at any time to see the full list of dependencies for your project.</span></span>

> [!Tip]
> <span data-ttu-id="b4834-113">ソフトウェアで使用する予定の各パッケージのライセンスを常に確認することをお勧めます。</span><span class="sxs-lookup"><span data-stu-id="b4834-113">It's prudent to always check the license for each package you intend to use in your software.</span></span> <span data-ttu-id="b4834-114">nuget.org には、各パッケージの説明ページの右側に **[ライセンス情報]** リンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b4834-114">On nuget.org, you find a **License Info** link on the right side of each package's description page.</span></span> <span data-ttu-id="b4834-115">パッケージでライセンス条項が指定されていない場合は、パッケージ ページの **[Contact owners]\(所有者に問い合わせる\)** リンクを使用して、パッケージ所有者に直接問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="b4834-115">If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="b4834-116">Microsoft はサードパーティのパッケージ プロバイダーを通じてユーザーに知的財産ライセンスを付与することはありません。また、サードパーティによって提供される情報について責任を負いません。</span><span class="sxs-lookup"><span data-stu-id="b4834-116">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

<span data-ttu-id="b4834-117">パッケージのインストール時に、NuGet は通常、パッケージがそのキャッシュから既に使用可能であるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="b4834-117">When installing packages, NuGet typically checks if the package is already available from its cache.</span></span> <span data-ttu-id="b4834-118">「[Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md)」 (グローバル パッケージおよびキャッシュ フォルダーを管理する) で説明されているように、コマンド ラインからこのキャッシュを手動でクリアすることができます。</span><span class="sxs-lookup"><span data-stu-id="b4834-118">You can manually clear this cache from the command line, as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="b4834-119">また、NuGet は、パッケージでサポートされるターゲット フレームワークがプロジェクトと互換性があることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b4834-119">NuGet also makes sure that the target frameworks supported by the package are compatible with your project.</span></span> <span data-ttu-id="b4834-120">パッケージに互換性のあるアセンブリが含まれていない場合、NuGet はエラーを示します。</span><span class="sxs-lookup"><span data-stu-id="b4834-120">If the package does not contain compatible assemblies, NuGet displays an error.</span></span> <span data-ttu-id="b4834-121">「[互換性のないパッケージのエラーの解決](dependency-resolution.md#resolving-incompatible-package-errors)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b4834-121">See [Resolving incompatible package errors](dependency-resolution.md#resolving-incompatible-package-errors).</span></span>

<span data-ttu-id="b4834-122">プロジェクト コードをソース リポジトリを追加する場合、通常は NuGet パッケージを含めません。</span><span class="sxs-lookup"><span data-stu-id="b4834-122">When adding project code to a source repository, you typically don't include NuGet packages.</span></span> <span data-ttu-id="b4834-123">Visual Studio Team Services などのシステムのビルド エージェントを含む、リポジトリを後で複製するか、そうでない場合はプロジェクトを取得するユーザーは、ビルドを実行する前に必要なパッケージを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b4834-123">Those who later clone the repository or otherwise acquire the project, including build agents on systems like Visual Studio Team Services, must restore the necessary packages prior to running a build:</span></span>

![リポジトリの複製およびいずれかの復元コマンドの使用による NuGet パッケージの復元フロー](media/Overview-02-RestoreFlow.png)

<span data-ttu-id="b4834-125">「[パッケージの復元](../consume-packages/package-restore.md)」では、プロジェクト ファイルまたは `packages.config` の情報を使用して、すべての依存関係を再インストールします。</span><span class="sxs-lookup"><span data-stu-id="b4834-125">[Package Restore](../consume-packages/package-restore.md) uses the information in the project file or `packages.config` to reinstall all dependencies.</span></span> <span data-ttu-id="b4834-126">「[Dependency Resolution](../consume-packages/dependency-resolution.md)」 (依存関係の解決) で説明されているように、関係するプロセスには違いがあることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b4834-126">Note that there are differences in the process involved, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span> <span data-ttu-id="b4834-127">また、コンソールで作業しているため、上図にはパッケージ マネージャー コンソールの復元コマンドは示されていません。ユーザーは既に Visual Studio のコンテキスト内にいて、通常、パッケージは自動で復元され、図に示されているようにソリューション レベルのコマンドが提供されます。</span><span class="sxs-lookup"><span data-stu-id="b4834-127">Also, the diagram above does not show a restore command for the Package Manager Console because you're with the Console you're already in the context of Visual Studio, which typically restores packages automatically and provides the solution-level command as shown.</span></span>

<span data-ttu-id="b4834-128">場合によっては、プロジェクトに既に含まれているパッケージの再インストールが必要になります。その場合、依存関係も再インストールされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b4834-128">Occasionally it's necessary to reinstall packages that are already included in a project, which may also reinstall dependencies.</span></span> <span data-ttu-id="b4834-129">これは、`nuget reinstall` コマンド使用するか、NuGet パッケージ マネージャー コンソールを使用して簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="b4834-129">This is easy to do using the `nuget reinstall` command or the NuGet Package Manager Console.</span></span> <span data-ttu-id="b4834-130">詳細については、「[Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md)」 (パッケージの再インストールと更新) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b4834-130">For details, see [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

<span data-ttu-id="b4834-131">最後に、NuGet の動作は `Nuget.Config` ファイルによって駆動されます。</span><span class="sxs-lookup"><span data-stu-id="b4834-131">Finally, NuGet's behavior is driven by `Nuget.Config` files.</span></span> <span data-ttu-id="b4834-132">「[Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md)」 (NuGet の動作の構成) で説明されているように、複数のファイルを使用して、さまざまなレベルの特定の設定を一元化することができます。</span><span class="sxs-lookup"><span data-stu-id="b4834-132">Multiple files can be used to centralize certain settings at different levels, as explained in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="b4834-133">それでは NuGet パッケージでの生産性の高いコーディングをお楽しみください。</span><span class="sxs-lookup"><span data-stu-id="b4834-133">Enjoy your productive coding with NuGet packages!</span></span>
