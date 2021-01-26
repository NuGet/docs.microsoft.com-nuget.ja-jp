---
title: NuGet 2.2 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780434"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="51c3e-103">NuGet 2.2 リリースノート</span><span class="sxs-lookup"><span data-stu-id="51c3e-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="51c3e-104">[NuGet 2.1 リリースノート](../release-notes/nuget-2.1.md)  | [NuGet 2.2.1 リリースノート](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="51c3e-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="51c3e-105">NuGet 2.2 は、2012年12月12日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="51c3e-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="51c3e-106">Visual Studio のクイック起動</span><span class="sxs-lookup"><span data-stu-id="51c3e-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="51c3e-107">Visual Studio 2012 で追加された新機能の1つに、[ [クイック起動] ダイアログ](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)がありました。</span><span class="sxs-lookup"><span data-stu-id="51c3e-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="51c3e-108">NuGet 2.2 では、このダイアログボックスが拡張され、クイック起動に入力された検索語句を使用してパッケージマネージャーダイアログを初期化できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="51c3e-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="51c3e-109">たとえば、クイック起動で「jquery」と入力すると、' jquery ' に一致する NuGet パッケージを検索するためのオプションが結果に含まれるようになります。</span><span class="sxs-lookup"><span data-stu-id="51c3e-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Visual Studio の NuGet のクイック起動](./media/quick-launch.png)

<span data-ttu-id="51c3e-111">このオプションを選択すると、"jquery" という用語に対して標準の NuGet パッケージマネージャーの検索エクスペリエンスが起動します。</span><span class="sxs-lookup"><span data-stu-id="51c3e-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![事前設定された NuGet パッケージマネージャーダイアログ](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="51c3e-113">パッケージコンテンツのフォルダー全体を指定する</span><span class="sxs-lookup"><span data-stu-id="51c3e-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="51c3e-114">NuGet 2.2 では、ファイルの要素にフォルダー全体を指定し `<file>` `.nuspec` て、そのフォルダーのすべての内容を含めることができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="51c3e-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="51c3e-115">たとえば、次のようにすると、パッケージがプロジェクトにインストールされるときに、パッケージの scripts フォルダー内のすべてのスクリプトが content\ scripts フォルダーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="51c3e-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="51c3e-116">**更新プログラム 6/24/16: パッケージのインストール時に、"content" フォルダー内の空のフォルダーは無視されます。**</span><span class="sxs-lookup"><span data-stu-id="51c3e-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="51c3e-117">既知の問題</span><span class="sxs-lookup"><span data-stu-id="51c3e-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="51c3e-118">パッケージマネージャーコンソールを使用すると、F # プロジェクトのパッケージのインストールが失敗する</span><span class="sxs-lookup"><span data-stu-id="51c3e-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="51c3e-119">パッケージマネージャーコンソールを使用して NuGet パッケージを F # プロジェクトにインストールしようとすると、InvalidOperationException がスローされます。</span><span class="sxs-lookup"><span data-stu-id="51c3e-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="51c3e-120">私たちは問題を解決するために F # チームと積極的に連携していますが、その間は、コンソールではなく NuGet の [パッケージマネージャー] ダイアログを使用して、NuGet パッケージを F # プロジェクトにインストールすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="51c3e-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="51c3e-121">[詳細については、CodePlex を](http://nuget.codeplex.com/workitem/2873)参照してください。</span><span class="sxs-lookup"><span data-stu-id="51c3e-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="51c3e-122">バグの修正</span><span class="sxs-lookup"><span data-stu-id="51c3e-122">Bug Fixes</span></span>
<span data-ttu-id="51c3e-123">NuGet 2.2 には、多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="51c3e-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="51c3e-124">NuGet 2.2 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="51c3e-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
