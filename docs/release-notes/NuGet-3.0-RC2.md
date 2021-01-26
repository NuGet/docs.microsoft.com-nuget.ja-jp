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
# <a name="nuget-30-rc2-release-notes"></a>NuGet 3.0 RC2 リリースノート

[NuGet 3.0 RC リリースノート](../release-notes/nuget-3.0-RC.md)  | [NuGet 3.0 リリースノート](../release-notes/nuget-3.0.0.md)

NuGet 3.0 RC2 は、Visual Studio 2015 拡張機能ギャラリーおよび [Codeplex](https://nuget.codeplex.com/releases/view/615507)から提供される中間リリースとして、2015年6月3日にリリースされました。 このリリースには、Visual Studio 2015 のリリースが完了する前にリリースすることが重要だった、いくつかの重要なバグ修正とパフォーマンスの向上があります。 この NuGet 拡張機能のバージョンは、Visual Studio 2015 でのみ使用できます。

合計では、このリリースで158の問題を解決し、 [GitHub の問題の完全な一覧](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)を確認することができます。

## <a name="summary-of-top-issues-resolved"></a>解決された上位の問題の概要

* [パッケージマネージャーウィンドウが更新したときに頻繁に発生するネットワーク更新呼び出し](https://github.com/NuGet/Home/issues/515)
* [パッケージマネージャーのインストール済みビューに変更するときの遅延スクロール](https://github.com/NuGet/Home/issues/519)
* [ネットワーク呼び出しはバックグラウンドスレッドで実行する必要があります](https://github.com/NuGet/Home/issues/516)
* [[プレビューウィンドウを表示しない] チェックボックスが追加されました](https://github.com/NuGet/Home/issues/566)
* [プロセッサ使用率を減らすためのプロセス調整を追加しました](https://github.com/NuGet/Home/issues/356)
* ポータブルクラスライブラリの参照処理の向上
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [オートコンプリートサービスでは大文字と小文字が区別される](https://github.com/NuGet/Home/issues/198)
* [基本認証資格情報を再度導入するように更新](https://github.com/NuGet/Home/issues/456)
* [エラー ログ記録の改善](https://github.com/NuGet/Home/issues/407)
* [更新プログラムパッケージを呼び出すときの powershell エラーメッセージの改善](https://github.com/NuGet/Home/issues/5)

Codeplex から [nuget 拡張機能にこの更新プログラムを](https://nuget.codeplex.com/releases/view/615507) ダウンロードしてください。 nuget 3.0 の詳細と発表については、 [こちらのブログ](http://blog.nuget.org) をご覧ください。