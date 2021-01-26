---
title: NuGet 2.2.1 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.2.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776801"
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 リリースノート

[NuGet 2.2 リリースノート](../release-notes/nuget-2.2.md)  | [NuGet 2.5 リリースノート](../release-notes/nuget-2.5.md)

NuGet 2.2.1 は2013年2月15日にリリースされました。  VS 拡張機能のバージョン番号は2.2.40116.9051 です。

## <a name="localization-refresh"></a>ローカリゼーションの更新
NuGet が Visual Studio 2012 の一部として出荷された場合、英語 + 13 の他の言語に完全にローカライズされています。  その後、NuGet 2.1 および2.2 は出荷されましたが、ローカライズは更新されていません。  NuGet 2.2.1 リリースでは、ローカライズを更新しています。

NuGet の UI と PowerShell コンソールは、次の言語にローカライズされています。

1. 簡体中国語
1. 繁体中国語
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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio テンプレートでは、複数のプレインストール済みパッケージリポジトリがサポート
Visual Studio テンプレートを作成する場合は、NuGet を使用して、テンプレートの一部として [パッケージをプレインストール](../visual-studio-extensibility/visual-studio-templates.md) できます。  これまで、この機能では、すべてのパッケージが同じソースから取得される必要があるという制限がありました。  ただし、NuGet 2.2.1 を使用すると、複数のリポジトリ (テンプレート内、VSIX 内、またはレジストリで定義されているディスク上のフォルダー内) からパッケージをインストールできます。

この機能の主なシナリオは、カスタム ASP.NET プロジェクトテンプレートです。  組み込みの ASP.NET テンプレートでは、プレインストールされたパッケージを使用して、ローカルディスクからパッケージをプルします。  ASP.NET によってインストールされた既存のパッケージを使用するカスタム ASP.NET プロジェクトテンプレートを作成できるようになりましたが、テンプレートに追加の NuGet パッケージを追加できます。

## <a name="bug-fixes"></a>バグの修正
NuGet 2.2.1 には、いくつかの対象となるバグ修正が含まれています。 NuGet 2.2.1 で修正された作業項目の一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を参照してください。


## <a name="known-issues"></a>既知の問題

ASP.NET プロジェクトテンプレートを拡張する場合は、インストールされているすべてのパッケージリポジトリで属性に同じ値を使用する必要があり `isPreunzipped` ます。
