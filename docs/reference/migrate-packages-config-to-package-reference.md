---
title: App.config から PackageReference 形式への移行
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているように、プロジェクトを app.config 管理形式から PackageReference に移行する方法の詳細について説明します。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: d1c32f4a926f1f688db3ea6a9ca2eed1a21b2dec
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433292"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>App.config から PackageReference への移行

Visual Studio 2017 バージョン15.7 以降では、[パッケージ](./packages-config.md)の管理形式から[PackageReference](../consume-packages/Package-References-in-Project-Files.md)形式へのプロジェクトの移行がサポートされています。

## <a name="benefits-of-using-packagereference"></a>PackageReference を使用する利点

* **すべてのプロジェクトの依存関係を1か所で管理**します。プロジェクト間参照やアセンブリ参照と同様に、NuGet パッケージ参照 ( `PackageReference`ノードを使用) は、個別のパッケージ .config ファイルを使用するのではなく、プロジェクトファイル内で直接管理されます。
* **最上位レベルの依存関係のすっきりしたビュー**:PackageReference とは異なり、では、プロジェクトに直接インストールした NuGet パッケージのみが一覧表示されます。 その結果、NuGet パッケージマネージャー UI とプロジェクトファイルが下位レベルの依存関係と共に乱雑になることはありません。
* **パフォーマンスの向上**:PackageReference を使用する場合、パッケージは、ソリューション内の`packages`フォルダーではなく、グローバルパッケージ[とキャッシュフォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)に関するページで説明されているように、"*グローバルパッケージ*" フォルダーに保持されます。 その結果、PackageReference のパフォーマンスが向上し、使用するディスク領域も少なくなります。
* **依存関係とコンテンツフローを細かく制御し**ます。MSBuild の既存の機能を使用すると、 [NuGet パッケージを条件付きで参照](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)し、ターゲットフレームワーク、構成、プラットフォーム、またはその他のピボットごとにパッケージ参照を選択できます。
* **PackageReference はアクティブな開発中**です。[GitHub の PackageReference の問題を](https://aka.ms/nuget-pr-improvements)参照してください。 app.config は、アクティブな開発ではなくなりました。

### <a name="limitations"></a>制限事項

* NuGet PackageReference は、Visual Studio 2015 以前では使用できません。 移行されたプロジェクトは、Visual Studio 2017 以降でのみ開くことができます。
* C++ プロジェクトと ASP.NET プロジェクトについては、現在のところ、移行を利用できません。
* 一部のパッケージは、PackageReference と完全に互換性がない場合があります。 詳細については、「[パッケージの互換性の問題](#package-compatibility-issues)」を参照してください。

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
> 移行を開始する前に、Visual Studio によってプロジェクトのバックアップが作成され、必要に応じて、 [app.config にロールバック](#how-to-roll-back-to-packagesconfig)できるようになります。

1. を使用して`packages.config`プロジェクトを含むソリューションを開きます。

1. **ソリューションエクスプローラー**で、 **[参照]** `packages.config`ノードまたはファイルを右クリックし、 **[パッケージを PackageReference に移行する]** を選択します。

1. Migrator は、プロジェクトの NuGet パッケージ参照を分析し、**トップレベルの依存関係**(直接インストールされた nuget パッケージ) と**推移的な依存関係**(としてインストールされたパッケージ) に分類しようとします。最上位レベルのパッケージの依存関係)。

   > [!Note]
   > PackageReference は推移的なパッケージの復元をサポートし、依存関係を動的に解決します。つまり、推移的な依存関係を明示的にインストールする必要はありません。

1. Optionalパッケージの**最上位レベル**のオプションを選択することで、依存関係として指定された NuGet パッケージを最上位レベルの依存関係として扱うことができます。 `build`このオプションは`analyzers` `buildCrossTargeting`、推移的(`developmentDependency = "true"`、、 、またはフォルダー内)ではなく、開発の依存関係()としてマークされている資産を含むパッケージに対して自動的に設定されます。`contentFiles`

1. パッケージの[互換性の問題](#package-compatibility-issues)を確認します。

1. **[OK]** を選択して移行を開始します。

1. 移行の最後に、Visual Studio によって、バックアップのパス、インストールされているパッケージの一覧 (最上位の依存関係)、推移的な依存関係として参照されるパッケージの一覧、およびの開始時に識別される互換性の問題の一覧が表示されます。移動. レポートがバックアップフォルダーに保存されます。

1. ソリューションがビルドされ、実行されることを確認します。 問題が発生した場合は、 [GitHub で問題](https://github.com/NuGet/Home/issues/)を発生させることができます。

## <a name="how-to-roll-back-to-packagesconfig"></a>App.config にロールバックする方法

1. 移行されたプロジェクトを閉じます。

1. プロジェクトファイルと`packages.config`バックアップ (通常は`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) をプロジェクトフォルダーにコピーします。 Obj フォルダーがプロジェクトのルートディレクトリに存在する場合は、削除します。

1. プロジェクトを開きます。

1. **[ツール > NuGet パッケージマネージャー > パッケージマネージャーコンソール]** メニューコマンドを使用して、パッケージマネージャーコンソールを開きます。

1. コンソールで次のコマンドを実行します。

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>移行後にパッケージを作成する

移行が完了したら、 [nuget. build. tasks. pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget パッケージへの参照を追加し、 [msbuild-](../reference/msbuild-targets.md#pack-target) n パッケージを使用してパッケージを作成することをお勧めします。 `dotnet.exe pack` の`msbuild -t:pack`代わりにを使用できるシナリオもありますが、推奨されません。

## <a name="package-compatibility-issues"></a>パッケージの互換性の問題

PackageReference でサポートされていたいくつかの側面は、ではサポートされていません。 Migrator は、このような問題を分析して検出します。 次の問題が1つ以上発生するパッケージは、移行後に予期したとおりに動作しない可能性があります。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>移行後にパッケージをインストールすると、"install. ps1" スクリプトは無視されます。

| | |
| --- | --- |
| **説明** | PackageReference では、パッケージをインストールまたはアンインストールするときに、ps1 と uninstall. ps1 PowerShell スクリプトは実行されません。 |
| **潜在的な影響** | これらのスクリプトに依存するパッケージは、変換先プロジェクトの動作を構成するために、期待どおりに機能しないことがあります。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>移行後にパッケージをインストールすると、"コンテンツ" 資産は使用できません。

| | |
| --- | --- |
| **説明** | パッケージの`content`フォルダー内の資産は、PackageReference ではサポートされておらず、無視されます。 PackageReference では、 `contentFiles`のサポートを追加して、推移的なサポートと共有コンテンツを向上させることができます。  |
| **潜在的な影響** | の資産`content`はプロジェクトにコピーされません。また、これらの資産の存在に依存するプロジェクトコードには、リファクタリングが必要です。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>アップグレード後にパッケージをインストールするときに XDT 変換が適用されない

| | |
| --- | --- |
| **説明** | Xdt 変換は PackageReference ではサポートさ`.xdt`れていません。パッケージをインストールまたはアンインストールするときに、ファイルは無視されます。   |
| **潜在的な影響** | Xdt 変換は、プロジェクトの XML ファイル (通常は) `web.config.install.xdt` `web.config.uninstall.xdt`には適用されません。つまり` web.config` 、パッケージをインストールまたはアンインストールしても、プロジェクトのファイルは更新されません。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>移行後にパッケージをインストールすると、lib ルート内のアセンブリは無視されます。

| | |
| --- | --- |
| **説明** | PackageReference では、ターゲットフレームワーク固有のサブ`lib`フォルダーのないフォルダーのルートにあるアセンブリは無視されます。 NuGet は、プロジェクトのターゲットフレームワークに対応するターゲットフレームワークモニカー (TFM) に一致するサブフォルダーを検索し、一致するアセンブリをプロジェクトにインストールします。 |
| **潜在的な影響** | プロジェクトのターゲットフレームワークに対応するターゲットフレームワークモニカー (TFM) と一致するサブフォルダーがないパッケージは、移行後に予期したとおりに動作しないか、移行中にインストールが失敗する可能性があります |

## <a name="found-an-issue-report-it"></a>問題が見つかりましたか? レポートを作成します。

移行環境で問題が発生した場合は、 [NuGet GitHub リポジトリで問題](https://github.com/NuGet/Home/issues/)を報告してください。
