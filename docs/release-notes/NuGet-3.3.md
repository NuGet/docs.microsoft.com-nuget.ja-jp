---
title: NuGet 3.3 のリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.3 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546648"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="a0f0a-103">NuGet 3.3 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="a0f0a-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="a0f0a-104">[NuGet 3.2.1 のリリース ノート](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC リリース ノート](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="a0f0a-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="a0f0a-105">NuGet 3.3 は、多数のユーザー インターフェイスの更新プログラムと機能のコマンド ラインほか NuGet クライアントに便利な修正プログラムのコレクションで、2015 年 11 月 30日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="a0f0a-106">新機能</span><span class="sxs-lookup"><span data-stu-id="a0f0a-106">New Features</span></span>

* <span data-ttu-id="a0f0a-107">NuGet コマンド ライン クライアントを認証済みフィードとシームレスに連携できるように許可する資格情報プロバイダーが導入されています。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="a0f0a-108">[資格情報プロバイダーの Visual Studio Team Services をインストールする方法について](../api/nuget-exe-credential-providers.md)NuGet の構成とそれを使用するクライアントは、NuGet Docs でご確認いただけます。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="a0f0a-109">ユーザー インターフェイスの新機能</span><span class="sxs-lookup"><span data-stu-id="a0f0a-109">New User Interface Features</span></span>

* <span data-ttu-id="a0f0a-110">参照、インストール、および使用可能な更新プログラムの個別のタブ</span><span class="sxs-lookup"><span data-stu-id="a0f0a-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="a0f0a-111">更新プログラムの使用可能なバッジが利用可能な更新を使用してパッケージの数を示す</span><span class="sxs-lookup"><span data-stu-id="a0f0a-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="a0f0a-112">パッケージがインストールされているまたは、更新プログラムが利用可能なかどうかを指定するパッケージの一覧でパッケージのバッジ</span><span class="sxs-lookup"><span data-stu-id="a0f0a-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="a0f0a-113">ダウンロード数と、パッケージ一覧に追加された作成者</span><span class="sxs-lookup"><span data-stu-id="a0f0a-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="a0f0a-114">最新の利用可能なバージョン番号とパッケージの一覧に現在インストールされているバージョン番号</span><span class="sxs-lookup"><span data-stu-id="a0f0a-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="a0f0a-115">動作設定ボタン クイックのインストールを許可するのには、更新、およびパッケージの一覧からアンインストール</span><span class="sxs-lookup"><span data-stu-id="a0f0a-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="a0f0a-116">パッケージの詳細 パネルでわかりやすい動作設定ボタン</span><span class="sxs-lookup"><span data-stu-id="a0f0a-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="a0f0a-117">パッケージの詳細 パネルでのパッケージの更新日</span><span class="sxs-lookup"><span data-stu-id="a0f0a-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="a0f0a-118">ソリューション ビューのパネルを統合します。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="a0f0a-119">プロジェクトとソリューション ビューでインストールされているバージョン番号の並べ替え可能なグリッド</span><span class="sxs-lookup"><span data-stu-id="a0f0a-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="a0f0a-120">コマンド ラインの新機能</span><span class="sxs-lookup"><span data-stu-id="a0f0a-120">New Command-line Features</span></span>

<span data-ttu-id="a0f0a-121">このバージョンで導入されました、`add`と`init`コマンド」の説明に従って、フォルダー ベースのリポジトリを初期化するために、 [nuget.exe 参照](../tools/nuget-exe-cli-reference.md)します。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="a0f0a-122">構築され、このフォルダーに保持するリポジトリの構造は[パフォーマンスに大きなメリットをもたらします](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)私たちのブログで説明されているようです。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="a0f0a-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a0f0a-123">ContentFiles</span></span>

<span data-ttu-id="a0f0a-124">コンテンツがサポートされるようになりました`project.json`マネージ プロジェクトでは、新しい`contentFiles`フォルダーと`.nuspec``contentFiles`要素表記します。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="a0f0a-125">このコンテンツは、プロジェクト システムとの対話のパッケージの作成者によって直接指定できます。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="a0f0a-126">ContentFiles を構成する方法については、`.nuspec`ドキュメントが記載されて、 [.nuspec リファレンス](../reference/nuspec.md)します。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="a0f0a-127">NuGet のローカル キャッシュの管理</span><span class="sxs-lookup"><span data-stu-id="a0f0a-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="a0f0a-128">NuGet コマンド ラインがワークステーションのローカル キャッシュを管理する方法についての情報を含めるように更新されました。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="a0f0a-129">ローカル コマンドの詳細についてで使用できる、 [NuGet コマンド ライン リファレンス](../tools/cli-ref-locals.md)します。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="a0f0a-130">問題を修正しました</span><span class="sxs-lookup"><span data-stu-id="a0f0a-130">Fixed Issues</span></span>

<span data-ttu-id="a0f0a-131">**注目に値する問題**</span><span class="sxs-lookup"><span data-stu-id="a0f0a-131">**Notable Issues**</span></span>

* <span data-ttu-id="a0f0a-132">復元するための NuGet コマンド ラインの復元されたサポート パッケージの Mono - でソリューション ファイルが[1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="a0f0a-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="a0f0a-133">3.3 のリリースで対処された問題の完全な一覧は、GitHub で確認できます、 [3.3 マイルス トーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)します。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="a0f0a-134">コマンド ライン 3.3 のリリースで修正された問題の一覧に記録、 [3.3 コマンド ライン マイルス トーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)します。</span><span class="sxs-lookup"><span data-stu-id="a0f0a-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="a0f0a-135">既知の問題</span><span class="sxs-lookup"><span data-stu-id="a0f0a-135">Known Issues</span></span>

<span data-ttu-id="a0f0a-136">GitHub の問題一覧上の問題を追跡するために引き続き。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="a0f0a-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>