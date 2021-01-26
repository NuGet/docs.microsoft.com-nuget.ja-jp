---
title: NuGet 2.8.2 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.8.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780373"
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 のリリースノート

[NuGet 2.8.1 のリリースノート](../release-notes/nuget-2.8.1.md)  | [NuGet 2.8.3 のリリースノート](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 は2014年5月22日にリリースされました。  このリリースには、nuget.exe コマンドライン、Nuget.exe パッケージ、およびその他の NuGet パッケージに対する変更のみが含まれていました。  リリースには、更新された Visual Studio 拡張機能または WebMatrix 拡張機能が含まれていませんでした。

## <a name="notable-updates"></a>注目に値する更新

最も注目すべき更新プログラムは、nuget.exe コマンドラインと、(自己ホスト型 NuGet フィード用の) サーバーパッケージに含まれていました。

### <a name="important-nugetexe-bug-fixes"></a>重要な nuget.exe バグ修正

1. [nuget.exe プッシュが失敗して再試行を続ける](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe プッシュでは基本的な認証資格情報が正しく送信されない](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe Push が一時的なリダイレクトに従わない](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>重要な NuGet. サーバーのバグ修正

1. [NuGet によって返された IsAbsoluteLatestVersion の値が間違っています](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>更新されたパッケージ

nuget.exe のコマンドラインと NuGet の修正プログラムは、NuGet パッケージの更新プログラムとして出荷されます。  他のパッケージも2.8.2 で更新されています。

更新されたパッケージの一覧を次に示します。

1. [NuGet. コア](https://www.nuget.org/packages/NuGet.Core/)
1. [Nuget.exe コマンドライン](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet。ビルド](https://www.nuget.org/packages/NuGet.Build/)
1. [VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (拡張子ではなくパッケージ)

## <a name="all-changes"></a>すべての変更
このリリースでは、10件の問題が解決されました。 NuGet 2.8.2 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)を参照してください。
