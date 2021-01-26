---
title: WebMatrix の NuGet 2.6.1 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む、NuGet 2.6.1 向けのリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780418"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="d957a-103">WebMatrix の NuGet 2.6.1 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="d957a-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="d957a-104">[NuGet 2.6 リリースノート](../release-notes/nuget-2.6.md)  | [NuGet 2.7 リリースノート](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="d957a-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="d957a-105">NuGet チームは、2014年3月26日に WebMatrix 用に更新された NuGet パッケージマネージャー拡張機能をリリースしました。</span><span class="sxs-lookup"><span data-stu-id="d957a-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="d957a-106">この更新プログラムは、次の手順を使用して [WebMatrix 拡張機能ギャラリー](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) からインストールできます。</span><span class="sxs-lookup"><span data-stu-id="d957a-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="d957a-107">WebMatrix 3 を開く</span><span class="sxs-lookup"><span data-stu-id="d957a-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="d957a-108">[ホーム] リボンの [拡張機能] アイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="d957a-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="d957a-109">[更新] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="d957a-109">Select the Updates tab</span></span>
1. <span data-ttu-id="d957a-110">クリックして NuGet パッケージマネージャーを2.6.1 に更新します</span><span class="sxs-lookup"><span data-stu-id="d957a-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="d957a-111">WebMatrix 3 を閉じて再起動する</span><span class="sxs-lookup"><span data-stu-id="d957a-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="d957a-112">注目すべき変更点</span><span class="sxs-lookup"><span data-stu-id="d957a-112">Notable Changes</span></span>

<span data-ttu-id="d957a-113">この拡張機能の更新では、ユーザーが WebMatrix で NuGet パッケージを使用することに直面した最大の問題の2つに対処します。</span><span class="sxs-lookup"><span data-stu-id="d957a-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="d957a-114">1つ目は NuGet スキーマバージョンエラーで、2番目はフォルダー内のゼロバイト Dll に先行するバグでした `bin` 。</span><span class="sxs-lookup"><span data-stu-id="d957a-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="d957a-115">NuGet スキーマバージョンエラー</span><span class="sxs-lookup"><span data-stu-id="d957a-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="d957a-116">WebMatrix 3 がリリースされたため、nuget パッケージの新しいスキーマバージョンを必要とする新しい機能が NuGet に導入されました。</span><span class="sxs-lookup"><span data-stu-id="d957a-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="d957a-117">Web サイトで NuGet パッケージを管理しようとすると、これらの新しいパッケージによって、WebMatrix に表示されるエラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d957a-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![エラーが発生しました。](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="d957a-121">この最新リリースでは、最新の NuGet パッケージとの互換性が確保されているため、このエラーの発生を回避できます。</span><span class="sxs-lookup"><span data-stu-id="d957a-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="d957a-122">WebMatrix を含む新しいバージョンのパッケージを WebMatrix にインストールできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="d957a-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="d957a-123">これらのパッケージの一部では、現在 WebMatrix ではサポートされていない [Xdt 構成変換](../release-notes/nuget-2.6.md#xdt)などの NuGet 機能を使用していました。</span><span class="sxs-lookup"><span data-stu-id="d957a-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="d957a-124">Bin フォルダー内の Dll の Zero-Byte</span><span class="sxs-lookup"><span data-stu-id="d957a-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="d957a-125">Bin にコピーされる Dll を含む、WebMatrix で NuGet パッケージをインストールした後、Dll が `bin` 0 バイトファイルとしてフォルダーに表示されることが、一部のユーザーに報告されています。</span><span class="sxs-lookup"><span data-stu-id="d957a-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="d957a-126">これにより、実行時にアプリケーションが中断されます。</span><span class="sxs-lookup"><span data-stu-id="d957a-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="d957a-127">[この問題](https://nuget.codeplex.com/workitem/4060) は修正されました。</span><span class="sxs-lookup"><span data-stu-id="d957a-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="d957a-128">その他の最新の機能強化</span><span class="sxs-lookup"><span data-stu-id="d957a-128">Other Recent Improvements</span></span>

<span data-ttu-id="d957a-129">Visual Studio の NuGet パッケージマネージャー2.8 がリリースされたときに、WebMatrix の NuGet パッケージマネージャー2.5.0 もリリースしました。</span><span class="sxs-lookup"><span data-stu-id="d957a-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="d957a-130">これは [NuGet 2.8 リリースノート](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)に記載されていますが、更新された特定の新機能については触れませんでした。</span><span class="sxs-lookup"><span data-stu-id="d957a-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="d957a-131">すべて更新</span><span class="sxs-lookup"><span data-stu-id="d957a-131">Update All</span></span>

<span data-ttu-id="d957a-132">これで、すべての web サイトのパッケージを1回の手順で更新できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="d957a-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="d957a-133">WebMatrix で NuGet 拡張機能を開くと、ギャラリーのすべてのパッケージ、インストールされているパッケージ、および更新プログラムが利用可能なすべてのパッケージの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d957a-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="d957a-134">以前は、すべてのパッケージを個別に更新する必要がありましたが、[更新] タブに表示される [すべて更新] ボタンがあります。</span><span class="sxs-lookup"><span data-stu-id="d957a-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![[すべて更新] をクリックして、利用可能な更新プログラムを含むすべてのパッケージを更新します](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="d957a-136">既存のファイルを上書きする</span><span class="sxs-lookup"><span data-stu-id="d957a-136">Overwrite Existing Files</span></span>

<span data-ttu-id="d957a-137">Web サイトに既に存在するファイルを含むパッケージをインストールする場合、NuGet は常にそのファイルを自動的に無視しただけです (既存のファイルはそのままです)。</span><span class="sxs-lookup"><span data-stu-id="d957a-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="d957a-138">これにより、パッケージが正しくインストールまたは更新されたという印象が生じる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d957a-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="d957a-139">ファイルの上書きを確認するメッセージが表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="d957a-139">NuGet will now prompt for files to be overwritten.</span></span>

![ファイルの競合の解決](./media/NuGet-2.8/webmatrix-overwrite-file.png)
