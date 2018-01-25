---
title: "NuGet 1.3 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.3 リリース ノートです。"
keywords: "NuGet 1.3 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 リリース ノート

[NuGet 1.2 リリース ノート](../release-notes/nuget-1.2.md) | [NuGet 1.4 のリリース ノート](../release-notes/nuget-1.4.md)

NuGet 1.3 は、2011 年 4 月 25 日にリリースされました。

## <a name="new-features"></a>新機能

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>シンボル サーバーの統合パッケージの作成を簡素化

チームと提携して NuGet チーム[SymbolSource.org](http://www.symbolsource.org/)をソースと PDB をパッケージと共に公開の非常に簡単な方法を提供します。 これにより、パッケージのコンシューマーは、デバッガーでは、パッケージのソースにステップ インできます。 詳細については、読み取り[の作成とシンボル パッケージを公開する](../create-packages/symbol-packages.md)ソースと NuGet パッケージを公開する簡単な方法です。 ライブ デモについてこの機能の深さで NuGet の一部として Mix11 話しも監視できます。 この機能は完全にビデオの 20 分間のマークで始まる説明します。

### <a name="open-packagepage-command"></a>`Open-PackagePage`コマンド

このコマンドでは、簡単に、パッケージ マネージャー コンソール内からパッケージのプロジェクト ページにアクセスできます。 ライセンスの URL と、不正使用のレポート ページ、パッケージを開くオプションも用意されています。
コマンドの構文です。

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru`オプションを使用して、指定された URL の値を返します。

次に例を示します。

    PM> Open-PackagePage Ninject

Ninject パッケージで指定されたプロジェクト URL をブラウザーで開きます。

    PM> Open-PackagePage Ninject -License

Ninject パッケージで指定されたライセンス URL をブラウザーで開きます。

    PM> Open-PackagePage Ninject -ReportAbuse

指定したパッケージの不正使用を報告に使用される現在のパッケージ ソースで URL をブラウザーで開きます。

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

ブラウザーで URL を開かずに、その変数 $url にライセンス URL を割り当てます。

### <a name="performance-improvements"></a>パフォーマンスの向上

NuGet 1.3 では、多数のパフォーマンスの向上について説明します。 NuGet 1.3 では、ユーザーごとのローカル キャッシュを含めることによって、同じバージョンのパッケージを複数回ダウンロードを回避できます。 キャッシュのアクセスし、パッケージ マネージャーの設定ダイアログを介したクリアできます。

![NuGet パッケージ キャッシュの設定で [オプション] ダイアログ](./media/nuget-options.png)

その他のパフォーマンスの向上には、HTTP 圧縮サポートを追加して、Visual Studio でパッケージのインストールの処理速度の向上が含まれます。

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio と nuget.exe 同じパッケージ ソースの一覧を使用します。

NuGet 1.3 の前に同じ場所に nuget.exe と NuGet Visual Studio アドインで使用されるパッケージ ソースの一覧を保持できませんでした。 今すぐ NuGet 1.3 は両方の場所で同じリストを使用します。 一覧に入っている`NuGet.Config`AppData フォルダーに格納されているとします。

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe 無視ファイルとフォルダーで始まる '.' 既定

NuGet Subversion と Mercurial のようなソース管理システムで機能するために、nuget.exe を無視ファイルとフォルダーの開始が、'.' 文字のパッケージを作成するときにします。 これは、次の 2 つの新しいフラグを使用してオーバーライドできます。

* __-NoDefaultExcludes__にこの設定を上書きし、すべてのファイルを含めるために使用します。
* __-除外__パターンの使用を除外するファイルとフォルダーは、他の追加に使用します。 たとえば、".bak 拡張子を持つすべてのファイルを除外するには

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_注: パターンは、既定では再帰的ではありません。_

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX プロジェクトと .NET マイクロ Framework のサポート

コミュニティの皆様に感謝 NuGet には、WiX プロジェクトの種類だけでなく、.NET マイクロ Framework のサポートが含まれています。

## <a name="bug-fixes"></a>バグ修正

バグの修正プログラムの一覧についてを参照してください、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。

## <a name="bug-fixes-worth-noting"></a>注目すべきバグ修正

* パッケージのソース ファイルには、両方の web サイトおよび Web アプリケーション プロジェクト機能します。
Web サイトのソース ファイルのコピー、`App_Code`フォルダー
