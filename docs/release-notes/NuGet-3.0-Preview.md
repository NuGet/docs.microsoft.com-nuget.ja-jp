---
title: NuGet 3.0 プレビューのリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.0 プレビューのリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546466"
---
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="aea36-103">NuGet 3.0 プレビューのリリース ノート</span><span class="sxs-lookup"><span data-stu-id="aea36-103">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="aea36-104">[NuGet 2.9 RC リリース ノート](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 ベータ版のリリース ノート](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="aea36-104">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="aea36-105">Visual Studio 2015 Preview リリースの一部として、2014 年 11 月 12日で NuGet 3.0 プレビューがリリースされました。</span><span class="sxs-lookup"><span data-stu-id="aea36-105">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="aea36-106">NuGet 3.0 プレビューをリリースしました。</span><span class="sxs-lookup"><span data-stu-id="aea36-106">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="aea36-107">(ただし、プレビュー) は、私たちにとって大きなリリースこれは、私たちは、変更に関するフィードバックの取得を開始することを嬉しく思います。</span><span class="sxs-lookup"><span data-stu-id="aea36-107">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="aea36-108">Visual Studio 2012 以降</span><span class="sxs-lookup"><span data-stu-id="aea36-108">Visual Studio 2012+</span></span>

<span data-ttu-id="aea36-109">この NuGet 3.0 プレビューは、Visual Studio 2015 Preview に含まれます。</span><span class="sxs-lookup"><span data-stu-id="aea36-109">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="aea36-110">Visual Studio 2012 および Visual Studio 2013 のプレビューの削除を非常に早く取得取り組んでいます。</span><span class="sxs-lookup"><span data-stu-id="aea36-110">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="aea36-111">以前に自分の意図を公表しました[for Visual Studio 2010 の更新プログラムを中止](http://blog.nuget.org/20141002/visual-studio-2010.html)、し、困難な判断を行うことでした。</span><span class="sxs-lookup"><span data-stu-id="aea36-111">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="aea36-112">新しい UI</span><span class="sxs-lookup"><span data-stu-id="aea36-112">Brand New UI</span></span>

<span data-ttu-id="aea36-113">最初に注目する NuGet 3.0 プレビューの詳細については、まったく新しい UI です。</span><span class="sxs-lookup"><span data-stu-id="aea36-113">The first thing you notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="aea36-114">モーダル ダイアログ ボックスではありません。完全な Visual Studio ドキュメント ウィンドウです。</span><span class="sxs-lookup"><span data-stu-id="aea36-114">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="aea36-115">これにより、一度に複数のプロジェクト (およびソリューション) の UI を開き、別のモニターにウィンドウを切り離しなどの場合は、ドッキングできます。</span><span class="sxs-lookup"><span data-stu-id="aea36-115">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![新しい NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="aea36-117">モーダル ダイアログ ボックスの破棄のための使いやすさの違い、を超えても数多くの新機能にある新しい UI です。</span><span class="sxs-lookup"><span data-stu-id="aea36-117">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="aea36-118">バージョンの選択</span><span class="sxs-lookup"><span data-stu-id="aea36-118">Version Selection</span></span>

<span data-ttu-id="aea36-119">おそらく、最も要求、UI の機能は、パッケージのインストールと更新 - バージョンの選択を許可するこれが使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="aea36-119">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![パッケージのバージョンの選択](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="aea36-121">インストールまたは、パッケージを更新するかどうかのバージョン ドロップダウンで 簡単な選択範囲の一覧の一番上に昇格するいくつかの注目すべきバージョン パッケージ、利用可能なバージョンのすべてを表示できます。</span><span class="sxs-lookup"><span data-stu-id="aea36-121">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="aea36-122">不要になった PowerShell コンソールを使用して、最新ではない特定のバージョンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aea36-122">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="aea36-123">インストールされている/Online/更新ワークフローを組み合わせる</span><span class="sxs-lookup"><span data-stu-id="aea36-123">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="aea36-124">以前、UI では、オンラインでインストールと更新プログラムの 3 つのタブがありました。</span><span class="sxs-lookup"><span data-stu-id="aea36-124">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="aea36-125">一覧にあるパッケージされたこれらのワークフローを特定し、使用可能なアクションがもワークフローに固有です。</span><span class="sxs-lookup"><span data-stu-id="aea36-125">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="aea36-126">論理では、多くの場合に多くの要望が寄せられているように思えます中には、この分離によってづくを取得します。</span><span class="sxs-lookup"><span data-stu-id="aea36-126">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="aea36-127">インストール、更新、または選択したパッケージを取得した方法に関係なく、パッケージのアンインストールをする結合の経験があるようになりました。</span><span class="sxs-lookup"><span data-stu-id="aea36-127">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="aea36-128">特定のワークフローを支援するようになりましたがありますがフィルターのドロップダウン リストに表示され、パッケージをフィルター処理することができますし、パッケージに対して実行できるアクションは一貫性のあります。</span><span class="sxs-lookup"><span data-stu-id="aea36-128">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![パッケージをアンインストールします](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="aea36-130">インストール済み フィルターを使用すると、簡単に確認できます、インストールされているパッケージ、使用可能な更新プログラムがあるとできますいずれかをアンインストールまたは表示するバージョンの選択を変更することで、パッケージを更新し、使用可能なアクションを変更します。</span><span class="sxs-lookup"><span data-stu-id="aea36-130">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![パッケージを更新します。](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="aea36-132">バージョンの統合</span><span class="sxs-lookup"><span data-stu-id="aea36-132">Version Consolidation</span></span>

<span data-ttu-id="aea36-133">ソリューション内で複数のプロジェクトにインストールされている同じパッケージに一般的です。</span><span class="sxs-lookup"><span data-stu-id="aea36-133">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="aea36-134">各プロジェクトにインストールされているバージョンを離れているドリフトことができる場合もありますし、使用中のバージョンを統合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aea36-134">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="aea36-135">NuGet 3.0 プレビューでは、このシナリオでのみ新機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="aea36-135">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="aea36-136">ソリューション レベル パッケージの管理 ウィンドウは、ソリューションを右クリックし、ソリューションの NuGet パッケージの管理を選択してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="aea36-136">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="aea36-137">そこから、使用して、さまざまなバージョンが、複数のプロジェクトにインストールされているパッケージを選択した場合、新しい「統合」アクションは使用可能なになります。</span><span class="sxs-lookup"><span data-stu-id="aea36-137">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="aea36-138">以下のスクリーン ショット`Newtonsoft.Json`にインストールされた、`SamplesClassLibrary`バージョン`6.0.4`にインストールされていると`SamplesConsoleApp`バージョン`5.0.4`。</span><span class="sxs-lookup"><span data-stu-id="aea36-138">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![バージョンを統合します。](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="aea36-140">1 つのバージョンに統合するためのワークフローを次に示します。</span><span class="sxs-lookup"><span data-stu-id="aea36-140">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="aea36-141">選択、`Newtonsoft.Json`リスト内のパッケージ</span><span class="sxs-lookup"><span data-stu-id="aea36-141">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="aea36-142">選択`Consolidate`から、`Action`ドロップダウン</span><span class="sxs-lookup"><span data-stu-id="aea36-142">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="aea36-143">使用して、`Version`に統合するバージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="aea36-143">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="aea36-144">そのバージョン (既に選択されているバージョン上のプロジェクトはグレー メモ) に統合する必要があるプロジェクトのチェック ボックス</span><span class="sxs-lookup"><span data-stu-id="aea36-144">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="aea36-145">をクリックして、`Consolidate`連結を実行するボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="aea36-145">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="aea36-146">操作のプレビュー</span><span class="sxs-lookup"><span data-stu-id="aea36-146">Operation Previews</span></span>

<span data-ttu-id="aea36-147">--を実行している操作に関係なくインストール/更新/アンインストール - 新しい UI で、プロジェクトに行われる変更をプレビューする方法。</span><span class="sxs-lookup"><span data-stu-id="aea36-147">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="aea36-148">このプレビューは、新しいパッケージをインストールするとパッケージは、操作中には変更されませんが、アンインストール、更新され、パッケージをパッケージで表示されます。</span><span class="sxs-lookup"><span data-stu-id="aea36-148">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="aea36-149">次の例で Microsoft.AspNet.SignalR をインストールする原因になる多数の変更をプロジェクトにことがわかります。</span><span class="sxs-lookup"><span data-stu-id="aea36-149">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![プレビューの SignalR をインストールします。](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="aea36-151">インストール オプション</span><span class="sxs-lookup"><span data-stu-id="aea36-151">Installation Options</span></span>

<span data-ttu-id="aea36-152">PowerShell コンソールを使用したので注目すべきインストール オプションのいくつかを制御します。</span><span class="sxs-lookup"><span data-stu-id="aea36-152">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="aea36-153">同様の UI にそれらの機能を導入しました。</span><span class="sxs-lookup"><span data-stu-id="aea36-153">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="aea36-154">これで、依存関係のバージョンを選択する方法の依存関係の解決の動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="aea36-154">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![依存関係の動作](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="aea36-156">パッケージからコンテンツ ファイルが既にプロジェクト内のファイルと競合する場合に実行するアクションを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="aea36-156">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![ファイルの競合のアクション](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="aea36-158">無限スクロール</span><span class="sxs-lookup"><span data-stu-id="aea36-158">Infinite Scrolling</span></span>

<span data-ttu-id="aea36-159">かなり UI についてのフィードバックが両方のスクロールとパッケージを一覧表示するときに、パラダイムをページングを取得するために使用します。</span><span class="sxs-lookup"><span data-stu-id="aea36-159">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="aea36-160">簡単な一覧の一番下までスクロールし、次のページ番号をクリックし、スクロールし、もう一度が非常に一般的なでした。</span><span class="sxs-lookup"><span data-stu-id="aea36-160">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="aea36-161">新しい UI を使用したスクロール--以上ページングするだけで済みますようにパッケージの一覧で無限スクロールを実装しました。</span><span class="sxs-lookup"><span data-stu-id="aea36-161">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![無限スクロール](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="aea36-163">作業を行うことで、高速なきれいになります</span><span class="sxs-lookup"><span data-stu-id="aea36-163">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="aea36-164">この新しい UI を抜け出すを試すことを期待して止みません。経験がからこのプレビューのマイルス トーンの中に次の優れた格言「やすく機能、高速になります、見栄えを良くします」。</span><span class="sxs-lookup"><span data-stu-id="aea36-164">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="aea36-165">このプレビューでは、ほとんどを達成してきた--その第一の目標の動作します。</span><span class="sxs-lookup"><span data-stu-id="aea36-165">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="aea36-166">わかってはまだ非常に高速、および非常に非常にまだわかっています。</span><span class="sxs-lookup"><span data-stu-id="aea36-166">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="aea36-167">これらの目標を RC リリースの間で操作することを信頼します。</span><span class="sxs-lookup"><span data-stu-id="aea36-167">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="aea36-168">それまでは、に関するご意見をぜひ、*使いやすさ*--ワークフロー、操作、新しい UI の方法と、*を感じて*新しい UI を使用します。</span><span class="sxs-lookup"><span data-stu-id="aea36-168">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="aea36-169">比較すると、従来の UI を削除しました関数のいくつかがあります。</span><span class="sxs-lookup"><span data-stu-id="aea36-169">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="aea36-170">次のいずれかが、意図的なと、もう 1 つだけでした取得時間で実行します。</span><span class="sxs-lookup"><span data-stu-id="aea36-170">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="aea36-171">「すべて」のパッケージ ソースの検索</span><span class="sxs-lookup"><span data-stu-id="aea36-171">Searching "All" Package Sources</span></span>

<span data-ttu-id="aea36-172">従来の UI には、すべてのパッケージ ソースに対してパッケージの検索を実行することができました。</span><span class="sxs-lookup"><span data-stu-id="aea36-172">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="aea36-173">UI にその機能を削除しましたし、私たちはありませんが天然痘を復活します。</span><span class="sxs-lookup"><span data-stu-id="aea36-173">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="aea36-174">すべてのパッケージ ソース、に対する検索操作を実行するために使用するこの機能では、結果を組み合わせた、並べ替えの選択に基づく結果を並べ替えるしようとします。</span><span class="sxs-lookup"><span data-stu-id="aea36-174">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="aea36-175">検索の関連性がで一元管理を本当に難しいことがわかりました。</span><span class="sxs-lookup"><span data-stu-id="aea36-175">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="aea36-176">Google や Bing から検索を実行して、結果をまとめて作り上げるを想像でしたか。</span><span class="sxs-lookup"><span data-stu-id="aea36-176">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="aea36-177">この機能での低速な簡単ながさらに、*誤って*を使用して、実際に有用では非常にまれと考えています。</span><span class="sxs-lookup"><span data-stu-id="aea36-177">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="aea36-178">問題のため、導入された機能受け取りました修正されたことはありませんでしたバグ レポートの数値。</span><span class="sxs-lookup"><span data-stu-id="aea36-178">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="aea36-179">すべてを更新します。</span><span class="sxs-lookup"><span data-stu-id="aea36-179">Update All</span></span>

<span data-ttu-id="aea36-180">まだ新しい UI でない従来の UI で、[すべて更新] ボタンがあるを使用しました。</span><span class="sxs-lookup"><span data-stu-id="aea36-180">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="aea36-181">この機能を復活させる、RC のリリースのおされます。</span><span class="sxs-lookup"><span data-stu-id="aea36-181">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="aea36-182">新しいクライアント/サーバー API</span><span class="sxs-lookup"><span data-stu-id="aea36-182">New Client/Server API</span></span>

<span data-ttu-id="aea36-183">だけでなく、新しいパッケージ管理 UI の新機能のいずれも操作している NuGet のクライアント/サーバー プロトコルの実装の詳細。</span><span class="sxs-lookup"><span data-stu-id="aea36-183">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="aea36-184">私たちが行った作業は、パッケージをインストールするパッケージの復元など、重要なシナリオの高可用性に設計された、NuGet の"API v3"を作成します。</span><span class="sxs-lookup"><span data-stu-id="aea36-184">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="aea36-185">新しい API は REST に基づいており、ハイパー メディア、私たちが選択した[JSON-LD](http://json-ld.org)として、リソースの形式。</span><span class="sxs-lookup"><span data-stu-id="aea36-185">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="aea36-186">NuGet 3.0 プレビューのビット単位では、パッケージ ソースのドロップダウン リストで"preview.nuget.org"と呼ばれる新しいパッケージ ソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="aea36-186">In the NuGet 3.0 Preview bits, you see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="aea36-187">そのパッケージのソースを選択すると場合、nuget.org に接続するためではなく、新しい API を使用します。行いましたソースのプレビュー UI で使用可能なテスト、変更、および新しい API を改善するまでの間。</span><span class="sxs-lookup"><span data-stu-id="aea36-187">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="aea36-188">NuGet 3.0 RC では、この新しい API v3 に基づくパッケージのソースは、v2 ベース"nuget.org"のパッケージ ソースに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="aea36-188">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="aea36-189">API v3 に私たちを試そうと投資に関係なく、既存 API v2 プロトコルであり、それらは nuget.org も以外の既存のパッケージ ソースを扱うことを意味の操作もこれらの新機能のすべてを行っています。</span><span class="sxs-lookup"><span data-stu-id="aea36-189">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="aea36-190">導入される新機能</span><span class="sxs-lookup"><span data-stu-id="aea36-190">New Features Coming</span></span>

<span data-ttu-id="aea36-191">ここで、3.0 RTM の間も取り組んでいます根本的な新しい NuGet 機能に、UI に表示される内容を超える。</span><span class="sxs-lookup"><span data-stu-id="aea36-191">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you see in the UI.</span></span> <span data-ttu-id="aea36-192">重要な投資分野の短い一覧を次に示します。</span><span class="sxs-lookup"><span data-stu-id="aea36-192">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="aea36-193">私たちは、Visual Studio と提携しているし、MSBuild チームを取得する[NuGet プラットフォームを深く](http://blog.nuget.org/20141014/in-the-platform.html)します。</span><span class="sxs-lookup"><span data-stu-id="aea36-193">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="aea36-194">パッケージのインストール時の規則を破棄し、代わりに、新しい機能が導入されてパッケージ化時にこれらの規則を適用に取り組んでいるところ「権限がある」[パッケージ マニフェスト](http://blog.nuget.org/20141023/package-manifests.html)します。</span><span class="sxs-lookup"><span data-stu-id="aea36-194">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="aea36-195">リファクタリング、NuGet のコードベースを Visual Studio でパッケージの管理外の別のドメインに、クライアントとサーバー コンポーネントを再利用可能なことに取り組んでいます。</span><span class="sxs-lookup"><span data-stu-id="aea36-195">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="aea36-196">パッケージがその it を示すことができます"プライベート dependencies"の概念について調査実装の詳細についてのみ、他のパッケージに依存関係があり、これらの依存関係は、最上位レベルの依存関係として表示されることはできません。</span><span class="sxs-lookup"><span data-stu-id="aea36-196">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="aea36-197">お見逃しなく</span><span class="sxs-lookup"><span data-stu-id="aea36-197">Stay Tuned</span></span>

<span data-ttu-id="aea36-198">監視してください[ブログ](http://blog.nuget.org)の詳細の進行状況と NuGet 3.0 のお知らせください。</span><span class="sxs-lookup"><span data-stu-id="aea36-198">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>