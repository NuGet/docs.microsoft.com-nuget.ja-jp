---
title: NuGet 3.0 リリース ノート
description: NuGet 3.0.0 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551864"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="3c31a-103">NuGet 3.0 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="3c31a-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="3c31a-104">[NuGet 3.0 RC2 リリース ノート](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 リリース ノート](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="3c31a-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="3c31a-105">NuGet 3.0 は、Visual Studio 2015 にバンドルの拡張機能として、2015 年 7 月 20 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="3c31a-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="3c31a-106">私たちは、包括的な更新された NuGet 3.0 エクスペリエンスは新しい Visual Studio ユーザーできるようになりますように Visual Studio では、このリリースを配信するプッシュされます。</span><span class="sxs-lookup"><span data-stu-id="3c31a-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="3c31a-107">この NuGet 拡張機能のバージョンは、Visual Studio 2015 のできるだけです。</span><span class="sxs-lookup"><span data-stu-id="3c31a-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="3c31a-108">Windows 10 開発のサポートを含む Visual Studio 2015 のリリースの直後、後更新プログラムを公開するように使用可能な最新バージョンの Visual Studio ギャラリー更新プログラムにアクセスできる開発者をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3c31a-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="3c31a-109">私たちの合計、閉じられた 3.0 リリースでは、240 の問題と、確認することができます、 [GitHub 上の問題の完全な一覧](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)します。</span><span class="sxs-lookup"><span data-stu-id="3c31a-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="3c31a-110">既知の問題</span><span class="sxs-lookup"><span data-stu-id="3c31a-110">Known Issues</span></span>

<span data-ttu-id="3c31a-111">数、このリリースで提供される既知の問題があったし、これらすべての項目では 29 年 7 月に Windows 10 のリリースと一致する場合は、スケジュールされた 3.1 リリースで修正します。</span><span class="sxs-lookup"><span data-stu-id="3c31a-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="3c31a-112">これらの既知の問題を解決するには、その日付以降には、ギャラリーから Visual Studio 拡張機能を更新することは。</span><span class="sxs-lookup"><span data-stu-id="3c31a-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="3c31a-113">プレビュー ウィンドウに「は今後表示しないこの」ラベルおよびパッケージの説明 ウィンドウで"Authors"のラベルは、翻訳が指定されていません。</span><span class="sxs-lookup"><span data-stu-id="3c31a-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="3c31a-114">コントロールをソース TFS を使用して、プロジェクトで作業するときに NuGet ことはできません、パッケージ マネージャー ユーザー インターフェイスを提供、Nuget.Config ファイルが読み取り専用としてマークされている場合。</span><span class="sxs-lookup"><span data-stu-id="3c31a-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="3c31a-115">**回避策**TFS からファイルをチェック アウトします。</span><span class="sxs-lookup"><span data-stu-id="3c31a-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="3c31a-116">Visual Studio ダーク テーマを使用すると、"再起動 bar"NuGet Powershell ウィンドウで、黄色のテキストは表示されません。</span><span class="sxs-lookup"><span data-stu-id="3c31a-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="3c31a-117">**回避策**Visual Studio の明るい色のテーマを使用します。</span><span class="sxs-lookup"><span data-stu-id="3c31a-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="3c31a-118">主な問題解決の概要</span><span class="sxs-lookup"><span data-stu-id="3c31a-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="3c31a-119">頻繁にネットワークの更新プログラムを呼び出すパッケージ マネージャー ウィンドウが更新されます。</span><span class="sxs-lookup"><span data-stu-id="3c31a-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="3c31a-120">変更する、パッケージ マネージャーでビューがインストールされている場合は、スクロールを遅延</span><span class="sxs-lookup"><span data-stu-id="3c31a-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="3c31a-121">ネットワーク呼び出しをバック グラウンド スレッドで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3c31a-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="3c31a-122">'プレビュー ウィンドウを表示しない チェック ボックスを追加</span><span class="sxs-lookup"><span data-stu-id="3c31a-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="3c31a-123">追加のプロセスがプロセッサ使用率を低減調整</span><span class="sxs-lookup"><span data-stu-id="3c31a-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="3c31a-124">ポータブル クラス ライブラリ参照の処理を改善</span><span class="sxs-lookup"><span data-stu-id="3c31a-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="3c31a-125">オートコンプリートのサービスが大文字小文字を区別</span><span class="sxs-lookup"><span data-stu-id="3c31a-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="3c31a-126">基本認証資格情報を再導入する更新プログラム</span><span class="sxs-lookup"><span data-stu-id="3c31a-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="3c31a-127">強化されたエラーのログ記録</span><span class="sxs-lookup"><span data-stu-id="3c31a-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="3c31a-128">更新プログラム パッケージを呼び出すときに、powershell が強化されたエラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="3c31a-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="3c31a-129">Windows 10 でクラッシュを防ぐために 'オプションの詳細' リンクを修正しました</span><span class="sxs-lookup"><span data-stu-id="3c31a-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="3c31a-130">プレリリース版のチェック ボックスの設定に注意してください。</span><span class="sxs-lookup"><span data-stu-id="3c31a-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="3c31a-131">ソリューション内のプロジェクト間で結果をキャッシュすることによってパフォーマンスを向上の収集</span><span class="sxs-lookup"><span data-stu-id="3c31a-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="3c31a-132">複数のパッケージを並列で収集することができます。</span><span class="sxs-lookup"><span data-stu-id="3c31a-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="3c31a-133">インストール パッケージの削除のコマンドを強制</span><span class="sxs-lookup"><span data-stu-id="3c31a-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="3c31a-134">監視してください[ブログ](http://blog.nuget.org)の詳細の進行状況とお知らせにつれて、Windows 10 開発のサポートを提供する準備ができます。</span><span class="sxs-lookup"><span data-stu-id="3c31a-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>