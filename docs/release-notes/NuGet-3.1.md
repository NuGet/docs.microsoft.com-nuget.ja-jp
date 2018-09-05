---
title: NuGet 3.1 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.1 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545348"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="91cc2-103">NuGet 3.1 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="91cc2-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="91cc2-104">[NuGet 3.0 リリース ノート](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 リリース ノート](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="91cc2-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="91cc2-105">NuGet 3.1 は、Visual Studio 2015 用ユニバーサル Windows プラットフォーム SDK にバンドルされている拡張機能として、2015 年 7 月 27 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="91cc2-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="91cc2-106">このリリースには、Windows プラットフォーム SDK を配信される、その Windows 開発のエクスペリエンスは以前に起動されている NuGet のクロスプラット フォームで作業の利用可能性があります。</span><span class="sxs-lookup"><span data-stu-id="91cc2-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="91cc2-107">この NuGet 拡張機能のバージョンは、Visual Studio 2015 のできるだけです。</span><span class="sxs-lookup"><span data-stu-id="91cc2-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="91cc2-108">バグ修正と新機能と更新プログラムを常に公開するように使用可能な最新バージョンの Visual Studio ギャラリー更新プログラムにアクセスできる開発者をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="91cc2-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="91cc2-109">NuGet Visual Studio の拡張機能</span><span class="sxs-lookup"><span data-stu-id="91cc2-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="91cc2-110">問題と、このリリースの機能を使用して GitHub にタグが付けられた、 [「3.1 の RTM UWP 推移的なサポート」マイルス トーン](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)3.1 のリリースでは 67 の問題の合計を終了します。</span><span class="sxs-lookup"><span data-stu-id="91cc2-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="91cc2-111">新機能</span><span class="sxs-lookup"><span data-stu-id="91cc2-111">New Features</span></span>

* <span data-ttu-id="91cc2-112">`project.json` Windows UWP および ASP.NET 5 のサポートのサポート</span><span class="sxs-lookup"><span data-stu-id="91cc2-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="91cc2-113">推移的なパッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="91cc2-113">Transitive package installation</span></span>

<span data-ttu-id="91cc2-114">これらの機能の説明と定義は、ドキュメントの他の場所で見つかんだことができます。</span><span class="sxs-lookup"><span data-stu-id="91cc2-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="91cc2-115">非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="91cc2-115">Deprecated</span></span>

<span data-ttu-id="91cc2-116">Visual Studio 2015 の次の機能は無効になります。</span><span class="sxs-lookup"><span data-stu-id="91cc2-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="91cc2-117">ソリューション レベル パッケージをインストールすることができません。</span><span class="sxs-lookup"><span data-stu-id="91cc2-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="91cc2-118">次の機能は Visual Studio 2015 を使用するプロジェクトを利用できなく、`project.json`仕様</span><span class="sxs-lookup"><span data-stu-id="91cc2-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="91cc2-119">`install.ps1` `uninstall.ps1` -これらのスクリプトは、パッケージのインストール時に無視する、復元、更新、およびアンインストール</span><span class="sxs-lookup"><span data-stu-id="91cc2-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="91cc2-120">構成の変換は無視されます。</span><span class="sxs-lookup"><span data-stu-id="91cc2-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="91cc2-121">コンテンツは、実行しますが、プロジェクトにコピーされません。</span><span class="sxs-lookup"><span data-stu-id="91cc2-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="91cc2-122">チームはこの機能を再実装やディスカッションをフォローするで進行状況に取り組んでいます。 [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="91cc2-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="91cc2-123">既知の問題</span><span class="sxs-lookup"><span data-stu-id="91cc2-123">Known Issues</span></span>

<span data-ttu-id="91cc2-124">このリリースで提供される既知の問題が発生しました。</span><span class="sxs-lookup"><span data-stu-id="91cc2-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="91cc2-125">Windows 10 SDK を使用した 3.1 リリースのインストールが以前にインストールされた NuGet 拡張機能の任意のバージョンをダウン グレードします。</span><span class="sxs-lookup"><span data-stu-id="91cc2-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="91cc2-126">NuGet コマンドライン</span><span class="sxs-lookup"><span data-stu-id="91cc2-126">NuGet Command-line</span></span>

<span data-ttu-id="91cc2-127">NuGet コマンドライン実行可能ファイルが更新され、使用可能にする履歴のバージョンの nuget.exe を続行するために、新しい再頒布可能場所に移動します。</span><span class="sxs-lookup"><span data-stu-id="91cc2-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="91cc2-128">Windows のベータ版の 3.1 バージョンの nuget.exe をダウンロードできます。 [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="91cc2-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="91cc2-129">Dist.nuget.org ホストでこのテンプレートを次のフォルダー構造を持つ、新しい配布可能な場所に存在します。</span><span class="sxs-lookup"><span data-stu-id="91cc2-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="91cc2-130">新機能</span><span class="sxs-lookup"><span data-stu-id="91cc2-130">New Features</span></span>

* <span data-ttu-id="91cc2-131">nuget.exe を復元し、使用するプロジェクトにパッケージをインストール、`project.json`ファイル。</span><span class="sxs-lookup"><span data-stu-id="91cc2-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="91cc2-132">nuget.exe に接続しで NuGet v3 プロトコルを使用できます。 [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="91cc2-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="91cc2-133">既知の問題</span><span class="sxs-lookup"><span data-stu-id="91cc2-133">Known Issues</span></span> ##

1.    <span data-ttu-id="91cc2-134">に対してパックを実行することはできません、`project.json`ファイル - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="91cc2-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="91cc2-135">Mono のではサポートされていません[1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="91cc2-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="91cc2-136">ローカライズされていない - [1058](https://github.com/NuGet/Home/issues/1058)、 [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="91cc2-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="91cc2-137">既存のと同じように、署名されていない http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="91cc2-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
