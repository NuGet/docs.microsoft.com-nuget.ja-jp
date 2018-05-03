---
title: NuGet 3.4.3 リリース ノート
description: NuGet 3.4.3 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="6b817-103">NuGet 3.4.3 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="6b817-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="6b817-104">[NuGet 3.4.2 リリース ノート](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 リリース ノート](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="6b817-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="6b817-105">NuGet 3.4.3 は、2016 年 4 月 22 日 3.4 以降のリリースで識別されたいくつかの問題を解決するにリリースされました。</span><span class="sxs-lookup"><span data-stu-id="6b817-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="6b817-106">VSIX と nuget.exe の両方をダウンロードする[ここ](https://dist.nuget.org/index.html)です。</span><span class="sxs-lookup"><span data-stu-id="6b817-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="6b817-107">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="6b817-107">Updates and Improvements</span></span>

* <span data-ttu-id="6b817-108">Visual Studio、信頼性が向上します。</span><span class="sxs-lookup"><span data-stu-id="6b817-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="6b817-109">Visual Studio でのクラッシュの原因となった NuGet でいくつかの問題が解決されました。</span><span class="sxs-lookup"><span data-stu-id="6b817-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="6b817-110">修正プログラム</span><span class="sxs-lookup"><span data-stu-id="6b817-110">Fixes</span></span>

* <span data-ttu-id="6b817-111">固定いくつかの認証の問題はパスワードで保護されたプライベート nuget フィードです。</span><span class="sxs-lookup"><span data-stu-id="6b817-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="6b817-112">問題を修正、周囲から PCL を復元することができません`project.json`指定されたランタイムを使用します。</span><span class="sxs-lookup"><span data-stu-id="6b817-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="6b817-113">一部のお客様は、パッケージをインストールするときに断続的なエラーに実行されていた。</span><span class="sxs-lookup"><span data-stu-id="6b817-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="6b817-114">これは、このリリースで修正されましたがようになりました。</span><span class="sxs-lookup"><span data-stu-id="6b817-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="6b817-115">C + の復元の障害の原因となった問題を修正しました + CLI プロジェクトに関するプロジェクト`project.json`です。</span><span class="sxs-lookup"><span data-stu-id="6b817-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="6b817-116">一部のパッケージ (例: ModernHttpClient) 場所にない解凍正しくモノラルで nuget を使用する場合。</span><span class="sxs-lookup"><span data-stu-id="6b817-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="6b817-117">これは、このリリースで修正されましたがようになりました。</span><span class="sxs-lookup"><span data-stu-id="6b817-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="6b817-118">、修正し、このリリースの機能強化の完全な一覧を確認して問題の一覧[ここ](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)です。</span><span class="sxs-lookup"><span data-stu-id="6b817-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>