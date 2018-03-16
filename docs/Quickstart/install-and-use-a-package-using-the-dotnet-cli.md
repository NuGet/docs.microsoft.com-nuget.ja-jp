---
title: "dotnet CLI を使って NuGet パッケージを使用するための入門ガイド | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: ".NET Core プロジェクトで NuGet パッケージをインストールし、使用するプロセスを説明したチュートリアル。"
keywords: "NuGet をインストールする, NuGet パッケージの使用, NuGet パッケージをインストールする, NuGet パッケージ参照, NuGet パッケージを使用する"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: accc6d7bb5abff43ffaa083fa55c13cd5b10ce10
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="cf1c9-104">dotnet CLI を使用してパッケージをインストールし使用する</span><span class="sxs-lookup"><span data-stu-id="cf1c9-104">Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="cf1c9-105">NuGet パッケージには、他の開発者がお客様のプロジェクトで使用できるようにした、再利用可能なコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="cf1c9-106">背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="cf1c9-107">一般的な [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージに関するこの記事で説明するとおり、パッケージを .NET Core プロジェクトにインストールするには、`dotnet add package` コマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-107">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="cf1c9-108">インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="cf1c9-109">参照が行われたら、その API からパッケージを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="cf1c9-110">**nuget.org を開始する**: nuget.org を参照するのは、.NET 開発者が自身のアプリケーションで再利用可能なコンポーネントを検索するための一般的な方法です。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="cf1c9-111">この記事で説明するように、nuget.org を直接検索することも、Visual Studio 内でパッケージを見つけてインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf1c9-112">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="cf1c9-112">Prerequisites</span></span>

- <span data-ttu-id="cf1c9-113">[.NET Core SDK](https://www.microsoft.com/net/download/)。これは、`dotnet`コマンド ライン ツールを提供します。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-113">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="cf1c9-114">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="cf1c9-114">Create a project</span></span>

<span data-ttu-id="cf1c9-115">NuGet パッケージは、ある種類の .NET プロジェクトにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="cf1c9-116">このチュートリアルでは、次の手順に従って、単純な .NET Core コンソール プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="cf1c9-117">プロジェクトのフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="cf1c9-118">次のコマンドを使用して、プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="cf1c9-119">`dotnet run` を使用して、アプリが正しく作成されたことをテストします。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="cf1c9-120">Newtonsoft.Json NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="cf1c9-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="cf1c9-121">次のコマンドを使用して、`Newtonsoft.json` パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. <span data-ttu-id="cf1c9-122">コマンドが完了したら、`.csproj` ファイルを開いて、追加された参照を確認します。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
  </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="cf1c9-123">アプリで Newtonsoft.Json API を使用する</span><span class="sxs-lookup"><span data-stu-id="cf1c9-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="cf1c9-124">`Program.cs`ファイルを開いて、ファイルの上部に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="cf1c9-125">`class Program` 行の前に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="cf1c9-126">`Main` 関数を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-126">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="cf1c9-127">`dotnet run` コマンドを使用して、アプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="cf1c9-128">出力は、コード内の `Account` オブジェクトの JSON 表現になります。</span><span class="sxs-lookup"><span data-stu-id="cf1c9-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="cf1c9-129">関連記事</span><span class="sxs-lookup"><span data-stu-id="cf1c9-129">Related articles</span></span>

- [<span data-ttu-id="cf1c9-130">パッケージ使用の概要とワークフロー</span><span class="sxs-lookup"><span data-stu-id="cf1c9-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="cf1c9-131">パッケージの検索と選択</span><span class="sxs-lookup"><span data-stu-id="cf1c9-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="cf1c9-132">パッケージをインストールする方法</span><span class="sxs-lookup"><span data-stu-id="cf1c9-132">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="cf1c9-133">NuGet の動作を構成する</span><span class="sxs-lookup"><span data-stu-id="cf1c9-133">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
