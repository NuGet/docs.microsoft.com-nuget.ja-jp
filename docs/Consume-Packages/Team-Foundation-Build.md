---
title: "Team Foundation ビルドでの NuGet パッケージの復元のチュートリアル | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Team Foundation ビルド (TFS と Visual Studio Team Services の両方) で NuGet パッケージを復元する方法について説明します。"
keywords: "NuGet パッケージの復元、NuGet および TFS、NuGet および VSTS、NuGet のビルド システム、team foundation ビルド、カスタム MSBuild プロジェクト、クラウドを構築、継続的インテグレーション"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e3ef6e3bcc55705315fcb6ccf3e917963c62250
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="caf4e-104">Team Foundation ビルドでのパッケージの復元の設定</span><span class="sxs-lookup"><span data-stu-id="caf4e-104">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="caf4e-105">この記事では、Git と Team Services バージョン管理の両方における [Team Services ビルド](/vsts/build-release/index)の一環としてパッケージを復元する方法に関する詳細なチュートリアルを提供します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-105">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="caf4e-106">このチュートリアルは、Visual Studio Team Service の使用のシナリオに固有ですが、概念は他のバージョン管理およびビルドシステムにも適用されます。</span><span class="sxs-lookup"><span data-stu-id="caf4e-106">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="caf4e-107">対象:</span><span class="sxs-lookup"><span data-stu-id="caf4e-107">Applies To:</span></span>

- <span data-ttu-id="caf4e-108">TFS の任意のバージョンで実行されているカスタム MSBuild プロジェクト</span><span class="sxs-lookup"><span data-stu-id="caf4e-108">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="caf4e-109">Team Foundation Server 2012 またはそれ以前</span><span class="sxs-lookup"><span data-stu-id="caf4e-109">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="caf4e-110">TFS 2013 以降に移行されたカスタム Team Foundation ビルド プロセス テンプレート</span><span class="sxs-lookup"><span data-stu-id="caf4e-110">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="caf4e-111">Nuget の復元機能が削除されたビルド プロセス テンプレート</span><span class="sxs-lookup"><span data-stu-id="caf4e-111">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="caf4e-112">ビルド プロセス テンプレートを含む Visual Studio Team Services または Team Foundation Server 2013 を使用している場合は、パッケージの自動復元がビルド プロセスの一環として発生します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-112">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="caf4e-113">一般的な方法</span><span class="sxs-lookup"><span data-stu-id="caf4e-113">The general approach</span></span>

<span data-ttu-id="caf4e-114">NuGet を使用する利点は、バージョン管理システムへのバイナリのチェックインを回避できることです。</span><span class="sxs-lookup"><span data-stu-id="caf4e-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="caf4e-115">これは、git などの[分散バージョン管理](http://en.wikipedia.org/wiki/Distributed_revision_control)システムを使用している場合に特に有効です。これは、開発者が、ローカルで作業を始める前に、完全な履歴を含めた全体のリポジトリを複製する必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="caf4e-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="caf4e-116">バイナリ ファイルは一般的に差分圧縮なしで保存されるので、バイナリ ファイルをチェックインすると、大幅なリポジトリの肥大化を招く可能性があります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="caf4e-117">NuGet は、現在まで長期にわたってビルドの一部としての[パッケージ復元](../consume-packages/package-restore.md)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="caf4e-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="caf4e-118">以前の実装では、NuGet は、プロジェクトのビルド中にパッケージを復元したので、ビルド プロセスを拡張する必要があるパッケージの場合に、卵が先か鶏が先かという問題がありました。</span><span class="sxs-lookup"><span data-stu-id="caf4e-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="caf4e-119">しかし、MSBuild では、ビルド中のビルドの拡張は許可されないので、これは MSBuild の問題だと主張されることがありますが、私はこれが固有の問題であると主張します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="caf4e-120">拡張する必要がある局面によっては、パッケージが復元されるときには登録するのに遅すぎることがあります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="caf4e-121">この問題の解決策として、ビルド プロセスの最初の手順としてパッケージが復元されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-121">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="caf4e-122">ビルド プロセスでコードをビルドする前にパッケージを復元する場合、`.targets` ファイルをチェックインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="caf4e-122">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="caf4e-123">Visual Studio での読み込みを許可するようにパッケージを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-123">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="caf4e-124">そのようになっていない場合、他の開発者も、パッケージを最初に復元しなくともソリューションを単純に開くことができるようにするために、引き続き `.targets` ファイルもチェックインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-124">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="caf4e-125">次のデモ プロジェクトは、`packages` フォルダーと `.targets` ファイルをチェックインする必要がないような方法でビルドを設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="caf4e-125">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="caf4e-126">このサンプル プロジェクト用の Team Foundation Service で自動ビルドを設定する方法も示しています。</span><span class="sxs-lookup"><span data-stu-id="caf4e-126">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="caf4e-127">リポジトリの構造</span><span class="sxs-lookup"><span data-stu-id="caf4e-127">Repository structure</span></span>

