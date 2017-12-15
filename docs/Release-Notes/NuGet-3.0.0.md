---
title: "NuGet 3.0 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 8ad13a67-9348-4f04-8f8b-b8f4a0b2c6df
description: "NuGet 3.0.0 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 3.0.0 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 95c4bf92f5eeb676fa6bcc3b7bcbf191efa9cb9e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 リリース ノート

[NuGet 3.0 RC2 リリース ノート](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 リリース ノート](../release-notes/nuget-3.1.md)

NuGet 3.0 は、Visual Studio 2015 にバンドル拡張機能として、2015 年 7 月 20 日にリリースされました。 完全に更新された NuGet 3.0 機能ができるように Visual Studio の新しいユーザーのこのリリースには、Visual Studio を配信することがプッシュされます。 この NuGet 拡張機能のバージョンは Visual Studio 2015 のできるだけです。

開発者は、Windows 10 の開発のサポートを含む Visual Studio 2015 のリリースのすぐ後に更新プログラムを公開として使用すると、最新のバージョンの Visual Studio ギャラリーの更新にアクセスできることをお勧めします。

おの合計、閉じられたリリースでは、3.0、240 の問題と、確認することができます、 [GitHub 上の問題の完全な一覧](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)です。

## <a name="known-issues"></a>既知の問題

このリリースで提供される既知の問題の数があったし、これらの項目すべてでは 7 月 29日で Windows 10 のリリースで一致するように、スケジュールされた 3.1 リリースで修正します。  これらの既知の問題を解決するには、その日以降に、ギャラリーから、Visual Studio 拡張機能を更新することができます。

*  プレビュー ウィンドウに「を表示しない次回からこの」ラベルと、「作成者」パッケージの説明 ウィンドウでラベルの翻訳が指定されていません。
*  コントロールをソース TFS を使用して、プロジェクトで作業する時に NuGet ことはできません、package manager ユーザー インターフェイスを提供 Nuget.Config ファイルが読み取り専用とマークされている場合。
   * **回避策**TFS からファイルをチェック アウトします。
*  Visual Studio ダーク テーマを使用する場合は、黄色、NuGet Powershell ウィンドウで「再起動バー」のテキストは表示されません。
   * **回避策**Visual Studio の明るい色のテーマを使用します。


## <a name="summary-of-top-issues-resolved"></a>最上位の問題を解決の概要

* [頻繁にネットワークの更新呼び出しが更新されるとパッケージ マネージャー ウィンドウ](https://github.com/NuGet/Home/issues/515)
* [パッケージ マネージャーでインストールされたビューに変更する場合は、スクロールを遅延](https://github.com/NuGet/Home/issues/519)
* [ネットワークの呼び出しは、バック グラウンド スレッドで実行する必要があります。](https://github.com/NuGet/Home/issues/516)
* ['プレビュー ウィンドウを表示しない チェック ボックスを追加](https://github.com/NuGet/Home/issues/566)
* [追加されたプロセスのプロセッサ使用率を削減する調整](https://github.com/NuGet/Home/issues/356)
* ポータブル クラス ライブラリ参照処理の向上
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [オートコンプリートのサービスが大文字小文字を区別](https://github.com/NuGet/Home/issues/198)
* [基本認証資格情報を再導入する更新プログラム](https://github.com/NuGet/Home/issues/456)
* [強化されたエラーのログ記録](https://github.com/NuGet/Home/issues/407)
* [更新プログラム パッケージを呼び出すときに、強化された powershell エラー メッセージ](https://github.com/NuGet/Home/issues/5)
* [Windows 10 でクラッシュを防ぐために 'オプションの詳細' リンクを修正](https://github.com/NuGet/Home/issues/822)
* [プレリリース版のチェック ボックスの設定に注意してください。](https://github.com/NuGet/Home/issues/732)
* [ソリューション内のプロジェクト間で結果をキャッシュしてパフォーマンスを向上ギャザー](https://github.com/NuGet/Home/issues/721)
* [複数のパッケージを並列で収集することができます。](https://github.com/NuGet/Home/issues/713)
* [インストール パッケージを削除しました-コマンドの強制](https://github.com/NuGet/Home/issues/697)

ください。 注意を続け[私たちのブログ](http://blog.nuget.org)の詳細の進行状況と知らせにつれて、Windows 10 の開発のサポートを提供する準備ができます。