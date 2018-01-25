---
title: "NuGet 3.0 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.0.0 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 3.0.0 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ef8557c37105eb7915919c7b15d41d024921761f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="4e2d1-104">NuGet 3.0 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="4e2d1-104">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="4e2d1-105">[NuGet 3.0 RC2 リリース ノート](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 リリース ノート](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="4e2d1-105">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="4e2d1-106">NuGet 3.0 は、Visual Studio 2015 にバンドル拡張機能として、2015 年 7 月 20 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-106">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="4e2d1-107">完全に更新された NuGet 3.0 機能ができるように Visual Studio の新しいユーザーのこのリリースには、Visual Studio を配信することがプッシュされます。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-107">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="4e2d1-108">この NuGet 拡張機能のバージョンは Visual Studio 2015 のできるだけです。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="4e2d1-109">開発者は、Windows 10 の開発のサポートを含む Visual Studio 2015 のリリースのすぐ後に更新プログラムを公開として使用すると、最新のバージョンの Visual Studio ギャラリーの更新にアクセスできることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="4e2d1-110">おの合計、閉じられたリリースでは、3.0、240 の問題と、確認することができます、 [GitHub 上の問題の完全な一覧](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)です。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-110">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="4e2d1-111">既知の問題</span><span class="sxs-lookup"><span data-stu-id="4e2d1-111">Known Issues</span></span>

<span data-ttu-id="4e2d1-112">このリリースで提供される既知の問題の数があったし、これらの項目すべてでは 7 月 29日で Windows 10 のリリースで一致するように、スケジュールされた 3.1 リリースで修正します。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-112">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="4e2d1-113">これらの既知の問題を解決するには、その日以降に、ギャラリーから、Visual Studio 拡張機能を更新することができます。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-113">You will be able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="4e2d1-114">プレビュー ウィンドウに「を表示しない次回からこの」ラベルと、「作成者」パッケージの説明 ウィンドウでラベルの翻訳が指定されていません。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-114">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="4e2d1-115">コントロールをソース TFS を使用して、プロジェクトで作業する時に NuGet ことはできません、package manager ユーザー インターフェイスを提供 Nuget.Config ファイルが読み取り専用とマークされている場合。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-115">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="4e2d1-116">**回避策**TFS からファイルをチェック アウトします。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-116">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="4e2d1-117">Visual Studio ダーク テーマを使用する場合は、黄色、NuGet Powershell ウィンドウで「再起動バー」のテキストは表示されません。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-117">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="4e2d1-118">**回避策**Visual Studio の明るい色のテーマを使用します。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-118">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="4e2d1-119">最上位の問題を解決の概要</span><span class="sxs-lookup"><span data-stu-id="4e2d1-119">Summary of top issues resolved</span></span>

* [<span data-ttu-id="4e2d1-120">頻繁にネットワークの更新呼び出しが更新されるとパッケージ マネージャー ウィンドウ</span><span class="sxs-lookup"><span data-stu-id="4e2d1-120">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="4e2d1-121">パッケージ マネージャーでインストールされたビューに変更する場合は、スクロールを遅延</span><span class="sxs-lookup"><span data-stu-id="4e2d1-121">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="4e2d1-122">ネットワークの呼び出しは、バック グラウンド スレッドで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-122">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="4e2d1-123">'プレビュー ウィンドウを表示しない チェック ボックスを追加</span><span class="sxs-lookup"><span data-stu-id="4e2d1-123">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="4e2d1-124">追加されたプロセスのプロセッサ使用率を削減する調整</span><span class="sxs-lookup"><span data-stu-id="4e2d1-124">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="4e2d1-125">ポータブル クラス ライブラリ参照処理の向上</span><span class="sxs-lookup"><span data-stu-id="4e2d1-125">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="4e2d1-126">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="4e2d1-126">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="4e2d1-127">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="4e2d1-127">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="4e2d1-128">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="4e2d1-128">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="4e2d1-129">オートコンプリートのサービスが大文字小文字を区別</span><span class="sxs-lookup"><span data-stu-id="4e2d1-129">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="4e2d1-130">基本認証資格情報を再導入する更新プログラム</span><span class="sxs-lookup"><span data-stu-id="4e2d1-130">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="4e2d1-131">強化されたエラーのログ記録</span><span class="sxs-lookup"><span data-stu-id="4e2d1-131">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="4e2d1-132">更新プログラム パッケージを呼び出すときに、強化された powershell エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="4e2d1-132">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="4e2d1-133">Windows 10 でクラッシュを防ぐために 'オプションの詳細' リンクを修正</span><span class="sxs-lookup"><span data-stu-id="4e2d1-133">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="4e2d1-134">プレリリース版のチェック ボックスの設定に注意してください。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-134">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="4e2d1-135">ソリューション内のプロジェクト間で結果をキャッシュしてパフォーマンスを向上ギャザー</span><span class="sxs-lookup"><span data-stu-id="4e2d1-135">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="4e2d1-136">複数のパッケージを並列で収集することができます。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-136">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="4e2d1-137">インストール パッケージを削除しました-コマンドの強制</span><span class="sxs-lookup"><span data-stu-id="4e2d1-137">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="4e2d1-138">ください。 注意を続け[私たちのブログ](http://blog.nuget.org)の詳細の進行状況と知らせにつれて、Windows 10 の開発のサポートを提供する準備ができます。</span><span class="sxs-lookup"><span data-stu-id="4e2d1-138">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>