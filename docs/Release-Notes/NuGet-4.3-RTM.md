---
title: "NuGet 4.3 RTM のリリース ノート | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 4.3 RTM の既知の問題、バグ修正、追加機能、および DCR を含む、そのリリース ノートです。"
keywords: "NuGet 4.3 RTM リリース ノート, バグ修正, 既知の問題, 追加機能, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: a2b61d854f4a5f1490832dab9a272c3a13b56adf
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-43-rtm-release-notes"></a>NuGet 4.3 RTM リリース ノート

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、.NET Standard 2.0/.NET Core 2.0 などの新しいシナリオ用のサポートを追加し、多数の品質修正を含み、パフォーマンスを改善する NuGet 4.3 RTM が付属しています。 このリリースには、セマンティック バージョニング 2.0.0、NuGet の警告とエラーの MSBuild への統合などのサポートのいくつかの機能強化もあります。

## <a name="known-issues"></a>既知の問題

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>NuGet の復元で無効になっているパッケージ ソースが有効として扱われることがある

#### <a name="issue"></a>懸案事項

次の復元コマンド ライン手法を使うと、無効になっているパッケージ ソースが有効として処理されます。 [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (VS または NetCore SDK 2.0.0 に付属する dotnet.exe を使用)

#### <a name="workaround"></a>回避策

1. Visual Studio (2017 15.3 以降) または NuGet.exe (v4.3.0 以降) を使います。
1. 無効なソースを削除し、引き続き msbuild または dotnet.exe を使います。
1. ソリューションの場合、NuGet.config で "Clear" を使った後、そのソリューションに必要なソースを定義できます。

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

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>NuGet 4.3 RTM の時間枠で修正された問題

[NuGet 4.0 RTM のリリースノート](../release-notes/nuget-4.0-RTM.md) - NuGet 4.0 RTM で修正されたすべての問題が掲載されています

### <a name="features"></a>フィーチャー

- NuGet の復元のパフォーマンスの向上: コマンドラインからの復元と VS でのよりスマートな NoOp の実装 - [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2.0: VS/Dotnet CLI で既存の NuGet 機能を使用開始する必要がある: FallBack フォルダー - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0: 特定の復元の警告をユーザーが無視 (またはエラーを昇格) できるようにする - [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0: CLI のローカライズ アセンブリ - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0: アセット ファイルへのすべての警告/エラーの登録 (PackageTargetFallback を含む) - [#4895](https://github.com/NuGet/Home/issues/4895)

- TFM のサポートの有効化: NetStandard2.0、Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- NuGet.Core および NuGet.Client プロジェクト (そして結果として DLL) の数の削減 - [#2446](https://github.com/NuGet/Home/issues/2446)

- nuget 警告をエラーとしてマークする機能の追加 - [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>バグ

- "PackTask" タスクで "DevelopmentDependency" パラメーターで失敗する msbuild /t:pack はサポートされない - [#5584](https://github.com/NuGet/Home/issues/5584)

- PackagePath の最後に Windows ディレクトリの区切り記号を追加しないと、コンテンツ ファイルのディレクトリ構造がフラット化する - [#4795](https://github.com/NuGet/Home/issues/4795)

- netcore プロジェクトでは developmentDependency としての設定がサポートされない - [#4694](https://github.com/NuGet/Home/issues/4694)

- UI スレッドをブロックし VS をデッドロックさせた RestoreManagerPackage が同期的に読み込まれる - [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet Restore (そのため msbuild /t:restore) はソリューションで明示的なプロジェクト依存関係があるプロジェクトをスキップする [#4578](https://github.com/NuGet/Home/issues/4578)

- ソリューションに、大文字と小文字が異なる、同じプロジェクトを参照するプロジェクトへの参照がある場合、復元ができない場合があります。 これは、別の相対パスで、大文字と小文字に違いがない場合にも影響します - [#4574](https://github.com/NuGet/Home/issues/4574)

- NuGet パッケージから復元した実行可能ファイルが .NET Core 2.0 で実行できない - [#4424](https://github.com/NuGet/Home/issues/4424)

- ソリューション ファイルの解析時に、NuGet.exe が例外の詳細を受け取る - [#4411](https://github.com/NuGet/Home/issues/4411)

- Windows で ContentTargetFolders に '/' で終わるパスが含まれている場合、パックがコンテンツ ファイルを不正な場所に配置する - [#4407](https://github.com/NuGet/Home/issues/4407)

- netcoreapp1.1 をターゲットとするツール パッケージ用に DotNetCliToolReference を復元できない - [#4396](https://github.com/NuGet/Home/issues/4396)

- Nuget 更新 CLI が古いパッケージ バージョンの状態をプロジェクト ファイルに残す (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCR

- CPS 候補からの DotnetCliToolTargetFramework の読み取り - [#5397](https://github.com/NuGet/Home/issues/5397)

- TPMinV チェックは pj スタイル UWP 用に動作する必要がある - [#4763](https://github.com/NuGet/Home/issues/4763)

- AutoReferenced パッケージ用の UI の説明の向上 - [#4471](https://github.com/NuGet/Home/issues/4471)

- NuGet の復元は、ランタイム セクションからコンパイル アセットを選択しています。 - [#4207](https://github.com/NuGet/Home/issues/4207)

- ロック ファイルに依存関係の診断を入れる - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>4.3 RTM で修正された GitHub の懸案事項へのリンク

[懸案事項リスト](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