<span data-ttu-id="caf4e-128">デモのプロジェクトは、Bing のクエリにコマンドライン引数を使用しているシンプルなコマンド ライン ツールです。</span><span class="sxs-lookup"><span data-stu-id="caf4e-128">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="caf4e-129">.NET Framework 4 を対象とし、多くの [BCL パッケージ](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http)、[Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl)、[Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async)、[Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)) を使用しています。</span><span class="sxs-lookup"><span data-stu-id="caf4e-129">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="caf4e-130">リポジトリの構造は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-130">The structure of the repository looks as follows:</span></span>

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

<span data-ttu-id="caf4e-131">`packages` フォルダーも、どの `.targets` ファイルもチェックインしていないことがわかります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-131">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="caf4e-132">ただし、`nuget.exe` はビルド時に必要なのでチェックインしました。</span><span class="sxs-lookup"><span data-stu-id="caf4e-132">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="caf4e-133">広く使用されている規則に従って、共有 `tools` フォルダーの下にチェックインしました。</span><span class="sxs-lookup"><span data-stu-id="caf4e-133">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="caf4e-134">ソース コードは `src` フォルダーの下にあります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-134">The source code is under the `src` folder.</span></span> <span data-ttu-id="caf4e-135">このデモでは、1 つのソリューションのみを使用しますが、このフォルダーに複数のソリューションが含まれていることは容易に想像できます。</span><span class="sxs-lookup"><span data-stu-id="caf4e-135">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="caf4e-136">ファイルを無視</span><span class="sxs-lookup"><span data-stu-id="caf4e-136">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="caf4e-137">現在、[NuGet クライアントに既知のバグ](https://nuget.codeplex.com/workitem/4072)があり、そのためにクライアントが依然として `packages` フォルダーをバージョン管理に追加します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-137">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="caf4e-138">回避策は、ソース管理の統合を無効にすることです。</span><span class="sxs-lookup"><span data-stu-id="caf4e-138">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="caf4e-139">そのためには、ソリューションと並列な `.nuget` フォルダーに `Nuget.Config ` ファイルが必要です。</span><span class="sxs-lookup"><span data-stu-id="caf4e-139">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="caf4e-140">このフォルダーがまだ存在しない場合は、それを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-140">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="caf4e-141">[`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) に次のコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-141">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="caf4e-142">**packages** フォルダーをチェックインしないことをバージョン管理に伝達するために、git (`.gitignore`) および TF バージョン管理 (`.tfignore`) の両方の無視ファイルも追加しました。</span><span class="sxs-lookup"><span data-stu-id="caf4e-142">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="caf4e-143">これらのファイルは、チェックインしたくないファイルのパターンについて記述します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-143">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="caf4e-144">`.gitignore` ファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-144">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages

<span data-ttu-id="caf4e-145">`.gitignore` ファイルは[非常に強力](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html)です。</span><span class="sxs-lookup"><span data-stu-id="caf4e-145">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="caf4e-146">たとえば、`packages` フォルダーの内容を一般的にチェックインしなくとも、`.targets` ファイルのチェックインに関する前のガイドに従う場合、代わりに次のコマンドを使用できます。</span><span class="sxs-lookup"><span data-stu-id="caf4e-146">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="caf4e-147">これはすべての `packages` フォルダーを除外しますが、すべての含まれる `.targets` ファイルを再び含めます。</span><span class="sxs-lookup"><span data-stu-id="caf4e-147">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="caf4e-148">ところで、Visual Studio 開発者のニーズに合わせて特別にカスタマイズされた `.gitignore` ファイルのテンプレートを[ここ](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)で見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="caf4e-148">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="caf4e-149">TF バージョン管理は、[.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) ファイルを使用してよく似たメカニズムをサポートします。</span><span class="sxs-lookup"><span data-stu-id="caf4e-149">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="caf4e-150">構文はほぼ同じです。</span><span class="sxs-lookup"><span data-stu-id="caf4e-150">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages

## <a name="buildproj"></a><span data-ttu-id="caf4e-151">build.proj</span><span class="sxs-lookup"><span data-stu-id="caf4e-151">build.proj</span></span>

<span data-ttu-id="caf4e-152">このデモでは、非常にシンプルなビルド プロセスを維持しています。</span><span class="sxs-lookup"><span data-stu-id="caf4e-152">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="caf4e-153">ソリューションをビルドする前にパッケージを復元することを確認しながらすべてのソリューションをビルドする MSBuild プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-153">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="caf4e-154">このプロジェクトには、従来の 3 つのターゲット `Clean`、`Build`、`Rebuild` だけでなく、新しいターゲット `RestorePackages` があります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-154">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="caf4e-155">`Build` と `Rebuild` のターゲットはどちらも `RestorePackages` に依存します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-155">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="caf4e-156">これにより、`Build` と `Rebuild` の両方を実行できることを確認し、パッケージが復元されていることに依存できます。</span><span class="sxs-lookup"><span data-stu-id="caf4e-156">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="caf4e-157">`Clean`、`Build`、および `Rebuild` は、すべてソリューション ファイルの対応する MSBuild ターゲットを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-157">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="caf4e-158">`RestorePackages` ターゲットは、各ソリューション ファイルの `nuget.exe` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-158">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="caf4e-159">これは、[MSBuild のバッチ機能](/visualstudio/msbuild/msbuild-batching)を使用して実行されます。</span><span class="sxs-lookup"><span data-stu-id="caf4e-159">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="caf4e-160">この結果は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-160">The result looks as follows:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a><span data-ttu-id="caf4e-161">チーム ビルドを構成する</span><span class="sxs-lookup"><span data-stu-id="caf4e-161">Configuring Team Build</span></span>

<span data-ttu-id="caf4e-162">チーム ビルドは、さまざまなプロセス テンプレートを提供します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-162">Team Build offers various process templates.</span></span> <span data-ttu-id="caf4e-163">このデモでは、Team Foundation Service を使用しています。</span><span class="sxs-lookup"><span data-stu-id="caf4e-163">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="caf4e-164">TFS のオンプレミス インストールはよく似ています。</span><span class="sxs-lookup"><span data-stu-id="caf4e-164">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="caf4e-165">Git および TF バージョン管理には異なるチーム ビルド テンプレートがあるので、次の手順は、使用しているバージョン管理システムによって異なります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-165">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="caf4e-166">どちらの場合でも、必要なのは、ビルドするプロジェクトとして build.proj を選択することだけです。</span><span class="sxs-lookup"><span data-stu-id="caf4e-166">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="caf4e-167">最初に、git のプロセス テンプレートを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="caf4e-167">First, let's look at the process template for git.</span></span> <span data-ttu-id="caf4e-168">git ベースのテンプレートで、プロパティ `Solution to build` を介してビルドが選択されています。</span><span class="sxs-lookup"><span data-stu-id="caf4e-168">In the git based template the build is selected via the property `Solution to build`:</span></span>

![git のビルド プロセス](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="caf4e-170">このプロパティは、リポジトリ内の場所であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="caf4e-170">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="caf4e-171">`build.proj` はルートにあるので、単純に `build.proj` を使用します。</span><span class="sxs-lookup"><span data-stu-id="caf4e-171">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="caf4e-172">ビルド ファイルを `tools` というフォルダーの下に置いた場合、値は `tools\build.proj` になります。</span><span class="sxs-lookup"><span data-stu-id="caf4e-172">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="caf4e-173">TF バージョン管理テンプレートでは、プロパティ `Projects` を介してプロジェクトが選択されます。</span><span class="sxs-lookup"><span data-stu-id="caf4e-173">In the TF version control template the project is selected via the property `Projects`:</span></span>

![TFVC のビルド プロセス](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="caf4e-175">Git ベースのテンプレートとは対照的に、TF バージョン管理は、ピッカー (右側にある 3 つのドット付きのボタン) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="caf4e-175">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="caf4e-176">したがって、入力エラーを回避するために、それらを使用してプロジェクトを選択することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="caf4e-176">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
