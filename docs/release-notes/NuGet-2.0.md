---
title: NuGet 2.0 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.0 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776989"
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 リリースノート

[NuGet 1.8 リリースノート](../release-notes/nuget-1.8.md)  | [NuGet 2.1 リリースノート](../release-notes/nuget-2.1.md)

NuGet 2.0 は、2012年6月19日にリリースされました。

## <a name="known-installation-issue"></a>インストールに関する既知の問題
VS 2010 SP1 を実行している場合は、以前のバージョンがインストールされている場合に NuGet をアップグレードしようとすると、インストールエラーが発生することがあります。

この回避策は、単純に NuGet をアンインストールし、VS 拡張機能ギャラリーからインストールすることです。  詳細については、「」を参照 <https://support.microsoft.com/kb/2581019> するか、 [VS 修正プログラムに直接アクセス](http://bit.ly/vsixcertfix)してください。

注: Visual Studio で拡張機能をアンインストールできない場合 ([アンインストール] ボタンが無効になっている場合)、"管理者として実行" を使用して Visual Studio を再起動する必要が生じる可能性があります。

## <a name="package-restore-consent-is-now-active"></a>パッケージの復元の同意がアクティブになりました

パッケージの復元 [の同意に関するこの記事](http://blog.nuget.org/20120518/package-restore-and-consent.html)で説明されているように、NuGet 2.0 では、パッケージの復元をオンラインにしてパッケージをダウンロードできるようにするための同意が必要になります。 パッケージマネージャーの構成ダイアログまたは EnableNuGetPackageRestore 環境変数のいずれかを使用して同意したことを確認してください。

## <a name="group-dependencies-by-target-frameworks"></a>ターゲットフレームワークによる依存関係のグループ化

バージョン2.0 以降では、パッケージの依存関係はターゲットプロジェクトのフレームワークプロファイルによって異なる場合があります。 これは、更新されたスキーマを使用して実現され `.nuspec` ます。 `<dependencies>`要素に要素のセットを含めることができるようになりました `<group>` 。 各グループには、0個以上 `<dependency>` の要素と1つの属性が含まれてい `targetFramework` ます。 ターゲットフレームワークがターゲットプロジェクトフレームワークプロファイルと互換性がある場合、グループ内のすべての依存関係が一緒にインストールされます。 次に例を示します。

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

グループには、 **0 個** の依存関係を含めることができます。 上記の例では、パッケージが Silverlight 3.0 以降を対象とするプロジェクトにインストールされている場合、依存関係はインストールされません。 パッケージが .NET 4.0 以降を対象とするプロジェクトにインストールされている場合は、jQuery と WebActivator の2つの依存関係がインストールされます。  パッケージが、これら2つのフレームワークの初期バージョンまたはその他のフレームワークを対象とするプロジェクトにインストールされている場合は、RouteMagic 1.1.0 がインストールされます。 グループ間に継承はありません。 プロジェクトのターゲットフレームワークがグループの属性と一致する場合 `targetFramework` 、そのグループ内の依存関係のみがインストールされます。

パッケージは、次の2つの形式のいずれかでパッケージの依存関係を指定できます。1つは、要素の単純なリストの古い形式です。 `<dependency>` 形式が使用されている場合は、 `<group>` 2.0 より前のバージョンの NuGet にパッケージをインストールすることはできません。

2つの形式を混在させることはできません。 たとえば、次のスニペットは **無効** であり、NuGet によって拒否されます。

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>ターゲットフレームワークによるコンテンツファイルと PowerShell スクリプトのグループ化

アセンブリ参照だけでなく、コンテンツファイルと PowerShell スクリプトをターゲットフレームワーク別にグループ化することもできます。 ターゲットフレームワークを指定するためにフォルダーで見つかったものと同じフォルダー構造を、フォルダー `lib` とフォルダーに対して同じ方法で適用できるようになりました `content` `tools` 。 次に例を示します。

```
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
```

**注**: `init.ps1` はソリューションレベルで実行され、個々のプロジェクトに依存しないため、フォルダーの直下に配置する必要があり `tools` ます。 フレームワーク固有のフォルダー内に配置されている場合は無視されます。

また、NuGet 2.0 の新機能として、フレームワークフォルダーを *空* にすることができます。この場合、nuget では、アセンブリ参照の追加、コンテンツファイルの追加、特定のフレームワークバージョンの PowerShell スクリプトの実行は行われません。 上記の例では、フォルダー `content\net40` は空です。

## <a name="improved-tab-completion-performance"></a>タブ補完のパフォーマンスの向上
NuGet パッケージマネージャーコンソールのタブ補完機能が更新され、パフォーマンスが大幅に向上しました。 [候補] ドロップダウンが表示されるまで、tab キーが押されるまでにかかる時間が大幅に短縮されます。

## <a name="bug-fixes"></a>バグの修正
NuGet 2.0 には、パッケージの復元の同意とパフォーマンスを重視した多くのバグ修正が含まれています。
NuGet 2.0 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)を参照してください。
