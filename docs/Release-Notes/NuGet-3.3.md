---
title: "NuGet 3.3 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.3 のリリース ノートです。"
keywords: "NuGet 3.3 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c83f87231497e14c36f1b8100b7bec720bb63b1c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="82485-104">NuGet 3.3 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="82485-104">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="82485-105">[NuGet 3.2.1 リリース ノート](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC のリリース ノート](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="82485-105">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="82485-106">NuGet 3.3 は、多数のユーザー インターフェイスを更新し、コマンド ライン機能だけでなく NuGet クライアントに役立ちますの修正プログラムのコレクションで、2015 年 11 月 30日でリリースされました。</span><span class="sxs-lookup"><span data-stu-id="82485-106">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="82485-107">新機能</span><span class="sxs-lookup"><span data-stu-id="82485-107">New Features</span></span>

* <span data-ttu-id="82485-108">NuGet コマンド ライン クライアントには、認証済みのフィードをシームレスに連携することを許可する資格情報プロバイダーが導入されました。</span><span class="sxs-lookup"><span data-stu-id="82485-108">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="82485-109">[資格情報プロバイダーの Visual Studio Team Services をインストールする方法について](../API/nuget-exe-Credential-Providers.md)と NuGet の構成を使用するクライアントは、NuGet Docs でご確認いただけます。</span><span class="sxs-lookup"><span data-stu-id="82485-109">[Instructions on how to install the Visual Studio Team Services credential provider ](../API/nuget-exe-Credential-Providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="82485-110">新しいユーザー インターフェイスの機能</span><span class="sxs-lookup"><span data-stu-id="82485-110">New User Interface Features</span></span>

* <span data-ttu-id="82485-111">別々 の参照、インストール、および更新プログラムの使用可能なタブ</span><span class="sxs-lookup"><span data-stu-id="82485-111">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="82485-112">利用可能な更新の数を示す、使用可能なバッジを更新します。</span><span class="sxs-lookup"><span data-stu-id="82485-112">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="82485-113">パッケージのパッケージがインストールされているかどうかを指定するパッケージの一覧はバッジまたは、更新プログラムが利用可能です</span><span class="sxs-lookup"><span data-stu-id="82485-113">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="82485-114">カウントとパッケージの一覧に追加の作成者をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="82485-114">Download count and author added to the package list</span></span>
* <span data-ttu-id="82485-115">最新の利用可能なバージョン番号と、パッケージ一覧に現在インストールされているバージョン番号</span><span class="sxs-lookup"><span data-stu-id="82485-115">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="82485-116">クイック インストールは、使用できるようにアクション ボタンは、更新、およびパッケージの一覧からアンインストール</span><span class="sxs-lookup"><span data-stu-id="82485-116">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="82485-117">パッケージの詳細パネルのわかりやすい動作設定ボタン</span><span class="sxs-lookup"><span data-stu-id="82485-117">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="82485-118">パッケージの詳細パネルのパッケージの更新日</span><span class="sxs-lookup"><span data-stu-id="82485-118">Package update date on the package detail panel</span></span>
* <span data-ttu-id="82485-119">ソリューション ビューのパネルを統合します。</span><span class="sxs-lookup"><span data-stu-id="82485-119">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="82485-120">プロジェクトとソリューション ビューでインストールされているバージョン番号の並べ替え可能なグリッド</span><span class="sxs-lookup"><span data-stu-id="82485-120">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="82485-121">コマンド ラインの新機能</span><span class="sxs-lookup"><span data-stu-id="82485-121">New Command-line Features</span></span>

<span data-ttu-id="82485-122">このバージョンでは導入された、`add`と`init`」の説明に従ってフォルダー ベースのリポジトリを初期化するためのコマンド、 [nuget.exe 参照](../tools/nuget-exe-cli-reference.md)です。</span><span class="sxs-lookup"><span data-stu-id="82485-122">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="82485-123">構築され、このフォルダーに保持するリポジトリの構造は[かなり高いパフォーマンス メリットをもたらします](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)ブログで説明したようです。</span><span class="sxs-lookup"><span data-stu-id="82485-123">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="82485-124">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="82485-124">ContentFiles</span></span>

<span data-ttu-id="82485-125">コンテンツがサポートされるようになりました`project.json`マネージ プロジェクトは、新しい`contentFiles`フォルダーと`.nuspec``contentFiles`要素表記します。</span><span class="sxs-lookup"><span data-stu-id="82485-125">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="82485-126">このコンテンツは、プロジェクト システムとのやり取りのパッケージの作成者によって直接指定できます。</span><span class="sxs-lookup"><span data-stu-id="82485-126">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="82485-127">コンテンツ ファイルを構成する方法の詳細について、`.nuspec`ドキュメントは含まれて、 [.nuspec 参照](../schema/nuspec.md)です。</span><span class="sxs-lookup"><span data-stu-id="82485-127">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../schema/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="82485-128">NuGet ローカル キャッシュの管理</span><span class="sxs-lookup"><span data-stu-id="82485-128">NuGet Locals Cache Management</span></span>

<span data-ttu-id="82485-129">コマンド ラインの NuGet がワークステーション上のローカルのキャッシュを管理する方法に関する情報が含まれる更新されました。</span><span class="sxs-lookup"><span data-stu-id="82485-129">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="82485-130">[ローカル] コマンドの詳細についてで使用できる、 [NuGet コマンド ライン リファレンス](../tools/cli-ref-locals.md)です。</span><span class="sxs-lookup"><span data-stu-id="82485-130">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="82485-131">問題を修正しました</span><span class="sxs-lookup"><span data-stu-id="82485-131">Fixed Issues</span></span>

<span data-ttu-id="82485-132">**注目すべき問題**</span><span class="sxs-lookup"><span data-stu-id="82485-132">**Notable Issues**</span></span>

* <span data-ttu-id="82485-133">復元するための NuGet コマンド ラインの復元されたサポート パッケージの Mono - 上のファイルをソリューションが[1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="82485-133">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="82485-134">GitHub の 3.3 のリリースで処理された問題の一覧が見つかりません、 [3.3 マイルス トーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)です。</span><span class="sxs-lookup"><span data-stu-id="82485-134">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="82485-135">3.3 コマンド ライン リリースで修正された問題の一覧に記録されます、 [3.3 コマンド ライン マイルス トーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)です。</span><span class="sxs-lookup"><span data-stu-id="82485-135">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="82485-136">既知の問題</span><span class="sxs-lookup"><span data-stu-id="82485-136">Known Issues</span></span>

<span data-ttu-id="82485-137">あることができます、GitHub の問題一覧上の問題を追跡するために続行: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="82485-137">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>