---
title: NuGet 3.5 のベータ版のリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.5 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550685"
---
# <a name="nuget-35-release-notes"></a>NuGet 3.5 のリリース ノート

[NuGet 3.5 RC リリース ノート](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC リリース ノート](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>バグ修正

* パックは、mono で MSBuild 14.1 を使用しない[#3550](https://github.com/NuGet/Home/issues/3550)

* 更新プログラム タブは、代わりに現在インストールされているバージョンの選択を更新する利用可能な最新のバージョンを選択しない[#3498](https://github.com/NuGet/Home/issues/3498)

* MyGet フィード プライベート v2 を認証し、"x は詳細の表示 をクリックするとクラッシュを修正しました- [#3469](https://github.com/NuGet/Home/issues/3469)

* ログ メッセージは、UI - 逆の順序であると思われる[#3446](https://github.com/NuGet/Home/issues/3446)

* 「指定されたパスの形式はサポートされていません -」v3.4.4 - Nuget の復元をスローします[#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet コマンドライン 3.6 ベータ版を考慮しません - Prop 構成リリース - = [#3432](https://github.com/NuGet/Home/issues/3432)

* 大規模なプロジェクトのインストール、Nuget IKVM 低速[#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe 自己保持で更新自体の更新プログラム[#3395](https://github.com/NuGet/Home/issues/3395)

* UNC 共有から 3.5 のインストール/復元が 3.4.4 - からパフォーマンス回帰[#3355](https://github.com/NuGet/Home/issues/3355)

* エラー - net451 プロジェクトのパッケージ管理 UI から Moq をインストールするときに[#3349](https://github.com/NuGet/Home/issues/3349)

* ソリューション レベルでは、[インストール] タブは、パッケージのバージョンを表示しない[#3339](https://github.com/NuGet/Home/issues/3339)

* xproj`project.json`インストール済み タブから更新プログラムが状態を失う[#3303](https://github.com/NuGet/Home/issues/3303)

* NuGet パックを`.csproj`内の空のファイルの要素を無視`.nuspec`ファイル - [#3257](https://github.com/NuGet/Home/issues/3257)

* IIS でホストされる web サイト プロジェクトには、復元が失敗にする必要がありますされません[#3235](https://github.com/NuGet/Home/issues/3235)

* 資格情報のない v2 - v3 エンドポイントにリダイレクトすると、Nuget.Config から取得[#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet の pack が失敗するポータブル アセンブリ メタデータを取得するときに、アセンブリを解決するのには[#3128](https://github.com/NuGet/Home/issues/3128)

* Nuget で見つけることができません`msbuild.exe`mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe パックは、その最初の数値のプレリリース タグを許可しない[#1743](https://github.com/NuGet/Home/issues/1743)

* VS2015E - で nuget パッケージのインストールが失敗する[#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions フィルター ソリューション レベルで作業しない[#333](https://github.com/NuGet/Home/issues/333)

* 復元に同じ項目をランダムに失敗したキーが既に追加されています。 - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nuget.Common でをインストールすることはできません`.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* UI を使用して、V2 ソースを検索する、FindPackagesById が各 ID - に対して 2 回呼び出されます[#2517。](https://github.com/NuGet/Home/issues/2517)

* パッケージがプロジェクト - に依存できない[#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe パック - 除外が記載されていますが、サポートされていません - [#2284](https://github.com/NuGet/Home/issues/2284)

* メッセージ エラーに関する問題の 'contentFiles' セクション`.nuspec`が無効です - [#1686](https://github.com/NuGet/Home/issues/1686)

* パッケージ全体 2 回認証パッケージ ソースのプッシュが常に送信[#1501](https://github.com/NuGet/Home/issues/1501)

* プロジェクトの中に update *.csproj の nuget.exe を呼び出すことがあるない場合に情報が指定されません、 `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` 復元が V2 ソース - から 5 xx ステータス コードに再試行しない[#1217](https://github.com/NuGet/Home/issues/1217)

* 2 つのドットでファイル src で`.nuspec`が動作しない - [#2947](https://github.com/NuGet/Home/issues/2947)

* 暗号化 - を使用したフィードを無視する必要がある CoreCLR 復元[#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe プッシュ - 正しくない資格情報を求める - 403 処理[#2910](https://github.com/NuGet/Home/issues/2910)

* パッケージ マネージャーで NuGet の更新プログラムからプロパティが削除、 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* "NuGet.TeamFoundationServer14"が"NuGet.TeamFoundationServer"- に DLL の名前が変更されたことをロードしようとしている NuGet.PackageManagement.VisualStudio [#2857](https://github.com/NuGet/Home/issues/2857)

* パッケージ マネージャーの UI が新しく表示されない更新バージョン - [#2828](https://github.com/NuGet/Home/issues/2828)

* 更新プログラム パッケージの id を使用しようとしています package.version - ではなくバージョン[#2771。](https://github.com/NuGet/Home/issues/2771)

* プロジェクトで nuget を使用していない場合、nuget 復元 csproj がエラー (`packages.config`または`project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* TFS エラー"[ファイル] ワークスペースに存在できないまたはへのアクセス許可がありません"中にアップグレードまたはアンインストールを TFS ソース管理のソリューション/プロジェクトがバインドされる[#2739](https://github.com/NuGet/Home/issues/2739)

* 更新プログラム パッケージは、- 非対象のパッケージの依存関係を取得しない[#2724](https://github.com/NuGet/Home/issues/2724)

* Nuget パッケージ マネージャー UI の操作でのログの詳細レベルを設定する方法はありません[#2705](https://github.com/NuGet/Home/issues/2705)

* nuget の構成が無効です - VS 2015 の VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) が動作しない - [#2653](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 リリース - をパッケージのビルドを null にする値を取得することはできません[#2648](https://github.com/NuGet/Home/issues/2648)

* VSTS フィードの場合に、復元で Nuget.Config から保存された資格情報が使用されていない[#2647](https://github.com/NuGet/Home/issues/2647)

* cmd dir - ではなくプロジェクト ディレクトリに対する相対パス [dotnet restore]--configfile です[#2639](https://github.com/NuGet/Home/issues/2639)

* バージョンの比較コード - で過剰な割り当て[#2632](https://github.com/NuGet/Home/issues/2632)

* 同じをインストールしようとしています nuget.exe の複数のインスタンスのパッケージ化は並列原因二重書き込み - [#2628。](https://github.com/NuGet/Home/issues/2628)

* 複数プロジェクトの操作 - の依存関係情報がキャッシュされない[#2619](https://github.com/NuGet/Home/issues/2619)

* インストールし、最初のパッケージ フォルダーをチェックせず、ダウンロード パッケージを更新[#2618](https://github.com/NuGet/Home/issues/2618)

* パッケージ ソースの一覧が空の場合は、UI を使用してパッケージ ソースを追加できません (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* デザイン時のファサードに依存するパッケージをインストールするときにエラーは誤解を招く[#2594](https://github.com/NuGet/Home/issues/2594)

* のみ最初のソース -"All"の設定で PackageManager コンソールからパッケージをインストールしようと[#2557](https://github.com/NuGet/Home/issues/2557)

* 最新のベータ版を解凍できません - ModernHttpClient [#2518](https://github.com/NuGet/Home/issues/2518)

* 自作 nuget 3.4.1 - 起動時にクラッシュを VS2015 [#2419](https://github.com/NuGet/Home/issues/2419)

* Update コマンドを i を依頼するいかがの場合、少し冗長になる可能性があります[#2418](https://github.com/NuGet/Home/issues/2418)

* ローカルでビルドされた VSIX は、CI ビルドとして同じ Dll およびファイルが必要です。 - [#2401](https://github.com/NuGet/Home/issues/2401)

* -ビルドで NuGet のダウン グレードの警告を修正[#2396](https://github.com/NuGet/Home/issues/2396)

* 永久にブロックされます (3 回) のパッケージ ソースを認証に失敗した[#2362](https://github.com/NuGet/Home/issues/2362)

* 引数でフィードから nuget v3.3 以降、パッケージをインストールするときにパッケージのコンテンツは正しく復元されません、パッケージが含まれている場合 - NoCache`.nupkg`ファイル - [#2354](https://github.com/NuGet/Home/issues/2354)

* すべてのパッケージ ソースが、1 つのソースから不足しているパッケージで Nuget のインストールが失敗する - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson]UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt;&gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* 1 つのソース - 承認に失敗した場合は、ブロックをインストール[#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` バージョン範囲は-IncludeReferencedProjects バージョン - をオーバーライドする必要があります[#1983](https://github.com/NuGet/Home/issues/1983)

* 更新プログラム パッケージが、「しようとすると依存関係情報を収集する」- 低速 super [#1909](https://github.com/NuGet/Home/issues/1909)

* ステルス ダウン グレードの NuGet パッケージの場合にバッチ更新の依存関係 - [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe の更新プログラムは、アセンブリの厳密な名前とプライベートの属性を削除します。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* 相対ファイル パスの"DefaultPushSource"- [#1746](https://github.com/NuGet/Home/issues/1746)

* 競合回避モジュールのエラー メッセージを向上させる[#1373](https://github.com/NuGet/Home/issues/1373)

* v3 での更新プログラムのパッケージが失敗する - 指定したソースではなくパッケージを使用した[#1013](https://github.com/NuGet/Home/issues/1013)

* パッケージ ソースの相対パスを使用するには - を使用する問題が[#865](https://github.com/NuGet/Home/issues/865)

* NUPKG ファイルに低いバージョンの要件では、間接的な依存関係が既に存在する場合は、プロジェクトから生成された依存関係がありません[#759](https://github.com/NuGet/Home/issues/759)

* プロジェクトを削除する対応する UI ウィンドウを閉じます。 は、プロジェクトの名前変更は、UI ウィンドウを変更できません。 PMC をプロジェクトの名前変更、およびプロジェクトの削除イベントのリッスン注[#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web ワークロード]Razor v3 WSP の作成がハングする - [#3241](https://github.com/NuGet/Home/issues/3241)

* 特定のパッケージのインストール/復元は、「パッケージには、複数の nuspec ファイルが含まれています」。 - [#3231](https://github.com/NuGet/Home/issues/3231)

* 小文字の Id (& a)`packages.config`シナリオ - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5 beta 2]パッケージの復元が失敗する -「レガシ」のパッケージを復元する[#3208](https://github.com/NuGet/Home/issues/3208)

* nuget の pack が強制的に .tt ファイルを何であってもコンテンツのフォルダーに追加[#3203](https://github.com/NuGet/Home/issues/3203)

* ASP.NET web アプリの更新プログラムのパッケージ ファイルに関連する警告が生成されますソース - [#3194。](https://github.com/NuGet/Home/issues/3194)

* nuget パック csproj (で`project.json`) packOptions と JSON ファイルの所有者がない場合のクラッシュ[#3180](https://github.com/NuGet/Home/issues/3180)

* 用の nuget パック`project.json`概要、作成者、所有者などのような packOptions タグは無視[#3161](https://github.com/NuGet/Home/issues/3161)

* NuGet.Packaging.PhysicalPackageFile.GetStream - 経由で NullReferenceException [#3160](https://github.com/NuGet/Home/issues/3160)

* 出力内の依存関係を無視する NuGet の pack`.nuspec`の`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* プロジェクトの破損した状態のままロールバックを含む複数のパッケージを更新[#3139](https://github.com/NuGet/Home/issues/3139)

* いずれかの ContentFiles は netstandard プロジェクトには追加されません[#3118](https://github.com/NuGet/Home/issues/3118)

* .Net をターゲットとするライブラリをパッケージ化できません標準- [#3108](https://github.com/NuGet/Home/issues/3108)

* ファイルに新しいプロジェクト]-> [VS2015 で Dev15 - クラス ライブラリ (ポータブル) プロジェクトの失敗]-> [ [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet エラー - 1.0.0-* が有効なバージョン文字列のではない[#3070](https://github.com/NuGet/Home/issues/3070)

* 表示が、インストール パッケージの機能の検索パッケージが失敗する[#3068](https://github.com/NuGet/Home/issues/3068)

* エラー時に - dev15 で"Install-package jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* xproj の nuget パックは既定で無効なターゲット パス - [#3060](https://github.com/NuGet/Home/issues/3060)

* VS 2015 がインストールされている 3 バージョン 3.5.0 のエラーが発生した、NuGet を使用して VS を更新するときに[#3053](https://github.com/NuGet/Home/issues/3053)

* 「Packages.config によってブロック」 `project.json` (UWP、別名、ビルドの統合) プロジェクト - [#3046](https://github.com/NuGet/Home/issues/3046)

* これは公式 preview2 ビルド preview2 003121 にビルド スクリプトによってインストールされている dotnet cli を更新します。 - [#3045](https://github.com/NuGet/Home/issues/3045)

* パッケージ マネージャー UI: パッケージの更新後に新しいバージョンが表示されません- [#3041](https://github.com/NuGet/Home/issues/3041)

* -Apikey コマンド行の削除が読み取り/で送信されない 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* 文字列が正しくありません。 プレリリースの依存関係のパッケージの安定したリリースはありません。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage キャッシュが空のフォルダー - [#3029](https://github.com/NuGet/Home/issues/3029)

* PCL (net46 および windows 10) プロジェクト get NullRef 例外を作成します。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* AllowedVersions 制約 - によって新しいバージョンが制限されていると、Nuget の更新プログラムは情報メッセージを提供する必要があります[#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 の復元に関する問題 - [#2891](https://github.com/NuGet/Home/issues/2891)

* 資格情報プラグインが-1 のエラーで終了しました]、[複数のソースの資格情報プロバイダーを使用する場合にパッケージをダウンロード中にエラー [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` nuget の復元が再コンパイル時に何も変更されました - [#2817](https://github.com/NuGet/Home/issues/2817)

* シンボル パッケージがこれまでがないインストールまたは更新 - で使用される[#2807](https://github.com/NuGet/Home/issues/2807)

* VS が repositoryPath 内の環境変数をサポートしていません (nuget.exe が) - [#2763](https://github.com/NuGet/Home/issues/2763)

* パッケージ マネージャー UI でラベル付けされていない Uielement をラベルには、ユーザー補助 - [#2745](https://github.com/NuGet/Home/issues/2745)

* ハイフンでつながれたプロファイルを使用した移植可能なフレームワークは拒否されます。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet パッケージ マネージャーで、そのオプションの一覧でパッケージの詳細には適用されませんを明確にするため必要があります`project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe プッシュ/削除は、API キー - を使用しない[#2627](https://github.com/NuGet/Home/issues/2627)

* ロックされているプロパティはロック ファイルから削除[#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 更新が失敗 '... 制約で定義されている packages.config には、この動作ができなくなります '。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* 無効なメッセージがスローされますが存在しないローカル ソースからパッケージをインストールする[#1674](https://github.com/NuGet/Home/issues/1674)

* 「アップグレード可能」フィルターはバージョン制約に違反するアップグレードでは、表示[#1094](https://github.com/NuGet/Home/issues/1094)

* -ネイティブのパッケージを更新できません[#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>フィーチャー

* NuGet - によって追加された参照を false に設定 CopyLocal をサポートして[#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15 - nuget.exe サポート[#1937](https://github.com/NuGet/Home/issues/1937)

* パックのサポート。`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* 実行されているユーザーの操作がある場合は、ユーザーの操作を無効にする- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet のサポートを追加する必要があります`runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* NuGet で不足しているフレームワークの互換性を追加 (これは 3.x で、既に) 2.x - [#2720](https://github.com/NuGet/Home/issues/2720)

* フォールバックのパッケージ フォルダー - サポート[#2899](https://github.com/NuGet/Home/issues/2899)

* 設計および実装ツール パッケージをサポートするには、パッケージの種類の概念[#2476](https://github.com/NuGet/Home/issues/2476)

* グローバル パッケージ フォルダーのパスを取得するための API を追加[#2403](https://github.com/NuGet/Home/issues/2403)

* パックには、SemVer 2.0.0 を有効にする[#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* nuget.exe プッシュのタイムアウト パラメーターは機能しません - [#2785](https://github.com/NuGet/Home/issues/2785)

* パッケージの説明テキストが選択できる - [#1769](https://github.com/NuGet/Home/issues/1769)

* 生成するために nuget.exe を有効にする`.props`と`.targets`ファイル`.nuproj`プロジェクト[#2711](https://github.com/NuGet/Home/issues/2711)

* 機能拡張フレームワークの imports とを比較する API を追加[#2633](https://github.com/NuGet/Home/issues/2633)

* 使用する場合は、依存関係のオプションを非表示に`project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* 詳細な出力 - で nuget.exe のバージョン ヘッダーを印刷[#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet は、ベース dotnet tfm でアップグレード/インストール PCL の問題が生じたり - ユーザーに通知する必要があります[#3138](https://github.com/NuGet/Home/issues/3138)

* Tfm を使用したプロジェクトの不適切なインストールまたはアップグレードを警告する ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* ReShaper と NuGet の更新 - パフォーマンスの問題を修正[#3044](https://github.com/NuGet/Home/issues/3044)

* 追加 netcoreapp11 と netstandard17 サポート - [#2998](https://github.com/NuGet/Home/issues/2998)

* 利用して AssemblyMetadata 属性`.nuspec`トークンの置換 - [#2851](https://github.com/NuGet/Home/issues/2851)
