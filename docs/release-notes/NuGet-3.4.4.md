---
title: NuGet 3.4.4 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.4.4 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780228"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="ccb52-103">NuGet 3.4.4 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="ccb52-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="ccb52-104">[NuGet 3.4.3 のリリースノート](../release-notes/nuget-3.4.3.md)  | [NuGet 3.5-ベータリリースノート](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="ccb52-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="ccb52-105">このリリースの主な目的は、Visual Studio 拡張機能に対していくつかの修正を加えて、nuget.exe の3.4.3 バージョンの品質を向上させることでした。</span><span class="sxs-lookup"><span data-stu-id="ccb52-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="ccb52-106">VSIX と nuget.exe の両方を [ここで](https://dist.nuget.org/index.html)ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="ccb52-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="ccb52-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="ccb52-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="ccb52-108">完全な Changelog</span><span class="sxs-lookup"><span data-stu-id="ccb52-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="ccb52-109">問題の一覧</span><span class="sxs-lookup"><span data-stu-id="ccb52-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="ccb52-110">[変更点]</span><span class="sxs-lookup"><span data-stu-id="ccb52-110">Changes</span></span>

- <span data-ttu-id="ccb52-111">パックの改善: シンボルのパッキングの改善、606でのパッキング、 `project.json` およびその他の[ \# ](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="ccb52-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="ccb52-112">Update コマンドでプロジェクトの検索エラーが発生したときに例外を表示する [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="ccb52-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="ccb52-113">入力からのパッケージの種類の読み取り `.nuspec` と、 `project.json` [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)のパッキング</span><span class="sxs-lookup"><span data-stu-id="ccb52-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="ccb52-114">NuGet を作成します。共有はプロジェクトではありません。</span><span class="sxs-lookup"><span data-stu-id="ccb52-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="ccb52-115">\#602</span><span class="sxs-lookup"><span data-stu-id="ccb52-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="ccb52-116">HTTP 応答タイムアウト[ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)としてプッシュタイムアウトを使用する</span><span class="sxs-lookup"><span data-stu-id="ccb52-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="ccb52-117">将来の時刻を含むパッケージファイルの使用時間は[ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="ccb52-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="ccb52-118">`NuGet.Core.dll`XML の問題を修正するためにバージョンを2.12.0 に更新しています[ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="ccb52-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="ccb52-119">サポート./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="ccb52-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="ccb52-120">`project.json`または `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)を使用せずに復元エラーを表示する</span><span class="sxs-lookup"><span data-stu-id="ccb52-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="ccb52-121">必要なバージョンが異なる場合の依存関係バージョンの修正[ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="ccb52-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>