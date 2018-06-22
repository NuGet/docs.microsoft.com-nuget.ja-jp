---
title: NuGet 1.7 リリース ノート
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.7 リリース ノートです。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 81db81642ac21b7dd41f5940dfba919d0871ec01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820928"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 リリース ノート

[NuGet 1.6 リリース ノート](../release-notes/nuget-1.6.md) | [NuGet 1.8 リリース ノート](../release-notes/nuget-1.8.md)

NuGet 1.7 は、2012 年 4 月 4 日にリリースされました。

## <a name="known-installation-issue"></a>インストールの既知の問題
VS 2010 SP1 を実行している場合、インストールされている古いバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーに発生する可能性があります。

回避策では、NuGet をシンプルにアンインストールし、VS 拡張機能ギャラリーからインストールします。  詳細については、「[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)」を参照してください。

注意: Visual Studio には、(削除 ボタンは無効になっている) 拡張機能をアンインストールすることを許可しません、可能性の高い場合"管理者として実行 を使用して Visual Studio を再起動するには

## <a name="features"></a>フィーチャー

### <a name="support-opening-readmetxt-file-after-installation"></a>サポートのインストール後に readme.txt ファイルを開く
新機能、1.7、パッケージに含まれる場合、`readme.txt`パッケージのインストールが完了した後は、NuGet パッケージのルートにあるファイルにこのファイルは開く自動的にします。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>NuGet の管理の [パッケージ] ダイアログ ボックスのプレリリースのパッケージを表示します。
[NuGet パッケージの管理] ダイアログには、プレリリースのパッケージを表示するオプションを提供するドロップダウン リストが含まれています。

![プレリリースのパッケージを表示](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>パッケージ ファイルが見つからない場合は、パッケージの復元 ボタンを表示します。
パッケージ マネージャー コンソールを開くか、マネージャーの NuGet パッケージ ダイアログ、NuGet の現在のソリューションが、パッケージの復元モードを有効なかどうかは確認と、すべてのパッケージ ファイルがない場合、`packages`フォルダーです。 これら 2 つの条件が満たされた場合 NuGet 通知が表示され、便利な [復元] ボタンを表示します。 このボタンをクリックすると、不足しているすべてのパッケージを復元する NuGet がトリガーされます。

![ダイアログでパッケージの復元 ボタン](./media/packagerestore-dialog.png)

![コンソールでパッケージの復元 ボタン](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>ソリューション レベル packages.config ファイルを追加します。
各プロジェクトには NuGet の以前のバージョンで、`packages.config`ファイルを追跡する NuGet パッケージは、そのプロジェクトにインストールされます。 ただし、なかった同様のファイル レベルのソリューション パッケージを追跡するため、ソリューション レベルで。 その結果、ソリューション レベルのパッケージを復元する方法がありませんでした。
NuGet 1.7 では、この機能は実装されてようになりました。 ソリューション レベル`packages.config`ファイルが下に置かれて、`.nuget`ソリューションの下のフォルダーのルートし、ソリューション レベルのみのパッケージを格納します。

### <a name="remove-new-package-command"></a>新規パッケージを削除します。
使用頻度の低いため、新規パッケージ コマンドは削除されました。 開発者は nuget.exe または NuGet パッケージの便利なエクスプ ローラーを使用してパッケージを作成することをお勧めします。

## <a name="bug-fixes"></a>バグ修正
NuGet 1.7 は、パッケージの復元のワークフローとネットワーク/ソース制御シナリオを囲む多くのバグを修正しました。

作業の完全な一覧の項目で修正 NuGet 1.7 くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)です。
