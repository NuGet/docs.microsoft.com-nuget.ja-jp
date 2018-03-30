---
title: NuGet.Server を使用して NuGet フィードをホストする | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: HTTP および OData 経由でパッケージを利用できるようにして、NuGet.Server を使用し、IIS を実行している任意のサーバー上に NuGet パッケージ フィードを作成およびホストする方法です。
keywords: NuGet フィード、NuGet ギャラリー、リモート パッケージ フィード、NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a8996fed537e5745a1dbeb1c3d12b2a0670e744d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server は、.NET Foundation によって提供されるパッケージです。このパッケージでは、IIS を実行する任意のサーバー上でパッケージ フィードをホストできる、ASP.NET アプリケーションを作成します。 単純に言うと、NuGet.Server では HTTP (具体的には OData) 経由で利用できるサーバーにフォルダーを作成します。 設定は簡単で、単純なシナリオに最適です。

1. Visual Studio で空の ASP.NET Web アプリケーションを作成して、NuGet.Server パッケージを追加します。
1. アプリケーションで `Packages` フォルダーを設定し、パッケージを追加します。
1. アプリケーションを適切なサーバーに展開します。

次のセクションでは、C# を使用して、このプロセスを詳しく確認します。

NuGet.Server についてさらに質問がある場合は、[https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) で問題を作成してください。

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>NuGet.Server を使用して ASP.NET Web アプリケーションを作成して配置する

1. Visual Studio で、**[ファイル] > [新規] > [プロジェクト]** を選択し、「ASP.NET」を検索し、C# 用に **[ASP.NET Web アプリケーション (.NET Framework)]** テンプレートを選択し、**[フレームワーク]** を [.NET Framework 4.6] に設定します。

    ![新しいプロジェクトのターゲット フレームワークを設定する](media/Hosting_01-NuGet.Server-Set4.6.png)

1. アプリケーションに NuGet.Server *以外*の適切な名前を付けて [OK] を選択し、次のダイアログで**空**のテンプレートを選択して **[OK]** を選択します。

1. プロジェクトを右クリックし、**[NuGet パッケージの管理]** を選択します。

1. .NET Framework 4.6 を対象にしている場合は、パッケージ マネージャー UI で **[参照]** タブを選択し、最新バージョンの NuGet.Server パッケージを検索してインストールします (また、`Install-Package NuGet.Server` を使用して、パッケージ マネージャー コンソールからインストールすることもできます。)メッセージに従って、ライセンス条項に同意します。

    ![NuGet.Server パッケージをインストールする](media/Hosting_02-NuGet.Server-Package.png)

1. NuGet.Server をインストールすると、空の Web アプリケーションはパッケージ ソースに変換されます。 この操作を行うと、他の多様なパッケージがインストールされ、アプリケーション内に `Packages` フォルダーが作成され、追加の設定を含めるために `web.config` が変更されます (詳細については、ファイルのコメントを参照してください)。

    > [!Important]
    > NuGet.Server パッケージでファイルの変更が完了した後は、`web.config` をよく確認してください。 NuGet.Server で既存の要素を上書きすることはできません。代わりに重複する要素が作成されます。 このような重複があると、後でプロジェクトを実行しようとしたときに "内部サーバー エラー" が発生します。 たとえば、NuGet.Server をインストールする前に `web.config` に `<compilation debug="true" targetFramework="4.5.2" />` を含めると、パッケージによって上書きされませんが 2 つ目の `<compilation debug="true" targetFramework="4.6" />` が挿入されます。 この場合は、以前の Framework バージョンの要素を削除してください。

1. アプリケーションをサーバーに公開するときに、パッケージをフィードで使用できるようにするには、Visual Studio の `Packages` フォルダーに各 `.nupkg` ファイルを追加して、それぞれの **[ビルド アクション]** を **[コンテンツ]** に、**[出力ディレクトリにコピー]** を **[常にコピーする]** に設定します。

    ![プロジェクト内の [Packages] フォルダーにパッケージをコピーする](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Visual Studio のローカルでサイトを実行します (**[デバッグ] > [デバッグなしで開始]** を使用するか Ctrl キーを押しながら F5 キーを押します)。 ホーム ページには、パッケージ フィードの URL が次のように表示されます。 エラーが表示される場合は、手順 5 で説明したような重複する要素がないか `web.config` をよく確認します。

    ![NuGet.Server を使用したアプリケーションの既定のホーム ページ](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. パッケージの OData フィードを表示するには、上記の囲まれた領域内にある **[ここ]** をクリックします。

1. 初めてアプリケーションを実行すると、NuGet.Server では各パッケージにフォルダーが含まれるように、`Packages` フォルダーが再構築されます。 これは、パフォーマンスを向上させるために、NuGet 3.3 で導入された[ローカル記憶域のレイアウト](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)に一致します。 さらにパッケージを追加する場合、継続してこの構造に従います。

1. ローカルの配置をテストしたら、必要に応じてアプリケーションをその他の内部または外部のサイトに展開します。

1. `http://<domain>` に展開されると、パッケージ ソースに使用する URL は `http://<domain>/nuget` になります。

## <a name="configuring-the-packages-folder"></a>パッケージ フォルダーを構成する

`NuGet.Server` 1.5 以降を使用して、`web.config` 内の `appSetting/packagesPath` 値を使用して、パッケージ フォルダーをより具体的に構成できます。

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` は絶対パスまたは仮想パスにすることができます。

`packagesPath` が省略された場合、または空白のままの場合は、パッケージ フォルダーは既定の `~/Packages` です。

## <a name="adding-packages-to-the-feed-externally"></a>パッケージを外部からフィードに追加する

`web.config` で API キーの値を設定した場合、NuGet.Server サイトが実行されているときに、[nuget push](../tools/cli-ref-push.md) を使用してパッケージを追加できます。

NuGet.Server パッケージをインストールした後、`web.config` に空の `appSetting/apiKey` 値が含まれます。

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

`apiKey` が省略された場合、または空白の場合は、パッケージのフィードへのプッシュは無効になります。

この機能を有効にするには、`apiKey` に値 (理想的には、強力なパスワード) を設定し、`true` の値を含む `appSettings/requireApiKey` と呼ばれるキーを追加します。

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

サーバーが既にセキュリティで保護されているか、または、API キーが必要ない場合 (たとえば、ローカル チーム ネットワーク上でプライベート サーバーを使用している場合)、`requireApiKey` を `false` に設定できます。 これで、サーバーへのアクセス権を持つすべてのユーザーは、パッケージをプッシュできるようになります。

## <a name="removing-packages-from-the-feed"></a>フィードからパッケージを削除する

NuGet.Server で、API キーをコメントに追加して [nuget delete](../tools/cli-ref-delete.md) コマンドを実行すると、リポジトリからパッケージを削除できます。

代わりにパッケージをリストから削除する (パッケージの復元のために使用できる状態のままにする) ように動作を変更する場合は、`web.config` の `enableDelisting` キーを true に変更します。

## <a name="nugetserver-support"></a>NuGet.Server のサポート

NuGet.Server の使用についてその他のサポートが必要な場合は、[https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) で問題を作成してください。