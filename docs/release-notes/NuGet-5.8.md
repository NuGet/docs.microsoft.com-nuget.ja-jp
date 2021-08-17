---
title: NuGet 5.8 リリース ノート
description: 新機能、バグ修正NuGet DCRs など、NuGet 5.8 のリリース ノート。
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: fca9d2d068aadec207bfbf12f3ea82af872825a5
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209931"
---
# <a name="nuget-58-release-notes"></a>NuGet 5.8 リリース ノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン | 利用可能な .NET SDK |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.8](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1</sup> .NET Core ワークロードVisual Studio 2019 でインストール済み
  
> [!NOTE]
> Visual Studio 16.8、MSBuild 16.8、および .NET 5.0 には 5.8 以降NuGet.exe必要があります。


## <a name="summary-whats-new-in-58"></a>概要: 5.8 の新機能
🎉.NET **5.0** を対象とする NuGet パッケージの完全な作成と復元のサポートを提供する最初のリリース🎉

* mmap/CreateFileMapping を使用して nupkg 抽出を高速化する - [#9807](https://github.com/NuGet/Home/issues/9807)

* [UI パッケージの詳細] ウィンドウでパッケージ マネージャーの脆弱性の詳細を表示する - [#9850](https://github.com/NuGet/Home/issues/9850)

* 新しいコマンドNuGetして、署名済みパッケージを [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) 確認[します](https://github.com/NuGet/Home/issues/8051)- #8051

* [`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) では `--prerelease` 、プレリリース バージョンを含むパッケージの最新バージョンを追加するオプションがサポート [#4699](https://github.com/NuGet/Home/issues/4699)

* コマンドを使用して CLI でパッケージを [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) 検索する - [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) コマンドはオプション `--verbosity` をサポートしています - [#9600](https://github.com/NuGet/Home/issues/9600)

* csproj No-Op PackageReference ベースのプロジェクトに対する高速復元の最適化を有効にする - Visual Studio - [#9565](https://github.com/NuGet/Home/issues/9565)

* パッケージのインストールパッケージ マネージャー更新プログラムなどの UI 操作のソリューション レベルは最大 10 倍高速[です](https://github.com/NuGet/Home/issues/6010)。#6010

* Visual Studio、#9982、#9984、#10052[など](https://github.com/NuGet/Home/issues/9982)、NuGetの[](https://github.com/NuGet/Home/issues/9984)他のいくつかの[#10052向上](https://github.com/NuGet/Home/issues/10052)[#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**DCRs:**

* .NET 5.0 TFM: フレームワークの優先順位規則 - [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet TargetFramework を解析するときに、ドット プラットフォームのバージョンを特定[#9842](https://github.com/NuGet/Home/issues/9842)

* TargetFrameworkMoniker & TargetPlatformMoniker を使用して、個々の TFI、TFV、TPI、TPV プロパティを使用する代わりに[](https://github.com/NuGet/Home/issues/9895)フレームワークを#9895

* プラットフォーム `GetReferenceNearestTargetFrameworkTask()` (net5.0-windows など) を使用したターゲット フレームワークを[](https://github.com/NuGet/Home/issues/9894)サポートする更新 - #9894

* .NET 5.0 Visual Studio API - [#9650](https://github.com/NuGet/Home/issues/9650)

* パッケージ マネージャーUI: エラー (パッケージダウングレードなど) のためにパッケージの統合または更新操作をブロックしない[-](https://github.com/NuGet/Home/issues/9224) #9224

* NuGet機能を持つプロジェクトでは、次の機能が点灯する必要があります。"PackageReferences" - [#9957](https://github.com/NuGet/Home/issues/9957)

* [No-Op メッセージの復元を抑制Visual Studio - [#6384](https://github.com/NuGet/Home/issues/6384)

**バグ：**

* OutputWindowTextWriter コンストラクターをバックグラウンド スレッドで呼び出す必要はありません[-](https://github.com/NuGet/Home/issues/9764) #9764

* ビッグ エンディアン CPU で署名済みパッケージを復元する - [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger は MEF コンストラクターでアフィニティ化されたメソッドを[](https://github.com/NuGet/Home/issues/9591)呼び出さ#9591

* バグが発生NuGet。CommandLine.Console `PrintJustified()` メソッド - [#9737](https://github.com/NuGet/Home/issues/9737)

* パッケージ マネージャーバインドの不備によりパッケージ メタデータがガベージ コレクションされた場合の UI メモリ[リーク](https://github.com/NuGet/Home/issues/9757)- #9757

* [署名]UI の形式で署名済みパッケージをインストールするときにエラー一覧packages.config警告パッケージ マネージャー表示されません - [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet。CommandLine.XPlat にはパブリック API を含め "しない" - [#9821](https://github.com/NuGet/Home/issues/9821)

* スレッドプール スレッドをブロックしてリソースを読み込む場合のソリューションの読み込み時間の#9822 `BlockingCollection.Take()`  -  [](https://github.com/NuGet/Home/issues/9822)

* コマンド ライン復元では、複数の対象プロジェクトを使用NuGet、内部ビルドからターゲット フレームワーク関連の情報を読み取る必要[#9869](https://github.com/NuGet/Home/issues/9869)

* TargetFrameworkInformation 項目を使用してランタイム識別子グラフを読み取る - [#9874](https://github.com/NuGet/Home/issues/9874)

* 静的グラフの復元は、CrossTargeting プロパティに関して、Visual Studio と定期的な評価MSBuildに関して一[貫性がありません](https://github.com/NuGet/Home/issues/9881)- #9881

* 静的グラフの復元では、複数の対象プロジェクトをNuGet、内部ビルドからターゲット フレームワーク関連の情報を読み取る必要があります。 - [#9870](https://github.com/NuGet/Home/issues/9870)

* プロジェクト `net5.0-platform` の読み込みと復元を Visual Studio - [#9863](https://github.com/NuGet/Home/issues/9863)

* 解決済みバージョンを UI にパッケージ マネージャーする - [#9826](https://github.com/NuGet/Home/issues/9826)

* パッケージ マネージャーUI: ソリューション エクスプローラーパッケージの依存関係の一部NuGet表示されない - [#9898](https://github.com/NuGet/Home/issues/9898)

* SPDX ライセンス の一覧を更新する - [#9946](https://github.com/NuGet/Home/issues/9946)

* [パッケージの管理] を開いたNuGet VS 2019 がクラッシュする: アイコンをクリックすると、イメージ conversio でハンドルされない例外が発生する - [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet。Packaging.Extraction では、データを除外するために ilmerge が[Newtonsoft.Js必要です](https://github.com/NuGet/Home/issues/9966)- #9966

* エラーがない場合、ContinuePackingAfterGeneratingNuspec=false を使用したパッキングは失敗しない[-](https://github.com/NuGet/Home/issues/9786) #9786

* パッケージ マネージャーUI: アイコンが色を正しく反転しない - [#10017](https://github.com/NuGet/Home/issues/10017)

* 最新のプロジェクトのプロジェクト数と復元時の No-Opプロジェクトの数が正しくない - [#10026](https://github.com/NuGet/Home/issues/10026)

* 値 `/p:RestoreUseStaticGraphEvaluation=true` に結果を使用して Null にすることはできません - [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` WPF ライブラリ プロジェクトのエイリアスを誤って使用する - [#10020](https://github.com/NuGet/Home/issues/10020)

* パッケージ マネージャーUI: 署名の検証が失敗した場合の NullReferenceException [-](https://github.com/NuGet/Home/issues/10042) #10042

* Codespaces: プロジェクト メタデータ値 `object` に型を使用[](https://github.com/NuGet/Home/issues/10055)しない - #10055

* Codespaces: ツール オプションでパッケージ ソースを保存すると、[資格情報が上書](https://github.com/NuGet/Home/issues/9711)き#9711


**[このリリースで修正された問題の一覧 - 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[このリリースの問題の一覧 - 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>コミュニティからの投稿

このリリースをすばらしいものにするのに役立ったNuGetありがとうございます。

|担当者|Prs|発行|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | エラー メッセージの入力ミス。 "administrator" ではなく "administator" [-](https://github.com/NuGet/Home/issues/9662) #9662
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | NuGet無効な AssemblyInformationalVersion レポートを含むパック "description is required" - [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` では、Branch プロパティと Commit プロパティは考慮されません - [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | [エラー一覧] ウィンドウVisual Studio NU コードをクリックすると、次 [https://docs.microsoft.com/nuget/reference/errors-and-warnings/](/nuget/reference/errors-and-warnings/) の#9934  -  [](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | 新しいパッケージ ソース https:// を追加する場合は、"https://" を使用します。Visual Studioオプション - [#9974](https://github.com/NuGet/Home/issues/9974)
[The最も人気の高い](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` Mono のパフォーマンスの問題 - [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | SemanticVersion クラスの TypeConverter を[追加する](https://github.com/NuGet/Home/issues/9125)- #9125

## <a name="summary-whats-new-in-581"></a>概要: 5.8.1 の新機能

* packages.config package.lock.js5.8 では正しくないターゲット フレームワークが使用されます - [#10257](https://github.com/NuGet/Home/issues/10257)

* 5.8 + 16.8 PackageReference と packages.config を混在するときに推移的なプロジェクトの依存関係を解決できない - [#10326](https://github.com/NuGet/Home/issues/10326)

**[このリリースで修正された問題の一覧 - 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[このリリースのコミットの一覧 - 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>フィードバックへようこそ

お客様のフィードバックは Microsoft にとって重要です。  このリリースで問題が発生した場合は、既存の[](https://github.com/NuGet/Home/issues)問題GitHub問題と開発者Visual Studio問題[](https://developercommunity.visualstudio.com/)Community確認してください。  NuGet 内の新しい問題については、 [GitHub の問題](https://github.com/NuGet/Home/issues/new)を報告してください。
NuGet エクスペリエンスに関する一般的な問題については、[**ヘルプ] >**[問題の報告] の下にあるお気に入りの IDE にある [問題点の [報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] オプションを使用してお知らせください。