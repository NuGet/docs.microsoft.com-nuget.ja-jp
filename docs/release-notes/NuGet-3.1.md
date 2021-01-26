---
title: NuGet 3.1 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776540"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="092f4-103">NuGet 3.1 リリースノート</span><span class="sxs-lookup"><span data-stu-id="092f4-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="092f4-104">[NuGet 3.0 リリースノート](../release-notes/nuget-3.0.0.md)  | [NuGet 3.1.1 リリースノート](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="092f4-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="092f4-105">NuGet 3.1 は、ユニバーサル Windows プラットフォーム SDK for Visual Studio 2015 のバンドル拡張として2015年7月27日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="092f4-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="092f4-106">Windows 開発者が以前に開始された NuGet クロスプラットフォームの作業を利用できるように、Windows プラットフォーム SDK を使用してこのリリースを提供しています。</span><span class="sxs-lookup"><span data-stu-id="092f4-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="092f4-107">この NuGet 拡張機能のバージョンは、Visual Studio 2015 でのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="092f4-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="092f4-108">Visual Studio ギャラリーへのアクセス権を持つ開発者は、常にバグ修正と新機能を使用して更新プログラムを公開するため、利用可能な最新バージョンに更新することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="092f4-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="092f4-109">NuGet Visual Studio 拡張機能</span><span class="sxs-lookup"><span data-stu-id="092f4-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="092f4-110">このリリースの問題と機能については、GitHub で ["3.1 RTM UWP 推移サポート"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  というマイルストーンの合計について説明しています。3.1 リリースでは67の問題が解決されました。</span><span class="sxs-lookup"><span data-stu-id="092f4-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="092f4-111">新機能</span><span class="sxs-lookup"><span data-stu-id="092f4-111">New Features</span></span>

* <span data-ttu-id="092f4-112">`project.json` Windows UWP および ASP.NET 5 サポートのサポート</span><span class="sxs-lookup"><span data-stu-id="092f4-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="092f4-113">推移的パッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="092f4-113">Transitive package installation</span></span>

<span data-ttu-id="092f4-114">これらの機能の説明と定義は、ドキュメント内の他の場所にあります。</span><span class="sxs-lookup"><span data-stu-id="092f4-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="092f4-115">非推奨</span><span class="sxs-lookup"><span data-stu-id="092f4-115">Deprecated</span></span>

<span data-ttu-id="092f4-116">Visual Studio 2015 では、次の機能は使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="092f4-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="092f4-117">ソリューションレベルのパッケージはインストールできなくなりました</span><span class="sxs-lookup"><span data-stu-id="092f4-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="092f4-118">次の機能は、Visual Studio 2015 および仕様を使用するプロジェクトでは使用できなくなりました。 `project.json`</span><span class="sxs-lookup"><span data-stu-id="092f4-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="092f4-119">`install.ps1``uninstall.ps1`これらのスクリプトは、パッケージのインストール、復元、更新、およびアンインストール中は無視されます</span><span class="sxs-lookup"><span data-stu-id="092f4-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="092f4-120">構成の変換は無視されます</span><span class="sxs-lookup"><span data-stu-id="092f4-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="092f4-121">コンテンツは実行されますが、プロジェクトにコピーされることはありません。</span><span class="sxs-lookup"><span data-stu-id="092f4-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="092f4-122">チームはこの機能の再実装に取り組んでおり、以下の説明と進行状況に従ってください。 [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="092f4-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="092f4-123">既知の問題</span><span class="sxs-lookup"><span data-stu-id="092f4-123">Known Issues</span></span>

<span data-ttu-id="092f4-124">このリリースでは、いくつかの既知の問題が配信されました。</span><span class="sxs-lookup"><span data-stu-id="092f4-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="092f4-125">Windows 10 SDK を使用して3.1 リリースをインストールすると、以前にインストールされたすべてのバージョンの NuGet 拡張機能がダウングレードされます</span><span class="sxs-lookup"><span data-stu-id="092f4-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="092f4-126">NuGet コマンドライン</span><span class="sxs-lookup"><span data-stu-id="092f4-126">NuGet Command-line</span></span>

<span data-ttu-id="092f4-127">NuGet コマンドラインの実行可能ファイルが更新され、新しい再配布可能な場所に移動されたため、nuget.exe の履歴バージョンを引き続き使用できます。</span><span class="sxs-lookup"><span data-stu-id="092f4-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="092f4-128">Windows 用 nuget.exe の3.1 ベータ版は、次の場所からダウンロードできます。 [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="092f4-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="092f4-129">新しい再配布可能な場所は dist.nuget.org ホスト上にあり、このテンプレートの後にフォルダー構造があります。</span><span class="sxs-lookup"><span data-stu-id="092f4-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="092f4-130">新機能</span><span class="sxs-lookup"><span data-stu-id="092f4-130">New Features</span></span>

* <span data-ttu-id="092f4-131">nuget.exe では、ファイルを使用するプロジェクトにパッケージを復元してインストールでき `project.json` ます。</span><span class="sxs-lookup"><span data-stu-id="092f4-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="092f4-132">nuget.exe は、次の場所で NuGet v3 プロトコルに接続して使用できます。 [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="092f4-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="092f4-133">既知の問題</span><span class="sxs-lookup"><span data-stu-id="092f4-133">Known Issues</span></span> ##

1.    <span data-ttu-id="092f4-134">ファイルに対してパックを実行できません `project.json` - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="092f4-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="092f4-135">Mono- [1059](https://github.com/NuGet/Home/issues/1059)ではサポートされていません</span><span class="sxs-lookup"><span data-stu-id="092f4-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="092f4-136">ローカライズされていない- [1058](https://github.com/NuGet/Home/issues/1058)、   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="092f4-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="092f4-137">既存の1073と同じように、署名されていません http://nuget.org/nuget.exe  -  [](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="092f4-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
