---
title: "NuGet 1.6 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.6 リリース ノートです。"
keywords: "NuGet 1.6 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 リリース ノート

[NuGet 1.5 のリリース ノート](../release-notes/nuget-1.5.md) | [NuGet 1.7 リリース ノート](../release-notes/nuget-1.7.md)

NuGet 1.6 は、2011 年 12 月 13 日にリリースされました。

## <a name="known-installation-issue"></a>インストールの既知の問題
VS 2010 SP1 を実行している場合、インストールされている古いバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーに発生する可能性があります。

回避策では、NuGet をシンプルにアンインストールし、VS 拡張機能ギャラリーからインストールします。  詳細については、[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) を参照してください。

注意: Visual Studio には、(削除 ボタンは無効になっている) 拡張機能をアンインストールすることを許可しません、可能性の高い場合"管理者として実行 を使用して Visual Studio を再起動するには

## <a name="features"></a>フィーチャー

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>セマンティック バージョニングとプレリリースのパッケージのサポート
NuGet 1.6 には、セマンティック バージョニング (SemVer) のサポートが導入されています。 SemVer を使用する方法の詳細については、読み取り、[バージョン管理のドキュメント](../create-packages/prerelease-packages.md)です。

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>パッケージ (パッケージの復元) をチェックインせず NuGet を使用します。
NuGet 1.6 では、どの NuGet でパッケージは、ソース管理に追加されませんが代わりには復元ビルド時に存在しない場合、ワークフローの最初のクラスのサポートできるようになりました。 詳細については、読み取り、[をソース管理パッケージをコミットすることがなくを使用して NuGet](../consume-packages/packages-and-source-control.md)トピックです。

### <a name="item-templates-that-install-nuget-packages"></a>NuGet パッケージのインストール項目テンプレート
Visual Studio プロジェクト テンプレートにプレインストールされている NuGet パッケージをサポートする作業の構築、NuGet 1.6 はまた、Visual Studio 項目テンプレートのサポートを追加します。 項目テンプレートには、内のテンプレートが呼び出されたときにインストールされている NuGet パッケージを関連付けることができます。

NuGet パッケージをインストールするプロジェクト/項目テンプレートを変更する方法の詳細については、読み取り、 [Visual Studio のテンプレート内のパッケージ](../visual-studio-extensibility/visual-studio-templates.md)トピックです。

### <a name="support-for-disabling-package-sources"></a>パッケージ ソースを無効にするためのサポート
複数のパッケージ ソースを構成したら、NuGet はパッケージとその依存関係のインストール中にパッケージの 1 つずつになります。 何らかの理由により著しく遅くなる可能性が NuGet、ダウンされているパッケージのソース。

NuGet 1.6 する前にパッケージ ソースを削除する可能性がありますが、しに再び追加する場合の詳細を注意してください。

NuGet 1.6 では、無効にし、それを確保するためのパッケージ ソースをオフにするを使用できます。

![パッケージを無効にします。](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>バグ修正
NuGet 1.6 では、作業項目の固定 106 の合計がありました。 これらの 95 はバグとして分類され、機能は、そのうち 10 でした。

作業の完全な一覧の項目で修正 NuGet 1.6 くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)です。
