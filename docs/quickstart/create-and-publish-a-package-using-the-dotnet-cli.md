---
title: dotnet CLI を使用した NuGet パッケージの作成と公開
description: .NET Core CLI (dotnet) を使用した NuGet パッケージの作成と公開に関するチュートリアル。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8727f67608593e6ae8b96daa81b7423782dfc219
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096932"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="865ff-103">クイック スタート: パッケージの作成と公開 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="865ff-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="865ff-104">これは、`dotnet`コマンド ライン インターフェイス (CLI) を使用して、.NET クラス ライブラリから NuGet パッケージを作成し、nuget.org に公開する簡単なプロセスです。</span><span class="sxs-lookup"><span data-stu-id="865ff-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="865ff-105">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="865ff-105">Prerequisites</span></span>

1. <span data-ttu-id="865ff-106">`dotnet` CLI を含む [.NET Core SDK](https://www.microsoft.com/net/download/) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="865ff-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="865ff-107">Visual Studio 2017 以降、dotnet CLI は .NET Core 関連のワークロードで自動的にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="865ff-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="865ff-108">まだ持っていない場合は、[nuget.org で無料アカウントを登録](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)します。</span><span class="sxs-lookup"><span data-stu-id="865ff-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="865ff-109">新しいアカウントを作成すると、確認メールが送信されます。</span><span class="sxs-lookup"><span data-stu-id="865ff-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="865ff-110">パッケージをアップロードするには、その前にアカウントを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="865ff-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="865ff-111">クラス ライブラリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="865ff-111">Create a class library project</span></span>

<span data-ttu-id="865ff-112">パッケージ化するコードに既存の .NET クラス ライブラリ プロジェクトを使用することも、次の手順に従って単純なプロジェクトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="865ff-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="865ff-113">`AppLogger` という名前のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="865ff-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="865ff-114">コマンド プロンプトを開いて、`AppLogger` フォルダーに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="865ff-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="865ff-115">「`dotnet new classlib`」と入力します。ここでは、プロジェクトに現在のフォルダーの名前が使用されます。</span><span class="sxs-lookup"><span data-stu-id="865ff-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="865ff-116">これにより、新しいプロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="865ff-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="865ff-117">パッケージのメタデータをプロジェクト ファイルに追加する</span><span class="sxs-lookup"><span data-stu-id="865ff-117">Add package metadata to the project file</span></span>

<span data-ttu-id="865ff-118">すべての NuGet パッケージには、その内容と依存関係を説明するマニフェストが必要です。</span><span class="sxs-lookup"><span data-stu-id="865ff-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="865ff-119">最終的なパッケージでは、マニフェストは、プロジェクト ファイルに含まれる NuGet メタデータのプロパティから生成される `.nuspec` ファイルです。</span><span class="sxs-lookup"><span data-stu-id="865ff-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="865ff-120">プロジェクト ファイル (`.csproj`) を開いて、既存の `<PropertyGroup>` タグ内に次の最小限のプロパティを追加し、必要に応じて値を変更します。</span><span class="sxs-lookup"><span data-stu-id="865ff-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="865ff-121">パッケージに、nuget.org または使用しているホスト全体で一意の識別子を付けます。</span><span class="sxs-lookup"><span data-stu-id="865ff-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="865ff-122">このチュートリアルでは、以降の公開手順でパッケージを一般公開するので (ただし、誰かが実際に使用する可能性はありません)、名前に "Sample" または "Test" を含めることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="865ff-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="865ff-123">「[NuGet メタデータ プロパティ](/dotnet/core/tools/csproj#nuget-metadata-properties)」で説明する省略可能なプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="865ff-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="865ff-124">公開用にビルドされたパッケージの場合は、**PackageTags**プロパティに特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="865ff-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="865ff-125">pack コマンドを実行する</span><span class="sxs-lookup"><span data-stu-id="865ff-125">Run the pack command</span></span>

<span data-ttu-id="865ff-126">プロジェクトから NuGet パッケージ (`.nupkg` ファイル) を作成するには、`dotnet pack` コマンドを実行します。このコマンドではプロジェクトのビルドも自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="865ff-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="865ff-127">出力に、`.nupkg` ファイルへのパスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="865ff-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="865ff-128">ビルド時に自動的にパッケージを生成する</span><span class="sxs-lookup"><span data-stu-id="865ff-128">Automatically generate package on build</span></span>

<span data-ttu-id="865ff-129">`dotnet build` の実行時に自動的に `dotnet pack` を実行させるには、プロジェクト ファイルの `<PropertyGroup>` 内に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="865ff-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="865ff-130">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="865ff-130">Publish the package</span></span>

<span data-ttu-id="865ff-131">`.nupkg` ファイルを作成したら、`dotnet nuget push` コマンドと、nuget.org から取得した API キーを使用して、そのファイルを nuget.org に公開します。</span><span class="sxs-lookup"><span data-stu-id="865ff-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="865ff-132">API キーを取得する</span><span class="sxs-lookup"><span data-stu-id="865ff-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="865ff-133">dotnet nuget push を使用して公開する</span><span class="sxs-lookup"><span data-stu-id="865ff-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="865ff-134">公開エラー</span><span class="sxs-lookup"><span data-stu-id="865ff-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="865ff-135">公開済みパッケージを管理する</span><span class="sxs-lookup"><span data-stu-id="865ff-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="865ff-136">次の手順</span><span class="sxs-lookup"><span data-stu-id="865ff-136">Next steps</span></span>

<span data-ttu-id="865ff-137">無事に、最初の NuGet パッケージを作成できました。</span><span class="sxs-lookup"><span data-stu-id="865ff-137">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="865ff-138">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="865ff-138">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="865ff-139">NuGet による提供についてさらに詳しく調べるには、下のリンクを選択してください。</span><span class="sxs-lookup"><span data-stu-id="865ff-139">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="865ff-140">パッケージの公開</span><span class="sxs-lookup"><span data-stu-id="865ff-140">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="865ff-141">プレリリース パッケージ</span><span class="sxs-lookup"><span data-stu-id="865ff-141">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="865ff-142">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="865ff-142">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="865ff-143">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="865ff-143">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="865ff-144">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="865ff-144">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="865ff-145">シンボル パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="865ff-145">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="865ff-146">署名パッケージ</span><span class="sxs-lookup"><span data-stu-id="865ff-146">Signing packages</span></span>](../create-packages/Sign-a-package.md)
