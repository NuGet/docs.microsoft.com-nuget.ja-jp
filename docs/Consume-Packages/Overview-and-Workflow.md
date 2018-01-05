---
title: "NuGet パッケージの使用の概要とワークフロー | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3c60f920-457d-4f43-9efe-210c514e5242
description: "プロジェクトで NuGet パッケージを利用する場合のプロセスの概要と、プロセスの他の特定の部分へのリンク。"
keywords: "NuGet パッケージの利用, NuGet 利用の概要, NuGet 利用のワークフロー, パッケージ利用のワークフロー, パッケージ利用の概要"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c48351cb6fed0ac94bd437d9443811f46c032bd0
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="package-consumption-workflow"></a><span data-ttu-id="efc30-104">パッケージ利用のワークフロー</span><span class="sxs-lookup"><span data-stu-id="efc30-104">Package consumption workflow</span></span>

<span data-ttu-id="efc30-105">nuget.org と組織が確立する可能性のあるプライベート パッケージ ギャラリーの間で、アプリとサービスで使用する数万の非常に有用なパッケージを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="efc30-105">Between nuget.org and private package galleries that your organization might establish, you can find tens of thousands of highly useful packages to use in your apps and services.</span></span> <span data-ttu-id="efc30-106">ただし、ソースに関係なく、パッケージを利用する場合は以下と同じ一般的なワークフローに従います。</span><span class="sxs-lookup"><span data-stu-id="efc30-106">But regardless of the source, consuming a package follows the same general workflow as shown below.</span></span> <span data-ttu-id="efc30-107">詳細については、「[パッケージの検索と選択](../consume-packages/finding-and-choosing-packages.md)」と[パッケージの使用に関するクイック スタート](../quickstart/use-a-package.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="efc30-107">For details, see [Finding and Choosing Packages](../consume-packages/finding-and-choosing-packages.md) and the [Use a Package quickstart](../quickstart/use-a-package.md).</span></span>

![パッケージ ソースへの移動、パッケージの検索、プロジェクトへのインストール、パッケージ API への using ステートメントと呼び出しの追加を示すフロー](media/Overview-01-GeneralFlow.png)

<span data-ttu-id="efc30-109">\* _コマンドラインから `nuget install` を使用する場合を除く。使用する場合は、構成ファイルを手動で編集する必要があります。[install コマンド リファレンス](../tools/cli-ref-install.md)に関するページを参照してください。_</span><span class="sxs-lookup"><span data-stu-id="efc30-109">\* _Except with `nuget install` from the command-line, in which case it's necessary to edit the configuration files by hand. See the [install command reference](../tools/cli-ref-install.md)._</span></span>

<span data-ttu-id="efc30-110">NuGet はインストールされているパッケージごとに ID とバージョン番号を記憶します。その場合、プロジェクトの種類と使用している NuGet のバージョンに応じて、`packages.config`、プロジェクト ファイル、`project.json` ファイルのいずれかに記録します。</span><span class="sxs-lookup"><span data-stu-id="efc30-110">NuGet remembers the identity and version number of each installed package, recording it in either `packages.config`, the project file, or a `project.json` file in your project root, depending on project type and your version of NuGet.</span></span> <span data-ttu-id="efc30-111">NuGet 4.0+ では、既定で[プロジェクト ファイルに依存関係が格納](../consume-packages/package-references-in-project-files.md)されます (Windows 10 RS1 をターゲットとする UWP プロジェクトの場合を除く)。</span><span class="sxs-lookup"><span data-stu-id="efc30-111">With NuGet 4.0+, [storing dependencies in the project file](../consume-packages/package-references-in-project-files.md) is the default (except for UWP projects targeting Windows 10 RS1).</span></span> <span data-ttu-id="efc30-112">いずれの場合も、適切なファイルでいつでもプロジェクトの依存関係の完全なリストを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="efc30-112">In any case, you can look in the appropriate file at any time to see the full list of dependencies for your project.</span></span>

> [!Tip]
> <span data-ttu-id="efc30-113">ソフトウェアで使用する予定の各パッケージのライセンスを常に確認することをお勧めます。</span><span class="sxs-lookup"><span data-stu-id="efc30-113">It's prudent to always check the license for each package you intend to use in your software.</span></span> <span data-ttu-id="efc30-114">nuget.org には、各パッケージの説明ページの右側に **[ライセンス情報]** リンクがあります。</span><span class="sxs-lookup"><span data-stu-id="efc30-114">On nuget.org, you'll find a **License Info** link on the right side of each package's description page.</span></span> <span data-ttu-id="efc30-115">パッケージでライセンス条項が指定されていない場合は、パッケージ ページの **[Contact owners]\(所有者に問い合わせる\)** リンクを使用して、パッケージ所有者に直接問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="efc30-115">If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="efc30-116">Microsoft はサードパーティのパッケージ プロバイダーを通じてユーザーに知的財産ライセンスを付与することはありません。また、サードパーティによって提供される情報について責任を負いません。</span><span class="sxs-lookup"><span data-stu-id="efc30-116">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

<span data-ttu-id="efc30-117">パッケージのインストール時に、NuGet は通常、パッケージがそのキャッシュから既に使用可能であるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="efc30-117">When installing packages, NuGet typically checks if the package is already available from its cache.</span></span> <span data-ttu-id="efc30-118">「[NuGet のキャッシュを管理する](../consume-packages/managing-the-nuget-cache.md)」で説明されているように、コマンド ラインからこのキャッシュを手動でクリアすることができます。</span><span class="sxs-lookup"><span data-stu-id="efc30-118">You can manually clear this cache from the command line, as described on [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

<span data-ttu-id="efc30-119">また、NuGet は、パッケージでサポートされるターゲット フレームワークがプロジェクトと互換性があることを確認します。</span><span class="sxs-lookup"><span data-stu-id="efc30-119">NuGet also makes sure that the target frameworks supported by the package are compatible with your project.</span></span> <span data-ttu-id="efc30-120">パッケージに互換性のあるアセンブリが含まれていない場合、NuGet はエラー メッセージを示します。</span><span class="sxs-lookup"><span data-stu-id="efc30-120">If the package does not contain compatible assemblies, NuGet will give you an error message.</span></span> <span data-ttu-id="efc30-121">「[互換性のないパッケージのエラーの解決](dependency-resolution.md#resolving-incompatible-package-errors)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="efc30-121">See [Resolving incompatible package errors](dependency-resolution.md#resolving-incompatible-package-errors).</span></span>

<span data-ttu-id="efc30-122">プロジェクト コードをソース リポジトリを追加する場合、通常は NuGet パッケージを含めません。</span><span class="sxs-lookup"><span data-stu-id="efc30-122">When adding project code to a source repository, you typically don't include NuGet packages.</span></span> <span data-ttu-id="efc30-123">Visual Studio Team Services などのシステムのビルド エージェントを含む、リポジトリを後で複製するユーザーは、ビルドを実行する前に必要なパッケージを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="efc30-123">Those who later clone the repository, which includes build agents on systems like Visual Studio Team Services, must restore the necessary packages prior to running a build:</span></span>

![リポジトリの複製およびいずれかの復元コマンドの使用による NuGet パッケージの復元フロー](media/Overview-02-RestoreFlow.png)

<span data-ttu-id="efc30-125">「[Package Restore](../consume-packages/package-restore.md)」 (パッケージの復元) では、プロジェクト ファイル、`packages.config`、`project.json` の情報を使用して、依存関係をすべて再インストールします。</span><span class="sxs-lookup"><span data-stu-id="efc30-125">[Package Restore](../consume-packages/package-restore.md) uses the information in the project file, `packages.config`, `project.json` to reinstall all dependencies.</span></span> <span data-ttu-id="efc30-126">「[Dependency Resolution](../consume-packages/dependency-resolution.md)」 (依存関係の解決) で説明されているように、関係するプロセスには違いがあることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="efc30-126">Note that there are differences in the process involved, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>

<span data-ttu-id="efc30-127">場合によっては、プロジェクトに既に含まれているパッケージの再インストールが必要になります。その場合、依存関係も再インストールされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="efc30-127">Occasionally it's necessary to reinstall packages that are already included in a project, which may also reinstall dependencies.</span></span> <span data-ttu-id="efc30-128">これは、NuGet コマンド ラインで `reinstall` コマンドを使用するか、NuGet パッケージ マネージャー コンソールを使用して簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="efc30-128">This is easy to do using the `reinstall` command via the NuGet command line or the NuGet Package Manager Console.</span></span> <span data-ttu-id="efc30-129">詳細については、「[Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md)」 (パッケージの再インストールと更新) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="efc30-129">For details, see [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

<span data-ttu-id="efc30-130">最後に、NuGet の動作は `Nuget.Config` 構成ファイルによって駆動されます。</span><span class="sxs-lookup"><span data-stu-id="efc30-130">Finally, NuGet's behavior is driven by `Nuget.Config` configuration files.</span></span> <span data-ttu-id="efc30-131">「[Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md)」 (NuGet の動作の構成) で説明されているように、複数のファイルを使用して、さまざまなレベルの特定の設定を一元化することができます。</span><span class="sxs-lookup"><span data-stu-id="efc30-131">Multiple files can be used to centralize certain settings at different levels, as explained in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="efc30-132">それでは NuGet パッケージでの生産性の高いコーディングをお楽しみください。</span><span class="sxs-lookup"><span data-stu-id="efc30-132">Enjoy your productive coding with NuGet packages!</span></span>
