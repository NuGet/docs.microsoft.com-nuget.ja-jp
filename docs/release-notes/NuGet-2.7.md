---
title: NuGet 2.7 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.7 リリース ノートです。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550966"
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 リリース ノート

[WebMatrix のリリース ノートについては、NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 リリース ノート](../release-notes/nuget-2.7.1.md)

NuGet 2.7 は、2013 年 8 月 22 日にリリースされました。

## <a name="acknowledgements"></a>謝辞

今回は外部の共同作成者、次の NuGet 2.7 に、多大な貢献に感謝します。

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - パッケージと詳細度を一覧表示の詳細とライセンス url を表示します。
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -developmentDependency 属性を追加`packages.config`をランタイム パッケージだけを pack コマンドで使用
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Nuget.exe パック コマンド プロパティ キーが重複しないようにします。
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -200 をマシン キャッシュのサイズを大ききます。
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -間違った タブで更新プログラムを表示する修正 NuGet ダイアログ
    - 修正 Project.TargetFramework をプロジェクト管理者では null にすることができます。
    - [#3248](http://nuget.codeplex.com/workitem/3248) -修正 SharedPackageRepository FindPackage/FindPackagesById は存在しない packageId の失敗
6. [Kevin ボイル](http://www.codeplex.com/site/users/view/KevinBoyleRG)([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Nomad プロジェクトのサポートを有効にします。
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -ファイルが存在しない場合、終了、修正プログラムのプッシュ コマンドが失敗コード 0。
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -追加 BindingRedirect コマンド、プロジェクトは、データベース プロジェクトを参照するときのバグを修正します。
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -nuget.pack 'exclude' 属性でワイルドカードを正しく解析のバグを修正します。
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -バグの修正プログラム`NuGet.targets`パッケージの復元も nuget.exe に $ が渡されません。
11. [Brian わたし](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -で最終的に「既に項目が存在します」の例外の原因とする、さまざまな大文字と小文字が同じ名前のファイルを追加することを許可する nuget.exe パッケージ コマンドのバグを修正します。
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -NetPortableProfile クラスへのバージョンの追加プロパティ。
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -場合 NullReferenceException バグは修正 requireApiKey、ヘッダーは、true を = X-APIKEY NUGET が存在しません。
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -修正 NuGet.Build ターゲットは、MonoDevelop で正しく動作するようにファイル
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - 並列処理を増やすことで復元コマンドのパフォーマンスを向上させる

## <a name="notable-features-in-the-release"></a>リリースで注目すべき機能

### <a name="package-restore-by-default-with-implicit-consent"></a>(暗黙的な同意) では既定でパッケージの復元

NuGet 2.7 がパッケージの復元の新しいアプローチを紹介し、主要な課題の解決にも: パッケージの復元の同意が既定で有効と今すぐいます! 新しいアプローチと、暗黙的な同意の組み合わせは、パッケージの復元シナリオと大幅に簡略化します。

#### <a name="implicit-consent"></a>暗黙的な同意

NuGet のバージョン 2.0、2.1、2.2、2.5、2.6 では、中に見つからないパッケージのダウンロードを NuGet を明示的に許可するために必要なユーザーを作成します。 この同意があるない場合は、明示的に指定されて、パッケージの復元を有効にしたソリューションは、ユーザーが同意するまでのビルドに失敗し、します。

NuGet 2.7 以降では、パッケージ復元の同意、既定でオンにユーザーを明示的に許可するときに*オプトアウト*の Visual Studio で NuGet の設定で、チェック ボックスを使用して、必要な場合は、パッケージの復元。 暗黙的な同意のこの変更には、次の環境での NuGet に影響します。

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe コマンド ライン ユーティリティ

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio で自動パッケージの復元

NuGet 2.7 以降では、NuGet は自動的に見つからないパッケージのダウンロード Visual Studio で、ビルド中にソリューションのパッケージの復元が明示的に有効にしていないされている場合でもです。 この自動パッケージの復元は Visual Studio では発生、MSBuild が呼び出される前に、プロジェクトまたはソリューションをビルドするときにします。 これには、いくつかの重要な利点が得られます。

1. それ以上でソリューション「を有効にする NuGet パッケージの復元」ジェスチャを使用する必要があります。
1. プロジェクトを変更する必要はありませんし、NuGet はパッケージの復元が有効になっていることを確認するようにプロジェクトに変更を加えるしません
1. プロパティ/ターゲット ファイルのインポートの MSBuild が含まれているものも含め、すべての NuGet パッケージが復元されます*する前に*MSBuild が呼び出される、ビルド時にこれらのプロパティ/ターゲットが正しく認識されたことを確認

Visual Studio でパッケージの自動復元を使用して、するためにのみ (in) アクションのいずれかを実行する必要があります。

1. チェックインしないと、`packages`フォルダー

省略するいくつかの方法がある、`packages`ソース管理からフォルダー。 詳細については、次を参照してください。、[パッケージとソース管理](../consume-packages/packages-and-source-control.md)トピック。

すべてのユーザーが暗黙的には同意のパッケージの復元を自動選択されるため、簡単にオプトアウトできます Visual Studio のパッケージ マネージャー設定を使用します。

![パッケージ マネージャーの設定](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>コマンドラインからの簡略化されたパッケージの復元

NuGet 2.7 には、nuget.exe の新機能が導入されています。 `nuget.exe restore`

この新しい復元コマンドでは、ソリューション ファイルまたはフォルダーを引数としてそのまま使用して 1 つのコマンドを含むソリューションのすべてのパッケージを簡単に復元できます。 さらに、現在のフォルダーに 1 つのソリューションのみがある場合にその引数が含まれます。 つまり、すべての次のように 1 つのソリューション ファイル (MySolution.sln) が含まれているフォルダーから。

1. nuget.exe restore MySolution.sln
1. nuget.exe restore .
1. nuget.exe restore

Restore コマンドはソリューション ファイルを開くし、ソリューション内のすべてのプロジェクトを検索します。 そこからは検索、`packages.config`プロジェクトと検出されたすべてのパッケージ復元の各ファイル。 あるソリューション レベル パッケージが復元されます、`.nuget\packages.config`ファイル。 新しい復元コマンドの詳細についてで参照できる、[コマンド ライン リファレンス](../tools/cli-ref-restore.md)します。

#### <a name="the-new-package-restore-workflow"></a>新しいパッケージの復元ワークフロー

新しいワークフローを説明しながらはこれらの変更をパッケージの復元、嬉しいです。 ソース管理からパッケージを省略する場合を単にコミットしないで、`packages`フォルダー。 開き、ソリューションをビルドする visual Studio のユーザーに自動的に復元されたパッケージが表示されます。 コマンド ライン ビルドを呼び出すだけ`nuget.exe restore`を呼び出す前に`msbuild`します。 ソリューションでは、上で「を有効にする NuGet パッケージの復元」ジェスチャを使用する必要がなくなったと、不要になった変更、ビルドするプロジェクトを変更する必要があります。 特にインポートの NuGet の最新の機能を使用して追加の場合、MSBuild インポートを含むパッケージに対して大幅に改善されたエクスペリエンスもが生成されます。 と[プロパティ/ターゲット ファイルを自動的にインポート](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files)\build フォルダーから。

自分たちが行った作業、に加えて取り組んでいるところもいくつかの重要なパートナーをこの新しいアプローチを仕上げるとします。具体的なタイムラインこれらのいずれかの必要私たちはまだありませんが、各パートナーは新しいアプローチの詳細については同じぐらいワクワクします。

* 呼び出しを統合する作業が team Foundation Service -`nuget.exe restore`を既定のシナリオを構築します。
* 作業をし、プロジェクトを Azure にプッシュできるように Windows Azure の Web サイト - `nuget.exe restore` web サイトを構築する前に呼び出されます。
* TeamCity の TeamCity の NuGet インストーラーのプラグインを更新して 8.x
* AppHarbor にリポジトリをプッシュしを許可する操作、AppHarbor -`nuget.exe restore`ソリューションがビルド前に呼び出されます。

各上記のパートナーと nuget.exe の独自のコピーを使用して、ソリューションに nuget.exe を実行する必要はありません。

#### <a name="known-issues"></a>既知の問題

初期 2.7 リリースでは、nuget.exe の復元に関する 2 つの既知の問題がありましたが、9/6/2013 の更新プログラムで修正されたが、 [NuGet.CommandLine パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)します。  この更新はできるも、 [NuGet 2.7 ダウンロード ページ](https://nuget.codeplex.com/releases/view/107605)CodePlex でします。  実行している`nuget.exe update -self`最新リリースに更新されます。

固定されました。

1. [SLN ファイルを使用する場合、Mono で新しいパッケージの復元が機能しません](https://nuget.codeplex.com/workitem/3596)
1. [Wix プロジェクトで新しいパッケージの復元は機能しません](https://nuget.codeplex.com/workitem/3598)

新しいパッケージの復元ワークフローに関する既知の問題という[自動パッケージの復元は、ソリューション フォルダーの下のプロジェクトは適していません](https://nuget.codeplex.com/workitem/3625)します。 この問題は、NuGet 2.7.1 で修正されました。

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>プロジェクトの再ターゲットおよびアップグレード ビルド エラー/警告

何度も後に再ターゲットまたはプロジェクトをアップグレード、見つかったら NuGet パッケージの一部が正しく機能していないこと。 残念ながら、これを示す値はありませんがしないガイダンスの対処方法。 NuGet 2.7、Visual Studio の一部のイベントを使用して今すぐ再ターゲットまたは、インストールされている NuGet パッケージに影響を与える方法でプロジェクトをアップグレードしたときに認識。

再ターゲットまたはアップグレードによって影響を受けた、パッケージのいずれかを検出することを知らせる直ちにビルド エラーを生成します。 だけでなく、直ちにビルド エラーも維持、`requireReinstallation="true"`フラグ、`packages.config`ファイルの Visual Studio でのビルド、再ターゲットによって影響を受けると後に続く各されたすべてのパッケージをそれらのパッケージのビルド警告が発生させます。

NuGet は、影響を受けるパッケージを再インストールする自動アクションを実行できません、示唆されていることと思い、警告に従ってヘルプ パッケージを再インストールする必要がある場合を検出します。 取り組んでいますも[ガイダンスのドキュメントを再インストールをパッケージ化](../consume-packages/reinstalling-and-updating-packages.md)これらのエラー メッセージが送信します。

### <a name="nuget-configuration-defaults"></a>NuGet の既定の設定

多くの企業では、内部的には、NuGet を使用しているが、nuget.org ではなく、内部のパッケージ ソースを使用するには、その開発者ガイド ハード時間があります。NuGet 2.7 には、コンピューター全体の既定値を指定する構成の既定値の機能が導入されています。

1. 有効なパッケージ ソース
1. 無効になっているパッケージ ソースが登録します。
1. 既定の nuget.exe プッシュ ソース

これらの各内にあるファイルで構成できます`%ProgramData%\NuGet\NuGetDefaults.Config`します。 この構成ファイル、パッケージ ソースを指定するかどうかは、既定の nuget.org パッケージ ソースが自動的に登録されずで使用されている`NuGetDefaults.Config`は代わりに登録されます。

この機能を使用するため必要ありませんが、デプロイする企業が予定`NuGetDefaults.Config`ファイルのグループ ポリシーを使用します。

*この機能が開発者の NuGet の設定から削除するパッケージ ソース発生しないことに注意してください。つまり、開発者が既に NuGet を使用し、したがって nuget.org パッケージ ソースを持つかどうか、登録されていることも削除されませんの作成後、`NuGetDefaults.Config`ファイル。*

参照してください[NuGet 構成は既定で](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file)詳細については、この機能はします。

### <a name="renaming-the-default-package-source"></a>既定のパッケージ ソースの名前を変更します。

NuGet は、nuget.org を指す「NuGet のオフィシャル パッケージ ソース」と呼ばれる既定のパッケージ ソースを登録して常に。その名前の詳細が、ポイントが実際にも指定しませんでした。 これら 2 つの問題に対処するには、を単に"nuget.org"に、UI には、このパッケージ ソースに変更しました。 パッケージ ソースの URL も変更を"www."を含める プレフィックスを含むバンドル ID です。 NuGet 2.7 を使用した後、既存「NuGet オフィシャル パッケージ ソース」が自動的に更新を名前として"nuget.org"と"<https://www.nuget.org/api/v2/>"としてその URL。

### <a name="performance-improvements"></a>パフォーマンスの向上

メモリ フット プリントが小さく、少ないディスク使用量とパッケージのインストールを高速化が得られます 2.7 でなんらかのパフォーマンス改善を行いました。 全体的なペイロードが減少する OData ベースのフィードをよりスマートなクエリもなりました。

### <a name="new-extensibility-apis"></a>新しい拡張性 Api

一部の新しい Api は、以前のリリースで不足している機能のギャップを埋める、機能拡張サービスを追加しました。

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>開発専用の依存関係

この機能が提供された[Adam Ralph](https://twitter.com/adamralph)これにより、開発に使用されたのみの依存関係は、時間し、パッケージの依存関係を必要としないを宣言するパッケージ作成者とします。 追加することで、`developmentDependency="true"`属性でパッケージを`packages.config`、`nuget.exe pack`依存関係としてそのパッケージは含まれません。

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Visual Studio 2010 Express for Windows Phone のサポートの削除

2.7 で新しいパッケージの復元モデルは、これは、メイン NuGet VSPackage からさまざまな新しい VSPackage によって実装されます。 技術的な問題によりこの新しい VSPackage はで正しく機能しません、 *Visual Studio 2010 Express for Windows Phone* SKU に他の同じコード ベースを伝えは、Visual Studio Sku をサポートします。 そのため、NuGet 2.7 以降、削除されるサポート*Visual Studio 2010 Express for Windows Phone*発行済みの拡張機能から。 サポート*Visual Studio 2010 の Express for Web* Visual Studio の拡張機能ギャラリーにパブリッシュされたプライマリの拡張機能にまだ含まれています。

ありませんが、どのように多くの開発者が Visual Studio のバージョン/エディションで NuGet をまだ使っている、ためそれらのユーザー専用の個別の Visual Studio 拡張機能を公開あり、(Visual Studio の拡張機能ギャラリーではなく) CodePlex で公開. これに影響する場合は、その拡張機能を維持するために続行する予定はありません CodePlex で問題を提出して通知してください。

(Visual Studio 2010 Express for Windows Phone) 用の NuGet パッケージ マネージャーをダウンロードするを参照してください。、 [NuGet 2.7 をダウンロード](https://nuget.codeplex.com/releases/view/107605)ページ。

### <a name="bug-fixes"></a>バグ修正

NuGet のこのリリースには、これらの機能に加えて、他の多くのバグ修正も含まれています。 リリースで対処された 97 合計問題が発生しました。 作業の完全な一覧の項目で修正された NuGet 2.7 の場合、くださいビュー、[このリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)します。
