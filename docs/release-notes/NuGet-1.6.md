---
title: NuGet 1.6 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.6 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549013"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 リリース ノート

[NuGet 1.5 のリリース ノート](../release-notes/nuget-1.5.md) | [NuGet 1.7 のリリース ノート](../release-notes/nuget-1.7.md)

NuGet 1.6 は、2011 年 12 月 13 日にリリースされました。

## <a name="known-installation-issue"></a>インストールの既知の問題
VS 2010 SP1 を実行している場合は、インストールされている以前のバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーが発生実行可能性があります。

回避策では、単に NuGet をアンインストールしてから、VS 拡張ギャラリーからインストールします。  詳細については、「[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)」を参照してください。

注: Visual Studio ([アンインストール] ボタンは無効です) 拡張機能をアンインストールすることができず、しの場合必要があります「管理者として実行」を使用して Visual Studio を再起動するには

## <a name="features"></a>フィーチャー

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>セマンティック バージョン管理とプレリリース パッケージのサポート
NuGet 1.6 では、セマンティック バージョン管理 (SemVer) のサポートについて説明します。 SemVer を使用する方法の詳細については、読み取り、[バージョン管理ドキュメント](../create-packages/prerelease-packages.md)します。

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>パッケージ (パッケージの復元) をチェックインせずに NuGet を使用します。
NuGet 1.6 では、どの nuget パッケージは、ソース管理に追加されませんが代わりには復元ビルド時に不足している場合、ワークフローのファースト クラス サポートできるようになりました。 詳細については、読み取り、 [NuGet パッケージをソース管理にコミットせずを使用して](../consume-packages/packages-and-source-control.md)トピック。

### <a name="item-templates-that-install-nuget-packages"></a>NuGet パッケージをインストールする項目テンプレート
Visual Studio プロジェクト テンプレートにプレインストールされている NuGet パッケージをサポートする作業に基づき、NuGet 1.6 はまた、Visual Studio 項目テンプレートのサポートを追加します。 項目テンプレートには、内のテンプレートが呼び出されたときにインストールされている NuGet パッケージを関連付けることができます。

NuGet パッケージをインストールするプロジェクト/項目テンプレートを変更する方法の詳細については、読み取り、 [Visual Studio テンプレート パッケージ](../visual-studio-extensibility/visual-studio-templates.md)トピック。

### <a name="support-for-disabling-package-sources"></a>パッケージ ソースを無効にするためのサポート
複数のパッケージ ソースが構成されている場合、パッケージとその依存関係のインストール中に NuGet はパッケージごとに 1 つになります。 パッケージ ソースをダウンは何らかの理由は、NuGet に深刻な低速化できます。

NuGet 1.6 では、前に、パッケージ ソースを削除する可能性がありますをもう一度追加する場合の詳細を覚える必要がし。

NuGet 1.6 は、無効にし、それを確保するためのパッケージ ソースをオフにするを使用できます。

![パッケージを無効にします。](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>バグ修正
NuGet 1.6 では、作業項目の固定 106 の合計がありました。 バグとして分類されたこれらの 95 と機能は、そのうち 10 でした。

作業の完全な一覧の項目で修正された NuGet 1.6 では、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)します。
