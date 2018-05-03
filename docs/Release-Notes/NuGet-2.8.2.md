---
title: NuGet 2.8.2 リリース ノート
description: NuGet 2.8.2 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="f3e60-103">NuGet 2.8.2 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="f3e60-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="f3e60-104">[NuGet 2.8.1 リリース ノート](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 リリース ノート](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="f3e60-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="f3e60-105">NuGet 2.8.2 は、22、2014 年 5 月にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="f3e60-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="f3e60-106">このリリースには、のみ、変更するコマンド ライン nuget.exe NuGet.Server パッケージとその他の NuGet パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3e60-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="f3e60-107">更新された Visual Studio 拡張機能または WebMatrix 拡張機能、リリースは含まれませんでした。</span><span class="sxs-lookup"><span data-stu-id="f3e60-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="f3e60-108">重要な更新プログラム</span><span class="sxs-lookup"><span data-stu-id="f3e60-108">Notable Updates</span></span>

<span data-ttu-id="f3e60-109">代表的な更新プログラムは、コマンド ライン nuget.exe と NuGet.Server パッケージ (NuGet フィードの自己ホスト型) 用にしました。</span><span class="sxs-lookup"><span data-stu-id="f3e60-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="f3e60-110">重要な nuget.exe バグ修正</span><span class="sxs-lookup"><span data-stu-id="f3e60-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="f3e60-111">nuget.exe プッシュが失敗し、再試行を保持</span><span class="sxs-lookup"><span data-stu-id="f3e60-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="f3e60-112">nuget.exe プッシュに基本認証資格情報が正しく送信できません。</span><span class="sxs-lookup"><span data-stu-id="f3e60-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="f3e60-113">nuget.exe プッシュは一時的なリダイレクトに従うされません。</span><span class="sxs-lookup"><span data-stu-id="f3e60-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="f3e60-114">重要な NuGet.Server バグ修正</span><span class="sxs-lookup"><span data-stu-id="f3e60-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="f3e60-115">間違った IsAbsoluteLatestVersion NuGet.Server によって返される値</span><span class="sxs-lookup"><span data-stu-id="f3e60-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="f3e60-116">更新パッケージ</span><span class="sxs-lookup"><span data-stu-id="f3e60-116">Packages Updated</span></span>

<span data-ttu-id="f3e60-117">Nuget.exe コマンドラインと NuGet.Server 修正は、NuGet パッケージの更新プログラムとして出荷されます。</span><span class="sxs-lookup"><span data-stu-id="f3e60-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="f3e60-118">その他のパッケージも 2.8.2 で更新が発生しました。</span><span class="sxs-lookup"><span data-stu-id="f3e60-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="f3e60-119">更新したパッケージの一覧を次に示します。</span><span class="sxs-lookup"><span data-stu-id="f3e60-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="f3e60-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="f3e60-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="f3e60-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="f3e60-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="f3e60-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="f3e60-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="f3e60-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="f3e60-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="f3e60-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (パッケージ、拡張子ではなく)</span><span class="sxs-lookup"><span data-stu-id="f3e60-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="f3e60-125">すべての変更</span><span class="sxs-lookup"><span data-stu-id="f3e60-125">All Changes</span></span>
<span data-ttu-id="f3e60-126">リリースで解決される 10 の問題が発生しました。</span><span class="sxs-lookup"><span data-stu-id="f3e60-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="f3e60-127">作業の完全な一覧の項目で修正 NuGet 2.8.2、くださいビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)です。</span><span class="sxs-lookup"><span data-stu-id="f3e60-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
