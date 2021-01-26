---
title: NuGet 2.8.1 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.8.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776768"
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 のリリースノート

[NuGet 2.8 リリースノート](../release-notes/nuget-2.8.md)  | [NuGet 2.8.2 のリリースノート](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 は2014年4月2日にリリースされました。

## <a name="notable-features-in-the-release"></a>リリースの注目すべき機能

### <a name="support-for-windows-phone-81-projects"></a>Windows Phone 8.1 プロジェクトのサポート
このリリースでは、Windows Phone 8.1 プロジェクトのターゲットとして使用できる次の新しいターゲットフレームワークモニカーがサポートされるようになりました。

* WindowsPhone81/WP81 (Silverlight ベースの Windows Phone プロジェクトの場合)
* WindowsPhoneApp81/WPA81 (WinRT ベースの Windows Phone アプリプロジェクト用)

### <a name="update-of-the-nuget-webmatrix-extension"></a>NuGet WebMatrix 拡張機能の更新
このリリースでは、WebMatrix の NuGet クライアントを [2.6.1 に](https://www.nuget.org/packages/Nuget.Core/2.6.1) 更新し、xdt 変換などの it 機能を利用できます。 さらに重要な点として、2.6.1 core 更新プログラムを使用すると、WebMatrix クライアントは、ASP.NET NuGet パッケージを含む、より新しいバージョンのスキーマを含む NuGet パッケージをインストールでき `.nuspec` ます。

WebMatrix 拡張機能の更新の詳細については、これらの特定の [リリースノート](../release-notes/nuget-2.6.1-for-WebMatrix.md)を参照してください。

### <a name="bug-fixes"></a>バグの修正
これらの機能に加えて、この NuGet のリリースには他のバグ修正が含まれています。 リリースで解決された問題の合計数は16個でした。 NuGet 2.8.1 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)を参照してください。

### <a name="reshipping-with-visual-studio-14-ctp"></a>Visual Studio "14" CTP での再配布
2014年6月3日にリリースされた Visual Studio "14" CTP では、このボックスに NuGet 2.8.1 が付属しています。 サポートされている機能は、Visual Studio 2013 のような他の 2.8.1 VSIXes と同等のものです。
