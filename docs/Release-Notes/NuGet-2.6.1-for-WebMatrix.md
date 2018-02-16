---
title: "WebMatrix のリリース ノートについては、NuGet 2.6.1 |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "WebMatrix の既知の問題、バグの修正、追加された機能は、Dcr などの NuGet 2.6.1 のリリース ノートです。"
keywords: "WebMatrix のリリース ノート、バグの修正プログラム、既知の問題、NuGet 2.6.1 Dcr、機能の追加"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6150fc34dd05c2e7ce132d2d6744b823daeb1a07
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="fc97f-104">WebMatrix のリリース ノートについては、NuGet 2.6.1</span><span class="sxs-lookup"><span data-stu-id="fc97f-104">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="fc97f-105">[NuGet 2.6 リリース ノート](../release-notes/nuget-2.6.md) | [NuGet 2.7 リリース ノート](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="fc97f-105">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="fc97f-106">NuGet チームは、2014 年 3 月 26 日に WebMatrix の最新の NuGet Package Manager 拡張機能をリリースします。</span><span class="sxs-lookup"><span data-stu-id="fc97f-106">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="fc97f-107">この更新プログラムをインストールすることができます、 [WebMatrix 拡張機能ギャラリー](http://extensions.webmatrix.com/packages/NuGetPackageManager/)次の手順を使用します。</span><span class="sxs-lookup"><span data-stu-id="fc97f-107">This update can be installed from the [WebMatrix Extension Gallery](http://extensions.webmatrix.com/packages/NuGetPackageManager/) using the following steps:</span></span>

1. <span data-ttu-id="fc97f-108">WebMatrix 3 を開く</span><span class="sxs-lookup"><span data-stu-id="fc97f-108">Open WebMatrix 3</span></span>
2. <span data-ttu-id="fc97f-109">[ホーム] リボンの拡張機能のアイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="fc97f-109">Click the Extensions icon in the Home ribbon</span></span>
3. <span data-ttu-id="fc97f-110">更新プログラム タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="fc97f-110">Select the Updates tab</span></span>
4. <span data-ttu-id="fc97f-111">2.6.1 に NuGet Package Manager を更新する をクリックします。</span><span class="sxs-lookup"><span data-stu-id="fc97f-111">Click to update NuGet Package Manager to 2.6.1</span></span>
6. <span data-ttu-id="fc97f-112">終了し、WebMatrix 3 の再起動</span><span class="sxs-lookup"><span data-stu-id="fc97f-112">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="fc97f-113">主な変更点</span><span class="sxs-lookup"><span data-stu-id="fc97f-113">Notable Changes</span></span>

<span data-ttu-id="fc97f-114">この拡張機能の更新プログラムにより 2 つの問題を最も多く使用には、WebMatrix 内で NuGet パッケージの使用が直面しています。</span><span class="sxs-lookup"><span data-stu-id="fc97f-114">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="fc97f-115">NuGet スキーマ バージョン エラーが発生しました、最初と 2 つ目が先頭のゼロ バイト Dll へのバグ、`bin`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="fc97f-115">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="fc97f-116">NuGet のスキーマ バージョン エラー</span><span class="sxs-lookup"><span data-stu-id="fc97f-116">NuGet Schema Version Error</span></span>

<span data-ttu-id="fc97f-117">WebMatrix 3 がリリースされた後に、NuGet パッケージを新しいスキーマのバージョンを必要とする NuGet の新機能が導入されました。</span><span class="sxs-lookup"><span data-stu-id="fc97f-117">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="fc97f-118">Web サイトの NuGet パッケージを管理するとき、これらの新しいパッケージ エラー WebMatrix に表示される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fc97f-118">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![エラーが発生しました。](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="fc97f-122">この最新リリースでは、最新の NuGet パッケージは、このエラーが発生していることを妨げてとの互換性を提供します。</span><span class="sxs-lookup"><span data-stu-id="fc97f-122">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="fc97f-123">Microsoft.AspNet.WebPages を含むパッケージの新しいバージョンは、WebMatrix で今すぐインストールできます。</span><span class="sxs-lookup"><span data-stu-id="fc97f-123">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="fc97f-124">これらのパッケージの一部を使用していた NuGet 機能など、 [XDT 構成変換](../release-notes/nuget-2.6.md#xdt)、これまで WebMatrix でサポートされていませんでした。</span><span class="sxs-lookup"><span data-stu-id="fc97f-124">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="fc97f-125">Bin フォルダー内の 0 バイト Dll</span><span class="sxs-lookup"><span data-stu-id="fc97f-125">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="fc97f-126">一部のユーザーが報告される NuGet のインストールをパッケージ化をビン分割にコピーする Dll を含む WebMatrix で Dll スライド ショーにした後、 `bin` 0 バイトのファイルとフォルダー。</span><span class="sxs-lookup"><span data-stu-id="fc97f-126">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="fc97f-127">これは、実行時にアプリケーションを中断します。</span><span class="sxs-lookup"><span data-stu-id="fc97f-127">This breaks the application at runtime.</span></span>

<span data-ttu-id="fc97f-128">[この問題](https://nuget.codeplex.com/workitem/4060)固定されているようになりました。</span><span class="sxs-lookup"><span data-stu-id="fc97f-128">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="fc97f-129">最近使用したその他の改善</span><span class="sxs-lookup"><span data-stu-id="fc97f-129">Other Recent Improvements</span></span>

<span data-ttu-id="fc97f-130">Visual Studio の NuGet パッケージ マネージャー 2.8 のリリース時おもリリース NuGet Package Manager 2.5.0 WebMatrix です。</span><span class="sxs-lookup"><span data-stu-id="fc97f-130">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="fc97f-131">説明したこの中に、 [NuGet 2.8 のリリース ノート](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)特定の更新プログラムが導入された新機能が記述されていません。</span><span class="sxs-lookup"><span data-stu-id="fc97f-131">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="fc97f-132">すべて更新します。</span><span class="sxs-lookup"><span data-stu-id="fc97f-132">Update All</span></span>

<span data-ttu-id="fc97f-133">すべての 1 つの手順で、web サイトのパッケージを今すぐ更新することができます。</span><span class="sxs-lookup"><span data-stu-id="fc97f-133">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="fc97f-134">WebMatrix で、NuGet 拡張機能を開くときは、ギャラリー、インストールされている、および利用可能な更新を持つ方すべてのパッケージの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="fc97f-134">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="fc97f-135">以前は、すべてのパッケージが個別に更新する必要がありますが、今すぐは [更新] タブに表示される便利すべて"更新"ボタン。</span><span class="sxs-lookup"><span data-stu-id="fc97f-135">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![利用可能な更新ですべてのパッケージを更新するには、[すべて更新] をクリックします。](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="fc97f-137">既存のファイルを上書き</span><span class="sxs-lookup"><span data-stu-id="fc97f-137">Overwrite Existing Files</span></span>

<span data-ttu-id="fc97f-138">Web サイトに既に存在するファイルを含むパッケージをインストールするときに、NuGet には常に同じサイレント (単独で、既存のファイルのまま)、それらのファイルが無視されました。</span><span class="sxs-lookup"><span data-stu-id="fc97f-138">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="fc97f-139">これは、パッケージがインストールされているか、ときに実際にはありませんでしたが正しく更新印象に可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fc97f-139">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="fc97f-140">NuGet が求められますファイルを上書きするようになりました。</span><span class="sxs-lookup"><span data-stu-id="fc97f-140">NuGet will now prompt for files to be overwritten.</span></span>

![ファイルの競合の解決](./media/NuGet-2.8/webmatrix-overwrite-file.png)
