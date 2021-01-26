---
title: NuGet 1.4 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.4 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777145"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 リリースノート

[NuGet 1.3 リリースノート](../release-notes/nuget-1.3.md)  | [NuGet 1.5 リリースノート](../release-notes/nuget-1.5.md)

NuGet 1.4 は、2011年6月17日にリリースされました。

## <a name="features"></a>特徴

### <a name="update-package-improvements"></a>Update-Package の機能強化
NuGet 1.4 では、Update-Package コマンドが大幅に改善され、ソリューション内の複数のプロジェクトで同じバージョンのパッケージを簡単に保持できるようになりました。 たとえば、パッケージを最新バージョンにアップグレードする場合、そのパッケージがインストールされているすべてのプロジェクトを同じバージョンに更新することが非常に一般的です。

`Update-Package`コマンドを使用すると、次の操作が簡単になります。

#### <a name="update-all-packages-in-a-single-project"></a>1つのプロジェクト内のすべてのパッケージを更新する

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a>すべてのプロジェクトのパッケージを更新する

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a>すべてのプロジェクトのすべてのパッケージを更新する

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a>すべてのパッケージに対して "安全な" 更新を実行する
フラグは、 `-Safe` メジャーバージョンとマイナーバージョンの同じコンポーネントを持つバージョンにのみアップグレードを制限します。 たとえば、パッケージのバージョン1.0.0 がインストールされていて、バージョン1.0.1、1.0.2、および1.1 がフィードで使用できる場合、このフラグによって `-Safe` パッケージが1.0.2 に更新されます。 フラグを指定せず `-Safe` にアップグレードすると、パッケージが最新バージョン1.1 にアップグレードされます。

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a>ソリューションレベルでのパッケージの管理
NuGet 1.4 より前では、複数のプロジェクトへのパッケージのインストールは、ダイアログを使用すると煩雑でした。 プロジェクトごとに1回ダイアログを起動する必要があります。

NuGet 1.4 では、複数のプロジェクトで同時にパッケージをインストール/アンインストール/更新するためのサポートが追加されています。 を起動するには、ソリューションを右クリックし、[ **NuGet パッケージの管理** ] メニューオプションを選択します。

![ソリューションレベルの NuGet パッケージの管理ダイアログ](./media/manage-nuget-packages-solution-dialog.png)

ダイアログのタイトルバーには、プロジェクトの名前ではなく、ソリューションの名前が表示されていることに注意してください。
パッケージ操作で、操作を適用するプロジェクトの一覧を含むチェックボックスの一覧が提供されるようになりました。

![NuGet パッケージプロジェクト選択の管理](./media/manage-nuget-packages-project-selection.png)

詳細については、 [ソリューションのパッケージの管理](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)に関するトピックを参照してください。

### <a name="constraining-upgrades-to-allowed-versions"></a>許可されているバージョンへのアップグレードを制限する
既定で `Update-Package` は、パッケージに対してコマンドを実行する (または、ダイアログを使用してパッケージを更新する) と、フィードの最新バージョンに更新されます。 すべてのパッケージを更新するための新しいサポートでは、パッケージを特定のバージョン範囲にロックすることが必要になる場合があります。 たとえば、アプリケーションが3.0 以降ではなく、パッケージのバージョン 2. * のみで動作することが事前にわかっている場合があります。 パッケージが誤って3に更新されないようにするため、NuGet 1.4 では、新しい属性を使用してファイルを手動で編集することによって、パッケージをアップグレードできるバージョンの範囲を制限するためのサポートが追加さ `packages.config` `allowedVersions` れています。

