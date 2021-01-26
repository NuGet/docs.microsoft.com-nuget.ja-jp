---
title: NuGet 3.5 RTM リリース ノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.5 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776355"
---
# <a name="nuget-35-release-notes"></a>NuGet 3.5 リリースノート

[NuGet 3.5-RC リリースノート](../release-notes/nuget-3.5-RC.md)  | [NuGet 4.0 RC リリースノート](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>バグの修正

* パッケージが mono [#3550](https://github.com/NuGet/Home/issues/3550)で MSBuild 14.1 を使用していない

* [更新] タブでは、更新に使用できる最新のバージョンが選択されていません。現在インストールされているバージョンを選択し [#3498](https://github.com/NuGet/Home/issues/3498)

* プライベート v2 MyGet feed を認証し、[その他の結果を表示] をクリックした後にクラッシュを修正する- [#3469](https://github.com/NuGet/Home/issues/3469)

* ログメッセージは、UI [#3446](https://github.com/NuGet/Home/issues/3446)の逆の順序であるように見えます。

* v 3.4.4-Nuget の復元で "指定されたパスの形式はサポートされていません"- [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 beta は、Prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)を優先しません

* 大規模なプロジェクトでの Nuget IKVM の遅いインストール- [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe 更新プログラム-自己更新 (自己更新)- [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 UNC 共有からのインストール/復元は[#3355](https://github.com/NuGet/Home/issues/3355) 3.4.4 からのパフォーマンスの回帰を持つ

* Net451 プロジェクトのパッケージ管理 UI から Moq をインストールするときにエラーが発生する- [#3349](https://github.com/NuGet/Home/issues/3349)

* ソリューションレベルの [インストール] タブにパッケージのバージョンが表示されない- [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` 更新プログラムがインストールされたタブから状態が失われる- [#3303](https://github.com/NuGet/Home/issues/3303)

* の NuGet パック `.csproj` は `.nuspec` 、ファイル[#3257](https://github.com/NuGet/Home/issues/3257)内の空のファイル要素を無視します

* IIS でホストされている web サイトプロジェクトで復元が失敗することはありません- [#3235](https://github.com/NuGet/Home/issues/3235)

* V3 エンドポイントが v2- [#3179](https://github.com/NuGet/Home/issues/3179)にリダイレクトされると、Nuget.Config から資格情報が取得されない

* ポータブルアセンブリメタデータを取得するときに NuGet パックがアセンブリを解決できない- [#3128](https://github.com/NuGet/Home/issues/3128)

* Nuget `msbuild.exe` が Mono [#3085](https://github.com/NuGet/Home/issues/3085)で見つかりません

* nuget.exe パックでは、番号で始まるプレリリースタグを許可しません- [#1743](https://github.com/NuGet/Home/issues/1743)

* [#1298](https://github.com/NuGet/Home/issues/1298) VS2015E で nuget パッケージのインストールが失敗する

* allowedVersions フィルターがソリューションレベルで機能していません- [#333](https://github.com/NuGet/Home/issues/333)

* 同じキーを持つ項目が既に追加されているため、復元はランダムに失敗します。 - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nuget をインストールできません。 `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)に共通

* UI を使用して V2 ソースを検索する場合、FindPackagesById は各[#2517](https://github.com/NuGet/Home/issues/2517) ID に対して2回呼び出されます。

* パッケージはプロジェクトに依存できません- [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe pack-Exclude はドキュメントに記載されていますが、サポートされていません- [#2284](https://github.com/NuGet/Home/issues/2284)

* の ' contentFiles ' セクションが無効な場合のエラーメッセージに関する問題 `.nuspec` - [#1686](https://github.com/NuGet/Home/issues/1686)

* プッシュは、常にパッケージ全体を、認証されたパッケージソースと共に2回送信します- [#1501](https://github.com/NuGet/Home/issues/1501)

* プロジェクトに #1496 がないときに nuget.exe update * .csproj を呼び出すときに情報が指定されませんでした `packages.config`  -  [](https://github.com/NuGet/Home/issues/1496)

* `packages.config` 復元では、V2 ソースからの5xx 状態コードでは再試行されません- [#1217](https://github.com/NuGet/Home/issues/1217)

* のファイル src の2つのドット `.nuspec` が機能しません- [#2947](https://github.com/NuGet/Home/issues/2947)

* CoreCLR 復元では、暗号化を使用したフィードを無視する必要があり [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe push 403 処理-資格情報の入力を誤って要求しています- [#2910](https://github.com/NuGet/Home/issues/2910)

* パッケージマネージャーを使用した NuGet の更新では、 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)からプロパティを削除します

* VisualStudio は "TeamFoundationServer14" の読み込みを試行しますが、その DLL 名は "NuGet. Teamfound Ationserver"- [#2857](https://github.com/NuGet/Home/issues/2857)に変更されました

* パッケージマネージャー UI に新しく更新されたバージョンが表示されない- [#2828](https://github.com/NuGet/Home/issues/2828)

* packageid の代わりにを使用しようとしているパッケージのバージョン- [#2771](https://github.com/NuGet/Home/issues/2771)

* プロジェクトが nuget (または) を使用していない場合は、nuget の restore .csproj がエラーになります ( `packages.config` または `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)

* Tfs エラー "[ファイル] がワークスペースに見つかりません。または、ソリューション/プロジェクトが TFS ソース管理にバインドされている場合、アップグレードまたはアンインストール中に、このファイルにアクセスするためのアクセス許可がありません- [#2739](https://github.com/NuGet/Home/issues/2739)

* 更新プログラムパッケージは、ターゲットでないパッケージの依存関係を取得しません- [#2724](https://github.com/NuGet/Home/issues/2724)

* Nuget パッケージマネージャーの UI 操作のログの詳細レベルを設定する方法はありません- [#2705](https://github.com/NuGet/Home/issues/2705)

* nuget の構成が無効です-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* () の DefaultPushSource `NuGetDefaults.Config` `ProgramData\NuGet` が動作しません [#2653](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 のリリース-パッケージビルドで値を null にすることはできません- [#2648](https://github.com/NuGet/Home/issues/2648)

* 復元では、VSTS フィードの Nuget.Config から保存された資格情報が使用されていません- [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--configfile は、cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)の代わりにプロジェクトディレクトリを基準としています

* バージョン comparsion の過剰な割り当て (コード[#2632](https://github.com/NuGet/Home/issues/2632) )

* 同じパッケージを並行してインストールしようとしている nuget.exe の複数のインスタンスによって、ダブル書き込みが [#2628](https://github.com/NuGet/Home/issues/2628)

* 複数プロジェクトの操作の依存関係情報はキャッシュされていません- [#2619](https://github.com/NuGet/Home/issues/2619)

* パッケージフォルダーを最初にチェックせずに、ダウンロードパッケージをインストールおよび更新する [#2618](https://github.com/NuGet/Home/issues/2618)

* パッケージソースリストが空の場合、UI (NuGet 3.4. x) を介してパッケージソースを追加することはできません- [#2617](https://github.com/NuGet/Home/issues/2617)

* デザイン時のファサードに依存するパッケージをインストールしようとすると[#2594](https://github.com/NuGet/Home/issues/2594) 、誤解を招くエラーが発生する

* "All" に設定して、パッケージを "All" に設定してパッケージをインストールすると、最初のソース[#2557](https://github.com/NuGet/Home/issues/2557)のみが試行される

* ModernHttpClient を解凍していない最新[#2518](https://github.com/NuGet/Home/issues/2518)のベータ版

* 自己ビルド型の NuGet [#2419](https://github.com/NuGet/Home/issues/2419) 3.4.1 を使用した起動時の VS2015 クラッシュ

* Update コマンドを実行するように要求すると、さらに詳細な情報が表示される場合があります...- [#2418](https://github.com/NuGet/Home/issues/2418)

* ローカルでビルドされた VSIX は、CI ビルドと同じ Dll およびファイルを持つ必要があります。 - [#2401](https://github.com/NuGet/Home/issues/2401)

* ビルド[#2396](https://github.com/NuGet/Home/issues/2396)で NuGet ダウングレードの警告を修正する

* パッケージソース (3 回) の認証に失敗すると、無期限にブロックされ [#2362](https://github.com/NuGet/Home/issues/2362)

* パッケージに `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354)ファイルが含まれている場合、NoCache という引数を使用して nuget v 3.3 + フィードからパッケージをインストールすると、パッケージコンテンツが正しく復元されない

* すべてのパッケージソースと共に Nuget をインストールしますが、1つのソースからのパッケージが見つからない場合は、 [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson]Uide のレイアウト: nuget.packagemanagement.visualstudio.dll!VisualStudio. VSMSBuildNuGetProjectSystem + * lt; &gt;c__DisplayClass_0 + &lt; &lt; addreference &gt; b__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)

* 1つのソースが承認に失敗した場合のインストールブロック- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`バージョン範囲は IncludeReferencedProjects バージョン- [#1983](https://github.com/NuGet/Home/issues/1983)をオーバーライドする必要があります

* Update-Package super 低速-"依存関係情報を収集しようとしています"- [#1909](https://github.com/NuGet/Home/issues/1909)

* 依存関係をバッチ更新するときの NuGet ステルスダウンパッケージパッケージ- [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe の更新では、アセンブリの厳密な名前とプライベート属性が削除されます。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource" の相対ファイルパス- [#1746](https://github.com/NuGet/Home/issues/1746)

* 競合回避モジュールのエラーメッセージの改善- [#1373](https://github.com/NuGet/Home/issues/1373)

* v3 の更新パッケージが、指定されたソース[#1013](https://github.com/NuGet/Home/issues/1013)にないパッケージで失敗する

* パッケージソースに相対パスを使用すると、- [#865](https://github.com/NuGet/Home/issues/865)を使用すると問題が発生する

* 古いバージョンの要件を持つ間接的な依存関係が既に存在する場合、プロジェクトから生成された依存関係が見つからない- [#759](https://github.com/NuGet/Home/issues/759)

* プロジェクトを削除すると、対応する UI ウィンドウが閉じますが、プロジェクトの名前を変更しても UI ウィンドウの名前は変更されません。 PMC がプロジェクトの名前変更とプロジェクト削除イベントをリッスンすることに注意してください- [#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web ワークロード]Razor v3 WSP ハングの作成- [#3241](https://github.com/NuGet/Home/issues/3241)

* 特定のパッケージのインストール/復元が失敗し、"パッケージに複数の nuspec ファイルが含まれています。" というエラーが表示されます。 - [#3231](https://github.com/NuGet/Home/issues/3231)

* 小文字の Id & `packages.config` シナリオ- [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5-beta2]パッケージの復元で "従来の" パッケージの復元に失敗する- [#3208](https://github.com/NuGet/Home/issues/3208)

* nuget パックによって、 [#3203](https://github.com/NuGet/Home/issues/3203)に関係なく、コンテンツフォルダーに .tt ファイルが強制的に追加される

* ASP.NET web アプリの更新プログラムパッケージによって、ファイルに関連する警告が生成されます: ソース- [#3194](https://github.com/NuGet/Home/issues/3194)

* `project.json`JSON ファイル内に packOptions と owner がない場合[#3180](https://github.com/NuGet/Home/issues/3180) 、nuget pack .csproj (を含む) がクラッシュする

* の nuget パックでは `project.json` 、summary、authors、owners などの packOptions タグが無視されます。 [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException を使用して、System.resources.resourcemanager.getstream- [#3160](https://github.com/NuGet/Home/issues/3160)

* NuGet パック `.nuspec` は `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)の出力の依存関係を無視します

* ロールバックを使用して複数のパッケージを更新すると、プロジェクトが破損した状態のままになります- [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandard.library プロジェクトでは、ContentFiles は追加されません- [#3118](https://github.com/NuGet/Home/issues/3118)

* .Net Standard をターゲットとするライブラリをパッケージ化できません- [#3108](https://github.com/NuGet/Home/issues/3108)

* ファイル > 新しいプロジェクト-> クラスライブラリ (ポータブル) プロジェクトが VS2015 と[#3094](https://github.com/NuGet/Home/issues/3094) Dev15 で失敗する

* nuGet エラー-1.0.0-* は有効なバージョン文字列ではありません- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package を表示できませんが、Install-Package 動作 [#3068](https://github.com/NuGet/Home/issues/3068)

* Dev15 で "パッケージのインストール-検証" を行うとエラー [#3061](https://github.com/NuGet/Home/issues/3061)が発生する

* xproj の nuget パックは、既定で無効なターゲットパスを示しています- [#3060](https://github.com/NuGet/Home/issues/3060)

* NuGet バージョンを使用する VS で VS 2015 update 3 をインストールすると3.5.0 エラーが発生する- [#3053](https://github.com/NuGet/Home/issues/3053)

* 「 `project.json` (UWP、a. k. a build integrated) プロジェクト」の「packages.config によってブロックされました」- [#3046](https://github.com/NuGet/Home/issues/3046)

* ビルドスクリプトによってインストールされた dotnet cli を preview2-003121) に更新します。これは、公式の preview2 ビルドです。 - [#3045](https://github.com/NuGet/Home/issues/3045)

* パッケージマネージャー UI: パッケージを更新した後、新しいバージョンは表示されません- [#3041](https://github.com/NuGet/Home/issues/3041)

* -Delete コマンドラインの ApiKey は3.5.0 で読み取り/送信されません- [#3037](https://github.com/NuGet/Home/issues/3037)

* 文字列が正しくありません: パッケージの安定したリリースでは、プレリリースの依存関係を設定することはできません。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage cache が空のフォルダーを残す- [#3029](https://github.com/NuGet/Home/issues/3029)

* PCL (net46 および windows 10) プロジェクトを作成すると、NullRef 例外が生成されます。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* 新しいバージョンが allowedVersions 制約によって制限されている場合、Nuget 更新プログラムは情報メッセージを提供する必要があり [#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 の復元に関する問題- [#2891](https://github.com/NuGet/Home/issues/2891)

* 複数の[#2885](https://github.com/NuGet/Home/issues/2885)ソースで資格情報プロバイダーを使用しているときに、資格情報プラグインがエラーで終了しました-1/エラーが発生したパッケージのダウンロード中

* `project.json`何も変更されなかった場合に、nuget の復元によって再コンパイル[#2817](https://github.com/NuGet/Home/issues/2817)が行われる

* シンボルパッケージは、インストールまたは更新[#2807](https://github.com/NuGet/Home/issues/2807)では使用しないでください

* VS は repositoryPath の環境変数をサポートしていません (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)

* パッケージマネージャー UI でラベル付けされていない UIElements にアクセシビリティ対応のラベルを付けます- [#2745](https://github.com/NuGet/Home/issues/2745)

* ハイフネーションされたプロファイルを含むポータブルフレームワークは拒否されます。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet パッケージマネージャーは、[パッケージの詳細] のオプション一覧が適用されないことを明確にする必要があり `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* プッシュ/削除 nuget.exe は API キーを使用しません- [#2627](https://github.com/NuGet/Home/issues/2627)

* ロックファイルからロックされたプロパティを削除し [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 の更新が ' 追加の制約で失敗しました...packages.config で定義されているため、この操作を実行できません。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 存在しないローカルソースからパッケージをインストールすると、偽のメッセージ[#1674](https://github.com/NuGet/Home/issues/1674)がスローされる

* [使用可能なアップグレード] フィルターにより、バージョンの制約に違反するアップグレードが表示されます- [#1094](https://github.com/NuGet/Home/issues/1094)

* ネイティブパッケージを更新できません- [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>特徴

* NuGet によって追加された参照に対して CopyLocal を false に設定することをサポートする [#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15 [#1937](https://github.com/NuGet/Home/issues/1937)の nuget.exe サポート

* のパックサポート。`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* ユーザー操作が実行されているときにユーザー操作を無効にする- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet は #2782 のサポートを追加する必要があります `runtimes/{rid}/nativeassets/{txm}/`  -  [](https://github.com/NuGet/Home/issues/2782)

* NuGet 2.x (既に 3. x に存在する) で[#2720](https://github.com/NuGet/Home/issues/2720) 、互換性のフレームワークを追加します。

* フォールバックパッケージフォルダーのサポート- [#2899](https://github.com/NuGet/Home/issues/2899)

* ツールパッケージをサポートするためのパッケージの種類の概念を設計および実装する- [#2476](https://github.com/NuGet/Home/issues/2476)

* API を追加して、グローバルパッケージフォルダーへのパスを取得します- [#2403](https://github.com/NuGet/Home/issues/2403)

* パック[#3356](https://github.com/NuGet/Home/issues/3356)で semver 2.0.0 を有効にする

## <a name="dcrs"></a>DCR

* nuget.exe のプッシュタイムアウトパラメーターが機能しません- [#2785](https://github.com/NuGet/Home/issues/2785)

* パッケージの説明テキストは選択可能である必要があります- [#1769](https://github.com/NuGet/Home/issues/1769)

* `.props` `.targets` プロジェクトのファイルとファイルを生成するための nuget.exe を有効に `.nuproj` [#2711](https://github.com/NuGet/Home/issues/2711)

* 拡張 API を追加して、フレームワークとインポート[#2633](https://github.com/NuGet/Home/issues/2633)を比較する

* #2486 の使用時に依存関係オプションを非表示にする `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)

* 詳細な出力[#1887](https://github.com/NuGet/Home/issues/1887)に nuget.exe バージョンヘッダーを出力する

* NuGet では、dotnet tfm ベースの PCL でのアップグレードまたはインストールによって問題が発生する可能性があることをユーザーに知らせる必要があり [#3138](https://github.com/NuGet/Home/issues/3138)

* [プロジェクトに対して無効なインストール/アップグレードを警告する]: "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* ReShaper と NuGet の更新プログラム[#3044](https://github.com/NuGet/Home/issues/3044)のパフォーマンスの問題を修正します。

* Netcoreapp11 と netstandard17 のサポートを追加する- [#2998](https://github.com/NuGet/Home/issues/2998)

* トークンの置換に AssemblyMetadata 属性を利用する `.nuspec` - [#2851](https://github.com/NuGet/Home/issues/2851)
