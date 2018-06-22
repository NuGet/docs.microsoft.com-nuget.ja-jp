---
title: NuGet 3.4.4 リリース ノート
description: NuGet 3.4.4 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820868"
---
# <a name="nuget-344-release-notes"></a>NuGet 3.4.4 リリース ノート

[NuGet 3.4.3 リリース ノート](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 ベータ リリース ノート](../release-notes/nuget-3.5-Beta.md)

このリリースの主な目的が 3.4.3 の品質の機能強化で Visual Studio 拡張機能をいくつかの修正 nuget.exe のバージョン。

VSIX と nuget.exe の両方をダウンロードする[ここ](https://dist.nuget.org/index.html)です。

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[すべての変更ログ](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[問題の一覧](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>変更

- パックの改良: の機能強化、シンボルを梱包にパッキング`project.json`詳細および[ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- 更新コマンド内のプロジェクトの検索エラーが発生したときに例外を表示 [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- パッケージの種類を入力から読み取る`.nuspec`と`project.json`パッキングと[ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- プロジェクトではなく NuGet.Shared を確認します。 [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- HTTP 応答のタイムアウトとしてプッシュ タイムアウトを使用して[ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- 将来の時刻にパッケージ ファイルには、使用される、時間がありません[ \#597。](https://github.com/NuGet/NuGet.Client/pull/597)
- 更新`NuGet.Core.dll`バージョンを XML の問題を解決する 2.12.0 [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- サポート./NuGet.CommandLine.XPlat v\<詳細度\>\<モード\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- エラーを復元することがなく表示`project.json`または`packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- 必要なバージョンが異なる場合は、依存関係のバージョンを修正して[ \#559](https://github.com/NuGet/NuGet.Client/pull/559)