---
title: "NuGet 3.0 プレビューのリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6762b6f8-82b7-4bab-a1f0-cd25e5dc1fb4
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.0 プレビューのリリース ノートします。"
keywords: "NuGet 3.0 プレビュー リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ae137af6f9722c454458fdcb4f20760c08d6e8bb
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="dbf7f-104">NuGet 3.0 プレビューのリリース ノート</span><span class="sxs-lookup"><span data-stu-id="dbf7f-104">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="dbf7f-105">[NuGet 2.9 RC のリリース ノート](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta リリース ノート](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="dbf7f-105">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="dbf7f-106">NuGet 3.0 プレビューは、Visual Studio 2015 Preview のリリースの一環として 2014 年 11 月 12 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-106">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="dbf7f-107">NuGet 3.0 プレビューをリリースしました。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-107">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="dbf7f-108">(ただし、プレビュー) はご利用の米国の大規模なリリース、ご案内の変更に関するフィードバックの取得を開始します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-108">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="dbf7f-109">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="dbf7f-109">Visual Studio 2012+</span></span>

<span data-ttu-id="dbf7f-110">Visual Studio 2015 Preview では、この NuGet 3.0 プレビューが含まれます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-110">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="dbf7f-111">Visual Studio 2012 および Visual Studio 2013 プレビューのドロップを非常に早く取得に努めています。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-111">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="dbf7f-112">目的とした共有していた[for Visual Studio 2010 の更新プログラムを中止](http://blog.nuget.org/20141002/visual-studio-2010.html)、難しい判断するためでした。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-112">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="dbf7f-113">新しい UI</span><span class="sxs-lookup"><span data-stu-id="dbf7f-113">Brand New UI</span></span>

<span data-ttu-id="dbf7f-114">最初に気付くこと NuGet 3.0 プレビューについては、まったく新しい UI です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-114">The first thing you'll notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="dbf7f-115">モーダル ダイアログ ボックスではなくなりましたVisual Studio ドキュメント ウィンドウの完全では今すぐです。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-115">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="dbf7f-116">これにより、一度に複数のプロジェクト (または、ソリューション) の UI を開き、別のモニターにウィンドウを切り離し、ドッキングするには like などができます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-116">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![新しい NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="dbf7f-118">モーダル ダイアログ ボックスの破棄のための使いやすさの違い、を超えても数多くの新機能にある新しい UI。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-118">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="dbf7f-119">バージョンの選択</span><span class="sxs-lookup"><span data-stu-id="dbf7f-119">Version Selection</span></span>

<span data-ttu-id="dbf7f-120">おそらく、最も要求された UI の機能はパッケージのインストールおよび更新 - バージョン選択できるようにこれが使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-120">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![パッケージのバージョンの選択](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="dbf7f-122">インストールまたは、パッケージを更新するかどうか、バージョンのドロップダウン リストでは、すべての簡単な選択については、一覧の上部に昇格注目に値する一部のバージョンで、パッケージの利用可能なバージョンを参照してくださいすることができます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-122">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="dbf7f-123">不要になった PowerShell コンソールを使用して、最新ではない特定のバージョンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-123">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="dbf7f-124">結合のインストール/Online/更新ワークフロー</span><span class="sxs-lookup"><span data-stu-id="dbf7f-124">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="dbf7f-125">以前 UI には、インストールされている、オンライン、および更新のための 3 つのタブが必要があります。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-125">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="dbf7f-126">表示されているパッケージがこれらのワークフローを特定し、利用可能なアクションがワークフローを同様に固有。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-126">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="dbf7f-127">この分離によって、論理、多くの場合に多くの耳にするように見えました中トリップを取得します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-127">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="dbf7f-128">結合されたエクスペリエンスをインストール、更新、または選択したパッケージを入手した方法に関係なく、パッケージのアンインストールをしたがあるようになりました。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-128">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="dbf7f-129">特定のワークフローに役立てるため、おようになりましたフィルターのドロップダウン リストを表示、パッケージをフィルター処理できますがパッケージに対して実行できるアクションが一致しています。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-129">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![パッケージをアンインストールします。](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="dbf7f-131">「インストール」フィルターを使用すると、簡単に確認できますインストールされているパッケージで使用可能な更新があるとをか、アンインストールまたは表示するバージョンの選択を変更することによって、パッケージを更新し、使用可能なアクションを変更します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-131">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![パッケージを更新します。](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="dbf7f-133">バージョンの統合</span><span class="sxs-lookup"><span data-stu-id="dbf7f-133">Version Consolidation</span></span>

<span data-ttu-id="dbf7f-134">ソリューション内の複数のプロジェクトにインストールされる同じパッケージに共通です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-134">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="dbf7f-135">各プロジェクトにインストールされているバージョンを分解誤差できる場合もありますし、使用中のバージョンを統合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-135">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="dbf7f-136">NuGet 3.0 プレビューには、このシナリオでのみ、新しい機能が導入されています。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-136">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="dbf7f-137">ソリューション レベルのパッケージの管理 ウィンドウは、ソリューションを右クリックして、Manage NuGet Packages for Solution を選択してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-137">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="dbf7f-138">そこから、使用、さまざまなバージョンが、複数のプロジェクトにインストールされているパッケージを選択する場合は「統合」の新しいアクションを有効になります。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-138">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="dbf7f-139">以下のスクリーン ショット`Newtonsoft.Json`にインストールされた、`SamplesClassLibrary`バージョンと`6.0.4`にインストールされていると`SamplesConsoleApp`バージョンと`5.0.4`です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-139">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![バージョンを統合します。](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="dbf7f-141">1 つのバージョンに統合するためのワークフローを次に示します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-141">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="dbf7f-142">選択、`Newtonsoft.Json`リスト内のパッケージ</span><span class="sxs-lookup"><span data-stu-id="dbf7f-142">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="dbf7f-143">選択`Consolidate`から、`Action`ドロップダウン</span><span class="sxs-lookup"><span data-stu-id="dbf7f-143">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="dbf7f-144">使用して、`Version`に統合するバージョンを選択するドロップダウン リスト</span><span class="sxs-lookup"><span data-stu-id="dbf7f-144">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="dbf7f-145">そのバージョン (既に選択したバージョンのプロジェクトはグレーでメモ) に統合する必要があります、プロジェクトのチェック ボックス</span><span class="sxs-lookup"><span data-stu-id="dbf7f-145">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="dbf7f-146">クリックして、`Consolidate`統合を実行するボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-146">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="dbf7f-147">操作のプレビュー</span><span class="sxs-lookup"><span data-stu-id="dbf7f-147">Operation Previews</span></span>

<span data-ttu-id="dbf7f-148">--を実行している操作に関係なくインストール/更新/アンインストール--新しい UI ではプロジェクトに加え、変更をプレビューする方法です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-148">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="dbf7f-149">このプレビューは、新しいパッケージをインストールするパッケージが更新され、パッケージは変更されず、操作中にパッケージと共に、アンインストールされるで表示されます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-149">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="dbf7f-150">次の例では、Microsoft.AspNet.SignalR をインストールする原因になる多数の変更をプロジェクトには確認できます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-150">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![SignalR のインストールのプレビュー](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="dbf7f-152">インストール オプション</span><span class="sxs-lookup"><span data-stu-id="dbf7f-152">Installation Options</span></span>

<span data-ttu-id="dbf7f-153">PowerShell コンソールを使用したので注目に値するインストール オプションのいくつかを制御します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-153">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="dbf7f-154">これらの機能は、UI もに取り込まおしたようになりました。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-154">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="dbf7f-155">これで、依存関係のバージョンを選択する方法の依存関係の解決の動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-155">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![依存関係の動作](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="dbf7f-157">パッケージからコンテンツ ファイルが既にプロジェクト内のファイルと競合する場合に実行するアクションを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-157">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![ファイルの競合のアクション](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="dbf7f-159">無限スクロール</span><span class="sxs-lookup"><span data-stu-id="dbf7f-159">Infinite Scrolling</span></span>

<span data-ttu-id="dbf7f-160">取得少し UI に関するフィードバックを持つ両方スクロールし、パッケージを一覧表示するときのパラダイムのページングを使用しました。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-160">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="dbf7f-161">して短い一覧の一番下までスクロールし、次のページ番号をクリックし、スクロールし、もう一度が非常に一般的でした。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-161">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="dbf7f-162">新しい UI を使用したのみ--これ以上のページングをスクロールする必要があるように、パッケージの一覧で無限スクロールを実装しました。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-162">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![無限スクロール](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="dbf7f-164">作業を行う、高速できれいやすくなります。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-164">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="dbf7f-165">弊社は、試用するこの新しい UI を取得します。このプレビューのマイルス トーンの中にしましたの適切な古い格言を次って動作など、高速、見栄えを良くします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-165">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="dbf7f-166">このプレビューでは、ほとんどを達成してきた--最初その目標の動作です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-166">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="dbf7f-167">まだかなり高速、およびはまだかなりかなりわかってがわかっています。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-167">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="dbf7f-168">これらの目標を今すぐ RC のリリースまでに操作することを信頼します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-168">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="dbf7f-169">その間は、歓迎に関するご意見、*使いやすさ*--操作、ワークフローは、新しい UI のと方法、*感じる*新しい UI を使用します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-169">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="dbf7f-170">比較すると、古い UI 取り除きました関数の 2 つがあります。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-170">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="dbf7f-171">これらのいずれかが、意図的なし、もう 1 つだけでした取得期間中に完了します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-171">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="dbf7f-172">「すべて」のパッケージ ソースの検索</span><span class="sxs-lookup"><span data-stu-id="dbf7f-172">Searching "All" Package Sources</span></span>

<span data-ttu-id="dbf7f-173">古い UI を使用すると、すべてのパッケージ ソースに対してパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-173">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="dbf7f-174">UI でその機能を削除しましたし、おされませんされますに戻る。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-174">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="dbf7f-175">すべてのパッケージ ソース、に対する検索操作を実行するために使用するこの機能は、結果を組み合わせた、並べ替えの選択内容に基づいて、結果の並べ替えしようとします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-175">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="dbf7f-176">検索の適合性がで一元管理する非常に困難であるが見つかりました。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-176">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="dbf7f-177">Google と Bing に対して検索を実行して同時に結果を作り上げるを想像でしたしますか。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-177">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="dbf7f-178">さらに、この機能はでしたが低速で簡単に*誤って*使用、およびおは、実際には便利ですがほとんどと考えています。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-178">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="dbf7f-179">問題のため、導入された機能を受信しました、に関する多数のバグ レポート、修正されたことはありませんでした。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-179">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="dbf7f-180">すべて更新します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-180">Update All</span></span>

<span data-ttu-id="dbf7f-181">ない新しい UI にまだ古い UI で [すべて更新] ボタンを使用しました。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-181">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="dbf7f-182">この機能を再生、RC のリリースのおされます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-182">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="dbf7f-183">新しいクライアント/サーバー API</span><span class="sxs-lookup"><span data-stu-id="dbf7f-183">New Client/Server API</span></span>

<span data-ttu-id="dbf7f-184">に加えて、新しいパッケージ管理 UI の新機能のすべてもきております NuGet のクライアント/サーバー プロトコルの実装の詳細。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-184">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="dbf7f-185">実行した作業は、パッケージをインストールするパッケージの復元など、重要なシナリオの高可用性を軸に設計されている NuGet の"API v3"を作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-185">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="dbf7f-186">新しい API は REST に基づいており、Hypermedia と選択[JSON %LD](http://json-ld.org)として、リソース形式。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-186">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="dbf7f-187">NuGet 3.0 プレビュー ビット単位で、パッケージ ソースのドロップダウン リストで"preview.nuget.org"と呼ばれる新しいパッケージ ソースが表示されます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-187">In the NuGet 3.0 Preview bits, you'll see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="dbf7f-188">そのパッケージのソースを選択すると、nuget.org への接続にではなく、新しい API が使用されます。しましたソースのプレビュー UI で使用可能なテスト、修正、および新しい API を改善してまいります中。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-188">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="dbf7f-189">NuGet 3.0 RC では、この新しい API v3 ベースのパッケージ ソースは v2 ベース"nuget.org"のパッケージ ソースに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-189">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="dbf7f-190">API v3 に導入されていること、投資効果に関係なく、既存 API v2 プロトコルであり、nuget.org も以外の既存のパッケージ ソースを使用することを意味の操作も、すべてこれらの新機能を行っています。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-190">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="dbf7f-191">導入された新機能</span><span class="sxs-lookup"><span data-stu-id="dbf7f-191">New Features Coming</span></span>

<span data-ttu-id="dbf7f-192">現在 3.0 RTM までも取り組んでおり根本的な新しい NuGet 機能に、を超えて UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-192">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you'll see in the UI.</span></span> <span data-ttu-id="dbf7f-193">次に、注目すべき投資分野の短い一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-193">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="dbf7f-194">Visual Studio との提携しているおおよび MSBuild のチームを取得するために[NuGet プラットフォームに深く](http://blog.nuget.org/20141014/in-the-platform.html)です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-194">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="dbf7f-195">パッケージのインストール時の規則を破棄し、代わりに新しい導入することによってパッケージ化時にこれらの規則を適用する取り組んでいます「権限がある」[パッケージ マニフェスト](http://blog.nuget.org/20141023/package-manifests.html)です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-195">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="dbf7f-196">NuGet の Visual Studio でパッケージの管理を超える別のドメインをクライアントとサーバー コンポーネントを再利用可能なコードベースをリファクタリング取り組んでいます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-196">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="dbf7f-197">「プライベート依存関係の」パッケージことを示すことができますの概念を調査しているお実装の詳細についてのみ、その他のパッケージに依存しているし、これらの依存関係は、最上位レベルの依存関係として表示されるべきではありません。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-197">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="dbf7f-198">待ち</span><span class="sxs-lookup"><span data-stu-id="dbf7f-198">Stay Tuned</span></span>

<span data-ttu-id="dbf7f-199">くださいに注意[私たちのブログ](http://blog.nuget.org)の詳細の進行状況と NuGet 3.0 のお知らせください。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-199">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>