---
title: "NuGet パッケージ使用の入門ガイド | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "プロジェクトで NuGet パッケージをインストールし、使用するプロセスを説明するチュートリアル。"
keywords: "NuGet をインストールする, NuGet パッケージの使用, NuGet パッケージをインストールする, NuGet パッケージ参照, NuGet パッケージを使用する"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bcccc7139de31a8d07e9ed52abfd12fe9e6d687b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="bb1a8-104">パッケージをインストールして使用する</span><span class="sxs-lookup"><span data-stu-id="bb1a8-104">Install and use a package</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="bb1a8-105">インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-105">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="bb1a8-106">参照が行われたら、その API からパッケージを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-106">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="bb1a8-107">このトピックの残りでは、Package Manager UI を使用し、ユニバーサル Windows プラットフォーム (UWP) プロジェクトで人気の [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージをインストールする方法を段階的に説明します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-107">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="bb1a8-108">その後、パッケージの使用例を紹介します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-108">It then shows an example of using the package.</span></span> <span data-ttu-id="bb1a8-109">プロジェクトで使用するほとんどすべての NuGet パッケージで同様のワークフローを使用します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-109">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="bb1a8-110">前提条件をインストールする</span><span class="sxs-lookup"><span data-stu-id="bb1a8-110">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="bb1a8-111">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="bb1a8-111">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="bb1a8-112">Newtonsoft.Json NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="bb1a8-112">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="bb1a8-113">アプリで Newtonsoft.Json API を使用する</span><span class="sxs-lookup"><span data-stu-id="bb1a8-113">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="bb1a8-114">**nuget.org を始める**: nuget.org からのパッケージのインストールは、自分のアプリケーションで再利用できるコンポーネントを .NET 開発者が見つけるための一般的ワークフローです。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-114">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="bb1a8-115">このトピックで紹介するように、いつでも nuget.org を直接、検索したり、Visual Studio 内でパッケージを見つけ、インストールしたりできます。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-115">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="bb1a8-116">前提条件をインストールする</span><span class="sxs-lookup"><span data-stu-id="bb1a8-116">Install pre-requisites</span></span>

<span data-ttu-id="bb1a8-117">このチュートリアルには、Visual Studio 2015 Update 3 とユニバーサル Windows アプリ用ツール、または Visual Studio 2017 とユニバーサル Windows プラットフォーム開発ワークロードが必要です。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-117">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="bb1a8-118">Visual Studio を既にインストールしている場合、インストーラーをもう一度実行し、UWP ツールを追加できます。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-118">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="bb1a8-119">[visualstudio.com](https://www.visualstudio.com/) から無料の Community Edition をインストールします。Professional Edition と Enterprise Edition も使用できます。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-119">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="bb1a8-120">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="bb1a8-120">Create a project</span></span>

<span data-ttu-id="bb1a8-121">NuGet パッケージをインストールするには、Visual Studio で何らかの .NET ベースのプロジェクトが必要です。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-121">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="bb1a8-122">このチュートリアルでは、単純な Windows Presentation Foundation (WPF) またはユニバーサル Windows (UWP) アプリを使用できます。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-122">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="bb1a8-123">WPF (Windows 7+) の場合、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、**[Visual C#]** を展開し、**[Windows クラシック デスクトップ]、[WPF アプリ (.NET フレームワーク)]**、**[OK]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-123">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="bb1a8-124">UWP (Windows 10) の場合、**[Windows ユニバーサル]、[空のアプリ (ユニバーサル Windows)]** を代わりに使用します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-124">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="bb1a8-125">プロンプトが表示されたら、ターゲット バージョンと最小バージョンの既定値を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-125">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="bb1a8-126">Newtonsoft.Json NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="bb1a8-126">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="bb1a8-127">ソリューション エクスプローラーで **[参照]** を右クリックし、**[NuGet パッケージの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-127">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![プロジェクト参照の NuGet パッケージ管理コマンド](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="bb1a8-129">**[パッケージ ソース]** として "nuget.org" を選択し、**[参照]** タブを選択し、「**Newtonsoft.Json**」を検索し、一覧からそのパッケージを選択し、**[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-129">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="bb1a8-131">パッケージ管理形式を選択するように求められた場合、PackageReference (推奨) または `packages.config` を選択します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-131">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![パッケージ参照形式を選択する](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="bb1a8-133">変更の確認を求められた場合、**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-133">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="bb1a8-134">ソリューション エクスプローラーを右クリックし、**[ソリューションのビルド]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-134">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="bb1a8-135">これで NuGet パッケージが復元され、**[参照]** の下の一覧に表示されます。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-135">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="bb1a8-136">詳細については、「[パッケージの復元](../consume-packages/package-restore.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-136">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="bb1a8-137">アプリで Newtonsoft.Json API を使用する</span><span class="sxs-lookup"><span data-stu-id="bb1a8-137">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="bb1a8-138">プロジェクトに Newtonsoft.Json パッケージがある場合、その `JsonConvert.SerializeObject` メソッドを呼び出し、オブジェクトを人間が読める文字列に変換できます。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-138">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="bb1a8-139">`MainWindow.xaml` (WPF) または `MainPage.xaml` (UWP) を開き、既存の `Grid` 要素を次のもので置換します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-139">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="bb1a8-140">ソリューション エクスプローラーで `MainWindow.xaml` (WPF) または `MainPage.xaml` (UWP) ノードを展開し、`.cs` ファイルを開き、`MainWindow` または `MainPage` クラス内でコンストラクターの後に次のコードを挿入します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-140">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. <span data-ttu-id="bb1a8-141">プロジェクトに Newtonsoft.Json パッケージを追加した後でも、`JsonConvert` の下に赤い波線が表示されます。これは `using` ステートメントが必要であるためです。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-141">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="bb1a8-142">下線の付いた `JsonConvert` にカーソルを合わせると電球と**考えられる修正内容を表示する**オプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-142">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![電球と考えられる修正内容を表示するコマンド](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="bb1a8-144">**[考えられる修正内容を表示する]** (電球) をクリックし、最初の修正案である `using Newtonsoft.Json;` を選択します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-144">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="bb1a8-145">これでファイルの一番上に必要な行が追加されます。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-145">This adds the necessary line to the top of the file.</span></span>

    ![using ステートメントを追加するオプションを表示する電球](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="bb1a8-147">アプリをビルドして実行します。F5 を押すか、**[デバッグ]、[デバッグの開始]** を選択してください。ここの例では UWP ですが、WPF の場合も同様です。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![UWP アプリの最初の出力](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="bb1a8-149">ボタンを選択し、TextBlock の内容が JSON テキストに置換されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="bb1a8-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![ボタンを選択した後の UWP アプリの出力](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="bb1a8-151">関連トピック</span><span class="sxs-lookup"><span data-stu-id="bb1a8-151">Related topics</span></span>

- [<span data-ttu-id="bb1a8-152">パッケージ使用の概要とワークフロー</span><span class="sxs-lookup"><span data-stu-id="bb1a8-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="bb1a8-153">パッケージの検索と選択</span><span class="sxs-lookup"><span data-stu-id="bb1a8-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="bb1a8-154">NuGet の動作を構成する</span><span class="sxs-lookup"><span data-stu-id="bb1a8-154">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
