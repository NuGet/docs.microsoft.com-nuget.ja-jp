---
title: "NuGet 3.4 RC のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.4 RC の既知の問題、バグの修正、追加された機能は、Dcr などのリリース ノートします。"
keywords: "NuGet 3.4 RC のリリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4 RC のリリース ノート

[NuGet 3.3 リリース ノート](../release-notes/nuget-3.3.md) | [NuGet 3.4 リリース ノート](../release-notes/nuget-3.4.md)

NuGet 3.4 RC では、Visual Studio 2015 Update 2 RC と共に、2016 年 3 月 3日がリリースされ、心にいくつかの基本思想でビルドされました。

* クロスプラット フォーム サポート
* パフォーマンスの向上
* マイナーの UI 機能強化

次の機能は、複数の 3.4 最終リリースの計画とこの RC で利用します。

## <a name="new-features"></a>新機能

* NuGet クライアント サポート gzip コンテンツ エンコード リポジトリから
* Xproj プロジェクトでパッケージから Pdb のサポート
* IOS および Android のビルド アクション contentFiles 要素でのサポート
* Netstandard および netstandardapp フレームワーク モニカーのサポート

## <a name="new-user-interface-features"></a>新しいユーザー インターフェイスの機能

* 特に、インストール、更新、および統合のタブ上の大幅なパフォーマンスの向上
* インストールされているし、更新プログラムのタブがアルファベット順に並べ替えられました
* 更新する検索を許可する更新 ボタンの追加

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* パッケージで参照されている`project.json`浮動があるすべてのビルドでバージョンは更新されません。 強制復元、クリーン、再構築、または変更する場合にのみを更新する代わりに、`project.json`です。
* nuget.org のリポジトリ ソースを NuGet 構成 UI を使用するときに、不要になったプロジェクト構成に求められます。
* 不要になった NuGet は、共有プロジェクトでパッケージを復元も、ロック ファイルを書き込みます。
* ネットワーク障害を改良しましたし、到達できないか、応答に低速のサーバーの処理を再試行してください。
* Visual Studio のパッケージ マネージャーの UI では、キーボードとマウスの動作が強化されています。
* 最新のサポート`project.json`DNX 内のスキーマです。

## <a name="known-issues"></a>既知の問題

あることができます、GitHub の問題一覧上の問題を追跡するために続行: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)