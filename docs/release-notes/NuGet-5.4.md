---
title: NuGet 5.4 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.4 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384112"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="77779-103">NuGet 5.4 リリースノート</span><span class="sxs-lookup"><span data-stu-id="77779-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="77779-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="77779-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="77779-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="77779-105">NuGet version</span></span> | <span data-ttu-id="77779-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="77779-106">Available in Visual Studio version</span></span>| <span data-ttu-id="77779-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="77779-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="77779-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="77779-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="77779-109">Visual Studio 2019 バージョン16.4</span><span class="sxs-lookup"><span data-stu-id="77779-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="77779-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="77779-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="77779-111"><sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="77779-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="77779-112">概要: 5.4 の新機能</span><span class="sxs-lookup"><span data-stu-id="77779-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="77779-113">ソリューションの読み込み時間の短縮-最初のソリューションの読み込み中に NuGet コードを実行するオーバーヘッドが、JIT コストを削減するために部分的な ngen を使用して削減されました- [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="77779-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="77779-114">新しいヘルパー関数-パッケージ id とバージョンの一覧が表示されたら、最上位レベルのパッケージを取得します。</span><span class="sxs-lookup"><span data-stu-id="77779-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="77779-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="77779-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="77779-116">[GitHub アクション](https://github.com/features/actions)で nuget.exe をインストールおよび構成するための新しい[`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions)アクション。</span><span class="sxs-lookup"><span data-stu-id="77779-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="77779-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="77779-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="77779-118">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="77779-118">Issues fixed in this release</span></span>

<span data-ttu-id="77779-119">**バグ**</span><span class="sxs-lookup"><span data-stu-id="77779-119">**Bugs**</span></span>

* <span data-ttu-id="77779-120">プラグイン: linux/Mac [#8747](https://github.com/NuGet/Home/issues/8747)での時間の精度のログ記録がオフになっています</span><span class="sxs-lookup"><span data-stu-id="77779-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="77779-121">プラグインを破棄すると、操作全体がスローされ、失敗する場合があります。</span><span class="sxs-lookup"><span data-stu-id="77779-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="77779-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="77779-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="77779-123">PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)で、許可されているバージョンとブロックされているバージョンの一覧でのバージョンの重複の表示を停止します</span><span class="sxs-lookup"><span data-stu-id="77779-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="77779-124">ロックファイルが正しく生成されませんでした。フレームワークの順序付けは、 [#8645](https://github.com/NuGet/Home/issues/8645) lockedmode による復元に影響しないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="77779-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="77779-125">SDK 3.0.100 で <RuntimeIdentifiers> が設定されるプロジェクトの LockFile 検証が失敗する- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="77779-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="77779-126">署名の検証では、同じ OID の下に2つの値を持つタイムスタンプの署名が適切に拒否されるようになりました- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="77779-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="77779-127">ライセンスリストを更新する- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="77779-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="77779-128">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="77779-128">**DCRs**</span></span>

* <span data-ttu-id="77779-129">診断ファイルを IFeedbackDiagnosticFileProvider にオンボードする[#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="77779-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="77779-130">**[このリリースで修正されるすべての問題の一覧-5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="77779-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
