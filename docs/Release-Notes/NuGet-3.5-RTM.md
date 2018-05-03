---
title: NuGet 3.5 のベータ リリース ノート
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.5 用のリリース ノートです。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-35-release-notes"></a>NuGet 3.5 のリリース ノート

[NuGet 3.5 RC のリリース ノート](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC のリリース ノートには](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>バグ修正

* パックは、mono - に MSBuild 14.1 を使用しない[#3550](https://github.com/NuGet/Home/issues/3550)

* 更新プログラム タブは、代わりに現在インストールされているバージョンの選択を更新する最新バージョンを選択しない[#3498](https://github.com/NuGet/Home/issues/3498)

* フィードの MyGet プライベート v2 を認証し、詳細結果 x [表示] をクリックした後のクラッシュを修正しました- [#3469](https://github.com/NuGet/Home/issues/3469)

* ログ メッセージは、UI の逆の順序でのように見えて[#3446](https://github.com/NuGet/Home/issues/3446)

* 「指定されたパスの形式はサポートされていません -」をスロー v3.4.4 - Nuget 復元[#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 beta を認めません - Prop 構成リリースを = [#3432](https://github.com/NuGet/Home/issues/3432)

* Nuget IKVM 低速に大規模なプロジェクトは、インストール[#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe 自己保持で更新自体の更新[#3395](https://github.com/NuGet/Home/issues/3395)

* UNC 共有から 3.5 のインストール/復元が 3.4.4 - からパフォーマンス回帰[#3355](https://github.com/NuGet/Home/issues/3355)

* エラー - net451 プロジェクトのパッケージ管理 UI から Moq をインストールするときに[#3349](https://github.com/NuGet/Home/issues/3349)

* ソリューション レベルでのインストール タブは、パッケージのバージョンを表示しない[#3339](https://github.com/NuGet/Home/issues/3339)

* xproj`project.json`インストール済み タブから更新プログラムを失った状態 - [#3303](https://github.com/NuGet/Home/issues/3303)

* NuGet パック`.csproj`内の空のファイルの要素を無視`.nuspec`ファイル - [#3257](https://github.com/NuGet/Home/issues/3257)

* IIS でホストされる web サイト プロジェクト原因にはなりません復元が失敗 - [#3235](https://github.com/NuGet/Home/issues/3235)

* 資格情報が v2 - v3 エンドポイントにリダイレクト時に Nuget.Config から取得されない[#3179](https://github.com/NuGet/Home/issues/3179)

* ポータブル アセンブリ メタデータを取得するときに、アセンブリを解決するのには NuGet のパックが失敗した[#3128](https://github.com/NuGet/Home/issues/3128)

* Nuget を見つけることができません`msbuild.exe`モノラル -  [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe パックは、プレリリース版のタグ番号 - で始まるを許可しない[#1743](https://github.com/NuGet/Home/issues/1743)

* VS2015E - で nuget パッケージのインストールが失敗した[#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions ソリューション レベルでない作業をフィルター処理[#333](https://github.com/NuGet/Home/issues/333)

* 復元にランダムに同じ項目に失敗したキーが既に追加されています。 - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nuget.Common をインストールすることはできません`.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* UI を使用して、V2 のソースを検索、FindPackagesById が各 ID - に対して 2 回呼び出されます[#2517。](https://github.com/NuGet/Home/issues/2517)

* パッケージのプロジェクトに依存できません[#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe パック - 除外が記載されていますが、サポートされていません - [#2284](https://github.com/NuGet/Home/issues/2284)

* メッセージ エラーに関する問題の 'コンテンツ ファイル' セクション`.nuspec`無効です - [#1686](https://github.com/NuGet/Home/issues/1686)

* パッケージ全体 2 回の認証パッケージ ソースのプッシュが常に送信[#1501](https://github.com/NuGet/Home/issues/1501)

* について指定されていませんプロジェクトの中に nuget.exe 更新 *.csproj を呼び出すことがないとき、 `packages.config`  -  [#1496。](https://github.com/NuGet/Home/issues/1496)

* `packages.config` 5 xx 状態コード - V2 のソースからの復元を再試行しません[#1217](https://github.com/NuGet/Home/issues/1217)

* 2 つのドットでファイル src で`.nuspec`それでも - [#2947](https://github.com/NuGet/Home/issues/2947)

* 暗号化に使用したフィードを無視する必要がある CoreCLR 復元[#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe プッシュに正しくの入力を求めていません資格情報 - 403 処理[#2910](https://github.com/NuGet/Home/issues/2910)

* パッケージ マネージャーで NuGet の更新プログラムがからプロパティを削除、 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio"NuGet.TeamFoundationServer14"が"NuGet.TeamFoundationServer"- に DLL の名前が変更されたことをロードしようとしました[#2857。](https://github.com/NuGet/Home/issues/2857)

* パッケージ マネージャーの UI が新しく表示されない更新バージョン - [#2828](https://github.com/NuGet/Home/issues/2828)

* 更新プログラム パッケージのパッケージ id を使用しようとしています package.version - ではなくバージョン[#2771。](https://github.com/NuGet/Home/issues/2771)

* nuget 復元 csproj は、プロジェクトは、nuget を使用していない場合、エラーを必要があります (`packages.config`または`project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* TFS エラー"[ファイル]、ワークスペースに存在することできませんまたはへのアクセス許可がありません"中にアップグレードまたはアンインストール ソリューション/プロジェクトが TFS ソース コントロールにバインドされると[#2739](https://github.com/NuGet/Home/issues/2739)

* 更新プログラム パッケージが目標ではないパッケージの依存関係を取得しない[#2724](https://github.com/NuGet/Home/issues/2724)

* Nuget パッケージ マネージャーの UI アクションのログ詳細レベルを設定する方法はありません[#2705](https://github.com/NuGet/Home/issues/2705)

* nuget 構成が無効です - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) は機能しません - [#2653](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 リリースの値を取得することはできません null にする - パッケージのビルドで[#2648](https://github.com/NuGet/Home/issues/2648)

* 復元 VSTS フィード - Nuget.Config から保存された資格情報が使用されていない[#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet 復元]--configfile は cmd dir - の代わりにプロジェクト ディレクトリに対する相対[#2639](https://github.com/NuGet/Home/issues/2639)

* バージョンの比較コード - 内の過剰割り当て[#2632](https://github.com/NuGet/Home/issues/2632)

* 同じをインストールしようとしています nuget.exe の複数のインスタンスのパッケージ化は並列原因二重書き込み - [#2628。](https://github.com/NuGet/Home/issues/2628)

* 複数プロジェクトの操作 - の依存関係情報はキャッシュされません[#2619](https://github.com/NuGet/Home/issues/2619)

* インストールし、更新プログラムのダウンロード パッケージを最初のパッケージ フォルダーをチェックせず[#2618](https://github.com/NuGet/Home/issues/2618)

* パッケージ ソースの一覧が空の場合は、UI を使用してパッケージのソースを追加できません (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* デザイン時のファサード - に依存しているパッケージをインストールしようとしましたエラーは誤解を招く[#2594。](https://github.com/NuGet/Home/issues/2594)

* だけ最初のソースの設定"All"PackageManager コンソールから、パッケージをインストールしようと[#2557](https://github.com/NuGet/Home/issues/2557)

* 最新のベータ版がない解凍 ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* ビルドされた自己 NuGet 3.4.1 - 起動時 VS2015 クラッシュ[#2419](https://github.com/NuGet/Home/issues/2419)

* 更新コマンドの場合は i を依頼する... - より詳細可能性があります[#2418](https://github.com/NuGet/Home/issues/2418)

* ローカルでビルドされた VSIX は、CI ビルドとして同じ Dll とファイルが必要です。 - [#2401](https://github.com/NuGet/Home/issues/2401)

* ビルド - NuGet ダウン グレードの警告を修正[#2396](https://github.com/NuGet/Home/issues/2396)

* パッケージ ソース (3 倍) の認証に失敗したがブロックされている永続 - [#2362](https://github.com/NuGet/Home/issues/2362)

* 引数でフィード nuget v3.3 + からパッケージをインストールするときにパッケージの内容は正しく復元されません - NoCache パッケージが含まれている`.nupkg`ファイル - [#2354](https://github.com/NuGet/Home/issues/2354)

* すべてのパッケージ ソースが見つからない、1 つのソースからパッケージを使用して Nuget のインストールが失敗した場合 - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson]UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt です。&gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* 1 つのソースの承認に失敗した場合は、ブロックをインストール[#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` バージョン範囲は-IncludeReferencedProjects バージョン - をオーバーライドする必要があります[#1983](https://github.com/NuGet/Home/issues/1983)

* 更新プログラム パッケージ super 速度の遅い -「しようとした依存関係情報を収集する」- [#1909](https://github.com/NuGet/Home/issues/1909)

* 鋭いのダウン グレードの NuGet パッケージの場合にバッチ更新の依存関係 - [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe の更新プログラムは、アセンブリの厳密な名前およびプライベートの属性を削除します。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource"- の相対ファイル パス[#1746](https://github.com/NuGet/Home/issues/1746)

* 競合回避モジュール エラー メッセージを向上させる[#1373](https://github.com/NuGet/Home/issues/1373)

* -指定したソースでないパッケージ v3 での更新プログラム パッケージが失敗した[#1013](https://github.com/NuGet/Home/issues/1013)

* パッケージ ソースの相対パスを使用するにを使用する問題が[#865](https://github.com/NuGet/Home/issues/865)

* NUPKG ファイルを下位バージョンの要件では、間接的な依存関係が既に存在する場合は、プロジェクトから生成された依存関係がありません[#759](https://github.com/NuGet/Home/issues/759)

* 対応する UI ウィンドウを閉じますプロジェクトの削除は、プロジェクトの名前を変更する名前は変更されません UI ウィンドウ。 注 PMC をプロジェクトの名前変更、およびプロジェクトの削除イベントのリッスン[#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web ワークロード]Razor v3 WSP の作成がハングする - [#3241](https://github.com/NuGet/Home/issues/3241)

* 「パッケージには、複数の nuspec ファイルが含まれています」で特定のパッケージのインストール/復元が失敗します。 - [#3231](https://github.com/NuGet/Home/issues/3231)

* 小文字の Id (& a)`packages.config`シナリオ - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5 beta2]パッケージの復元が「レガシ」パッケージの復元に失敗した[#3208](https://github.com/NuGet/Home/issues/3208)

* nuget パックでは、新機能に関係なくコンテンツ フォルダーを .tt ファイルを強制的に追加[#3203](https://github.com/NuGet/Home/issues/3203)

* ASP.NET web アプリの更新プログラム パッケージには、ファイルに関連する警告が生成されますソースの構成 - [#3194。](https://github.com/NuGet/Home/issues/3194)

* nuget パック csproj (で`project.json`) packOptions と JSON ファイルの所有者が存在しない場合のクラッシュ[#3180](https://github.com/NuGet/Home/issues/3180)

* 用の nuget パック`project.json`概要、作成者、所有者などのような packOptions タグは無視[#3161](https://github.com/NuGet/Home/issues/3161)

* NuGet.Packaging.PhysicalPackageFile.GetStream - を介して NullReferenceException [#3160](https://github.com/NuGet/Home/issues/3160)

* 出力内の依存関係が NuGet パックには無視されます`.nuspec`の`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* ロールバックを含む複数のパッケージの更新結果が、プロジェクト、破損状態 - [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandard プロジェクトのいずれかの下にあるコンテンツ ファイルは追加されません[#3118](https://github.com/NuGet/Home/issues/3118)

* ターゲットを .Net ライブラリをパッケージすることはできません標準正しく - [#3108](https://github.com/NuGet/Home/issues/3108)

* ファイルに新しいプロジェクト]-> [クラス ライブラリ (ポータブル) プロジェクトが失敗する VS2015 と Dev15 - -> [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet エラー - 1.0.0-* は有効なバージョン文字列ではありません[#3070。](https://github.com/NuGet/Home/issues/3070)

* 表示、パッケージのインストールの動作の失敗した Find-package [#3068](https://github.com/NuGet/Home/issues/3068)

* エラー時"Install-package jquery.validation"dev15 -  [#3061](https://github.com/NuGet/Home/issues/3061)

* xproj の nuget パックは既定で無効なターゲット パス - [#3060](https://github.com/NuGet/Home/issues/3060)

* VS 2015 がインストールされているバージョン 3.5.0 エラーが発生した、NuGet を使用すると上の 3 を更新するときに[#3053](https://github.com/NuGet/Home/issues/3053)

* 「Packages.config によってブロック」 `project.json` (UWP、別名のビルドと統合) プロジェクト - [#3046](https://github.com/NuGet/Home/issues/3046)

* これは、公式 preview2 ビルド preview2 003121 をビルド スクリプトがインストールされている dotnet cli を更新します。 - [#3045](https://github.com/NuGet/Home/issues/3045)

* パッケージ マネージャーの UI: パッケージを更新した後に新しいバージョンが表示されない- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey delete コマンド ラインでは、読み取り/に送信されない 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* 不適切な文字列: 安定したパッケージのリリースのプレリリースの依存関係のないです。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage キャッシュが空のフォルダーの[#3029](https://github.com/NuGet/Home/issues/3029)

* PCL (net46 および windows 10) プロジェクト get NullRef 例外を作成します。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* AllowedVersions 制約 - によってより新しいバージョンが制限されているときに、Nuget の更新プログラムは情報メッセージを提供する必要があります[#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 の復元に関する問題 - [#2891](https://github.com/NuGet/Home/issues/2891)

* 資格情報のプラグインは、エラー-1 で終了しましたエラーをダウンロードする、複数のソースの資格情報プロバイダーを使用する場合にパッケージ化/ [#2885。](https://github.com/NuGet/Home/issues/2885)

* `project.json` nuget の復元時に変更されました - 何も再コンパイルの原因[#2817](https://github.com/NuGet/Home/issues/2817)

* シンボルしていないパッケージを今まででインストールまたは更新に使用される[#2807](https://github.com/NuGet/Home/issues/2807)

* VS が repositoryPath 内の環境変数をサポートしていません (nuget.exe は) - [#2763](https://github.com/NuGet/Home/issues/2763)

* パッケージ マネージャー UI のラベル付けされていない Uielement をラベルにユーザー補助 - [#2745](https://github.com/NuGet/Home/issues/2745)

* ハイフンでつながれたプロファイルでポータブル フレームワークは拒否されます。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet パッケージ マネージャーで、詳細には適用されませんパッケージでそのオプションの一覧を明確にするため必要があります`project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe プッシュ/削除の API キーを使用しない[#2627](https://github.com/NuGet/Home/issues/2627)

* ロックされているプロパティ ファイルから削除、ロックの[#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 更新で失敗 ' 追加の制約 で定義されている packages.config には、この動作ができなくなります '。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* 無効なメッセージのスローを存在しないローカル ソースからパッケージをインストールする[#1674](https://github.com/NuGet/Home/issues/1674)

* 「アップグレード」使用可能なフィルターは、表示のバージョンの制約に違反するアップグレード[#1094](https://github.com/NuGet/Home/issues/1094)

* ネイティブなパッケージを更新できません[#1291。](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>フィーチャー

* 追加された NuGet - によって参照に false に設定 CopyLocal をサポートして[#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15 - nuget.exe サポート[#1937](https://github.com/NuGet/Home/issues/1937)

* サポートをパックします。`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* 実行されているユーザーの操作がある場合は、ユーザーの操作を無効にする- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet のサポートを追加する必要があります`runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* NuGet で見つからない framework の互換性を追加 (既ににある 3.x) 2.x - [#2720](https://github.com/NuGet/Home/issues/2720)

* -フォールバック パッケージ フォルダーへのサポート[#2899](https://github.com/NuGet/Home/issues/2899)

* 設計およびツール パッケージをサポートするには、パッケージの種類の概念を実装[#2476](https://github.com/NuGet/Home/issues/2476)

* グローバルのパッケージ フォルダーへのパスを取得するために API を追加[#2403](https://github.com/NuGet/Home/issues/2403)

* パックに SemVer 2.0.0 を有効にする[#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* nuget.exe プッシュ タイムアウト パラメーターは機能しません - [#2785](https://github.com/NuGet/Home/issues/2785)

* パッケージの説明テキストが選択可能にする必要があります[#1769](https://github.com/NuGet/Home/issues/1769)

* 生成するために nuget.exe を有効にする`.props`と`.targets`ファイル`.nuproj`プロジェクト[#2711](https://github.com/NuGet/Home/issues/2711)

* フレームワークのインポートとを比較する API の機能を拡張する[#2633](https://github.com/NuGet/Home/issues/2633)

* 使用する場合は、依存関係のオプションを非表示に`project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* 詳細な出力に nuget.exe バージョン ヘッダーを印刷[#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet は、ユーザーがいるベース dotnet tfm でアップグレード/インストール PCL に問題が発生の通知する必要があります[#3138](https://github.com/NuGet/Home/issues/3138)

* Tfm を使用したプロジェクトの不適切なインストールまたはアップグレードに警告する ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* ReShaper と NuGet の更新のパフォーマンスの問題を修正[#3044](https://github.com/NuGet/Home/issues/3044)

* Netcoreapp11 と netstandard17 サポート - 追加[#2998](https://github.com/NuGet/Home/issues/2998)

* 活用 AssemblyMetadata 属性`.nuspec`トークンの置換 - [#2851](https://github.com/NuGet/Home/issues/2851)
