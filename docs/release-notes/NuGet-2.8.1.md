---
title: NuGet 2.8.1 のリリース ノート
description: NuGet 2.8.1 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545240"
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 のリリース ノート

[NuGet 2.8 のリリース ノート](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 リリース ノート](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 は、2014 年 4 月 2 日にリリースされました。

## <a name="notable-features-in-the-release"></a>リリースで注目すべき機能

### <a name="support-for-windows-phone-81-projects"></a>Windows Phone 8.1 プロジェクトのサポート
このリリースでは、Windows Phone 8.1 をターゲット プロジェクトに使用できる次の新しいターゲット フレームワーク モニカーできるようになりました。

* WindowsPhone81/(Windows Phone の Silverlight ベースのプロジェクト) に対して WP81
* WindowsPhoneApp81/WPA81 (の WinRT ベースの Windows Phone アプリ プロジェクトの場合)

### <a name="update-of-the-nuget-webmatrix-extension"></a>WebMatrix の NuGet 拡張機能の更新
このリリースで更新するために WebMatrix に、NuGet クライアント[NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 し、XDT 変換などの機能が使用されます。 2.6.1 さらに、中核となる更新プログラムによりより新しいバージョンを含む NuGet パッケージをインストールする WebMatrix クライアント、`.nuspec`スキーマで、ASP.NET の NuGet パッケージが含まれています。

WebMatrix 拡張機能の更新プログラムの詳細については、これらの参照してください[リリース ノート](../release-notes/nuget-2.6.1-for-WebMatrix.md)します。

### <a name="bug-fixes"></a>バグ修正
これらの機能に加えて NuGet のこのリリースには、その他のバグ修正が含まれています。 リリースで解決された問題の合計 16 が発生しました。 作業の完全な一覧については固定のアイテムの nuget 2.8.1、くださいビュー、[このリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)します。

### <a name="reshipping-with-visual-studio-14-ctp"></a>Visual studio「14」CTP を reshipping
3 番目の 2014 年 6 月にリリースされた Visual Studio「14」ctp では、NuGet 2.8.1 は、ボックスに付属しています。 ですが、サポート機能には、同等がそのまま他 2.8.1 で VSIXes for Visual Studio 2013 など。
