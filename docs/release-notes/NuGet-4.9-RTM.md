---
title: NuGet 4.9 RTM リリース ノート
description: NuGet 4.9 のリリース ノートです。既知の問題、バグ修正、新機能、および DCR について示します。
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496464"
---
# <a name="nuget-49-release-notes"></a>NuGet 4.9 リリース ノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 バージョン 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500、2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | N/A | N/A |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 バージョン 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502、2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 バージョン 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>概要:4.9.0 の新機能

* 署名: ClientPolicies において、NuGet.Config に記載されている信頼された作成者とリポジトリのセットの使用を要求することを可能にする - [#6961](https://github.com/NuGet/Home/issues/6961)、[ブログ記事](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* パックにシンボルを含める ".snupkg" ファイルの作成 -- シンボル サーバーの snupkg ファイルを受け入れるための nuget プロトコルを把握できるようプッシュを強化する - [#6878](https://github.com/NuGet/Home/issues/6878)、[ブログ記事](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* NuGet 資格情報プラグイン V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* 自己完結型の NuGet パッケージ - ライセンス - [#4628](https://github.com/NuGet/Home/issues/4628)、[お知らせ](https://github.com/NuGet/Announcements/issues/32)

* PackageReference 上の "GeneratePathProperty" オプトイン メタデータで、"Foo.Bar\1.0\" ディレクトリにパッケージごとの MSBuild プロパティを生成することを可能にする - [#6949](https://github.com/NuGet/Home/issues/6949)

* NuGet の操作での顧客の成功を改善する - [#7108](https://github.com/NuGet/Home/issues/7108)

* ロック ファイルを使った反復可能なパッケージの復元を可能にする - [#5602](https://github.com/NuGet/Home/issues/5602)、[お知らせ](https://github.com/NuGet/Announcements/issues/28)、[ブログ記事](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

* PackageExtraction によって発生した、(WarnAsErrors を介して) エラーに昇格された警告は、抽出されたパッケージを抜けるべきではない - [#7445](https://github.com/NuGet/Home/issues/7445)

* 不正に署名されたパッケージは、最終的にグローバル パッケージ フォルダーに含まれるべきではない - [#7423](https://github.com/NuGet/Home/issues/7423)

* バインド リダイレクトの生成でファサード アセンブリがスキップされるべきではない - [#7393](https://github.com/NuGet/Home/issues/7393)

* VersionRange Equals で浮動小数の範囲が比較されない - [#7324](https://github.com/NuGet/Home/issues/7324)

* 復元: 新しい .NET Core 2.1 の HTTP スタックを使う際のパフォーマンスの低下 - [#7314](https://github.com/NuGet/Home/issues/7314)

* パッケージの更新で PackageReference の PrivateAssets が変更されるべきではない - [#7285](https://github.com/NuGet/Home/issues/7285)

* 署名: パッケージに含まれるパッケージ エントリが多すぎる (> 65534) 場合は、署名を失敗させる必要がある - [#7248](https://github.com/NuGet/Home/issues/7248)

* "dotnet nuget push" コードパスで新しい資格情報プロバイダーをサポートする必要がある - [#7233](https://github.com/NuGet/Home/issues/7233)

* インバリアント カルチャを使ったプラグインの実行をサポートする (docker で起こるように) - [#7223](https://github.com/NuGet/Home/issues/7223)

* nuget ソースの追加で NuGet.config から資格情報を削除するべきではない - [#7200](https://github.com/NuGet/Home/issues/7200)

* devDependency PackageReference のインストールの規定値を excludeassets=compile にする必要がある - [#7084](https://github.com/NuGet/Home/issues/7084)

* migrator オプションを修正してすべてのプロジェクトに対して表示させ、プロジェクトに互換性がない場合はエラーを表示させる - [#6958](https://github.com/NuGet/Home/issues/6958)

* "dotnet add package" では、それが資産ファイルに対して実行する復元をコミットする必要がある - [#6928](https://github.com/NuGet/Home/issues/6928)

* 署名: 署名に関連するエラー メッセージを改善する - [#6906](https://github.com/NuGet/Home/issues/6906)

* [テスト失敗] [zh-TW] パッケージ マネージャー コンソールで文字列 "Package Manager Console" がローカライズされない - [#6381](https://github.com/NuGet/Home/issues/6381)

* VS 内で、"プロジェクト情報が見つかりません" というエラー メッセージをもう少し具体的にする必要がある - [#5350](https://github.com/NuGet/Home/issues/5350)

* nuget パックの nuspec バージョンのタグを誤って使ったときのエラー メッセージが役に立たない - [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR - 署名: NuGet プロトコルのサポート: RepositorySignatures/4.9.0 リソース - [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR - .nupkg.metadata ファイルがパッケージの抽出中に作成されるようになった - "content-hash" を含む - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - Mono での実行中にプラグインの authenticode 検証をスキップする - [#7222](https://github.com/NuGet/Home/issues/7222)

[この 4.9.0 リリースで修正されたすべての問題一覧](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>概要:4.9.1 の新機能

* 新しいコマンド trusted-signers を介して nuget.config への書き込みの読み取りのサポートを追加する - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

* ライセンスのリンクの生成を修正 - [#7515](https://github.com/NuGet/Home/issues/7515)

* 署名の検証に対するエラー コードの回帰 - [#7492](https://github.com/NuGet/Home/issues/7492)

* NuGet.Build.Tasks.Pack パッケージにライセンス情報がない - [#7379](https://github.com/NuGet/Home/issues/7379)

[この 4.9.1 リリースで修正されたすべての問題一覧](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>概要:4.9.2 の新機能

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

* ソース名に空白文字が含まれていると、VS/dotnet.exe/nuget.exe/msbuild.exe で資格情報が使用されない - [#7517](https://github.com/NuGet/Home/issues/7517)

* LicenseAcceptanceWindow と LicenseFileWindow のアクセシビリティの問題 - [#7452](https://github.com/NuGet/Home/issues/7452)

* DateTimeConverter の DateTime.Parse の FormatException の修正 - [#7539](https://github.com/NuGet/Home/issues/7539)

[この 4.9.2 リリースで修正されたすべての問題一覧](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>概要:4.9.3 の新機能

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>"ロック ファイルを使った反復可能なパッケージの復元" に関する問題

* 以前にキャッシュされたパッケージに対して、ハッシュとして動作していないロック モードが正しく計算されない - [#7682](https://github.com/NuGet/Home/issues/7682)

* 復元が `packages.lock.json` ファイル内で定義されているものと別のバージョンに解決される - [#7667](https://github.com/NuGet/Home/issues/7667)

* ProjectReferences が関係していると '--locked-mode / RestoreLockedMode' で実際には発生していない復元の失敗が発生する - [#7646](https://github.com/NuGet/Home/issues/7646)

* MSBuild SDK リゾルバーは SDK パッケージの SHA を検証しようとするが、packages.lock.json を使うと復元に失敗する - [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>"構成可能な信頼ポリシーを使った依存関係のロックダウン" に関する問題
* 署名済みパッケージがサポートされていない間は dotnet.exe で trusted-signers を評価すべきではない - [#7574](https://github.com/NuGet/Home/issues/7574)

* 構成ファイル内での trustedSigners の順序が信頼評価に影響を与える - [#7572](https://github.com/NuGet/Home/issues/7572)

* ISettings を実装できない [信頼ポリシー機能をサポートするための API の設定のリファクタリングによって発生] - [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>"デバッグ エクスペリエンスの向上" に関する問題

* .NET Core グローバル ツールのシンボル パッケージを発行できない - [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>"自己完結型の NuGet パッケージ - ライセンス" に関する問題

* 埋め込みライセンス ファイルを使うとシンボル .snupkg パッケージのビルド中にエラーが発生する - [#7591](https://github.com/NuGet/Home/issues/7591)

[この 4.9.3 リリースで修正されたすべての問題一覧](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>概要:4.9.4 の新機能

* セキュリティ修正プログラム: ~/.nuget 内で作成されたファイルに対するアクセス許可の範囲が広すぎる [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)


## <a name="known-issues"></a>既知の問題

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a>dotnet nuget push --interactive が Mac 上でエラーになる。 - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>懸案事項
`--interactive` 引数が dotnet CLI によって転送されていないため、エラー `error: Missing value for option 'interactive'` が発生します

#### <a name="workaround"></a>回避策
`dotnet restore --interactive` のように、対話型のオプションを使ってその他の任意の dotnet コマンドを実行し、認証します。 そうすると、認証が資格情報プロバイダーによってキャッシュされる可能性があります。 その後、`dotnet nuget push` を実行します。

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>.NET Core SDK によってインストールされる FallbackFolders 内のパッケージがカスタム インストールされ、署名の検証に失敗する。 - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>懸案事項
dotnet.exe 2.x を使って netcoreapp 1.x と netcoreapp 2.x をマルチターゲットにするプロジェクトを復元すると、そのフォールバック フォルダーがファイル フィードとして扱われます。 つまり、復元するときに、NuGet ではフォールバック フォルダーからパッケージを選択し、それをグローバル パッケージ フォルダーにインストールしようと試み、通常の署名の検証を行って、失敗します。

#### <a name="workaround"></a>回避策
`RestoreAdditionalProjectSources` に何も設定しないことで、フォールバック フォルダーの使用を無効にします。 `<RestoreAdditionalProjectSources/>` これは慎重に使う必要があります。フォールバック フォルダーから復元されていたはずの多くのパッケージが、NuGet.org からダウンロードされることになるためです。
