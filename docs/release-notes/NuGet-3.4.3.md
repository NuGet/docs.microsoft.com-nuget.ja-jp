---
title: NuGet 3.4.3 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.4.3 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776466"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="237a8-103">NuGet 3.4.3 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="237a8-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="237a8-104">[NuGet 3.4.2 のリリースノート](../release-notes/nuget-3.4.2.md)  | [NuGet 3.4.4 のリリースノート](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="237a8-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="237a8-105">2016年4月22日にリリースされた NuGet 3.4.3 は、3.4 以降のリリースで特定されたいくつかの問題に対処しています。</span><span class="sxs-lookup"><span data-stu-id="237a8-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="237a8-106">VSIX と nuget.exe の両方を [ここで](https://dist.nuget.org/index.html)ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="237a8-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="237a8-107">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="237a8-107">Updates and Improvements</span></span>

* <span data-ttu-id="237a8-108">Visual Studio の信頼性が向上しました。</span><span class="sxs-lookup"><span data-stu-id="237a8-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="237a8-109">Visual Studio のクラッシュの原因となった NuGet のいくつかの問題を修正しました。</span><span class="sxs-lookup"><span data-stu-id="237a8-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="237a8-110">修正</span><span class="sxs-lookup"><span data-stu-id="237a8-110">Fixes</span></span>

* <span data-ttu-id="237a8-111">パスワードで保護されたプライベート nuget フィードに関する一部の承認の問題を修正した。</span><span class="sxs-lookup"><span data-stu-id="237a8-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="237a8-112">指定されたランタイムで PCL のを復元できない問題を修正 `project.json` しました。</span><span class="sxs-lookup"><span data-stu-id="237a8-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="237a8-113">一部のお客様は、パッケージのインストール時に断続的にエラーが発生していました。</span><span class="sxs-lookup"><span data-stu-id="237a8-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="237a8-114">これは、今回のリリースで修正されました。</span><span class="sxs-lookup"><span data-stu-id="237a8-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="237a8-115">での C++/CLI プロジェクトの復元エラーの原因となった問題を修正しました `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="237a8-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="237a8-116">Mono で nuget を使用すると、正しく解凍されていないパッケージ (ModernHttpClient など) があります。</span><span class="sxs-lookup"><span data-stu-id="237a8-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="237a8-117">これは、今回のリリースで修正されました。</span><span class="sxs-lookup"><span data-stu-id="237a8-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="237a8-118">このリリースの修正プログラムと機能強化の完全な一覧については、 [ここ](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)で問題の一覧を確認してください。</span><span class="sxs-lookup"><span data-stu-id="237a8-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>