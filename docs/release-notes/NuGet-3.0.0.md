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
# <a name="nuget-30-release-notes"></a>NuGet 3.0 リリース ノート

[NuGet 3.0 RC2 リリース ノート](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 リリース ノート](../release-notes/nuget-3.1.md)

NuGet 3.0 は、Visual Studio 2015 にバンドルの拡張機能として、2015 年 7 月 20 日にリリースされました。 私たちは、包括的な更新された NuGet 3.0 エクスペリエンスは新しい Visual Studio ユーザーできるようになりますように Visual Studio では、このリリースを配信するプッシュされます。 この NuGet 拡張機能のバージョンは、Visual Studio 2015 のできるだけです。

Windows 10 開発のサポートを含む Visual Studio 2015 のリリースの直後、後更新プログラムを公開するように使用可能な最新バージョンの Visual Studio ギャラリー更新プログラムにアクセスできる開発者をお勧めします。

私たちの合計、閉じられた 3.0 リリースでは、240 の問題と、確認することができます、 [GitHub 上の問題の完全な一覧](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)します。

## <a name="known-issues"></a>既知の問題

数、このリリースで提供される既知の問題があったし、これらすべての項目では 29 年 7 月に Windows 10 のリリースと一致する場合は、スケジュールされた 3.1 リリースで修正します。  これらの既知の問題を解決するには、その日付以降には、ギャラリーから Visual Studio 拡張機能を更新することは。

*  プレビュー ウィンドウに「は今後表示しないこの」ラベルおよびパッケージの説明 ウィンドウで"Authors"のラベルは、翻訳が指定されていません。
*  コントロールをソース TFS を使用して、プロジェクトで作業するときに NuGet ことはできません、パッケージ マネージャー ユーザー インターフェイスを提供、Nuget.Config ファイルが読み取り専用としてマークされている場合。
   * **回避策**TFS からファイルをチェック アウトします。
*  Visual Studio ダーク テーマを使用すると、"再起動 bar"NuGet Powershell ウィンドウで、黄色のテキストは表示されません。
   * **回避策**Visual Studio の明るい色のテーマを使用します。


## <a name="summary-of-top-issues-resolved"></a>主な問題解決の概要

* [頻繁にネットワークの更新プログラムを呼び出すパッケージ マネージャー ウィンドウが更新されます。](https://github.com/NuGet/Home/issues/515)
* [変更する、パッケージ マネージャーでビューがインストールされている場合は、スクロールを遅延](https://github.com/NuGet/Home/issues/519)
* [ネットワーク呼び出しをバック グラウンド スレッドで実行する必要があります。](https://github.com/NuGet/Home/issues/516)
* ['プレビュー ウィンドウを表示しない チェック ボックスを追加](https://github.com/NuGet/Home/issues/566)
* [追加のプロセスがプロセッサ使用率を低減調整](https://github.com/NuGet/Home/issues/356)
* ポータブル クラス ライブラリ参照の処理を改善
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [オートコンプリートのサービスが大文字小文字を区別](https://github.com/NuGet/Home/issues/198)
* [基本認証資格情報を再導入する更新プログラム](https://github.com/NuGet/Home/issues/456)
* [強化されたエラーのログ記録](https://github.com/NuGet/Home/issues/407)
* [更新プログラム パッケージを呼び出すときに、powershell が強化されたエラー メッセージ](https://github.com/NuGet/Home/issues/5)
* [Windows 10 でクラッシュを防ぐために 'オプションの詳細' リンクを修正しました](https://github.com/NuGet/Home/issues/822)
* [プレリリース版のチェック ボックスの設定に注意してください。](https://github.com/NuGet/Home/issues/732)
* [ソリューション内のプロジェクト間で結果をキャッシュすることによってパフォーマンスを向上の収集](https://github.com/NuGet/Home/issues/721)
* [複数のパッケージを並列で収集することができます。](https://github.com/NuGet/Home/issues/713)
* [インストール パッケージの削除のコマンドを強制](https://github.com/NuGet/Home/issues/697)

監視してください[ブログ](http://blog.nuget.org)の詳細の進行状況とお知らせにつれて、Windows 10 開発のサポートを提供する準備ができます。