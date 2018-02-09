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
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a><span data-ttu-id="94a16-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="94a16-104">NuGet.Server</span></span>

<span data-ttu-id="94a16-105">NuGet.Server は、.NET Foundation によって提供されるパッケージです。このパッケージでは、IIS を実行する任意のサーバー上でパッケージ フィードをホストできる、ASP.NET アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="94a16-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="94a16-106">単純に言うと、NuGet.Server では HTTP (具体的には OData) 経由で利用できるサーバーにフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="94a16-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="94a16-107">設定は簡単で、単純なシナリオに最適です。</span><span class="sxs-lookup"><span data-stu-id="94a16-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="94a16-108">Visual Studio で空の ASP.NET Web アプリケーションを作成して、NuGet.Server パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="94a16-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="94a16-109">アプリケーションで `Packages` フォルダーを設定し、パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="94a16-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="94a16-110">アプリケーションを適切なサーバーに展開します。</span><span class="sxs-lookup"><span data-stu-id="94a16-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="94a16-111">次のセクションでは、C# を使用して、このプロセスを詳しく確認します。</span><span class="sxs-lookup"><span data-stu-id="94a16-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="94a16-112">NuGet.Server を使用して ASP.NET Web アプリケーションを作成して配置する</span><span class="sxs-lookup"><span data-stu-id="94a16-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="94a16-113">Visual Studio では、**[ファイル] > [新規] > [プロジェクト]** を選択して、.NET Framework 4.6 のターゲット フレームワークを設定し (以下を参照)、"ASP.NET" を検索して、C# に **[ASP.NET Web アプリケーション (.NET Framework)]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="94a16-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![.NET Framework ターゲットを 4.6 に設定する](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="94a16-115">アプリケーションに NuGet.Server *以外*の適切な名前を付けて、[OK] を選択し、次のダイアログで**空の**テンプレートを選択して [OK] を選択します。</span><span class="sxs-lookup"><span data-stu-id="94a16-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="94a16-116">プロジェクトを右クリックして、**[NuGet パッケージの管理]** を選択し、.NET Framework 4.6 を対象にしている場合、パッケージ マネージャー UI で、最新バージョンの NuGet.Server パッケージを検索してインストールします。</span><span class="sxs-lookup"><span data-stu-id="94a16-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="94a16-117">(また、`Install-Package NuGet.Server` を使用して、パッケージ マネージャー コンソールからインストールすることもできます。)</span><span class="sxs-lookup"><span data-stu-id="94a16-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![NuGet.Server パッケージをインストールする](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="94a16-119">Web アプリケーションが .NET Framework 4.5.2 を対象にする場合、代わりに NuGet Server **2.10.3** をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="94a16-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="94a16-120">NuGet.Server をインストールすると、空の Web アプリケーションはパッケージ ソースに変換されます。</span><span class="sxs-lookup"><span data-stu-id="94a16-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="94a16-121">この操作を行うと、アプリケーション内に `Packages` フォルダーが作成され、追加の設定を含めるために `web.config` を上書きします (詳細については、ファイルのコメントを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="94a16-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="94a16-122">アプリケーションをサーバーに公開するときに、パッケージをフィードで使用できるようにするには、Visual Studio の `Packages` フォルダーに `.nupkg` ファイルを追加して、**[ビルド アクション]** を **[コンテンツ]** に、**[出力ディレクトリにコピー]** を **[常にコピーする]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="94a16-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![プロジェクト内の [Packages] フォルダーにパッケージをコピーする](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="94a16-124">サイトを Visual Studio のローカルで実行します (デバッグを行わないので、Ctrl + F5 キーです)。</span><span class="sxs-lookup"><span data-stu-id="94a16-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="94a16-125">ホーム ページには、パッケージ フィードの URL が示されます。</span><span class="sxs-lookup"><span data-stu-id="94a16-125">The home page provides the package feed URLs:</span></span>

    ![NuGet.Server を使用したアプリケーションの既定のホーム ページ](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="94a16-127">パッケージの OData フィードを表示するには、上記の囲まれた領域内にある **[ここ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="94a16-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="94a16-128">初めてアプリケーションを実行すると、NuGet.Server では各パッケージにフォルダーが含まれるように、`Packages` フォルダーが再構築されます。</span><span class="sxs-lookup"><span data-stu-id="94a16-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="94a16-129">これは、パフォーマンスを向上させるために、NuGet 3.3 で導入された[ローカル記憶域のレイアウト](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)に一致します。</span><span class="sxs-lookup"><span data-stu-id="94a16-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="94a16-130">さらにパッケージを追加する場合、継続してこの構造に従います。</span><span class="sxs-lookup"><span data-stu-id="94a16-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="94a16-131">ローカルの配置をテストしたら、必要に応じてアプリケーションをその他の内部または外部のサイトに展開します。</span><span class="sxs-lookup"><span data-stu-id="94a16-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="94a16-132">`http://<domain>` に展開されると、パッケージ ソースに使用する URL は `http://<domain>/nuget` になります。</span><span class="sxs-lookup"><span data-stu-id="94a16-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="94a16-133">パッケージ フォルダーを構成する</span><span class="sxs-lookup"><span data-stu-id="94a16-133">Configuring the Packages folder</span></span>

<span data-ttu-id="94a16-134">`NuGet.Server` 1.5 以降を使用して、`web.config` 内の `appSetting/packagesPath` 値を使用して、パッケージ フォルダーをより具体的に構成できます。</span><span class="sxs-lookup"><span data-stu-id="94a16-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="94a16-135">`packagesPath` は絶対パスまたは仮想パスにすることができます。</span><span class="sxs-lookup"><span data-stu-id="94a16-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="94a16-136">`packagesPath` が省略された場合、または空白のままの場合は、パッケージ フォルダーは既定の `~/Packages` です。</span><span class="sxs-lookup"><span data-stu-id="94a16-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="94a16-137">パッケージを外部からフィードに追加する</span><span class="sxs-lookup"><span data-stu-id="94a16-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="94a16-138">NuGet.Server サイトが実行されていると、`web.config` で API キーの値を設定していれば、nuget.exe を使用して、パッケージを追加または削除できます。</span><span class="sxs-lookup"><span data-stu-id="94a16-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="94a16-139">NuGet.Server パッケージをインストールした後、`web.config` に空の `appSetting/apiKey` 値が含まれます。</span><span class="sxs-lookup"><span data-stu-id="94a16-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="94a16-140">`apiKey` が省略された場合、または空白の場合は、パッケージのフィードへのプッシュは無効になります。</span><span class="sxs-lookup"><span data-stu-id="94a16-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="94a16-141">この機能を有効にするには、`apiKey` に値 (理想的には、強力なパスワード) を設定し、`true` の値を含む `appSettings/requireApiKey` と呼ばれるキーを追加します。</span><span class="sxs-lookup"><span data-stu-id="94a16-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="94a16-142">サーバーが既にセキュリティで保護されているか、または、API キーが必要ない場合 (たとえば、ローカル チーム ネットワーク上でプライベート サーバーを使用している場合)、`requireApiKey` を `false` に設定できます。</span><span class="sxs-lookup"><span data-stu-id="94a16-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="94a16-143">その後、サーバーへのアクセス権を持つすべてのユーザーが、パッケージをプッシュまたは削除できます。</span><span class="sxs-lookup"><span data-stu-id="94a16-143">All users with access to the server can then push or delete packages.</span></span>