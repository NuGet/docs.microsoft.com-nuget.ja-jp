---
title: "NuGet 2.8.2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "NuGet 2.8.2 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.8.2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="b3e3f-104">NuGet 2.8.2 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="b3e3f-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="b3e3f-105">[NuGet 2.8.1 リリース ノート](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 リリース ノート](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="b3e3f-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="b3e3f-106">NuGet 2.8.2 は、22、2014 年 5 月にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="b3e3f-107">このリリースには、のみ、変更するコマンド ライン nuget.exe NuGet.Server パッケージとその他の NuGet パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="b3e3f-108">更新された Visual Studio 拡張機能または WebMatrix 拡張機能、リリースは含まれませんでした。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="b3e3f-109">重要な更新プログラム</span><span class="sxs-lookup"><span data-stu-id="b3e3f-109">Notable Updates</span></span>

<span data-ttu-id="b3e3f-110">代表的な更新プログラムは、コマンド ライン nuget.exe と NuGet.Server パッケージ (NuGet フィードの自己ホスト型) 用にしました。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="b3e3f-111">重要な nuget.exe バグ修正</span><span class="sxs-lookup"><span data-stu-id="b3e3f-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="b3e3f-112">nuget.exe プッシュが失敗し、再試行を保持</span><span class="sxs-lookup"><span data-stu-id="b3e3f-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="b3e3f-113">nuget.exe プッシュに基本認証資格情報が正しく送信できません。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="b3e3f-114">nuget.exe プッシュは一時的なリダイレクトに従うされません。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="b3e3f-115">重要な NuGet.Server バグ修正</span><span class="sxs-lookup"><span data-stu-id="b3e3f-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="b3e3f-116">間違った IsAbsoluteLatestVersion NuGet.Server によって返される値</span><span class="sxs-lookup"><span data-stu-id="b3e3f-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="b3e3f-117">更新パッケージ</span><span class="sxs-lookup"><span data-stu-id="b3e3f-117">Packages Updated</span></span>

<span data-ttu-id="b3e3f-118">Nuget.exe コマンドラインと NuGet.Server 修正は、NuGet パッケージの更新プログラムとして出荷されます。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="b3e3f-119">その他のパッケージも 2.8.2 で更新が発生しました。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="b3e3f-120">更新したパッケージの一覧を次に示します。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="b3e3f-121">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="b3e3f-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="b3e3f-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="b3e3f-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="b3e3f-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="b3e3f-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="b3e3f-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="b3e3f-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="b3e3f-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (パッケージ、拡張子ではなく)</span><span class="sxs-lookup"><span data-stu-id="b3e3f-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="b3e3f-126">すべての変更</span><span class="sxs-lookup"><span data-stu-id="b3e3f-126">All Changes</span></span>
<span data-ttu-id="b3e3f-127">リリースで解決される 10 の問題が発生しました。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="b3e3f-128">作業の完全な一覧の項目で修正 NuGet 2.8.2、くださいビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)です。</span><span class="sxs-lookup"><span data-stu-id="b3e3f-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
