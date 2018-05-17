---
title: Visual Studio 内から NuGet パッケージを使用するための入門ガイド
description: Visual Studio プロジェクトで NuGet パッケージをインストールし、使用するプロセスを説明したチュートリアル。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: c61f8929d34bc9ff1a84ee186636543da5bcee63
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="965bb-103">クイック スタート: Visual Studio でパッケージをインストールして使用する</span><span class="sxs-lookup"><span data-stu-id="965bb-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="965bb-104">NuGet パッケージには、他の開発者がお客様のプロジェクトで使用できるようにした、再利用可能なコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="965bb-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="965bb-105">背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="965bb-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="965bb-106">Package Manager UI または Package Manager Console を使用して、パッケージが Visual Studio プロジェクトにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="965bb-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="965bb-107">この記事では、よく使用されている [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージとユニバーサル Windows プラットフォーム (UWP) プロジェクトを使用したプロセスを示します。</span><span class="sxs-lookup"><span data-stu-id="965bb-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="965bb-108">同じプロセスは、他の任意の .NET または .NET Core プロジェクトにも適用されます。</span><span class="sxs-lookup"><span data-stu-id="965bb-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="965bb-109">インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。</span><span class="sxs-lookup"><span data-stu-id="965bb-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="965bb-110">参照が行われたら、その API からパッケージを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="965bb-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="965bb-111">**nuget.org を開始する**: nuget.org を参照するのは、.NET 開発者が自身のアプリケーションで再利用可能なコンポーネントを検索するための一般的な方法です。</span><span class="sxs-lookup"><span data-stu-id="965bb-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="965bb-112">この記事で説明するように、nuget.org を直接検索することも、Visual Studio 内でパッケージを見つけてインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="965bb-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="965bb-113">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="965bb-113">Prerequisites</span></span>

- <span data-ttu-id="965bb-114">ユニバーサル Windows プラットフォーム開発ワークロードを含む Visual Studio 2017、または</span><span class="sxs-lookup"><span data-stu-id="965bb-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="965bb-115">ユニバーサル Windows アプリ用ツールを含む Visual Studio 2015 Update 3。</span><span class="sxs-lookup"><span data-stu-id="965bb-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="965bb-116">[visualstudio.com](https://www.visualstudio.com/) から無料の 2017 Community Edition をインストールできます。Professional Edition または Enterprise Edition を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="965bb-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="965bb-117">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="965bb-117">Create a project</span></span>

<span data-ttu-id="965bb-118">NuGet パッケージは任意の .NET プロジェクトにインストールできます。ただし、パッケージが同じターゲット フレームワークをプロジェクトとしてサポートしていることが条件です。</span><span class="sxs-lookup"><span data-stu-id="965bb-118">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="965bb-119">このチュートリアルでは、単純なユニバーサル Windows (UWP) アプリを使用します。</span><span class="sxs-lookup"><span data-stu-id="965bb-119">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="965bb-120">**[ファイル]、[新しいプロジェクト]** の順に使用し、**[Windows ユニバーサル]、[空白のアプリ (ユニバーサル Windows)]** の順に選択して、Visual Studio でプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="965bb-120">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="965bb-121">プロンプトが表示されたら、ターゲット バージョンと最小バージョンの既定値を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="965bb-121">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="965bb-122">Newtonsoft.Json NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="965bb-122">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="965bb-123">パッケージをインストールするには、パッケージ マネージャー UI またはパッケージ マネージャー コンソールのいずれかを使用できます。</span><span class="sxs-lookup"><span data-stu-id="965bb-123">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="965bb-124">パッケージをインストールすると、NuGet で依存関係がプロジェクト ファイルまたは `packages.config` ファイルに記録されます。</span><span class="sxs-lookup"><span data-stu-id="965bb-124">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="965bb-125">詳細については、「[パッケージ利用のワークフロー](../consume-packages/Overview-and-Workflow.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="965bb-125">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="965bb-126">パッケージ マネージャー UI</span><span class="sxs-lookup"><span data-stu-id="965bb-126">Package Manager UI</span></span>

1. <span data-ttu-id="965bb-127">ソリューション エクスプローラーで **[参照]** を右クリックし、**[NuGet パッケージの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="965bb-127">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![プロジェクト参照の NuGet パッケージ管理コマンド](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="965bb-129">**[パッケージ ソース]** として "nuget.org" を選択し、**[参照]** タブを選択し、「**Newtonsoft.Json**」を検索し、一覧からそのパッケージを選択し、**[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="965bb-129">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="965bb-131">ラインセンス プロンプトに同意します。</span><span class="sxs-lookup"><span data-stu-id="965bb-131">Accept any license prompts.</span></span>

1. <span data-ttu-id="965bb-132">(Visual Studio 2017) パッケージ管理形式を選択するように求められたら、**[プロジェクト ファイルの PackageReference]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="965bb-132">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![パッケージ管理形式の選択](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="965bb-134">変更の確認を求められた場合、**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="965bb-134">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="965bb-135">パッケージ マネージャー コンソール</span><span class="sxs-lookup"><span data-stu-id="965bb-135">Package Manager Console</span></span>

1. <span data-ttu-id="965bb-136">**[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー コンソール]** メニュー コマンドの順に選択します。</span><span class="sxs-lookup"><span data-stu-id="965bb-136">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="965bb-137">コンソールが開いたら、**[既定のプロジェクト]** ドロップダウン リストに、パッケージをインストールするプロジェクトが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="965bb-137">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="965bb-138">ソリューション内に単一のプロジェクトがあれば、それは既に選択されています。</span><span class="sxs-lookup"><span data-stu-id="965bb-138">If you have a single project in the solution, it is already selected.</span></span>

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="965bb-140">コマンド `Install-Package Newtonsoft.json` を入力します (「[Install-Package](../tools/ps-ref-install-package.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="965bb-140">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="965bb-141">コンソール ウィンドウに、このコマンドの出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="965bb-141">The console window shows output for the command.</span></span> <span data-ttu-id="965bb-142">通常、エラーは、パッケージがプロジェクトのターゲット フレームワークと互換性がないことを示します。</span><span class="sxs-lookup"><span data-stu-id="965bb-142">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="965bb-143">アプリで Newtonsoft.Json API を使用する</span><span class="sxs-lookup"><span data-stu-id="965bb-143">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="965bb-144">プロジェクトに Newtonsoft.Json パッケージがある場合、その `JsonConvert.SerializeObject` メソッドを呼び出し、オブジェクトを人間が読める文字列に変換できます。</span><span class="sxs-lookup"><span data-stu-id="965bb-144">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="965bb-145">`MainPage.xaml`を開いて、既存の `Grid` 要素を次の XAML に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="965bb-145">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="965bb-146">`MainPage.xaml.cs` ファイル (ソリューション エクスプローラーの `MainPage.xaml`ノードの下にあります) を開いて、`MainPage`コンストラクター内に次のコードを挿入します。</span><span class="sxs-lookup"><span data-stu-id="965bb-146">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="965bb-147">プロジェクトに Newtonsoft.Json パッケージを追加した後でも、`JsonConvert` の下に赤い波線が表示されます。これは、コード ファイルの上部に `using` ステートメントが必要であるためです。</span><span class="sxs-lookup"><span data-stu-id="965bb-147">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="965bb-148">アプリをビルドして実行します。F5 キーを押すか、**[デバッグ]、[デバッグの開始]** を選択してください。</span><span class="sxs-lookup"><span data-stu-id="965bb-148">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![UWP アプリの最初の出力](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="965bb-150">ボタンを選択し、TextBlock の内容が JSON テキストに置換されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="965bb-150">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![ボタンを選択した後の UWP アプリの出力](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="965bb-152">関連記事</span><span class="sxs-lookup"><span data-stu-id="965bb-152">Related articles</span></span>

- [<span data-ttu-id="965bb-153">パッケージ使用の概要とワークフロー</span><span class="sxs-lookup"><span data-stu-id="965bb-153">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="965bb-154">パッケージの検索と選択</span><span class="sxs-lookup"><span data-stu-id="965bb-154">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="965bb-155">パッケージをインストールする方法</span><span class="sxs-lookup"><span data-stu-id="965bb-155">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="965bb-156">NuGet の動作を構成する</span><span class="sxs-lookup"><span data-stu-id="965bb-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
