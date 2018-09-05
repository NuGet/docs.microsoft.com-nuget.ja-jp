---
title: NuGet 2.2.1 リリース ノート
description: NuGet 2.2.1 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550699"
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 リリース ノート

[NuGet 2.2 リリース ノート](../release-notes/nuget-2.2.md) | [NuGet 2.5 リリース ノート](../release-notes/nuget-2.5.md)

NuGet 2.2.1 は、2013 年 2 月 15 日にリリースされました。  VS 拡張機能のバージョン番号は、2.2.40116.9051 です。

## <a name="localization-refresh"></a>ローカリゼーションの更新
NuGet が Visual Studio 2012 の一部として出荷されたときに、英語とその他の 13 か国語にローカライズが完全に。  その後、NuGet 2.1、2.2 の配布が始まりましたが、ローカリゼーションが更新されていません。  NuGet 2.2.1 リリースでは、ローカリゼーションを更新します。

NuGet の UI と PowerShell コンソールは、次の言語にローカライズされます。

1. 中国語 (簡体字、中国)
1. では [
1. チェコ語
1. 英語
1. フランス語
1. ドイツ語
1. イタリア語
1. 日本語
1. 韓国語
1. ポーランド語
1. ポルトガル語 (ブラジル)
1. ロシア語
1. スペイン語
1. トルコ語

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio テンプレートは、複数のパッケージがプレインストールされているリポジトリをサポートします。
Visual Studio テンプレートを作成する場合は、NuGet を使用できます[パッケージがプレインストール](../visual-studio-extensibility/visual-studio-templates.md)テンプレートの一部として。  この機能が制限をこれまで、同じソースからのものに必要であるすべてのパッケージ。  ただし、NuGet 2.2.1 では、(テンプレート、VSIX、またはレジストリで定義されているディスク上のフォルダー) 内の複数のリポジトリからインストールされているパッケージができます。

この機能の主なシナリオは、カスタムの ASP.NET プロジェクト テンプレートです。  組み込みの ASP.NET テンプレートでは、ローカル ディスクからのパッケージを引き出して、プレインストールされているパッケージを使用します。  ASP.NET がインストールされている既存のパッケージを使用するカスタムの ASP.NET プロジェクト テンプレートを作成するようになりましたがテンプレートに追加の NuGet パッケージを追加できます。

## <a name="bug-fixes"></a>バグ修正
NuGet 2.2.1 では、対象となるいくつかのバグ修正が含まれています。 作業の一覧の項目で修正された NuGet 2.2.1 くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)します。


## <a name="known-issues"></a>既知の問題

プレインストールされているパッケージのすべてのリポジトリが、同じ値を使用する必要があります ASP.NET プロジェクト テンプレートを拡張する場合、`isPreunzipped`属性。
