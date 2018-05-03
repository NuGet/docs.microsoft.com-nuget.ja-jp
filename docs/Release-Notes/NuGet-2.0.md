---
title: NuGet 2.0 のリリース ノート
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.0 のリリース ノートします。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0e637a953d9d5d10394857a352be96a7f68dc4e8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 のリリース ノート

[NuGet 1.8 リリース ノート](../release-notes/nuget-1.8.md) | [NuGet 2.1 リリース ノート](../release-notes/nuget-2.1.md)

NuGet 2.0 は、2012 年 6 月 19 日にリリースされました。

## <a name="known-installation-issue"></a>インストールの既知の問題
VS 2010 SP1 を実行している場合、インストールされている古いバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーに発生する可能性があります。

回避策では、NuGet をシンプルにアンインストールし、VS 拡張機能ギャラリーからインストールします。  参照してください[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)詳細については、または[VS 修正プログラムに直接進んで](http://bit.ly/vsixcertfix)です。

注意: Visual Studio には、(削除 ボタンは無効になっている) 拡張機能をアンインストールすることを許可しません、可能性の高い場合"管理者として実行 を使用して Visual Studio を再起動するには

## <a name="package-restore-consent-is-now-active"></a>パッケージ復元同意はアクティブになりました

この」の説明に従って[パッケージ復元同意に投稿](http://blog.nuget.org/20120518/package-restore-and-consent.html)、NuGet 2.0 は、同意がオンラインでパッケージをダウンロードするパッケージの復元を有効に指定する必要がありますようになりました。 パッケージ マネージャーの構成 ダイアログまたは EnableNuGetPackageRestore 環境変数のどちらか経由での同意を入力したことを確認してください。

## <a name="group-dependencies-by-target-frameworks"></a>ターゲット フレームワークでグループの依存関係

バージョン 2.0 以降では、パッケージの依存関係が異なる場合は、ターゲット プロジェクトのフレームワークのプロファイルに基づいています。 これは、更新された`.nuspec`スキーマです。 `<dependencies>`要素のセットを含めるようになりましたことができます`<group>`要素。 各グループは、0 個以上含まれています。`<dependency>`要素および`targetFramework`属性。 ターゲット フレームワークをプロジェクトのターゲット フレームワーク プロファイルと互換性がある場合、グループ内のすべての依存関係が一緒にインストールされます。 例えば:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

グループを含めることができる注**0**の依存関係。 上記の例では、パッケージが Silverlight 3.0 を対象とするプロジェクトにインストールされているか、後で、場合の依存関係はインストールされません。 パッケージがインストール先を .NET 4.0 を対象とするプロジェクトまたはそれ以降の場合は、次の 2 つの依存関係、jQuery、および WebActivator がインストールされます。  パッケージが、以前のバージョンのこれら 2 つのフレームワークまたはその他の任意のフレームワークを対象とするプロジェクトにインストールされている場合は、RouteMagic 1.1.0 がインストールされます。 グループ間の継承はありません。 プロジェクトのターゲット フレームワークと一致する場合、`targetFramework`グループ、そのグループ内の依存関係のみの属性はインストールされます。

パッケージは、2 つの形式のいずれかでパッケージの依存関係を指定できます: 旧形式の単純なリストの`<dependency>`要素、またはグループ。 場合、`<group>`形式が使用される、2.0 より前のバージョンの NuGet パッケージをインストールすることはできません。

2 つの形式を混在させるを使用できないことに注意してください。 たとえば、次のスニペットは**無効な**とは、NuGet によって拒否されます。

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>ターゲット フレームワークでコンテンツ ファイルおよび PowerShell スクリプトをグループ化

アセンブリの参照に加えてターゲット フレームワークではコンテンツ ファイルおよび PowerShell スクリプトのグループ化をもできます。 同じフォルダー構造がで見つかった、`lib`ターゲット フレームワークを指定するためのフォルダーに同じ方法で適用できます、`content`と`tools`フォルダーです。 例えば:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**注**: ため`init.ps1`ソリューション レベルで実行され、は、個々 のプロジェクトには依存しない、配置しなければなりません直下にある、`tools`フォルダーです。 フレームワーク固有のフォルダー内で、配置している場合は無視されます。

フレームワーク フォルダーがあることを NuGet 2.0 の新機能はまた、*空*、この場合は、NuGet はいないアセンブリ参照を追加、コンテンツ ファイルを追加または特定のフレームワークのバージョンの PowerShell スクリプトを実行します。 フォルダー上の例で`content\net40`が空です。

## <a name="improved-tab-completion-performance"></a>強化されたタブ補完のパフォーマンス
NuGet パッケージ マネージャー コンソールの tab 補完機能が大幅にパフォーマンスを向上させる更新されました。 修正候補のドロップダウン リストが表示されるまで tab キーが押された時間の間には、はるかに少ない遅延があります。

## <a name="bug-fixes"></a>バグ修正
NuGet 2.0 には、パッケージの復元の同意画面およびパフォーマンスに重点を置いて、多くのバグ修正が含まれています。
作業の完全な一覧の項目で修正 NuGet 2.0 では、くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)です。
