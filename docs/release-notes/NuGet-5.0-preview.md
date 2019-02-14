---
title: NuGet 5.0 preview リリース ノート
description: 既知の問題、バグの修正、新機能、および Dcr を含む NuGet 5.0 プレビューのリリース ノート。
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247660"
---
# <a name="nuget-50-preview-release-notes"></a>NuGet 5.0 Preview リリース ノート

## <a name="nuget-50-preview-releases"></a>NuGet 5.0 プレビュー リリース

* 2019 年 2 月 13日 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)
* 2019 年 1 月 23日 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)

## <a name="summary-whats-new-in-nuget-50-preview-3"></a>概要:NuGet 5.0 Preview 3 の新機能新機能

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題 

**バグ:**

* nuget.exe/でしょうか。 should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): error :パスの一部が見つかりませんでした '/tmp/NuGetScratch - mono - [#7793。](https://github.com/NuGet/Home/issues/7793)

* 復元が不必要にマシン キャッシュ - で参照されるパッケージのすべてのバージョンの内容を列挙[#7639](https://github.com/NuGet/Home/issues/7639)

* MSBuild の自動検出は 16.0 を常に選択インストール VS 2019 プレビュー - 後[#7621](https://github.com/NuGet/Home/issues/7621)

* ソリューションに dotnet リスト パッケージ フレームワークの重複するエントリを出力する[#7607](https://github.com/NuGet/Home/issues/7607)

* 例外「空のパス名は有効な」old IVsPackageInstaller.InstallPackage を呼び出し元がプロジェクトし、パッケージ フォルダーが存在しません。 - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)

**Dcr**

* パッケージ作成者ビルド アセットの推移的な動作の定義を許可する[#6091](https://github.com/NuGet/Home/issues/6091)

* プロジェクトは、ソリューションの一部でないか、アンロードされますが復元された以前の場合は成功を VS での復元を有効にする[#5820](https://github.com/NuGet/Home/issues/5820)


## <a name="summary-whats-new-in-50-preview-2"></a>概要:5.0 Preview 2 の新機能新機能

### <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

**バグ:**

* VS 16.0 の NuGet UI には、色の問題のため、読み取り不可能なタブ[#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt clarification on - [#7629](https://github.com/NuGet/Home/issues/7629)

* 復元は、- の種類を判断するためのグローバル パッケージ フォルダーを列挙する不必要に[#7596](https://github.com/NuGet/Home/issues/7596)

* エラー一覧 ウィンドウ - にロック ファイル強制からエラーが表示されます[#7429](https://github.com/NuGet/Home/issues/7429)

* NuGet.Configuration の問題を修正[#7326](https://github.com/NuGet/Home/issues/7326)

* MSBuild の更新に合わせてそれはのインストール場所。  - [#7325](https://github.com/NuGet/Home/issues/7325)

* 開発の依存関係 - をする必要があります NuGet.Build.Tasks.Pack [#7249](https://github.com/NuGet/Home/issues/7249)

* などのパック拡張機能ポイントを追加するデバッグ シンボルの[#7234](https://github.com/NuGet/Home/issues/7234)

* dotnet pack には、作成した nupkg で依存関係のバージョンの範囲を保持する必要があります。 (浮動バージョンが使用されている場合も含む) - [#7232](https://github.com/NuGet/Home/issues/7232)

* ユーザー レベルの構成には、ソースもがある場合、認証済みのソースで dotnet 復元が失敗した[#7209](https://github.com/NuGet/Home/issues/7209)

* パック BuildActions - コンテンツのファイルのセットを制限せず[#7155](https://github.com/NuGet/Home/issues/7155)

* 警告 AssetTargetFallback が成功する必要があります projectreference を使用してください。 - [#7137](https://github.com/NuGet/Home/issues/7137)

* CPS (CommonProjectSystem) - を呼び出すときに、スレッドの問題によりデッドロック[#7103](https://github.com/NuGet/Home/issues/7103)

* dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)

* スレッド処理の MEF される問題非同期コードパス - で呼び出される[#6771](https://github.com/NuGet/Home/issues/6771)

* 署名: エラーが報告されずコール スタックの 2 回[#6455](https://github.com/NuGet/Home/issues/6455)

* エラー - を表示する署名証明書を信頼されていないと、署名付きパッケージをインストールする必要があります[#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet の復元を正しく Noop obj ディレクトリ - を共有する 2 つのプロジェクトと[#6114](https://github.com/NuGet/Home/issues/6114)

* -認証済みのフィードからパッケージを使用した Linux での dotnet restore で PAT を使用することはできません[#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet 復元が失敗するため、無効になっているマシン ワイド フィード - [#5410](https://github.com/NuGet/Home/issues/5410)

**Dcr**

* (変更) - TFM を使用して .NET 4.7.2 を必要とする NuGet 5.0 アセンブリ[#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData NuGet.Packaging からパブリック型である必要があります。 Spdx から取り込まれたライセンス メタデータを更新します。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 削除の設定の廃止された Api - [#7294](https://github.com/NuGet/Home/issues/7294)

* 1 システムでの回避策復元タイムアウト cpu - [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet.config の資格情報がある場合でも、NuGet は NTLM auth を優先 - 資格情報の認証の種類のフィルターを構成オプションを追加する[#5286](https://github.com/NuGet/Home/issues/5286)

* PackageReference (一致する Packages.Config 機能) - の EmbedInteropTypes を有効にする[#2365](https://github.com/NuGet/Home/issues/2365)

[このリリース 5.0.0-preview2 で修正されたすべての問題の一覧](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>既知の問題

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push --interactive が Mac 上でエラーになる。 - [#7519](https://github.com/NuGet/Home/issues/7519)
**問題**、`--interactive`引数は dotnet cli を使用して転送されていませんが、エラーが発生`error: Missing value for option 'interactive'` 
**回避策**などの対話型のオプションを使用して、他のdotnetコマンドを実行`dotnet restore --interactive`および認証します。 そうすると、認証が資格情報プロバイダーによってキャッシュされる可能性があります。 その後、`dotnet nuget push` を実行します。

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK によってインストールされる FallbackFolders 内のパッケージがカスタム インストールされ、署名の検証に失敗する。 - [#7414](https://github.com/NuGet/Home/issues/7414)
**問題**dotnet.exe を使用するときにそのマルチ ターゲット netcoreapp プロジェクトを復元する 2.x 1.x と netcoreapp 2.x、フォールバックのフォルダーはフィード ファイルとして扱われます。 つまり、復元するときに、NuGet ではフォールバック フォルダーからパッケージを選択し、それをグローバル パッケージ フォルダーにインストールしようと試み、通常の署名の検証を行って、失敗します。
**回避策**フォールバック フォルダーの使用状況を無効に設定して、 `RestoreAdditionalProjectSources` nothing にします。 `<RestoreAdditionalProjectSources/>` これは慎重に使う必要があります。フォールバック フォルダーから復元されていたはずの多くのパッケージが、NuGet.org からダウンロードされることになるためです。
