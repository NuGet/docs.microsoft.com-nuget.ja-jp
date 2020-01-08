---
title: NuGet 1.7 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.7 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a98da76038582202396c8da96f8eae166e6096f6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383320"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 リリースノート

Nuget [1.6 リリースノート](../release-notes/nuget-1.6.md) | [Nuget 1.8 リリースノート](../release-notes/nuget-1.8.md)

NuGet 1.7 は、2012年4月4日にリリースされました。

## <a name="known-installation-issue"></a>インストールに関する既知の問題
VS 2010 SP1 を実行している場合は、以前のバージョンがインストールされている場合に NuGet をアップグレードしようとすると、インストールエラーが発生することがあります。

この回避策は、単純に NuGet をアンインストールし、VS 拡張機能ギャラリーからインストールすることです。  詳細については、「<https://support.microsoft.com/kb/2581019>」を参照してください。

注: Visual Studio で拡張機能をアンインストールできない場合 ([アンインストール] ボタンが無効になっている場合)、"管理者として実行" を使用して Visual Studio を再起動する必要が生じる可能性があります。

## <a name="features"></a>フィーチャー

### <a name="support-opening-readmetxt-file-after-installation"></a>インストール後の readme.txt ファイルのオープンをサポートする
1\.7 の新機能では、パッケージのルートに `readme.txt` ファイルがパッケージに含まれている場合、パッケージのインストールが完了した後に、NuGet によってこのファイルが自動的に開きます。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>[NuGet パッケージの管理] ダイアログボックスでプレリリースパッケージを表示する
[NuGet パッケージの管理] ダイアログボックスに、プレリリースパッケージを表示するオプションを提供するドロップダウンが追加されました。

![プレリリースパッケージの表示](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>パッケージファイルが見つからないときに [パッケージの復元] ボタンを表示する
パッケージマネージャーコンソールまたは [マネージャー NuGet パッケージ] ダイアログを開くと、現在のソリューションでパッケージ復元モードが有効になっているかどうか、および `packages` フォルダーにパッケージファイルが見つからないかどうかが確認されます。 これら2つの条件が満たされている場合は、NuGet によって通知され、便利な [復元] ボタンが表示されます。 このボタンをクリックすると、NuGet がトリガーされ、不足しているすべてのパッケージが復元されます。

![ダイアログの [パッケージの復元] ボタン](./media/packagerestore-dialog.png)

![コンソールの [パッケージの復元] ボタン](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>ソリューションレベルのパッケージ .config ファイルの追加
以前のバージョンの NuGet では、各プロジェクトには、そのプロジェクトにインストールされている NuGet パッケージを追跡する `packages.config` ファイルがあります。 ただし、ソリューションレベルでは、ソリューションレベルのパッケージを追跡するための類似したファイルはありませんでした。 そのため、ソリューションレベルのパッケージを復元する方法はありませんでした。
この機能は現在、NuGet 1.7 で実装されています。 ソリューションレベルの `packages.config` ファイルは、ソリューションルートの下の `.nuget` フォルダーに配置され、ソリューションレベルのパッケージのみを格納します。

### <a name="remove-new-package-command"></a>新しいパッケージコマンドの削除
使用率が低いため、新しいパッケージコマンドが削除されました。 開発者は、nuget.exe または便利な NuGet パッケージエクスプローラーを使用してパッケージを作成することをお勧めします。

## <a name="bug-fixes"></a>バグ修正
NuGet 1.7 では、パッケージの復元ワークフローとネットワーク/ソース管理のシナリオに関する多くのバグが修正されています。

NuGet 1.7 で修正された作業項目の完全な一覧については、[このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)を参照してください。
