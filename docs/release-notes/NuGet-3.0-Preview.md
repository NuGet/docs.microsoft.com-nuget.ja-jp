---
title: NuGet 3.0 Preview リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.0 Preview のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780335"
---
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="96d4d-103">NuGet 3.0 Preview リリースノート</span><span class="sxs-lookup"><span data-stu-id="96d4d-103">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="96d4d-104">[NuGet 2.9 RC リリースノート](../release-notes/nuget-2.9-rc.md)  | [NuGet 3.0 ベータリリースノート](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="96d4d-104">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="96d4d-105">NuGet 3.0 Preview は、Visual Studio 2015 Preview リリースの一部として、2014年11月12日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-105">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="96d4d-106">NuGet 3.0 Preview がリリースされました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-106">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="96d4d-107">これは私たちにとっての大きなリリースです (プレビュー版ではありません)。変更についてフィードバックをお寄せください。</span><span class="sxs-lookup"><span data-stu-id="96d4d-107">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="96d4d-108">Visual Studio 2012 以降</span><span class="sxs-lookup"><span data-stu-id="96d4d-108">Visual Studio 2012+</span></span>

<span data-ttu-id="96d4d-109">この NuGet 3.0 Preview は、Visual Studio 2015 Preview に含まれています。</span><span class="sxs-lookup"><span data-stu-id="96d4d-109">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="96d4d-110">Visual Studio 2012 および Visual Studio 2013 近日中にプレビューが削除される予定です。</span><span class="sxs-lookup"><span data-stu-id="96d4d-110">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="96d4d-111">私たちは、 [Visual Studio 2010 の更新を中止](http://blog.nuget.org/20141002/visual-studio-2010.html)することを以前に共有していましたが、このような難しい決定を行っていました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-111">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="96d4d-112">新しい UI</span><span class="sxs-lookup"><span data-stu-id="96d4d-112">Brand New UI</span></span>

<span data-ttu-id="96d4d-113">NuGet 3.0 Preview に関する最初の注意点は、新しい UI です。</span><span class="sxs-lookup"><span data-stu-id="96d4d-113">The first thing you notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="96d4d-114">これはモーダルダイアログではなくなりました。これで、Visual Studio の完全なドキュメントウィンドウになりました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-114">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="96d4d-115">これにより、一度に複数のプロジェクト (またはソリューション) の UI を開いて、別のモニターにウィンドウを破棄し、必要になったときにドッキングできます。</span><span class="sxs-lookup"><span data-stu-id="96d4d-115">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![新しい NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="96d4d-117">モーダルダイアログを破棄することでユーザビリティの違いを上回るだけでなく、新しい UI にも多くの新機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="96d4d-117">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="96d4d-118">バージョンの選択</span><span class="sxs-lookup"><span data-stu-id="96d4d-118">Version Selection</span></span>

<span data-ttu-id="96d4d-119">おそらく、最も要求の厳しい UI 機能は、パッケージのインストールと更新のバージョン選択を許可することです。これは現在利用可能です。</span><span class="sxs-lookup"><span data-stu-id="96d4d-119">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![パッケージバージョンの選択](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="96d4d-121">パッケージをインストールするか更新するかにかかわらず、[バージョン] ドロップダウンでは、パッケージで使用可能なすべてのバージョンを確認できます。一部のバージョンは、一覧の一番上に昇格して簡単に選択できます。</span><span class="sxs-lookup"><span data-stu-id="96d4d-121">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="96d4d-122">PowerShell コンソールを使用して、最新ではない特定のバージョンを取得する必要がなくなりました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-122">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="96d4d-123">インストール済み/オンライン/更新プログラムの組み合わせのワークフロー</span><span class="sxs-lookup"><span data-stu-id="96d4d-123">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="96d4d-124">前の UI には、インストール済み、オンライン、および更新用の3つのタブがありました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-124">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="96d4d-125">ここに記載されているパッケージは、これらのワークフローに固有のものであり、利用できるアクションもワークフローに固有のものです。</span><span class="sxs-lookup"><span data-stu-id="96d4d-125">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="96d4d-126">このようなことが考えられていましたが、多くの場合、多くの場合、この分離によって多くのことが発生します。</span><span class="sxs-lookup"><span data-stu-id="96d4d-126">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="96d4d-127">これで、パッケージを選択した方法に関係なく、パッケージのインストール、更新、またはアンインストールを行うことができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-127">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="96d4d-128">特定のワークフローを支援するために、[フィルター] ドロップダウンを使用して、表示されているパッケージをフィルター処理できます。ただし、パッケージで使用可能なアクションは一貫しています。</span><span class="sxs-lookup"><span data-stu-id="96d4d-128">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![パッケージのアンインストール](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="96d4d-130">"インストール済み" フィルターを使用すると、インストールされているパッケージを簡単に確認できます。更新プログラムが利用可能な場合は、バージョンの選択を変更して、使用可能なアクションを変更してパッケージをアンインストールまたは更新できます。</span><span class="sxs-lookup"><span data-stu-id="96d4d-130">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![パッケージを更新する](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="96d4d-132">バージョンの統合</span><span class="sxs-lookup"><span data-stu-id="96d4d-132">Version Consolidation</span></span>

<span data-ttu-id="96d4d-133">ソリューション内の複数のプロジェクトに同じパッケージをインストールするのが一般的です。</span><span class="sxs-lookup"><span data-stu-id="96d4d-133">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="96d4d-134">各プロジェクトにインストールされているバージョンが異なる場合があり、使用中のバージョンを統合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="96d4d-134">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="96d4d-135">NuGet 3.0 Preview では、このシナリオのための新機能が導入されました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-135">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="96d4d-136">ソリューションレベルのパッケージ管理ウィンドウにアクセスするには、ソリューションを右クリックし、[ソリューションの NuGet パッケージの管理] を選択します。</span><span class="sxs-lookup"><span data-stu-id="96d4d-136">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="96d4d-137">そこから、複数のプロジェクトにインストールされているパッケージを選択した場合に、異なるバージョンのを使用すると、新しい "統合" アクションが使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="96d4d-137">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="96d4d-138">次のスクリーンショットでは、がにインストールされ、バージョンがにインストールされてい `Newtonsoft.Json` `SamplesClassLibrary` `6.0.4` `SamplesConsoleApp` `5.0.4` ます。</span><span class="sxs-lookup"><span data-stu-id="96d4d-138">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![バージョンの統合](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="96d4d-140">1つのバージョンに統合するためのワークフローを次に示します。</span><span class="sxs-lookup"><span data-stu-id="96d4d-140">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="96d4d-141">一覧からパッケージを選択します `Newtonsoft.Json`</span><span class="sxs-lookup"><span data-stu-id="96d4d-141">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="96d4d-142">`Consolidate` `Action` ドロップダウンから選択</span><span class="sxs-lookup"><span data-stu-id="96d4d-142">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="96d4d-143">ドロップダウンを使用して `Version` 、統合先のバージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="96d4d-143">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="96d4d-144">そのバージョンに統合するプロジェクトのチェックボックスをオンにします (選択したバージョンに既に存在するプロジェクトはグレーで表示されます)。</span><span class="sxs-lookup"><span data-stu-id="96d4d-144">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="96d4d-145">`Consolidate`統合を実行するには、このボタンをクリックします</span><span class="sxs-lookup"><span data-stu-id="96d4d-145">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="96d4d-146">操作のプレビュー</span><span class="sxs-lookup"><span data-stu-id="96d4d-146">Operation Previews</span></span>

<span data-ttu-id="96d4d-147">実行している操作 (インストール/更新/アンインストール) に関係なく、新しい UI では、プロジェクトに対して行われる変更をプレビューする方法が提供されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-147">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="96d4d-148">このプレビューには、インストールされる新しいパッケージ、更新されるパッケージ、および削除されるパッケージと、操作中に変更されないパッケージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="96d4d-148">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="96d4d-149">次の例では、SignalR をインストールすると、プロジェクトに大幅な変更が加えられることがわかります。</span><span class="sxs-lookup"><span data-stu-id="96d4d-149">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![SignalR のインストールのプレビュー](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="96d4d-151">インストール オプション</span><span class="sxs-lookup"><span data-stu-id="96d4d-151">Installation Options</span></span>

<span data-ttu-id="96d4d-152">PowerShell コンソールを使用して、いくつかの注目すべきインストールオプションを制御できました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-152">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="96d4d-153">これらの機能が UI にも組み込まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-153">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="96d4d-154">依存関係のバージョンを選択する方法について、依存関係の解決動作を制御できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-154">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![依存関係の動作](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="96d4d-156">また、パッケージのコンテンツファイルがプロジェクト内の既存のファイルと競合する場合に実行するアクションを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="96d4d-156">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![ファイルの競合アクション](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="96d4d-158">無限スクロール</span><span class="sxs-lookup"><span data-stu-id="96d4d-158">Infinite Scrolling</span></span>

<span data-ttu-id="96d4d-159">パッケージの一覧を表示するときに、スクロールとページングの両方のパラダイムを持つ UI について、非常に多くのフィードバックを取得していました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-159">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="96d4d-160">短い一覧の一番下までスクロールし、次のページ番号をクリックしてから、もう一度スクロールする必要がありました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-160">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="96d4d-161">新しい UI では、[パッケージ] の一覧に無限のスクロールが実装されているため、スクロールのみが必要になり、ページングが不要になります。</span><span class="sxs-lookup"><span data-stu-id="96d4d-161">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![無限スクロール](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="96d4d-163">作業をして迅速に実行する</span><span class="sxs-lookup"><span data-stu-id="96d4d-163">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="96d4d-164">この新しい UI を試してみることをお待ちしております。このプレビューのマイルストーンでは、"it の動作を向上させ、迅速に作成してください" という古い格言に従うことになりました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-164">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="96d4d-165">このプレビューでは、最初の目標のほとんどを達成しました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-165">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="96d4d-166">まだ非常に高速ではないことがわかっています。</span><span class="sxs-lookup"><span data-stu-id="96d4d-166">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="96d4d-167">現在と RC リリースの間でこれらの目標に取り組んでいることを信頼します。</span><span class="sxs-lookup"><span data-stu-id="96d4d-167">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="96d4d-168">*それまで* の間は、新しい ui の *使いやすさ* に関するフィードバック (ワークフロー、操作、新しい ui の使用方法など) についてご意見をお寄せください。</span><span class="sxs-lookup"><span data-stu-id="96d4d-168">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="96d4d-169">古い UI と比較すると、いくつかの関数が削除されています。</span><span class="sxs-lookup"><span data-stu-id="96d4d-169">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="96d4d-170">これらのうちの1つは意図的なものであり、もう1つは時間内には実行されませんでした。</span><span class="sxs-lookup"><span data-stu-id="96d4d-170">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="96d4d-171">"すべて" のパッケージソースを検索しています</span><span class="sxs-lookup"><span data-stu-id="96d4d-171">Searching "All" Package Sources</span></span>

<span data-ttu-id="96d4d-172">古い UI では、すべてのパッケージソースに対してパッケージ検索を実行できました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-172">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="96d4d-173">この機能は UI から削除されており、元に戻されることはありません。</span><span class="sxs-lookup"><span data-stu-id="96d4d-173">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="96d4d-174">この機能は、すべてのパッケージソースに対して検索操作を実行し、結果を比較して、並べ替えの選択に基づいて結果の順序付けを試行するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="96d4d-174">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="96d4d-175">検索の関連性は、一体にするのが非常に困難であることがわかりました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-175">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="96d4d-176">Google と Bing に対して検索を実行して、結果を揺れ動くにすることを想像してみてください。</span><span class="sxs-lookup"><span data-stu-id="96d4d-176">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="96d4d-177">また、この機能は低速で、 *誤っ* て使用することが簡単であり、実際にはあまり役に立ちませんでした。</span><span class="sxs-lookup"><span data-stu-id="96d4d-177">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="96d4d-178">機能に関する問題のために、修正されていない可能性があるバグレポートをいくつか受け取りました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-178">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="96d4d-179">すべて更新</span><span class="sxs-lookup"><span data-stu-id="96d4d-179">Update All</span></span>

<span data-ttu-id="96d4d-180">以前の UI には、新しい UI にはまだない [すべて更新] ボタンを使用しました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-180">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="96d4d-181">RC リリースでは、この機能をやり直すします。</span><span class="sxs-lookup"><span data-stu-id="96d4d-181">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="96d4d-182">新しいクライアント/サーバー API</span><span class="sxs-lookup"><span data-stu-id="96d4d-182">New Client/Server API</span></span>

<span data-ttu-id="96d4d-183">新しいパッケージ管理 UI の新機能のすべてに加えて、NuGet のクライアント/サーバープロトコルの実装の詳細についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="96d4d-183">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="96d4d-184">ここで行った作業は、パッケージの復元やパッケージのインストールなどの重要なシナリオに対して高可用性を重視して設計された NuGet 用の "API v3" を作成することです。</span><span class="sxs-lookup"><span data-stu-id="96d4d-184">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="96d4d-185">新しい API は、REST とハイパーメディアに基づいており、リソース形式として [JSON-LD](http://json-ld.org) を選択しています。</span><span class="sxs-lookup"><span data-stu-id="96d4d-185">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="96d4d-186">NuGet 3.0 Preview ビットでは、[パッケージソース] ボックスの一覧に "preview.nuget.org" という新しいパッケージソースが表示されます。</span><span class="sxs-lookup"><span data-stu-id="96d4d-186">In the NuGet 3.0 Preview bits, you see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="96d4d-187">そのパッケージソースを選択した場合は、新しい API を使用して nuget.org に接続します。UI でプレビューソースを使用できるようにしましたが、新しい API のテスト、改訂、および改善を続けています。</span><span class="sxs-lookup"><span data-stu-id="96d4d-187">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="96d4d-188">NuGet 3.0 RC では、この新しい API v3 ベースのパッケージソースによって、v2 ベースの "nuget.org" パッケージソースが置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="96d4d-188">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="96d4d-189">API v3 に導入されている投資にかかわらず、これらの新機能はすべて、既存の API v2 プロトコルでも動作します。つまり、nuget.org 以外の既存のパッケージソースでも動作します。</span><span class="sxs-lookup"><span data-stu-id="96d4d-189">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="96d4d-190">新機能</span><span class="sxs-lookup"><span data-stu-id="96d4d-190">New Features Coming</span></span>

<span data-ttu-id="96d4d-191">現時点と 3.0 RTM では、UI に表示されるもの以外に、いくつかの基本的な新しい NuGet 機能についても取り組んでいます。</span><span class="sxs-lookup"><span data-stu-id="96d4d-191">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you see in the UI.</span></span> <span data-ttu-id="96d4d-192">次に、注目すべき投資分野の簡単な一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="96d4d-192">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="96d4d-193">Visual Studio および MSBuild チームと提携して、NuGet を [プラットフォームに深く](http://blog.nuget.org/20141014/in-the-platform.html)活用します。</span><span class="sxs-lookup"><span data-stu-id="96d4d-193">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="96d4d-194">ここでは、インストール時のパッケージ規則を破棄し、代わりに、新しい "権限のある" [パッケージマニフェスト](http://blog.nuget.org/20141023/package-manifests.html)を導入することによって、パッケージ化時にそれらの規則を適用しています。</span><span class="sxs-lookup"><span data-stu-id="96d4d-194">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="96d4d-195">ここでは、NuGet コードベースをリファクターして、Visual Studio のパッケージ管理以外の異なるドメインでクライアントとサーバーのコンポーネントを再利用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="96d4d-195">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="96d4d-196">"プライベートな依存関係" の概念を調査しています。パッケージは、実装の詳細のみを対象として他のパッケージへの依存関係があることを示すことができ、それらの依存関係をトップレベルの依存関係として表示することはできません。</span><span class="sxs-lookup"><span data-stu-id="96d4d-196">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="96d4d-197">引き続きご期待ください</span><span class="sxs-lookup"><span data-stu-id="96d4d-197">Stay Tuned</span></span>

<span data-ttu-id="96d4d-198">NuGet 3.0 の進行状況と発表の詳細については、 [ブログをご覧](http://blog.nuget.org) ください。</span><span class="sxs-lookup"><span data-stu-id="96d4d-198">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>