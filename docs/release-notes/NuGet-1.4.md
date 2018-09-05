---
title: NuGet 1.4 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.4 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550632"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 リリース ノート

[NuGet 1.3 のリリース ノート](../release-notes/nuget-1.3.md) | [NuGet 1.5 のリリース ノート](../release-notes/nuget-1.5.md)

NuGet 1.4 は、2011 年 6 月 17 日にリリースされました。

## <a name="features"></a>フィーチャー

### <a name="update-package-improvements"></a>更新プログラム パッケージの機能強化
NuGet 1.4 には、多数のバージョンが同じで、ソリューション内の複数のプロジェクトでパッケージを維持しやすく更新プログラム パッケージ コマンドに機能強化が導入されています。 たとえば、パッケージを最新バージョンをアップグレードする場合、すべてのプロジェクトを同じバージョンに更新するインストール パッケージにするのには非常に一般的なは。

`Update-Package`コマンド今すぐ簡単になります。

#### <a name="update-all-packages-in-a-single-project"></a>1 つのプロジェクトでパッケージをすべて更新します。

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>すべてのプロジェクトでパッケージを更新します。

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>すべてのプロジェクトでパッケージをすべて更新します。

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>すべてのパッケージで「安全」更新を実行します。
`-Safe`フラグが同じメジャーおよびマイナー バージョン コンポーネントとの唯一のバージョンにアップグレードを制約します。 たとえば、バージョン 1.0.0 のパッケージがインストールされている場合、バージョン 1.0.1、1.0.2、および 1.1 が、フィードで利用可能な場合、 `-Safe` 1.0.2 フラグによって、パッケージを更新します。 なしのアップグレード、`-Safe`フラグは、パッケージが最新バージョン 1.1 にアップグレードします。

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>ソリューション レベルでパッケージを管理します。
NuGet 1.4 では、前に、複数のプロジェクトにパッケージをインストール ダイアログを使用して面倒でした。 プロジェクトごとに 1 回 ダイアログを起動することが必要です。

NuGet 1.4 では、同時に複数のプロジェクトのパッケージのインストール/アンインストール/更新のサポートを追加します。 単に起動、ソリューションを右クリックしを選択すると、 **NuGet パッケージの管理**メニュー オプション。

![ソリューションの NuGet パッケージの管理レベル ダイアログ](./media/manage-nuget-packages-solution-dialog.png)

ダイアログのタイトル バーで、ソリューションの名前が表示されることに注意してください、プロジェクトの名前ではありません。
パッケージの操作は、プロジェクトに適用する操作の一覧でチェック ボックスの一覧を提供します。

![管理の NuGet パッケージのプロジェクトの選択](./media/manage-nuget-packages-project-selection.png)

