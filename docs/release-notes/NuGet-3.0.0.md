---
title: NuGet 3.0 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.0.0 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776558"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="23ed2-103">NuGet 3.0 リリースノート</span><span class="sxs-lookup"><span data-stu-id="23ed2-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="23ed2-104">[NuGet 3.0 RC2 リリースノート](../release-notes/nuget-3.0-RC2.md)  | [NuGet 3.1 リリースノート](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="23ed2-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="23ed2-105">NuGet 3.0 は、Visual Studio 2015 のバンドル拡張として2015年7月20日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="23ed2-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="23ed2-106">このリリースの Visual Studio を使用して、新しい Visual Studio ユーザーが完全に更新された NuGet 3.0 エクスペリエンスを利用できるようにしました。</span><span class="sxs-lookup"><span data-stu-id="23ed2-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="23ed2-107">この NuGet 拡張機能のバージョンは、Visual Studio 2015 でのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="23ed2-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="23ed2-108">Visual studio ギャラリーへのアクセス権を持つ開発者は、Windows 10 開発のサポートが含まれている Visual Studio 2015 のリリースの直後に更新プログラムを発行するため、利用可能な最新バージョンに更新することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="23ed2-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="23ed2-109">合計では、3.0 リリースで240の問題を解決し、 [GitHub の問題の完全な一覧](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)を確認することができます。</span><span class="sxs-lookup"><span data-stu-id="23ed2-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="23ed2-110">既知の問題</span><span class="sxs-lookup"><span data-stu-id="23ed2-110">Known Issues</span></span>

<span data-ttu-id="23ed2-111">このリリースではいくつかの既知の問題が提供されており、これらのすべての項目は、7月29日の Windows 10 のリリースと一致するように、スケジュールされた3.1 リリースで修正されています。</span><span class="sxs-lookup"><span data-stu-id="23ed2-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="23ed2-112">この既知の問題を修正するには、その日以降にギャラリーから Visual Studio 拡張機能を更新することができます。</span><span class="sxs-lookup"><span data-stu-id="23ed2-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="23ed2-113">[プレビュー] ウィンドウと [パッケージの説明] ウィンドウの "作成者" ラベルに "次回からこの画面を表示しない" ラベルの翻訳が提供されていません。</span><span class="sxs-lookup"><span data-stu-id="23ed2-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="23ed2-114">TFS ソース管理を使用してプロジェクトを操作する場合、Nuget.Config ファイルが読み取り専用としてマークされていると、NuGet はパッケージマネージャーのユーザーインターフェイスを表示できません。</span><span class="sxs-lookup"><span data-stu-id="23ed2-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="23ed2-115">**回避策** TFS からファイルをチェックアウトします。</span><span class="sxs-lookup"><span data-stu-id="23ed2-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="23ed2-116">Visual Studio のダークテーマを使用すると、NuGet Powershell ウィンドウの黄色の "再起動バー" のテキストは表示されません。</span><span class="sxs-lookup"><span data-stu-id="23ed2-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="23ed2-117">**回避策** Visual Studio light テーマを使用します。</span><span class="sxs-lookup"><span data-stu-id="23ed2-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="23ed2-118">解決された上位の問題の概要</span><span class="sxs-lookup"><span data-stu-id="23ed2-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="23ed2-119">パッケージマネージャーウィンドウが更新したときに頻繁に発生するネットワーク更新呼び出し</span><span class="sxs-lookup"><span data-stu-id="23ed2-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="23ed2-120">パッケージマネージャーのインストール済みビューに変更するときの遅延スクロール</span><span class="sxs-lookup"><span data-stu-id="23ed2-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="23ed2-121">ネットワーク呼び出しはバックグラウンドスレッドで実行する必要があります</span><span class="sxs-lookup"><span data-stu-id="23ed2-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* <span data-ttu-id="23ed2-122">[[プレビューウィンドウを表示しない] チェックボックスが追加されました](https://github.com/NuGet/Home/issues/566)</span><span class="sxs-lookup"><span data-stu-id="23ed2-122">[Added 'Do not show preview window' checkbox](https://github.com/NuGet/Home/issues/566)</span></span>
* [<span data-ttu-id="23ed2-123">プロセッサ使用率を減らすためのプロセス調整を追加しました</span><span class="sxs-lookup"><span data-stu-id="23ed2-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="23ed2-124">ポータブルクラスライブラリの参照処理の向上</span><span class="sxs-lookup"><span data-stu-id="23ed2-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="23ed2-125">オートコンプリートサービスでは大文字と小文字が区別される</span><span class="sxs-lookup"><span data-stu-id="23ed2-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="23ed2-126">基本認証資格情報を再度導入するように更新</span><span class="sxs-lookup"><span data-stu-id="23ed2-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="23ed2-127">エラー ログ記録の改善</span><span class="sxs-lookup"><span data-stu-id="23ed2-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="23ed2-128">更新プログラムパッケージを呼び出すときの powershell エラーメッセージの改善</span><span class="sxs-lookup"><span data-stu-id="23ed2-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* <span data-ttu-id="23ed2-129">[Windows 10 でのクラッシュを防ぐための [オプションの詳細] リンクを修正した](https://github.com/NuGet/Home/issues/822)</span><span class="sxs-lookup"><span data-stu-id="23ed2-129">[Fixed the 'Learn about Options' link to prevent crashing on Windows 10](https://github.com/NuGet/Home/issues/822)</span></span>
* [<span data-ttu-id="23ed2-130">プレリリースチェックボックスの設定を保存する</span><span class="sxs-lookup"><span data-stu-id="23ed2-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="23ed2-131">ソリューション内のプロジェクト間で結果をキャッシュすることによってパフォーマンスを向上させる</span><span class="sxs-lookup"><span data-stu-id="23ed2-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="23ed2-132">複数のパッケージを並行して収集できます。</span><span class="sxs-lookup"><span data-stu-id="23ed2-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="23ed2-133">インストールパッケージ-force コマンドを削除しました</span><span class="sxs-lookup"><span data-stu-id="23ed2-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="23ed2-134">Windows 10 開発のサポートを提供する準備ができたら、 [ブログ](http://blog.nuget.org) で詳細を確認してください。</span><span class="sxs-lookup"><span data-stu-id="23ed2-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>