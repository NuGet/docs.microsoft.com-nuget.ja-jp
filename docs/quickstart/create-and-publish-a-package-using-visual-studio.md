---
title: Windows 上で Visual Studio を使用した .NET Standard NuGet パッケージの作成と公開
description: Windows の Visual Studio を使用した、.NET Standard NuGet パッケージの作成と公開に関するチュートリアルです。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 86e71460094de9b799384db83456a68db57647af
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419904"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="36661-103">クイック スタート: Visual Studio を使用した NuGet パッケージの作成と公開 (.NET Standard、Windows のみ)</span><span class="sxs-lookup"><span data-stu-id="36661-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="36661-104">Windows の Visual Studio で .NET Standard クラス ライブラリから NuGet パッケージを作成し、CLI ツールを使用してパッケージを nuget.org に公開する簡単なプロセスです。</span><span class="sxs-lookup"><span data-stu-id="36661-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="36661-105">Visual Studio for Mac をお使いの場合は、NuGet パッケージの作成に関する[こちらの情報](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library)を参照するか、[dotnet CLI ツール](create-and-publish-a-package-using-the-dotnet-cli.md)をご使用ください。</span><span class="sxs-lookup"><span data-stu-id="36661-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36661-106">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="36661-106">Prerequisites</span></span>

