---
title: NuGet 2.9-RC リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.9 RC のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780319"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="f0d2e-103">NuGet 2.9-RC リリースノート</span><span class="sxs-lookup"><span data-stu-id="f0d2e-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="f0d2e-104">[NuGet 2.8.7 のリリースノート](../release-notes/nuget-2.8.7.md)  | [NuGet 3.0 Preview リリースノート](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="f0d2e-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="f0d2e-105">NuGet 2.9 は、Visual Studio 2012 および2013の 2.8.7 VSIX の更新プログラムとして、2015年9月10日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="f0d2e-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="f0d2e-106">このリリースの更新プログラム</span><span class="sxs-lookup"><span data-stu-id="f0d2e-106">Updates in this release</span></span>

* <span data-ttu-id="f0d2e-107">含まれているドキュメントの形式が正しくない場合にパッケージの処理をスキップするようになりました `.nuspec` - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="f0d2e-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="f0d2e-108">Unix/Linux シナリオ用に \r\n の multipartwebrequest の処理を修正しました- [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="f0d2e-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="f0d2e-109">Visual Studio 2013 Community edition でのビルドイベントとの統合の修正- [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="f0d2e-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="f0d2e-110">このリリースの修正プログラムの完全な一覧については、 [2.8.8 マイルストーン](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)の GitHub を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f0d2e-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
