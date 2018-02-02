---
title: "NuGet.Server を使用して NuGet フィードをホストする | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "HTTP および OData 経由でパッケージを利用できるようにして、NuGet.Server を使用し、IIS を実行している任意のサーバー上に NuGet パッケージ フィードを作成およびホストする方法です。"
keywords: "NuGet フィード、NuGet ギャラリー、リモート パッケージ フィード、NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server は、.NET Foundation によって提供されるパッケージです。このパッケージでは、IIS を実行する任意のサーバー上でパッケージ フィードをホストできる、ASP.NET アプリケーションを作成します。 単純に言うと、NuGet.Server では HTTP (具体的には OData) 経由で利用できるサーバーにフォルダーを作成します。 設定は簡単で、単純なシナリオに最適です。

1. Visual Studio で空の ASP.NET Web アプリケーションを作成して、NuGet.Server パッケージを追加します。
1. アプリケーションで `Packages` フォルダーを設定し、パッケージを追加します。
1. アプリケーションを適切なサーバーに展開します。

次のセクションでは、C# を使用して、このプロセスを詳しく確認します。

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>NuGet.Server を使用して ASP.NET Web アプリケーションを作成して配置する

1. Visual Studio では、**[ファイル] > [新規] > [プロジェクト]** を選択して、.NET Framework 4.6 のターゲット フレームワークを設定し (以下を参照)、"ASP.NET" を検索して、C# に **[ASP.NET Web アプリケーション (.NET Framework)]** テンプレートを選択します。

    ![.NET Framework ターゲットを 4.6 に設定する](media/Hosting_01-NuGet.Server-Set4.6.png)

1. アプリケーションに NuGet.Server *以外*の適切な名前を付けて、[OK] を選択し、次のダイアログで**空の**テンプレートを選択して [OK] を選択します。

1. プロジェクトを右クリックして、**[NuGet パッケージの管理]** を選択し、.NET Framework 4.6 を対象にしている場合、パッケージ マネージャー UI で、最新バージョンの NuGet.Server パッケージを検索してインストールします。 (また、`Install-Package NuGet.Server` を使用して、パッケージ マネージャー コンソールからインストールすることもできます。)

    ![NuGet.Server パッケージをインストールする](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > Web アプリケーションが .NET Framework 4.5.2 を対象にする場合、代わりに NuGet Server **2.10.3** をインストールする必要があります。

1. NuGet.Server をインストールすると、空の Web アプリケーションはパッケージ ソースに変換されます。 この操作を行うと、アプリケーション内に `Packages` フォルダーが作成され、追加の設定を含めるために `web.config` を上書きします (詳細については、ファイルのコメントを参照してください)。

1. アプリケーションをサーバーに公開するときに、パッケージをフィードで使用できるようにするには、Visual Studio の `Packages` フォルダーに `.nupkg` ファイルを追加して、**[ビルド アクション]** を **[コンテンツ]** に、**[出力ディレクトリにコピー]** を **[常にコピーする]** に設定します。

    ![プロジェクト内の [Packages] フォルダーにパッケージをコピーする](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. サイトを Visual Studio のローカルで実行します (デバッグを行わないので、Ctrl + F5 キーです)。 ホーム ページには、パッケージ フィードの URL が示されます。

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

NuGet.Server サイトが実行されていると、`web.config` で API キーの値を設定していれば、nuget.exe を使用して、パッケージを追加または削除できます。

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

サーバーが既にセキュリティで保護されているか、または、API キーが必要ない場合 (たとえば、ローカル チーム ネットワーク上でプライベート サーバーを使用している場合)、`requireApiKey` を `false` に設定できます。 その後、サーバーへのアクセス権を持つすべてのユーザーが、パッケージをプッシュまたは削除できます。