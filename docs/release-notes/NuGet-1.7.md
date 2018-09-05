---
title: NuGet 1.7 のリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.7 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551468"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 のリリース ノート

[NuGet 1.6 リリース ノート](../release-notes/nuget-1.6.md) | [NuGet 1.8 のリリース ノート](../release-notes/nuget-1.8.md)

NuGet 1.7 は、2012 年 4 月 4 日にリリースされました。

## <a name="known-installation-issue"></a>インストールの既知の問題
VS 2010 SP1 を実行している場合は、インストールされている以前のバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーが発生実行可能性があります。

回避策では、単に NuGet をアンインストールしてから、VS 拡張ギャラリーからインストールします。  詳細については、「[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)」を参照してください。

注: Visual Studio ([アンインストール] ボタンは無効です) 拡張機能をアンインストールすることができず、しの場合必要があります「管理者として実行」を使用して Visual Studio を再起動するには

## <a name="features"></a>フィーチャー

### <a name="support-opening-readmetxt-file-after-installation"></a>サポートのインストール後に readme.txt ファイルを開く
パッケージが含まれている場合、1.7 では新しい、`readme.txt`パッケージのインストールが完了した後は、NuGet パッケージのルートにあるファイルにこのファイルは開く自動的にします。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>NuGet の管理の [パッケージ] ダイアログ ボックスのプレリリース パッケージを表示します。
NuGet パッケージの管理 ダイアログには、プレリリース パッケージを表示するオプションを提供するドロップダウン リストが含まれています。

![プレリリース パッケージを表示](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>パッケージ ファイルが見つからない場合は、パッケージの復元 ボタンを表示します。
パッケージ マネージャー コンソールを開くか Manager NuGet パッケージのダイアログ、NuGet は、現在のソリューションがパッケージの復元モードを有効なかどうかを確認し、すべてのパッケージ ファイルがない場合、`packages`フォルダー。 これら 2 つの条件が満たされた場合、NuGet は通知して、便利な復元 ボタンが表示されます。 このボタンをクリックすると、NuGet に不足しているすべてのパッケージの復元がトリガーされます。

![ダイアログ ボックスでパッケージの復元 ボタン](./media/packagerestore-dialog.png)

![コンソールでパッケージの復元 ボタン](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>ソリューション レベルの packages.config ファイルを追加します。
以前のバージョンの NuGet では、各プロジェクトには、`packages.config`ファイルを追跡する NuGet パッケージは、そのプロジェクトにインストールされます。 ただし、なかったようなファイルをソリューション レベル パッケージの追跡ソリューション レベルで。 その結果、ソリューション レベル パッケージを復元する方法がありませんでした。
NuGet 1.7 でこの機能が実装されているようになりました。 ソリューション レベル`packages.config`ファイルが下に配置、`.nuget`ソリューションの下のフォルダーのルートし、のみのソリューション レベル パッケージを格納します。

### <a name="remove-new-package-command"></a>新規パッケージのコマンドを削除します。
使用率が低いため、新規パッケージ コマンドが削除されました。 Nuget.exe または便利な NuGet パッケージ エクスプ ローラーを使用してパッケージを作成するには、開発者がお勧めします。

## <a name="bug-fixes"></a>バグ修正
NuGet 1.7 は、パッケージの復元ワークフローとネットワーク/ソース管理のシナリオに関して、多くのバグを修正しました。

作業の完全な一覧の項目で修正された NuGet 1.7、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)します。
