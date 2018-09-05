---
title: NuGet 2.6.1 for WebMatrix のリリース ノート
description: NuGet 2.6.1 の既知の問題、バグの修正、追加機能、および Dcr を含む WebMatrix のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550318"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="e5f70-103">NuGet 2.6.1 for WebMatrix のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="e5f70-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="e5f70-104">[NuGet 2.6 リリース ノート](../release-notes/nuget-2.6.md) | [NuGet 2.7 リリース ノート](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="e5f70-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="e5f70-105">NuGet チームでは、2014 年 3 月 26日に WebMatrix の最新の NuGet パッケージ マネージャー拡張機能をリリースします。</span><span class="sxs-lookup"><span data-stu-id="e5f70-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="e5f70-106">この更新プログラムをインストールすることができます、 [WebMatrix 拡張機能ギャラリー](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery)次の手順を使用します。</span><span class="sxs-lookup"><span data-stu-id="e5f70-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="e5f70-107">WebMatrix 3 を開く</span><span class="sxs-lookup"><span data-stu-id="e5f70-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="e5f70-108">[ホーム] リボンの拡張機能アイコンをクリックします</span><span class="sxs-lookup"><span data-stu-id="e5f70-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="e5f70-109">[更新] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="e5f70-109">Select the Updates tab</span></span>
1. <span data-ttu-id="e5f70-110">2.6.1 に NuGet パッケージ マネージャーを更新する をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e5f70-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="e5f70-111">閉じて再起動 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="e5f70-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="e5f70-112">主な変更点</span><span class="sxs-lookup"><span data-stu-id="e5f70-112">Notable Changes</span></span>

<span data-ttu-id="e5f70-113">この拡張機能の更新プログラムにより 2 つの問題を最も多く使用には、WebMatrix 内で NuGet パッケージの使用が直面しています。</span><span class="sxs-lookup"><span data-stu-id="e5f70-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="e5f70-114">最初は、NuGet のスキーマ バージョンのエラーと、もう 1 つは、先頭のゼロ バイトの Dll にバグは、`bin`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="e5f70-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="e5f70-115">NuGet のスキーマ バージョン エラー</span><span class="sxs-lookup"><span data-stu-id="e5f70-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="e5f70-116">WebMatrix 3 がリリースされてから新機能は NuGet パッケージを新しいスキーマ バージョンを必要とする NuGet に導入されています。</span><span class="sxs-lookup"><span data-stu-id="e5f70-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="e5f70-117">Web サイトの NuGet パッケージを管理するときに、これらの新しいパッケージは WebMatrix に表示されるエラーにつながります。</span><span class="sxs-lookup"><span data-stu-id="e5f70-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![エラーが発生しました。](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="e5f70-121">この最新リリースでは、最新の NuGet パッケージは、このエラーが発生していることを防止との互換性を提供します。</span><span class="sxs-lookup"><span data-stu-id="e5f70-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="e5f70-122">Microsoft.AspNet.WebPages を含むパッケージの新しいバージョンは、WebMatrix で今すぐインストールできます。</span><span class="sxs-lookup"><span data-stu-id="e5f70-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="e5f70-123">などに、NuGet の機能を使用してこれらのパッケージの一部が[XDT 構成変換の](../release-notes/nuget-2.6.md#xdt)、これまで WebMatrix でサポートされていませんでした。</span><span class="sxs-lookup"><span data-stu-id="e5f70-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="e5f70-124">Bin フォルダーで 0 バイトの Dll</span><span class="sxs-lookup"><span data-stu-id="e5f70-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="e5f70-125">一部のユーザーが報告する NuGet のインストールをパッケージ化を含む Dll を bin にコピーを WebMatrix で Dll の表示にした後、 `bin` 0 バイトのファイルとフォルダー。</span><span class="sxs-lookup"><span data-stu-id="e5f70-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="e5f70-126">これにより、アプリケーションは、実行時に中断します。</span><span class="sxs-lookup"><span data-stu-id="e5f70-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="e5f70-127">[この問題](https://nuget.codeplex.com/workitem/4060)が修正されました。</span><span class="sxs-lookup"><span data-stu-id="e5f70-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="e5f70-128">その他の最新の機能強化</span><span class="sxs-lookup"><span data-stu-id="e5f70-128">Other Recent Improvements</span></span>

<span data-ttu-id="e5f70-129">Visual Studio の NuGet パッケージ マネージャー 2.8 のリリース時もリリースされました。 NuGet パッケージ マネージャー 2.5.0 WebMatrix の。</span><span class="sxs-lookup"><span data-stu-id="e5f70-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="e5f70-130">説明したこの中に、 [NuGet 2.8 リリース ノート](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)特定の更新プログラムが導入された新機能をお伝えします。</span><span class="sxs-lookup"><span data-stu-id="e5f70-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="e5f70-131">すべてを更新します。</span><span class="sxs-lookup"><span data-stu-id="e5f70-131">Update All</span></span>

<span data-ttu-id="e5f70-132">すべての 1 つの手順で web サイトのパッケージを更新できます。</span><span class="sxs-lookup"><span data-stu-id="e5f70-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="e5f70-133">NuGet 拡張機能を開くには、WebMatrix で、ギャラリー、インストールされている、および、使用可能な更新プログラムのあるものすべてのパッケージの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="e5f70-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="e5f70-134">以前は、すべてのパッケージが個別に更新する必要がありますが、[更新] タブに表示される便利な [すべて更新] ボタンがあるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e5f70-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![利用可能な更新ですべてのパッケージを更新するには、[すべて更新] をクリックします。](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="e5f70-136">既存のファイルを上書きします。</span><span class="sxs-lookup"><span data-stu-id="e5f70-136">Overwrite Existing Files</span></span>

<span data-ttu-id="e5f70-137">Web サイトに既に存在するファイルが含まれているパッケージをインストールするときに、NuGet には常にサイレント モードでそれらのファイル (単独で、既存のファイルを離れること) が無視されました。</span><span class="sxs-lookup"><span data-stu-id="e5f70-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="e5f70-138">これは、パッケージがインストールされているか、ときに実際にはありませんでしたが正しく更新という印象につながりますでした。</span><span class="sxs-lookup"><span data-stu-id="e5f70-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="e5f70-139">ファイルを上書きするには、NuGet は求められますようになりました。</span><span class="sxs-lookup"><span data-stu-id="e5f70-139">NuGet will now prompt for files to be overwritten.</span></span>

![ファイルの競合の解決](./media/NuGet-2.8/webmatrix-overwrite-file.png)