1. <span data-ttu-id="36661-107">[visualstudio.com](https://www.visualstudio.com/) から Visual Studio 2017 以降の任意のエディションを、.NET Core 関連のワークロードと共にインストールします。</span><span class="sxs-lookup"><span data-stu-id="36661-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="36661-108">まだインストールされていない場合、`dotnet` CLI をインストールします。</span><span class="sxs-lookup"><span data-stu-id="36661-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="36661-109">`dotnet` CLI について、Visual Studio 2017 以降、`dotnet` CLI は .NET Core 関連のワークロードと共に自動的にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="36661-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="36661-110">それ以外の場合は、[.NET Core SDK](https://www.microsoft.com/net/download/) をインストールして `dotnet` CLI を取得します。</span><span class="sxs-lookup"><span data-stu-id="36661-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="36661-111">[SDK スタイルの形式](../resources/check-project-format.md) (SDK 属性) を使用する .NET Standard プロジェクトには、`dotnet` CLI が必要です。</span><span class="sxs-lookup"><span data-stu-id="36661-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="36661-112">Visual Studio 2017 以降の既定のクラス ライブラリ テンプレート (この記事で使用するものです) では、SDK 属性が使用されます。</span><span class="sxs-lookup"><span data-stu-id="36661-112">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="36661-113">この記事では、`dotnet` CLI を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="36661-113">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="36661-114">`nuget.exe` CLI を使用してもあらゆる NuGet パッケージを公開できますが、この記事の手順の一部は SDK スタイルのプロジェクトと dotnet CLI に固有のものです。</span><span class="sxs-lookup"><span data-stu-id="36661-114">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="36661-115">nuget.exe CLI は、[非 SDK 形式のプロジェクト](../resources/check-project-format.md) (通常は .NET Framework) 用に使用されます。</span><span class="sxs-lookup"><span data-stu-id="36661-115">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="36661-116">非 SDK スタイルのプロジェクトを使用している場合は、[.NET Framework パッケージの作成と公開 (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) に関するページの手順に従って、パッケージの作成と公開を行ってください。</span><span class="sxs-lookup"><span data-stu-id="36661-116">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="36661-117">まだ持っていない場合は、[nuget.org で無料アカウントを登録](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account)します。</span><span class="sxs-lookup"><span data-stu-id="36661-117">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="36661-118">新しいアカウントを作成すると、確認メールが送信されます。</span><span class="sxs-lookup"><span data-stu-id="36661-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="36661-119">パッケージをアップロードするには、その前にアカウントを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="36661-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="36661-120">クラス ライブラリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="36661-120">Create a class library project</span></span>

<span data-ttu-id="36661-121">パッケージ化するコードに既存の .NET Standard クラス ライブラリ プロジェクトを使用することも、次の手順に従って単純なプロジェクトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="36661-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="36661-122">Visual Studio で、 **[ファイル]、[新規]、[プロジェクト]** の順に選択し、 **[Visual C#]、[.NET Standard]** ノードの順に展開して "クラス ライブラリ (.NET Standard)" テンプレートを選択し、プロジェクトに AppLogger という名前を付け、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="36661-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="36661-123">作成されたプロジェクト ファイルを右クリックし、 **[ビルド]** を選択して、プロジェクトが正しく作成されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="36661-123">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="36661-124">DLL は、デバッグ フォルダー (または代わりにその構成をビルドした場合はリリース フォルダー) 内にあります。</span><span class="sxs-lookup"><span data-stu-id="36661-124">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="36661-125">実際の NuGet パッケージ内ではもちろん、多くの便利な機能を実装し、他のユーザーはそれを使用してアプリケーションをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="36661-125">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="36661-126">しかし、このチュートリアルでは、パッケージを作成するには、テンプレートのクラス ライブラリで十分なため、追加のコードを記述することはありません。</span><span class="sxs-lookup"><span data-stu-id="36661-126">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="36661-127">それでも、パッケージの一部の機能コードが必要な場合は、次のように使用します。</span><span class="sxs-lookup"><span data-stu-id="36661-127">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> <span data-ttu-id="36661-128">それ以外を選択する理由がない限り、.NET Standard は最も広い範囲の使用プロジェクトとの互換性を提供するため、NuGet パッケージの優先ターゲットです。</span><span class="sxs-lookup"><span data-stu-id="36661-128">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="36661-129">パッケージのプロパティを構成する</span><span class="sxs-lookup"><span data-stu-id="36661-129">Configure package properties</span></span>

1. <span data-ttu-id="36661-130">ソリューション エクスプローラーでプロジェクトを右クリックし、 **[プロパティ]** メニュー コマンドを選択してから、 **[パッケージ]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="36661-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="36661-131">**[パッケージ]** タブは、Visual Studio の SDK スタイルのプロジェクト (通常は .NET Standard または .NET Core クラス ライブラリ プロジェクト) に対してのみ表示されます。非 SDK スタイルのプロジェクト (通常は .NET Framework) をターゲットとしている場合は、[プロジェクトを移行](../reference/migrate-packages-config-to-package-reference.md)して `dotnet` CLI を使用するか、[.NET Framework パッケージの作成と公開](create-and-publish-a-package-using-visual-studio-net-framework.md)または [.NET Framework パッケージの作成と公開](create-and-publish-a-package-using-visual-studio-net-framework.md)に関するページの詳細な手順をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="36661-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Visual Studio プロジェクト内の NuGet パッケージのプロパティ](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="36661-133">公開用にビルドされたパッケージの場合は、**Tags**プロパティに特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="36661-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="36661-134">パッケージに一意の識別子を付けて、他の必要なプロパティを指定します。</span><span class="sxs-lookup"><span data-stu-id="36661-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="36661-135">さまざまなプロパティについては、[.nuspec ファイルのリファレンス](../reference/nuspec.md) ページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="36661-135">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="36661-136">これらのプロパティはすべて、Visual Studio でプロジェクト用に作成された `.nuspec`マニフェストに保存されます。</span><span class="sxs-lookup"><span data-stu-id="36661-136">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="36661-137">パッケージには、nuget.org または使用しているホスト全体で一意の識別子を付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="36661-137">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="36661-138">このチュートリアルでは、以降の公開手順でパッケージを一般公開するので (ただし、誰かが実際に使用する可能性はありません)、名前に "Sample" または "Test" を含めることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="36661-138">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="36661-139">既に存在する名前のパッケージを公開しようとすると、エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="36661-139">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="36661-140">省略可能: プロジェクト ファイルで直接プロパティを表示するには、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[Edit AppLogger.csproj]\(AppLogger.csproj の編集\)** を選択します。</span><span class="sxs-lookup"><span data-stu-id="36661-140">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="36661-141">このオプションは、Visual Studio 2017 以降で、SDK スタイルの属性を使用するプロジェクトに対してのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="36661-141">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="36661-142">それ以外の場合は、プロジェクトを右クリックして **[プロジェクトのアンロード]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="36661-142">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="36661-143">次に、アンロードされたプロジェクトを右クリックし、 **[Edit AppLogger.csproj]\(AppLogger.csproj の編集\)** を選択します。</span><span class="sxs-lookup"><span data-stu-id="36661-143">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="36661-144">pack コマンドを実行する</span><span class="sxs-lookup"><span data-stu-id="36661-144">Run the pack command</span></span>

1. <span data-ttu-id="36661-145">構成を **[リリース]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="36661-145">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="36661-146">**ソリューション エクスプローラー**で、プロジェクトを右クリックし、 **[パック]** コマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="36661-146">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio プロジェクトのコンテキスト メニューの NuGet パック コマンド](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="36661-148">**[パック]** コマンドが表示されない場合は、プロジェクトがおそらく SDK スタイルのプロジェクトではないため、`nuget.exe` CLI を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="36661-148">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="36661-149">[プロジェクトを移行](../reference/migrate-packages-config-to-package-reference.md)して `dotnet` CLIを使用するか、代わりに [.NET Framework パッケージの作成と公開](create-and-publish-a-package-using-visual-studio-net-framework.md)に関するページの詳細な手順をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="36661-149">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="36661-150">Visual Studio により、プロジェクトがビルドされ、`.nupkg` ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="36661-150">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="36661-151">**[出力]** ウィンドウで (次のような) 詳細を確認します。このウィンドウには、パッケージ ファイルへのパスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="36661-151">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="36661-152">ビルドされたアセンブリは .NET Standard 2.0 ターゲットに適合するため `bin\Release\netstandard2.0` にもあります。</span><span class="sxs-lookup"><span data-stu-id="36661-152">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="36661-153">別のオプション: MSBuild の pack</span><span class="sxs-lookup"><span data-stu-id="36661-153">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="36661-154">NuGet 4.x 以降と MSBuild 15.1 以降では、**Pack** メニュー コマンドを使用する代わりに、プロジェクトに必要なパッケージ データが含まれている場合に `pack` ターゲットをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="36661-154">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="36661-155">コマンド プロンプトを開き、プロジェクト フォルダーに移動し、次のコマンドを実行します</span><span class="sxs-lookup"><span data-stu-id="36661-155">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="36661-156">(MSBuild に必要なすべてのパスが構成されるため、通常は [スタート] メニューの [Developer Command Prompt for Visual Studio]\(Visual Studio 用開発者コマンド プロンプト\) を使用します)。</span><span class="sxs-lookup"><span data-stu-id="36661-156">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="36661-157">このパッケージは `bin\Release` フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="36661-157">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="36661-158">`msbuild -t:pack` のその他のオプションについては、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target)」(MSBuild ターゲットとしての NuGet のパックと復元) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="36661-158">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="36661-159">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="36661-159">Publish the package</span></span>

