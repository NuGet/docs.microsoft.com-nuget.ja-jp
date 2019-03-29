---
title: NuGet 4.4 RTM リリース ノート
description: NuGet 4.3 RTM のリリース ノートであり、既知の問題、バグ修正、追加機能、および DCR が含まれています。
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432570"
---
# <a name="nuget-44-release-notes"></a>NuGet 4.4 リリース ノート

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、NuGet 4.4 RTM が付属しています。

## <a name="summary-whats-new-in-440"></a>概要:4.4.0 の新機能

## <a name="summary-whats-new-in-442"></a>概要:4.4.2 の新機能

* セキュリティ修正プログラム: ~/.nuget 内で作成されたファイルに対するアクセス許可の範囲が広すぎる [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-443"></a>概要:4.4.3 の新機能

* セキュリティ修正プログラム: NUPKG ディレクトリより上の NUPKG 内のファイルに相対パスが含まれる場合がある [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>既知の問題

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework と NuGet での .NET Standard 2.0 の問題 

.NET Standard とそのツールは、.NET Framework 4.6.1 をターゲットとするプロジェクトが、.NET Standard 2.0 以前をターゲットとする NuGet パッケージおよびプロジェクトを使用できるように設計されています。 [このドキュメント](https://github.com/dotnet/standard/issues/481)では、そのシナリオに関連する問題の概要、それらの問題を解決する計画、そのツールの今日の状態で展開できる解決策について説明します。

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>パッケージ マネージャー コンソールの使用中、'Enter' キーが機能しない

#### <a name="issue"></a>懸案事項

パッケージ マネージャー コンソールで、Enter キーが機能しないことがあります。 その場合、修正プログラムで進捗状況を確認してください。再現手順について役に立つ情報があれば提供してください。 [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>回避策

ソリューションを開く前に、Visual Studio を再起動し、PMC を開いてください。 または、`project.lock.json` を削除し、もう一度復元してください。

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>NuGet パッケージ マネージャーを使用した DotNetCLITools の表示、追加、更新ができない

#### <a name="issue"></a>懸案事項

NuGet パッケージ マネージャーが表示されず、DotNetCLITools を追加または更新できません。 [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>回避策

DotNetCLIToolReferences はプロジェクト ファイルで手動編集する必要があります。

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>ターゲット フレームワーク バージョンを再ターゲットすると、IntelliSense が不完全になる

#### <a name="issue"></a>懸案事項

Visual Studio では、ターゲット フレームワーク バージョンを再ターゲットすると、IntelliSense が不完全になることがあります。 これは、パッケージ マネージャー形式として PackageReferences を使用しているときに発生します。 [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>回避策

手動で復元します。

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>署名が無効なアセンブリを含む .NET Core プロジェクトのパッケージは無限の復元ループを始動させることがある

#### <a name="issue"></a>懸案事項

無効な署名付きのアセンブリを含むパッケージを使用するとき、あるいはパッケージ バージョンに 'DateTime' ティッカーが設定されているとき、パッケージの復元が無限ループで実行されることがあります (dotnet/project-system#1457)。

#### <a name="workaround"></a>回避策

この問題の回避策はありません。

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>NuGet 4.4 RTM の時間枠で修正された問題

[NuGet 4.3 RTM のリリース ノート](../release-notes/nuget-4.3-RTM.md) - NuGet 4.3 RTM で修正されたすべての問題が掲載されています

### <a name="features"></a>フィーチャー

- PMC および NuGet PM UI のシナリオでのライトウェイト ソリューション ロードのサポート - [#5180](https://github.com/NuGet/Home/issues/5180)

- MSBuild パック ターゲットには、それ自体の前にユーザー ターゲットを実行するためのパブリック フックを含める必要があります - [#5143](https://github.com/NuGet/Home/issues/5143)

- 機能:nuget install に dependencyVersion スイッチを追加します - [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 は .NET Standard 2.0 for NuGet にマップする必要があります - [#5684](https://github.com/NuGet/Home/issues/5684)

- Visual Studio Build Tools SKU と msbuild /t:restore をサポートします - [#5562](https://github.com/NuGet/Home/issues/5562)

- 復元中、.NET Standard 2.0 用の .NET 4.6.1 のサポートが必要な場合、それがインストールされていないと、エラーを生成されます - [#5325](https://github.com/NuGet/Home/issues/5325)

- パッケージ ID プレフィックス予約クライアント UI - [#5572](https://github.com/NuGet/Home/issues/5572)

- dotnet.exe のローカライズをサポートするためにローカライズされた NuGet コンポーネントを提供します - [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>バグ

- プロジェクト パスの大文字/小文字の指定が異なると、復元において PackageReferences が失われる可能性があります - [#5855](https://github.com/NuGet/Home/issues/5855)

- 警告番号を持つエラー コードがエラー範囲に移動されます - [#5824](https://github.com/NuGet/Home/issues/5824)

- .NET Standard バージョンがターゲット フレームワークと互換性がないことが判明すると、誤ったエラーが返されます - [#5818](https://github.com/NuGet/Home/issues/5818)

- テスト ファイルに混乱を招くライセンスが含まれています - [#5776](https://github.com/NuGet/Home/issues/5776)

- EndToEnd テスト テンプレートでライセンス ヘッダーが欠落しています - [#5774](https://github.com/NuGet/Home/issues/5774)

- packages.config restore でエラーが NU1000 として表示されます - [#5743](https://github.com/NuGet/Home/issues/5743)

- nuget.exe install には Mono に対する DisableParallelProcessing が含まれている必要があります - [#5741](https://github.com/NuGet/Home/issues/5741)

- nuget.exe install でキャッシュが誤って無効にされます - [#5737](https://github.com/NuGet/Home/issues/5737)

- VS: 復元が無効になっているときに packages.config の restore コマンドを実行すると、誤ったメッセージが表示されます - [#5718](https://github.com/NuGet/Home/issues/5718)

- VS: 復元が無効になっているときに復元コマンドを実行すると、混乱を招くメッセージが表示されます - [#5659](https://github.com/NuGet/Home/issues/5659)

- バージョンのメタデータが欠落していると、GetRestoreDotnetCliToolsTask が失敗します - [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - dotnetcore add package によって csproj から空の行が消去される場合があります - [#5697](https://github.com/NuGet/Home/issues/5697)

- NuGet.Config の資格情報設定のソース名に大文字小文字の区別があります - [#5695](https://github.com/NuGet/Home/issues/5695)

- GeneratePackageOnBuild を有効にすることにより、パッケージの履歴全体が削除されました - [#5676](https://github.com/NuGet/Home/issues/5676)

- 復元において、mono.cecil パッケージまたは semver パッケージが復元されません。ただし、その他のパッケージはすべて復元されます。 - [#5649](https://github.com/NuGet/Home/issues/5649)

- エラーと警告 - ソースが使用できない状態で不適切なエラーが発生します。  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] NuGet インストールのステータス テキストが現在のところ、ダーク テーマで適切に表示されません。 - [#5642](https://github.com/NuGet/Home/issues/5642)

- ソリューションの更新/インストール時にすべてのプロジェクトについてパッケージが更新されます - [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - TargetFramework と TargetFrameworks によって、dotnetcore pack の動作が異なります - [#5281](https://github.com/NuGet/Home/issues/5281)

- ツール フォルダーに含まれている DLL により、警告がスローされます - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel が文字列操作で過度のメモリを消費します - [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux が OSX に対して true を返します - [#4648](https://github.com/NuGet/Home/issues/4648)

- 'dotnet pack' が obj\Debug ではなく obj の下に nuspec を配置します - [#4644](https://github.com/NuGet/Home/issues/4644)

- NuGet でのパッケージのアップグレードが極端に遅くなります - [#4534](https://github.com/NuGet/Home/issues/4534)

- LSL (ライトウェイト ソリューション復元) をオンにしていない大規模なソリューションで、CPS と Restore が同期しません - [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 - 指定したバージョンの NuGet パックがメタデータを無視します (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

- Version 番号と ExcludeVersion フラグが指定された nuget.exe (3.+) インストール パッケージがパッケージを新しいバージョンに更新しません - [#2405](https://github.com/NuGet/Home/issues/2405)

- 最上位のパッケージが制約に違反したときに、Project.json restore で警告が生成されます - [#2358](https://github.com/NuGet/Home/issues/2358)

- install コマンド上で -ConfigFile がカスタム構成を設定しません - [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe install で '-DisableParallelProcessing' スイッチが受け入れられません - [#1556](https://github.com/NuGet/Home/issues/1556)

- 無効にされたソースが DotNet.exe または msbuild.exe でまだ使用されています - [#5704](https://github.com/NuGet/Home/issues/5704)

- LSL シナリオでのハングアップの修正 - [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>DCR

- nuget.exe install による TargetFramework のサポート - [#5736](https://github.com/NuGet/Home/issues/5736)

- 異なる msbuild タスク UserAgent 文字列の追加 (netcore 対 desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName は仮想的なものである必要があります - [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] NuGet パッケージを追加したときの混乱を招くメッセージ[#5641](https://github.com/NuGet/Home/issues/5641)

- [警告とエラー] NoWarn が P2P 参照を介して推移的にフローしません - [#5501](https://github.com/NuGet/Home/issues/5501)

- ライトウェイト ソリューション ロード: PM UI、PMC、および IV 用の共通コア - - [#5057](https://github.com/NuGet/Home/issues/5057)

- ライトウェイト ソリューション ロード: サポート - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- Visual Studio がトリガーする復元前の MSBuild ターゲットのサポートが追加されます - [#4781](https://github.com/NuGet/Home/issues/4781)

- BeforeTargets を使用して参照可能な NuGet.targets にパブリック ターゲットを追加します - [#4634](https://github.com/NuGet/Home/issues/4634)

- パック ターゲットがビルド アクションで contentFiles を正常に作成できません - [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do によってスレッド プール スレッドがブロックされます - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Install コマンドの DependencyVersion フラグおよび Framework フラグに関するドキュメント - [#5858](https://github.com/NuGet/Home/issues/5858)

- NuGet の警告およびエラーに関するドキュメントに対する更新 - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>4.4 RTM で修正された GitHub の懸案事項へのリンク

[懸案事項リスト 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[懸案事項リスト 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[懸案事項リスト 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
