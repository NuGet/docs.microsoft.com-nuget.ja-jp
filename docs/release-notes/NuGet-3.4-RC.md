---
title: NuGet 3.4-RC リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.4 RC のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780233"
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4-RC リリースノート

[NuGet 3.3 リリースノート](../release-notes/nuget-3.3.md)  | [NuGet 3.4 リリースノート](../release-notes/nuget-3.4.md)

NuGet 3.4-RC は、Visual Studio 2015 Update 2 RC と共に2016年3月3日にリリースされ、いくつかの原則に基づいて構築されました。

* クロスプラットフォームサポート
* パフォーマンスの向上
* UI のマイナー機能強化

この RC では、次の機能が提供されています。これは、3.4 最終リリースに対してより多くの計画があります。

## <a name="new-features"></a>新機能

* NuGet クライアントでリポジトリからの gzip コンテンツエンコードがサポートされるようになりました
* Xproj プロジェクトのパッケージからの Pdb のサポート
* ContentFiles 要素での iOS および Android ビルドアクションのサポート
* Netstandard.library と netstandardapp フレームワークのモニカーのサポート

## <a name="new-user-interface-features"></a>新しいユーザーインターフェイスの機能

* インストール、更新、統合の各タブで大幅なパフォーマンスの向上
* インストールおよび更新のタブがアルファベット順に並べ替えられるようになりました。
* 検索を更新するための更新ボタンを追加しました

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* `project.json`浮動バージョンを持つで参照されるパッケージは、すべてのビルドで更新されません。 代わりに、復元、クリーン、リビルド、または変更を強制した場合にのみ更新され `project.json` ます。
* NuGet 構成 UI を使用する場合、nuget.org リポジトリソースはプロジェクト構成に強制されなくなりました。
* NuGet では、共有プロジェクトのパッケージが復元されず、ロックファイルも書き込まれなくなりました。
* ネットワークエラーを改善し、到達不能または応答の遅いサーバーの処理を再試行しました。
* Visual Studio パッケージマネージャーの UI では、キーボードとマウスの動作が改善されています。
* DNX の最新のスキーマがサポートされるようになりました `project.json` 。

## <a name="known-issues"></a>既知の問題

GitHub の問題の一覧に関する問題は、引き続き次の場所にあります。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)