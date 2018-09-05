---
title: NuGet 3.3 のリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.3 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546648"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 のリリース ノート

[NuGet 3.2.1 のリリース ノート](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC リリース ノート](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 は、多数のユーザー インターフェイスの更新プログラムと機能のコマンド ラインほか NuGet クライアントに便利な修正プログラムのコレクションで、2015 年 11 月 30日にリリースされました。

## <a name="new-features"></a>新機能

* NuGet コマンド ライン クライアントを認証済みフィードとシームレスに連携できるように許可する資格情報プロバイダーが導入されています。 [資格情報プロバイダーの Visual Studio Team Services をインストールする方法について](../api/nuget-exe-credential-providers.md)NuGet の構成とそれを使用するクライアントは、NuGet Docs でご確認いただけます。

## <a name="new-user-interface-features"></a>ユーザー インターフェイスの新機能

* 参照、インストール、および使用可能な更新プログラムの個別のタブ
* 更新プログラムの使用可能なバッジが利用可能な更新を使用してパッケージの数を示す
* パッケージがインストールされているまたは、更新プログラムが利用可能なかどうかを指定するパッケージの一覧でパッケージのバッジ
* ダウンロード数と、パッケージ一覧に追加された作成者
* 最新の利用可能なバージョン番号とパッケージの一覧に現在インストールされているバージョン番号
* 動作設定ボタン クイックのインストールを許可するのには、更新、およびパッケージの一覧からアンインストール
* パッケージの詳細 パネルでわかりやすい動作設定ボタン
* パッケージの詳細 パネルでのパッケージの更新日
* ソリューション ビューのパネルを統合します。
* プロジェクトとソリューション ビューでインストールされているバージョン番号の並べ替え可能なグリッド

## <a name="new-command-line-features"></a>コマンド ラインの新機能

このバージョンで導入されました、`add`と`init`コマンド」の説明に従って、フォルダー ベースのリポジトリを初期化するために、 [nuget.exe 参照](../tools/nuget-exe-cli-reference.md)します。 構築され、このフォルダーに保持するリポジトリの構造は[パフォーマンスに大きなメリットをもたらします](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)私たちのブログで説明されているようです。

## <a name="contentfiles"></a>contentFiles

コンテンツがサポートされるようになりました`project.json`マネージ プロジェクトでは、新しい`contentFiles`フォルダーと`.nuspec``contentFiles`要素表記します。  このコンテンツは、プロジェクト システムとの対話のパッケージの作成者によって直接指定できます。  ContentFiles を構成する方法については、`.nuspec`ドキュメントが記載されて、 [.nuspec リファレンス](../reference/nuspec.md)します。

## <a name="nuget-locals-cache-management"></a>NuGet のローカル キャッシュの管理

NuGet コマンド ラインがワークステーションのローカル キャッシュを管理する方法についての情報を含めるように更新されました。  ローカル コマンドの詳細についてで使用できる、 [NuGet コマンド ライン リファレンス](../tools/cli-ref-locals.md)します。

## <a name="fixed-issues"></a>問題を修正しました

**注目に値する問題**

* 復元するための NuGet コマンド ラインの復元されたサポート パッケージの Mono - でソリューション ファイルが[1543](https://github.com/NuGet/Home/issues/1543)

3.3 のリリースで対処された問題の完全な一覧は、GitHub で確認できます、 [3.3 マイルス トーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)します。

コマンド ライン 3.3 のリリースで修正された問題の一覧に記録、 [3.3 コマンド ライン マイルス トーン](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)します。

## <a name="known-issues"></a>既知の問題

GitHub の問題一覧上の問題を追跡するために引き続き。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)