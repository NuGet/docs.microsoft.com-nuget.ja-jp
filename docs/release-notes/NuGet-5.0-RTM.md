---
title: NuGet 5.0 RTM リリースノート
description: 既知の問題、バグ修正、新機能、および DCRs を含む NuGet 5.0 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: e4a6be7fb26e3cc4bd297eaf02999f6ac1389b77
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236803"
---
# <a name="nuget-50-release-notes"></a>NuGet 5.0 リリースノート

NuGet 配布の種類:

| NuGet のバージョン | 利用可能な Visual Studio バージョン| 利用可能な .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 バージョン16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。 

<sup>2</sup>.NET Core ワークロードを含む Visual Studio 2019 を使用したオプションのインストールとして利用可能

## <a name="summary-whats-new-in-50"></a>概要: 5.0 の新機能

* Visual Studio 2019 での [フィルター選択](/visualstudio/ide/filtered-solutions?view=vs-2019) されたソリューションの復元のサポート- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` フォルダーを使用すると、パッケージのターゲット/プロパティをホストプロジェクトに推移的に投稿でき [#6091](https://github.com/NuGet/Home/issues/6091)
* NuGet Iv Api での PackageReference シナリオのサポートの向上- [#7005](https://github.com/NuGet/Home/issues/7005)、 [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` は非推奨とされました- [#7928](https://github.com/NuGet/Home/issues/7928)
* Gen 1 Credential Provider プラグインは [gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) に置き換えられており、まもなく非推奨となりました- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ**

* NoOp 復元を実行する場合は、obj ディレクトリへの書き込み時に * .dgspec.jsを避ける- [#7854](https://github.com/NuGet/Home/issues/7854)

* ~/.Nuget の内部で作成されたファイルのアクセス許可がオープン [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` 認証を必要とするソースでは機能しません。 [#7605](https://github.com/NuGet/Home/issues/7605)

* VisualStudio IVsPackageInstaller-既定値が[#7005](https://github.com/NuGet/Home/issues/7005) PackageReference に設定されている場合でも、パッケージ参照のないプロジェクトでを呼び出すと、常に packages.config が使用されます。

* PMC: Update-Package の再インストールが、delisted パッケージで失敗します ("パッケージが見つかりません")。 - [#7268](https://github.com/NuGet/Home/issues/7268)

* リポジトリと VSIX [#7409](https://github.com/NuGet/Home/issues/7409)にサードパーティの通知を追加する

* VisualStudio のバージョンが指定されていない場合、IVsPackageInstaller は最新バージョンをインストールする必要があり [#7493](https://github.com/NuGet/Home/issues/7493)

* --dotnet nuget プッシュ[#7519](https://github.com/NuGet/Home/issues/7519)の対話形式のサポート

* ロックファイルを使用して復元する場合、NU1603 warning を発生させることはできません。 - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet では、最小ログ記録を使用して復元中にプロジェクトパスを印刷しないようにする必要があり [#7647](https://github.com/NuGet/Home/issues/7647)

* --dotnet remove パッケージ[#7727](https://github.com/NuGet/Home/issues/7727)の対話型サポート

* TypeForwardedTo [#7768](https://github.com/NuGet/Home/issues/7768) attrs を使用してを追加します。

* plugins_cache が正常に機能するためには、短いパスが必要です。 [#7770](https://github.com/NuGet/Home/issues/7770)

* ユーザーが特定の msbuild バージョンを要求しなかった場合に、msbuild 検出のパスを優先する- [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` 正しい msbuild バージョンを一覧表示する必要があります- [#7794](https://github.com/NuGet/Home/issues/7794)

* Nuget.exe (498, 5): エラー: パス '/tmp/NuGetScratch ' の一部が見つかりませんでした- [#7793](https://github.com/NuGet/Home/issues/7793)

* 復元では、コンピューターキャッシュ内の参照されているパッケージのすべてのバージョンのコンテンツを不要に列挙します- [#7639](https://github.com/NuGet/Home/issues/7639)

* VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621)をインストールした後、MSBuild の自動検出では常に16.0 が選択されます。

* ソリューションの dotnet list パッケージは、フレームワーク[#7607](https://github.com/NuGet/Home/issues/7607)の重複したエントリを出力します

* 例外 "空のパス名は無効です" は、古いプロジェクトとパッケージフォルダーで IVsPackageInstaller を呼び出すと存在しません。 - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild/t: 最小の復元の詳細は、より少なくする必要があり [#4695](https://github.com/NuGet/Home/issues/4695)

* 色の問題により、VS 16.0 の NuGet UI にタブが読み取られない- [#7735](https://github.com/NuGet/Home/issues/7735)

* Nuget. Core & License.txt の説明- [#7629](https://github.com/NuGet/Home/issues/7629)

* 型[#7596](https://github.com/NuGet/Home/issues/7596)を特定するために、不要な復元のグローバルパッケージフォルダーを復元します

* ロックファイルの適用からのエラーはエラー一覧ウィンドウに表示される必要があります- [#7429](https://github.com/NuGet/Home/issues/7429)

* NuGet.Configuration の問題を修正する- [#7326](https://github.com/NuGet/Home/issues/7326)

* MSBuild に適合するインストール場所の更新- [#7325](https://github.com/NuGet/Home/issues/7325)

* Nuget.exe は開発の依存関係である必要があります- [#7249](https://github.com/NuGet/Home/issues/7249)

* デバッグシンボルを含むようにパック拡張ポイントを追加する- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` は、(浮動バージョンが使用されている場合でも) 作成された nupkg の依存関係バージョンの範囲を保持する必要があります。- [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore`ユーザーレベルの構成もソース[#7209](https://github.com/NuGet/Home/issues/7209)を持っている場合、認証されたソースで失敗する

* パックでは、コンテンツファイルに対する BuildActions のセットを制限しないでください。 [#7155](https://github.com/NuGet/Home/issues/7155)

* AssetTargetFallback を成功させる必要がある ProjectReference を使用すると、警告が通知されます。 - [#7137](https://github.com/NuGet/Home/issues/7137)

* CPS (CommonProjectSystem) の呼び出し時にスレッド処理の問題が原因でデッドロックが発生する- [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` ローカル構成で指定されたソースのグローバル構成の資格情報を使用しません- [#6935](https://github.com/NuGet/Home/issues/6935)

* 非同期コードパスで MEF が呼び出されているスレッド処理の問題- [#6771](https://github.com/NuGet/Home/issues/6771)

* 署名: エラーは呼び出し履歴を使用せずに2回報告されました- [#6455](https://github.com/NuGet/Home/issues/6455)

* 信頼されていない署名証明書を含む署名済みパッケージをインストールすると、エラー [#6318](https://github.com/NuGet/Home/issues/6318)が表示される

* 2つのプロジェクトが obj ディレクトリを共有している場合、NuGet の復元に誤りがありません- [#6114](https://github.com/NuGet/Home/issues/6114)

* `dotnet restore`認証済みフィードからのパッケージを使用して Linux 上で PAT を使用することはできません- [#5651](https://github.com/NuGet/Home/issues/5651)

* コンピューター全体のフィード[#5410](https://github.com/NuGet/Home/issues/5410)が無効になっているため dotnet restore が失敗する

**DCR**

* "Dotnet pack project.json" が今後削除されることを警告する- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Gen1 credential プラグインの非推奨の警告を追加する- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* 署名: 有効にされたリポジトリは、署名されたリポジトリとしてのすべてのパッケージのクライアント検証を必要とします--via RepositorySignatures/5.0.0 リソース- [#7759](https://github.com/NuGet/Home/issues/7759)

* NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)を使用して、ソースごとの http 要求番号を制限する

* NuGet は Net472 をターゲットにする必要があります (VSIX の16.0 ビルドのクリーンアップに役立ちます)- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: OpenPackagePage コマンド[#7384](https://github.com/NuGet/Home/issues/7384)の削除

* NetCoreApp 3.0 を NetStandard 2.1 にマップする- [#7762](https://github.com/NuGet/Home/issues/7762)

* NuGet. * パッケージに netstandard 2.0 サポートを追加する- [#6516](https://github.com/NuGet/Home/issues/6516)

* パッケージ作成者がビルドアセットを定義できるようにする推移的な動作- [#6091](https://github.com/NuGet/Home/issues/6091)

* VS 2019 ソリューションフィルター機能をサポートします。 では、プロジェクトがソリューションに含まれていないか、プロジェクトがアンロードされています。 最初の[#5820](https://github.com/NuGet/Home/issues/5820) (CLI または VS を使用) で完全なソリューションを復元する必要がある

* .NET 4.7.2 を必要とする NuGet 5.0 アセンブリ (TFM change を使用)- [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData からのパッケージはパブリック型である必要があります。 Spdx からライセンスメタデータ取り込まれたを更新します。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 古い設定の Api を削除する- [#7294](https://github.com/NuGet/Home/issues/7294)

* 1 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)のシステムでの復元タイムアウトの回避

* NuGet.config-[構成の追加] オプションで資格情報がある場合でも、NuGet は NTLM 認証を優先します。資格情報の認証の種類をフィルター処理するには [#5286](https://github.com/NuGet/Home/issues/5286)

* PackageReference の EmbedInteropTypes を有効にする (一致する Packages.Config 機能)- [#2365](https://github.com/NuGet/Home/issues/2365)

**[このリリース-5.0 RTM で修正されるすべての問題の一覧](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>概要: 5.0.2 の新機能

* セキュリティ (dotnet.exe または mono.exe 経由で実行する場合)-obj フォルダーは正しいアクセス許可で作成する必要があり [#7908](https://github.com/NuGet/Home/issues/7908)

* Mono/MacOS での nuget.exe の復元がカスタム nuget.config と `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)で失敗する


## <a name="known-issues"></a>既知の問題

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>.NET Core SDK によってインストールされる FallbackFolders 内のパッケージがカスタム インストールされ、署名の検証に失敗する。 - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>問題
dotnet.exe 2.x を使って netcoreapp 1.x と netcoreapp 2.x をマルチターゲットにするプロジェクトを復元すると、そのフォールバック フォルダーがファイル フィードとして扱われます。 つまり、復元するときに、NuGet ではフォールバック フォルダーからパッケージを選択し、それをグローバル パッケージ フォルダーにインストールしようと試み、通常の署名の検証を行って、失敗します。<br>
#### <a name="workaround"></a>回避策
を nothing に設定することにより、フォールバックフォルダーの使用を無効にし `RestoreAdditionalProjectSources` ます。

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

フォールバックフォルダーから復元されるパッケージは NuGet.org からダウンロードされるので、これは注意して使用してください。