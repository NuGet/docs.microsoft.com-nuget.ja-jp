---
title: NuGet 4.0 RC リリース ノート
description: 既知の問題、バグ修正、追加された機能、DCR を含む NuGet 4.0 RTM のリリース ノート。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: f1c5408f75966068e8fa11e63118426bbf562047
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-40-rtm-release-notes"></a>NuGet 4.0 RTM リリース ノート

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には NuGet 4.0 が付属しています。NuGet 4.0 には .NET Core のサポートが追加され、品質の改善とパフォーマンスの向上が図られています。 このリリースでは、PackageReference のサポート、MSBuild ターゲットとしての NuGet コマンド、バックグラウンド パッケージの復元など、いくつかの改善点もあります。

## <a name="known-issues"></a>既知の問題

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>複数のプロジェクト参照が 1 つのソリューションの別のプロジェクトを参照しているとき、NuGet の復元が失敗することがある

#### <a name="issue"></a>懸案事項

あるソリューションで大文字/小文字の区別または相対パスが異なる同じプロジェクトが参照されているとき、NuGet 復元が失敗することがあります。 [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>回避策

大文字/小文字または相対パスをすべてのプロジェクト参照で同じになるように修正します。

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>パッケージ マネージャー コンソールの使用中、'Enter' キーが機能しない

#### <a name="issue"></a>懸案事項

パッケージ マネージャー コンソールで、Enter キーが機能しないことがあります。 その場合、修正プログラムで進捗状況を確認してください。再現手順について役に立つ情報があれば提供してください。 [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>回避策

ソリューションを開く前に、Visual Studio を再起動し、PMC を開いてください。 または、`project.lock.json` を削除し、もう一度復元してください。

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>.NET Core プロジェクトで、署名が無効なアセンブリを含むパッケージを使用するとき、無限の復元ループが発生することがある

#### <a name="issue"></a>懸案事項

無効なアセンブリを含むパッケージを使用するとき、あるいはパッケージ バージョンに 'DateTime' ティッカーが設定されているとき、パッケージ復元が無限ループになることがあります。 [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>回避策

この問題の回避策はありません。

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>NuGet パッケージ マネージャーを使用した DotNetCLITools の表示、追加、更新ができない

#### <a name="issue"></a>懸案事項

NuGet パッケージ マネージャーが表示されず、DotNetCLITools を追加または更新できません。 [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>回避策

DotNetCLIToolReferences はプロジェクト ファイルで手動編集する必要があります。

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>プロジェクトの PackageId プロパティを設定すると、NuGet の復元が失敗する

#### <a name="issue"></a>懸案事項

.NET Core プロジェクトの場合、Visual Studio の NuGet 復元では、プロジェクトの PackageId プロパティが適用されません。 [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>回避策

コマンドラインを使用して復元を実行します。

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>プロジェクトに 'obj' フォルダーがないとき、パッケージ復元に失敗する

#### <a name="issue"></a>懸案事項

'obj' フォルダーが削除されると、Visual Studio は PackageReferences を復元できません。 [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>回避策

'obj' フォルダーを手動作成すると、復元できるようになります。

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>コンソールで Update-Package を使用するとき、パッケージを手動更新できないことがある

#### <a name="issue"></a>懸案事項

Update-Package は、変換されたばかりの PackageReferences プロジェクトに対して、コンソールで 1 回だけ手動で利用できます。 [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>回避策

この問題の回避策はありません。

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>ターゲット フレームワーク バージョンを再ターゲットすると、IntelliSense が不完全になる

#### <a name="issue"></a>懸案事項

Visual Studio では、ターゲット フレームワーク バージョンを再ターゲットすると、IntelliSense が不完全になることがあります。 これは、パッケージ マネージャー形式として PackageReferences を使用しているときに発生します。 [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>回避策

手動で復元します。

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>.NET461 をターゲットにするプロジェクトが .NETStandard をターゲットにする別のプロジェクトを参照するとき、msbuild /t:restore が失敗する

#### <a name="issue"></a>懸案事項

.NET461 をターゲットにする PackageReferenece ベースのプロジェクトが .NETStandard をターゲットにする別の PackageReferenece ベースのプロジェクトを参照するとき、msbuild /t:restore が失敗します。  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>回避策

この問題の回避策はありません。

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>NuGet 4.0 RTM の時間枠で修正された問題

[NuGet 4.0 RC のリリースノート](../release-notes/nuget-4.0-RC.md) - NuGet 4.0 RC で修正されたすべての問題が掲載されています

### <a name="features"></a>フィーチャー

- NuGet.Core.sln の文字列をローカライズする - [#2041](https://github.com/NuGet/Home/issues/2041)

- NuGet で強制的に Web アプリケーション プロジェクトを LSL モードに読み込む - [#4258](https://github.com/NuGet/Home/issues/4258)

- AutoReferenced PackageReference で、"sdk がインストールされている" パッケージの UI のバージョン変更をブロックする機能をサポートする - [#4044](https://github.com/NuGet/Home/issues/4044)

- 任意のプロジェクトの依存関係に対して PackageSpec.Version を正しく伝える (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)

- コマンドラインから `.csproj` への参照を削除するためのサポート - [#4101](https://github.com/NuGet/Home/issues/4101)

- PackageReference プロジェクト (通常と xplat) と Lightweight ソリューション読み込みの復元をサポートする - [#4003](https://github.com/NuGet/Home/issues/4003)

- コマンドラインからの `.csproj` への参照を追加する機能のサポート - [#3751](https://github.com/NuGet/Home/issues/3751)

- `packages.config` or `project.json` の NuGet 復元のライトウェイト ソリューション ロードのサポート  - [#3711](https://github.com/NuGet/Home/issues/3711)

- nuget で生成されたターゲット ファイルの contentFiles のサポート - [#3683](https://github.com/NuGet/Home/issues/3683)

- MSBuild を使用して Mac 上で nuget.exe の検証の Mono CI を確立する - [#3646](https://github.com/NuGet/Home/issues/3646)

- v2 NuGet.Core 依存関係から NuGet を移動する - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>バグ

- Visual Studio の NuGet 復元で、プロジェクトの PackageId プロパティが適用されない - [#4586](https://github.com/NuGet/Home/issues/4586)

- vsix パッケージにパッケージを追加するときの NuGet ProjectSystemCache エラー - [#4545](https://github.com/NuGet/Home/issues/4545)

- IncludeSource が複数の TFM を持つプロジェクトで使用されている場合、パックから例外がスローされる - [#4536](https://github.com/NuGet/Home/issues/4536)

- ソリューション全体のパッケージ管理から更新プログラムを使用すると、VS 2017 RC3 がクラッシュする - [#4474](https://github.com/NuGet/Home/issues/4474)

- 新しくインストールしたパッケージをアンインストールできない - [#4435](https://github.com/NuGet/Home/issues/4435)

- PackageRef に移行すると、ハイブリッド ソリューションで復元動作が正常に実行されません - [#4433](https://github.com/NuGet/Home/issues/4433)

- NuGet 操作 (インストール、更新、復元) を開始した直後にビルドすると、VS がハングすることがある - [#4420](https://github.com/NuGet/Home/issues/4420)

- UI ハング - NuGet.SolutionRestoreManager.RestoreManagerPackage の初期化中のデッドロック - [#4371](https://github.com/NuGet/Home/issues/4371)

- パッケージの追加コマンドで、要素ではなく属性としてバージョンが追加される必要がある - [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet
  - dotnetcore Restore foo.sln -- SLN の構成によって復元グラフにプロジェクトの重複が発生する (ただし、構成は異なる) ときに失敗する - [#4316](https://github.com/NuGet/Home/issues/4316)

- コンテンツのみのパッケージ - [#3668](https://github.com/NuGet/Home/issues/3668)

- 既定で、パッケージ形式の選択オプションが無効になっている - [#4468](https://github.com/NuGet/Home/issues/4468)

- パフォーマンス: CreateUAP_CSharp_VS.01.1.Create プロジェクトの Duration_TotalElapsedTime が 3,153.570 ミリ秒 (149.1%) 遅くなった。 ベースライン 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- パフォーマンス: ManagedLangs_CS_DDRIT.0300.Rebuild ソリューションの Duration_TotalElapsedTime が 1.5 秒遅くなった。 ベースライン 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- マルチ TFM プロジェクトで候補表示が失敗する - [#4419](https://github.com/NuGet/Home/issues/4419)

- パフォーマンス: WebForms_DDRIT.1200.Close Solution の VM_ImagesInMemory_Total_devenv は 3.000 カウント (0.5%) 低下しました。 ベースライン 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - netcoreapp1.1 をターゲットとするときのパックの警告 - [#4397](https://github.com/NuGet/Home/issues/4397)

- 空の ASP.NET Core Web アプリケーションに NuGet パッケージを追加しようとすると、PathTooLongException が発生する - [#4391](https://github.com/NuGet/Home/issues/4391)

- パックの実行頻度が高すぎる -- dotnet
  - ターゲット "Pack" が関係するターゲット依存関係グラフに循環依存の関係が存在するため、dotnetcore pack が失敗する - [#4381](https://github.com/NuGet/Home/issues/4381)

- パックの実行頻度が高すぎる -- NuGet パッケージの生成にすべての構成が含まれていない - [#4380](https://github.com/NuGet/Home/issues/4380)

- C++ プロジェクトで packageref を使用して NuGet を追加するときに NullReferenceException が発生する - [#4378](https://github.com/NuGet/Home/issues/4378)

- アクセシビリティ: ナレーターで、パッケージをインストールするプロジェクトを選択するためのチェックボックスが読み上げられない - [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 がときどき VSO/VSTS フィードへの接続に失敗する - VS バグ 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)

- PackagePath が path を "contentFiles" として指定した場合、contentFiles は不適切な場所に出力される - [#4348](https://github.com/NuGet/Home/issues/4348)

- パック ターゲットで、PackageVersion プロパティに VersionSuffix が付加される - [#4324](https://github.com/NuGet/Home/issues/4324)

- パッケージ パスを指定しても dotnet pack で機能しない - [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet から復元中に重複するインポートに関する警告が出力される - [#4304](https://github.com/NuGet/Home/issues/4304)

- 暗い色のテーマの場合、[NuGet パッケージ マネージャーの形式の選択] ダイアログが適切に表示されない - [#4300](https://github.com/NuGet/Home/issues/4300)

- ビルドの復元時に VS がクラッシュする - [#4298](https://github.com/NuGet/Home/issues/4298)

- ターゲット フレームワークに TFM を追加して保存しビルドすると、Visual Studio はデッドロックします。 時間の 10% - [#4295](https://github.com/NuGet/Home/issues/4295)

- プロジェクトのパック化に成功しても、NuGet パックから成功メッセージが出力されない - [#4294](https://github.com/NuGet/Home/issues/4294)

- System.IO.Compression 4.1 が見つからないため、PackTask が失敗する - [#4290](https://github.com/NuGet/Home/issues/4290)

- パックの実行頻度が高すぎる - PackTask がファイル アクセスの競合で頻繁に失敗する - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet で、バックグラウンドの復元中に出力ウィンドウが開く - [#4274](https://github.com/NuGet/Home/issues/4274)

- ServiceProvider を危険な (ハングを引き起こす可能性がある) コーディング パターンとして削除する - [#4268 ](https://github.com/NuGet/Home/issues/4268)

- パフォーマンス/UI ハング - DownloadTimeoutStream の読み取りの改善 - [#4266](https://github.com/NuGet/Home/issues/4266)

- NuGet の復元が完了する前にプロジェクトを閉じると、Visual Studio がデッドロックする - [#4257](https://github.com/NuGet/Home/issues/4257)

- PackTask とパッキングに関する問題 `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] 新しいプロジェクトで NuGet パッケージを解決できない (Visual Studio を再起動する必要がある) - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] 使用可能なパッケージ バージョンが表示される [バージョン] ドロップ ダウンが、選択した NuGet パッケージと同期状態を保つことが困難 - [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client は、デッドロックを防ぐために CPS と対話するときに、CPS JoinableTaskFactory を使用する必要がある - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 がパッケージの `.targets` をアンパックしない - [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - `.csproj` で dotnetcore pack がタイトルをサポートしていない  - [#4150](https://github.com/NuGet/Home/issues/4150)

- VS2017 RC で Install-Package の結果、エラー ダイアログが表示される - [#4127](https://github.com/NuGet/Home/issues/4127)

- UI が候補から CPS 更新プログラムを取得しないため、.NET Core プロジェクトのパッケージの更新が機能しません。 - [#4035](https://github.com/NuGet/Home/issues/4035)

- 未解決の参照警告を改善する - [#3955 ](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - dotnetcore pack - ProjectReference でバージョン情報が失われる - [#3953](https://github.com/NuGet/Home/issues/3953)

- UWP アプリ作成プロジェクトを作成し、総経過時間の回帰をリビルドする - [#3873](https://github.com/NuGet/Home/issues/3873)

- 復元中にエラーが発生した後でも、成功の復元メッセージが表示されます。 - [#3799](https://github.com/NuGet/Home/issues/3799)

- Nuget.CommandLine 3.4.4 を Nuget.org に再発行する - [#2931](https://github.com/NuGet/Home/issues/2931)

- 移行時に、プロジェクトが `project.json` から `.csproj` に変更される --- 復元に失敗する - [#4297](https://github.com/NuGet/Home/issues/4297)

- 新しく作成された xunit テスト プロジェクトで復元に失敗する - [#4296](https://github.com/NuGet/Home/issues/4296)

- コア プロジェクトがハングし、UI が開いたままロックされることがある - [#4269](https://github.com/NuGet/Home/issues/4269)

- ビルド タスクのターゲット ファイルを修正する - [#4267](https://github.com/NuGet/Home/issues/4267)

- 参照先プロジェクトをアンロードするビルド ソリューションの後にエラー リストにエラーが発生する - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: ターゲット "_GenerateRestoreGraphProjectEntry" がプロジェクトに存在しません。 - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: すべてのプロジェクトを選択するとソリューションがクラッシュする NuGet マネージャー UI - [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe の msbuildpath の末尾にスラッシュがあると、msbuildpath が失敗する - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: NuGet の復元で、LinqToTwitter プロジェクトに関するプロジェクト参照の警告を受け取る - [#4156](https://github.com/NuGet/Home/issues/4156)

- `.csproj` のパックに minClientVersion 属性が含まれていない - [#4135](https://github.com/NuGet/Home/issues/4135)

- VS2017 (d15rel 26014.00) で NuGet.Build.Tasks.Pack.dll は遅延署名された状態でリリースされた - [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: CMake 3.7.1 で生成された VS 2015 プロジェクトの復元に失敗する - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: 復元エラーにより、ビルドで発生する詳細なエラー メッセージがあいまいになることがある - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Web サイト プロジェクトの NuGet パッケージを復元するときにエラー "値を null にすることはできません" が発生する - [#4092](https://github.com/NuGet/Home/issues/4092)

- 移行時に NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker で "オブジェクト参照の例外" がスローされる - [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet
  - dotnetcore pack は、パッケージがビルドされたバージョンでツールをパックする必要がある - [#4063](https://github.com/NuGet/Home/issues/4063)

- 新しいバックグラウンド復元で、復元に数秒かかるときに、ステータス バーにミリ秒が書き込まれる - [#4036](https://github.com/NuGet/Home/issues/4036)

- すべてのプロジェクト参照を解決できなかった場合の誤植 - [#4018](https://github.com/NuGet/Home/issues/4018)

- パッケージ参照シナリオで PCM ワークフローを有効にする - [#4016](https://github.com/NuGet/Home/issues/4016)

- パッケージ マネージャーの UI でインストールされたパッケージが見つからない - [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - PackagePath が空の場合、dotnetcore pack が失敗する - [#3993](https://github.com/NuGet/Home/issues/3993)

- マルチ ユーザー シナリオで復元タスクが失敗する - [#3897](https://github.com/NuGet/Home/issues/3897)

- NuGet パック タスクを使用してパックするときに、コンテンツ タイプを変更できない - [#3895](https://github.com/NuGet/Home/issues/3895)

- MsBuild /t:pack について ContentFiles の既定のコピーが正しくない - [#3894](https://github.com/NuGet/Home/issues/3894)

- インストール パッケージの復元で、パッケージの復元メッセージのログが二重に記録される - [#3785](https://github.com/NuGet/Home/issues/3785)

- Guardrails の削除 - "runtimes" セクションの復元を現在のプロジェクトにのみ適用するようにする - [#3768](https://github.com/NuGet/Home/issues/3768)

- パック タスクで、コンテンツ ファイルが 'content/' と 'contentFiles/' の両方に配置される - [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore pack3 で、余計なタグ分割が行われる - [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - dotnetcore pack: パッケージ参照があるプロジェクトのパックで重複インポートの警告が表示される - [#3665](https://github.com/NuGet/Home/issues/3665)

- VS の復元ログ記録が表示されないことがある - [#3633](https://github.com/NuGet/Home/issues/3633)

- nuget locals のヘルプ テキストで、まだパッケージ キャッシュについて言及されている - [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 は PackageReferences を TargetFrameworks と結合する。 - [#3504](https://github.com/NuGet/Home/issues/3504)

- VS "15" Preview 4 dev コマンド プロンプトで、Nuget によって予期しないバージョンの MSBuild が選択される - [#3408](https://github.com/NuGet/Home/issues/3408)

- 失敗した復元でターゲット/プロパティ ファイルを書き出す - [#3399](https://github.com/NuGet/Home/issues/3399)

- VS 15 コマンド プロンプトで実行するときに、復元中の NuGet が、MSBuild と同じ互換 shim を使用しない - [#3387](https://github.com/NuGet/Home/issues/3387)

- VS15 の場合に PackFromProjectWithDevelopmentDependencySet を再び有効にする - [#3272](https://github.com/NuGet/Home/issues/3272)

- Blend と NuGet の問題 - [#4043](https://github.com/NuGet/Home/issues/4043)

- 4.0.0.2067 を CLI と SDK リポジトリに統合して RC2 と共にリリースする - [#4029](https://github.com/NuGet/Home/issues/4029)

- 新しいコア コンソール アプリケーションを作成し、ソリューションを終了し、ソリューションを開き、ソリューションを閉じるときに VS がハングする - [#4008](https://github.com/NuGet/Home/issues/4008)

- d15prerel.25916.01 に対してプロジェクトを開こうとするとハングする - [#3982](https://github.com/NuGet/Home/issues/3982)

- dotnet/nuget.exe のローカル ドキュメント/ヘルプ メッセージの修正 - [#3919](https://github.com/NuGet/Home/issues/3919)

- 末尾または先頭の空白に関する問題の PackTask の検査 - [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet
  - dotnetcore pack が bin ではなく obj からパックを実行する - [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - dotnetcore pack が ProjectReference のバージョンを常に 1.0.0 に設定しているように見える - [#3874](https://github.com/NuGet/Home/issues/3874)

- dotnet
  - dotnetcore pack がプロジェクト参照と <TargetFramework> で失敗する  - [#3865](https://github.com/NuGet/Home/issues/3865)

- ProjectSystemCache.TryGetProjectNameByShortName の LockRecursionException - [#3861](https://github.com/NuGet/Home/issues/3861)

- MSBuild プロパティから空白を削除する - [#3819](https://github.com/NuGet/Home/issues/3819)

- プロジェクトの読み込み時に発生する 2 つのプロジェクト イベントを統合する - [#3759](https://github.com/NuGet/Home/issues/3759)

- `project.assets.json` ファイルの P2P ライブラリのバージョンが正しくない - [#3748](https://github.com/NuGet/Home/issues/3748)

- 応答しないフィードと使用できないパッケージによる復元のクラッシュ - [#3672](https://github.com/NuGet/Home/issues/3672)

- 大量の MSBuild エラー出力で、nuget.exe がハングする可能性がある - [#3572](https://github.com/NuGet/Home/issues/3572)

- Blend のビルド時の復元が、初回は失敗し 2 回目に成功する (VS シナリオは固定) - [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCR

- v2 vsix から v3 vsix への vsix の移行 - [#4196](https://github.com/NuGet/Home/issues/4196)

- MSBuild でロック ファイルへのパスを取得するメカニズムが NuGet に必要 - [#3351](https://github.com/NuGet/Home/issues/3351)

- ビルド アセットを TFM 互換性チェックとアセット ファイルに追加する - [#3296](https://github.com/NuGet/Home/issues/3296)

- パッケージ関連の機能を有効にするためにパック ターゲットに新しい ProjectCapability "パック" を定義する - [#4146](https://github.com/NuGet/Home/issues/4146)

- "GeneratePackageOnBuild" MSBuild プロパティに基づく条件で、ビルド後のターゲットとしてパックを実行する - [#4145](https://github.com/NuGet/Home/issues/4145)

- NuGet プロパティ RestoreProjectStyle を使用して特定の NuGet プロジェクトを作成する - [#4134](https://github.com/NuGet/Home/issues/4134)

- 推移的プロジェクト参照の変更に復元を適応させる - [#4076](https://github.com/NuGet/Home/issues/4076)

- 非 UWP プロジェクトのターゲット ファイルに NuGet プロパティを追加する - [#4030](https://github.com/NuGet/Home/issues/4030)

- UWP TargetPlatformVersion のサポート - [#3923](https://github.com/NuGet/Home/issues/3923)

- プロジェクト参照メタデータを NuGet プロジェクト システムに伝える - [#3922](https://github.com/NuGet/Home/issues/3922)

- パッケージ モードの UI を追加する - [#3921](https://github.com/NuGet/Home/issues/3921)

- 従来の `.csproj` では、NugetTargetMoniker と RuntimeIdentifier を proj/targets に設定する必要がある - [#3854](https://github.com/NuGet/Home/issues/3854)

- 自動復元時にインストール パッケージが重複することがある - [#3836](https://github.com/NuGet/Home/issues/3836)

- VSPackage が読み込まれない場合にコンテキスト メニュー QueryStatus が生成されない - [#3835](https://github.com/NuGet/Home/issues/3835)

- ソリューションの復元とビルドの復元でダイアログが表示され続ける - [#3789](https://github.com/NuGet/Home/issues/3789)

- NuGet.Clients ソリューション ビルドで VSSDK のバージョンを分離する - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>RTM で修正された GitHub の問題へのリンク
[懸案事項リスト 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[懸案事項リスト 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[懸案事項リスト 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[懸案事項リスト 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[懸案事項リスト 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
