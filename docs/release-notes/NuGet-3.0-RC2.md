---
title: NuGet 3.0 RC2 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.0 RC2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780282"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="90e43-103">NuGet 3.0 RC2 リリースノート</span><span class="sxs-lookup"><span data-stu-id="90e43-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="90e43-104">[NuGet 3.0 RC リリースノート](../release-notes/nuget-3.0-RC.md)  | [NuGet 3.0 リリースノート](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="90e43-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="90e43-105">NuGet 3.0 RC2 は、Visual Studio 2015 拡張機能ギャラリーおよび [Codeplex](https://nuget.codeplex.com/releases/view/615507)から提供される中間リリースとして、2015年6月3日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="90e43-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="90e43-106">このリリースには、Visual Studio 2015 のリリースが完了する前にリリースすることが重要だった、いくつかの重要なバグ修正とパフォーマンスの向上があります。</span><span class="sxs-lookup"><span data-stu-id="90e43-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="90e43-107">この NuGet 拡張機能のバージョンは、Visual Studio 2015 でのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="90e43-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="90e43-108">合計では、このリリースで158の問題を解決し、 [GitHub の問題の完全な一覧](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)を確認することができます。</span><span class="sxs-lookup"><span data-stu-id="90e43-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="90e43-109">解決された上位の問題の概要</span><span class="sxs-lookup"><span data-stu-id="90e43-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="90e43-110">パッケージマネージャーウィンドウが更新したときに頻繁に発生するネットワーク更新呼び出し</span><span class="sxs-lookup"><span data-stu-id="90e43-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="90e43-111">パッケージマネージャーのインストール済みビューに変更するときの遅延スクロール</span><span class="sxs-lookup"><span data-stu-id="90e43-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="90e43-112">ネットワーク呼び出しはバックグラウンドスレッドで実行する必要があります</span><span class="sxs-lookup"><span data-stu-id="90e43-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* <span data-ttu-id="90e43-113">[[プレビューウィンドウを表示しない] チェックボックスが追加されました](https://github.com/NuGet/Home/issues/566)</span><span class="sxs-lookup"><span data-stu-id="90e43-113">[Added 'Do not show preview window' checkbox](https://github.com/NuGet/Home/issues/566)</span></span>
* [<span data-ttu-id="90e43-114">プロセッサ使用率を減らすためのプロセス調整を追加しました</span><span class="sxs-lookup"><span data-stu-id="90e43-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="90e43-115">ポータブルクラスライブラリの参照処理の向上</span><span class="sxs-lookup"><span data-stu-id="90e43-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="90e43-116">オートコンプリートサービスでは大文字と小文字が区別される</span><span class="sxs-lookup"><span data-stu-id="90e43-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="90e43-117">基本認証資格情報を再度導入するように更新</span><span class="sxs-lookup"><span data-stu-id="90e43-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="90e43-118">エラー ログ記録の改善</span><span class="sxs-lookup"><span data-stu-id="90e43-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="90e43-119">更新プログラムパッケージを呼び出すときの powershell エラーメッセージの改善</span><span class="sxs-lookup"><span data-stu-id="90e43-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="90e43-120">Codeplex から [nuget 拡張機能にこの更新プログラムを](https://nuget.codeplex.com/releases/view/615507) ダウンロードしてください。 nuget 3.0 の詳細と発表については、 [こちらのブログ](http://blog.nuget.org) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="90e43-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>