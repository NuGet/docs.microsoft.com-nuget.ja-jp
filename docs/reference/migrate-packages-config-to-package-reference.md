---
title: Package.config から PackageReference 形式への移行
description: Package.config 管理形式から PackageReference NuGet 4.0 以降および VS2017 と .NET Core 2.0 でサポートされるようにプロジェクトを移行する方法の詳細
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: e0a4363a2807874ec8e2693c5b1c1a0eb2e8af0e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818787"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Packages.config から PackageReference への移行します。

Visual Studio 2017 バージョン 15.7 Preview 3 からプロジェクトを移行する以降をサポートして、 [packages.config](./packages-config.md)管理形式を[PackageReference](../consume-packages/Package-References-in-Project-Files.md)形式です。

## <a name="benefits-of-using-packagereference"></a>PackageReference を使用する利点

* **1 つの場所でのすべてのプロジェクト依存関係の管理**: NuGet パッケージを参照してプロジェクト間参照とアセンブリ参照と同じように (を使用して、`PackageReference`ノード) を別々 のではなく、プロジェクト ファイル内で直接管理packages.config ファイル。
* **最上位レベルの依存関係のっきりビュー**: packages.config とは異なり、PackageReference が直接、プロジェクトにインストールされている NuGet パッケージのみを一覧表示します。 その結果、NuGet パッケージ マネージャーの UI とプロジェクト ファイルは下位レベルの依存関係を持つ整理されています。
* **パフォーマンスの向上**: PackageReference を使用すると、パッケージが管理で、*グローバル パッケージ*フォルダー (の定義に従って[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)なく、`packages`ソリューション内のフォルダーです。 その結果、PackageReference は高速に実行し、少ないディスク領域を使用します。
* **依存関係とコンテンツのフロー制御を微調整**: MSBuild の既存の機能を使用することにより[条件付きで、NuGet パッケージを参照](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)ターゲット フレームワークでごとのパッケージ参照の選択と構成では、プラットフォーム、またはその他のピボットします。
* **アクティブな開発では、PackageReference**: を参照してください[PackageReference が GitHub の問題](https://aka.ms/nuget-pr-improvements)です。 packages.config がアクティブな開発ではなくなりました。

### <a name="limitations"></a>制限事項

* NuGet PackageReference は、Visual Studio 2015 で利用可能な以前ではありません。 移行後のプロジェクトは、Visual Studio 2017 でのみ開くことができます。
* 移行は、C++ と ASP.NET プロジェクトに使用できる現在ではありません。
* 一部のパッケージは、PackageReference と完全に互換性ない場合があります。 詳細については、次を参照してください。[互換性の問題をパッケージ化](#package-compatibility-issues)です。

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

## <a name="migration-steps"></a>移行手順

> [!Note]
> Visual Studio ができるようにするには、プロジェクトのバックアップを作成する移行を開始する前に[packages.config にロールバック](#how-to-roll-back-to-packagesconfig)必要な場合です。

1. 使用してプロジェクトを含むソリューションを開く`packages.config`です。

1. **ソリューション エクスプ ローラー**を右クリックし、**参照**ノードまたは`packages.config`ファイルおよび選択した**PackageReference に packages.config を移行しています.**.

1. Migrator は、プロジェクトの NuGet パッケージの参照を分析しに分類しようとしています**最上位レベルの依存関係**(NuGet パッケージをインストールしたディレクトリ) および**推移的な依存関係**。(最上位のパッケージの依存関係としてインストールされたパッケージ)。

   > [!Note]
   > PackageReference 推移的なパッケージの復元をサポートし、解決の依存関係、動的に依存関係が推移的な必要なインストールしないことに明示的に意味します。

1. (省略可能)選択すると、最上位レベルの依存関係として、推移的な依存関係として分類された NuGet パッケージを処理することもできます、**トップレベル**パッケージのオプションです。 このオプションは推移的にフローしないアセットを含むパッケージを自動的に設定 (内、 `build`、 `buildCrossTargeting`、 `contentFiles`、または`analyzers`フォルダー)、開発の依存関係としてマークされているものと (`developmentDependency = "true"`)。

1. いずれかを確認[互換性の問題をパッケージ化](#package-compatibility-issues)です。

1. 選択**OK**移行を開始します。

1. 移行の最後に、Visual Studio が、バックアップ、インストールされているパッケージ (最上位レベルの依存関係) の一覧、推移的な依存関係として参照されるパッケージの一覧およびの開始時に特定の互換性の問題の一覧にパスを含むレポートを提供します。移行します。 レポートは、バックアップ フォルダーに保存されます。

1. ソリューションがビルドされ、実行されることを検証します。 問題が発生した場合[GitHub の問題を報告](https://github.com/NuGet/Home/issues/)です。

## <a name="how-to-roll-back-to-packagesconfig"></a>Packages.config をロールバックする方法

1. 移行されたプロジェクトを閉じます。

1. プロジェクト ファイルをコピーし、`packages.config`バックアップから (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) プロジェクトのフォルダーにします。 プロジェクトのルート ディレクトリ内に存在する場合は、obj フォルダーを削除します。

1. プロジェクトを開きます。

1. 使用してパッケージ マネージャー コンソールを開き、**ツール > NuGet Package Manager > パッケージ マネージャー コンソール**メニュー コマンド。

1. コンソールで、次のコマンドを実行します。

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>パッケージの互換性の問題

Packages.config にサポートされていた一部の機能は、PackageReference でサポートされていません。 Migrator は、分析し、このような問題を検出します。 次の問題の 1 つ以上を持つすべてのパッケージは、移行後に期待どおりに動作しない可能性があります。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>移行後に、パッケージがインストールされている場合、"install.ps1"スクリプトは無視されます。

| | |
| --- | --- |
| **説明** | PackageReference をインストールしたり、パッケージのアンインストール中に install.ps1 および uninstall.ps1 PowerShell スクリプトは実行されません。 |
| **潜在的な影響** | ターゲット プロジェクトにいくつかの動作を構成するこれらのスクリプトに依存しているパッケージには、期待どおりに動かないことがあります。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>"content"資産は、移行後に、パッケージがインストールされている場合は使用できません。

| | |
| --- | --- |
| **説明** | パッケージの内の資産`content`フォルダー PackageReference がサポートされていないは無視されます。 PackageReference サポートを追加する`contentFiles`より推移的なサポートと共有のコンテンツが必要です。  |
| **潜在的な影響** | 内の資産`content`はコピーされませんプロジェクトとプロジェクト、それらの資産の存在に依存するコードが必要なにリファクタリングします。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>XDT 変換は、アップグレード後に、パッケージがインストールされているときに適用されません。

| | |
| --- | --- |
| **説明** | PackageReference XDT 変換はサポートされず`.xdt`インストールまたはパッケージをアンインストールするときに、ファイルは無視されます。   |
| **潜在的な影響** | XDT いない変換は、プロジェクトの XML ファイルを一般的に、`web.config.install.xdt`と`web.config.uninstall.xdt`、つまり、プロジェクトの` web.config`パッケージをインストールまたはアンインストールする場合、ファイルは更新されません。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>移行後に、パッケージがインストールされているときに lib ルート内のアセンブリは無視されます。

| | |
| --- | --- |
| **説明** | ルートに存在するアセンブリ PackageReference で`lib`ターゲット フレームワークの特定サブ フォルダーがないフォルダーは無視されます。 NuGet は、プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) に一致するサブ フォルダーを検索し、プロジェクトに一致するアセンブリをインストールします。 |
| **潜在的な影響** | プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) に一致するサブ フォルダーがないパッケージの移行後に期待どおりに動作または移行中にインストールが失敗する可能性がありますいません。 |

## <a name="found-an-issue-report-it"></a>問題を発見しますか。 報告してください。

問題は、移行操作を実行する場合は、次のようにしてください。 [NuGet GitHub リポジトリのファイルの問題](https://github.com/NuGet/Home/issues/)です。
