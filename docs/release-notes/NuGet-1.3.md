---
title: NuGet 1.3 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.3 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777125"
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 リリースノート

[NuGet 1.2 リリースノート](../release-notes/nuget-1.2.md)  | [NuGet 1.4 リリースノート](../release-notes/nuget-1.4.md)

NuGet 1.3 は、2011年4月25日にリリースされました。

## <a name="new-features"></a>新機能

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>シンボルサーバー統合による合理化されるパッケージの作成

NuGet チームは、 [SymbolSource.org](http://www.symbolsource.org/) の担当者と提携して、パッケージと共にソースと PDB を簡単に公開する方法を提供しています。 これにより、パッケージのコンシューマーは、デバッガーでパッケージのソースにステップインできます。 詳細については、「 [シンボルパッケージの作成と発行](../create-packages/symbol-packages.md) 」を参照してください。ソースと共に NuGet パッケージを発行する簡単な方法です。 また、この機能のライブデモについては、Mix11 で詳しく説明されている NuGet の一部としてもご覧いただけます。 この機能は、ビデオの20分のマークから完全に示されています。

### <a name="open-packagepage-command"></a>`Open-PackagePage` コマンド

このコマンドを使用すると、パッケージマネージャーコンソール内からパッケージのプロジェクトページを簡単に取得できます。 また、パッケージのライセンス URL とレポートの不正使用ページを開くためのオプションも用意されています。
コマンドの構文は次のとおりです。

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

`-PassThru`オプションは、指定された URL の値を返すために使用されます。

例 :

```
PM> Open-PackagePage Ninject
```

Ninject パッケージに指定されているプロジェクト URL をブラウザーで開きます。

```
PM> Open-PackagePage Ninject -License
```

Ninject パッケージに指定されているライセンス URL をブラウザーで開きます。

```
PM> Open-PackagePage Ninject -ReportAbuse
```

指定したパッケージの誤用を報告するために使用する、現在のパッケージソースの URL をブラウザーで開きます。

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

ブラウザーで URL を開かずに、$url の変数にライセンス URL を割り当てます。

### <a name="performance-improvements"></a>パフォーマンスの強化

NuGet 1.3 では、パフォーマンスが大幅に向上しています。 NuGet 1.3 では、ローカルのユーザーごとのキャッシュを含めることにより、同じバージョンのパッケージが複数回ダウンロードされることを回避しています。 キャッシュには、[パッケージマネージャーの設定] ダイアログを使用してアクセスしたり、消去したりできます。

![パッケージキャッシュ設定を含む NuGet オプションダイアログ](./media/nuget-options.png)

その他のパフォーマンスの向上には、HTTP 圧縮のサポートの追加と、Visual Studio 内でのパッケージのインストール速度の向上が含まれます。

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio と nuget.exe は、同じパッケージソースの一覧を使用します。

NuGet 1.3 より前では、nuget.exe によって使用されているパッケージソースの一覧と NuGet Visual Studio Add-In が同じ場所に格納されていませんでした。 NuGet 1.3 では、両方の場所で同じリストが使用されるようになりました。 リストはに格納され、 `NuGet.Config` AppData フォルダーに格納されます。

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>既定では、'. ' で始まるファイルとフォルダーは無視され nuget.exe

NuGet を Subversion や Mercurial などのソース管理システムで適切に機能させるために、nuget.exe では、パッケージの作成時に '. ' 文字で始まるフォルダーやファイルは無視されます。 これは、2つの新しいフラグを使用してオーバーライドできます。

* __-Nodefaultexcludes__ は、この設定を上書きし、すべてのファイルを含めるために使用されます。
* __-Exclude__ は、パターンを使用して除外する他のファイルやフォルダーを追加するために使用されます。 たとえば、".bak" ファイル拡張子を持つすべてのファイルを除外するには、次のようにします。

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_注: 既定では、パターンは再帰的ではありません。_

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX プロジェクトと .NET Micro Framework のサポート

コミュニティへの投稿により、NuGet には、WiX プロジェクトの種類と .NET Micro Framework のサポートが含まれています。

## <a name="bug-fixes"></a>バグの修正

バグ修正の完全な一覧については、 [このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)をご覧ください。

## <a name="bug-fixes-worth-noting"></a>バグの修正に値する注意点

* ソースファイルを含むパッケージは、Web サイトと Web アプリケーションプロジェクトの両方で動作します。
Web サイトの場合、ソースファイルはフォルダーにコピーされます。 `App_Code`
