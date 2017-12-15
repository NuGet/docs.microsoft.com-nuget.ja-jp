---
title: "NuGet 2.7 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba2edaad-4795-47a0-a572-d0e1716bd540
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.7 リリース ノートです。"
keywords: "NuGet 2.7 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 502cb5e68f905e9ad8f4003bb0690d3e676f6bb7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 リリース ノート

[WebMatrix のリリース ノートについては、NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 リリース ノート](../release-notes/nuget-2.7.1.md)

NuGet 2.7 は、2013 年 8 月 22 日にリリースされました。

## <a name="acknowledgements"></a>謝辞

NuGet 2.7、多大な協力の次の外部共同作成者いただき、ありがとうたいと思います。

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - パッケージおよび詳細度の一覧の詳細とライセンス url を表示します。
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -developmentDependency 属性を追加`packages.config`パック コマンドで実行時のパッケージだけを使用して
1. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Nuget.exe パック コマンド プロパティ キーが重複しないようにします。
1. [佐藤さん Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -を 200 マシン キャッシュのサイズを大ききます。
1. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -修正 NuGet ダイアログが正しくありません タブで更新プログラムを表示
    - 修正プログラム Project.TargetFramework をプロジェクト管理者では null にすることができます。
    - [#3248](http://nuget.codeplex.com/workitem/3248) -修正 SharedPackageRepository FindPackage/FindPackagesById は、存在しない packageId に失敗
1. [Kevin ボイル](http://www.codeplex.com/site/users/view/KevinBoyleRG)([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Nomad プロジェクトのサポートを有効にします。
1. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -ファイルが存在しない場合、修正プッシュ コマンドが失敗する終了コード 0。
1. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -追加 BindingRedirect コマンド プロジェクトは、データベース プロジェクトを参照する場合のバグを修正します。
1. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -'除外' 属性でワイルドカードを正しく解析されなかった nuget.pack のバグを修正します。
1. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
    - [#3307](http://nuget.codeplex.com/workitem/3307) -バグの修正プログラム`NuGet.targets`渡しません $(Platform) nuget.exe へのパッケージを復元するときにします。
1. [Brian わたし](http://www.codeplex.com/site/users/view/benerdin)
    - [#3294](http://nuget.codeplex.com/workitem/3294) -大文字小文字が異なる、最終的に「項目が既に存在する」の例外の原因と、同じ名前のファイルを追加することを許可する nuget.exe パッケージ コマンドでバグを修正します。
1. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
    - [#2990](http://nuget.codeplex.com/workitem/2990) -NetPortableProfile クラスへのバージョンの追加プロパティ。
1. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
    - [#3460](https://nuget.codeplex.com/workitem/3460)の場合は、NullReferenceException のバグを修正 requireApiKey = true の場合、ヘッダー X-NUGET-APIKEY が存在しません。
1. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
    - [#3278](https://nuget.codeplex.com/workitem/3278) -MonoDevelop で正しく動作するようにファイルの修正 NuGet.Build ターゲット
1. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
    - 並列処理を増やすことで復元コマンドのパフォーマンスを向上させる

## <a name="notable-features-in-the-release"></a>リリースで注目に値する機能

### <a name="package-restore-by-default-with-implicit-consent"></a>既定では (暗黙の同意) のパッケージの復元

NuGet 2.7 復元では、パッケージ化するための新しいアプローチを紹介しも主要な課題を克服: パッケージの復元の同意は現在は既定では! 新しいアプローチと、暗黙の同意の組み合わせは、パッケージの復元シナリオと大幅に簡略化します。

#### <a name="implicit-consent"></a>暗黙の同意

NuGet のバージョン 2.0、2.1、2.2、2.5、および 2.6 中に足りないパッケージをダウンロードを NuGet を明示的に許可するために必要なユーザーを構築します。 この同意があるない場合は、明示的に指定されて、ビルドは、ユーザーが承諾されるまでパッケージの復元が有効になっているソリューションは失敗し、します。

NuGet 2.7 以降では、パッケージの復元の同意は既定で ON にユーザーを明示的に許可するときに*脱退*のパッケージの復元が必要な場合、Visual Studio で NuGet の設定で、チェック ボックスを使用します。 暗黙の同意は、この変更には、次の環境での NuGet に影響します。

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe コマンド ライン ユーティリティ

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio での自動のパッケージの復元

NuGet 2.7 以降では、NuGet は自動的に足りないパッケージをダウンロード、Visual Studio でのビルド中に、ソリューションのパッケージの復元が明示的に有効にしていないされている場合でもです。 MSBuild が呼び出される前に、プロジェクトまたはソリューションをビルドするときに、Visual Studio で発生この自動パッケージを復元します。 これには、いくつかの重要な利点が得られます。

1. それ以上、ソリューションに「を有効にする NuGet パッケージの復元」ジェスチャを使用する必要があります。
1. プロジェクトを変更する必要はありませんし、NuGet は、パッケージの復元が有効になっていることを確認するようにプロジェクトに変更を加えるされません。
1. Props/ターゲット ファイルのインポートを MSBuild が含まれているものも含め、すべての NuGet パッケージは、復元する*する前に*MSBuild が呼び出され、それらのプロパティ/ターゲットがビルド中に正しく認識されたことを確認

パッケージの復元を自動で Visual Studio を使用するためにのみ、いずれか (in) アクションを実行する必要があります。

1. チェックインしない、`packages`フォルダー

省略するいくつかの方法、`packages`ソース管理からフォルダーです。 詳細については、次を参照してください。、[パッケージおよびソース管理](../consume-packages/packages-and-source-control.md)トピックです。

すべてのユーザーは、暗黙的に、同意のパッケージの復元を自動選択されるため、簡単に選択できます Visual Studio でパッケージ マネージャーの設定をします。

![パッケージ マネージャーの設定](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>コマンドラインからの簡略化されたパッケージの復元

NuGet 2.7 nuget.exe の新機能が導入されています。`nuget.exe restore`

この新しい Restore コマンドでは、ソリューション ファイルまたはフォルダーを引数としてそのまま使用して 1 つのコマンドを使用して、ソリューションのすべてのパッケージを簡単に復元することができます。 さらに、その引数では、現在のフォルダー内に 1 つのソリューションのみがある場合に暗黙的です。 つまり、すべての次のように 1 つのソリューション ファイル (MySolution.sln) を含むフォルダーから。

1. nuget.exe restore MySolution.sln
1. nuget.exe 復元します。
1. nuget.exe restore

Restore コマンドはソリューション ファイルを開くし、ソリューション内のすべてのプロジェクトを検索します。 そこが検出されます、`packages.config`プロジェクトと検出されたすべてのパッケージ復元は、の各ファイルです。 あるソリューション レベルのパッケージも復元、`.nuget\packages.config`ファイル。 詳細については、新しい復元コマンドは含まれて、[コマンド ライン リファレンス](../tools/cli-ref-restore.md)です。

#### <a name="the-new-package-restore-workflow"></a>新しいパッケージの復元ワークフロー

新しいワークフローを説明しながら興奮してその変更がパッケージを復元するには。 ソース管理からパッケージを省略する場合、単にコミットしないように、`packages`フォルダーです。 Visual Studio ユーザーを開き、ソリューションのビルドは、パッケージを自動的に復元に表示されます。 コマンド ライン ビルドは、単に呼び出し`nuget.exe restore`を呼び出す前に`msbuild`です。 ソリューションに「を有効にする NuGet パッケージの復元」ジェスチャを使用する必要がありますのでは不要になったとビルドを変更するプロジェクトを変更して必要がなくなります。 ここでも、かなりエクスペリエンスの向上を特に NuGet の最新機能を通じて追加されたインポート用の MSBuild imports を含むパッケージの結果と[props/ターゲット ファイルを自動的にインポート](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files)\build フォルダーからです。

社内で実行した作業、に加えても取り組んでいますいくつか重要なパートナーをこの新しい手法を完了するとします。お必要はありませんが具象タイムラインこれらのいずれにもまだ、各パートナーは新しいアプローチにあるため、期待します。

* 呼び出しを統合している team Foundation Service -`nuget.exe restore`既定値にシナリオを構築します。
* 使用できるようにして、プロジェクトを Azure にプッシュしている Windows Azure Web サイト - `nuget.exe restore` web サイトをビルドする前に呼び出されます。
* TeamCity - TeamCity 用の NuGet インストーラー プラグインを更新して 8.x
* AppHarbor リポジトリにプッシュしてできるようにしている AppHarbor -`nuget.exe restore`ソリューションがビルド前に呼び出されます。

上記のパートナーの各 nuget.exe の独自のコピーを使用して、ソリューションに nuget.exe を実行する必要はありません。

#### <a name="known-issues"></a>既知の問題

初期の 2.7 リリースでは、nuget.exe restore に 2 つの既知の問題が発生しましたが、9/6/2013 更新プログラムを固定された、 [NuGet.CommandLine パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)です。  この更新はできるもの[NuGet 2.7 ダウンロード ページ](https://nuget.codeplex.com/releases/view/107605)CodePlex で公開します。  実行している`nuget.exe update -self`最新のリリースに更新されます。

固定されました。

1. [SLN ファイルを使用するときにモノラルで新しいパッケージの復元は機能しません](https://nuget.codeplex.com/workitem/3596)
1. [Wix プロジェクトで新しいパッケージの復元は機能しません](https://nuget.codeplex.com/workitem/3598)

新しいパッケージの復元のワークフローの既知の問題、[自動パッケージの復元は、ソリューション フォルダーの下のプロジェクトに対しては機能しません](https://nuget.codeplex.com/workitem/3625)です。 この問題は、NuGet 2.7.1 で修正されました。

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>ビルド エラー/警告の再ターゲットのプロジェクトとアップグレード

何度も再ターゲットまたはしたら、プロジェクトをアップグレードした後、検索する一部の NuGet パッケージが正しく機能していないこと。 残念ながら、これを示す値がないと、ガイダンスはありませんこれに対処する方法のです。 NuGet 2.7 と、Visual Studio の一部のイベントを使用して今すぐ再ターゲットまたはインストールされている NuGet パッケージの影響を与えるようにプロジェクトをアップグレードしたときに認識します。

再ターゲットまたはアップグレードして影響を受けた、パッケージのいずれかを検出した場合は、イミディ エイト ビルド エラーを知らせるを得ることがおです。 即時ビルド エラーだけでなくまた保存、`requireReinstallation="true"`フラグ、`packages.config`ファイル、再ターゲットの影響を受けるとその後に実行されたすべてのパッケージの Visual Studio でビルドが生成されます、それらのパッケージのビルドの警告です。

NuGet は、影響を受けるパッケージを再インストールを自動操作を実行できない、このを示す値を願っていますし、警告では、ヘルプを説明します。 パッケージを再インストールする必要がある場合を検出します。 取り組んでいるところ[ガイダンスのドキュメントを再インストールをパッケージ化](../consume-packages/reinstalling-and-updating-packages.md)をこれらのエラー メッセージに指示します。

### <a name="nuget-configuration-defaults"></a>NuGet の既定の設定

多くの企業では、内部的には、NuGet を使用しているが、難しいソースを使用してパッケージの内部 nuget.org の代わりに、開発者が行うことがあった。NuGet 2.7 には、コンピューター全体の既定値は、指定を許可する既定の設定機能が導入されています。

1. 有効なパッケージ ソース
1. 無効なパッケージ ソースが登録します。
1. 既定の nuget.exe プッシュ ソース

これらの各構成可能であるファイル内`%ProgramData%\NuGet\NuGetDefaults.Config`です。 この構成ファイルがパッケージ ソースを指定し、既定 nuget.org パッケージ ソースが自動的に登録されていないかどうかと含まれていない`NuGetDefaults.Config`代わりに登録されます。

この機能を使用する必要ありません、中を展開する企業が予定`NuGetDefaults.Config`ファイルのグループ ポリシーを使用します。

*この機能を開発者用の NuGet 設定から削除するパッケージ ソースが発生しないことに注意してください。つまり、かどうか、開発者は NuGet を使用して既に nuget.org パッケージ ソースのために登録されると、そのコンポーネントは削除されませんの作成後に、`NuGetDefaults.Config`ファイル。*

参照してください[NuGet 構成が既定で](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file)詳細については、この機能します。

### <a name="renaming-the-default-package-source"></a>既定のパッケージ ソースの名前を変更します。

NuGet は、"NuGet オフィシャル パッケージ ソースという"nuget.org を指す既定のパッケージ ソースと常に登録されました。その名前が verbose、ポイントが実際にも指定しませんでした。 これら 2 つの問題に対処するには、単に"nuget.org"、UI でこのパッケージ ソースを変更してしました。 パッケージ ソースの URL も変更されており"www." プレフィックスを含むバンドル ID です。 NuGet 2.7 を使用するは既存の「NuGet オフィシャル パッケージ ソース」は名前として"nuget.org"と"https://www.nuget.org/api/v2/"としてその URL を自動的に更新されます。

### <a name="performance-improvements"></a>パフォーマンスの向上

メモリ量が削減され、少ないディスク使用量および高速なパッケージのインストールが得られます 2.7 のいくつかのパフォーマンスの向上にしています。 スマートなクエリは、全体的なペイロードを削減する OData ベースのフィードをにもされました。

### <a name="new-extensibility-apis"></a>新しい機能拡張 Api

いくつかの新しい Api を以前のリリースで不足している機能のギャップを埋める、機能拡張サービスに追加されました。

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

この機能に占める[Adam Ralph](https://twitter.com/adamralph)パッケージ作成者が開発に使用されたのみの依存関係は、時間し、パッケージの依存関係を必要としないを宣言することができします。 追加することによって、`developmentDependency="true"`属性内のパッケージを`packages.config`、`nuget.exe pack`依存関係としてそのパッケージに含まれなくなります。

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Windows Phone 用の Visual Studio 2010 Express のサポートの削除

パッケージの新しい復元モデル 2.7 には、メインの NuGet VSPackage からでは新しい VSPackage によって実装されます。 技術的な問題は、この新しい VSPackage それでもで正しく、 *Visual Studio 2010 Express を Windows Phone* SKU に他のと同じコード ベースを共有おようは、Visual Studio Sku をサポートします。 そのため、NuGet 2.7 以降、削除されるのサポート*Visual Studio 2010 Express を Windows Phone*公開済みの拡張機能からです。 サポート*Visual Studio 2010 の Express for Web* Visual Studio 拡張機能ギャラリーにパブリッシュされたプライマリの拡張機能に掲載されています。

ありませんが、開発者が何人もを使用している NuGet の Visual Studio のバージョンとエディションで、ためそれらのユーザー専用の別個の Visual Studio 拡張機能を公開あり、(Visual Studio 拡張機能ギャラリーではなく) CodePlex で公開. これは影響する場合は、その拡張を維持する予定がないお知らせください CodePlex での問題をファイリングすることで。

(Visual Studio 2010 Express を Windows Phone) の NuGet Package Manager をダウンロードするを参照してください。、 [NuGet 2.7 をダウンロード](https://nuget.codeplex.com/releases/view/107605)ページ。

### <a name="bug-fixes"></a>バグ修正

NuGet の今回のリリースには、これらの機能に加えて、他の多くのバグ修正も含まれます。 リリースで対処 97 の合計の問題が発生しました。 作業の完全な一覧の項目で修正 NuGet 2.7 くださいビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)です。
