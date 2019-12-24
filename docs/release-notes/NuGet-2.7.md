---
title: NuGet 2.7 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.7 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f26ac80046ec321ce5bdbf2bac23c0e1939cd69a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317083"
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 リリースノート

[WebMatrix の nuget 2.6.1 のリリースノート](../release-notes/nuget-2.6.1-for-webmatrix.md) | [nuget 2.7.1 のリリースノート](../release-notes/nuget-2.7.1.md)

NuGet 2.7 は、2013年8月22日にリリースされました。

## <a name="acknowledgements"></a>謝辞

NuGet 2.7 への重要な貢献について、次の外部の共同作成者に感謝いたします。

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss)([@mxrss](https://twitter.com/mxrss))
    - パッケージと詳細度の一覧表示時にライセンス url を表示します。
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph)([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -developmentDependency 属性をに`packages.config`追加し、それを pack コマンドで使用して、ランタイムパッケージのみを含める
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael)([@tkrafael](https://twitter.com/tkrafael))
    - Nuget.exe pack コマンドに重複するプロパティキーを含めないでください。
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan)([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -コンピューターのキャッシュサイズを200に増やします。
5. [Slava Tr(gin](http://www.codeplex.com/site/users/view/derigel) )([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -間違ったタブに更新プログラムが表示されている NuGet ダイアログを修正する
    - プロジェクトを修正します。 ProjectManager では、TargetFramework を null にすることができます
    - [#3248](http://nuget.codeplex.com/workitem/3248) -SharedPackageRepository findpackage/FindPackagesById は存在しない packageId で失敗します。
6. [加山 Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG)([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Nomad プロジェクトのサポートを有効にする
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie)([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -ファイルが存在しない場合は、push コマンドが終了コード0で失敗します。
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -プロジェクトがデータベースプロジェクトを参照するときに BindingRedirect コマンドを使用してバグを修正します。
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos)([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -nuget のバグを修正します。 ' exclude ' 属性のワイルドカードを正しく解析できません。
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981)([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -バグ`NuGet.targets`は、パッケージを復元するときに、$ (Platform) を nuget.exe に渡すことはありません。
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -同じ名前で大文字と小文字が異なるファイルを追加でき、最終的に "項目が既に存在しています" という例外が発生する nuget.exe パッケージコマンドのバグを修正しました。
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino)([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -バージョンプロパティを NetPortableProfile クラスに追加します。
13. [David の場合](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -requireapikey = true になっていても、HEADER NullReferenceException キーが存在しない場合は、バグを修正します。
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism)([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -MonoDevelop で正常に動作するように、NuGet. ビルドターゲットファイルを修正します
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm)([@pranav_km](https://twitter.com/pranav_km))
     - 並列処理を増やすことで復元コマンドのパフォーマンスを向上させる

## <a name="notable-features-in-the-release"></a>リリースの注目すべき機能

### <a name="package-restore-by-default-with-implicit-consent"></a>既定でのパッケージの復元 (暗黙的な同意を含む)

NuGet 2.7 では、パッケージを復元するための新しい方法が導入されています。また、主要なハードルを克服することもできます。パッケージの復元の同意が既定でオンになっています。 新しいアプローチと暗黙の同意を組み合わせることにより、パッケージの復元シナリオが大幅に簡素化されます。

#### <a name="implicit-consent"></a>暗黙的な同意

NuGet バージョン2.0、2.1、2.2、2.5、および2.6 では、ビルド中に不足しているパッケージのダウンロードを NuGet に明示的に許可する必要があります。 この同意が明示的に指定されていない場合、パッケージの復元を有効にしたソリューションは、ユーザーが同意を許可されるまでビルドに失敗します。

NuGet 2.7 以降では、パッケージ復元の同意は既定で有効になっていますが、ユーザーは必要に応じてパッケージの復元*を明示的*に無効にすることができます。また、Visual Studio の nuget の [設定] にあるチェックボックスを使用します。 暗黙的な同意のこの変更は、次の環境での NuGet に影響します。

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe コマンドラインユーティリティ

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio でのパッケージの自動復元

NuGet 2.7 以降では、ソリューションに対してパッケージの復元が明示的に有効化されていない場合でも、Visual Studio でのビルド中に不足しているパッケージが自動的にダウンロードされます。 この自動パッケージ復元は、プロジェクトまたはソリューションをビルドするときに MSBuild が呼び出される前に、Visual Studio で行われます。 これには、いくつかの大きな利点があります。

1. ソリューションで [NuGet パッケージの復元を有効にする] ジェスチャを使用する必要はありません
1. プロジェクトを変更する必要はありません。 NuGet はプロジェクトに変更を加えて、パッケージの復元が有効になっていることを確認します。
1. すべての NuGet パッケージ (props/ターゲットファイルの MSBuild インポートを含むものを含む) は、msbuild が呼び出される*前に*復元され、ビルド時にこれらのプロパティの props とターゲットが正しく認識されるようにします。

Visual Studio で自動パッケージ復元を使用するには、1つの (in) 操作のみを実行する必要があります。

1. `packages`フォルダーをチェックインしないでください

ソース管理からフォルダーを省略する`packages`には、いくつかの方法があります。 詳細については、「[パッケージとソース管理](../consume-packages/packages-and-source-control.md)」を参照してください。

すべてのユーザーが自動パッケージ復元の同意を暗黙的に選択しますが、Visual Studio でパッケージマネージャーの設定を簡単にオプトアウトできます。

![パッケージマネージャーの設定](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>コマンドラインからのパッケージの復元の簡略化

NuGet 2.7 では、nuget.exe の新機能が導入されました。`nuget.exe restore`

この新しい復元コマンドを使用すると、ソリューションファイルまたはフォルダーを引数として受け入れることで、1つのコマンドでソリューションのすべてのパッケージを簡単に復元できます。 さらに、現在のフォルダーにソリューションが1つしかない場合は、その引数が暗黙的に指定されます。 つまり、次のすべての作業は、単一のソリューションファイル (MySolution .sln) を含むフォルダーから実行されます。

1. nuget.exe restore MySolution.sln
1. nuget.exe restore .
1. nuget.exe restore

Restore コマンドを実行すると、ソリューションファイルが開き、ソリューション内のすべてのプロジェクトが検索されます。 そこから、各プロジェクトの`packages.config`ファイルが検索され、見つかったすべてのパッケージが復元されます。 また、 `.nuget\packages.config`ファイルで見つかったソリューションレベルのパッケージも復元します。 新しい復元コマンドの詳細については、「[コマンドラインリファレンス](../reference/cli-reference/cli-ref-restore.md)」を参照してください。

#### <a name="the-new-package-restore-workflow"></a>新しいパッケージの復元ワークフロー

このような変更は、新しいワークフローが導入されているため、パッケージの復元に関するものです。 ソース管理からパッケージを除外する場合は、単にフォルダーを`packages`コミットしません。 ソリューションを開いてビルドした Visual Studio ユーザーには、自動的に復元されたパッケージが表示されます。 コマンドラインビルドの場合は、を`nuget.exe restore`呼び出す`msbuild`前にを呼び出します。 ソリューションで "NuGet パッケージの復元を有効にする" ジェスチャを使用することを忘れずに、プロジェクトを変更してビルドを変更する必要がなくなりました。 また、これにより、MSBuild インポートを含むパッケージのエクスペリエンスが大幅に向上します。特に、\ build フォルダーから[props/ターゲットファイルを自動的にインポート](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files)するために NuGet の最新機能を使用して追加されたインポートの場合は、非常に改善されています。

私たちは自分で行った作業に加えて、この新しいアプローチを実現するために、いくつかの重要なパートナーとも連携しています。これらのいずれについても具体的なタイムラインはありませんが、新しいアプローチについては、それぞれのパートナーが非常に興奮しています。

* Team Foundation Service-の呼び出し`nuget.exe restore`を既定のビルドシナリオに統合するために動作しています。
* Windows azure websites-プロジェクトを azure にプッシュし`nuget.exe restore` 、Web サイトを構築する前にを呼び出すことができるようにするために機能しています。
* TeamCity-TeamCity 8. x の NuGet インストーラープラグインを更新しています
* Appharbor-これらの機能は、リポジトリを appharbor にプッシュし`nuget.exe restore` 、ソリューションをビルドする前にを呼び出すことができるようにするために動作しています。

上記の各パートナーは、独自の nuget.exe コピーを使用して、ソリューションで nuget.exe を実行する必要はありません。

#### <a name="known-issues"></a>既知の問題

最初の2.7 リリースでは、nuget.exe の復元に関して2つの既知の問題がありましたが、これらは9/6/2013 で修正され、 [nuget.exe パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)が更新されました。  この更新プログラムは、CodePlex の[NuGet 2.7 ダウンロードページ](https://nuget.codeplex.com/releases/view/107605)でも利用できます。  を`nuget.exe update -self`実行すると、最新のリリースに更新されます。

修正されたは次のとおりです。

1. [.SLN ファイルを使用すると、新しいパッケージの復元が Mono で機能しない](https://nuget.codeplex.com/workitem/3596)
1. [新しいパッケージの復元が Wix プロジェクトで機能しない](https://nuget.codeplex.com/workitem/3598)

また、新しいパッケージ復元ワークフローには既知の問題もあります。これにより、[パッケージの自動復元は、ソリューションフォルダーの下にあるプロジェクトに対しては機能しません](https://nuget.codeplex.com/workitem/3625)。 この問題は NuGet 2.7.1 で修正されました。

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Project 再ターゲットと Upgrade ビルドのエラー/警告

プロジェクトを再ターゲットまたはアップグレードした後は、いくつかの NuGet パッケージが正常に機能していないことがわかります。 残念ながら、これについては何も示されていません。その対処方法についてのガイダンスはありません。 NuGet 2.7 では、Visual Studio のイベントを使用して、インストールされている NuGet パッケージに影響を与えるような方法でプロジェクトを再ターゲットまたはアップグレードしたことを認識するようになりました。

再ターゲットまたは upgrade の影響を受けたパッケージが検出された場合は、すぐにビルドエラーを生成して通知します。 即時ビルドエラーに加えて、再ターゲットによって影響`requireReinstallation="true"`を受けた`packages.config`すべてのパッケージのフラグがファイルに保持されます。また、Visual Studio の後続のビルドでは、これらのパッケージのビルド警告が発生します。

NuGet は、影響を受けるパッケージを再インストールするための自動アクションを実行することはできませんが、パッケージを再インストールする必要がある場合は、このことを確認し、警告が表示されるようにしてください。 また、このようなエラーメッセージが表示される[パッケージ再インストールガイダンスドキュメント](../consume-packages/reinstalling-and-updating-packages.md)にも取り組んでいます。

### <a name="nuget-configuration-defaults"></a>NuGet の構成の既定値

多くの企業では、内部的に NuGet を使用していますが、開発者が nuget.org ではなく内部パッケージソースを使用するように、ハードタイムを設定していました。NuGet 2.7 では、次のようにマシン全体の既定値を指定できる構成の既定の機能が導入されています。

1. 有効なパッケージソース
1. 登録済みですが、無効になっているパッケージソース
1. 既定の nuget.exe プッシュソース

これらの各は、にあるファイル内で構成できる`%ProgramData%\NuGet\NuGetDefaults.Config`ようになりました。 この構成ファイルでパッケージソースが指定されている場合、既定の nuget.org パッケージソースは自動的に登録さ`NuGetDefaults.Config`れず、内にあるものも登録されます。

この機能を使用する必要はありませんが、企業`NuGetDefaults.Config`はグループポリシーを使用してファイルを展開することを想定しています。

*この機能では、パッケージソースが開発者の NuGet 設定から削除されることはないことに注意してください。つまり、開発者が既に NuGet を使用していて、nuget.org パッケージソースが登録されている場合は、 `NuGetDefaults.Config`ファイルの作成後に削除されません。*

この機能の詳細については、「 [NuGet の構成の既定値](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file)」を参照してください。

### <a name="renaming-the-default-package-source"></a>既定のパッケージソースの名前変更

NuGet は、nuget.org を指す "NuGet 公式パッケージソース" と呼ばれる既定のパッケージソースを常に登録しています。その名前は詳細で、実際にポイントした場所も指定していませんでした。 この2つの問題に対処するために、このパッケージソースの名前を UI の "nuget.org" に変更しました。 パッケージソースの URL も "www" を含むように変更されました。 プレフィックスを含むバンドル ID です。 Nuget 2.7 を使用すると、既存の "nuget 公式パッケージソース" は、その名前<https://www.nuget.org/api/v2/>として "nuget.org" に自動的に更新され、URL として "" に更新されます。

### <a name="performance-improvements"></a>パフォーマンスの向上

2\.7 のパフォーマンスが向上しました。これにより、メモリフットプリントが小さくなり、ディスク使用量が少なくなり、パッケージのインストールが高速になります。 また、OData ベースのフィードに対してよりスマートなクエリを実行し、ペイロード全体を削減します。

### <a name="new-extensibility-apis"></a>新しい機能拡張 Api

以前のリリースでは、不足している機能のギャップを埋めるために、機能拡張サービスに新しい Api がいくつか追加されました。

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

この機能は[Adam Ralph](https://twitter.com/adamralph)によって提供されており、パッケージの作成者は、開発時にのみ使用され、パッケージの依存関係を必要としない依存関係を宣言できます。 で`developmentDependency="true"` `nuget.exe pack`パッケージに属性を追加すると、そのパッケージが依存関係として含まれなくなります。 `packages.config`

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Visual Studio 2010 Express for Windows Phone のサポートが削除されました

2\.7 の新しいパッケージ復元モデルは、メインの NuGet VSPackage とは異なる新しい VSPackage によって実装されます。 技術的な問題により、この新しい VSPackage は、 *Visual studio 2010 Express for Windows Phone* SKU では正しく機能しません。これは、サポートされている他の Visual studio sku と同じコードベースを共有するためです。 そのため、NuGet 2.7 以降、発行された拡張機能から*Visual Studio 2010 Express for Windows Phone*のサポートを削除しています。 Visual studio *2010 Express For Web*のサポートは、Visual Studio 拡張機能ギャラリーに公開されているプライマリ拡張機能にまだ含まれています。

Visual Studio のバージョン/エディションではまだ NuGet を使用している開発者の数がわからないため、visual studio 拡張機能ギャラリーではなく、ユーザー専用の個別の Visual Studio 拡張機能を公開し、CodePlex で公開します. この拡張機能を引き続き維持する予定はありませんが、それが影響を受ける場合は、CodePlex で問題を提出してお知らせください。

NuGet パッケージマネージャー (Visual Studio 2010 Express for Windows Phone) をダウンロードするには、 [nuget 2.7 のダウンロード](https://nuget.codeplex.com/releases/view/107605)ページにアクセスしてください。

### <a name="bug-fixes"></a>バグ修正

これらの機能に加えて、この NuGet のリリースには、他にも多くのバグ修正が含まれています。 リリースで解決された問題の合計は97でした。 NuGet 2.7 で修正された作業項目の完全な一覧については、[このリリースの Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)を参照してください。
