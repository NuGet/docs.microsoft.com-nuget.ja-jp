---
title: "NuGet 3.4 RC のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.4 RC の既知の問題、バグの修正、追加された機能は、Dcr などのリリース ノートします。"
keywords: "NuGet 3.4 RC のリリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="dd1b7-104">NuGet 3.4 RC のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="dd1b7-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="dd1b7-105">[NuGet 3.3 リリース ノート](../release-notes/nuget-3.3.md) | [NuGet 3.4 リリース ノート](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="dd1b7-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="dd1b7-106">NuGet 3.4 RC では、Visual Studio 2015 Update 2 RC と共に、2016 年 3 月 3日がリリースされ、心にいくつかの基本思想でビルドされました。</span><span class="sxs-lookup"><span data-stu-id="dd1b7-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="dd1b7-107">クロスプラット フォーム サポート</span><span class="sxs-lookup"><span data-stu-id="dd1b7-107">Cross-Platform support</span></span>
* <span data-ttu-id="dd1b7-108">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="dd1b7-108">Performance improvements</span></span>
* <span data-ttu-id="dd1b7-109">マイナーの UI 機能強化</span><span class="sxs-lookup"><span data-stu-id="dd1b7-109">Minor UI improvements</span></span>

<span data-ttu-id="dd1b7-110">次の機能は、複数の 3.4 最終リリースの計画とこの RC で利用します。</span><span class="sxs-lookup"><span data-stu-id="dd1b7-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="dd1b7-111">新機能</span><span class="sxs-lookup"><span data-stu-id="dd1b7-111">New Features</span></span>

* <span data-ttu-id="dd1b7-112">NuGet クライアント サポート gzip コンテンツ エンコード リポジトリから</span><span class="sxs-lookup"><span data-stu-id="dd1b7-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="dd1b7-113">Xproj プロジェクトでパッケージから Pdb のサポート</span><span class="sxs-lookup"><span data-stu-id="dd1b7-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="dd1b7-114">IOS および Android のビルド アクション contentFiles 要素でのサポート</span><span class="sxs-lookup"><span data-stu-id="dd1b7-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="dd1b7-115">Netstandard および netstandardapp フレームワーク モニカーのサポート</span><span class="sxs-lookup"><span data-stu-id="dd1b7-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="dd1b7-116">新しいユーザー インターフェイスの機能</span><span class="sxs-lookup"><span data-stu-id="dd1b7-116">New User Interface Features</span></span>

* <span data-ttu-id="dd1b7-117">特に、インストール、更新、および統合のタブ上の大幅なパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="dd1b7-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="dd1b7-118">インストールされているし、更新プログラムのタブがアルファベット順に並べ替えられました</span><span class="sxs-lookup"><span data-stu-id="dd1b7-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="dd1b7-119">更新する検索を許可する更新 ボタンの追加</span><span class="sxs-lookup"><span data-stu-id="dd1b7-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="dd1b7-120">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="dd1b7-120">Updates and Improvements</span></span>

* <span data-ttu-id="dd1b7-121">パッケージで参照されている`project.json`浮動があるすべてのビルドでバージョンは更新されません。</span><span class="sxs-lookup"><span data-stu-id="dd1b7-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="dd1b7-122">強制復元、クリーン、再構築、または変更する場合にのみを更新する代わりに、`project.json`です。</span><span class="sxs-lookup"><span data-stu-id="dd1b7-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="dd1b7-123">nuget.org のリポジトリ ソースを NuGet 構成 UI を使用するときに、不要になったプロジェクト構成に求められます。</span><span class="sxs-lookup"><span data-stu-id="dd1b7-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="dd1b7-124">不要になった NuGet は、共有プロジェクトでパッケージを復元も、ロック ファイルを書き込みます。</span><span class="sxs-lookup"><span data-stu-id="dd1b7-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="dd1b7-125">ネットワーク障害を改良しましたし、到達できないか、応答に低速のサーバーの処理を再試行してください。</span><span class="sxs-lookup"><span data-stu-id="dd1b7-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="dd1b7-126">Visual Studio のパッケージ マネージャーの UI では、キーボードとマウスの動作が強化されています。</span><span class="sxs-lookup"><span data-stu-id="dd1b7-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="dd1b7-127">最新のサポート`project.json`DNX 内のスキーマです。</span><span class="sxs-lookup"><span data-stu-id="dd1b7-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="dd1b7-128">既知の問題</span><span class="sxs-lookup"><span data-stu-id="dd1b7-128">Known Issues</span></span>

<span data-ttu-id="dd1b7-129">あることができます、GitHub の問題一覧上の問題を追跡するために続行: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="dd1b7-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>