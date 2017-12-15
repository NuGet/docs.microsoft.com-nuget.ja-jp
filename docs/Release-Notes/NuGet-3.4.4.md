---
title: "NuGet 3.4.4 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f0aa9bb-75e5-429d-9954-3cb41a909c14
description: "NuGet 3.4.4 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 3.4.4 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 51ddb918d2269990588e9cba4d15ffeb878de5f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="3b957-104">NuGet 3.4.4 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="3b957-104">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="3b957-105">[NuGet 3.4.3 リリース ノート](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 ベータ リリース ノート](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="3b957-105">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="3b957-106">このリリースの主な目的が 3.4.3 の品質の機能強化で Visual Studio 拡張機能をいくつかの修正 nuget.exe のバージョン。</span><span class="sxs-lookup"><span data-stu-id="3b957-106">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="3b957-107">VSIX と nuget.exe の両方をダウンロードする[ここ](https://dist.nuget.org/index.html)です。</span><span class="sxs-lookup"><span data-stu-id="3b957-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="3b957-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="3b957-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="3b957-109">すべての変更ログ</span><span class="sxs-lookup"><span data-stu-id="3b957-109">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="3b957-110">問題の一覧</span><span class="sxs-lookup"><span data-stu-id="3b957-110">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="3b957-111">変更</span><span class="sxs-lookup"><span data-stu-id="3b957-111">Changes</span></span>

- <span data-ttu-id="3b957-112">パックの改良: の機能強化、シンボルを梱包にパッキング`project.json`詳細および[ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="3b957-112">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="3b957-113">更新コマンド内のプロジェクトの検索エラーが発生したときに例外を表示 [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="3b957-113">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="3b957-114">パッケージの種類を入力から読み取る`.nuspec`と`project.json`パッキングと[ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="3b957-114">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="3b957-115">プロジェクトではなく NuGet.Shared を確認します。</span><span class="sxs-lookup"><span data-stu-id="3b957-115">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="3b957-116">\#602</span><span class="sxs-lookup"><span data-stu-id="3b957-116">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="3b957-117">HTTP 応答のタイムアウトとしてプッシュ タイムアウトを使用して[ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="3b957-117">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="3b957-118">将来の時刻にパッケージ ファイルには、使用される、時間がありません[ \#597。](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="3b957-118">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="3b957-119">更新`NuGet.Core.dll`バージョンを XML の問題を解決する 2.12.0 [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="3b957-119">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="3b957-120">サポート./NuGet.CommandLine.XPlat v\<詳細度\>\<モード\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="3b957-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="3b957-121">エラーを復元することがなく表示`project.json`または`packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="3b957-121">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="3b957-122">必要なバージョンが異なる場合は、依存関係のバージョンを修正して[ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="3b957-122">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>