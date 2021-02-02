---
title: dotnet CLI を使用して NuGet パッケージをインストールし、使用する
description: .NET Core プロジェクトで NuGet パッケージをインストールし、使用するプロセスを説明したチュートリアル。
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: adbf8f457d8520e3087e539b91ef932877aec3a0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775451"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="e65ec-103">クイック スタート: dotnet CLI を使用してパッケージをインストールし使用する</span><span class="sxs-lookup"><span data-stu-id="e65ec-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="e65ec-104">NuGet パッケージには、他の開発者がお客様のプロジェクトで使用できるようにした、再利用可能なコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="e65ec-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="e65ec-105">背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e65ec-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="e65ec-106">一般的な [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージに関するこの記事で説明するとおり、パッケージを .NET Core プロジェクトにインストールするには、`dotnet add package` コマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="e65ec-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="e65ec-107">インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。</span><span class="sxs-lookup"><span data-stu-id="e65ec-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="e65ec-108">その後、パッケージの API を使用できます。</span><span class="sxs-lookup"><span data-stu-id="e65ec-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="e65ec-109">**nuget.org を開始する**: nuget.org を参照するのは、.NET 開発者が自身のアプリケーションで再利用可能なコンポーネントを検索するための一般的な方法です。</span><span class="sxs-lookup"><span data-stu-id="e65ec-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="e65ec-110">この記事で説明するように、nuget.org を直接検索することも、Visual Studio 内でパッケージを見つけてインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="e65ec-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e65ec-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="e65ec-111">Prerequisites</span></span>

- <span data-ttu-id="e65ec-112">[.NET Core SDK](https://www.microsoft.com/net/download/)。これは、`dotnet`コマンド ライン ツールを提供します。</span><span class="sxs-lookup"><span data-stu-id="e65ec-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="e65ec-113">Visual Studio 2017 以降、dotnet CLI は .NET Core 関連のワークロードで自動的にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="e65ec-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="e65ec-114">プロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="e65ec-114">Create a project</span></span>

<span data-ttu-id="e65ec-115">NuGet パッケージは、ある種類の .NET プロジェクトにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="e65ec-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="e65ec-116">このチュートリアルでは、次の手順に従って、単純な .NET Core コンソール プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="e65ec-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="e65ec-117">プロジェクトのフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="e65ec-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="e65ec-118">コマンド プロンプトを開いて、新しいフォルダーに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="e65ec-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="e65ec-119">次のコマンドを使用して、プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="e65ec-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="e65ec-120">`dotnet run` を使用して、アプリが正しく作成されたことをテストします。</span><span class="sxs-lookup"><span data-stu-id="e65ec-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="e65ec-121">Newtonsoft.Json NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="e65ec-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="e65ec-122">次のコマンドを使用して、`Newtonsoft.json` パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e65ec-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="e65ec-123">コマンドが完了したら、`.csproj` ファイルを開いて、追加された参照を確認します。</span><span class="sxs-lookup"><span data-stu-id="e65ec-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="e65ec-124">アプリで Newtonsoft.Json API を使用する</span><span class="sxs-lookup"><span data-stu-id="e65ec-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="e65ec-125">`Program.cs`ファイルを開いて、ファイルの上部に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="e65ec-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="e65ec-126">`class Program` 行の前に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="e65ec-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="e65ec-127">`Main` 関数を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e65ec-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="e65ec-128">`dotnet run` コマンドを使用して、アプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="e65ec-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="e65ec-129">出力は、コード内の `Account` オブジェクトの JSON 表現になります。</span><span class="sxs-lookup"><span data-stu-id="e65ec-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="e65ec-130">関連ビデオ</span><span class="sxs-lookup"><span data-stu-id="e65ec-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="e65ec-131">他の NuGet ビデオは、[Channel 9](https://channel9.msdn.com/Series/NuGet-101) および [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) でご覧いただけます。</span><span class="sxs-lookup"><span data-stu-id="e65ec-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e65ec-132">次のステップ</span><span class="sxs-lookup"><span data-stu-id="e65ec-132">Next steps</span></span>

<span data-ttu-id="e65ec-133">無事に、最初の NuGet パッケージをインストールして使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e65ec-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e65ec-134">dotnet CLI を使用してパッケージをインストールし使用する</span><span class="sxs-lookup"><span data-stu-id="e65ec-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="e65ec-135">NuGet による提供についてさらに詳しく調べるには、下のリンクを選択してください。</span><span class="sxs-lookup"><span data-stu-id="e65ec-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="e65ec-136">パッケージ使用の概要とワークフロー</span><span class="sxs-lookup"><span data-stu-id="e65ec-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="e65ec-137">パッケージの検索と選択</span><span class="sxs-lookup"><span data-stu-id="e65ec-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="e65ec-138">プロジェクト ファイルのパッケージ参照</span><span class="sxs-lookup"><span data-stu-id="e65ec-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
