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
ms.openlocfilehash: 639f4883f5ce904a44d8aa23d76c93ed79ea4b9d
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2018
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="192fe-104">パッケージをインストールして使用する</span><span class="sxs-lookup"><span data-stu-id="192fe-104">Install and use a package</span></span>

<span data-ttu-id="192fe-105">NuGet パッケージとは、自分のプロジェクトでの使用が他の開発者によって許可されている再利用可能なコードの単位です。</span><span class="sxs-lookup"><span data-stu-id="192fe-105">NuGet packages are units of reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="192fe-106">背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="192fe-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="192fe-107">インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。</span><span class="sxs-lookup"><span data-stu-id="192fe-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="192fe-108">参照が行われたら、その API からパッケージを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="192fe-108">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="192fe-109">このトピックの残りでは、Package Manager UI を使用し、ユニバーサル Windows プラットフォーム (UWP) プロジェクトで人気の [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージをインストールする方法を段階的に説明します。</span><span class="sxs-lookup"><span data-stu-id="192fe-109">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="192fe-110">その後、パッケージの使用例を紹介します。</span><span class="sxs-lookup"><span data-stu-id="192fe-110">It then shows an example of using the package.</span></span> <span data-ttu-id="192fe-111">プロジェクトで使用するほとんどすべての NuGet パッケージで同様のワークフローを使用します。</span><span class="sxs-lookup"><span data-stu-id="192fe-111">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="192fe-112">前提条件をインストールする</span><span class="sxs-lookup"><span data-stu-id="192fe-112">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="192fe-113">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="192fe-113">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="192fe-114">Newtonsoft.Json NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="192fe-114">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="192fe-115">アプリで Newtonsoft.Json API を使用する</span><span class="sxs-lookup"><span data-stu-id="192fe-115">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="192fe-116">**nuget.org を始める**: nuget.org からのパッケージのインストールは、自分のアプリケーションで再利用できるコンポーネントを .NET 開発者が見つけるための一般的ワークフローです。</span><span class="sxs-lookup"><span data-stu-id="192fe-116">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="192fe-117">このトピックで紹介するように、いつでも nuget.org を直接、検索したり、Visual Studio 内でパッケージを見つけ、インストールしたりできます。</span><span class="sxs-lookup"><span data-stu-id="192fe-117">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="192fe-118">前提条件をインストールする</span><span class="sxs-lookup"><span data-stu-id="192fe-118">Install pre-requisites</span></span>

<span data-ttu-id="192fe-119">このチュートリアルには、Visual Studio 2015 Update 3 とユニバーサル Windows アプリ用ツール、または Visual Studio 2017 とユニバーサル Windows プラットフォーム開発ワークロードが必要です。</span><span class="sxs-lookup"><span data-stu-id="192fe-119">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="192fe-120">Visual Studio を既にインストールしている場合、インストーラーをもう一度実行し、UWP ツールを追加できます。</span><span class="sxs-lookup"><span data-stu-id="192fe-120">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="192fe-121">[visualstudio.com](https://www.visualstudio.com/) から無料の Community Edition をインストールします。Professional Edition と Enterprise Edition も使用できます。</span><span class="sxs-lookup"><span data-stu-id="192fe-121">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="192fe-122">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="192fe-122">Create a project</span></span>

<span data-ttu-id="192fe-123">NuGet パッケージをインストールするには、Visual Studio で何らかの .NET ベースのプロジェクトが必要です。</span><span class="sxs-lookup"><span data-stu-id="192fe-123">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="192fe-124">このチュートリアルでは、単純な Windows Presentation Foundation (WPF) またはユニバーサル Windows (UWP) アプリを使用できます。</span><span class="sxs-lookup"><span data-stu-id="192fe-124">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="192fe-125">WPF (Windows 7+) の場合、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、**[Visual C#]** を展開し、**[Windows クラシック デスクトップ]、[WPF アプリ (.NET フレームワーク)]**、**[OK]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="192fe-125">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="192fe-126">UWP (Windows 10) の場合、**[Windows ユニバーサル]、[空のアプリ (ユニバーサル Windows)]** を代わりに使用します。</span><span class="sxs-lookup"><span data-stu-id="192fe-126">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="192fe-127">プロンプトが表示されたら、ターゲット バージョンと最小バージョンの既定値を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="192fe-127">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="192fe-128">Newtonsoft.Json NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="192fe-128">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="192fe-129">ソリューション エクスプローラーで **[参照]** を右クリックし、**[NuGet パッケージの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="192fe-129">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![プロジェクト参照の NuGet パッケージ管理コマンド](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="192fe-131">**[パッケージ ソース]** として "nuget.org" を選択し、**[参照]** タブを選択し、「**Newtonsoft.Json**」を検索し、一覧からそのパッケージを選択し、**[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="192fe-131">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="192fe-133">パッケージ管理形式を選択するように求められた場合、PackageReference (推奨) または `packages.config` を選択します。</span><span class="sxs-lookup"><span data-stu-id="192fe-133">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![パッケージ参照形式を選択する](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="192fe-135">変更の確認を求められた場合、**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="192fe-135">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="192fe-136">ソリューション エクスプローラーを右クリックし、**[ソリューションのビルド]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="192fe-136">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="192fe-137">これで NuGet パッケージが復元され、**[参照]** の下の一覧に表示されます。</span><span class="sxs-lookup"><span data-stu-id="192fe-137">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="192fe-138">詳細については、「[パッケージの復元](../consume-packages/package-restore.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="192fe-138">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="192fe-139">アプリで Newtonsoft.Json API を使用する</span><span class="sxs-lookup"><span data-stu-id="192fe-139">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="192fe-140">プロジェクトに Newtonsoft.Json パッケージがある場合、その `JsonConvert.SerializeObject` メソッドを呼び出し、オブジェクトを人間が読める文字列に変換できます。</span><span class="sxs-lookup"><span data-stu-id="192fe-140">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="192fe-141">`MainWindow.xaml` (WPF) または `MainPage.xaml` (UWP) を開き、既存の `Grid` 要素を次のもので置換します。</span><span class="sxs-lookup"><span data-stu-id="192fe-141">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="192fe-142">ソリューション エクスプローラーで `MainWindow.xaml` (WPF) または `MainPage.xaml` (UWP) ノードを展開し、`.cs` ファイルを開き、`MainWindow` または `MainPage` クラス内でコンストラクターの後に次のコードを挿入します。</span><span class="sxs-lookup"><span data-stu-id="192fe-142">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="192fe-143">プロジェクトに Newtonsoft.Json パッケージを追加した後でも、`JsonConvert` の下に赤い波線が表示されます。これは `using` ステートメントが必要であるためです。</span><span class="sxs-lookup"><span data-stu-id="192fe-143">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="192fe-144">下線の付いた `JsonConvert` にカーソルを合わせると電球と**考えられる修正内容を表示する**オプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="192fe-144">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![電球と考えられる修正内容を表示するコマンド](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="192fe-146">**[考えられる修正内容を表示する]** (電球) をクリックし、最初の修正案である `using Newtonsoft.Json;` を選択します。</span><span class="sxs-lookup"><span data-stu-id="192fe-146">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="192fe-147">これでファイルの一番上に必要な行が追加されます。</span><span class="sxs-lookup"><span data-stu-id="192fe-147">This adds the necessary line to the top of the file.</span></span>

    ![using ステートメントを追加するオプションを表示する電球](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="192fe-149">アプリをビルドして実行します。F5 を押すか、**[デバッグ]、[デバッグの開始]** を選択してください。ここの例では UWP ですが、WPF の場合も同様です。</span><span class="sxs-lookup"><span data-stu-id="192fe-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![UWP アプリの最初の出力](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="192fe-151">ボタンを選択し、TextBlock の内容が JSON テキストに置換されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="192fe-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![ボタンを選択した後の UWP アプリの出力](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="192fe-153">関連トピック</span><span class="sxs-lookup"><span data-stu-id="192fe-153">Related topics</span></span>

- [<span data-ttu-id="192fe-154">パッケージ使用の概要とワークフロー</span><span class="sxs-lookup"><span data-stu-id="192fe-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="192fe-155">パッケージの検索と選択</span><span class="sxs-lookup"><span data-stu-id="192fe-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="192fe-156">NuGet の動作を構成する</span><span class="sxs-lookup"><span data-stu-id="192fe-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
