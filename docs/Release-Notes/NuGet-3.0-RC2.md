---
title: NuGet 3.0 RC2 リリース ノート
description: リリース ノート NuGet 3.0 RC2 既知の問題、バグの修正、追加された機能は、Dcr などです。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eb8b514fa967cc6ef850483b6b2a5df3ab27a550
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="11334-103">NuGet 3.0 RC2 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="11334-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="11334-104">[NuGet 3.0 RC のリリース ノート](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 リリース ノート](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="11334-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="11334-105">NuGet 3.0 RC2 は、Visual Studio 2015 の拡張機能ギャラリーから使用可能な中間リリースとして、2015 年 6 月 3 日にリリースされたと[Codeplex](https://nuget.codeplex.com/releases/view/615507)です。</span><span class="sxs-lookup"><span data-stu-id="11334-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="11334-106">このリリースでは、多数の重要なバグ修正とパフォーマンスの向上が完了した Visual Studio 2015 のリリースの前に解放する重要な.</span><span class="sxs-lookup"><span data-stu-id="11334-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="11334-107">この NuGet 拡張機能のバージョンは Visual Studio 2015 のできるだけです。</span><span class="sxs-lookup"><span data-stu-id="11334-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="11334-108">合計閉じられた 158 問題のこのリリースで、確認することができます、 [GitHub 上の問題の完全な一覧](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)です。</span><span class="sxs-lookup"><span data-stu-id="11334-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="11334-109">最上位の問題を解決の概要</span><span class="sxs-lookup"><span data-stu-id="11334-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="11334-110">頻繁にネットワークの更新呼び出しが更新されるとパッケージ マネージャー ウィンドウ</span><span class="sxs-lookup"><span data-stu-id="11334-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="11334-111">パッケージ マネージャーでインストールされたビューに変更する場合は、スクロールを遅延</span><span class="sxs-lookup"><span data-stu-id="11334-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="11334-112">ネットワークの呼び出しは、バック グラウンド スレッドで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="11334-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="11334-113">'プレビュー ウィンドウを表示しない チェック ボックスを追加</span><span class="sxs-lookup"><span data-stu-id="11334-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="11334-114">追加されたプロセスのプロセッサ使用率を削減する調整</span><span class="sxs-lookup"><span data-stu-id="11334-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="11334-115">ポータブル クラス ライブラリ参照処理の向上</span><span class="sxs-lookup"><span data-stu-id="11334-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="11334-116">オートコンプリートのサービスが大文字小文字を区別</span><span class="sxs-lookup"><span data-stu-id="11334-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="11334-117">基本認証資格情報を再導入する更新プログラム</span><span class="sxs-lookup"><span data-stu-id="11334-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="11334-118">強化されたエラーのログ記録</span><span class="sxs-lookup"><span data-stu-id="11334-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="11334-119">更新プログラム パッケージを呼び出すときに、強化された powershell エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="11334-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="11334-120">これをダウンロード[NuGet 拡張機能を更新](https://nuget.codeplex.com/releases/view/615507)Codeplex からくださいに注意して[私たちのブログ](http://blog.nuget.org)の詳細の進行状況と NuGet 3.0 のお知らせください。</span><span class="sxs-lookup"><span data-stu-id="11334-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>