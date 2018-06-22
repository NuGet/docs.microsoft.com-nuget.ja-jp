---
title: NuGet 2.9 RC のリリース ノート
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.9 RC のリリース ノートします。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 15665e7c3f9f638b434b0d7be2f7ff3215c787c6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819376"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="2ba75-103">NuGet 2.9 RC のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="2ba75-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="2ba75-104">[NuGet 2.8.7 リリース ノート](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 プレビューのリリース ノート](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="2ba75-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="2ba75-105">NuGet 2.9 は 2015 年 9 月 10 日を 2.8.7 に更新プログラムとしてリリースされた Visual Studio 2012 および 2013 用の VSIX です。</span><span class="sxs-lookup"><span data-stu-id="2ba75-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="2ba75-106">このリリースで更新プログラム</span><span class="sxs-lookup"><span data-stu-id="2ba75-106">Updates in this release</span></span>

* <span data-ttu-id="2ba75-107">場合、パッケージの処理をスキップしていますので、含まれている`.nuspec`ドキュメント形式が正しくありません - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="2ba75-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="2ba75-108">Unix または Linux のシナリオ - \r\n の multipartwebrequest 処理を修正[776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="2ba75-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="2ba75-109">Visual Studio 2013 Community edition - のビルド イベントとの統合を修正[1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="2ba75-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="2ba75-110">GitHub でのこのリリースで修正プログラムの完全な一覧が見つかりません、 [2.8.8 マイルス トーン](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="2ba75-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
