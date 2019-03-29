---
title: NuGet 4.8 RTM リリース ノート
description: NuGet 4.8.1 のリリース ノートです。既知の問題、バグ修正、追加機能、および DCR について示します。
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: f85042b8fe1511934d6a3ac7de34da92c575f6e0
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432519"
---
# <a name="nuget-48-release-notes"></a>NuGet 4.8 リリース ノート

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、NuGet 4.8 機能が付属しています。


また、次の同一機能のコマンド ライン バージョンが利用可能です。
* NuGet.exe 4.8 - [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>概要:4.8.0 の新機能
* NuGet.exe では、Windows 10 上での長いファイル名がサポートされるようになりました。[#6937](https://github.com/NuGet/Home/issues/6937)
* クロス プラットフォームを含め、MsBuild、DotNet.exe、NuGet.exe、および Visual Studio 全体で、認証プラグインが機能するようになりました。 最初の世代の認証プラグインは、MsBuild、DotNet.exe ではサポートされていませんでした。 メモ:VS 2017 15.9 プレビューのビルドには、VSTS 認証プラグインが組み込まれています。 [#6486](https://github.com/NuGet/Home/issues/6486)
* MsBuild の SDK リゾルバーは、NuGet の一部としてビルドされ、VS 対応の NuGet ツールと共にインストールを行います。 これにより、複数のバージョンでの同期の取得を防止します。[#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference では、DevelopmentDependency メタデータがサポートされるようになりました。[#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>概要:4.8.2 の新機能

* セキュリティ修正プログラム: ~/.nuget 内で作成されたファイルに対するアクセス許可の範囲が広すぎる [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="known-issues"></a>既知の問題
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>CI マシン上またはオフライン環境に署名済みパッケージをインストールすると、通常よりも長い時間がかかる。

#### <a name="issue"></a>懸案事項
マシンのインターネット アクセスが制限されている場合 (CI/CD シナリオでのビルド マシンなど)、失効サーバーには到達できないため、署名済みの nuget パッケージからの警告 ([NU3028](https://docs.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu3028)) が発生します。 これは想定されている動作です。 ただし、場合によっては、これによって通常よりも時間がかるパッケージのインストール/復元など、意図しない結果を引き起こす場合があります。

#### <a name="workaround"></a>回避策
失効チェック モードを切り替えるために環境変数を導入した Visual Studio 15.8.4 および NuGet.exe 4.8.1 に更新します。
`NUGET_CERT_REVOCATION_MODE` 環境変数を `offline` に設定すると、NuGet は、キャッシュされた証明書失効リストに対してのみ証明書の失効ステータスをチェックするように設定され、NuGet は失効サーバーへのアクセスを試行しなくなります。 失効チェック モードが `offline` に設定された場合、警告は情報へとダウングレードされます。

> [!Warning]
> 通常の状況では、失効チェック モードをオフラインに切り替えることはお勧めしません。 オフラインに切り替えると、NuGet はオンライン失効チェックをスキップして、キャッシュされた証明書失効リスト (期限切れの場合もある) に対するオフライン失効チェックのみを実行します。 これは、証明書の署名が失効済みになった可能性のあるパッケージが、引き続きインストール/復元されることを意味します。オフラインに切り替えなければ、失効チェックでエラーになり、インストールされなかったはずのパッケージです。

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>右クリックのコンテキスト メニューで `Migrate packages.config to PackageReference...` オプションを使用できない

#### <a name="issue"></a>懸案事項

プロジェクトを最初に開いたとき、NuGet 操作を行うまで NuGet が初期化されていない場合があります。 これにより、`packages.config` または `References` 上の右クリックのコンテキスト メニューで、移行オプションが表示されません。

#### <a name="workaround"></a>回避策

次の NuGet アクションのいずれかを実行します。
* パッケージ マネージャー UI を開く - `References` を右クリックし、`Manage NuGet Packages...` を選択する
* パッケージ マネージャー コンソールを開く - `Tools > NuGet Package Manager` から、`Package Manager Console` を選択する
* NuGet 復元を実行する - ソリューション エクスプローラーのソリューション ノードを右クリックし、`Restore NuGet Packages` を選択する
* NuGet 復元もトリガーするプロジェクトをビルドする

これで、移行オプションを表示できるようになりました。 このオプションは ASP.NET と C++ のプロジェクト タイプではサポートされておらず、表示されません。
メモ:これは VS 2017 15.9 プレビュー 3 で修正されました

## <a name="issues-fixed-in-this-release"></a>このリリースで修正された問題

### <a name="bugs"></a>バグ
#### <a name="signing"></a>署名
* 署名: 署名済みパッケージのオフライン環境でのインストール [#7008](https://github.com/NuGet/Home/issues/7008) -- 4.8.1 で修正済み
* 署名: 不正な URL チェック - [#7174](https://github.com/NuGet/Home/issues/7174)
* 署名: パッケージにリポジトリの副署名がある場合に、RepositorySignatureVerifier でパッケージの整合性をチェックする - [#6926](https://github.com/NuGet/Home/issues/6926)
* "パッケージの整合性チェックに失敗しました。" のメッセージに、パッケージ ID (およびエラー コード) が必要である - [#6944](https://github.com/NuGet/Home/issues/6944)
* リポジトリの署名済みパッケージの検証によって、別の証明書で署名されたパッケージを許可する - [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet - 署名 - タイムスタンプ URL を https:// にできない。 - [#6871](https://github.com/NuGet/Home/issues/6871)
* NuSpec パッキングのシナリオで NullRef しない。また、オプションを改善。 - [#6866](https://github.com/NuGet/Home/issues/6866)
* 副署名にタイムスタンプを追加するとき、署名者情報の更新中はメモリが無効になる - [#6840](https://github.com/NuGet/Home/issues/6840)
* 署名: CTL 例外を削除する - [#6794](https://github.com/NuGet/Home/issues/6794)
* 署名:  contentUrl が必ず HTTPS になる - [#6777](https://github.com/NuGet/Home/issues/6777)
* 署名: SignedPackageVerifierSettings.VSClientDefaultPolicy が使用されない - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>パック
* nuspec のパックに dotnet.exe を使用している場合、復元およびビルドが必須ではいけない - [#6866](https://github.com/NuGet/Home/issues/6866)
* NuspecProperties で空の置換トークンが許可される  - [#6722](https://github.com/NuGet/Home/issues/6722)
* NuspecProperties が指定された場合に、PackTask が NullReferenceException をスローする - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>ユーザー補助
* ユーザー補助: PM UI で、パッケージ ボタン下にある 'プレリリース' という文字列が、そのパッケージの説明で隠れてしまう - [#4504](https://github.com/NuGet/Home/issues/4504)
* ユーザー補助: PM UI で、'Microsoft Visual Studio Offline Packages' を選択すると、パッケージ ソースのドロップ ダウンと設定ボタンの表示が切れてしまう- [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Powershell 管理コンソール (PMC)
* `Update-Package` で、PackageReference バージョンの範囲が無視される - [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` のソリューション全体の問題 - [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` で、名前が指定されたパッケージ単独ではなく、すべてのパッケージが再インストールされる - [#737](https://github.com/NuGet/Home/issues/737)
* パッケージ マネージャー コンソールから、一覧に記載されていない NuGet パッケージに対する更新が可能 - [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>[その他]
* `NuGet update self` を修正するために、NuGet.Commandline nupkg を semver2.0 にできない - [#7116](https://github.com/NuGet/Home/issues/7116)
* NU1107 インストール エラーでのエクスペリエンスの向上 - [#7107](https://github.com/NuGet/Home/issues/7107)
* GetAuthenticationCredentialRequest のシリアル化が正しくない - [#6983](https://github.com/NuGet/Home/issues/6983)
* UI スレッド以外で初期化された場合、NuGet Visual Studio AsyncPackage が読み込めない - [#6976](https://github.com/NuGet/Home/issues/6976)
* 復元において、project.json が必要であることを示す誤ったエラーが報告される - [#6959](https://github.com/NuGet/Home/issues/6959)
* パッケージ マネージャー UI : 変更のプレビューで、[OK] ボタンがキーボードから自動的に使用できない - [#6893](https://github.com/NuGet/Home/issues/6893)
* p2p リファレンスのあるプロジェクトで、RestoreSources が無視される - [#6776](https://github.com/NuGet/Home/issues/6776)
* .NET Framework テンプレートを使用して単体テスト プロジェクトを作成すると、packages.config を使ったより古いプロジェクト モデルが開かれる - [#6736](https://github.com/NuGet/Home/issues/6736)
* プロジェクト リファレンスでパッケージ依存関係を上書き可能にする - [#6536](https://github.com/NuGet/Home/issues/6536)
* MSBuild タスクで NoDefaultExcludes を公開する - [#6450](https://github.com/NuGet/Home/issues/6450)
* ウィンドウ サイズを変更すると、"Clear All NuGet Cache(s)\(すべての NuGet キャッシュをクリアする\)" のステータス メッセージが表示されなくなる場合がある - [#5938](https://github.com/NuGet/Home/issues/5938)


[このリリースで修正されたすべての問題一覧](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
