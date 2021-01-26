---
title: NuGet 2.8.2 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.8.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780373"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="60da7-103">NuGet 2.8.2 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="60da7-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="60da7-104">[NuGet 2.8.1 のリリースノート](../release-notes/nuget-2.8.1.md)  | [NuGet 2.8.3 のリリースノート](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="60da7-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="60da7-105">NuGet 2.8.2 は2014年5月22日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="60da7-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="60da7-106">このリリースには、nuget.exe コマンドライン、Nuget.exe パッケージ、およびその他の NuGet パッケージに対する変更のみが含まれていました。</span><span class="sxs-lookup"><span data-stu-id="60da7-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="60da7-107">リリースには、更新された Visual Studio 拡張機能または WebMatrix 拡張機能が含まれていませんでした。</span><span class="sxs-lookup"><span data-stu-id="60da7-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="60da7-108">注目に値する更新</span><span class="sxs-lookup"><span data-stu-id="60da7-108">Notable Updates</span></span>

<span data-ttu-id="60da7-109">最も注目すべき更新プログラムは、nuget.exe コマンドラインと、(自己ホスト型 NuGet フィード用の) サーバーパッケージに含まれていました。</span><span class="sxs-lookup"><span data-stu-id="60da7-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="60da7-110">重要な nuget.exe バグ修正</span><span class="sxs-lookup"><span data-stu-id="60da7-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="60da7-111">nuget.exe プッシュが失敗して再試行を続ける</span><span class="sxs-lookup"><span data-stu-id="60da7-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="60da7-112">nuget.exe プッシュでは基本的な認証資格情報が正しく送信されない</span><span class="sxs-lookup"><span data-stu-id="60da7-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="60da7-113">nuget.exe Push が一時的なリダイレクトに従わない</span><span class="sxs-lookup"><span data-stu-id="60da7-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="60da7-114">重要な NuGet. サーバーのバグ修正</span><span class="sxs-lookup"><span data-stu-id="60da7-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="60da7-115">NuGet によって返された IsAbsoluteLatestVersion の値が間違っています</span><span class="sxs-lookup"><span data-stu-id="60da7-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="60da7-116">更新されたパッケージ</span><span class="sxs-lookup"><span data-stu-id="60da7-116">Packages Updated</span></span>

<span data-ttu-id="60da7-117">nuget.exe のコマンドラインと NuGet の修正プログラムは、NuGet パッケージの更新プログラムとして出荷されます。</span><span class="sxs-lookup"><span data-stu-id="60da7-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="60da7-118">他のパッケージも2.8.2 で更新されています。</span><span class="sxs-lookup"><span data-stu-id="60da7-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="60da7-119">更新されたパッケージの一覧を次に示します。</span><span class="sxs-lookup"><span data-stu-id="60da7-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="60da7-120">NuGet. コア</span><span class="sxs-lookup"><span data-stu-id="60da7-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="60da7-121">Nuget.exe コマンドライン</span><span class="sxs-lookup"><span data-stu-id="60da7-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="60da7-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="60da7-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="60da7-123">NuGet。ビルド</span><span class="sxs-lookup"><span data-stu-id="60da7-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="60da7-124">[VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (拡張子ではなくパッケージ)</span><span class="sxs-lookup"><span data-stu-id="60da7-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="60da7-125">すべての変更</span><span class="sxs-lookup"><span data-stu-id="60da7-125">All Changes</span></span>
<span data-ttu-id="60da7-126">このリリースでは、10件の問題が解決されました。</span><span class="sxs-lookup"><span data-stu-id="60da7-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="60da7-127">NuGet 2.8.2 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="60da7-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
