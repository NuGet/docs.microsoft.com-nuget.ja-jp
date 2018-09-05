---
title: NuGet 2.0 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.0 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547576"
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 リリース ノート

[NuGet 1.8 のリリース ノート](../release-notes/nuget-1.8.md) | [NuGet 2.1 リリース ノート](../release-notes/nuget-2.1.md)

NuGet 2.0 は、2012 年 6 月 19 日にリリースされました。

## <a name="known-installation-issue"></a>インストールの既知の問題
VS 2010 SP1 を実行している場合は、インストールされている以前のバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーが発生実行可能性があります。

回避策では、単に NuGet をアンインストールしてから、VS 拡張ギャラリーからインストールします。  参照してください[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)詳細については、または[VS 修正プログラムに直接移動](http://bit.ly/vsixcertfix)します。

注: Visual Studio ([アンインストール] ボタンは無効です) 拡張機能をアンインストールすることができず、しの場合必要があります「管理者として実行」を使用して Visual Studio を再起動するには

## <a name="package-restore-consent-is-now-active"></a>パッケージの復元の同意はアクティブになりました

この」の説明に従って[パッケージ復元の同意に投稿](http://blog.nuget.org/20120518/package-restore-and-consent.html)、NuGet 2.0 が同意するパッケージをダウンロードするパッケージの復元を有効にすることが必要になりました。 パッケージ マネージャーの構成 ダイアログまたは EnableNuGetPackageRestore 環境変数を使用して同意を入力したことを確認してください。

## <a name="group-dependencies-by-target-frameworks"></a>ターゲット フレームワークによってグループの依存関係

バージョン 2.0 以降、パッケージの依存関係が異なる場合は、ターゲット プロジェクトのフレームワーク プロファイルに基づいています。 これは、更新された`.nuspec`スキーマ。 `<dependencies>`要素が現在のセットを含めることができます`<group>`要素。 各グループは、0 個以上含まれています。`<dependency>`要素と`targetFramework`属性。 ターゲット フレームワークがターゲット プロジェクトのフレームワーク プロファイルと互換性のある場合は、グループ内のすべての依存関係は一緒にインストールされます。 例えば:

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

グループに含めることができますに注意してください**0**依存関係。 上記の例では、パッケージが Silverlight 3.0 を対象とするプロジェクトにインストールされている以降の場合の依存関係はインストールされません。 パッケージが .NET 4.0 を対象とするプロジェクトにインストールされている、またはそれ以降の場合は、2 つの依存関係、jQuery、および WebActivator がインストールされます。  これら 2 つのフレームワーク、またはその他のフレームワークの初期のバージョンを対象とするプロジェクトにパッケージがインストールされている、RouteMagic 1.1.0 がインストールされます。 グループ間の継承はありません。 プロジェクトのターゲット フレームワークと一致する場合、`targetFramework`属性のグループ、そのグループ内の依存関係のみがインストールされます。

パッケージは 2 つの形式のいずれかでパッケージの依存関係を指定することができます。 旧形式の単純なリストの`<dependency>`要素、またはグループ。 場合、`<group>`形式が使用される、2.0 より前のバージョンの NuGet にパッケージをインストールすることはできません。

2 つの形式の混在が許可されないことに注意してください。 たとえば、次のスニペットは**無効な**NuGet によって拒否されます。

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>ターゲット フレームワークによって、コンテンツ ファイルと PowerShell スクリプトをグループ化

アセンブリの参照だけでなくターゲット フレームワークによってはコンテンツ ファイルと PowerShell スクリプトのグループ化をもできます。 同じフォルダー構造がある、`lib`ターゲット フレームワークを指定するためのフォルダーを同じ方法で適用できる、`content`と`tools`フォルダー。 例えば:

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

**注**: ため`init.ps1`はソリューション レベルで実行、個々 のプロジェクトには依存しないを置く必要がありますの直下にある、`tools`フォルダー。 、フレームワーク固有のフォルダーに配置している場合は、これは無視されます。

また、NuGet 2.0 の新機能は、フレームワーク フォルダーができる*空*、する場合は、NuGet はないアセンブリ参照を追加、コンテンツ ファイルを追加または特定のフレームワークのバージョンの PowerShell スクリプトを実行します。 フォルダーの上の例では`content\net40`が空です。

## <a name="improved-tab-completion-performance"></a>強化されたタブ補完のパフォーマンス
NuGet パッケージ マネージャー コンソールの tab 補完機能が大幅にパフォーマンスを向上させる更新されました。 修正候補のドロップダウンが表示されるまで tab キーが押された時間の間には、はるかに少ない遅延があります。

## <a name="bug-fixes"></a>バグ修正
NuGet 2.0 には、パッケージ復元の同意とパフォーマンスを重視した多くのバグ修正が含まれています。
作業の完全な一覧の項目で修正された NuGet 2.0 では、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)します。
