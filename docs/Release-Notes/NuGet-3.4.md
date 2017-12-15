---
title: "NuGet 3.4 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 80a429f5-7569-4349-ad7f-4fe9218eac23
description: "NuGet 3.4 が既知の問題、バグの修正、追加された機能は、Dcr などのリリース ノートします。"
keywords: "NuGet 3.4 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 911e4377ad9c8b1f865b0721f43ff73b62df6d1e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 リリース ノート

[NuGet 3.4 RC のリリース ノート](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 リリース ノート](../release-notes/nuget-3.4.1.md)

NuGet 3.4 機は、Visual Studio 2015 Update 2 と Visual Studio 15 Preview リリースの一部として、2016 年 3 月 30 日がリリースされ、心にいくつかの基本思想でビルドされました。

*  クロスプラット フォーム サポート
*  パフォーマンスの向上
*  マイナーの UI 機能強化

次の機能 RC で以前に追加されたと更新またはされた 3.4 のリリースでは、完了しました。

## <a name="new-features"></a>新機能

* NuGet クライアント サポート gzip コンテンツ エンコード リポジトリから
* Xproj プロジェクトでパッケージから Pdb のサポート
* IOS および Android のビルド アクション contentFiles 要素でのサポート
* Netstandard および netstandardapp フレームワーク モニカーのサポート

## <a name="new-user-interface-features"></a>新しいユーザー インターフェイスの機能

* 特に、インストール、更新、および統合のタブ上の大幅なパフォーマンスの向上
* 集計の 'すべてのパッケージ ソース' ソースを適切な検索結果の結合を使用
* インストールされているし、更新プログラムのタブがアルファベット順に並べ替えられました
* 更新する検索を許可する更新 ボタンの追加
* バージョンのリストの上部にある最新のビルド オプション

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* パッケージで参照されている`project.json`浮動があるすべてのビルドでバージョンは更新されません。 強制復元、クリーン、再構築、または変更する場合にのみを更新する代わりに、`project.json`です。
* nuget.org のリポジトリ ソースを NuGet 構成 UI を使用するときに、不要になったプロジェクト構成に求められます。
* 不要になった NuGet は、共有プロジェクトでパッケージを復元も、ロック ファイルを書き込みます。
* ネットワーク障害を改良しましたし、到達できないか、応答に低速のサーバーの処理を再試行してください。
* Visual Studio のパッケージ マネージャーの UI では、キーボードとマウスの動作が強化されています。
* 最新のサポート`project.json`DNX 内のスキーマです。

## <a name="breaking-changes"></a>互換性に影響する変更点

* パッケージのバージョン番号が、形式に正規化されたようになりました*メジャー*.*マイナー*.*修正プログラム*-*プレリリース*のメジャー、マイナー、し、修正プログラムは整数として扱われ、すべて先頭に 0 を削除します。  プレリリース情報が文字列として扱われに変更は適用されません。 これらの番号は、NuGet クライアントおよび nuget.org サービスによって指定された検索クエリで使用されます。  詳細については、NuGet のドキュメントを参照できます[プレリリース バージョン](../create-packages/prerelease-packages.md)します。

## <a name="known-issues"></a>既知の問題

* **問題点:** v1511 ユーザーの Windows 10 の問題またはでも Visual Studio でクラッシュが Visual Studio での Powershell で、次のシナリオが適用される場合があります。
    * インストール/install.ps1 をされているパッケージをアンインストールする/uninstall.ps1 スクリプト
    * Init.ps1 スクリプト (EntityFramework) のように既にあるプロジェクトの読み込み
    * Web コンテンツの発行

* **回避策:** Windows 10 のインストールが最新のパッチが適用されて、expecially (KB 情報 3124263) 2016 年 1 月、または以降の更新プログラムがあることを確認します。  詳細についてで使用できる[GitHub 問題 #1638](http://github.com/nuget/home/issues/1638)

* **問題:** NuGet v2 プロトコル リダイレクトが壊れています。
要求を代替ホストにリダイレクトするカスタム NuGet リポジトリが、リダイレクト要求を行いません。
* **回避策:**この問題を回避するには、リダイレクトされたサーバーの場所を指す設定でパッケージ リポジトリの URI を構成します。
詳細については、次を参照してください。 [GitHub プル要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)です。

あることができます、GitHub の問題一覧上の問題を追跡するために続行: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)