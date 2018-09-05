---
title: NuGet 2.2 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.2 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545993"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="92c91-103">NuGet 2.2 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="92c91-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="92c91-104">[NuGet 2.1 リリース ノート](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 リリース ノート](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="92c91-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="92c91-105">NuGet 2.2 は、2012 年 12 月 12 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="92c91-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="92c91-106">Visual Studio のクイック起動</span><span class="sxs-lookup"><span data-stu-id="92c91-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="92c91-107">Visual Studio 2012 で追加された新機能の 1 つが、[クイック起動ダイアログ](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)します。</span><span class="sxs-lookup"><span data-stu-id="92c91-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="92c91-108">NuGet 2.2 では、クイック起動で入力した検索語句でパッケージ マネージャー ダイアログを初期化することができます、このダイアログ ボックスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="92c91-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="92c91-109">クイック起動で"jquery"を入力すると、今すぐなどには、"jquery"に一致する NuGet パッケージの検索結果でオプションを含まれます。</span><span class="sxs-lookup"><span data-stu-id="92c91-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Visual Studio のクイック起動の NuGet](./media/quick-launch.png)

<span data-ttu-id="92c91-111">このオプションを選択すると、"jquery"という用語の標準的な NuGet パッケージ マネージャー検索エクスペリエンスが起動します。</span><span class="sxs-lookup"><span data-stu-id="92c91-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![あらかじめ設定されている NuGet パッケージ マネージャー ダイアログ ボックス](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="92c91-113">パッケージのコンテンツのフォルダー全体を指定します。</span><span class="sxs-lookup"><span data-stu-id="92c91-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="92c91-114">NuGet 2.2 のフォルダー全体を指定できるようになりました、`<file>`の要素、`.nuspec`ファイルをそのフォルダーの内容のすべてが含まれます。</span><span class="sxs-lookup"><span data-stu-id="92c91-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="92c91-115">たとえば、次によりすべてのスクリプト パッケージのスクリプト フォルダーをプロジェクトにパッケージがインストールされている場合、contents\scripts フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="92c91-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="92c91-116">**6/24/16 の更新: パッケージをインストールするときに、"content"フォルダー内の空のフォルダーは無視されます。**</span><span class="sxs-lookup"><span data-stu-id="92c91-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="92c91-117">既知の問題</span><span class="sxs-lookup"><span data-stu-id="92c91-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="92c91-118">パッケージ マネージャー コンソールを使用する場合、f# プロジェクトのパッケージのインストールが失敗しました。</span><span class="sxs-lookup"><span data-stu-id="92c91-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="92c91-119">パッケージ マネージャー コンソールを使用して、f# プロジェクトに NuGet パッケージをインストールしようとすると、InvalidOperationException がスローされます。</span><span class="sxs-lookup"><span data-stu-id="92c91-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="92c91-120">問題を解決するには、f# チームと協力して積極的にいますが、それまでは、回避は、コンソールではなく、NuGet のパッケージ マネージャー ダイアログ ボックスを使用して、f# のプロジェクトに NuGet パッケージをインストールするには。</span><span class="sxs-lookup"><span data-stu-id="92c91-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="92c91-121">[詳細については、codeplex から入手できる](http://nuget.codeplex.com/workitem/2873)します。</span><span class="sxs-lookup"><span data-stu-id="92c91-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="92c91-122">バグ修正</span><span class="sxs-lookup"><span data-stu-id="92c91-122">Bug Fixes</span></span>
<span data-ttu-id="92c91-123">NuGet 2.2 には、多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="92c91-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="92c91-124">作業の完全な一覧の項目で修正された NuGet 2.2、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)します。</span><span class="sxs-lookup"><span data-stu-id="92c91-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
