---
title: NuGet 3.0 RC リリース ノートします。
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.0 RC のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551720"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC リリース ノートします。

[NuGet 3.0 ベータ版のリリース ノート](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 リリース ノート](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC は、Visual Studio 2015 RC リリースでは、2015 年 4 月 29 日にリリースされました。 このリリースではさまざまな重要なバグの修正、パフォーマンスの向上と新しいフレームワークをサポートするために更新します。  Visual Studio 2015 の使用可能なは。

### <a name="continued-focus-on-performance"></a>パフォーマンスで継続的なフォーカス

安定性と NuGet のクエリのパフォーマンスに注目していますが、ホットなトピックを続行します。  このリリースでは、NuGet UI と web サイトで非常に高速検索操作を参照してくださいを開始する必要があります。  サービスおよびこれらの操作を調整することを続行するために、サービスを使用する方法を監視しています。

## <a name="significant-issues-resolved"></a>重要な問題の解決

NuGet クライアントを安定化するためには、このリリースの一環として多くの問題を解決しました。  さらに重要な問題を解決のいくつかの簡単な一覧だけを次に示します。

* Dnx と dnxcore を処理する ASP.NET 5 の K フレームワークの名前の変更の一環として、フレームワークのモニカーが更新されました[リンク](https://github.com/NuGet/Home/issues/215)
* Visual Studio UI 内のリンクからヘルプ ドキュメントが追加されました[リンク](https://github.com/NuGet/Home/issues/232)
* 複雑な参照の処理の改善`.nuspec`フレームワークのコンマ区切りの参照を含む[リンク](https://github.com/NuGet/Home/issues/276)
* 日本語のカルチャのサポートを修正しました[リンク。](https://github.com/NuGet/Home/issues/253)
* ASP.NET 5 プロジェクトで新しい v3 エンドポイントの使用を許可する更新されたクライアント[リンク](https://github.com/NuGet/Home/issues/219)
* ソース コントロールにハンドルを適切に更新されたパッケージ フォルダー[リンク](https://github.com/NuGet/Home/issues/56)
* サテライト パッケージのサポートを修正しました[リンク。](https://github.com/NuGet/Home/issues/17)
* フレームワークに固有のコンテンツ ファイルのサポートを修正[リンク](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub のプレゼンスの改訂

いくつかの変更を行いました、[ソース コード リポジトリの GitHub](http://github.com/nuget/home)します。  Visual Studio の NuGet クライアント、Powershell コマンド、または、コマンド ラインで問題がある場合実行可能ファイルこれらの問題を記録してで進行状況を監視、[ホームの GitHub リポジトリの issue 一覧](http://github.com/nuget/home/issues)します。  ギャラリーでの問題を追跡します、[リポジトリの GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues)します。


## <a name="stay-tuned"></a>お見逃しなく

監視してください[ブログ](http://blog.nuget.org)の詳細の進行状況と NuGet 3.0 のお知らせください。