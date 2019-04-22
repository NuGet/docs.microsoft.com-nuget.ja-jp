---
title: NuGet 5.0 RTM リリース ノート
description: 既知の問題、バグの修正、新機能、および Dcr を含む NuGet 5.0 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921586"
---
# <a name="nuget-50-release-notes"></a>NuGet 5.0 のリリース ノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>.NET Core ワークロードと共に Visual Studio 2019 のインストール 

<sup>2</sup>.NET Core ワークロードと共に Visual Studio 2019 と省略可能なインストールとして利用可能

## <a name="summary-whats-new-in-50"></a>概要:5.0 の新機能新機能

* 復元するためのサポート[ソリューションをフィルター処理された](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019)で Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` フォルダーにより、パッケージをホスト プロジェクトのターゲット/プロパティを推移的に投稿する[#6091](https://github.com/NuGet/Home/issues/6091)
* Iv api は NuGet の PackageReference シナリオのサポート強化[#7005](https://github.com/NuGet/Home/issues/7005)、 [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` 非推奨 - [#7928](https://github.com/NuGet/Home/issues/7928)
* Gen 1 の資格情報プロバイダー プラグインに置き換えられました[Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin)は間もなく非推奨 - [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* NoOp 復元を行うときに避ける *. obj ディレクトリ - dgspec.json 書き込み[#7854](https://github.com/NuGet/Home/issues/7854)

* ~/.Nuget 内で作成されたファイルに対するアクセス許可が開きすぎる[#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` 認証 - の必要なソースを使用しない[#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller - パッケージに含まれないプロジェクトの呼び出しを参照して常に使用 packages.config、PackageReference - に既定値が設定されている場合でも[#7005](https://github.com/NuGet/Home/issues/7005)

* PMC:更新プログラム パッケージでは、除外されるパッケージが失敗した (「できませんパッケージが見つかりません」) を再インストールします。 - [#7268](https://github.com/NuGet/Home/issues/7268)

* リポジトリと VSIX - サード パーティに関する通知を追加[#7409](https://github.com/NuGet/Home/issues/7409)

* -指定されたバージョンがないときに、最新バージョンをインストールする必要があります NuGet.VisualStudio.IVsPackageInstaller.InstallPackage [#7493](https://github.com/NuGet/Home/issues/7493)

* --interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)

* ロック ファイルを復元する場合は、NU1603 警告が発生しないでください。 - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet は、最小ログ記録 - 復元中にプロジェクト パスを印刷する必要があります[#7647](https://github.com/NuGet/Home/issues/7647)

* -- dotnet の対話型のサポートは、パッケージを削除する - [#7727](https://github.com/NuGet/Home/issues/7727)

* Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache 必要 - うまく動作するための短いパス[#7770](https://github.com/NuGet/Home/issues/7770)

* ユーザーが特定の msbuild バージョン - 質問されていなかった場合、msbuild の検出パスを優先[#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` 適切な msbuild のバージョンを一覧表示する必要があります[#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): error :パスの一部が見つかりませんでした '/tmp/NuGetScratch - mono - [#7793。](https://github.com/NuGet/Home/issues/7793)

* 復元が不必要にマシン キャッシュ - で参照されるパッケージのすべてのバージョンの内容を列挙[#7639](https://github.com/NuGet/Home/issues/7639)

* MSBuild の自動検出は 16.0 を常に選択インストール VS 2019 プレビュー - 後[#7621](https://github.com/NuGet/Home/issues/7621)

* ソリューションに dotnet リスト パッケージ フレームワークの重複するエントリを出力する[#7607](https://github.com/NuGet/Home/issues/7607)

* 例外「空のパス名は有効な」old IVsPackageInstaller.InstallPackage を呼び出し元がプロジェクトし、パッケージ フォルダーが存在しません。 - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16.0 の NuGet UI には、色の問題のため、読み取り不可能なタブ[#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt clarification on - [#7629](https://github.com/NuGet/Home/issues/7629)

* 復元は、- の種類を判断するためのグローバル パッケージ フォルダーを列挙する不必要に[#7596](https://github.com/NuGet/Home/issues/7596)

* エラー一覧 ウィンドウ - にロック ファイル強制からエラーが表示されます[#7429](https://github.com/NuGet/Home/issues/7429)

* NuGet.Configuration の問題を修正[#7326](https://github.com/NuGet/Home/issues/7326)

* MSBuild の更新のインストールに合わせて場所 - [#7325](https://github.com/NuGet/Home/issues/7325)

* 開発の依存関係 - をする必要があります NuGet.Build.Tasks.Pack [#7249](https://github.com/NuGet/Home/issues/7249)

* などのパック拡張機能ポイントを追加するデバッグ シンボルの[#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` (浮動バージョンが使用されている場合も含む) の作成の nupkg で依存関係のバージョンの範囲を保持する必要があります[#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` ユーザー レベルの構成があります - ソースと認証済みのソースでは失敗[#7209](https://github.com/NuGet/Home/issues/7209)

* パック BuildActions - コンテンツのファイルのセットを制限せず[#7155](https://github.com/NuGet/Home/issues/7155)

* 警告 AssetTargetFallback が成功する必要があります ProjectReference を使用してください。 - [#7137](https://github.com/NuGet/Home/issues/7137)

* CPS (CommonProjectSystem) - を呼び出すときに、スレッドの問題によりデッドロック[#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` ローカル設定で指定されたソースのグローバル構成から資格情報を使用しない[#6935](https://github.com/NuGet/Home/issues/6935)

* MEF が非同期で呼び出されると、スレッドの問題のコード パス - [#6771](https://github.com/NuGet/Home/issues/6771)

* 署名: エラーが報告されずコール スタックの 2 回[#6455](https://github.com/NuGet/Home/issues/6455)

* エラー - を表示する署名証明書を信頼されていないと、署名付きパッケージをインストールする必要があります[#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet の復元を正しく Noop obj ディレクトリ - を共有する 2 つのプロジェクトと[#6114](https://github.com/NuGet/Home/issues/6114)

* PAT では使用できません`dotnet restore`- 認証済みのフィードからパッケージを使用した linux [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet 復元が失敗するため、無効になっているマシン ワイド フィード - [#5410](https://github.com/NuGet/Home/issues/5410)

**Dcr**

* Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Gen1 資格情報プラグインの非推奨の警告を追加[#7819](https://github.com/NuGet/Home/issues/7819)
 
* 署名: RepositorySignatures/5.0.0 リソースを使用してすべてのパッケージのリポジトリとしてのクライアント検証を要求するリポジトリを有効になっている署名-- [#7759](https://github.com/NuGet/Home/issues/7759)

* limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet のために、VSIX の 16.0 ビルドのクリーンアップ) Net472 - 対象[#7143](https://github.com/NuGet/Home/issues/7143)

* PMC:Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)

* NetStandard 2.1 - make NetCoreApp 3.0 マップ[#7762](https://github.com/NuGet/Home/issues/7762)

* NuGet.* パッケージ - に netstandard2.0 サポートを追加[#6516](https://github.com/NuGet/Home/issues/6516)

* パッケージ作成者ビルド アセットの推移的な動作の定義を許可する[#6091](https://github.com/NuGet/Home/issues/6091)

* VS 2019 ソリューション フィルター機能をサポートします。 また、ソリューションではなくプロジェクトまたはアンロードされたプロジェクトをサポートします。 CLI または VS) (完全なソリューションを最初に復元する必要があります[#5820](https://github.com/NuGet/Home/issues/5820)

* (変更) - TFM を使用して .NET 4.7.2 を必要とする NuGet 5.0 アセンブリ[#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData NuGet.Packaging からパブリック型である必要があります。 Spdx から取り込まれたライセンス メタデータを更新します。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 削除の設定の廃止された Api - [#7294](https://github.com/NuGet/Home/issues/7294)

* 1 システムでの回避策復元タイムアウト cpu - [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet.config の資格情報がある場合でも、NuGet は NTLM auth を優先 - 資格情報の認証の種類のフィルターを構成オプションを追加する[#5286](https://github.com/NuGet/Home/issues/5286)

* PackageReference (一致する Packages.Config 機能) - の EmbedInteropTypes を有効にする[#2365](https://github.com/NuGet/Home/issues/2365)

**[このリリースでは、5.0 RTM で修正されたすべての問題の一覧](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a>既知の問題

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK によってインストールされる FallbackFolders 内のパッケージがカスタム インストールされ、署名の検証に失敗する。 - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>懸案事項
dotnet.exe 2.x を使って netcoreapp 1.x と netcoreapp 2.x をマルチターゲットにするプロジェクトを復元すると、そのフォールバック フォルダーがファイル フィードとして扱われます。 つまり、復元するときに、NuGet ではフォールバック フォルダーからパッケージを選択し、それをグローバル パッケージ フォルダーにインストールしようと試み、通常の署名の検証を行って、失敗します。<br>
#### <a name="workaround"></a>回避策
フォールバックのフォルダーの使用状況を無効に設定して、 `RestoreAdditionalProjectSources` nothing に。

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

フォールバック フォルダーから復元されるパッケージは NuGet.org からダウンロードするよう注意して使用します。
