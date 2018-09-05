---
title: NuGet 3.4.4 リリース ノート
description: NuGet 3.4.4 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547474"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="b637f-103">NuGet 3.4.4 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="b637f-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="b637f-104">[NuGet 3.4.3 リリース ノート](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 のベータ リリース ノート](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="b637f-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="b637f-105">このリリースの主な目的が 3.4.3 の品質の機能強化を Visual Studio 拡張機能のいくつかの修正と nuget.exe のバージョン。</span><span class="sxs-lookup"><span data-stu-id="b637f-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="b637f-106">VSIX と nuget.exe の両方をダウンロードする[ここ](https://dist.nuget.org/index.html)します。</span><span class="sxs-lookup"><span data-stu-id="b637f-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="b637f-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="b637f-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="b637f-108">完全な変更ログ</span><span class="sxs-lookup"><span data-stu-id="b637f-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="b637f-109">問題の一覧</span><span class="sxs-lookup"><span data-stu-id="b637f-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="b637f-110">変更</span><span class="sxs-lookup"><span data-stu-id="b637f-110">Changes</span></span>

- <span data-ttu-id="b637f-111">パックの改良: の機能強化、シンボルのパックと梱包`project.json`詳細と[ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="b637f-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="b637f-112">Update コマンド内のプロジェクトの検索エラーがある場合に表示される例外 [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="b637f-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="b637f-113">パッケージの種類を入力から読み取る`.nuspec`と`project.json`パックするときに[ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="b637f-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="b637f-114">プロジェクトではない NuGet.Shared を確認します。</span><span class="sxs-lookup"><span data-stu-id="b637f-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="b637f-115">\#602</span><span class="sxs-lookup"><span data-stu-id="b637f-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="b637f-116">プッシュのタイムアウトを使用して、HTTP 応答のタイムアウトとして[ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="b637f-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="b637f-117">将来の時間のパッケージ ファイルには、使用、時刻はありません[ \#597。](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="b637f-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="b637f-118">更新`NuGet.Core.dll`2.12.0 XML 問題を解決するにはバージョン[ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="b637f-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="b637f-119">サポート./NuGet.CommandLine.XPlat v\<詳細度\>\<モード\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="b637f-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="b637f-120">エラーを復元することがなく表示`project.json`または`packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="b637f-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="b637f-121">必要なバージョンが異なる場合に、依存関係のバージョンを修正[ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="b637f-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>