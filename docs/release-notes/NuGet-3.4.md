---
title: NuGet 3.4 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.4 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776413"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 リリースノート

[NuGet 3.4-RC リリースノート](../release-notes/nuget-3.4-RC.md)  | [NuGet 3.4.1 のリリースノート](../release-notes/nuget-3.4.1.md)

NuGet 3.4 は、Visual Studio 2015 Update 2 および Visual Studio 15 Preview リリースの一部として2016年3月30日にリリースされ、いくつかの原則に基づいて構築されました。

* クロスプラットフォームサポート
* パフォーマンスの向上
* UI のマイナー機能強化

RC では、次の機能が以前に追加されており、3.4 リリースで更新または完了しています。

## <a name="new-features"></a>新機能

* NuGet クライアントでリポジトリからの gzip コンテンツエンコードがサポートされるようになりました
* Xproj プロジェクトのパッケージからの Pdb のサポート
* ContentFiles 要素での iOS および Android ビルドアクションのサポート
* Netstandard.library と netstandardapp フレームワークのモニカーのサポート

## <a name="new-user-interface-features"></a>新しいユーザーインターフェイスの機能

* インストール、更新、統合の各タブで大幅なパフォーマンスの向上
* 集計 ' すべてのパッケージソース ' ソースは、適切な検索結果のマージで使用できます
* インストールおよび更新のタブがアルファベット順に並べ替えられるようになりました。
* 検索を更新するための更新ボタンを追加しました
* バージョン一覧の先頭にある最新のビルドオプション

## <a name="updates-and-improvements"></a>更新プログラムと機能強化

* `project.json`浮動バージョンを持つで参照されるパッケージは、すべてのビルドで更新されません。 代わりに、復元、クリーン、リビルド、または変更を強制した場合にのみ更新され `project.json` ます。
* NuGet 構成 UI を使用する場合、nuget.org リポジトリソースはプロジェクト構成に強制されなくなりました。
* NuGet では、共有プロジェクトのパッケージが復元されず、ロックファイルも書き込まれなくなりました。
* ネットワークエラーを改善し、到達不能または応答の遅いサーバーの処理を再試行しました。
* Visual Studio パッケージマネージャーの UI では、キーボードとマウスの動作が改善されています。
* DNX の最新のスキーマがサポートされるようになりました `project.json` 。

## <a name="breaking-changes"></a>重大な変更

* パッケージのバージョン番号が *major* の形式に正規化されました。*minor*。*修正プログラム* -*プレリリース*  メジャー、マイナー、およびパッチはそれぞれ整数として扱われ、先頭のゼロは削除されます。  プレリリース情報は文字列として扱われ、変更は適用されません。 これらの数値は、NuGet クライアントによるクエリと、nuget.org サービスによって提供される検索で使用されます。  詳細については、NuGet のドキュメント ( [プレリリース版](../create-packages/prerelease-packages.md)) を参照してください。

## <a name="known-issues"></a>既知の問題

* **問題:** 次のシナリオでは、Windows 10 バージョン1511ユーザーが Visual Studio で Powershell を使用して問題を発生させるか、Visual Studio をクラッシュさせる可能性があります。
    * install.ps1/uninstall.ps1 スクリプトを含むパッケージのインストール/アンインストール
    * init.ps1 スクリプトを含むプロジェクトの読み込み (EntityFramework など)
    * Web コンテンツの発行

* **回避策:** Windows 10 のインストールに最新のパッチが適用されていることを確認してください。2016年1月 (KB 3124263) 以降の更新プログラムが適用されます。  詳細については、 [GitHub の問題](http://github.com/nuget/home/issues/1638)を参照してください #1638

* **問題:** NuGet v2 プロトコル リダイレクトが壊れています。
要求を代替ホストにリダイレクトするカスタム NuGet リポジトリが、リダイレクト要求を行いません。
* **回避策:**  この問題を回避するには、リダイレクトされたサーバーの場所を指すように [設定] でパッケージリポジトリの URI を構成します。
詳細については、「 [GitHub プル要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)」を参照してください。

GitHub の問題の一覧に関する問題は、引き続き次の場所にあります。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)