---
title: NuGet 2.8.2 リリース ノート
description: NuGet 2.8.2 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551149"
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 リリース ノート

[NuGet 2.8.1 のリリース ノート](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 リリース ノート](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 は、2014 年 5 月 22 日にリリースされました。  このリリースでは、nuget.exe コマンド ライン、NuGet.Server パッケージおよびその他の NuGet パッケージへの変更のみ含まれます。  更新された Visual Studio 拡張機能または WebMatrix 拡張機能をリリースは含まれませんでした。

## <a name="notable-updates"></a>注目すべき更新プログラム

最も注目すべき更新プログラムは、コマンドラインの nuget.exe および NuGet.Server パッケージ (NuGet フィードの自己ホスト型) 用にしました。

### <a name="important-nugetexe-bug-fixes"></a>Nuget.exe 重要なバグの修正

1. [nuget.exe プッシュは失敗し、再試行を保持](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe プッシュが基本認証資格情報を正しく送信できません。](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe プッシュは一時的なリダイレクトに従うしません](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>NuGet.Server の重要なバグを修正

1. [NuGet.Server によって返される IsAbsoluteLatestVersion の正しくない値](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>パッケージの更新

Nuget.exe コマンドラインと NuGet.Server 修正は、NuGet パッケージの更新プログラムとして出荷されます。  その他のパッケージも 2.8.2 で更新が発生しました。

更新されたパッケージの一覧を次に示します。

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (パッケージ、拡張機能ではありません)

## <a name="all-changes"></a>すべての変更
リリースで解決された 10 の問題が発生しました。 作業の完全な一覧については固定のアイテムの nuget 2.8.2、くださいビュー、[このリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)します。
