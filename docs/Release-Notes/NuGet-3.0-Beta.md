---
title: "NuGet 3.0 Beta リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4153ff3f-f97f-4e54-b638-e844f70edf22
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.0 Beta リリース ノートです。"
keywords: "NuGet 3.0 Beta リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 46b2a81845f5ac06b8c80975c55fcfc33b86636e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-beta-release-notes"></a><span data-ttu-id="32604-104">NuGet 3.0 Beta リリース ノート</span><span class="sxs-lookup"><span data-stu-id="32604-104">NuGet 3.0 Beta Release Notes</span></span>

<span data-ttu-id="32604-105">[NuGet 3.0 プレビューのリリース ノート](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC のリリース ノートには](../release-notes/nuget-3.0-rc.md)</span><span class="sxs-lookup"><span data-stu-id="32604-105">[NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-rc.md)</span></span>

<span data-ttu-id="32604-106">NuGet 3.0 Beta は、Visual Studio 2015 CTP の 6 リリースの 2015 年 2 月 23 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="32604-106">NuGet 3.0 Beta was released on February 23, 2015 for the Visual Studio 2015 CTP 6 release.</span></span> <span data-ttu-id="32604-107">このリリースを意味ずっと私たちのチームを共有するには、アーキテクチャとパフォーマンスの向上の数があるし、ご案内 nuget.org サービスのパフォーマンスの設定のチューニングを開始します。</span><span class="sxs-lookup"><span data-stu-id="32604-107">This release means a lot to our team, as we have a number of architecture and performance improvements to share, and we're excited to start tuning the performance settings on our nuget.org service.</span></span>

