---
title: "Visual Studio を使用して NuGet パッケージを作成し公開するための入門ガイド | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Visual Studio 2017 を使用した、NuGet パッケージの作成と公開に関するチュートリアル。"
keywords: "NuGet パッケージの作成、NuGet パッケージの公開、NuGet チュートリアル、Visual Studio による NuGet パッケージの作成、msbuild pack"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a4d60fdc0f27f9c4080266e212ac1cfe470ba925
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package-using-visual-studio"></a><span data-ttu-id="85cbf-104">Visual Studio を使用した、パッケージの作成と公開</span><span class="sxs-lookup"><span data-stu-id="85cbf-104">Create and publish a package using Visual Studio</span></span>

<span data-ttu-id="85cbf-105">Visual Studio で.NET クラス ライブラリから NuGet パッケージを作成し、CLI ツールを使用してパッケージを nuget.org に公開する簡単なプロセスです。</span><span class="sxs-lookup"><span data-stu-id="85cbf-105">It's a simple process to create a NuGet package from a .NET Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="85cbf-106">前提条件</span><span class="sxs-lookup"><span data-stu-id="85cbf-106">Pre-requisites</span></span>

1. <span data-ttu-id="85cbf-107">[visualstudio.com](https://www.visualstudio.com/) から Visual Studio 2017 の任意のエディションと、.NET 関連の任意のワークロードをインストールします。</span><span class="sxs-lookup"><span data-stu-id="85cbf-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="85cbf-108">Visual Studio 2017 では、.NET ワークロードをインストールする際、NuGet 機能は自動的に含まれません。</span><span class="sxs-lookup"><span data-stu-id="85cbf-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="85cbf-109">`nuget.exe` CLI をインストールします。[nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)からその `.exe`ファイルをダウンロードし、適切なフォルダーに保存して、そのフォルダーを PATH 環境変数に追加してください。</span><span class="sxs-lookup"><span data-stu-id="85cbf-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="85cbf-110">または、[.NET Core SDK](https://www.microsoft.com/net/download/) をインストールしている場合は、`dotnet` CLI を使用できます。</span><span class="sxs-lookup"><span data-stu-id="85cbf-110">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="85cbf-111">まだ持っていない場合は、[nuget.org で無料アカウントを登録](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-111">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="85cbf-112">新しいアカウントを作成すると、確認メールが送信されます。</span><span class="sxs-lookup"><span data-stu-id="85cbf-112">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="85cbf-113">パッケージをアップロードするには、その前にアカウントを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85cbf-113">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="85cbf-114">クラス ライブラリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="85cbf-114">Create a class library project</span></span>

<span data-ttu-id="85cbf-115">パッケージ化するコードに既存の .NET クラス ライブラリ プロジェクトを使用することも、次の手順に従って単純なプロジェクトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="85cbf-115">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="85cbf-116">Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、**[Visual C#]、[.NET Standard]** ノードの順に展開して "クラス ライブラリ (.NET Standard)" テンプレートを選択し、プロジェクトに AppLogger という名前を付け、**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="85cbf-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="85cbf-117">作成されたプロジェクト ファイルを右クリックし、**[ビルド]** を選択して、プロジェクトが正しく作成されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="85cbf-118">DLL は、デバッグ フォルダー (または代わりにその構成をビルドした場合はリリース フォルダー) 内にあります。</span><span class="sxs-lookup"><span data-stu-id="85cbf-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="85cbf-119">実際の NuGet パッケージ内ではもちろん、多くの便利な機能を実装し、他のユーザーはそれを使用してアプリケーションをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="85cbf-119">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="85cbf-120">しかし、このチュートリアルでは、パッケージを作成するには、テンプレートのクラス ライブラリで十分なため、追加のコードを記述することはありません。</span><span class="sxs-lookup"><span data-stu-id="85cbf-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="85cbf-121">それでも、パッケージの一部の機能コードが必要な場合は、次のように使用します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-121">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="85cbf-122">それ以外を選択する理由がない限り、.NET Standard は最も広い範囲の使用プロジェクトとの互換性を提供するため、NuGet パッケージの優先ターゲットです。</span><span class="sxs-lookup"><span data-stu-id="85cbf-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="85cbf-123">パッケージのプロパティを構成する</span><span class="sxs-lookup"><span data-stu-id="85cbf-123">Configure package properties</span></span>

1. <span data-ttu-id="85cbf-124">**[プロジェクト]、[プロパティ]** メニュー コマンドの順に選択し、**[パッケージ]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-124">Select the **Project > Properties** menu command, then select the **Package** tab:</span></span>

    ![Visual Studio プロジェクト内の NuGet パッケージのプロパティ](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="85cbf-126">公開用にビルドされたパッケージの場合は、**Tags**プロパティに特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="85cbf-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="85cbf-127">パッケージに一意の識別子を付けて、他の必要なプロパティを指定します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="85cbf-128">さまざまなプロパティについては、[.nuspec ファイルのリファレンス](../reference/nuspec.md) ページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="85cbf-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="85cbf-129">これらのプロパティはすべて、Visual Studio でプロジェクト用に作成された `.nuspec`マニフェストに保存されます。</span><span class="sxs-lookup"><span data-stu-id="85cbf-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="85cbf-130">パッケージには、nuget.org または使用しているホスト全体で一意の識別子を付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="85cbf-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="85cbf-131">このチュートリアルでは、以降の公開手順でパッケージを一般公開するので (ただし、誰かが実際に使用する可能性はありません)、名前に "Sample" または "Test" を含めることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="85cbf-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="85cbf-132">既に存在する名前のパッケージを公開しようとすると、エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="85cbf-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="85cbf-133">省略可能: プロジェクト ファイルで直接プロパティを表示するには、ソリューション エクスプローラーでプロジェクトを右クリックし、**[Edit AppLogger.csproj]\(AppLogger.csproj の編集\)** を選択します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="85cbf-134">pack コマンドを実行する</span><span class="sxs-lookup"><span data-stu-id="85cbf-134">Run the pack command</span></span>

1. <span data-ttu-id="85cbf-135">構成を **[リリース]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="85cbf-136">**ソリューション エクスプローラー**で、プロジェクトを右クリックし、**[パック]** コマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio プロジェクトのコンテキスト メニューの NuGet パック コマンド](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="85cbf-138">Visual Studio により、プロジェクトがビルドされ、`.nupkg` ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="85cbf-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="85cbf-139">**[出力]** ウィンドウで (次のような) 詳細を確認します。このウィンドウには、パッケージ ファイルへのパスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="85cbf-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="85cbf-140">ビルドされたアセンブリは .NET Standard 2.0 ターゲットに適合するため `bin\Release\netstandard2.0` にもあります。</span><span class="sxs-lookup"><span data-stu-id="85cbf-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="85cbf-141">別のオプション: MSBuild の pack</span><span class="sxs-lookup"><span data-stu-id="85cbf-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="85cbf-142">**Pack** メニュー コマンドを使用する代わりとして、NuGet 4.x+ と MSBuild 15.1+ ではプロジェクトに必要なパッケージ データが含まれている場合に `pack` ターゲットをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="85cbf-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data:</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="85cbf-143">このパッケージは `bin\Release` フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="85cbf-143">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="85cbf-144">`msbuild /t:pack` のその他のオプションについては、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target)」(MSBuild ターゲットとしての NuGet のパックと復元) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="85cbf-144">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="85cbf-145">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="85cbf-145">Publish the package</span></span>

<span data-ttu-id="85cbf-146">`.nupkg` ファイルを作成したら、`nuget.exe` CLI または `dotnet.exe` CLI と、nuget.org から取得した API キーを使用して、そのファイルを nuget.org に公開します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-146">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="85cbf-147">API キーを取得する</span><span class="sxs-lookup"><span data-stu-id="85cbf-147">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="85cbf-148">nuget push を使用して公開する</span><span class="sxs-lookup"><span data-stu-id="85cbf-148">Publish with nuget push</span></span>

<span data-ttu-id="85cbf-149">この手順は、`dotnet.exe`の使用に代わる方法です。</span><span class="sxs-lookup"><span data-stu-id="85cbf-149">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="85cbf-150">`.nupkg`ファイルを含むフォルダーに変更します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-150">Change to the folder containing the `.nupkg` file..</span></span>

1. <span data-ttu-id="85cbf-151">次のコマンドでパッケージ名を指定し、キーを API キーに置き換えて、コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="85cbf-151">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="85cbf-152">nuget.exe によって公開プロセスの結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="85cbf-152">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="85cbf-153">[nuget push](../tools/cli-ref-push.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="85cbf-153">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="85cbf-154">dotnet nuget push を使用して公開する</span><span class="sxs-lookup"><span data-stu-id="85cbf-154">Publish with dotnet nuget push</span></span>

<span data-ttu-id="85cbf-155">この手順は、`nuget.exe`の使用に代わる方法です。</span><span class="sxs-lookup"><span data-stu-id="85cbf-155">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="85cbf-156">公開エラー</span><span class="sxs-lookup"><span data-stu-id="85cbf-156">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="85cbf-157">公開済みパッケージを管理する</span><span class="sxs-lookup"><span data-stu-id="85cbf-157">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="85cbf-158">関連トピック</span><span class="sxs-lookup"><span data-stu-id="85cbf-158">Related topics</span></span>

- [<span data-ttu-id="85cbf-159">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="85cbf-159">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="85cbf-160">パッケージの公開</span><span class="sxs-lookup"><span data-stu-id="85cbf-160">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="85cbf-161">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="85cbf-161">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="85cbf-162">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="85cbf-162">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="85cbf-163">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="85cbf-163">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="85cbf-164">.NET Standard ライブラリのドキュメント</span><span class="sxs-lookup"><span data-stu-id="85cbf-164">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="85cbf-165">.NET Framework から .NET Core への移植</span><span class="sxs-lookup"><span data-stu-id="85cbf-165">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)