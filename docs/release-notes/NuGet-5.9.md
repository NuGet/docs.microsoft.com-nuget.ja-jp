---
title: NuGet 5.9 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.9 のリリースノート。
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 1152af99cf1421918a42d0d1faa33f1452f54a8f
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323883"
---
# <a name="nuget-59-release-notes"></a>NuGet 5.9 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン | 利用可能な .NET SDK |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Visual Studio 2019 と .net Core ワークロードと共にインストールされる
  
> [!NOTE]
> Visual Studio 16.9、MSBuild 16.9、および .NET 5.0.200 + には NuGet.exe 5.9 以降が必要です。

## <a name="summary-whats-new-in-59"></a>概要: 5.9 の新機能

* 事前に選択されたパッケージを使用してパッケージマネージャーの UI を起動し、パッケージの依存関係の [更新] コンテキストメニュー項目を追加 [#10378](https://github.com/NuGet/Home/issues/10378)

    ![パッケージの "更新" エクスペリエンスを右クリックします。](media/releasenotes-59-update.png)

* ソリューションレベルパッケージマネージャー UI の [プロジェクト] リストの [バージョン] 列に、要求されたバージョン (フローティングバージョンまたはバージョン範囲の要求を含む) を表示し [#9827](https://github.com/NuGet/Home/issues/9827)

    ![ソリューションレベルのパッケージマネージャー UI で要求されたバージョン](media/releasenotes-59-requested-version.png)

* パッケージマネージャー UI の IntelliCode パッケージの提案 A/B テスト[#10053](https://github.com/NuGet/Home/issues/10053)としてリリース

* `.nupkg.metadata`インストールソースを含むようにファイルを拡張する- [#10354](https://github.com/NuGet/Home/issues/10354)

* パックタスクの実行中に特定の TFMs のビルド出力を除外する新しい msbuild プロパティを導入する- [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**DCRs (デザイン変更要求):**

* 最新のパッケージバージョンがインストールされている場合、下位アイコンアイコンは直観的ではありません。 以前の緑のティックは完全に [#9789](https://github.com/NuGet/Home/issues/9789)

* Nuget デバッグの詳細度は、パッケージの送信元- [#3055](https://github.com/NuGet/Home/issues/3055)

* NuGet パックでは、バージョン番号にドットが含まれている誤った省略をキャッチする必要があり [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM]中央推移的な依存関係のピン留めを無効にする- [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: TFM- [#9441](https://github.com/NuGet/Home/issues/9441)がない場合にエラーを生成する

* 復元ログ中にパッケージ contenthash をログに記録する (抽出中)- [#10384](https://github.com/NuGet/Home/issues/10384)

* ソリューションオープン[#9986](https://github.com/NuGet/Home/issues/9986)で復元を呼び出す従来の PR プロジェクトの事前登録メカニズムを実装する

* パッケージマネージャーで複数のソースが選択されている場合は、NuGet パッケージレコメンダーを使用する必要があります- [#10433](https://github.com/NuGet/Home/issues/10433)

* 通常の詳細度で復元する場合は、パッケージの復元元のソースをログに記録し [#10461](https://github.com/NuGet/Home/issues/10461)

**バグ**

* INuGetPackageFileService-Codespaces とスタンドアロン[#10151](https://github.com/NuGet/Home/issues/10151)のイメージと埋め込みライセンスを取得します。

* VS OE: IProjectMetadataContextInfo にフォーマッタがありません- [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf][#10002](https://github.com/NuGet/Home/issues/10002) centralTransitiveDependencyGroups に書き込まれる情報を減らします。

* プロジェクトが読み込まれなかったことが原因でスローされる復元操作は `NoOp` 、テレメトリ- [#9985](https://github.com/NuGet/Home/issues/9985)として報告されます。

* 特定のカラーパレットを持つアイコンにより、PM UI がクラッシュし [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-Perf]CPVM 情報を追加するときに PackageSpec clone を減らす- [#10003](https://github.com/NuGet/Home/issues/10003)

* PM UI-asyncify アイコン読み込み- [#10009](https://github.com/NuGet/Home/issues/10009)

* PM UI でアイコンの Url を読み込むときの UI の遅延 [#8505](https://github.com/NuGet/Home/issues/8505)

* BitmapSource と WPF UI スレッドでのスレッドアフィニティ- [#9161](https://github.com/NuGet/Home/issues/9161)

* Packastool が[targetframework](https://github.com/NuGet/Home/issues/10097) framework NU5128 の場合の警告の警告

* カスタマイズされたビルドでの OutputPath logic in Pack ターゲットは正常に機能しません- [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: クライアント[#10141](https://github.com/NuGet/Home/issues/10141)での IServiceBroker インスタンスのキャッシュ

* PM UI からのアンインストールの NuGetProjectActions を作成する並列操作- [#9956](https://github.com/NuGet/Home/issues/9956)

* パフォーマンス: 従来のプロジェクトおよび PR 以外のプロジェクトのために、Uide を使用して Get/Async を縮小する方法については、 [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg``複数のファイル[#4393](https://github.com/NuGet/Home/issues/4393)をプッシュしません。

* リダイレクトされると、出力は macOS で80文字でラップされ [#10198](https://github.com/NuGet/Home/issues/10198)

* -Source #9406 で復元が失敗する <Relative Path>  -  [](https://github.com/NuGet/Home/issues/9406)

* netcoreapp 5.0-windows はラウンドトリップせず、プラットフォーム情報を解析しません- [#10177](https://github.com/NuGet/Home/issues/10177)

* カスタム CPS プロジェクトを復元するには、AssemblyReferences プロジェクト機能が必要です。 - [#8071](https://github.com/NuGet/Home/issues/8071)

* ライセンスとアイコンファイルの存在チェックでは、常に大文字と小文字を区別する比較を使用する必要があり [#9817](https://github.com/NuGet/Home/issues/9817)

* DotnetCLiToolReference の復元では、no op プロジェクトの数/uptodateprojectscount- [#10038](https://github.com/NuGet/Home/issues/10038)

* ダークテーマで [NuGet パッケージマネージャーの形式を選択] ダイアログボックスを使用して移動するときに、パッケージ形式のダッシュラインボックスを表示するのは困難です。 [#9729](https://github.com/NuGet/Home/issues/9729)

* #10314 からの推移的なフレームワーク参照を除外する `CollectFrameworkReferences`  -  [](https://github.com/NuGet/Home/issues/10314)

* 比較子の静的プロパティはべき等 [#10339](https://github.com/NuGet/Home/issues/10339)

* 内部コントラクトアセンブリの読み込みの解決 (RPS の修正または例外の取得)- [#9919](https://github.com/NuGet/Home/issues/9919)

* GetService を GetServiceAsync に置き換え、パート 1- [#10362](https://github.com/NuGet/Home/issues/10362)

* インストールされていないパッケージをインストールすることはできません- [#7466](https://github.com/NuGet/Home/issues/7466)

* 静的 msbuild グラフ復元- [#10335](https://github.com/NuGet/Home/issues/10335) MSBuildStartupDirectory に関する必要なログ記録の解除

* PrivateAssets とマークされている ProjectReferences のプロジェクトの依存関係は、[最新の情報に更新するまでロックファイルに含めないでください。 [#8565](https://github.com/NuGet/Home/issues/8565)

* 無効なデータを含む SDK プロジェクトは、VS- [#10406](https://github.com/NuGet/Home/issues/10406)に復元エラーが表示されない

* NU1004 と netstandard2 プロジェクトが混在しているソリューションを[#9623](https://github.com/NuGet/Home/issues/9623) LockedMode を使用して cmd 行から復元する場合の

* パッケージには、依存関係パッケージを通じて現在のプロジェクトのパッケージに取り込まれたコンテンツが含まれます (SDK ベースのプロジェクトのみ)- [#8867](https://github.com/NuGet/Home/issues/8867)

* NuGet の VS 機能拡張 API エラーのテレメトリを追加する- [#10062](https://github.com/NuGet/Home/issues/10062)

* デバッグ機能を向上させるために、静的なグラフの復元で GenerateRestoreGraphFile を追加します。  - [#10365](https://github.com/NuGet/Home/issues/10365)

* NuGet パッケージマネージャーを開くことができません- [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/ナレーターは、"Apache-2.0" リンク[#10425](https://github.com/NuGet/Home/issues/10425)の "ライセンス" ラベルを読み取っていません

* 最新のステータスバーメッセージは、VS [#9402](https://github.com/NuGet/Home/issues/9402)では十分ではありません

* の packages.config package.lock.jsは不適切なターゲットフレームワークを使用して [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: #10439 からテレメトリを修正します https://github.com/NuGet/NuGet.Client/pull/3786  -  [](https://github.com/NuGet/Home/issues/10439)

* "RestoreLockedMode"- [#8973](https://github.com/NuGet/Home/issues/8973)を有効にした後にソリューションをビルドすると、エラー NU1004 が消えます

* 逆方向の PMUI を使用して tab キーを移動すると、前方の方向がミラー化され [#10234](https://github.com/NuGet/Home/issues/10234)

* 実験用インスタンスで PMUI をデバッグすると、SolutionView から ProjectView [#10416](https://github.com/NuGet/Home/issues/10416)に InvalidCastException がスローされることがある

* 既定のバージョンは、[参照] タブで非推奨のパッケージをクリックすると null になり [#10380](https://github.com/NuGet/Home/issues/10380)

* Visual Studio の NuGet マネージャーは、フォーカスが再度表示されたときに再読み込みを行い [#4176](https://github.com/NuGet/Home/issues/4176)

* IPackageSourceProvider2 と関連する型の削除- [#10098](https://github.com/NuGet/Home/issues/10098)

* パッケージ ' NameOfPackage ' は、プロジェクト内の ' all ' フレームワークと互換性がありません- [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync が不要な NuGetVersion を比較する- [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet。クライアントは ManagedImageMonikers と KnownMonikers を使用して置き換える必要があります- [#9977](https://github.com/NuGet/Home/issues/9977)

* 非推奨のアイコンは、[参照] タブで非推奨のパッケージのバージョンと重複しています- [#10452](https://github.com/NuGet/Home/issues/10452)

* PackageReference NU1604 のエラー処理は VS とコマンドラインで異なります (Restore & Package Manager UI)- [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: 必要なフォーマッタが登録されていません- [#10467](https://github.com/NuGet/Home/issues/10467)

* Net45 からターゲットフレームワークとしてを削除します[#10470](https://github.com/NuGet/Home/issues/10470) 。

* 実装-新しいテレメトリを追加して、PMC と Powershell の使用状況に関連するイベントを追跡します。 - [#10142](https://github.com/NuGet/Home/issues/10142)

* パッケージマネージャー UI で更新できるパッケージが複数ある場合、[変更のプレビュー] ウィンドウに表示されるパッケージは1つだけです [#10483](https://github.com/NuGet/Home/issues/10483)

* 複数の対象を持つプロジェクトをパッキングする場合は、空の frameworkReferences グループを生成する必要があり [#10218](https://github.com/NuGet/Home/issues/10218)

* [更新] タブでパッケージのチェックボックスが表示されるのは、青い/Blue (エクストラコントラスト)/明るいテーマを使用してタブ間を移動するときに、ダッシュラインボックスを使用することです。 [#8963](https://github.com/NuGet/Home/issues/8963)

* [更新] タブのチェックボックスは、スクリーンリーダーでは適切に機能しません- [#10449](https://github.com/NuGet/Home/issues/10449)

* PMUI で更新すると、オブジェクト参照がオブジェクトのインスタンスに設定されません- [#9882](https://github.com/NuGet/Home/issues/9882)

* 実装-新しいテレメトリを追加して、PMC と Powershell の使用状況に関連するイベントを追跡します。 - [#10478](https://github.com/NuGet/Home/issues/10478)

* [#10480](https://github.com/NuGet/Home/issues/10480) V2FeedPackageInfo でのコピー/貼り付けエラー

* NuGetPackageFileService の修正 - 使い捨て可能なメモリストリームに を使用 - [#10503](https://github.com/NuGet/Home/issues/10503)

**[このリリースで修正された問題の一覧 - 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[このリリースのコミットの一覧 - 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>コミュニティからの投稿

この NuGet リリースをすばらしいものにするのに役立ったすべての共同作成者に感謝します。

|担当者|Prs|発行|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | V2FeedPackageInfo のコピー/貼り付けエラー - [#10480](https://github.com/NuGet/Home/issues/10480)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | PrivateAssets="All" 属性でパッケージが参照されている場合のテスト[が見つからない](https://github.com/NuGet/Home/issues/10397)- #10397
[marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | 複数のパッケージをプッシュするサポートの追加 - [#4393](https://github.com/NuGet/Home/issues/4393)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | アセンブリの署名が無効になっていると、NuGet ライブラリのビルドが破損する - [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | 貢献しているドキュメントをクリーンアップする - [#10399](https://github.com/NuGet/Home/issues/10399)
[1000000000](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | ライセンスとアイコン ファイルの存在チェックでは、常に大文字と小文字を区別する比較を使用する必要[があります](https://github.com/NuGet/Home/issues/9817)- #9817
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | DecodePixelWidth を使用する場合の WPF の問題を回避するには、BitmapCreateOptions.IgnoreColorProfile を使用します - [#10037](https://github.com/NuGet/Home/issues/10037)
[bjorkjorm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Windows SDK 10 のリンクは、NuGet.Client Contribution ガイド[-](https://github.com/NuGet/Home/issues/10099) #10099
[bjorkjorm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | NuGet.Client デバッグ ガイドで相対リンクが破損している[-](https://github.com/NuGet/Home/issues/10100) #10100
[Malmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | テスト フィクスチャと関連するコードを改善する - [#9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | 出力は、リダイレクト時に macOS で 80 文字でラップされます - [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | NuGet.PackageManagement を新しいパッケージとして使用[.NET Standardする](https://github.com/NuGet/Home/issues/6150)- #6150
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | パック タスク中に特定の tfms のビルド出力を除外する新しい msbuild プロパティを[導入する](https://github.com/NuGet/Home/issues/10396)- #10396

## <a name="summary-whats-new-in-591"></a>概要: 5.9.1 の新機能

* "dotnet nuget remove source nuget.org" が初めて動作しない[-](https://github.com/NuGet/Home/issues/10745) #10745
* Linux では既定の検証を無効にし、Windows では既定[で有効にする](https://github.com/NuGet/Home/issues/10713)- #10713

**[このリリースで修正された問題の一覧 - 5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[このリリースのコミットの一覧 - 5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="known-issues"></a>既知の問題

### <a name="nuget-59-pack-raises-null-reference-exception---10685"></a>nuget 5.9 パックでは例外が発生 `Null Reference` します。 - [#10685](https://github.com/NuGet/Home/issues/10685)

#### <a name="issue"></a>問題
ファイルを使用する場合、 を対象とするプロジェクトにを追加せずに明示的なアセンブリ参照が指定されている場合、バージョンによって `pack` `.nuspec` `NuGet 5.9` `null reference` [](../reference/nuspec.md#explicit-assembly-references) `reference groups` 例外が発生します `multiple frameworks` 。

#### <a name="workaround"></a>回避策
`nuget.exe` [5.8.1 または 以外の](https://dist.nuget.org/win-x86-commandline/v5.8.1/nuget.exe)最新バージョンを使用します `5.9.1` 。

## <a name="feedback-welcome"></a>フィードバックへようこそ

お客様のフィードバックは Microsoft にとって重要です。  このリリースで問題が発生した場合は [、GitHub](https://github.com/NuGet/Home/issues) の問題と既存の問題 [Visual Studio Developer Community確認してください](https://developercommunity.visualstudio.com/) 。  NuGet 内の新しい問題については [、GitHub の問題 を報告してください](https://github.com/NuGet/Home/issues/new)。
NuGet エクスペリエンスに関する一般的な問題については、[](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)お気に入りの IDE の [問題の報告] オプションの [ヘルプ] の [問題の報告] >**お知らせください**。
