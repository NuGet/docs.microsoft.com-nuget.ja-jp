---
title: "NuGet 2.2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.2 リリース ノートです。"
keywords: "NuGet 2.2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 63a1ae2315ea0c26fb5d26507ac0bcba8567aa9a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="18e98-104">NuGet 2.2 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="18e98-104">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="18e98-105">[NuGet 2.1 リリース ノート](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 リリース ノート](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="18e98-105">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="18e98-106">NuGet 2.2 は、2012 年 12 月 12 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="18e98-106">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="18e98-107">Visual Studio のクイック起動</span><span class="sxs-lookup"><span data-stu-id="18e98-107">Visual Studio Quick Launch</span></span>
<span data-ttu-id="18e98-108">Visual Studio 2012 で追加された新機能の 1 つが、[クイック起動ダイアログ](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)です。</span><span class="sxs-lookup"><span data-stu-id="18e98-108">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="18e98-109">NuGet 2.2 は、クイック起動 で入力した検索語句をパッケージ マネージャー ダイアログを初期化できるようにこのダイアログ ボックスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="18e98-109">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="18e98-110">たとえば、'jquery' を今サイド リンク バーに入力するオプションが含まれます 'jquery' と一致する NuGet パッケージを検索する結果にします。</span><span class="sxs-lookup"><span data-stu-id="18e98-110">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Visual Studio のクイック起動で NuGet](./media/quick-launch.png)

<span data-ttu-id="18e98-112">このオプションを選択すると、という用語は、'jquery' の標準的な NuGet パッケージ マネージャー検索エクスペリエンスが起動します。</span><span class="sxs-lookup"><span data-stu-id="18e98-112">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![事前設定済みの NuGet パッケージ マネージャー ダイアログ ボックス](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="18e98-114">パッケージの内容をフォルダー全体を指定します。</span><span class="sxs-lookup"><span data-stu-id="18e98-114">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="18e98-115">NuGet 2.2 でフォルダー全体を指定できるようになりました、`<file>`の要素、`.nuspec`ファイルをそのフォルダーの内容のすべてが含まれます。</span><span class="sxs-lookup"><span data-stu-id="18e98-115">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="18e98-116">たとえば、次によりすべてのスクリプトをプロジェクトにパッケージがインストールされている場合、contents\scripts フォルダーに追加するパッケージのスクリプト フォルダーにされます。</span><span class="sxs-lookup"><span data-stu-id="18e98-116">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="18e98-117">**6/24/16 を更新します。 パッケージをインストールするときに、"content"フォルダーに空のフォルダーは無視されます。**</span><span class="sxs-lookup"><span data-stu-id="18e98-117">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="18e98-118">既知の問題</span><span class="sxs-lookup"><span data-stu-id="18e98-118">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="18e98-119">パッケージ マネージャー コンソールを使用する場合、f# プロジェクトのパッケージのインストールが失敗します。</span><span class="sxs-lookup"><span data-stu-id="18e98-119">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="18e98-120">パッケージ マネージャー コンソールを使用して、f# プロジェクトに NuGet パッケージをインストールしようとすると、ときに、InvalidOperationException がスローされます。</span><span class="sxs-lookup"><span data-stu-id="18e98-120">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="18e98-121">私たちは積極的に連携し、問題を解決するには、f# チームがその間は、回避策は、コンソールではなく、NuGet のパッケージ マネージャー ダイアログ ボックスを使用して、f# のプロジェクトに NuGet パッケージのインストールします。</span><span class="sxs-lookup"><span data-stu-id="18e98-121">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="18e98-122">[詳細については、codeplex から入手できる](http://nuget.codeplex.com/workitem/2873)です。</span><span class="sxs-lookup"><span data-stu-id="18e98-122">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="18e98-123">バグ修正</span><span class="sxs-lookup"><span data-stu-id="18e98-123">Bug Fixes</span></span>
<span data-ttu-id="18e98-124">NuGet 2.2 には、多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="18e98-124">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="18e98-125">作業の完全な一覧アイテムを固定 NuGet 2.2 でくださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="18e98-125">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
