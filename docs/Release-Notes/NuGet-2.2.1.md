---
title: "NuGet 2.2.1 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 2.2.1 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.2.1 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c3e912dcabeb3a26c880b42560a3cec6f7bf2db9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 リリース ノート

[NuGet 2.2 リリース ノート](../release-notes/nuget-2.2.md) | [NuGet 2.5 リリース ノート](../release-notes/nuget-2.5.md)

NuGet 2.2.1 は、2013 年 2 月 15 日にリリースされました。  VS 拡張機能のバージョン番号は、2.2.40116.9051 です。

## <a name="localization-refresh"></a>ローカリゼーションの更新
NuGet は Visual Studio 2012 の一部として提供されている、ときに、英語 + 13 の他の言語に完全にローカライズされます。  それ以降は、NuGet 2.1、2.2 が付属しているが、ローカリゼーションが更新されていません。  NuGet 2.2.1 リリースでは、ローカリゼーションを更新します。

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio のテンプレートが複数のプレインストールされたパッケージ リポジトリをサポートします。
Visual Studio のテンプレートを作成する場合は、NuGet を使用できます[パッケージをプレインストール](../visual-studio-extensibility/visual-studio-templates.md)テンプレートの一部として。  この機能が制限をこれまでは、同じソースから入手するすべてのパッケージに必要なです。  ただし、NuGet 2.2.1 では、(テンプレートを VSIX や、レジストリで定義されているディスク上のフォルダー) 内の複数のリポジトリからインストールされているパッケージを設定できます。

この機能の主なシナリオは、カスタムの ASP.NET プロジェクト テンプレートです。  組み込みの ASP.NET テンプレートは、ローカル ディスクからのパッケージの抽出、プレインストールされたパッケージを使用します。  ASP.NET がインストールされている既存のパッケージを使用するカスタム ASP.NET プロジェクト テンプレートを作成するようになりましたが、テンプレートに追加の NuGet パッケージを追加できます。

## <a name="bug-fixes"></a>バグ修正
NuGet 2.2.1 には、対象となる、いくつかのバグ修正が含まれています。 作業の一覧の項目で修正 NuGet 2.2.1、してください。 ビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。


## <a name="known-issues"></a>既知の問題

プレインストールされたパッケージのすべてのリポジトリが、同じ値を使用する必要があります ASP.NET プロジェクト テンプレートを拡張する場合、`isPreunzipped`属性。
