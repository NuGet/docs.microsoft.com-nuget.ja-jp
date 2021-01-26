---
title: NuGet 1.6 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.6 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777012"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 リリースノート

[NuGet 1.5 リリースノート](../release-notes/nuget-1.5.md)  | [NuGet 1.7 リリースノート](../release-notes/nuget-1.7.md)

NuGet 1.6 は、2011年12月13日にリリースされました。

## <a name="known-installation-issue"></a>インストールに関する既知の問題
VS 2010 SP1 を実行している場合は、以前のバージョンがインストールされている場合に NuGet をアップグレードしようとすると、インストールエラーが発生することがあります。

この回避策は、単純に NuGet をアンインストールし、VS 拡張機能ギャラリーからインストールすることです。  詳細については、「 <https://support.microsoft.com/kb/2581019> 」を参照してください。

注: Visual Studio で拡張機能をアンインストールできない場合 ([アンインストール] ボタンが無効になっている場合)、"管理者として実行" を使用して Visual Studio を再起動する必要が生じる可能性があります。

## <a name="features"></a>特徴

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>セマンティックバージョン管理とプレリリースパッケージのサポート
NuGet 1.6 では、セマンティックバージョン管理 (SemVer) のサポートが導入されています。 SemVer の使用方法の詳細については、 [バージョン管理に関するドキュメント](../create-packages/prerelease-packages.md)を参照してください。

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>パッケージをチェックインせずに NuGet を使用する (パッケージの復元)
NuGet 1.6 では、NuGet パッケージがソース管理に追加されないワークフローに対して、最初のクラスがサポートされるようになりましたが、必要でない場合はビルド時に復元されます。 詳細については、「 [パッケージをソース管理にコミットせずに NuGet を使用](../consume-packages/packages-and-source-control.md) する」を参照してください。

### <a name="item-templates-that-install-nuget-packages"></a>NuGet パッケージをインストールする項目テンプレート
Visual Studio プロジェクトテンプレートへのプレインストールされた NuGet パッケージをサポートする作業をビルドすると、NuGet 1.6 では Visual Studio 項目テンプレートのサポートも追加されます。 項目テンプレートには、テンプレートが呼び出されたときにインストールされる NuGet パッケージを関連付けることができます。

プロジェクト/項目テンプレートを変更して NuGet パッケージをインストールする方法の詳細については、「 [Visual Studio テンプレートのパッケージ](../visual-studio-extensibility/visual-studio-templates.md) 」を参照してください。

### <a name="support-for-disabling-package-sources"></a>パッケージソースの無効化のサポート
複数のパッケージソースが構成されている場合、NuGet では、パッケージとその依存関係のインストール中にパッケージごとにパッケージが検索されます。 何らかの理由で停止しているパッケージソースがあると、NuGet の速度が著しく低下する可能性があります。

NuGet 1.6 より前では、パッケージソースを削除することもできましたが、その後、に再度追加する必要がある場合の詳細について覚えておく必要があります。

NuGet 1.6 では、パッケージソースをオフにして無効にすることができますが、そのままにしておいてください。

![パッケージの無効化](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>バグの修正
NuGet 1.6 では、合計106個の作業項目が修正済みです。 これらのうちの95はバグとして分類され、そのうちの10は機能でした。

NuGet 1.6 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)を参照してください。
