---
title: "NuGet 2.8.1 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: eebbbae4-fc6a-4c05-9102-4ec66b4c64a4
description: "NuGet 2.8.1 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.8.1 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac33369644d312591bfe8c06540935b2c6063c5d
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 リリース ノート

[NuGet 2.8 リリース ノート](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 リリース ノート](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 は、2014 年 4 月 2 日にリリースされました。

## <a name="notable-features-in-the-release"></a>リリースで注目に値する機能

### <a name="support-for-windows-phone-81-projects"></a>Windows Phone 8.1 プロジェクトのサポート
このリリースでは、Windows Phone 8.1 を対象のプロジェクトに使用できる次の新しいターゲット フレームワーク モニカーできるようになりました。

* WindowsPhone81/WP81 (Silverlight ベースの Windows Phone プロジェクトに対して)
* WindowsPhoneApp81/WPA81 (WinRT ベースの Windows Phone アプリ プロジェクトに対して)

### <a name="update-of-the-nuget-webmatrix-extension"></a>NuGet WebMatrix 拡張機能の更新
このリリースを更新するために WebMatrix で見つかった NuGet クライアント[NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 され XDT 変換などの機能です。 2.6.1 さらに、コア更新により、WebMatrix クライアントを含むより新しいバージョンの NuGet パッケージをインストールする、`.nuspec`スキーマがあり、ASP.NET の NuGet パッケージが含まれています。

WebMatrix 拡張機能の更新に関する詳細についてを参照してください特化[リリース ノート](../release-notes/nuget-2.6.1-for-WebMatrix.md)です。

### <a name="bug-fixes"></a>バグ修正
これらの機能だけでなく NuGet のこのリリースには、その他のバグ修正が含まれています。 リリースで解決される 16 の合計の問題が発生しました。 作業の完全な一覧の項目で修正 NuGet 2.8.1、くださいビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)です。

### <a name="reshipping-with-visual-studio-14-ctp"></a>With Visual Studio「14」CTP を reshipping
第 3 の 2014 年 6 月にリリースされた Visual Studio「14」ctp では、NuGet 2.8.1 はボックスに付属しています。 Par でままですが、サポートとその他の 2.8.1 VSIXes など Visual Studio 2013 用の 1 つです。
