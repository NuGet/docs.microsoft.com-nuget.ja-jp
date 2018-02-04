---
title: "NuGet 2.8.2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 2.8.2 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.8.2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f50bd1f0c981ef293a4d2ff425e0dffbdf58036c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 リリース ノート

[NuGet 2.8.1 リリース ノート](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 リリース ノート](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 は、22、2014 年 5 月にリリースされました。  このリリースには、のみ、変更するコマンド ライン nuget.exe NuGet.Server パッケージとその他の NuGet パッケージが含まれています。  更新された Visual Studio 拡張機能または WebMatrix 拡張機能、リリースは含まれませんでした。

## <a name="notable-updates"></a>重要な更新プログラム

代表的な更新プログラムは、コマンド ライン nuget.exe と NuGet.Server パッケージ (NuGet フィードの自己ホスト型) 用にしました。

### <a name="important-nugetexe-bug-fixes"></a>重要な nuget.exe バグ修正

1. [nuget.exe プッシュが失敗し、再試行を保持](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe プッシュに基本認証資格情報が正しく送信できません。](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe プッシュは一時的なリダイレクトに従うされません。](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>重要な NuGet.Server バグ修正

1. [間違った IsAbsoluteLatestVersion NuGet.Server によって返される値](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>更新パッケージ

Nuget.exe コマンドラインと NuGet.Server 修正は、NuGet パッケージの更新プログラムとして出荷されます。  その他のパッケージも 2.8.2 で更新が発生しました。

更新したパッケージの一覧を次に示します。

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (パッケージ、拡張子ではなく)

## <a name="all-changes"></a>すべての変更
リリースで解決される 10 の問題が発生しました。 作業の完全な一覧の項目で修正 NuGet 2.8.2、くださいビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)です。
