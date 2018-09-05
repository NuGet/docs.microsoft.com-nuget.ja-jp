---
title: NuGet 3.4 RC リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.4 RC のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546755"
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4 RC リリース ノート

[NuGet 3.3 のリリース ノート](../release-notes/nuget-3.3.md) | [NuGet 3.4 のリリース ノート](../release-notes/nuget-3.4.md)

NuGet 3.4-RC では、2016 年 3 月 3 日 Visual Studio 2015 Update 2 RC と共にリリースされ、心でいくつかの基本思想付きでビルドされました。

* クロス プラットフォームのサポート
* パフォーマンスの向上
* UI の軽微な改善

次の機能は、複数の 3.4 の最終リリースの計画と、この RC で利用できます。

## <a name="new-features"></a>新機能

* Gzip コンテンツ エンコード リポジトリから NuGet クライアントを今すぐサポートします。
* Xproj プロジェクトでパッケージから Pdb のサポート
* IOS と Android のビルド アクションで contentFiles 要素のサポート
* Netstandard および netstandardapp フレームワーク モニカーのサポート

## <a name="new-user-interface-features"></a>ユーザー インターフェイスの新機能

* 特に、インストールされている、更新プログラム、および統合 タブで大幅なパフォーマンスの向上
* インストールし、更新プログラムのタブがアルファベット順に並べ替えるようになりました
* 更新を検索できるようにする更新 ボタンの追加

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* 参照されるパッケージ`project.json`浮動のあるバージョンですべてのビルドでは更新されません。 復元、クリーン、リビルド、または変更されたときにのみを更新する代わりに、`project.json`します。
* nuget.org リポジトリ ソースを NuGet 構成 UI を使用すると、不要になったプロジェクト構成に求められます。
* 不要になった NuGet では、共有プロジェクトでパッケージを復元もロック ファイルを書き込みます。
* 私たちは、ネットワーク障害を改善しました、到達できないか、応答に低速のサーバーの処理を再試行してください。
* Visual Studio パッケージ マネージャー UI では、キーボードとマウスの動作が向上しました。
* 最新のサポート`project.json`DNX 内のスキーマ。

## <a name="known-issues"></a>既知の問題

GitHub の問題一覧上の問題を追跡するために引き続き。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)