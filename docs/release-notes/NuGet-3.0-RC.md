---
title: NuGet 3.0 RC リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.0 RC のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776567"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC リリースノート

[NuGet 3.0 ベータリリースノート](../release-notes/nuget-3.0-beta.md)  | [NuGet 3.0 RC2 リリースノート](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC は、Visual Studio 2015 RC リリースで2015年4月29日にリリースされました。 このリリースには、新しいフレームワークをサポートするために、いくつかの重要なバグ修正、パフォーマンスの向上、および更新が含まれています。  これは、Visual Studio 2015 でのみ使用できます。

### <a name="continued-focus-on-performance"></a>パフォーマンスについての継続的な取り組み

NuGet クエリの安定性とパフォーマンスは、注目している最新のトピックとして引き続き利用できます。  このリリースでは、NuGet UI と web サイトで非常に簡単な検索操作を確認できます。  サービスを監視し、サービスの使用方法を監視して、引き続きこれらの操作を調整できるようにします。

## <a name="significant-issues-resolved"></a>重大な問題の解決

NuGet クライアントを安定化するために、このリリースの一部として多くの問題を解決しました。  次に、いくつかの重要な問題の解決方法を簡単に示します。

* ASP.NET 5 用の K フレームワークの名前変更の一部として、dnx および dnxcore[リンク](https://github.com/NuGet/Home/issues/215)を処理するようにフレームワークモニカーが更新されました。
* Visual Studio UI[リンク](https://github.com/NuGet/Home/issues/232)のリンクからヘルプドキュメントを追加しました
* `.nuspec`コンマ区切りフレームワーク参照[リンク](https://github.com/NuGet/Home/issues/276)を使用したでの複雑な参照の処理の向上
* 日本語のカルチャ[リンク](https://github.com/NuGet/Home/issues/253)のサポートを修正した
* ASP.NET 5 プロジェクトが新しい v3 エンドポイント[リンク](https://github.com/NuGet/Home/issues/219)を使用できるように更新されたクライアント
* ソース管理[リンク](https://github.com/NuGet/Home/issues/56)を使用してパッケージフォルダーをより適切に処理するよう更新されました
* サテライトパッケージ[リンク](https://github.com/NuGet/Home/issues/17)のサポートを修正した
* フレームワーク固有のコンテンツファイル[リンク](https://github.com/NuGet/Home/issues/18)のサポートを修正しました

## <a name="github-presence-overhaul"></a>GitHub のプレゼンスの見直し

[GitHub のソースコードリポジトリ](http://github.com/nuget/home)にいくつかの変更を加えました。  NuGet Visual Studio クライアント、Powershell コマンド、またはコマンドライン実行可能ファイルに問題がある場合は、それらの問題をログに記録し、 [GitHub ホームリポジトリの問題リスト](http://github.com/nuget/home/issues)で進行状況を監視することができます。  [GitHub NuGetGallery リポジトリ](http://github.com/nuget/NuGetGallery/issues)でギャラリーの問題を追跡しています。


## <a name="stay-tuned"></a>引き続きご期待ください

NuGet 3.0 の進行状況と発表の詳細については、 [ブログをご覧](http://blog.nuget.org) ください。