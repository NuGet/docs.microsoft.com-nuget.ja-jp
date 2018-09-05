---
title: NuGet の 1.3 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.3 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551352"
---
# <a name="nuget-13-release-notes"></a>NuGet の 1.3 リリース ノート

[NuGet 1.2 リリース ノート](../release-notes/nuget-1.2.md) | [NuGet 1.4 のリリース ノート](../release-notes/nuget-1.4.md)

NuGet 1.3 は、2011 年 4 月 25 日にリリースされました。

## <a name="new-features"></a>新機能

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>シンボル サーバーの統合を簡素化されたパッケージの作成

開発者と提携して、NuGet チーム[SymbolSource.org](http://www.symbolsource.org/)と共に、パッケージの公開、ソースとの PDB の非常に簡単な方法を提供します。 これにより、デバッガーでパッケージのソースにステップ インするパッケージのコンシューマーができます。 詳細については、「[の作成とシンボル パッケージを公開](../create-packages/symbol-packages.md)ソースと NuGet パッケージを公開する簡単な方法です。 ライブ デモについてこの機能の深さで NuGet の一部として Mix11 講演を視聴することもできます。 ビデオの 20 分後に開始、この機能が完全に示します。

### <a name="open-packagepage-command"></a>`Open-PackagePage` コマンド

このコマンドでは、簡単にパッケージ マネージャー コンソール内からパッケージのプロジェクト ページを表示できます。 ライセンスの URL と、パッケージのレポートの不正使用のページを開くためのオプションも提供します。
コマンドの構文です。

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru`オプションを使用して、指定した URL の値を返します。

次に例を示します。

    PM> Open-PackagePage Ninject

Ninject パッケージで指定されたプロジェクトの URL をブラウザーが開きます。

    PM> Open-PackagePage Ninject -License

Ninject パッケージで指定されたライセンスの URL にブラウザーを開きます。

    PM> Open-PackagePage Ninject -ReportAbuse

指定したパッケージの不正使用を報告するために使用、現在のパッケージ ソース URL をブラウザーが開きます。

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

ブラウザーで URL を開くことがなく、変数 $url にライセンス URL を割り当てます。

### <a name="performance-improvements"></a>パフォーマンスの向上

NuGet 1.3 では、多数のパフォーマンスの機能強化について説明します。 NuGet 1.3 では、ユーザーごとのローカル キャッシュを含めることによって、同じバージョンのパッケージを複数回のダウンロードを回避できます。 キャッシュのアクセスおよびパッケージ マネージャー設定 ダイアログでクリアできます。

![NuGet のパッケージ キャッシュの設定のオプション ダイアログ ボックス](./media/nuget-options.png)

その他のパフォーマンスの向上には、HTTP 圧縮のサポートを追加して、Visual Studio 内でパッケージのインストールの処理速度の向上が含まれます。

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio と nuget.exe 同じパッケージ ソースのリストを使用します。

NuGet 1.3 では、前に、nuget.exe および NuGet Visual Studio アドインで使用されるパッケージ ソースの一覧は、同じ場所に保持できませんでした。 今すぐ、NuGet 1.3 は、両方の場所で同じリストを使用します。 一覧が格納されている`NuGet.Config`AppData フォルダーに格納されているとします。

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe を無視ファイルとフォルダーで始まる '.' 既定

フォルダーとファイルで始まる NuGet Subversion と Mercurial のようなソース管理システムでうまく動作するために、nuget.exe を無視します '.' パッケージを作成するときに文字します。 これは、2 つの新しいフラグを使用してオーバーライドできます。

* __-NoDefaultExcludes__この設定を上書きし、すべてのファイルを含めるために使用します。
* __-除外__パターンを使用してを除外するファイルとフォルダーは、他の追加に使用されます。 たとえば、".bak"ファイル拡張子を持つすべてのファイルを除外するには

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_注: パターンは、既定では再帰ではありません。_

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX プロジェクトと .NET Micro Framework のサポート

コミュニティへの投稿に協力してくれた NuGet には、WiX プロジェクトの種類に加えて、.NET Micro Framework のサポートが含まれています。

## <a name="bug-fixes"></a>バグ修正

バグの修正の完全な一覧を参照してください、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)します。

## <a name="bug-fixes-worth-noting"></a>注目すべきバグの修正

* パッケージ ソース ファイルでは、両方の web サイトでと Web アプリケーション プロジェクトで作業します。
Web サイトのソース ファイルのコピー、`App_Code`フォルダー
