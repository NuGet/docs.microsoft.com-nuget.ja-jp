---
title: NuGet 1.4 のリリース ノート
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.4 のリリース ノートします。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5e4c2a5f2db80b0ebc3fec7c653aecb8bcc4ab5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822059"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 のリリース ノート

[NuGet 1.3 リリース ノート](../release-notes/nuget-1.3.md) | [NuGet 1.5 のリリース ノート](../release-notes/nuget-1.5.md)

NuGet 1.4 は、2011 年 6 月 17 日にリリースされました。

## <a name="features"></a>フィーチャー

### <a name="update-package-improvements"></a>更新プログラム パッケージの機能強化
NuGet 1.4 には、多数の更新プログラム パッケージ コマンドがソリューション内の複数のプロジェクトにわたって、同じバージョンにパッケージを維持するが容易に機能強化が導入されています。 たとえば、パッケージを最新バージョンにアップグレードする場合は、ごく一般的を同じバージョンに更新するインストール パッケージにすべてのプロジェクトを選択します。

`Update-Package`コマンドようになりましたしやすきます。

#### <a name="update-all-packages-in-a-single-project"></a>1 つのプロジェクトのすべてのパッケージを更新します。

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>すべてのプロジェクトでパッケージを更新します。

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>すべてのプロジェクト内のすべてのパッケージを更新します。

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>すべてのパッケージに対して「安全な」の更新を実行します。
`-Safe`フラグが同じメジャーおよびマイナー バージョン コンポーネントを含む唯一のバージョンにアップグレードを制限します。 たとえば、パッケージの version 1.0.0 がインストールされているし、バージョン 1.0.1、1.0.2、および 1.1 がフィードで使用可能な場合、`-Safe`フラグによってパッケージが 1.0.2 に更新します。 なくをアップグレードする、`-Safe`フラグは、最新のバージョン 1.1 に、パッケージをアップグレードするとします。

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>ソリューション レベルでのパッケージを管理します。
NuGet 1.4 の前に、複数のプロジェクトにパッケージをインストールする、ダイアログを使用して複雑でした。 プロジェクトごとに 1 回 ダイアログを起動することが必要です。

NuGet 1.4 は、同時に複数のプロジェクトでパッケージのインストール/アンインストール/更新のサポートを追加します。 単を起動して、ソリューションを右クリックしを選択すると、 **NuGet パッケージの管理**メニュー オプション。

![ソリューションの NuGet パッケージの管理レベル ダイアログ](./media/manage-nuget-packages-solution-dialog.png)

ダイアログ ボックスのタイトル バーで、ソリューションの名前が表示されることに注意してください、プロジェクト名ではありません。
パッケージの操作は、プロジェクトに適用操作の一覧と対応するチェック ボックスの一覧を提供するようになりました。

![NuGet パッケージのプロジェクトの選択範囲を管理します。](./media/manage-nuget-packages-project-selection.png)

