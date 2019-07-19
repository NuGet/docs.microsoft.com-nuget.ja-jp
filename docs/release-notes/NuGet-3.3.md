---
title: NuGet 3.3 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.3 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 482c03a4f6ca39edf317b6ef8d535e79b53d5d16
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317038"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="8de15-103">NuGet 3.3 リリースノート</span><span class="sxs-lookup"><span data-stu-id="8de15-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="8de15-104">[Nuget 3.2.1 リリースノート](../release-notes/nuget-3.2.1.md) | [nuget 3.4-RC リリースノート](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="8de15-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="8de15-105">NuGet 3.3 は、2015年11月30日にリリースされました。これには、ユーザーインターフェイスの更新とコマンドライン機能が多数あり、NuGet クライアントに対する有用な修正プログラムが集められています。</span><span class="sxs-lookup"><span data-stu-id="8de15-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="8de15-106">新機能</span><span class="sxs-lookup"><span data-stu-id="8de15-106">New Features</span></span>

* <span data-ttu-id="8de15-107">認証済みフィードで NuGet コマンドラインクライアントがシームレスに動作できるようにする資格情報プロバイダーが導入されました。</span><span class="sxs-lookup"><span data-stu-id="8de15-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="8de15-108">[Visual Studio Team Services 資格情報プロバイダーをインストール](../api/nuget-exe-credential-providers.md)し、それを使用するように nuget クライアントを構成する手順については、Nuget のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="8de15-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="8de15-109">新しいユーザーインターフェイスの機能</span><span class="sxs-lookup"><span data-stu-id="8de15-109">New User Interface Features</span></span>

* <span data-ttu-id="8de15-110">使用可能なタブを個別に参照、インストール、および更新する</span><span class="sxs-lookup"><span data-stu-id="8de15-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="8de15-111">利用可能な更新プログラムが含まれているパッケージの数を示す更新可能なバッジ</span><span class="sxs-lookup"><span data-stu-id="8de15-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="8de15-112">パッケージがインストールされているか、更新プログラムが利用可能かどうかを示すパッケージバッジ</span><span class="sxs-lookup"><span data-stu-id="8de15-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="8de15-113">ダウンロード数と作成者がパッケージリストに追加されました</span><span class="sxs-lookup"><span data-stu-id="8de15-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="8de15-114">パッケージ一覧に表示可能な最大バージョン番号と現在インストールされているバージョン番号</span><span class="sxs-lookup"><span data-stu-id="8de15-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="8de15-115">パッケージリストからのクイックインストール、更新、およびアンインストールを可能にするアクションボタン</span><span class="sxs-lookup"><span data-stu-id="8de15-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="8de15-116">パッケージ詳細パネルのより明確なアクションボタン</span><span class="sxs-lookup"><span data-stu-id="8de15-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="8de15-117">パッケージの詳細パネルでのパッケージの更新日</span><span class="sxs-lookup"><span data-stu-id="8de15-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="8de15-118">ソリューションビューの統合パネル</span><span class="sxs-lookup"><span data-stu-id="8de15-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="8de15-119">ソリューションビューでのプロジェクトとインストールされているバージョン番号の並べ替え可能なグリッド</span><span class="sxs-lookup"><span data-stu-id="8de15-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="8de15-120">新しいコマンドライン機能</span><span class="sxs-lookup"><span data-stu-id="8de15-120">New Command-line Features</span></span>

<span data-ttu-id="8de15-121">このバージョンでは、 `add` [nuget.exe リファレンス](../reference/nuget-exe-cli-reference.md)で説明されているように、フォルダーベースのリポジトリを初期化するコマンドと`init`コマンドを導入しました。</span><span class="sxs-lookup"><span data-stu-id="8de15-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="8de15-122">このフォルダー構造を使用して構築および管理されるリポジトリは、このブログで説明されているように、大幅なパフォーマンス上の[利点を提供](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)します。</span><span class="sxs-lookup"><span data-stu-id="8de15-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="8de15-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="8de15-123">ContentFiles</span></span>

<span data-ttu-id="8de15-124">新しい`project.json` フォルダー`contentFiles`と要素の表記`contentFiles`によって、マネージプロジェクトでコンテンツがサポートされるようになりました。 `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="8de15-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="8de15-125">このコンテンツは、プロジェクトシステムとのやり取りのためにパッケージ作成者が直接指定できます。</span><span class="sxs-lookup"><span data-stu-id="8de15-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="8de15-126">`.nuspec`ドキュメントで contentfiles を構成する方法の詳細については、 [nuspec のリファレンスを参照](../reference/nuspec.md)してください。</span><span class="sxs-lookup"><span data-stu-id="8de15-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="8de15-127">NuGet ローカルキャッシュ管理</span><span class="sxs-lookup"><span data-stu-id="8de15-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="8de15-128">NuGet コマンドラインが更新され、ワークステーションでローカルキャッシュを管理する方法に関する情報が追加されました。</span><span class="sxs-lookup"><span data-stu-id="8de15-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="8de15-129">ローカルコマンドの詳細については、「 [NuGet コマンドラインリファレンス](../reference/cli-reference/cli-ref-locals.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8de15-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="8de15-130">修正済みの問題</span><span class="sxs-lookup"><span data-stu-id="8de15-130">Fixed Issues</span></span>

<span data-ttu-id="8de15-131">**注目すべき問題**</span><span class="sxs-lookup"><span data-stu-id="8de15-131">**Notable Issues**</span></span>

* <span data-ttu-id="8de15-132">Mono- [1543](https://github.com/NuGet/Home/issues/1543)でソリューションファイルを使用してパッケージを復元するための NuGet コマンドラインによる復元</span><span class="sxs-lookup"><span data-stu-id="8de15-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="8de15-133">3\.3 リリースで解決された問題の完全な一覧については、「 [3.3 マイルストーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)」の GitHub を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8de15-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="8de15-134">3\.3 コマンドラインリリースで修正された問題の一覧は、 [3.3 コマンドラインマイルストーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)に記録されます。</span><span class="sxs-lookup"><span data-stu-id="8de15-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="8de15-135">既知の問題</span><span class="sxs-lookup"><span data-stu-id="8de15-135">Known Issues</span></span>

<span data-ttu-id="8de15-136">GitHub の問題の一覧に関する問題は、引き続き次の場所にあります。[http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="8de15-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>