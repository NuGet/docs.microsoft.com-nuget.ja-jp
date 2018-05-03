---
title: NuGet 3.0 リリース ノート
description: NuGet 3.0.0 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 26236c2db0e1a6be9c660905db567d9ebbbbe377
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="49e54-103">NuGet 3.0 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="49e54-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="49e54-104">[NuGet 3.0 RC2 リリース ノート](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 リリース ノート](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="49e54-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="49e54-105">NuGet 3.0 は、Visual Studio 2015 にバンドル拡張機能として、2015 年 7 月 20 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="49e54-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="49e54-106">完全に更新された NuGet 3.0 機能ができるように Visual Studio の新しいユーザーのこのリリースには、Visual Studio を配信することがプッシュされます。</span><span class="sxs-lookup"><span data-stu-id="49e54-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="49e54-107">この NuGet 拡張機能のバージョンは Visual Studio 2015 のできるだけです。</span><span class="sxs-lookup"><span data-stu-id="49e54-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="49e54-108">開発者は、Windows 10 の開発のサポートを含む Visual Studio 2015 のリリースのすぐ後に更新プログラムを公開として使用すると、最新のバージョンの Visual Studio ギャラリーの更新にアクセスできることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="49e54-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="49e54-109">おの合計、閉じられたリリースでは、3.0、240 の問題と、確認することができます、 [GitHub 上の問題の完全な一覧](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)です。</span><span class="sxs-lookup"><span data-stu-id="49e54-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="49e54-110">既知の問題</span><span class="sxs-lookup"><span data-stu-id="49e54-110">Known Issues</span></span>

<span data-ttu-id="49e54-111">このリリースで提供される既知の問題の数があったし、これらの項目すべてでは 7 月 29日で Windows 10 のリリースで一致するように、スケジュールされた 3.1 リリースで修正します。</span><span class="sxs-lookup"><span data-stu-id="49e54-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="49e54-112">これらの既知の問題を解決するには、その日以降に、ギャラリーから、Visual Studio 拡張機能を更新できます。</span><span class="sxs-lookup"><span data-stu-id="49e54-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="49e54-113">プレビュー ウィンドウに「を表示しない次回からこの」ラベルと、「作成者」パッケージの説明 ウィンドウでラベルの翻訳が指定されていません。</span><span class="sxs-lookup"><span data-stu-id="49e54-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="49e54-114">コントロールをソース TFS を使用して、プロジェクトで作業する時に NuGet ことはできません、package manager ユーザー インターフェイスを提供 Nuget.Config ファイルが読み取り専用とマークされている場合。</span><span class="sxs-lookup"><span data-stu-id="49e54-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="49e54-115">**回避策**TFS からファイルをチェック アウトします。</span><span class="sxs-lookup"><span data-stu-id="49e54-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="49e54-116">Visual Studio ダーク テーマを使用する場合は、黄色、NuGet Powershell ウィンドウで「再起動バー」のテキストは表示されません。</span><span class="sxs-lookup"><span data-stu-id="49e54-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="49e54-117">**回避策**Visual Studio の明るい色のテーマを使用します。</span><span class="sxs-lookup"><span data-stu-id="49e54-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="49e54-118">最上位の問題を解決の概要</span><span class="sxs-lookup"><span data-stu-id="49e54-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="49e54-119">頻繁にネットワークの更新呼び出しが更新されるとパッケージ マネージャー ウィンドウ</span><span class="sxs-lookup"><span data-stu-id="49e54-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="49e54-120">パッケージ マネージャーでインストールされたビューに変更する場合は、スクロールを遅延</span><span class="sxs-lookup"><span data-stu-id="49e54-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="49e54-121">ネットワークの呼び出しは、バック グラウンド スレッドで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="49e54-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="49e54-122">'プレビュー ウィンドウを表示しない チェック ボックスを追加</span><span class="sxs-lookup"><span data-stu-id="49e54-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="49e54-123">追加されたプロセスのプロセッサ使用率を削減する調整</span><span class="sxs-lookup"><span data-stu-id="49e54-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="49e54-124">ポータブル クラス ライブラリ参照処理の向上</span><span class="sxs-lookup"><span data-stu-id="49e54-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="49e54-125">オートコンプリートのサービスが大文字小文字を区別</span><span class="sxs-lookup"><span data-stu-id="49e54-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="49e54-126">基本認証資格情報を再導入する更新プログラム</span><span class="sxs-lookup"><span data-stu-id="49e54-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="49e54-127">強化されたエラーのログ記録</span><span class="sxs-lookup"><span data-stu-id="49e54-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="49e54-128">更新プログラム パッケージを呼び出すときに、強化された powershell エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="49e54-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="49e54-129">Windows 10 でクラッシュを防ぐために 'オプションの詳細' リンクを修正</span><span class="sxs-lookup"><span data-stu-id="49e54-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="49e54-130">プレリリース版のチェック ボックスの設定に注意してください。</span><span class="sxs-lookup"><span data-stu-id="49e54-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="49e54-131">ソリューション内のプロジェクト間で結果をキャッシュしてパフォーマンスを向上ギャザー</span><span class="sxs-lookup"><span data-stu-id="49e54-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="49e54-132">複数のパッケージを並列で収集することができます。</span><span class="sxs-lookup"><span data-stu-id="49e54-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="49e54-133">インストール パッケージを削除しました-コマンドの強制</span><span class="sxs-lookup"><span data-stu-id="49e54-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="49e54-134">ください。 注意を続け[私たちのブログ](http://blog.nuget.org)の詳細の進行状況と知らせにつれて、Windows 10 の開発のサポートを提供する準備ができます。</span><span class="sxs-lookup"><span data-stu-id="49e54-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>