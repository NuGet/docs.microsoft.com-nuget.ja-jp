---
title: "NuGet 3.4.4 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.4.4 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 3.4.4 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fabc10ae5c8e0bd43581f85c7763eb23e9483aaf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
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
- Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)
- エラーを復元することがなく表示`project.json`または`packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- 必要なバージョンが異なる場合は、依存関係のバージョンを修正して[ \#559](https://github.com/NuGet/NuGet.Client/pull/559)