たとえば、次の例では、 `SomePackage` パッケージをバージョン範囲 2.0-3.0 (排他) にロックする方法を示しています。
属性は、 `allowedVersions` [バージョン範囲形式](../concepts/package-versioning.md#version-ranges)を使用して値を受け入れます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

1.4 では、特定のバージョン範囲へのパッケージのロックを手動で編集する必要があることに注意してください。 NuGet 1.5 では、コマンドを使用して、この範囲を配置するためのサポートを追加する予定 `Install-Package` です。

### <a name="package-visualizer"></a>パッケージビジュアライザー
[**ツール** ライブラリパッケージマネージャーパッケージビジュアライザー] メニューオプションを使用して起動された新しいパッケージビジュアライザーを使用すると、  ->    ->  ソリューション内のすべてのプロジェクトとそのパッケージの依存関係を簡単に視覚化できます。

_**重要な注意:** この機能は、Visual Studio の DGML サポートを利用します。視覚エフェクトの作成は、Visual Studio Ultimate でのみサポートされています。DGML 図の表示は Visual Studio Premium 以降でのみサポートされています。_

![パッケージビジュアライザー](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet ダイアログの自動更新チェック
NuGet のバージョンによっては、 `.nuspec` 古いバージョンの nuget ダイアログでは認識されない、ファイルによって表される新機能が導入されています。
1つの例として、 [フレームワークアセンブリを指定](../release-notes/nuget-1.2.md#framework-assembly-refs)するための NuGet 1.4 の概要を示します。
このため、最新バージョンの NuGet を使用して、最新の機能を利用してパッケージを使用できるようにすることが重要です。
NuGet の更新をより見やすくするために、NuGet ダイアログには、新しいバージョンが利用可能になったときに強調表示するロジックが含まれています。

_**注**: 現在のセッションで [ **オンライン** ] タブが選択されている場合にのみチェックが行われます。_

![新しいバージョンを使用できるようになった [NuGet パッケージの管理] ダイアログ](./media/manage-nuget-packages-update-notification.png)

更新プログラムの自動チェックをオフにするには、[NuGet の設定] ダイアログボックスで、[ **更新プログラムの自動確認] チェック** ボックスをオフにします。

![NuGet の設定](./media/nuget-settings.png)

この機能は NuGet 1.3 で実際に追加されましたが、もちろん、NuGet 1.4 などの1.3 の更新が利用可能になるまでは表示されません。

### <a name="package-manager-dialog-improvements"></a>パッケージマネージャーダイアログの機能強化
* **メニュー名が改善** されました: わかりやすくするために、ダイアログを起動するメニューオプションの名前を変更しました。 メニューオプションは **NuGet パッケージを管理** するようになりました。
* [**詳細] ウィンドウに最新の更新日が表示** されます。 [**オンライン**] または [**更新**] タブが選択されている場合、[NuGet] ダイアログには、パッケージの [詳細] ウィンドウに最新の更新プログラムの日付が表示されます。
* **表示されるタグの一覧**: [Nuget] ダイアログにタグが表示されます。

### <a name="powershell-improvements"></a>Powershell の機能強化
* **署名済み powershell スクリプト**: NuGet には、より制限の厳しい環境での使用を可能にする署名付きの powershell スクリプトが含まれています。
* **サポート** の確認: パッケージマネージャーコンソールで、 `$host.ui.Prompt` コマンドとコマンドを使用したプロンプトがサポートされるようになりました `$host.ui.PromptForChoice` 。
* パッケージソース **名**: フラグを使用してパッケージソースを指定するときに、パッケージソースの名前を指定することがサポートされてい `-Source` ます。

### <a name="nugetexe-command-line-improvements"></a>nuget.exe コマンドラインの機能強化
* **NuGet カスタムコマンド**: nuget.exe は、MEF を使用したカスタムコマンドを使用して拡張できます。
* **シンボルパッケージを作成するためのワークフローの簡素化**: フラグは、 `-Symbols` 標準規則ベースのフォルダー構造に適用できます。これにより、フォルダー内にソースとファイルのみを含めることで、シンボルパッケージが作成され `.pdb` ます。
* **複数のソースの指定**: コマンドは、 `NuGet install` セミコロンを区切り記号として使用するか、複数回指定することにより、複数のソースの指定をサポートします `-Source` 。
* **プロキシ認証のサポート**: nuget 1.4 では、認証を必要とするプロキシの背後で nuget を使用するときに、ユーザー資格情報の入力を求めるためのサポートが追加されます。
* **更新** `-Self` に関する重大な変更のnuget.exe: フラグは、nuget.exe を更新するために必要になりました。 `nuget.exe Update` は、ファイルへのパスを取得 `packages.config` し、パッケージの更新を試みます。 この更新は、プロジェクトファイル内のコンテンツの更新、追加、削除を行わないという点で制限されています。
* * パッケージ内で Powershell スクリプトを実行します。

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>nuget.exe を使用したパッケージのプッシュに対する NuGet サーバーのサポート
NuGet には、nuget パッケージを使用して [軽量の web ベースの nuget リポジトリ](../hosting-packages/nuget-server.md) をホストする簡単な方法が用意されてい `NuGet.Server` ます。 NuGet 1.4 では、ライトウェイトサーバーは nuget.exe を使用したパッケージのプッシュと削除をサポートします。
最新バージョンのでは、 `NuGet.Server` という名前の新しいが追加され `appSetting` `apiKey` ます。 キーを省略した場合、または空白のままにした場合、フィードへのパッケージのプッシュは無効になります。 ApiKey を値 (理想的には強力なパスワード) に設定すると、nuget.exe を使用してパッケージをプッシュできます。

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Windows Phone Tools Mango Edition のサポート
Windows Phone Tools for Mango のリリース候補版で NuGet がサポートされるようになりました。
現時点では、Windows Phone ツールは Visual Studio 拡張機能マネージャーをサポートしていないため、Windows Phone ツール用の NuGet をインストールするには、VSIX を手動でダウンロードして実行する必要がある場合があります。

Windows Phone ツールの NuGet をアンインストールするには、次のコマンドを実行します。

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a>バグの修正
NuGet 1.4 では、合計88個の作業項目が修正済みです。 これらの71はバグとしてマークされています。

NuGet 1.4 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を参照してください。

## <a name="bug-fixes-worth-noting"></a>バグ修正:

* [問題 603](http://nuget.codeplex.com/workitem/603): 特定のパッケージソースを指定すると、異なるリポジトリ間のパッケージの依存関係が正しく解決されます。
* [問題 1036](http://nuget.codeplex.com/workitem/1036): `NuGet Pack SomeProject.csproj` ビルド後イベントへの追加で、無限ループが発生しなくなりました。
* [Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` フラグは相対パスをサポートしています。

## <a name="nuget-14-update"></a>NuGet 1.4 更新プログラム
NuGet 1.4 のリリース直後、修正が必要ないくつかの問題が見つかりました。
この更新プログラムの1.4 への特定のバージョン番号は1.4.20615.9020 です。

### <a name="bug-fixes"></a>バグの修正
* [問題 1220](http://nuget.codeplex.com/workitem/1220): 複数の `install.ps1` / `uninstall.ps1` プロジェクトがある場合、すべてのプロジェクトで Update-Package が実行されない
* [問題 1156](http://nuget.codeplex.com/workitem/1156): パッケージマネージャー consol が W2K3/XP でスタックしている (Powershell 2 がインストールされていない場合)
