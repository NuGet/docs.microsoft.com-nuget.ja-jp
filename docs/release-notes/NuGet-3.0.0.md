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
# <a name="nuget-30-release-notes"></a>NuGet 3.0 リリースノート

[NuGet 3.0 RC2 リリースノート](../release-notes/nuget-3.0-RC2.md)  | [NuGet 3.1 リリースノート](../release-notes/nuget-3.1.md)

NuGet 3.0 は、Visual Studio 2015 のバンドル拡張として2015年7月20日にリリースされました。 このリリースの Visual Studio を使用して、新しい Visual Studio ユーザーが完全に更新された NuGet 3.0 エクスペリエンスを利用できるようにしました。 この NuGet 拡張機能のバージョンは、Visual Studio 2015 でのみ使用できます。

Visual studio ギャラリーへのアクセス権を持つ開発者は、Windows 10 開発のサポートが含まれている Visual Studio 2015 のリリースの直後に更新プログラムを発行するため、利用可能な最新バージョンに更新することをお勧めします。

合計では、3.0 リリースで240の問題を解決し、 [GitHub の問題の完全な一覧](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)を確認することができます。

## <a name="known-issues"></a>既知の問題

このリリースではいくつかの既知の問題が提供されており、これらのすべての項目は、7月29日の Windows 10 のリリースと一致するように、スケジュールされた3.1 リリースで修正されています。  この既知の問題を修正するには、その日以降にギャラリーから Visual Studio 拡張機能を更新することができます。

*  [プレビュー] ウィンドウと [パッケージの説明] ウィンドウの "作成者" ラベルに "次回からこの画面を表示しない" ラベルの翻訳が提供されていません。
*  TFS ソース管理を使用してプロジェクトを操作する場合、Nuget.Config ファイルが読み取り専用としてマークされていると、NuGet はパッケージマネージャーのユーザーインターフェイスを表示できません。
   * **回避策** TFS からファイルをチェックアウトします。
*  Visual Studio のダークテーマを使用すると、NuGet Powershell ウィンドウの黄色の "再起動バー" のテキストは表示されません。
   * **回避策** Visual Studio light テーマを使用します。


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
* [Windows 10 でのクラッシュを防ぐための [オプションの詳細] リンクを修正した](https://github.com/NuGet/Home/issues/822)
* [プレリリースチェックボックスの設定を保存する](https://github.com/NuGet/Home/issues/732)
* [ソリューション内のプロジェクト間で結果をキャッシュすることによってパフォーマンスを向上させる](https://github.com/NuGet/Home/issues/721)
* [複数のパッケージを並行して収集できます。](https://github.com/NuGet/Home/issues/713)
* [インストールパッケージ-force コマンドを削除しました](https://github.com/NuGet/Home/issues/697)

Windows 10 開発のサポートを提供する準備ができたら、 [ブログ](http://blog.nuget.org) で詳細を確認してください。