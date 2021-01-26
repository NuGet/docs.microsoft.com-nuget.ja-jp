---
title: NuGet 3.4-RC リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.4 RC のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780233"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="1f197-103">NuGet 3.4-RC リリースノート</span><span class="sxs-lookup"><span data-stu-id="1f197-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="1f197-104">[NuGet 3.3 リリースノート](../release-notes/nuget-3.3.md)  | [NuGet 3.4 リリースノート](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="1f197-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="1f197-105">NuGet 3.4-RC は、Visual Studio 2015 Update 2 RC と共に2016年3月3日にリリースされ、いくつかの原則に基づいて構築されました。</span><span class="sxs-lookup"><span data-stu-id="1f197-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="1f197-106">クロスプラットフォームサポート</span><span class="sxs-lookup"><span data-stu-id="1f197-106">Cross-Platform support</span></span>
* <span data-ttu-id="1f197-107">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="1f197-107">Performance improvements</span></span>
* <span data-ttu-id="1f197-108">UI のマイナー機能強化</span><span class="sxs-lookup"><span data-stu-id="1f197-108">Minor UI improvements</span></span>

<span data-ttu-id="1f197-109">この RC では、次の機能が提供されています。これは、3.4 最終リリースに対してより多くの計画があります。</span><span class="sxs-lookup"><span data-stu-id="1f197-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="1f197-110">新機能</span><span class="sxs-lookup"><span data-stu-id="1f197-110">New Features</span></span>

* <span data-ttu-id="1f197-111">NuGet クライアントでリポジトリからの gzip コンテンツエンコードがサポートされるようになりました</span><span class="sxs-lookup"><span data-stu-id="1f197-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="1f197-112">Xproj プロジェクトのパッケージからの Pdb のサポート</span><span class="sxs-lookup"><span data-stu-id="1f197-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="1f197-113">ContentFiles 要素での iOS および Android ビルドアクションのサポート</span><span class="sxs-lookup"><span data-stu-id="1f197-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="1f197-114">Netstandard.library と netstandardapp フレームワークのモニカーのサポート</span><span class="sxs-lookup"><span data-stu-id="1f197-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="1f197-115">新しいユーザーインターフェイスの機能</span><span class="sxs-lookup"><span data-stu-id="1f197-115">New User Interface Features</span></span>

* <span data-ttu-id="1f197-116">インストール、更新、統合の各タブで大幅なパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="1f197-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="1f197-117">インストールおよび更新のタブがアルファベット順に並べ替えられるようになりました。</span><span class="sxs-lookup"><span data-stu-id="1f197-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="1f197-118">検索を更新するための更新ボタンを追加しました</span><span class="sxs-lookup"><span data-stu-id="1f197-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="1f197-119">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="1f197-119">Updates and Improvements</span></span>

* <span data-ttu-id="1f197-120">`project.json`浮動バージョンを持つで参照されるパッケージは、すべてのビルドで更新されません。</span><span class="sxs-lookup"><span data-stu-id="1f197-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="1f197-121">代わりに、復元、クリーン、リビルド、または変更を強制した場合にのみ更新され `project.json` ます。</span><span class="sxs-lookup"><span data-stu-id="1f197-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="1f197-122">NuGet 構成 UI を使用する場合、nuget.org リポジトリソースはプロジェクト構成に強制されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="1f197-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="1f197-123">NuGet では、共有プロジェクトのパッケージが復元されず、ロックファイルも書き込まれなくなりました。</span><span class="sxs-lookup"><span data-stu-id="1f197-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="1f197-124">ネットワークエラーを改善し、到達不能または応答の遅いサーバーの処理を再試行しました。</span><span class="sxs-lookup"><span data-stu-id="1f197-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="1f197-125">Visual Studio パッケージマネージャーの UI では、キーボードとマウスの動作が改善されています。</span><span class="sxs-lookup"><span data-stu-id="1f197-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="1f197-126">DNX の最新のスキーマがサポートされるようになりました `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="1f197-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="1f197-127">既知の問題</span><span class="sxs-lookup"><span data-stu-id="1f197-127">Known Issues</span></span>

<span data-ttu-id="1f197-128">GitHub の問題の一覧に関する問題は、引き続き次の場所にあります。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="1f197-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>