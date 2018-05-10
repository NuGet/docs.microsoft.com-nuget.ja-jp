---
title: Visual Studio を使用した .NET Framework NuGet パッケージの作成と公開の入門ガイド
description: Visual Studio 2017 を使用した .NET Framework NuGet パッケージの作成と公開に関するチュートリアルです。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/13/2018
ms.topic: quickstart
ms.openlocfilehash: 01760034a121b1ff6f227e006415779898c4cf6d
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework"></a><span data-ttu-id="9a7b2-103">クイック スタート: Visual Studio を使用したパッケージの作成と公開 (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="9a7b2-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework)</span></span>

<span data-ttu-id="9a7b2-104">.NET Framework クラス ライブラリから NuGet パッケージを作成するには、Visual Studio で DLL を作成した後、nuget.exe コマンド ライン ツールを使用してパッケージを作成し、公開します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio, then using the nuget.exe command line tool to create and publish the package.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a7b2-105">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="9a7b2-105">Prerequisites</span></span>

1. <span data-ttu-id="9a7b2-106">[visualstudio.com](https://www.visualstudio.com/) から Visual Studio 2017 の任意のエディションと、.NET 関連の任意のワークロードをインストールします。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-106">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="9a7b2-107">Visual Studio 2017 では、.NET ワークロードをインストールする際、NuGet 機能は自動的に含まれません。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-107">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="9a7b2-108">`nuget.exe` CLI をインストールします。[nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)からその `.exe`ファイルをダウンロードし、適切なフォルダーに保存して、そのフォルダーを PATH 環境変数に追加してください。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-108">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="9a7b2-109">まだ持っていない場合は、[nuget.org で無料アカウントを登録](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-109">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="9a7b2-110">新しいアカウントを作成すると、確認メールが送信されます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-110">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="9a7b2-111">パッケージをアップロードするには、その前にアカウントを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-111">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="9a7b2-112">クラス ライブラリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="9a7b2-112">Create a class library project</span></span>

<span data-ttu-id="9a7b2-113">パッケージ化するコードに既存の .NET Framework クラス ライブラリ プロジェクトを使用することも、次の手順に従って単純なプロジェクトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-113">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="9a7b2-114">Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、**[Visual C#]** ノードを選択し、"クラス ライブラリ (.NET Framework)" テンプレートを選択し、プロジェクトに AppLogger という名前を付け、**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-114">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="9a7b2-115">作成されたプロジェクト ファイルを右クリックし、**[ビルド]** を選択して、プロジェクトが正しく作成されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-115">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="9a7b2-116">DLL は、デバッグ フォルダー (または代わりにその構成をビルドした場合はリリース フォルダー) 内にあります。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-116">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="9a7b2-117">実際の NuGet パッケージ内ではもちろん、多くの便利な機能を実装し、他のユーザーはそれを使用してアプリケーションをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-117">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="9a7b2-118">また、目的のターゲット フレームワークに設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-118">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="9a7b2-119">例については、[UWP](../guides/create-uwp-packages.md) と [Xamarin](../guides/create-packages-for-xamarin.md) のガイドを参照してください。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-119">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="9a7b2-120">しかし、このチュートリアルでは、パッケージを作成するには、テンプレートのクラス ライブラリで十分なため、追加のコードを記述することはありません。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="9a7b2-121">それでも、パッケージの一部の機能コードが必要な場合は、次のように使用します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-121">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
using System;

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
> <span data-ttu-id="9a7b2-122">それ以外を選択する理由がない限り、.NET Standard は最も広い範囲の使用プロジェクトとの互換性を提供するため、NuGet パッケージの優先ターゲットです。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="9a7b2-123">「[Visual Studio を使用したパッケージの作成と公開 (.NET Standard)](create-and-publish-a-package-using-visual-studio.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-123">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="9a7b2-124">パッケージのプロジェクト プロパティを構成する</span><span class="sxs-lookup"><span data-stu-id="9a7b2-124">Configure project properties for the package</span></span>

<span data-ttu-id="9a7b2-125">NuGet パッケージには、パッケージ識別子、バージョン番号、説明などの関連するメタデータを含むマニフェスト (`.nuspec` ファイル) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-125">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="9a7b2-126">これらの一部は、プロジェクトのプロパティから直接引き出すことができるので、プロジェクトとマニフェストの両方で個別に更新する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-126">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="9a7b2-127">このセクションでは、適用可能なプロパティを設定する場所について説明します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-127">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="9a7b2-128">**[プロジェクト]、[プロパティ]** メニュー コマンドの順に選択し、**[アプリケーション]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-128">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="9a7b2-129">**[アセンブリ名]** フィールドで、パッケージに一意の識別子を付けます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-129">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="9a7b2-130">パッケージには、nuget.org または使用しているホスト全体で一意の識別子を付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="9a7b2-131">このチュートリアルでは、以降の公開手順でパッケージを一般公開するので (ただし、誰かが実際に使用する可能性はありません)、名前に "Sample" または "Test" を含めることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="9a7b2-132">既に存在する名前のパッケージを公開しようとすると、エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="9a7b2-133">**[アセンブリ情報]** ボタンを選択すると、マニフェストに含める他のプロパティを入力するためのダイアログ ボックスが表示されます ([.nuspec ファイル リファレンスの置換トークン](../reference/nuspec.md#replacement-tokens)に関するセクションを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-133">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="9a7b2-134">最もよく使用されるフィールドは、**[タイトル]**、**[説明]**、**[会社名]**、**[著作権]**、**[アセンブリ バージョン]** です。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-134">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="9a7b2-135">これらのプロパティは、最終的に nuget.org のようなホスト上でパッケージと共に表示されるので、わかりやすい値を設定してください。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-135">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Visual Studio の .NET Framework プロジェクトのアセンブリ情報](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="9a7b2-137">省略可能: プロパティを直接表示および編集するには、プロジェクトの `Properties/AssemblyInfo.cs` ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-137">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="9a7b2-138">プロパティが設定されたら、プロジェクトの構成を**リリース**に設定し、プロジェクトをリビルドして、更新された DLL を生成します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-138">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="9a7b2-139">初期マニフェストを生成する</span><span class="sxs-lookup"><span data-stu-id="9a7b2-139">Generate the initial manifest</span></span>

<span data-ttu-id="9a7b2-140">DLL を入手し、プロジェクトのプロパティを設定したら、`nuget spec` コマンドを使用してプロジェクトから最初の `.nuspec` ファイルを生成します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-140">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="9a7b2-141">この手順には、プロジェクト ファイルから情報を引き出すための関連する置換トークンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-141">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="9a7b2-142">`nuget spec` を 1 回のみ実行して最初のマニフェストを生成します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-142">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="9a7b2-143">パッケージを更新するときは、プロジェクトの値を変更するか、マニフェストを直接編集します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-143">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="9a7b2-144">コマンド プロンプトを開き、`AppLogger.csproj` ファイルが格納されているプロジェクト フォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-144">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="9a7b2-145">次のコマンドを実行します: `nuget spec AppLogger.csproj`</span><span class="sxs-lookup"><span data-stu-id="9a7b2-145">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="9a7b2-146">プロジェクトを指定すると、NuGet でプロジェクトの名前 (この場合は `AppLogger.nuspec`) と一致するマニフェストが作成されます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-146">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="9a7b2-147">マニフェストには置換トークンも含まれます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-147">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="9a7b2-148">テキスト エディターで `AppLogger.nuspec` を開き、内容を確認します。内容は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-148">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="9a7b2-149">マニフェストを編集する</span><span class="sxs-lookup"><span data-stu-id="9a7b2-149">Edit the manifest</span></span>

1. <span data-ttu-id="9a7b2-150">`.nuspec` ファイルで既定値のパッケージを作成しようとすると NuGet でエラーが発生するため、次のフィールドを編集して続行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-150">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="9a7b2-151">これらの使用方法については、[.nuspec ファイル リファレンスの単一要素](../reference/nuspec.md#single-elements)に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-151">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="9a7b2-152">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="9a7b2-152">licenseUrl</span></span>
    - <span data-ttu-id="9a7b2-153">projectUrl</span><span class="sxs-lookup"><span data-stu-id="9a7b2-153">projectUrl</span></span>
    - <span data-ttu-id="9a7b2-154">iconUrl</span><span class="sxs-lookup"><span data-stu-id="9a7b2-154">iconUrl</span></span>
    - <span data-ttu-id="9a7b2-155">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="9a7b2-155">releaseNotes</span></span>
    - <span data-ttu-id="9a7b2-156">タグ</span><span class="sxs-lookup"><span data-stu-id="9a7b2-156">tags</span></span>

1. <span data-ttu-id="9a7b2-157">公開用にビルドされたパッケージの場合は、**Tags** プロパティに特に注意してください。これらのタグは nuget.org などのソースで他のユーザーがパッケージを検索して、パッケージの動作を理解する場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-157">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="9a7b2-158">[.nuspec ファイル リファレンス](../reference/nuspec.md)で説明されているように、この時点で他の要素をマニフェストに追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-158">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="9a7b2-159">続行する前にファイルを保存してください。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-159">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="9a7b2-160">pack コマンドを実行する</span><span class="sxs-lookup"><span data-stu-id="9a7b2-160">Run the pack command</span></span>

1. <span data-ttu-id="9a7b2-161">`.nuspec` ファイルを含むフォルダーのコマンド プロンプトから、コマンド `nuget pack` を実行します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-161">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="9a7b2-162">NuGet で、現在のフォルダー内に *identifier-version.nupkg* の形式で `.nupkg` ファイルが生成されます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-162">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="9a7b2-163">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="9a7b2-163">Publish the package</span></span>

<span data-ttu-id="9a7b2-164">`.nupkg` ファイルを作成したら、`nuget.exe` と、nuget.org から取得した API キーを使用して、そのファイルを nuget.org に公開します。nuget.org の場合は、`nuget.exe` 4.1.0 以降を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-164">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="9a7b2-165">API キーを取得する</span><span class="sxs-lookup"><span data-stu-id="9a7b2-165">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="9a7b2-166">nuget push を使用して公開する</span><span class="sxs-lookup"><span data-stu-id="9a7b2-166">Publish with nuget push</span></span>

1. <span data-ttu-id="9a7b2-167">`.nupkg` ファイルを含むフォルダーに変更します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-167">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="9a7b2-168">次のコマンドでパッケージ名を指定し、キーを API キーに置き換えて、コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-168">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="9a7b2-169">nuget.exe によって公開プロセスの結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="9a7b2-170">[nuget push](../tools/cli-ref-push.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="9a7b2-170">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="9a7b2-171">公開エラー</span><span class="sxs-lookup"><span data-stu-id="9a7b2-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="9a7b2-172">公開済みパッケージを管理する</span><span class="sxs-lookup"><span data-stu-id="9a7b2-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="9a7b2-173">関連トピック</span><span class="sxs-lookup"><span data-stu-id="9a7b2-173">Related topics</span></span>

- [<span data-ttu-id="9a7b2-174">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="9a7b2-174">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="9a7b2-175">パッケージの公開</span><span class="sxs-lookup"><span data-stu-id="9a7b2-175">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="9a7b2-176">プレリリース パッケージ</span><span class="sxs-lookup"><span data-stu-id="9a7b2-176">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="9a7b2-177">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="9a7b2-177">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9a7b2-178">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="9a7b2-178">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9a7b2-179">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="9a7b2-179">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
