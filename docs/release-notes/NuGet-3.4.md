---
title: NuGet 3.4 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.4 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551192"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 リリース ノート

[NuGet 3.4 RC リリース ノート](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 リリース ノート](../release-notes/nuget-3.4.1.md)

NuGet 3.4 では、Visual Studio 2015 Update 2 と Visual Studio 15 Preview リリースの一部として、2016 年 3 月 30 日にリリースされ、心でいくつかの基本思想付きでビルドされました。

* クロス プラットフォームのサポート
* パフォーマンスの向上
* UI の軽微な改善

次の機能、RC で以前に追加されたと更新または 3.4 のリリースが完了しました。

## <a name="new-features"></a>新機能

* Gzip コンテンツ エンコード リポジトリから NuGet クライアントを今すぐサポートします。
* Xproj プロジェクトでパッケージから Pdb のサポート
* IOS と Android のビルド アクションで contentFiles 要素のサポート
* Netstandard および netstandardapp フレームワーク モニカーのサポート

## <a name="new-user-interface-features"></a>ユーザー インターフェイスの新機能

* 特に、インストールされている、更新プログラム、および統合 タブで大幅なパフォーマンスの向上
* 集計の 'すべてのパッケージ ソース' のソースが適切な検索結果のマージに使用
* インストールし、更新プログラムのタブがアルファベット順に並べ替えるようになりました
* 更新を検索できるようにする更新 ボタンの追加
* バージョンの一覧の上部にある最新のビルド オプション

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* 参照されるパッケージ`project.json`浮動のあるバージョンですべてのビルドでは更新されません。 復元、クリーン、リビルド、または変更されたときにのみを更新する代わりに、`project.json`します。
* nuget.org リポジトリ ソースを NuGet 構成 UI を使用すると、不要になったプロジェクト構成に求められます。
* 不要になった NuGet では、共有プロジェクトでパッケージを復元もロック ファイルを書き込みます。
* 私たちは、ネットワーク障害を改善しました、到達できないか、応答に低速のサーバーの処理を再試行してください。
* Visual Studio パッケージ マネージャー UI では、キーボードとマウスの動作が向上しました。
* 最新のサポート`project.json`DNX 内のスキーマ。

## <a name="breaking-changes"></a>互換性に影響する変更点

* パッケージのバージョン番号が、形式に正規化されるようになりました*メジャー*.*マイナー*.*パッチ*-*プレリリース*それぞれのメジャー、マイナー、および修正プログラムは整数として扱われ、先頭に 0 を削除します。  プレリリース情報は、文字列として扱うし、して変更は適用されません。 これらの数値は、NuGet クライアントと、nuget.org のサービスによって提供される検索でクエリで使用されます。  詳細については、NuGet Docs で参照できます[プレリリース バージョン](../create-packages/prerelease-packages.md)します。

## <a name="known-issues"></a>既知の問題

* **問題:** 問題も Visual Studio のクラッシュなど Visual Studio で Powershell を使用した次のシナリオで Windows 10 v1511 ユーザーが発生する可能性があります。
    * インストール/install.ps1 のパッケージをアンインストール/uninstall.ps1 スクリプト
    * Init.ps1 スクリプトを (EntityFramework) のようなプロジェクトの読み込み
    * Web コンテンツの発行

* **回避策:** Windows 10 のインストールが最新のパッチ適用、expecially (KB 情報 3124263) 2016 年 1 月、または以降の更新プログラムがあることを確認します。  詳細についてで使用できる[GitHub 問題 #1638](http://github.com/nuget/home/issues/1638)

* **問題:** NuGet v2 プロトコル リダイレクトが壊れています。
要求を代替ホストにリダイレクトするカスタム NuGet リポジトリが、リダイレクト要求を行いません。
* **回避策:** この問題を回避するには、リダイレクトされたサーバーの場所を指す設定でパッケージ リポジトリ URI を構成します。
詳細については、[GitHub プル要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)を参照してください。

GitHub の問題一覧上の問題を追跡するために引き続き。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)