<span data-ttu-id="36661-160">`.nupkg` ファイルを作成したら、`nuget.exe` CLI または `dotnet.exe` CLI と、nuget.org から取得した API キーを使用して、そのファイルを nuget.org に公開します。</span><span class="sxs-lookup"><span data-stu-id="36661-160">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="36661-161">API キーを取得する</span><span class="sxs-lookup"><span data-stu-id="36661-161">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="36661-162">dotnet nuget push を使用して公開する (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="36661-162">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="36661-163">`nuget.exe` を使用する代わりに、この手順を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="36661-163">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="36661-164">パッケージを公開するには、まずコマンド ラインを開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="36661-164">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="36661-165">nuget push を使用して公開する (nuget.exe CLI)</span><span class="sxs-lookup"><span data-stu-id="36661-165">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="36661-166">この手順は、`dotnet.exe`の使用に代わる方法です。</span><span class="sxs-lookup"><span data-stu-id="36661-166">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="36661-167">コマンド ラインを開き、`.nupkg` ファイルを含むフォルダーに変更します。</span><span class="sxs-lookup"><span data-stu-id="36661-167">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="36661-168">使用するパッケージ名 (一意のパッケージ ID) を指定し、キーの値を使用する API キーに置き換えて、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="36661-168">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="36661-169">nuget.exe によって公開プロセスの結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="36661-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="36661-170">[nuget push](../reference/cli-reference/cli-ref-push.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="36661-170">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="36661-171">公開エラー</span><span class="sxs-lookup"><span data-stu-id="36661-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="36661-172">公開済みパッケージを管理する</span><span class="sxs-lookup"><span data-stu-id="36661-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="36661-173">ReadMe とその他のファイルの追加</span><span class="sxs-lookup"><span data-stu-id="36661-173">Adding a readme and other files</span></span>

<span data-ttu-id="36661-174">パッケージに含めるファイルを直接指定するには、プロジェクト ファイルを編集して、`content` プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="36661-174">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="36661-175">これにより、パッケージ ルートに `readme.txt` という名前のファイルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="36661-175">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="36661-176">Visual Studio では、パッケージを直接インストールした直後、そのファイルの内容がプレーンテキストとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="36661-176">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="36661-177">(パッケージが依存関係としてインストールされた場合、ReadMe ファイルは表示されません。)</span><span class="sxs-lookup"><span data-stu-id="36661-177">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="36661-178">たとえば、HtmlAgilityPack パッケージの ReadMe は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="36661-178">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![インストール時の NuGet パッケージの ReadMe ファイルの表示](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="36661-180">プロジェクトのルートに readme.txt を追加するだけでは、作成されたパッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="36661-180">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="36661-181">関連トピック</span><span class="sxs-lookup"><span data-stu-id="36661-181">Related topics</span></span>

- [<span data-ttu-id="36661-182">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="36661-182">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="36661-183">パッケージの公開</span><span class="sxs-lookup"><span data-stu-id="36661-183">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="36661-184">プレリリース パッケージ</span><span class="sxs-lookup"><span data-stu-id="36661-184">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="36661-185">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="36661-185">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="36661-186">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="36661-186">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="36661-187">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="36661-187">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="36661-188">.NET Standard ライブラリのドキュメント</span><span class="sxs-lookup"><span data-stu-id="36661-188">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="36661-189">.NET Framework から .NET Core への移植</span><span class="sxs-lookup"><span data-stu-id="36661-189">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