詳細については、のトピックを参照してください。[ソリューションのパッケージを管理する](../tools/package-manager-ui.md#managing-packages-for-the-solution)です。

### <a name="constraining-upgrades-to-allowed-versions"></a>許容バージョンにアップグレードを制限します。
既定を実行しているときに、`Update-Package`コマンドをパッケージ (またはダイアログを使用してパッケージを更新して)、フィード内の最新バージョンに更新されます。 すべてのパッケージを更新するための新しいサポート、特定のバージョンの範囲内にパッケージをロックする場合があります。 たとえば、可能性がありますがあらかじめわかって、アプリケーションが 3.0 ではありませんが、以降、パッケージのバージョン 2.* でのみ使用できます。 パッケージは、手動で編集にアップグレードできるバージョンの範囲を制限するサポートを追加する NuGet 1.4 を誤って 3 に、パッケージの更新を回避するために、`packages.config`新しいツールを使用して`allowedVersions`属性。

たとえば、次の例をロックする方法、`SomePackage`パッケージ バージョン 2.0、3.0 (排他) の範囲です。
`allowedVersions`属性を使用して値を受け入れる、[バージョン範囲形式](../reference/package-versioning.md#version-ranges-and-wildcards)です。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

1.4 で特定のバージョンの範囲内にパッケージをロックする必要があります手動で編集に注意してください。 使用してこの範囲を配置するためのサポートを追加する NuGet 1.5 の予定、`Install-Package`コマンド。

### <a name="package-visualizer"></a>パッケージのビジュアライザー
新しいパッケージ ビジュアライザーから起動、**ツール** -> **ライブラリ パッケージ マネージャー** -> **パッケージ ビジュアライザー**メニュー オプションを有効にします。すべてのプロジェクトおよびソリューション内でそのパッケージの依存関係を簡単に視覚化できます。

_**重要なメモ:** この機能では、Visual Studio の DGML サポートの活用します。視覚エフェクトの作成は、Visual Studio Ultimate でのみサポートされます。DGML 図の表示は、Visual Studio Premium または高でのみサポートされます。_

![パッケージのビジュアライザー](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet のダイアログ ボックスの自動更新チェック
一部のバージョンの NuGet 経由で表される新しい機能が導入されて、 `.nuspec` NuGet のダイアログ ボックスの以前のバージョンによって認識されないファイルです。
1 つの例は、の NuGet 1.4 の導入[フレームワーク アセンブリを指定する](../release-notes/nuget-1.2.md#framework-assembly-refs)です。
このためには、NuGet の最新バージョンを使用して、最新の機能を活用するパッケージを使用することを確認する必要があります。
NuGet への更新プログラムを目立たせる、NuGet のダイアログには、新しいバージョンが利用可能なときに強調表示するためのロジックが含まれています。

_**注**: 場合にのみ、チェックが行われます、**オンライン**現在のセッション タブが選択されています。_

![使用可能な新しいバージョンの NuGet パッケージ ダイアログを管理します。](./media/manage-nuget-packages-update-notification.png)

更新プログラムの自動チェックをオフに NuGet の [設定] ダイアログ ボックスに移動し、オフにして**更新プログラムを自動的に確認**です。

![NuGet の設定](./media/nuget-settings.png)

この機能は、NuGet 1.3 で実際に追加されましたは表示されません、もちろん、NuGet 1.4 など、1.3 を更新するまでに用意されていました。

### <a name="package-manager-dialog-improvements"></a>パッケージ マネージャー ダイアログ ボックスの機能強化
* **メニュー名向上**: わかりやすくするためのダイアログを起動するメニュー オプションが変更されました。 メニュー オプションは、今すぐ**NuGet パッケージの管理**です。
* **詳細ペインが最新の更新日を表示**: NuGet ダイアログは、詳細ウィンドウで、パッケージの最新の更新プログラムの日付を表示時に、**オンライン**または**更新**タブが選択されています。
* **表示されているタグの一覧**: Nuget ダイアログには、タグが表示されます。

### <a name="powershell-improvements"></a>Powershell の機能強化
* **PowerShell スクリプトを署名**: NuGet にはより制限の厳しい環境で使用状況を有効にすると、署名済みの Powershell スクリプトが含まれています。
* **サポートを求める**:「パッケージ マネージャー コンソールでは経由でメッセージを表示、`$host.ui.Prompt`と`$host.ui.PromptForChoice`コマンド。
* **ソース名をパッケージ化**: を使用してパッケージ ソースを指定する場合はサポートされてパッケージ ソースの名前を指定して、`-Source`フラグ。

### <a name="nugetexe-command-line-improvements"></a>nuget.exe コマンドラインの機能強化
* **カスタムの NuGet コマンド**: nuget.exe は MEF を使用してカスタムのコマンドを使用して拡張できます。
* **単純なシンボル パッケージを作成するためのワークフロー**:`-Symbols`フラグのみ、ソースを含めることによってシンボル パッケージを作成する標準規約に基づくフォルダー構造に適用できますと`.pdb`フォルダー内のファイルです。
* **複数のソースを指定する**:`NuGet install`コマンドでは、区切り記号としてセミコロンを使用を指定することによって複数のソースを指定することがサポートする`-Source`複数回です。
* **プロキシ認証がサポート**: NuGet 1.4 は、NuGet を使用して認証を必要とするプロキシの背後にあるときにユーザーの資格情報の入力を求めてのサポートを追加します。
* **nuget.exe 互換性に影響する変更の更新**:`-Self`フラグが、それ自体を更新する nuget.exe のために必要なです。 `nuget.exe Update` パスでは、`packages.config`ファイルし、パッケージの更新を試みます。 されませんが、この更新プログラムが制限されるに注意してください: * * 更新、追加、プロジェクト ファイルのコンテンツを削除します。
* *、パッケージ内の Powershell スクリプトを実行します。

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Nuget.exe を使用したプッシュのパッケージの NuGet サーバーのサポート
NuGet にホストを簡単な方法が含まれています、[かつ軽量の web ベースの NuGet リポジトリ](../hosting-packages/nuget-server.md)を介して、 `NuGet.Server` NuGet パッケージです。 NuGet 1.4 では、軽量なサーバーは、プッシュおよび nuget.exe を使用してパッケージの削除をサポートします。
最新バージョン`NuGet.Server`新しい`appSetting`、名前付き`apiKey`します。 キーを省略するか、空白のまま、フィードへのパッケージのプッシュが無効になります。 ApiKey を値 (理想的には強力なパスワード) に設定すると、nuget.exe を使用したプッシュのパッケージが有効になります。

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Windows Phone ツール Mango Edition のサポート
NuGet は、Windows Phone 用のツール Mango リリース候補版ではサポートされています。
現時点では、Windows Phone ツールには、Windows Phone ツールの NuGet をインストールするための Visual Studio 拡張機能マネージャーのサポートはありません、ダウンロードして、VSIX を手動で実行する必要があります。

Windows Phone NuGet ツールをアンインストールするには、次のコマンドを実行します。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>バグ修正
NuGet 1.4 は、作業項目の固定 88 の合計がありました。 これらの 71 はバグとしてマークされています。

作業の完全な一覧アイテムを固定 NuGet 1.4 にしてください。 ビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。

## <a name="bug-fixes-worth-noting"></a>注目すべきバグ修正:

* [問題 603](http://nuget.codeplex.com/workitem/603): 特定のパッケージ ソースを指定するときに、別のリポジトリ パッケージの依存関係が適切に解決します。
* [問題 1036](http://nuget.codeplex.com/workitem/1036): 追加`NuGet Pack SomeProject.csproj`ビルド後イベントに不要になったに無限ループが発生します。
* [問題 961](http://nuget.codeplex.com/workitem/961):`-Source`フラグは、相対パスをサポートしています。

## <a name="nuget-14-update"></a>NuGet 1.4 の更新
NuGet 1.4 のリリースでは、すぐ後に、いくつかの修正する必要がある問題が見つかりました。
1.4 にこの更新プログラムの特定のバージョン番号は、1.4.20615.9020 です。

### <a name="bug-fixes"></a>バグ修正
* [問題 1220](http://nuget.codeplex.com/workitem/1220): 更新プログラム パッケージを実行しない`install.ps1` / `uninstall.ps1`で複数のプロジェクトがある場合に、すべてのプロジェクト
* [問題 1156](http://nuget.codeplex.com/workitem/1156): (Powershell 2 がインストールされていない) 場合、パッケージ マネージャー コンソールが W2K3/XP にスタックしました。
