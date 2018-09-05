---
title: NuGet 3.4.4 リリース ノート
description: NuGet 3.4.4 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547474"
---
# <a name="nuget-344-release-notes"></a>NuGet 3.4.4 リリース ノート

[NuGet 3.4.3 リリース ノート](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 のベータ リリース ノート](../release-notes/nuget-3.5-Beta.md)

このリリースの主な目的が 3.4.3 の品質の機能強化を Visual Studio 拡張機能のいくつかの修正と nuget.exe のバージョン。

VSIX と nuget.exe の両方をダウンロードする[ここ](https://dist.nuget.org/index.html)します。

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[完全な変更ログ](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[問題の一覧](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>変更

- パックの改良: の機能強化、シンボルのパックと梱包`project.json`詳細と[ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Update コマンド内のプロジェクトの検索エラーがある場合に表示される例外 [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- パッケージの種類を入力から読み取る`.nuspec`と`project.json`パックするときに[ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- プロジェクトではない NuGet.Shared を確認します。 [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- プッシュのタイムアウトを使用して、HTTP 応答のタイムアウトとして[ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- 将来の時間のパッケージ ファイルには、使用、時刻はありません[ \#597。](https://github.com/NuGet/NuGet.Client/pull/597)
- 更新`NuGet.Core.dll`2.12.0 XML 問題を解決するにはバージョン[ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- サポート./NuGet.CommandLine.XPlat v\<詳細度\>\<モード\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- エラーを復元することがなく表示`project.json`または`packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- 必要なバージョンが異なる場合に、依存関係のバージョンを修正[ \#559](https://github.com/NuGet/NuGet.Client/pull/559)