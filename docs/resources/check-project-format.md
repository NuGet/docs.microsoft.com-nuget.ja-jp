---
title: プロジェクトの形式を特定する
description: プロジェクトの形式を特定する方法について説明します
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843444"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="3107c-103">プロジェクトの形式を特定する</span><span class="sxs-lookup"><span data-stu-id="3107c-103">Identify the project format</span></span>

<span data-ttu-id="3107c-104">NuGet はすべての .NET プロジェクトに対応しています。</span><span class="sxs-lookup"><span data-stu-id="3107c-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="3107c-105">ただし、NuGet パッケージの使用と作成のために使う必要がある一部のツールと方法は、プロジェクトの形式 (SDK スタイルまたは非 SDK スタイル) によって決まります。</span><span class="sxs-lookup"><span data-stu-id="3107c-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="3107c-106">SDK スタイルのプロジェクトでは、[SDK 属性](/dotnet/core/tools/csproj#additions)が使用されます。</span><span class="sxs-lookup"><span data-stu-id="3107c-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="3107c-107">NuGet パッケージの使用と作成のために使う方法とツールは、プロジェクトの形式によって異なるため、ご自分のプロジェクトの種類を特定することが重要です。</span><span class="sxs-lookup"><span data-stu-id="3107c-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="3107c-108">非 SDK スタイルのプロジェクトの場合、その方法とツールは、そのプロジェクトが `PackageReference` 形式に移行されているかどうかにも依存します。</span><span class="sxs-lookup"><span data-stu-id="3107c-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="3107c-109">ご自分のプロジェクトが SDK スタイルであるかどうかは、そのプロジェクトの作成に使用した方法によって異なります。</span><span class="sxs-lookup"><span data-stu-id="3107c-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="3107c-110">次の表は、Visual Studio 2017 以降のバージョンを使ってプロジェクトを作成した場合の、プロジェクトの既定の形式と、関連付けられている CLI ツールを示しています。</span><span class="sxs-lookup"><span data-stu-id="3107c-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="3107c-111">プロジェクト&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="3107c-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="3107c-112">プロジェクトの既定の形式</span><span class="sxs-lookup"><span data-stu-id="3107c-112">Default project format</span></span> | <span data-ttu-id="3107c-113">CLI ツール&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="3107c-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="3107c-114">メモ</span><span class="sxs-lookup"><span data-stu-id="3107c-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="3107c-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="3107c-115">.NET Standard</span></span> | <span data-ttu-id="3107c-116">SDK スタイル</span><span class="sxs-lookup"><span data-stu-id="3107c-116">SDK-style</span></span> | [<span data-ttu-id="3107c-117">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="3107c-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="3107c-118">Visual Studio 2017 より前に作成されたプロジェクトは SDK 形式ではありません。</span><span class="sxs-lookup"><span data-stu-id="3107c-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="3107c-119">`nuget.exe` CLI をお使いください。</span><span class="sxs-lookup"><span data-stu-id="3107c-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="3107c-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3107c-120">.NET Core</span></span> | <span data-ttu-id="3107c-121">SDK スタイル</span><span class="sxs-lookup"><span data-stu-id="3107c-121">SDK-style</span></span> | [<span data-ttu-id="3107c-122">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="3107c-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="3107c-123">Visual Studio 2017 より前に作成されたプロジェクトは SDK 形式ではありません。</span><span class="sxs-lookup"><span data-stu-id="3107c-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="3107c-124">`nuget.exe` CLI をお使いください。</span><span class="sxs-lookup"><span data-stu-id="3107c-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="3107c-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3107c-125">.NET Framework</span></span> | <span data-ttu-id="3107c-126">非 SDK スタイル</span><span class="sxs-lookup"><span data-stu-id="3107c-126">Non-SDK-style</span></span> | [<span data-ttu-id="3107c-127">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="3107c-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="3107c-128">他の方法で作成された .NET Framework プロジェクトは、SDK スタイルのプロジェクトである場合があります。</span><span class="sxs-lookup"><span data-stu-id="3107c-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="3107c-129">そのような場合は、代わりに [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) をお使いください。</span><span class="sxs-lookup"><span data-stu-id="3107c-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="3107c-130">[移行した](../reference/migrate-packages-config-to-package-reference.md) .NET プロジェクト</span><span class="sxs-lookup"><span data-stu-id="3107c-130">[Migrated](../reference/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="3107c-131">非 SDK スタイル</span><span class="sxs-lookup"><span data-stu-id="3107c-131">Non-SDK-style</span></span>| <span data-ttu-id="3107c-132">パッケージを作成する場合は、[msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) を使ってパッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="3107c-132">To create packages, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="3107c-133">パッケージを作成する場合は、`msbuild -t:pack` をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3107c-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="3107c-134">それ以外の場合は、[dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) をお使いください。</span><span class="sxs-lookup"><span data-stu-id="3107c-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="3107c-135">移行されたプロジェクトは、SDK スタイルのプロジェクトではありません。</span><span class="sxs-lookup"><span data-stu-id="3107c-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="3107c-136">プロジェクトの形式を確認する</span><span class="sxs-lookup"><span data-stu-id="3107c-136">Check the project format</span></span>

<span data-ttu-id="3107c-137">プロジェクトが SDK スタイルの形式であるかどうかがわからない場合は、プロジェクト ファイル (C# の場合は \*.csproj ファイル) の `<Project>` 要素で SDK 属性を探します。</span><span class="sxs-lookup"><span data-stu-id="3107c-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="3107c-138">これが存在する場合、そのプロジェクトは SDK スタイルのプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="3107c-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="3107c-139">Visual Studio でプロジェクトの形式を確認する</span><span class="sxs-lookup"><span data-stu-id="3107c-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="3107c-140">Visual Studio で作業している場合は、次のいずれかの方法を使用して、プロジェクトの形式をすばやく確認できます。</span><span class="sxs-lookup"><span data-stu-id="3107c-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="3107c-141">ソリューション エクスプローラーでプロジェクトを右クリックし、 **[<プロジェクト名>.csproj の編集]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3107c-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="3107c-142">このオプションは、Visual Studio 2017 以降で、SDK スタイルの属性を使用するプロジェクトに対してのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="3107c-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="3107c-143">それ以外の場合は、他の方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="3107c-143">Otherwise, use the other method.</span></span>

   ![プロジェクト ファイルを編集する](media/edit-project-file.png)

   <span data-ttu-id="3107c-145">SDK スタイルのプロジェクトのプロジェクト ファイルには、[SDK 属性](/dotnet/core/tools/csproj#additions)が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3107c-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="3107c-146">**[プロジェクト]** メニューから、 **[プロジェクトのアンロード]** を選択します (または、プロジェクトを右クリックして、 **[プロジェクトのアンロード]** を選択します)。</span><span class="sxs-lookup"><span data-stu-id="3107c-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="3107c-147">このプロジェクトのプロジェクト ファイルには、SDK 属性が含まれません。</span><span class="sxs-lookup"><span data-stu-id="3107c-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="3107c-148">これは SDK 形式のプロジェクトではありません。</span><span class="sxs-lookup"><span data-stu-id="3107c-148">It is not an SDK-style project.</span></span>

   ![プロジェクトのアンロード](media/unload-project.png)

   <span data-ttu-id="3107c-150">次に、アンロードされたプロジェクトを右クリックし、 **[<プロジェクト名>.csproj の編集]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3107c-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="3107c-151">関連項目</span><span class="sxs-lookup"><span data-stu-id="3107c-151">See also</span></span>

- [<span data-ttu-id="3107c-152">dotnet CLI を使用して .NET Standard パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="3107c-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="3107c-153">Visual Studio で .NET Standard パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="3107c-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="3107c-154">.NET Framework パッケージの作成と公開 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3107c-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="3107c-155">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="3107c-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
