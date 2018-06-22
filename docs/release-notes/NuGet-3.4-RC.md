---
title: NuGet 3.4 RC のリリース ノート
description: NuGet 3.4 RC の既知の問題、バグの修正、追加された機能は、Dcr などのリリース ノートします。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820821"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="cee2a-103">NuGet 3.4 RC のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="cee2a-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="cee2a-104">[NuGet 3.3 リリース ノート](../release-notes/nuget-3.3.md) | [NuGet 3.4 リリース ノート](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="cee2a-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="cee2a-105">NuGet 3.4 RC では、Visual Studio 2015 Update 2 RC と共に、2016 年 3 月 3日がリリースされ、心にいくつかの基本思想でビルドされました。</span><span class="sxs-lookup"><span data-stu-id="cee2a-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="cee2a-106">クロスプラット フォーム サポート</span><span class="sxs-lookup"><span data-stu-id="cee2a-106">Cross-Platform support</span></span>
* <span data-ttu-id="cee2a-107">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="cee2a-107">Performance improvements</span></span>
* <span data-ttu-id="cee2a-108">マイナーの UI 機能強化</span><span class="sxs-lookup"><span data-stu-id="cee2a-108">Minor UI improvements</span></span>

<span data-ttu-id="cee2a-109">次の機能は、複数の 3.4 最終リリースの計画とこの RC で利用します。</span><span class="sxs-lookup"><span data-stu-id="cee2a-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="cee2a-110">新機能</span><span class="sxs-lookup"><span data-stu-id="cee2a-110">New Features</span></span>

* <span data-ttu-id="cee2a-111">NuGet クライアント サポート gzip コンテンツ エンコード リポジトリから</span><span class="sxs-lookup"><span data-stu-id="cee2a-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="cee2a-112">Xproj プロジェクトでパッケージから Pdb のサポート</span><span class="sxs-lookup"><span data-stu-id="cee2a-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="cee2a-113">IOS および Android のビルド アクション contentFiles 要素でのサポート</span><span class="sxs-lookup"><span data-stu-id="cee2a-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="cee2a-114">Netstandard および netstandardapp フレームワーク モニカーのサポート</span><span class="sxs-lookup"><span data-stu-id="cee2a-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="cee2a-115">新しいユーザー インターフェイスの機能</span><span class="sxs-lookup"><span data-stu-id="cee2a-115">New User Interface Features</span></span>

* <span data-ttu-id="cee2a-116">特に、インストール、更新、および統合のタブ上の大幅なパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="cee2a-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="cee2a-117">インストールされているし、更新プログラムのタブがアルファベット順に並べ替えられました</span><span class="sxs-lookup"><span data-stu-id="cee2a-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="cee2a-118">更新する検索を許可する更新 ボタンの追加</span><span class="sxs-lookup"><span data-stu-id="cee2a-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="cee2a-119">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="cee2a-119">Updates and Improvements</span></span>

* <span data-ttu-id="cee2a-120">パッケージで参照されている`project.json`浮動があるすべてのビルドでバージョンは更新されません。</span><span class="sxs-lookup"><span data-stu-id="cee2a-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="cee2a-121">強制復元、クリーン、再構築、または変更する場合にのみを更新する代わりに、`project.json`です。</span><span class="sxs-lookup"><span data-stu-id="cee2a-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="cee2a-122">nuget.org のリポジトリ ソースを NuGet 構成 UI を使用するときに、不要になったプロジェクト構成に求められます。</span><span class="sxs-lookup"><span data-stu-id="cee2a-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="cee2a-123">不要になった NuGet は、共有プロジェクトでパッケージを復元も、ロック ファイルを書き込みます。</span><span class="sxs-lookup"><span data-stu-id="cee2a-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="cee2a-124">ネットワーク障害を改良しましたし、到達できないか、応答に低速のサーバーの処理を再試行してください。</span><span class="sxs-lookup"><span data-stu-id="cee2a-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="cee2a-125">Visual Studio のパッケージ マネージャーの UI では、キーボードとマウスの動作が強化されています。</span><span class="sxs-lookup"><span data-stu-id="cee2a-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="cee2a-126">最新のサポート`project.json`DNX 内のスキーマです。</span><span class="sxs-lookup"><span data-stu-id="cee2a-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="cee2a-127">既知の問題</span><span class="sxs-lookup"><span data-stu-id="cee2a-127">Known Issues</span></span>

<span data-ttu-id="cee2a-128">あることができます、GitHub の問題一覧上の問題を追跡するために続行します。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="cee2a-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>