---
title: Windows の Visual Studio を使用した .NET Standard パッケージの作成と公開
description: Windows の Visual Studio 2017 を使用した、.NET Standard NuGet パッケージの作成と公開に関するチュートリアルです。
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: faea00372bd387aee1502e388ad1ea88de07b95d
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453521"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="5e2b6-103">クイック スタート: Visual Studio を使用した NuGet パッケージの作成と公開 (.NET Standard、Windows のみ)</span><span class="sxs-lookup"><span data-stu-id="5e2b6-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="5e2b6-104">Windows の Visual Studio で .NET Standard クラス ライブラリから NuGet パッケージを作成し、CLI ツールを使用してパッケージを nuget.org に公開する簡単なプロセスです。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="5e2b6-105">このクイック スタートが適用されるのは、Windows の Visual Studio 2017 のみです。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="5e2b6-106">ここで説明される機能は、Visual Studio for Mac には含まれません。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="5e2b6-107">代わりに [dotnet CLI ツール](create-and-publish-a-package-using-the-dotnet-cli.md)を使用してください。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e2b6-108">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="5e2b6-108">Prerequisites</span></span>

1. <span data-ttu-id="5e2b6-109">[visualstudio.com](https://www.visualstudio.com/) から Visual Studio 2017 の任意のエディションと、.NET 関連の任意のワークロードをインストールします。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="5e2b6-110">Visual Studio 2017 では、.NET ワークロードをインストールする際、NuGet 機能は自動的に含まれません。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="5e2b6-111">`nuget.exe` CLI をインストールします。[nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)からその `.exe`ファイルをダウンロードし、適切なフォルダーに保存して、そのフォルダーを PATH 環境変数に追加してください。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="5e2b6-112">または、[.NET Core SDK](https://www.microsoft.com/net/download/) をインストールしている場合は、`dotnet` CLI を使用できます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-112">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="5e2b6-113">まだ持っていない場合は、[nuget.org で無料アカウントを登録](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-113">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="5e2b6-114">新しいアカウントを作成すると、確認メールが送信されます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-114">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="5e2b6-115">パッケージをアップロードするには、その前にアカウントを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-115">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="5e2b6-116">クラス ライブラリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="5e2b6-116">Create a class library project</span></span>

<span data-ttu-id="5e2b6-117">パッケージ化するコードに既存の .NET Standard クラス ライブラリ プロジェクトを使用することも、次の手順に従って単純なプロジェクトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-117">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="5e2b6-118">Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、**[Visual C#]、[.NET Standard]** ノードの順に展開して "クラス ライブラリ (.NET Standard)" テンプレートを選択し、プロジェクトに AppLogger という名前を付け、**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-118">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="5e2b6-119">作成されたプロジェクト ファイルを右クリックし、**[ビルド]** を選択して、プロジェクトが正しく作成されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-119">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="5e2b6-120">DLL は、デバッグ フォルダー (または代わりにその構成をビルドした場合はリリース フォルダー) 内にあります。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-120">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="5e2b6-121">実際の NuGet パッケージ内ではもちろん、多くの便利な機能を実装し、他のユーザーはそれを使用してアプリケーションをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-121">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="5e2b6-122">しかし、このチュートリアルでは、パッケージを作成するには、テンプレートのクラス ライブラリで十分なため、追加のコードを記述することはありません。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-122">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="5e2b6-123">それでも、パッケージの一部の機能コードが必要な場合は、次のように使用します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-123">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="5e2b6-124">それ以外を選択する理由がない限り、.NET Standard は最も広い範囲の使用プロジェクトとの互換性を提供するため、NuGet パッケージの優先ターゲットです。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-124">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="5e2b6-125">パッケージのプロパティを構成する</span><span class="sxs-lookup"><span data-stu-id="5e2b6-125">Configure package properties</span></span>

1. <span data-ttu-id="5e2b6-126">**[プロジェクト]、[プロパティ]** メニュー コマンドの順に選択し、**[パッケージ]** タブを選択します(**[パッケージ]** タブは .NET Standard クラス ライブラリ プロジェクトの場合にのみに表示されます。 .NET Framework をターゲットにする場合は代わりに「[Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md)」 (.NET Framework パッケージの作成と公開) を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-126">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="5e2b6-127">.NET Standard プロジェクトに対して表示されないときは、場合によっては、Visual Studio 2017 を最新リリースに更新する必要があります。)</span><span class="sxs-lookup"><span data-stu-id="5e2b6-127">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Visual Studio プロジェクト内の NuGet パッケージのプロパティ](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="5e2b6-129">公開用にビルドされたパッケージの場合は、**Tags**プロパティに特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-129">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="5e2b6-130">パッケージに一意の識別子を付けて、他の必要なプロパティを指定します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-130">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="5e2b6-131">さまざまなプロパティについては、[.nuspec ファイルのリファレンス](../reference/nuspec.md) ページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-131">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="5e2b6-132">これらのプロパティはすべて、Visual Studio でプロジェクト用に作成された `.nuspec`マニフェストに保存されます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-132">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="5e2b6-133">パッケージには、nuget.org または使用しているホスト全体で一意の識別子を付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="5e2b6-134">このチュートリアルでは、以降の公開手順でパッケージを一般公開するので (ただし、誰かが実際に使用する可能性はありません)、名前に "Sample" または "Test" を含めることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="5e2b6-135">既に存在する名前のパッケージを公開しようとすると、エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="5e2b6-136">省略可能: プロジェクト ファイルで直接プロパティを表示するには、ソリューション エクスプローラーでプロジェクトを右クリックし、**[Edit AppLogger.csproj]\(AppLogger.csproj の編集\)** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-136">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="5e2b6-137">pack コマンドを実行する</span><span class="sxs-lookup"><span data-stu-id="5e2b6-137">Run the pack command</span></span>

1. <span data-ttu-id="5e2b6-138">構成を **[リリース]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-138">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="5e2b6-139">**ソリューション エクスプローラー**で、プロジェクトを右クリックし、**[パック]** コマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-139">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio プロジェクトのコンテキスト メニューの NuGet パック コマンド](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="5e2b6-141">Visual Studio により、プロジェクトがビルドされ、`.nupkg` ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-141">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="5e2b6-142">**[出力]** ウィンドウで (次のような) 詳細を確認します。このウィンドウには、パッケージ ファイルへのパスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-142">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="5e2b6-143">ビルドされたアセンブリは .NET Standard 2.0 ターゲットに適合するため `bin\Release\netstandard2.0` にもあります。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-143">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="5e2b6-144">別のオプション: MSBuild の pack</span><span class="sxs-lookup"><span data-stu-id="5e2b6-144">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="5e2b6-145">NuGet 4.x 以降と MSBuild 15.1 以降では、**Pack** メニュー コマンドを使用する代わりに、プロジェクトに必要なパッケージ データが含まれている場合に `pack` ターゲットをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-145">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="5e2b6-146">コマンド プロンプトを開き、プロジェクト フォルダーに移動し、次のコマンドを実行します</span><span class="sxs-lookup"><span data-stu-id="5e2b6-146">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="5e2b6-147">(MSBuild に必要なすべてのパスが構成されるため、通常は [スタート] メニューの [Developer Command Prompt for Visual Studio]\(Visual Studio 用開発者コマンド プロンプト\) を使用します)。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-147">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="5e2b6-148">このパッケージは `bin\Release` フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-148">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="5e2b6-149">`msbuild -t:pack` のその他のオプションについては、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target)」(MSBuild ターゲットとしての NuGet のパックと復元) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-149">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="5e2b6-150">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="5e2b6-150">Publish the package</span></span>

<span data-ttu-id="5e2b6-151">`.nupkg` ファイルを作成したら、`nuget.exe` CLI または `dotnet.exe` CLI と、nuget.org から取得した API キーを使用して、そのファイルを nuget.org に公開します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-151">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="5e2b6-152">API キーを取得する</span><span class="sxs-lookup"><span data-stu-id="5e2b6-152">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="5e2b6-153">nuget push を使用して公開する</span><span class="sxs-lookup"><span data-stu-id="5e2b6-153">Publish with nuget push</span></span>

<span data-ttu-id="5e2b6-154">この手順は、`dotnet.exe`の使用に代わる方法です。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-154">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="5e2b6-155">`.nupkg` ファイルを含むフォルダーに変更します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-155">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="5e2b6-156">次のコマンドでパッケージ名を指定し、キーを API キーに置き換えて、コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-156">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="5e2b6-157">nuget.exe によって公開プロセスの結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-157">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="5e2b6-158">[nuget push](../tools/cli-ref-push.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-158">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="5e2b6-159">dotnet nuget push を使用して公開する</span><span class="sxs-lookup"><span data-stu-id="5e2b6-159">Publish with dotnet nuget push</span></span>

<span data-ttu-id="5e2b6-160">この手順は、`nuget.exe`の使用に代わる方法です。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-160">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="5e2b6-161">公開エラー</span><span class="sxs-lookup"><span data-stu-id="5e2b6-161">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="5e2b6-162">公開済みパッケージを管理する</span><span class="sxs-lookup"><span data-stu-id="5e2b6-162">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="5e2b6-163">ReadMe とその他のファイルの追加</span><span class="sxs-lookup"><span data-stu-id="5e2b6-163">Adding a readme and other files</span></span>

<span data-ttu-id="5e2b6-164">パッケージに含めるファイルを直接指定するには、プロジェクト ファイルを編集して、`content` プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-164">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="5e2b6-165">これにより、パッケージ ルートに `readme.txt` という名前のファイルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-165">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="5e2b6-166">Visual Studio では、パッケージを直接インストールした直後、そのファイルの内容がプレーンテキストとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-166">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="5e2b6-167">(パッケージが依存関係としてインストールされた場合、ReadMe ファイルは表示されません。)</span><span class="sxs-lookup"><span data-stu-id="5e2b6-167">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="5e2b6-168">たとえば、HtmlAgilityPack パッケージの ReadMe は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-168">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![インストール時の NuGet パッケージの ReadMe ファイルの表示](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="5e2b6-170">プロジェクトのルートに readme.txt を追加するだけでは、作成されたパッケージに含まれません。</span><span class="sxs-lookup"><span data-stu-id="5e2b6-170">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="5e2b6-171">関連トピック</span><span class="sxs-lookup"><span data-stu-id="5e2b6-171">Related topics</span></span>

- [<span data-ttu-id="5e2b6-172">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="5e2b6-172">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="5e2b6-173">パッケージの公開</span><span class="sxs-lookup"><span data-stu-id="5e2b6-173">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="5e2b6-174">プレリリース パッケージ</span><span class="sxs-lookup"><span data-stu-id="5e2b6-174">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="5e2b6-175">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="5e2b6-175">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="5e2b6-176">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="5e2b6-176">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="5e2b6-177">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="5e2b6-177">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="5e2b6-178">.NET Standard ライブラリのドキュメント</span><span class="sxs-lookup"><span data-stu-id="5e2b6-178">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="5e2b6-179">.NET Framework から .NET Core への移植</span><span class="sxs-lookup"><span data-stu-id="5e2b6-179">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
