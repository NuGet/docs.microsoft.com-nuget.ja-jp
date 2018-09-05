---
title: NuGet 2.8.2 リリース ノート
description: NuGet 2.8.2 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551149"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="96655-103">NuGet 2.8.2 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="96655-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="96655-104">[NuGet 2.8.1 のリリース ノート](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 リリース ノート](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="96655-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="96655-105">NuGet 2.8.2 は、2014 年 5 月 22 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="96655-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="96655-106">このリリースでは、nuget.exe コマンド ライン、NuGet.Server パッケージおよびその他の NuGet パッケージへの変更のみ含まれます。</span><span class="sxs-lookup"><span data-stu-id="96655-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="96655-107">更新された Visual Studio 拡張機能または WebMatrix 拡張機能をリリースは含まれませんでした。</span><span class="sxs-lookup"><span data-stu-id="96655-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="96655-108">注目すべき更新プログラム</span><span class="sxs-lookup"><span data-stu-id="96655-108">Notable Updates</span></span>

<span data-ttu-id="96655-109">最も注目すべき更新プログラムは、コマンドラインの nuget.exe および NuGet.Server パッケージ (NuGet フィードの自己ホスト型) 用にしました。</span><span class="sxs-lookup"><span data-stu-id="96655-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="96655-110">Nuget.exe 重要なバグの修正</span><span class="sxs-lookup"><span data-stu-id="96655-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="96655-111">nuget.exe プッシュは失敗し、再試行を保持</span><span class="sxs-lookup"><span data-stu-id="96655-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="96655-112">nuget.exe プッシュが基本認証資格情報を正しく送信できません。</span><span class="sxs-lookup"><span data-stu-id="96655-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="96655-113">nuget.exe プッシュは一時的なリダイレクトに従うしません</span><span class="sxs-lookup"><span data-stu-id="96655-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="96655-114">NuGet.Server の重要なバグを修正</span><span class="sxs-lookup"><span data-stu-id="96655-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="96655-115">NuGet.Server によって返される IsAbsoluteLatestVersion の正しくない値</span><span class="sxs-lookup"><span data-stu-id="96655-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="96655-116">パッケージの更新</span><span class="sxs-lookup"><span data-stu-id="96655-116">Packages Updated</span></span>

<span data-ttu-id="96655-117">Nuget.exe コマンドラインと NuGet.Server 修正は、NuGet パッケージの更新プログラムとして出荷されます。</span><span class="sxs-lookup"><span data-stu-id="96655-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="96655-118">その他のパッケージも 2.8.2 で更新が発生しました。</span><span class="sxs-lookup"><span data-stu-id="96655-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="96655-119">更新されたパッケージの一覧を次に示します。</span><span class="sxs-lookup"><span data-stu-id="96655-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="96655-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="96655-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="96655-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="96655-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="96655-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="96655-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="96655-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="96655-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="96655-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (パッケージ、拡張機能ではありません)</span><span class="sxs-lookup"><span data-stu-id="96655-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="96655-125">すべての変更</span><span class="sxs-lookup"><span data-stu-id="96655-125">All Changes</span></span>
<span data-ttu-id="96655-126">リリースで解決された 10 の問題が発生しました。</span><span class="sxs-lookup"><span data-stu-id="96655-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="96655-127">作業の完全な一覧については固定のアイテムの nuget 2.8.2、くださいビュー、[このリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)します。</span><span class="sxs-lookup"><span data-stu-id="96655-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
