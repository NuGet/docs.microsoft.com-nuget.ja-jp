---
title: NuGet 1.7 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.7 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777064"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 リリースノート

[NuGet 1.6 リリースノート](../release-notes/nuget-1.6.md)  | [NuGet 1.8 リリースノート](../release-notes/nuget-1.8.md)

NuGet 1.7 は、2012年4月4日にリリースされました。

## <a name="known-installation-issue"></a>インストールに関する既知の問題
VS 2010 SP1 を実行している場合は、以前のバージョンがインストールされている場合に NuGet をアップグレードしようとすると、インストールエラーが発生することがあります。

この回避策は、単純に NuGet をアンインストールし、VS 拡張機能ギャラリーからインストールすることです。  詳細については、「 <https://support.microsoft.com/kb/2581019> 」を参照してください。

注: Visual Studio で拡張機能をアンインストールできない場合 ([アンインストール] ボタンが無効になっている場合)、"管理者として実行" を使用して Visual Studio を再起動する必要が生じる可能性があります。

## <a name="features"></a>特徴

### <a name="support-opening-readmetxt-file-after-installation"></a>インストール後に readme.txt ファイルを開くことをサポートする
1.7 の新機能では、パッケージのルートにファイルが含まれている場合 `readme.txt` 、NuGet はパッケージのインストールが完了した後、このファイルを自動的に開きます。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>[NuGet パッケージの管理] ダイアログボックスでプレリリースパッケージを表示する
[NuGet パッケージの管理] ダイアログボックスに、プレリリースパッケージを表示するオプションを提供するドロップダウンが追加されました。

![プレリリースパッケージの表示](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>パッケージファイルが見つからないときに [パッケージの復元] ボタンを表示する
パッケージマネージャーコンソールまたは [マネージャー NuGet パッケージ] ダイアログを開くと、現在のソリューションでパッケージ復元モードが有効になっているかどうか、およびフォルダーにパッケージファイルが見つからないかどうかが NuGet によって確認され `packages` ます。 これら2つの条件が満たされている場合は、NuGet によって通知され、便利な [復元] ボタンが表示されます。 このボタンをクリックすると、NuGet がトリガーされ、不足しているすべてのパッケージが復元されます。

![ダイアログの [パッケージの復元] ボタン](./media/packagerestore-dialog.png)

![コンソールの [パッケージの復元] ボタン](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>ソリューションレベルの packages.config ファイルの追加
以前のバージョンの NuGet では、各プロジェクトには、 `packages.config` そのプロジェクトにインストールされている nuget パッケージを追跡するファイルがあります。 ただし、ソリューションレベルでは、ソリューションレベルのパッケージを追跡するための類似したファイルはありませんでした。 そのため、ソリューションレベルのパッケージを復元する方法はありませんでした。
この機能は現在、NuGet 1.7 で実装されています。 ソリューションレベルの `packages.config` ファイルは、ソリューションルートの下のフォルダーに配置され、 `.nuget` ソリューションレベルのパッケージのみを格納します。

### <a name="remove-new-package-command"></a>New-Package コマンドの削除
使用率が低いため、New-Package コマンドは削除されました。 開発者は、nuget.exe または便利な NuGet パッケージエクスプローラーを使用してパッケージを作成することをお勧めします。

## <a name="bug-fixes"></a>バグの修正
NuGet 1.7 では、パッケージの復元ワークフローとネットワーク/ソース管理のシナリオに関する多くのバグが修正されています。

NuGet 1.7 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)を参照してください。
