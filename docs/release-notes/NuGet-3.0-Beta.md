---
title: NuGet 3.0 ベータリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.0 Beta のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776622"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 ベータリリースノート

[NuGet 3.0 Preview リリースノート](../release-notes/nuget-3.0-preview.md)  | [NuGet 3.0 RC リリースノート](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta は、Visual Studio 2015 CTP 6 リリースでは、2015年2月23日にリリースされました。 このリリースでは、多くのアーキテクチャとパフォーマンスの向上が実現されており、nuget.org サービスのパフォーマンス設定のチューニングを開始することが期待されています。

この新しいバージョンをインストールする前に、NuGet Visual Studio 2015 拡張機能の以前のバージョンをアンインストールすることを強くお勧めします。  このバージョンの拡張機能に問題がある場合は、Visual Studio 2015 preview で使用するために、 [以前のバージョン](http://nuget.codeplex.com/downloads/get/909582) に戻すことをお勧めします。

## <a name="visual-studio-2012"></a>Visual Studio 2012 以降

この NuGet 3.0 Beta は、Visual Studio 2015 CTP 6 拡張機能ギャラリーにインストールできます。 Visual Studio 2012 および Visual Studio 2013 近日中にプレビューが削除される予定です。 私たちは、 [Visual Studio 2010 の更新を中止](http://blog.nuget.org/20141002/visual-studio-2010.html)することを以前に共有していましたが、このような難しい決定を行っていました。

## <a name="new-clientserver-api"></a>新しいクライアント/サーバー API

NuGet のクライアント/サーバープロトコルに関するいくつかの実装の詳細に取り組んでいます。 ここで行った作業は、パッケージの復元やパッケージのインストールなどの重要なシナリオに対して高可用性を重視して設計された NuGet 用の "API v3" を作成することです。 新しい API は、REST とハイパーメディアに基づいており、リソース形式として [JSON-LD](http://json-ld.org) を選択しています。

NuGet 3.0 Beta ビットでは、[パッケージソース] ボックスの一覧に "api.nuget.org" という新しいパッケージソースが表示されます。   そのパッケージソースを選択した場合は、新しい API を使用して nuget.org に接続します。NuGet 3.0 RC では、この新しい API v3 ベースのパッケージソースによって、v2 ベースの "nuget.org" パッケージソースが置き換えられます。  他のすべてのパブリックパッケージソースを無効にし、パブリックパッケージの唯一のリポジトリとして api.nuget.org のみを残しておくことをお勧めします。

V3 API の構築には時間がかかりますが、パブリックリポジトリへのアクセスを求める古いクライアントの標準 v2 API は引き続き維持されます。

## <a name="updated-ui"></a>更新された UI

このリリースでは、ユーザーインターフェイスを拡張して、パッケージで実行するアクションを選択し、画面の [オプション] 領域のチェックボックスに [プレビュー] ボタンを切り替えられるようにするコンボボックスを追加しました。  [オプション] 領域は折りたたむことができなくなり、使用可能なオプションを説明するヘルプリンクが表示されるようになりました。

![新しい NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>操作のログ記録

ログ情報を含むモーダルウィンドウを削除しました。ログ情報は、インストール時またはアンインストール時にすぐに表示され、非表示になります。  このウィンドウでは、情報を表示したり、コピーして貼り付けることができる場合に値が追加されませんでした。  ここでは、出力ログをすべて [出力] ウィンドウの [パッケージマネージャー] ウィンドウにリダイレクトしています。  これは、調査する一般的なビルドレポートとよく似ています。


### <a name="focus-on-performance"></a>パフォーマンスに焦点を当てる

NuGet 検索のパフォーマンスを向上させ、を取得するために、さまざまな変更を加えました。  これはお客様からの1つの懸念事項であり、今回のリリースで対処したいと考えていました。  サーバーを調整し、新しい CDN を構築しました。さらに、より関連性が高く、より高速なパッケージ検索結果を得られるように、クエリ照合ロジックが改善されました。

NuGet 3.0 の開発フェーズを進めながら、nuget.org サービスのチューニングと監視を行い、エクスペリエンスが向上したことを確認します。  ダウンタイムに関与する予定はありませんが、サービスのリソースの追加と変更が行われます。  サービス構成を変更した場合の詳細については、 [twitter フィード](http://twitter.com/nuget) に関する記事をご覧ください。

## <a name="building-nuget-with-nuget"></a>Nuget を使用した NuGet のビルド

Nuget パッケージに組み込まれているいくつかのコンポーネントに NuGet クライアントを rearchitected するようになりました。 独自のライブラリを再利用することで、再利用可能で、適切にパッケージ化できるコンポーネントを構築することができます。  重複するコードを排除し、ソリューション全体でパッケージを構築するための開発プロセスを適切に構成する方法を学習しました。  コードプロジェクトの構造とビルドプロセスの動作について説明するブログ記事をお探しください。

## <a name="stay-tuned"></a>引き続きご期待ください

NuGet 3.0 の進行状況と発表の詳細については、 [ブログをご覧](http://blog.nuget.org) ください。
