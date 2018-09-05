---
title: NuGet 3.0 RC2 リリース ノートします。
description: リリース ノート NuGet 3.0 RC2 の既知の問題、バグの修正、追加機能、および Dcr を含むです。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545822"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="78cdb-103">NuGet 3.0 RC2 リリース ノートします。</span><span class="sxs-lookup"><span data-stu-id="78cdb-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="78cdb-104">[NuGet 3.0 RC リリース ノート](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 リリース ノート](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="78cdb-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="78cdb-105">Visual Studio 2015 の拡張機能ギャラリーから使用可能な中間リリースとして、2015 年 6 月 3日 NuGet 3.0 RC2 がリリースされましたと[Codeplex](https://nuget.codeplex.com/releases/view/615507)します。</span><span class="sxs-lookup"><span data-stu-id="78cdb-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="78cdb-106">このリリースではさまざまな重要なバグの修正とパフォーマンスの向上が完成した Visual Studio 2015 のリリースの前にリリースする重要な.</span><span class="sxs-lookup"><span data-stu-id="78cdb-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="78cdb-107">この NuGet 拡張機能のバージョンは、Visual Studio 2015 のできるだけです。</span><span class="sxs-lookup"><span data-stu-id="78cdb-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="78cdb-108">私たちの合計、閉じられた、このリリースでは 158 の問題と、確認することができます、 [GitHub 上の問題の完全な一覧](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)します。</span><span class="sxs-lookup"><span data-stu-id="78cdb-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="78cdb-109">主な問題解決の概要</span><span class="sxs-lookup"><span data-stu-id="78cdb-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="78cdb-110">頻繁にネットワークの更新プログラムを呼び出すパッケージ マネージャー ウィンドウが更新されます。</span><span class="sxs-lookup"><span data-stu-id="78cdb-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="78cdb-111">変更する、パッケージ マネージャーでビューがインストールされている場合は、スクロールを遅延</span><span class="sxs-lookup"><span data-stu-id="78cdb-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="78cdb-112">ネットワーク呼び出しをバック グラウンド スレッドで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="78cdb-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="78cdb-113">'プレビュー ウィンドウを表示しない チェック ボックスを追加</span><span class="sxs-lookup"><span data-stu-id="78cdb-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="78cdb-114">追加のプロセスがプロセッサ使用率を低減調整</span><span class="sxs-lookup"><span data-stu-id="78cdb-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="78cdb-115">ポータブル クラス ライブラリ参照の処理を改善</span><span class="sxs-lookup"><span data-stu-id="78cdb-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="78cdb-116">オートコンプリートのサービスが大文字小文字を区別</span><span class="sxs-lookup"><span data-stu-id="78cdb-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="78cdb-117">基本認証資格情報を再導入する更新プログラム</span><span class="sxs-lookup"><span data-stu-id="78cdb-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="78cdb-118">強化されたエラーのログ記録</span><span class="sxs-lookup"><span data-stu-id="78cdb-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="78cdb-119">更新プログラム パッケージを呼び出すときに、powershell が強化されたエラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="78cdb-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="78cdb-120">これをダウンロード[NuGet 拡張機能を更新](https://nuget.codeplex.com/releases/view/615507)Codeplex からくださいに注意して[ブログ](http://blog.nuget.org)の詳細の進行状況と NuGet 3.0 のお知らせです。</span><span class="sxs-lookup"><span data-stu-id="78cdb-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>