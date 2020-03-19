---
title: package.config から PackageReference 形式への移行
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているように、プロジェクトを package.config 管理形式から PackageReference に移行する方法について詳しく説明します
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428523"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>packages.config から PackageReference への移行

Visual Studio 2017 バージョン 15.7 以降では、[packages.config](../reference/packages-config.md) 管理形式から [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 形式へのプロジェクトの移行がサポートされています。

## <a name="benefits-of-using-packagereference"></a>PackageReference を使用する利点

* **すべてのプロジェクトの依存関係を 1 か所で管理**:プロジェクト間参照やアセンブリ参照と同様に、NuGet パッケージ参照 (`PackageReference` ノードを使用) は、個別の packages.config ファイルを使用するのではなく、プロジェクト ファイル内で直接管理されます。
* **最上位の依存関係のすっきりしたビュー**:packages.config とは異なり、PackageReference では、プロジェクトに直接インストールした NuGet パッケージのみが一覧表示されます。 その結果、NuGet パッケージ マネージャー UI とプロジェクト ファイルが下位レベルの依存関係によって乱雑になることはありません。
* **パフォーマンスの向上**:PackageReference を使用する場合、(「[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)」で説明されているように) パッケージはソリューション内の `packages` フォルダーではなく "*グローバル パッケージ*" フォルダー内で管理されます。 その結果、PackageReference のパフォーマンスが向上し、使用するディスク領域も少なくなります。
* **依存関係とコンテンツ フローのきめ細かな制御**:MSBuild の既存の機能を使用して、[NuGet パッケージを条件付きで参照](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)し、ターゲット フレームワーク、構成、プラットフォーム、またはその他のピボットごとにパッケージ参照を選択できます。
* **PackageReference はアクティブに開発中**:[GitHub 上の PackageReference の問題](https://aka.ms/nuget-pr-improvements)に関するページをご覧ください。 packages.config の開発は現在継続されていません。

### <a name="limitations"></a>制限事項

* NuGet PackageReference は、Visual Studio 2015 以前では使用できません。 移行されたプロジェクトは、Visual Studio 2017 以降でのみ開くことができます。
* C++ プロジェクトと ASP.NET プロジェクトについては、現在のところ、移行を利用できません。
* 一部のパッケージは、PackageReference と完全に互換ではない場合があります。 詳しくは、「[パッケージの互換性の問題](#package-compatibility-issues)」をご覧ください。

また、PackageReferences のしくみには、packages.config と比べていくつかの違いがあります。たとえば、[アップグレード バージョンを制限する](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)ことは、PackageReference ではサポートされていませんが、[浮動小数点バージョン](../consume-packages/package-references-in-project-files.md#floating-versions)のサポートが追加されています。

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
> 移行を開始する前に、必要に応じて [packages.config にロールバック](#how-to-roll-back-to-packagesconfig)できるように Visual Studio によってプロジェクトのバックアップが作成されます。

1. `packages.config` を使用してプロジェクトを含むソリューションを開きます。

1. **ソリューション エクスプローラー**で、 **[参照]** ノードまたは `packages.config` ファイルを右クリックし、 **[packages.config を PackageReference に移行する...]** を選択します。

1. 移行プログラムによってプロジェクトの NuGet パッケージ参照が分析され、**最上位の依存関係** (直接インストールした NuGet パッケージ) と**推移的依存関係** (最上位のパッケージの依存関係としてインストールされたパッケージ) への分類が試行されます。

   > [!Note]
   > PackageReference では推移的なパッケージの復元がサポートされ、依存関係が動的に解決されます。つまり、推移的依存関係を明示的にインストールする必要はありません。

1. (省略可能) パッケージに対して **[最上位]** オプションを選択することで、推移的依存関係として分類された NuGet パッケージを最上位の依存関係として扱うことを選択できます。 このオプションは、推移的にフローしないアセットを含む (`build`、`buildCrossTargeting`、`contentFiles`、または `analyzers` フォルダー内にある) パッケージと、開発の依存関係 (`developmentDependency = "true"`) としてマークされているパッケージに対して自動的に設定されます。

1. 「[パッケージの互換性の問題](#package-compatibility-issues)」をご確認ください。

1. **[OK]** を選択して移行を開始します。

1. 移行の最後に、Visual Studio によって、バックアップのパス、インストールされているパッケージの一覧 (最上位の依存関係)、推移的依存関係として参照されるパッケージの一覧、移行の開始時に識別される互換性の問題の一覧に関するレポートが提供されます。 レポートがバックアップ フォルダーに保存されます。

1. ソリューションがビルドされ、実行されることを確認します。 問題が発生した場合は、[問題を GitHub に報告](https://github.com/NuGet/Home/issues/)します。

## <a name="how-to-roll-back-to-packagesconfig"></a>packages.config にロールバックする方法

1. 移行されたプロジェクトを閉じます。

1. プロジェクト ファイルと `packages.config` をバックアップ (通常は `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) からプロジェクト フォルダーにコピーします。 obj フォルダーがプロジェクトのルート ディレクトリに存在する場合は、これを削除します。

1. プロジェクトを開きます。

1. **[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー コンソール]** メニュー コマンドを使用して [パッケージ マネージャー コンソール] を開きます。

1. コンソール内で、次のコマンドを実行します。

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>移行後にパッケージを作成する

移行が完了したら [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget パッケージへの参照を追加し、[msbuild -t:pack](../reference/msbuild-targets.md#pack-target) を使用してパッケージを作成することをお勧めします。 `msbuild -t:pack` の代わりに `dotnet.exe pack` を使用できるシナリオもありますが、推奨されません。

## <a name="package-compatibility-issues"></a>パッケージの互換性の問題

packages.config でサポートされていたいくつかの機能は、PackageReference ではサポートされていません。 移行プログラムでは、このような問題が分析および検出されます。 以下の問題が 1 つ以上あるパッケージは、移行後に期待どおりに動作しない可能性があります。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>移行後にパッケージをインストールするときに、"install. ps1" スクリプトが無視される

| | |
| --- | --- |
| **説明** | PackageReference では、パッケージをインストールまたはアンインストールするときに、install.ps1 および uninstall.ps1 PowerShell スクリプトは実行されません。 |
| **潜在的な影響** | これらのスクリプトに依存して移行先プロジェクト内の一部の動作を構成するパッケージは、期待どおりに動作しないことがあります。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>移行後にパッケージをインストールするときに、"コンテンツ" アセットを使用できない

| | |
| --- | --- |
| **説明** | パッケージの `content` フォルダー内のアセットは、PackageReference ではサポートされず、無視されます。 PackageReference では、推移的なサポートと共有コンテンツを向上させるために `contentFiles` のサポートが追加されています。  |
| **潜在的な影響** | `content` 内のアセットはプロジェクトにコピーされず、これらのアセットの存在に依存するプロジェクト コードにはリファクタリングが必要です。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>アップグレード後にパッケージをインストールするときに XDT 変換が適用されない

| | |
| --- | --- |
| **説明** | XDT 変換は PackageReference ではサポートされず、パッケージをインストールまたはアンインストールするときに `.xdt` ファイルは無視されます。   |
| **潜在的な影響** | XDT 変換は、プロジェクトの XML ファイル (通常は `web.config.install.xdt` と `web.config.uninstall.xdt`) には適用されません。つまり、パッケージをインストールまたはアンインストールしても、プロジェクトの ` web.config` ファイルは更新されません。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>移行後にパッケージをインストールするときに、lib ルート内のアセンブリが無視される

| | |
| --- | --- |
| **説明** | PackageReference では、ターゲット フレームワーク固有のサブフォルダーがない `lib` フォルダーのルートにあるアセンブリは無視されます。 NuGet では、プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) に一致するサブフォルダーが検索され、一致するアセンブリがプロジェクトにインストールされます。 |
| **潜在的な影響** | プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) と一致するサブフォルダーがないパッケージは、移行後に期待どおりに動作しない場合や、移行中にインストールが失敗する場合があります |

## <a name="found-an-issue-report-it"></a>見つかった問題の 報告

移行のエクスペリエンスに問題が発生した場合は、[NuGet GitHub リポジトリに問題を報告](https://github.com/NuGet/Home/issues/)してください。
