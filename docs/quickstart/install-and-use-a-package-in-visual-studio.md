---
title: Visual Studio に NuGet パッケージをインストールして使用する
description: Visual Studio プロジェクトで NuGet パッケージをインストールし、使用するプロセスを説明したチュートリアル。
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775523"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="effb2-103">クイック スタート: Visual Studio にパッケージをインストールして使用する (Windows のみ)</span><span class="sxs-lookup"><span data-stu-id="effb2-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="effb2-104">NuGet パッケージには、他の開発者がお客様のプロジェクトで使用できるようにした、再利用可能なコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="effb2-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="effb2-105">背景については、[NuGet の紹介](../What-is-NuGet.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="effb2-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="effb2-106">パッケージは NuGet パッケージ マネージャー、[パッケージ マネージャー コンソール](../consume-packages/install-use-packages-powershell.md)、または [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md) を使用して、Visual Studio プロジェクトにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="effb2-106">Packages are installed into a Visual Studio project using the NuGet Package Manager, the [Package Manager Console](../consume-packages/install-use-packages-powershell.md), or the [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md).</span></span> <span data-ttu-id="effb2-107">この記事では、よく使用されている [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) パッケージと Windows Presentation Foundation (WPF) プロジェクトを使用したプロセスを示します。</span><span class="sxs-lookup"><span data-stu-id="effb2-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="effb2-108">同じプロセスは、他の任意の .NET または .NET Core プロジェクトにも適用されます。</span><span class="sxs-lookup"><span data-stu-id="effb2-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="effb2-109">インストール後、`using <namespace>` でコード内のパッケージを参照します。\<namespace\> は、使用しているパッケージに固有です。</span><span class="sxs-lookup"><span data-stu-id="effb2-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="effb2-110">参照が行われたら、その API からパッケージを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="effb2-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="effb2-111">**nuget.org を開始する**:*nuget.org* を参照するのは、.NET 開発者が自身のアプリケーションで再利用可能なコンポーネントを検索するための一般的な方法です。</span><span class="sxs-lookup"><span data-stu-id="effb2-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="effb2-112">*nuget.org* を直接検索するか、この記事に示すように、パッケージを検索して Visual Studio 内にインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="effb2-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="effb2-113">一般的な情報については、[NuGet パッケージの検索と評価](../consume-packages/finding-and-choosing-packages.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="effb2-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="effb2-114">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="effb2-114">Prerequisites</span></span>

- <span data-ttu-id="effb2-115">.NET デスクトップ開発ワークロードを利用する Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="effb2-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="effb2-116">[visualstudio.com](https://www.visualstudio.com/) から無料の 2019 Community Edition をインストールするか、Professional または Enterprise Edition を使用できます。</span><span class="sxs-lookup"><span data-stu-id="effb2-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="effb2-117">Visual Studio for Mac を使用している場合は、[Visual Studio for Mac でのパッケージのインストールと使用](install-and-use-a-package-in-visual-studio-mac.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="effb2-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="effb2-118">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="effb2-118">Create a project</span></span>

<span data-ttu-id="effb2-119">NuGet パッケージは任意の .NET プロジェクトにインストールできます。ただし、パッケージが同じターゲット フレームワークをプロジェクトとしてサポートしていることが条件です。</span><span class="sxs-lookup"><span data-stu-id="effb2-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="effb2-120">このチュートリアルでは、単純な WPF アプリを使用します。</span><span class="sxs-lookup"><span data-stu-id="effb2-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="effb2-121">**[ファイル]**  >  **[新しいプロジェクト]** を使用し、検索ボックスに「 **.NET**」と入力して、 **[WPF アプリ (.NET Framework)]** を選択し、Visual Studio にプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="effb2-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="effb2-122">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="effb2-122">Click **Next**.</span></span> <span data-ttu-id="effb2-123">プロンプトが表示されたら、 **[フレームワーク]** の既定値をそのまま受け入れます。</span><span class="sxs-lookup"><span data-stu-id="effb2-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="effb2-124">Visual Studio によってプロジェクトが作成され、ソリューション エクスプローラーに開かれます。</span><span class="sxs-lookup"><span data-stu-id="effb2-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="effb2-125">Newtonsoft.Json NuGet パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="effb2-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="effb2-126">パッケージをインストールするには、NuGet パッケージ マネージャーまたはパッケージ マネージャー コンソールのいずれかを使用できます。</span><span class="sxs-lookup"><span data-stu-id="effb2-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="effb2-127">パッケージをインストールすると、NuGet では、プロジェクト ファイルまたは `packages.config` ファイルのどちらかに依存関係が記録されます (プロジェクトの形式に依存します)。</span><span class="sxs-lookup"><span data-stu-id="effb2-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="effb2-128">詳細については、「[パッケージ利用のワークフロー](../consume-packages/Overview-and-Workflow.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="effb2-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="effb2-129">NuGet パッケージ マネージャー</span><span class="sxs-lookup"><span data-stu-id="effb2-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="effb2-130">ソリューション エクスプローラーで **[参照]** を右クリックし、 **[NuGet パッケージの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="effb2-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![プロジェクト参照の NuGet パッケージ管理コマンド](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="effb2-132">**[パッケージ ソース]** として "nuget.org" を選択し、 **[参照]** タブを選択し、「**Newtonsoft.Json**」を検索し、一覧からそのパッケージを選択し、 **[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="effb2-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft.Json パッケージを見つけます](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="effb2-134">NuGet パッケージ マネージャーについて詳しくは、[Visual Studio を使用したパッケージのインストールおよび管理](../consume-packages/install-use-packages-visual-studio.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="effb2-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="effb2-135">ラインセンス プロンプトに同意します。</span><span class="sxs-lookup"><span data-stu-id="effb2-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="effb2-136">(Visual Studio 2017 のみ) パッケージ管理の形式を選択するように求められたら、 **[プロジェクト ファイルの PackageReference]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="effb2-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![パッケージ管理形式の選択](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="effb2-138">変更の確認を求められた場合、 **[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="effb2-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="effb2-139">パッケージ マネージャー コンソール</span><span class="sxs-lookup"><span data-stu-id="effb2-139">Package Manager Console</span></span>

1. <span data-ttu-id="effb2-140">**[ツール]**  >  **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** メニュー コマンドの順に選択します。</span><span class="sxs-lookup"><span data-stu-id="effb2-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="effb2-141">コンソールが開いたら、 **[既定のプロジェクト]** ドロップダウン リストに、パッケージをインストールするプロジェクトが表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="effb2-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="effb2-142">ソリューション内に単一のプロジェクトがあれば、それは既に選択されています。</span><span class="sxs-lookup"><span data-stu-id="effb2-142">If you have a single project in the solution, it is already selected.</span></span>

    ![パッケージ用のプロジェクトを選択します](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="effb2-144">コマンド `Install-Package Newtonsoft.Json` を入力します (「[Install-Package](../reference/ps-reference/ps-ref-install-package.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="effb2-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="effb2-145">コンソール ウィンドウに、このコマンドの出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="effb2-145">The console window shows output for the command.</span></span> <span data-ttu-id="effb2-146">通常、エラーは、パッケージがプロジェクトのターゲット フレームワークと互換性がないことを示します。</span><span class="sxs-lookup"><span data-stu-id="effb2-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="effb2-147">パッケージ マネージャー コンソールについて詳しくは、[パッケージ マネージャー コンソールを使用したパッケージのインストールおよび管理](../consume-packages/install-use-packages-powershell.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="effb2-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="effb2-148">アプリで Newtonsoft.Json API を使用する</span><span class="sxs-lookup"><span data-stu-id="effb2-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="effb2-149">プロジェクトに Newtonsoft.Json パッケージがある場合、その `JsonConvert.SerializeObject` メソッドを呼び出し、オブジェクトを人間が読める文字列に変換できます。</span><span class="sxs-lookup"><span data-stu-id="effb2-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="effb2-150">`MainWindow.xaml`を開いて、既存の `Grid` 要素を次の XAML に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="effb2-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="effb2-151">`MainWindow.xaml.cs` ファイル (ソリューション エクスプローラーの `MainWindow.xaml` ノード下にあります) を開いて、`MainWindow` クラス内に次のコードを挿入します。</span><span class="sxs-lookup"><span data-stu-id="effb2-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="effb2-152">プロジェクトに Newtonsoft.Json パッケージを追加した後でも、`JsonConvert` の下に赤い波線が表示されます。これは、コード ファイルの上部に `using` ステートメントが必要であるためです。</span><span class="sxs-lookup"><span data-stu-id="effb2-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="effb2-153">アプリをビルドして実行します。F5 キーを押すか、 **[デバッグ]**  >  **[デバッグの開始]** を選択してください。</span><span class="sxs-lookup"><span data-stu-id="effb2-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![WPF アプリの最初の出力](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="effb2-155">ボタンを選択し、TextBlock の内容が JSON テキストに置換されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="effb2-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![ボタンを選択した後の WPF アプリの出力](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="effb2-157">関連ビデオ</span><span class="sxs-lookup"><span data-stu-id="effb2-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="effb2-158">他の NuGet ビデオは、[Channel 9](https://channel9.msdn.com/Series/NuGet-101) および [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) でご覧いただけます。</span><span class="sxs-lookup"><span data-stu-id="effb2-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="effb2-159">次の手順</span><span class="sxs-lookup"><span data-stu-id="effb2-159">Next steps</span></span>

<span data-ttu-id="effb2-160">無事に、最初の NuGet パッケージをインストールして使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="effb2-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="effb2-161">Visual Studio を使用してパッケージをインストールして管理する</span><span class="sxs-lookup"><span data-stu-id="effb2-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="effb2-162">パッケージ マネージャー コンソールを使用してパッケージをインストールして管理する</span><span class="sxs-lookup"><span data-stu-id="effb2-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="effb2-163">NuGet による提供についてさらに詳しく調べるには、下のリンクを選択してください。</span><span class="sxs-lookup"><span data-stu-id="effb2-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="effb2-164">パッケージ使用の概要とワークフロー</span><span class="sxs-lookup"><span data-stu-id="effb2-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="effb2-165">パッケージの検索と選択</span><span class="sxs-lookup"><span data-stu-id="effb2-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="effb2-166">プロジェクト ファイルのパッケージ参照</span><span class="sxs-lookup"><span data-stu-id="effb2-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
