---
title: NuGet 3.4.3 リリース ノート
description: NuGet 3.4.3 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549166"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="b35cc-103">NuGet 3.4.3 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="b35cc-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="b35cc-104">[NuGet 3.4.2 リリース ノート](../release-notes/nuget-3.4.2.md) | [3.4.4 を NuGet のリリース ノート](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="b35cc-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="b35cc-105">NuGet 3.4.3 は 3.4 以降のリリースで識別されたいくつかの問題に対処する、2016 年 4 月 22 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="b35cc-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="b35cc-106">VSIX と nuget.exe の両方をダウンロードする[ここ](https://dist.nuget.org/index.html)します。</span><span class="sxs-lookup"><span data-stu-id="b35cc-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="b35cc-107">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="b35cc-107">Updates and Improvements</span></span>

* <span data-ttu-id="b35cc-108">Visual Studio の信頼性の向上。</span><span class="sxs-lookup"><span data-stu-id="b35cc-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="b35cc-109">Visual Studio でのクラッシュの原因となった NuGet でいくつかの問題を修正しました。</span><span class="sxs-lookup"><span data-stu-id="b35cc-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="b35cc-110">修正プログラム</span><span class="sxs-lookup"><span data-stu-id="b35cc-110">Fixes</span></span>

* <span data-ttu-id="b35cc-111">パスワードで保護されたプライベート nuget フィードのいくつかの承認の問題を修正しました。</span><span class="sxs-lookup"><span data-stu-id="b35cc-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="b35cc-112">周囲の PCL を復元できない問題を修正しました`project.json`指定されたランタイムを使用します。</span><span class="sxs-lookup"><span data-stu-id="b35cc-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="b35cc-113">一部のお客様は、パッケージをインストールするときに断続的エラーに実行されていた。</span><span class="sxs-lookup"><span data-stu-id="b35cc-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="b35cc-114">これは、このリリースで修正されましたがようになりました。</span><span class="sxs-lookup"><span data-stu-id="b35cc-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="b35cc-115">C + での復元の障害を原因となった問題を修正しました/cli CLI を使用するとプロジェクト`project.json`します。</span><span class="sxs-lookup"><span data-stu-id="b35cc-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="b35cc-116">一部のパッケージ (例: ModernHttpClient) 場所にない解凍正しく mono で nuget を使用する場合。</span><span class="sxs-lookup"><span data-stu-id="b35cc-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="b35cc-117">これは、このリリースで修正されましたがようになりました。</span><span class="sxs-lookup"><span data-stu-id="b35cc-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="b35cc-118">修正し、このリリースの機能強化の完全な一覧で、問題の一覧をご覧ください[ここ](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)します。</span><span class="sxs-lookup"><span data-stu-id="b35cc-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>