<span data-ttu-id="32604-108">この新しいバージョンをインストールする前に、NuGet の Visual Studio 2015 の拡張機能のより前のバージョンをアンインストールすることを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="32604-108">We strongly recommend that you uninstall any prior version of the NuGet Visual Studio 2015 extension before installing this new version.</span></span>  <span data-ttu-id="32604-109">拡張機能のこのバージョンで問題があれば、ことをお勧めする元に戻す、[以前のバージョン](http://nuget.codeplex.com/downloads/get/909582)Visual Studio 2015 preview で使用するためです。</span><span class="sxs-lookup"><span data-stu-id="32604-109">If you have any problems with this version of the extension, we recommend you revert to the [prior version](http://nuget.codeplex.com/downloads/get/909582) for use with Visual Studio 2015 preview.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="32604-110">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="32604-110">Visual Studio 2012+</span></span>

<span data-ttu-id="32604-111">この NuGet 3.0 Beta は、Visual Studio 2015 CTP 6 拡張機能ギャラリーにインストールできるようにします。</span><span class="sxs-lookup"><span data-stu-id="32604-111">This NuGet 3.0 Beta is available to install in the Visual Studio 2015 CTP 6 Extension Gallery.</span></span> <span data-ttu-id="32604-112">Visual Studio 2012 および Visual Studio 2013 プレビューのドロップを非常に早く取得に努めています。</span><span class="sxs-lookup"><span data-stu-id="32604-112">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="32604-113">目的とした共有していた[for Visual Studio 2010 の更新プログラムを中止](http://blog.nuget.org/20141002/visual-studio-2010.html)、難しい判断するためでした。</span><span class="sxs-lookup"><span data-stu-id="32604-113">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="32604-114">新しいクライアント/サーバー API</span><span class="sxs-lookup"><span data-stu-id="32604-114">New Client/Server API</span></span>

<span data-ttu-id="32604-115">NuGet のクライアント/サーバー プロトコルの実装の詳細お操作しました。</span><span class="sxs-lookup"><span data-stu-id="32604-115">We've been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="32604-116">実行した作業は、パッケージをインストールするパッケージの復元など、重要なシナリオの高可用性を軸に設計されている NuGet の"API v3"を作成します。</span><span class="sxs-lookup"><span data-stu-id="32604-116">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="32604-117">新しい API は REST に基づいており、Hypermedia と選択[JSON %LD](http://json-ld.org)として、リソース形式。</span><span class="sxs-lookup"><span data-stu-id="32604-117">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="32604-118">NuGet 3.0 Beta のビット単位で、パッケージ ソースのドロップダウン リストで"api.nuget.org"と呼ばれる新しいパッケージ ソースが表示されます。</span><span class="sxs-lookup"><span data-stu-id="32604-118">In the NuGet 3.0 Beta bits, you'll see a new package source called "api.nuget.org" in the package source dropdown.</span></span>   <span data-ttu-id="32604-119">そのパッケージのソースを選択すると、nuget.org への接続にではなく、新しい API が使用されます。NuGet 3.0 RC では、この新しい API v3 ベースのパッケージ ソースは v2 ベース"nuget.org"のパッケージ ソースに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="32604-119">If you select that package source, we'll use our new API rather to connect to nuget.org. In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>  <span data-ttu-id="32604-120">すべての他のパブリックのパッケージ ソースを無効にすることを勧めし、としてのみ公開パッケージ リポジトリのみ api.nuget.org のままにします。</span><span class="sxs-lookup"><span data-stu-id="32604-120">We recommend disabling all of the other public package sources and leave only api.nuget.org as your only public package repository.</span></span>

<span data-ttu-id="32604-121">V3 API の構築に多くの時間を配置したして、パブリック リポジトリへのアクセスにシークする古いクライアントの標準 v2 API を維持するために続行されます。</span><span class="sxs-lookup"><span data-stu-id="32604-121">We've put a lot of time into building our v3 API and will continue to maintain the standard v2 API for old clients seeking to access the public repository.</span></span>

## <a name="updated-ui"></a><span data-ttu-id="32604-122">更新された UI</span><span class="sxs-lookup"><span data-stu-id="32604-122">Updated UI</span></span>

<span data-ttu-id="32604-123">コンボ ボックスには、パッケージを実行するアクションを選択することが、画面の [オプション] 領域でチェック ボックスをオンに移行して、[プレビュー] ボタンを含めるには、このリリースではユーザー インターフェイスを拡張しました。</span><span class="sxs-lookup"><span data-stu-id="32604-123">We've enhanced the user-interface in this release to include a combobox that will allow you to choose an action to take with the package and transitioned the preview button into a checkbox in the options area of the screen.</span></span>  <span data-ttu-id="32604-124">[オプション] 領域では、折りたたみが適用されなくし、今すぐ使用可能なオプションを説明するヘルプ リンクを提供します。</span><span class="sxs-lookup"><span data-stu-id="32604-124">The options area is no longer collapsible and now provides a help link describing the options available.</span></span>

![新しい NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a><span data-ttu-id="32604-126">操作のログ記録</span><span class="sxs-lookup"><span data-stu-id="32604-126">Operation Logging</span></span>

<span data-ttu-id="32604-127">モーダル ウィンドウにすばやく表示し、インストールまたはアンインストール中に非表示にログ情報を削除しました。</span><span class="sxs-lookup"><span data-stu-id="32604-127">We removed the modal window with logging information that would quickly appear and hide while installing or uninstalling.</span></span>  <span data-ttu-id="32604-128">実際にする情報を参照してください。 またはからコピーして貼り付けることができる場合に、このウィンドウに値が追加されていません。</span><span class="sxs-lookup"><span data-stu-id="32604-128">This window added no value when you would really want to see the information or be able to copy and paste from it.</span></span>  <span data-ttu-id="32604-129">代わりに、お今すぐをリダイレクトしてすべての出力は、出力ウィンドウの [パッケージ マネージャー] ウィンドウにログを記録します。</span><span class="sxs-lookup"><span data-stu-id="32604-129">Instead, we are now redirecting all of the output logging to the Package Manager pane of the Output window.</span></span>  <span data-ttu-id="32604-130">これより快適で検査する通常のビルド レポートと同様と思います。</span><span class="sxs-lookup"><span data-stu-id="32604-130">We think this is more comfortable and similar to a typical build report that you would want to inspect.</span></span>


### <a name="focus-on-performance"></a><span data-ttu-id="32604-131">パフォーマンスを焦点します。</span><span class="sxs-lookup"><span data-stu-id="32604-131">Focus on Performance</span></span>

<span data-ttu-id="32604-132">ここには、多数の NuGet 検索、およびフェッチのパフォーマンスを向上させる名前の変更が行われます。</span><span class="sxs-lookup"><span data-stu-id="32604-132">We made a lot of changes in the name of improving performance of NuGet searches, and fetches.</span></span>  <span data-ttu-id="32604-133">これは、懸案事項、マイクロソフトのお客様からおよび、このリリースで対処しだったことを確認します。</span><span class="sxs-lookup"><span data-stu-id="32604-133">This was our number one concern from our customers, and we wanted to be sure we addressed it in this release.</span></span>  <span data-ttu-id="32604-134">新しい CDN では、構築、サーバーをチューニングおよびできれば関連性を提供するためのロジックに一致するクエリが向上したし、高速のパッケージ検索結果します。</span><span class="sxs-lookup"><span data-stu-id="32604-134">We've tuned our servers, built out a new CDN, and improved the query matching logic to hopefully deliver to you more relevant and faster package search results.</span></span>

<span data-ttu-id="32604-135">NuGet 3.0 の開発のこのフェーズを続けていくおチューニングとする、改善を配信することを確認する nuget.org サービスを監視します。</span><span class="sxs-lookup"><span data-stu-id="32604-135">As we proceed through this phase of the development of NuGet 3.0, we will be tuning and monitoring the nuget.org service to ensure that we deliver an improved experience.</span></span>  <span data-ttu-id="32604-136">おはありません、ダウンタイムに関与する計画を追加してするサービスでリソースを変更します。</span><span class="sxs-lookup"><span data-stu-id="32604-136">We do not plan to engage in any downtime, but will be adding and changing resources in the service.</span></span>  <span data-ttu-id="32604-137">注意を続け、 [twitter フィード](http://twitter.com/nuget)詳細については、サービスの構成を変更するときにします。</span><span class="sxs-lookup"><span data-stu-id="32604-137">Keep an eye on our [twitter feed](http://twitter.com/nuget) for details on when we change the service configuration.</span></span>

## <a name="building-nuget-with-nuget"></a><span data-ttu-id="32604-138">NuGet を使ってビルド NuGet</span><span class="sxs-lookup"><span data-stu-id="32604-138">Building NuGet with NuGet</span></span>

<span data-ttu-id="32604-139">おが今すぐを再構築し、NuGet クライアント自体は NuGet パッケージに組み込まれているいくつかのコンポーネントにします。</span><span class="sxs-lookup"><span data-stu-id="32604-139">We have now rearchitected our NuGet clients into several components that are themselves being built into NuGet packages.</span></span> <span data-ttu-id="32604-140">独自のライブラリの再使用正しくをパッケージ化し、再利用可能ななっているコンポーネントを作成することを強制します。</span><span class="sxs-lookup"><span data-stu-id="32604-140">This re-use of our own libraries forces us to build components that are re-usable and that can be packaged properly.</span></span>  <span data-ttu-id="32604-141">コードの重複を排除し、改善、ソリューション全体でパッケージを作成する必要性をサポートするために、開発プロセスを構成する方法について学習しましたできました。</span><span class="sxs-lookup"><span data-stu-id="32604-141">We have been able to eliminate duplicated code and have learned how to better configure our development process to support the need to build packages throughout our solutions.</span></span>  <span data-ttu-id="32604-142">コード プロジェクトの構造し、ビルド処理のしくみについては話を早く、ブログの投稿を探します。</span><span class="sxs-lookup"><span data-stu-id="32604-142">Look for a blog post soon where we will talk about how the code projects are structured and how our build process works.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="32604-143">待ち</span><span class="sxs-lookup"><span data-stu-id="32604-143">Stay Tuned</span></span>

<span data-ttu-id="32604-144">くださいに注意[私たちのブログ](http://blog.nuget.org)の詳細の進行状況と NuGet 3.0 のお知らせください。</span><span class="sxs-lookup"><span data-stu-id="32604-144">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>
