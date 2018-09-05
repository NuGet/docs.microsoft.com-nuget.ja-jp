---
title: Package.config から PackageReference 形式への移行
description: NuGet 4.0 + と VS2017 および .NET Core 2.0 でサポートされている PackageReference に package.config 管理形式からプロジェクトを移行する方法の詳細について
author: karann-msft
ms.author: karann
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 05a82e48c7083a19c50a05fa1df74ebfff8030d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546687"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Packages.config から PackageReference に移行します。

以降のサポートからプロジェクトを移行している visual Studio 2017 バージョン 15.7年、 [packages.config](./packages-config.md)管理形式を[PackageReference](../consume-packages/Package-References-in-Project-Files.md)形式。

## <a name="benefits-of-using-packagereference"></a>PackageReference を使用する利点

* **1 か所ですべてのプロジェクトの依存関係を管理**: プロジェクト間参照とアセンブリの参照では、同様の NuGet パッケージの参照 (を使用して、`PackageReference`ノード) を別々 のではなく、プロジェクト ファイル内で直接管理されますpackages.config ファイル。
* **最上位レベルの依存関係の表示をすっきり**: PackageReference、packages.config とは異なり、プロジェクトに直接インストールする NuGet パッケージのみを一覧表示します。 その結果、NuGet パッケージ マネージャー UI とプロジェクト ファイルは、下位レベルの依存関係を持つ乱雑はありません。
* **パフォーマンスの向上**: PackageReference を使用して、パッケージが管理で、*グローバル パッケージ*フォルダー (上の説明に従って[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)なく、`packages`ソリューション内のフォルダー。 その結果、PackageReference は高速に実行し、少ないディスク領域を使用します。
* **依存関係とコンテンツのフロー制御を細かく**: MSBuild の既存の機能を使用することにより[条件付きで NuGet パッケージを参照](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)ターゲット フレームワークごとにパッケージ参照を選択し、構成では、プラットフォーム、またはその他のピボットします。
* **PackageReference は開発**: を参照してください[PackageReference の GitHub 問題](https://aka.ms/nuget-pr-improvements)します。 packages.config は、アクティブな開発ではなくなりました。

### <a name="limitations"></a>制限事項

* NuGet PackageReference は Visual Studio 2015 で使用でき、以前ではありません。 移行されたプロジェクトは、Visual Studio 2017 でのみ開くことができます。
* 移行は、C++、ASP.NET プロジェクトを現在ご利用いただけません。
* いくつかのパッケージは、PackageReference と完全に互換性がない可能性があります。 詳細については、次を参照してください。[互換性の問題をパッケージ化](#package-compatibility-issues)します。

### <a name="known-issues"></a>既知の問題

1. 右クリックのコンテキスト メニューで `Migrate packages.config to PackageReference...` オプションを使用できない 

#### <a name="issue"></a>懸案事項 
 
プロジェクトを最初に開いたとき、NuGet 操作を行うまで NuGet が初期化されていない場合があります。 これにより、`packages.config` または `References` 上の右クリックのコンテキスト メニューで、移行オプションが表示されません。 

#### <a name="workaround"></a>回避策 

次の NuGet アクションのいずれかを実行します。 
* パッケージ マネージャー UI を開く - `References` を右クリックし、`Manage NuGet Packages...` を選択する 
* パッケージ マネージャー コンソールを開く - `Tools > NuGet Package Manager` から、`Package Manager Console` を選択する 
* NuGet 復元を実行する - ソリューション エクスプローラーのソリューション ノードを右クリックし、`Restore NuGet Packages` を選択する 
* NuGet 復元もトリガーするプロジェクトをビルドする 

これで、移行オプションを表示できるようになりました。 このオプションは ASP.NET と C++ のプロジェクト タイプではサポートされておらず、表示されません。 

## <a name="migration-steps"></a>移行の手順

> [!Note]
> Visual Studio ができるようにするには、プロジェクトのバックアップを作成する移行を開始する前に[packages.config へのロールバック](#how-to-roll-back-to-packagesconfig)必要な場合。

1. 使用してプロジェクトを含むソリューションを開く`packages.config`します。

1. **ソリューション エクスプ ローラー**を右クリックし、**参照**ノードまたは`packages.config`ファイルおよび選択**packages.config の PackageReference に移行しています.**.

1. Migrator は、プロジェクトの NuGet パッケージ参照を分析し、分類にしようとしています**最上位レベルの依存関係**(直接インストールされている NuGet パッケージ) および**推移的依存関係**。(最上位のパッケージの依存関係としてインストールされたパッケージ)。

   > [!Note]
   > PackageReference は推移的なパッケージの復元をサポートしているし、依存関係を動的に解決する推移的依存関係が明示的にインストールしない必要がある意味します。

1. (省略可能)選択して、最上位レベルの依存関係として推移的依存関係として分類された NuGet パッケージを処理することができます、**トップレベル**パッケージのオプション。 このオプションは、推移的をフローしないアセットが含まれているパッケージは自動的に設定 (内、 `build`、 `buildCrossTargeting`、 `contentFiles`、または`analyzers`フォルダー) と開発の依存関係として指定されている (`developmentDependency = "true"`)。

1. いずれかを確認して[互換性の問題をパッケージ化](#package-compatibility-issues)します。

1. 選択**OK**移行を開始します。

1. 移行の最後に、Visual Studio は、バックアップ、インストールされているパッケージ (最上位レベルの依存関係) の一覧、推移的依存関係として参照されるパッケージの一覧およびの初めに特定の互換性の問題の一覧にパスを使用してレポートを提供します。移行します。 レポートは、バックアップ フォルダーに保存されます。

1. ソリューションをビルドし、実行を検証します。 問題が発生した場合[GitHub で問題を報告](https://github.com/NuGet/Home/issues/)します。

## <a name="how-to-roll-back-to-packagesconfig"></a>Packages.config にロールバックする方法

1. 移行されたプロジェクトを閉じます。

1. プロジェクト ファイルをコピーし、 `packages.config` 、バックアップから (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`)、プロジェクト フォルダーにします。 プロジェクトのルート ディレクトリに存在する場合は、obj フォルダーを削除します。

1. プロジェクトを開きます。

1. 使用してパッケージ マネージャー コンソールを開き、**ツール > NuGet パッケージ マネージャー > パッケージ マネージャー コンソール**メニュー コマンド。

1. コンソールで、次のコマンドを実行します。

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>パッケージの互換性の問題

Packages.config でサポートされていた一部の側面は、PackageReference のサポートされていません。 Migrator は、分析し、このような問題を検出します。 次の問題の 1 つ以上を持つ任意のパッケージは、移行後も正常動作しない可能性があります。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>移行後、パッケージがインストールされている場合、"install.ps1"スクリプトは無視されます。

| | |
| --- | --- |
| **説明** | Packagereference の場合、インストールしたり、パッケージのアンインストール中に install.ps1 お uninstall.ps1 の PowerShell スクリプトは実行されません。 |
| **潜在的な影響** | 対象のプロジェクトでいくつかの動作を構成するこれらのスクリプトに依存するパッケージが正しく機能しない可能性があります。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>"content"資産は、移行後、パッケージがインストールされている場合は使用できません。

| | |
| --- | --- |
| **説明** | パッケージの資産`content`フォルダーは、PackageReference でサポートされていないは無視されます。 PackageReference のサポートが追加`contentFiles`より推移的なサポートと共有のコンテンツを用意します。  |
| **潜在的な影響** | 資産`content`はコピーされませんリファクタリングがこれらの資産の存在に依存するコード プロジェクトとプロジェクトに必要です。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>アップグレード後に、パッケージがインストールされている場合、XDT 変換は適用されません。

| | |
| --- | --- |
| **説明** | PackageReference では、XDT 変換はサポートされていないと`.xdt`のインストールや、パッケージをアンインストールする場合、ファイルは無視されます。   |
| **潜在的な影響** | XDT 変換はほとんどの場合、そのプロジェクトの XML ファイルに適用されません`web.config.install.xdt`と`web.config.uninstall.xdt`、つまり、プロジェクトの` web.config`ファイルは、パッケージをインストールまたはアンインストール時に更新されません。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>移行後、パッケージがインストールされているときに lib ルート内のアセンブリは無視されます。

| | |
| --- | --- |
| **説明** | Packagereference の場合、アセンブリの表示のルートにある`lib`ターゲット フレームワークの特定サブ フォルダーがないフォルダーは無視されます。 NuGet では、プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) に一致するサブフォルダーを検索し、プロジェクトに一致するアセンブリをインストールします。 |
| **潜在的な影響** | プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) に一致するサブフォルダーがないパッケージが、移行後に期待どおりに動作しないまたは移行中にインストールが失敗 |

## <a name="found-an-issue-report-it"></a>問題が見つかりましたか。 報告してください。

移行エクスペリエンスに問題が発生した場合のください[NuGet GitHub リポジトリで問題を報告](https://github.com/NuGet/Home/issues/)します。
