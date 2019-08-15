---
title: dotnet CLI を使用して NuGet パッケージをインストールし、管理する
description: dotnet CLI を使用して NuGet パッケージを操作する方法。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: d9e9f0026e4c907351b4b0cd0adced28a4670575
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860596"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="1b061-103">dotnet CLI を使用してパッケージをインストールして管理する</span><span class="sxs-lookup"><span data-stu-id="1b061-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="1b061-104">CLI ツールを使用すると、プロジェクトやソリューションで NuGet パッケージを簡単にインストール、アンインストール、更新できます。</span><span class="sxs-lookup"><span data-stu-id="1b061-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="1b061-105">Windows、Mac OS X、Linux で実行されます。</span><span class="sxs-lookup"><span data-stu-id="1b061-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="1b061-106">dotnet CLI は .NET Core や .NET Standard のプロジェクト (SDK スタイルのプロジェクト タイプ) で使用され、また、その他の SDK スタイル プロジェクト (.NET Framework を対象とする SDK スタイルのプロジェクト) で使用されます。</span><span class="sxs-lookup"><span data-stu-id="1b061-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="1b061-107">詳細については、「[SDK 属性](/dotnet/core/tools/csproj#additions)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1b061-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="1b061-108">この記事では、最も一般的ないくつかの dotnet CLI コマンドの基本的な使用方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="1b061-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="1b061-109">これらのコマンドの多くでは、コマンドにプロジェクト ファイルが指定されていない限り、CLI ツールは現在のディレクトリでプロジェクト ファイルを探します (プロジェクト ファイルはオプションのスイッチです)。</span><span class="sxs-lookup"><span data-stu-id="1b061-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="1b061-110">コマンドと使用できる引数の完全一覧については、[.NET Core コマンドライン インターフェイス (CLI) ツール](../reference/dotnet-commands.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="1b061-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b061-111">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="1b061-111">Prerequisites</span></span>

- <span data-ttu-id="1b061-112">[.NET Core SDK](https://www.microsoft.com/net/download/)。これは、`dotnet`コマンド ライン ツールを提供します。</span><span class="sxs-lookup"><span data-stu-id="1b061-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="1b061-113">Visual Studio 2017 以降、dotnet CLI は .NET Core 関連のワークロードで自動的にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="1b061-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="1b061-114">パッケージをインストールします</span><span class="sxs-lookup"><span data-stu-id="1b061-114">Install a package</span></span>

<span data-ttu-id="1b061-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) では、パッケージ参照がプロジェクト ファイルに追加され、`dotnet restore` が実行されてパッケージがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="1b061-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="1b061-116">コマンド ラインを開き、プロジェクト ファイルが含まれるディレクトリに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="1b061-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="1b061-117">次のコマンドを使用して、NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="1b061-117">Use the following command to install a Nuget package:</span></span>

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="1b061-118">たとえば、`Newtonsoft.Json` パッケージをインストールするには、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="1b061-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="1b061-119">コマンドが完了したら、プロジェクト ファイルを見て、パッケージがインストールされたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="1b061-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="1b061-120">`.csproj` ファイルを開くと、追加された参照を確認できます。</span><span class="sxs-lookup"><span data-stu-id="1b061-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="1b061-121">パッケージの特定のバージョンをインストールする</span><span class="sxs-lookup"><span data-stu-id="1b061-121">Install a specific version of a package</span></span>

<span data-ttu-id="1b061-122">バージョンが指定されていない場合、NuGet では最新版のパッケージがインストールされまする</span><span class="sxs-lookup"><span data-stu-id="1b061-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="1b061-123">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) コマンドを使用し、特定のバージョンの NuGet パッケージをインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="1b061-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="1b061-124">たとえば、`Newtonsoft.Json` パッケージのバージョン 12.0.1 を追加するには、このコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="1b061-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="1b061-125">パッケージ参照の一覧表示</span><span class="sxs-lookup"><span data-stu-id="1b061-125">List package references</span></span>

<span data-ttu-id="1b061-126">[dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) コマンドを使用し、プロジェクトのパッケージ参照を一覧表示できます。</span><span class="sxs-lookup"><span data-stu-id="1b061-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```cli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="1b061-127">パッケージを削除する</span><span class="sxs-lookup"><span data-stu-id="1b061-127">Remove a package</span></span>

<span data-ttu-id="1b061-128">プロジェクト ファイルからパッケージ参照を削除するには、[dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) コマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="1b061-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```cli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="1b061-129">たとえば、`Newtonsoft.Json` パッケージを削除するには、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="1b061-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="1b061-130">パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="1b061-130">Update a package</span></span>

<span data-ttu-id="1b061-131">NuGet では、パッケージ バージョンを指定しない限り (`-v` スイッチ)、`dotnet add package` コマンドの使用時、最新版のパッケージがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="1b061-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="1b061-132">パッケージの復元</span><span class="sxs-lookup"><span data-stu-id="1b061-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
