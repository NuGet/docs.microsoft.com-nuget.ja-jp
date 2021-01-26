---
title: NuGet 3.4.4 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.4.4 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780228"
---
# <a name="nuget-344-release-notes"></a>NuGet 3.4.4 のリリースノート

[NuGet 3.4.3 のリリースノート](../release-notes/nuget-3.4.3.md)  | [NuGet 3.5-ベータリリースノート](../release-notes/nuget-3.5-Beta.md)

このリリースの主な目的は、Visual Studio 拡張機能に対していくつかの修正を加えて、nuget.exe の3.4.3 バージョンの品質を向上させることでした。

VSIX と nuget.exe の両方を [ここで](https://dist.nuget.org/index.html)ダウンロードできます。

## <a name="344-rtm-2016-05-19"></a>[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[完全な Changelog](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[問題の一覧](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>[変更点]

- パックの改善: シンボルのパッキングの改善、606でのパッキング、 `project.json` およびその他の[ \# ](https://github.com/NuGet/NuGet.Client/pull/606)
- Update コマンドでプロジェクトの検索エラーが発生したときに例外を表示する [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605
- 入力からのパッケージの種類の読み取り `.nuspec` と、 `project.json` [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)のパッキング
- NuGet を作成します。共有はプロジェクトではありません。 [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- HTTP 応答タイムアウト[ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)としてプッシュタイムアウトを使用する
- 将来の時刻を含むパッケージファイルの使用時間は[ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- `NuGet.Core.dll`XML の問題を修正するためにバージョンを2.12.0 に更新しています[ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)
- サポート./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- `project.json`または `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)を使用せずに復元エラーを表示する
- 必要なバージョンが異なる場合の依存関係バージョンの修正[ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)