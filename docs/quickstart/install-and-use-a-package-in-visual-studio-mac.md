---
title: Visual Studio for Mac に NuGet パッケージをインストールして使用する
description: Visual Studio for Mac プロジェクトに NuGet パッケージをインストールして使用するプロセスを説明したチュートリアル。
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238478"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="be69e-103">クイック スタート: Visual Studio for Mac にパッケージをインストールして使用する</span><span class="sxs-lookup"><span data-stu-id="be69e-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="be69e-104">NuGet パッケージには、他の開発者がお客様のプロジェクトで使用できるようにした、再利用可能なコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="be69e-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="be69e-105">背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="be69e-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="be69e-106">パッケージは、NuGet パッケージ マネージャーを使って Visual Studio for Mac プロジェクトにインストールします。</span><span class="sxs-lookup"><span data-stu-id="be69e-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="be69e-107">この記事では、人気のある [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージと .NET Core コンソール プロジェクトを使ってそのプロセスを説明します。</span><span class="sxs-lookup"><span data-stu-id="be69e-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="be69e-108">他の任意の Xamarin または .NET Core プロジェクトにも同じプロセスを適用できます。</span><span class="sxs-lookup"><span data-stu-id="be69e-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="be69e-109">インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。</span><span class="sxs-lookup"><span data-stu-id="be69e-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="be69e-110">参照が行われたら、その API からパッケージを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="be69e-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="be69e-111">**nuget.org を開始する**:*nuget.org* を参照するのは、.NET 開発者が自身のアプリケーションで再利用可能なコンポーネントを検索するための一般的な方法です。</span><span class="sxs-lookup"><span data-stu-id="be69e-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="be69e-112">*nuget.org* を直接検索するか、この記事に示すように、パッケージを検索して Visual Studio 内にインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="be69e-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="be69e-113">一般的な情報については、[NuGet パッケージの検索と評価](../consume-packages/finding-and-choosing-packages.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="be69e-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be69e-114">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="be69e-114">Prerequisites</span></span>

- <span data-ttu-id="be69e-115">Visual Studio 2019 for Mac。</span><span class="sxs-lookup"><span data-stu-id="be69e-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="be69e-116">[visualstudio.com](https://www.visualstudio.com/) から無料の 2019 Community Edition をインストールするか、Professional または Enterprise Edition を使用できます。</span><span class="sxs-lookup"><span data-stu-id="be69e-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="be69e-117">Windows 上の Visual Studio を使用している場合は、[Visual Studio でのパッケージのインストールと使用 (Windows のみ)](install-and-use-a-package-in-visual-studio.md) に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="be69e-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="be69e-118">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="be69e-118">Create a project</span></span>

<span data-ttu-id="be69e-119">NuGet パッケージは任意の .NET プロジェクトにインストールできます。ただし、パッケージが同じターゲット フレームワークをプロジェクトとしてサポートしていることが条件です。</span><span class="sxs-lookup"><span data-stu-id="be69e-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="be69e-120">このチュートリアルでは、シンプルな .NET Core コンソール アプリを使用します。</span><span class="sxs-lookup"><span data-stu-id="be69e-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="be69e-121">Visual Studio for Mac で、 **[ファイル] > [新しいソリューション...]** を使用し、 **[.NET Core] > [アプリ] > [コンソールアプリケーション]** テンプレートを選択して、プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="be69e-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="be69e-122">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="be69e-122">Click **Next**.</span></span> <span data-ttu-id="be69e-123">プロンプトが表示されたら、 **[ターゲット フレームワーク]** の既定値をそのまま受け入れます。</span><span class="sxs-lookup"><span data-stu-id="be69e-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="be69e-124">Visual Studio によってプロジェクトが作成され、ソリューション エクスプローラーに開かれます。</span><span class="sxs-lookup"><span data-stu-id="be69e-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="be69e-125">Newtonsoft.Json NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="be69e-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="be69e-126">パッケージをインストールするには、NuGet パッケージ マネージャーを使用します。</span><span class="sxs-lookup"><span data-stu-id="be69e-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="be69e-127">パッケージをインストールすると、NuGet によって、プロジェクト ファイルまたは `packages.config` ファイルのどちらか (プロジェクトの形式によって異なります) に依存関係が記録されます。</span><span class="sxs-lookup"><span data-stu-id="be69e-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="be69e-128">詳細については、「[パッケージ利用のワークフロー](../consume-packages/Overview-and-Workflow.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="be69e-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="be69e-129">NuGet パッケージ マネージャー</span><span class="sxs-lookup"><span data-stu-id="be69e-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="be69e-130">ソリューション エクスプローラーで、 **[依存関係]** を右クリックして、 **[パッケージの追加...]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="be69e-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![プロジェクト参照の NuGet パッケージ管理コマンド](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="be69e-132">ダイアログの左上隅で **[パッケージ ソース]** として "nuget.org" を選択し、「**Newtonsoft.Json**」を検索します。一覧からそのパッケージを選択して **[パッケージの追加...]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="be69e-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="be69e-134">NuGet パッケージ マネージャーに関する詳細が必要な場合は、[Visual Studio for Mac を使用したパッケージのインストールおよび管理](../consume-packages/install-use-packages-visual-studio.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="be69e-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="be69e-135">アプリで Newtonsoft.Json API を使用する</span><span class="sxs-lookup"><span data-stu-id="be69e-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="be69e-136">プロジェクトに Newtonsoft.Json パッケージがある場合、その `JsonConvert.SerializeObject` メソッドを呼び出し、オブジェクトを人間が読める文字列に変換できます。</span><span class="sxs-lookup"><span data-stu-id="be69e-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="be69e-137">`Program.cs` ファイルを開き (Solution Pad にあります)、ファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="be69e-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="be69e-138">**[実行] > [デバッグの開始]** を選択して、アプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="be69e-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="be69e-139">アプリを実行すると、コンソールにシリアル化された JSON 出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="be69e-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![コンソール アプリの出力](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="be69e-141">次の手順</span><span class="sxs-lookup"><span data-stu-id="be69e-141">Next steps</span></span>
<span data-ttu-id="be69e-142">無事に、最初の NuGet パッケージをインストールして使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="be69e-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="be69e-143">Visual Studio for Mac を使用してパッケージをインストールして管理する</span><span class="sxs-lookup"><span data-stu-id="be69e-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="be69e-144">NuGet による提供についてさらに詳しく調べるには、下のリンクを選択してください。</span><span class="sxs-lookup"><span data-stu-id="be69e-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="be69e-145">パッケージ使用の概要とワークフロー</span><span class="sxs-lookup"><span data-stu-id="be69e-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="be69e-146">プロジェクト ファイルのパッケージ参照</span><span class="sxs-lookup"><span data-stu-id="be69e-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
