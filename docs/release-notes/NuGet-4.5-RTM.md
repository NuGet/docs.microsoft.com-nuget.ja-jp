---
title: NuGet 4.5 RTM リリース ノート
description: NuGet 4.5 RTM の既知の問題、バグ修正、追加機能、および DCR を含む、そのリリース ノートです。
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432505"
---
# <a name="nuget-45-release-notes"></a>NuGet 4.5 リリース ノート

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、[NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe) が付属しています。

## <a name="summary-whats-new-in-450"></a>概要:4.5.0 の新機能

## <a name="summary-whats-new-in-452"></a>概要:4.5.2 の新機能

* セキュリティ修正プログラム: ~/.nuget 内で作成されたファイルに対するアクセス許可の範囲が広すぎる [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-453"></a>概要:4.5.3 の新機能

* セキュリティ修正プログラム: NUPKG ディレクトリより上の NUPKG 内のファイルに相対パスが含まれる場合がある [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>既知の問題

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework と NuGet での .NET Standard 2.0 の問題 

.NET Standard とそのツールは、.NET Framework 4.6.1 をターゲットとするプロジェクトが、.NET Standard 2.0 以前をターゲットとする NuGet パッケージおよびプロジェクトを使用できるように設計されています。 [このドキュメント](https://github.com/dotnet/standard/issues/481)では、そのシナリオに関連する問題の概要、それらの問題を解決する計画、そのツールの今日の状態で展開できる解決策について説明します。

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

無効なアセンブリを含むパッケージを使用するとき、あるいはパッケージ バージョンに 'DateTime' ティッカーが設定されているとき、パッケージ復元が無限ループになることがあります ([dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457))。

#### <a name="workaround"></a>回避策

この問題の回避策はありません。

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>NuGet 4.5 RTM の時間枠で修正された問題

NuGet 4.4 RTM で修正された問題については、[NuGet 4.4 RTM のリリース ノート](../release-notes/nuget-4.4-RTM.md)を参照してください。 

### <a name="features"></a>フィーチャー

- シンボル パッケージの自動プッシュを無効にする - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>バグ

- [回帰] 15.5p1: Portable0.0 がスキップされる - [#6105](https://github.com/NuGet/Home/issues/6105)
- 復元後パッケージのアセットが見つからない - [#5995](https://github.com/NuGet/Home/issues/5995)
- スペースを含む URI でプラグイン資格情報プロバイダーが動作しない - [#5982](https://github.com/NuGet/Home/issues/5982)
- パッケージの復元に失敗した場合、最小の詳細がオンであっても、エラーは出力に印字される必要がある - [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet
  - ソリューション レベルでの dotnetcore restore が ReferenceOutputAssembly が false の ProjectReference に従わず、ビルドがランダムに失敗する - [#5490](https://github.com/NuGet/Home/issues/5490)
- オブジェクト メソッドで PMC のオートコンプリートが正しく動作しない - [#4800](https://github.com/NuGet/Home/issues/4800)
- Visual Studio 2015 ツールセットで nuget.exe の復元が失敗する - [#4713](https://github.com/NuGet/Home/issues/4713)
- vs2017 で perf - pmc をインスタンス化するにはコストがかかる - [#4205](https://github.com/NuGet/Home/issues/4205)
- 低速接続で依存関係の情報を早く入手できない - [#4089](https://github.com/NuGet/Home/issues/4089)
- 複数のパッケージで同じ依存関係を共有する場合、uninstall-package で -RemoveDependencies を使用すると失敗する - [#4026](https://github.com/NuGet/Home/issues/4026)
- 発行用に NuGet.Core.nupkg を最終処理する - [#3581](https://github.com/NuGet/Home/issues/3581)
- -IncludeProjectReferences が csproj と project.json 用に使用される場合、NuGet パックは依存関係 ID をディレクトリ名から解決する - [#3566](https://github.com/NuGet/Home/issues/3566)
- 'NuGet.ProxyCache' 用のタイプ初期化子が例外をスロー - [#3144](https://github.com/NuGet/Home/issues/3144)
- kudu での nuget のパフォーマンスの復元の問題 - [#3087](https://github.com/NuGet/Home/issues/3087)
- 検索が登録 BLOB よりも前の場合、UI クライアントでエラーまたは警告が表示されない - [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages -Updates により不正なクエリが生成される - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>4.5 RTM で修正された GitHub の懸案事項へのリンク

[懸案事項リスト](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
