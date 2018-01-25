---
title: "NuGet 3.4.4 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.4.4 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 3.4.4 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fabc10ae5c8e0bd43581f85c7763eb23e9483aaf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="fdff5-104">NuGet 3.4.4 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="fdff5-104">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="fdff5-105">[NuGet 3.4.3 リリース ノート](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 ベータ リリース ノート](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="fdff5-105">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="fdff5-106">このリリースの主な目的が 3.4.3 の品質の機能強化で Visual Studio 拡張機能をいくつかの修正 nuget.exe のバージョン。</span><span class="sxs-lookup"><span data-stu-id="fdff5-106">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="fdff5-107">VSIX と nuget.exe の両方をダウンロードする[ここ](https://dist.nuget.org/index.html)です。</span><span class="sxs-lookup"><span data-stu-id="fdff5-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="fdff5-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="fdff5-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="fdff5-109">すべての変更ログ</span><span class="sxs-lookup"><span data-stu-id="fdff5-109">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="fdff5-110">問題の一覧</span><span class="sxs-lookup"><span data-stu-id="fdff5-110">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="fdff5-111">変更</span><span class="sxs-lookup"><span data-stu-id="fdff5-111">Changes</span></span>

- <span data-ttu-id="fdff5-112">パックの改良: の機能強化、シンボルを梱包にパッキング`project.json`詳細および[ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="fdff5-112">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="fdff5-113">更新コマンド内のプロジェクトの検索エラーが発生したときに例外を表示 [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="fdff5-113">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="fdff5-114">パッケージの種類を入力から読み取る`.nuspec`と`project.json`パッキングと[ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="fdff5-114">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="fdff5-115">プロジェクトではなく NuGet.Shared を確認します。</span><span class="sxs-lookup"><span data-stu-id="fdff5-115">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="fdff5-116">\#602</span><span class="sxs-lookup"><span data-stu-id="fdff5-116">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="fdff5-117">HTTP 応答のタイムアウトとしてプッシュ タイムアウトを使用して[ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="fdff5-117">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="fdff5-118">将来の時刻にパッケージ ファイルには、使用される、時間がありません[ \#597。](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="fdff5-118">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="fdff5-119">更新`NuGet.Core.dll`バージョンを XML の問題を解決する 2.12.0 [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="fdff5-119">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="fdff5-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="fdff5-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="fdff5-121">エラーを復元することがなく表示`project.json`または`packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="fdff5-121">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="fdff5-122">必要なバージョンが異なる場合は、依存関係のバージョンを修正して[ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="fdff5-122">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>