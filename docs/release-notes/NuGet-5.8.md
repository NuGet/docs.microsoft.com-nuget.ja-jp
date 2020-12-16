---
title: NuGet 5.8 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.8 のリリースノート。
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 329fdf6479d0799ae4b15cc3493848ba2d999853
ms.sourcegitcommit: 650c08f8bc3d48dfd206a111e5e2aaca3001f569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97523442"
---
# <a name="nuget-58-release-notes"></a>NuGet 5.8 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン | 利用可能な .NET SDK |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.8](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Visual Studio 2019 と .net Core ワークロードと共にインストールされる
  
> [!NOTE]
> Visual Studio 16.8、MSBuild 16.8、および .NET 5.0 には NuGet.exe 5.8 以降が必要です。


## <a name="summary-whats-new-in-58"></a>概要: 5.8 の新機能
🎉 **これは、.net 5.0 をターゲットとする NuGet パッケージの完全な作成と復元のサポートを提供するための最初のリリースです** 🎉

* Mmap/Createfilemapping にを使用した nupkg 抽出[#9807](https://github.com/NuGet/Home/issues/9807)の高速化

* パッケージマネージャー UI パッケージの詳細ペインでパッケージの脆弱性の詳細を表示する- [#9850](https://github.com/NuGet/Home/issues/9850)

* 新しい [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) コマンド[#8051](https://github.com/NuGet/Home/issues/8051)で署名済みの NuGet パッケージを確認する

* [`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples)`--prerelease`プレリリースバージョンを含むパッケージの最新バージョンを追加するオプションをサポートしてい[#4699](https://github.com/NuGet/Home/issues/4699)

* [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search)コマンド[#9704](https://github.com/NuGet/Home/issues/9704)を使用して CLI でパッケージを検索する

* [`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) コマンドはオプションをサポートしてい `--verbosity` [#9600](https://github.com/NuGet/Home/issues/9600)

* Visual Studio での、PackageReference ベースの .csproj スタイルのプロジェクトの高速 No-Op 復元の最適化を有効にする- [#9565](https://github.com/NuGet/Home/issues/9565)

* パッケージのインストールや更新などのソリューションレベルのパッケージマネージャーの UI 操作は、最大10倍の速度で実行され [#6010](https://github.com/NuGet/Home/issues/6010)

* Visual Studio でのその他のいくつかの NuGet パフォーマンスの向上- [#9982](https://github.com/NuGet/Home/issues/9982)、 [#9984](https://github.com/NuGet/Home/issues/9984)、 [#10052](https://github.com/NuGet/Home/issues/10052)、 [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**Dcr**

* .NET 5.0 TFM: フレームワークの優先順位の規則- [#9436](https://github.com/NuGet/Home/issues/9436)

* TargetFramework を解析するときに、NuGet はドットプラットフォームバージョンを推論することはできません- [#9842](https://github.com/NuGet/Home/issues/9842)

* TargetFrameworkMoniker & Targetframeworkmoniker を使用して、個々の TFI、TFI、TFI、TFI プロパティ- [#9895](https://github.com/NuGet/Home/issues/9895)を使用するのではなく、フレームワークを推測します。

* `GetReferenceNearestTargetFrameworkTask()`プラットフォーム (net 5.0-windows など) を使用したターゲットフレームワークをサポートするための更新プログラム- [#9894](https://github.com/NuGet/Home/issues/9894)

* .NET 5.0 Visual Studio Api- [#9650](https://github.com/NuGet/Home/issues/9650)

* パッケージマネージャー UI: パッケージの統合または更新は、エラー (パッケージダウングレードなど) が原因でブロックされないようにする必要があります。- [#9224](https://github.com/NuGet/Home/issues/9224)

* 機能があるプロジェクトについては、NuGet の機能が淡色になります。"PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)

* Visual Studio でメッセージの No-Op 復元を抑制する- [#6384](https://github.com/NuGet/Home/issues/6384)

**バグ**

* OutputWindowTextWriter コンストラクターをバックグラウンドスレッドで呼び出すことはできません- [#9764](https://github.com/NuGet/Home/issues/9764)

* ビッグエンディアン Cpu で署名されたパッケージを復元する- [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger は MEF コンストラクターで関連付けられたメソッドを呼び出すことはできません- [#9591](https://github.com/NuGet/Home/issues/9591)

* NuGet. CommandLine. Console メソッドのバグ `PrintJustified()` - [#9737](https://github.com/NuGet/Home/issues/9737)

* 不適切なバインドのためにパッケージメタデータがガベージコレクションされるときのパッケージマネージャー UI のメモリリーク [#9757](https://github.com/NuGet/Home/issues/9757)

* 付きパッケージマネージャー UI で packages.config 形式の署名付きパッケージをインストールすると、エラー一覧に警告は表示されません。 [#9798](https://github.com/NuGet/Home/issues/9798)

* XPlat にパブリック Api を含めることはできません- [#9821](https://github.com/NuGet/Home/issues/9821)

* #9822 でスレッドプールのスレッドをブロックすることによって、ソリューションの読み込み時にリソースの競合を軽減します `BlockingCollection.Take()`  -  [](https://github.com/NuGet/Home/issues/9822)

* 複数のターゲットが指定されたプロジェクトのコマンドライン復元では、NuGet は内部ビルドからターゲットフレームワーク関連情報を読み取る必要があり [#9869](https://github.com/NuGet/Home/issues/9869)

* TargetFrameworkInformation 項目を使用してランタイム識別子グラフを読み取ります。 [#9874](https://github.com/NuGet/Home/issues/9874)

* Visual Studio と通常の MSBuild 評価の復元[#9881](https://github.com/NuGet/Home/issues/9881)と比較した場合、静的なグラフの復元は、の CrossTargeting プロパティに関して一貫性がありません

* 複数のターゲットが指定されたプロジェクトの静的なグラフ復元では、NuGet は、内部ビルドからターゲットフレームワーク関連情報を読み取る必要があります。 - [#9870](https://github.com/NuGet/Home/issues/9870)

* `net5.0-platform`Visual Studio でのプロジェクトの読み込みと復元を許可する- [#9863](https://github.com/NuGet/Home/issues/9863)

* パッケージマネージャー UI で解決済みのバージョンを表示する- [#9826](https://github.com/NuGet/Home/issues/9826)

* パッケージマネージャー UI: ソリューションエクスプローラーにすべての NuGet パッケージの依存関係が表示されていません- [#9898](https://github.com/NuGet/Home/issues/9898)

* SPDX ライセンスリストを更新する- [#9946](https://github.com/NuGet/Home/issues/9946)

* [NuGet パッケージの管理] を開いた後、VS 2019 がクラッシュする: アイコンは[#9696](https://github.com/NuGet/Home/issues/9696) 、conversio イメージでハンドルされない例外を発生させます。

* [#9966](https://github.com/NuGet/Home/issues/9966)で Newtonsoft.Jsを除外するには、パッケージの抽出に ilmerge が必要です

* ContinuePackingAfterGeneratingNuspec = false でのパッキングは、エラーがない場合は失敗しません- [#9786](https://github.com/NuGet/Home/issues/9786)

* パッケージマネージャー UI: アイコンが正しく反転していません- [#10017](https://github.com/NuGet/Home/issues/10017)

* 復元時に最新のプロジェクトと No-Op プロジェクトのプロジェクト数が正しくない- [#10026](https://github.com/NuGet/Home/issues/10026)

* 結果を使用して `/p:RestoreUseStaticGraphEvaluation=true` 値を Null にすることはできません- [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` WPF ライブラリプロジェクトのエイリアスを誤って使用する- [#10020](https://github.com/NuGet/Home/issues/10020)

* パッケージマネージャー UI: 署名の検証に失敗した場合[#10042](https://github.com/NuGet/Home/issues/10042)の NullReferenceException

* Codespaces: `object` プロジェクトメタデータ値の型を使用しません- [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: [ツール] オプションでパッケージソースを保存すると、資格情報が上書きされ [#9711](https://github.com/NuGet/Home/issues/9711)


**[このリリースで修正されるすべての問題の一覧-5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[このリリースで修正される問題/コミットの一覧-5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>コミュニティからの投稿

この NuGet のリリースに役立ったすべての共同作成者に感謝します。

|担当者|Pr|発行|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | エラーメッセージに誤りがあります。 "administrator" ではなく "管理者"- [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | 無効な AssemblyInformationalVersion レポートの NuGet パックが必要です。 "- [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` ブランチとコミットのプロパティを考慮しない- [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Visual Studio の [エラー一覧] ウィンドウで [プログラム] をクリックすると、 https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)に変わります
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Visual Studio のオプションを使用して新しいパッケージソースを追加するときに ' https://' を使用する- [#9974](https://github.com/NuGet/Home/issues/9974)
[[& Zok]](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio`Mono [#9989](https://github.com/NuGet/Home/issues/9989)のパフォーマンスの問題
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | SemanticVersion クラスの TypeConverter を追加する- [#9125](https://github.com/NuGet/Home/issues/9125)


## <a name="feedback-welcome"></a>フィードバックの開始

お客様のフィードバックは Microsoft にとって重要です。  このリリースに問題がある場合は、GitHub の [問題](https://github.com/NuGet/Home/issues) と [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) で既存の問題を確認してください。  NuGet 内の新しい問題については、 [GitHub の問題](https://github.com/NuGet/Home/issues/new)を報告してください。
NuGet エクスペリエンスに関する一般的な問題については、[**ヘルプ > [問題の報告**] の下にあるお気に入りの IDE の [[問題点の報告](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] オプションを使用してお知らせください。
