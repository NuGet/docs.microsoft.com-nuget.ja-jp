---
title: NuGet 3.3 リリース ノート |Microsoft ドキュメント
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.3 のリリース ノートです。
keywords: NuGet 3.3 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ab5e1ca550297c608017cb56dff32f4bd4bbb885
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 のリリース ノート

[NuGet 3.2.1 リリース ノート](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC のリリース ノート](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 は、多数のユーザー インターフェイスを更新し、コマンド ライン機能だけでなく NuGet クライアントに役立ちますの修正プログラムのコレクションで、2015 年 11 月 30日でリリースされました。

## <a name="new-features"></a>新機能

* NuGet コマンド ライン クライアントには、認証済みのフィードをシームレスに連携することを許可する資格情報プロバイダーが導入されました。 [資格情報プロバイダーの Visual Studio Team Services をインストールする方法について](../api/nuget-exe-credential-providers.md)と NuGet の構成を使用するクライアントは、NuGet Docs でご確認いただけます。

## <a name="new-user-interface-features"></a>新しいユーザー インターフェイスの機能

* 別々 の参照、インストール、および更新プログラムの使用可能なタブ
* 利用可能な更新の数を示す、使用可能なバッジを更新します。
* パッケージのパッケージがインストールされているかどうかを指定するパッケージの一覧はバッジまたは、更新プログラムが利用可能です
* カウントとパッケージの一覧に追加の作成者をダウンロードします。
* 最新の利用可能なバージョン番号と、パッケージ一覧に現在インストールされているバージョン番号
* クイック インストールは、使用できるようにアクション ボタンは、更新、およびパッケージの一覧からアンインストール
* パッケージの詳細パネルのわかりやすい動作設定ボタン
* パッケージの詳細パネルのパッケージの更新日
* ソリューション ビューのパネルを統合します。
* プロジェクトとソリューション ビューでインストールされているバージョン番号の並べ替え可能なグリッド

## <a name="new-command-line-features"></a>コマンド ラインの新機能

このバージョンでは導入された、`add`と`init`」の説明に従ってフォルダー ベースのリポジトリを初期化するためのコマンド、 [nuget.exe 参照](../tools/nuget-exe-cli-reference.md)です。 構築され、このフォルダーに保持するリポジトリの構造は[かなり高いパフォーマンス メリットをもたらします](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)ブログで説明したようです。

## <a name="contentfiles"></a>ContentFiles

コンテンツがサポートされるようになりました`project.json`マネージ プロジェクトは、新しい`contentFiles`フォルダーと`.nuspec``contentFiles`要素表記します。  このコンテンツは、プロジェクト システムとのやり取りのパッケージの作成者によって直接指定できます。  コンテンツ ファイルを構成する方法の詳細について、`.nuspec`ドキュメントは含まれて、 [.nuspec 参照](../reference/nuspec.md)です。

## <a name="nuget-locals-cache-management"></a>NuGet ローカル キャッシュの管理

コマンド ラインの NuGet がワークステーション上のローカルのキャッシュを管理する方法に関する情報が含まれる更新されました。  [ローカル] コマンドの詳細についてで使用できる、 [NuGet コマンド ライン リファレンス](../tools/cli-ref-locals.md)です。

## <a name="fixed-issues"></a>問題を修正しました

**注目すべき問題**

* 復元するための NuGet コマンド ラインの復元されたサポート パッケージの Mono - 上のファイルをソリューションが[1543](https://github.com/NuGet/Home/issues/1543)

GitHub の 3.3 のリリースで処理された問題の一覧が見つかりません、 [3.3 マイルス トーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)です。

3.3 コマンド ライン リリースで修正された問題の一覧に記録されます、 [3.3 コマンド ライン マイルス トーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)です。

## <a name="known-issues"></a>既知の問題

あることができます、GitHub の問題一覧上の問題を追跡するために続行します。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)