詳細については、上のトピックを参照してください。[ソリューションのパッケージを管理する](../tools/package-manager-ui.md#managing-packages-for-the-solution)します。

### <a name="constraining-upgrades-to-allowed-versions"></a>許容バージョンにアップグレードの制約
既定で実行するときに、`Update-Package`パッケージ (またはダイアログを使用してパッケージを更新しています) で、コマンドは、フィードで最新バージョンに更新します。 すべてのパッケージを更新するための新しいサポート、特定のバージョン範囲にパッケージをロックする場合があります。 たとえば、ご存知かも事前に、アプリケーションは、パッケージ、3.0 ではありませんが、以降のバージョン 2. * でのみ動作します。 NuGet 1.4 を誤って 3 に、パッケージの更新を回避するために手動で編集してパッケージをアップグレードできるバージョンの範囲を制限するサポートの追加、 `packages.config` 、新しいツールを使用して`allowedVersions`属性。

たとえば、次の例をロックする方法を示しています。、`SomePackage`パッケージ バージョンの範囲 (排他) の 2.0 ~ 3.0。
`allowedVersions`属性を使用して値を受け入れる、[バージョン範囲の形式](../reference/package-versioning.md#version-ranges-and-wildcards)します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

なお、1.4 でパッケージを特定のバージョン範囲をロックする必要があります手動で編集です。 NuGet 1.5 ではこの範囲を使用して配置するためのサポートを追加する予定の`Install-Package`コマンド。

### <a name="package-visualizer"></a>パッケージのビジュアライザー
使用して起動される、新しいパッケージ ビジュアライザー、**ツール** -> **ライブラリ パッケージ マネージャー** -> **パッケージ ビジュアライザー**のメニュー オプションを使用します。すべてのプロジェクトおよびソリューション内でそのパッケージの依存関係を簡単に視覚化します。

_**重要な注意:** この機能では、Visual Studio の DGML サポートの活用。視覚エフェクトを作成するは、Visual Studio Ultimate でのみサポートされます。Visual Studio Premium または高では、DGML 図を表示することはサポートされてのみ。_

![パッケージのビジュアライザー](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet ダイアログの自動更新のチェック
いくつかのバージョンの NuGet を使用して表される新しい機能が導入されて、 `.nuspec` NuGet ダイアログ ボックスの以前のバージョンによって認識されないファイル。
1 つの例は導入の NuGet 1.4 で[フレームワーク アセンブリを指定する](../release-notes/nuget-1.2.md#framework-assembly-refs)します。
このため、NuGet の最新バージョンを使用して、最新の機能を活用するパッケージを使用することを確認する重要ななります。
NuGet に更新プログラムをよりわかりやすいように、NuGet ダイアログには、新しいバージョンがあるときに強調表示するためのロジックが含まれています。

_**注**: 場合にのみ、チェックが行われます、**オンライン** タブは、現在のセッションで選択されています。_

![管理可能な新しいバージョンの NuGet パッケージの ダイアログ ボックス](./media/manage-nuget-packages-update-notification.png)

更新プログラムの自動チェックをオフに、NuGet の設定 ダイアログに移動し、オフに**更新プログラムを自動的に確認**します。

![NuGet の設定](./media/nuget-settings.png)

この機能は、NuGet の 1.3 で実際に追加されましたは表示されません、もちろん、1.3、1.4 の NuGet などの更新プログラムまで、利用できるようにしました。

### <a name="package-manager-dialog-improvements"></a>パッケージ マネージャー ダイアログの改良
* **メニュー名の改善**: わかりやすくするためのダイアログ ボックスを表示するメニュー オプションが変更されています。 メニュー オプションは現在**NuGet パッケージの管理**します。
* **詳細ウィンドウには、最新の更新日が表示されます。**: NuGet ダイアログは、パッケージの詳細ウィンドウで、最新の更新プログラムの日付を表示しますときに、**オンライン**または**更新**タブが選択されます。
* **表示されているタグの一覧**: Nuget ダイアログには、タグが表示されます。

### <a name="powershell-improvements"></a>Powershell の機能強化
* **PowerShell スクリプトを署名**: NuGet より制限の厳しい環境での使用状況を有効にすると、署名済みの Powershell スクリプトが含まれています。
* **サポートを求める**: パッケージ マネージャー コンソール サポートを使用して入力を求める、`$host.ui.Prompt`と`$host.ui.PromptForChoice`コマンド。
* **ソース名をパッケージ化**: を使用してパッケージ ソースを指定する場合はパッケージ ソースの名前を指定して、`-Source`フラグ。

### <a name="nugetexe-command-line-improvements"></a>nuget.exe コマンドラインの機能強化
* **カスタムの NuGet コマンド**: nuget.exe は MEF を使用してカスタムのコマンドを使用して拡張します。
* **単純なシンボル パッケージを作成するためのワークフロー**:`-Symbols`のみ、ソースを含めることで、シンボル パッケージを作成する通常の規則ベースのフォルダー構造に適用できるフラグと`.pdb`フォルダー内のファイル。
* **複数のソースを指定する**:`NuGet install`コマンドかを指定して、区切り記号としてセミコロンを使用して複数のソースの指定をサポートしている`-Source`複数回です。
* **プロキシ認証のサポート**: NuGet 1.4 は、認証が必要なプロキシの背後にある NuGet を使用する場合は、ユーザーの資格情報の入力を求めるサポートを追加します。
* **nuget.exe 重大な変更を更新**:`-Self`フラグが、nuget.exe 自体を更新するために必要な。 `nuget.exe Update` パスでは、`packages.config`ファイルし、パッケージを更新しようとします。 これを行わないことで、この更新プログラムが制限されることに注意してください: * * 更新、追加、プロジェクト ファイルのコンテンツを削除します。
* *、パッケージ内での Powershell スクリプトを実行します。

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Nuget.exe を使用してプッシュのパッケージの NuGet サーバーのサポート
NuGet にホストする簡単な方法が含まれています、[かつ軽量の web ベースの NuGet リポジトリ](../hosting-packages/nuget-server.md)を使用して、 `NuGet.Server` NuGet パッケージ。 NuGet 1.4 とは、軽量のサーバーは、プッシュと nuget.exe を使用してパッケージの削除をサポートします。
最新バージョンの`NuGet.Server`新しい`appSetting`、名前付き`apiKey`します。 キーを省略して空白のままにするか、フィードにパッケージをプッシュは無効になります。 ApiKey を値 (理想的には強力なパスワード) に設定すると、nuget.exe を使用したプッシュのパッケージが有効になります。

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Windows Phone Tools Mango エディションのサポート
Windows Phone Mango ツールのリリース候補版では、NuGet がサポートされています。
現時点では、Windows Phone ツールには、Windows Phone NuGet ツールをインストールするための Visual Studio 拡張機能マネージャーのサポートはありません、ダウンロードして、VSIX を手動で実行する必要があります。

Windows Phone NuGet ツールをアンインストールするには、次のコマンドを実行します。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>バグ修正
NuGet 1.4 では、作業項目の固定が 88 の合計がありました。 これらの 71 はバグとしてマークされています。

作業の完全な一覧の項目で修正された NuGet 1.4、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)します。

## <a name="bug-fixes-worth-noting"></a>注目すべきバグ修正:

* [問題 603](http://nuget.codeplex.com/workitem/603): 特定のパッケージ ソースを指定するときに異なるリポジトリ間でパッケージの依存関係が正しく解決します。
* [問題 1036](http://nuget.codeplex.com/workitem/1036): 追加`NuGet Pack SomeProject.csproj`ビルド後イベントにできなくする無限ループが発生します。
* [問題 961](http://nuget.codeplex.com/workitem/961):`-Source`フラグは、相対パスをサポートしています。

## <a name="nuget-14-update"></a>NuGet 1.4 の更新
NuGet 1.4 のリリースでは、直後に解決する重要な問題のいくつかがわかりました。
この更新プログラムの 1.4 の特定のバージョン番号は、1.4.20615.9020 です。

### <a name="bug-fixes"></a>バグ修正
* [問題 1220](http://nuget.codeplex.com/workitem/1220): 更新プログラム パッケージは実行されません`install.ps1` / `uninstall.ps1`で 1 つ以上のプロジェクトがある場合に、すべてのプロジェクト
* [問題 1156](http://nuget.codeplex.com/workitem/1156): (Powershell 2 がインストールされていない) 場合に、パッケージ マネージャー コンソールが W2K3/xp スタック
