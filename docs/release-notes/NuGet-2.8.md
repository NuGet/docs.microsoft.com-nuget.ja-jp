---
title: NuGet 2.8 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.8 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547460"
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="1cce9-103">NuGet 2.8 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="1cce9-103">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="1cce9-104">[NuGet 2.7.2 リリース ノート](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 のリリース ノート](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="1cce9-104">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="1cce9-105">NuGet 2.8 は、2014 年 1 月 29 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="1cce9-105">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="1cce9-106">謝辞</span><span class="sxs-lookup"><span data-stu-id="1cce9-106">Acknowledgements</span></span>

1. <span data-ttu-id="1cce9-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span><span class="sxs-lookup"><span data-stu-id="1cce9-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="1cce9-108">[#3466](https://nuget.codeplex.com/workitem/3466) - パッケージの依存関係パッケージの Id を確認しています。</span><span class="sxs-lookup"><span data-stu-id="1cce9-108">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
2. <span data-ttu-id="1cce9-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span><span class="sxs-lookup"><span data-stu-id="1cce9-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="1cce9-110">[#2379](https://nuget.codeplex.com/workitem/2379) -persistening フィードの資格情報には、$metadata サフィックスを削除します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-110">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
3. <span data-ttu-id="1cce9-111">[Filip De の](https://www.codeplex.com/site/users/view/FilipDeVos)([@foxtricks](https://twitter.com/foxtricks))</span><span class="sxs-lookup"><span data-stu-id="1cce9-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="1cce9-112">[#3538](http://nuget.codeplex.com/workitem/3538) - nuget.exe の update コマンド用のプロジェクト ファイルの指定をサポートします。</span><span class="sxs-lookup"><span data-stu-id="1cce9-112">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
4. [<span data-ttu-id="1cce9-113">Juan Gonzalez</span><span class="sxs-lookup"><span data-stu-id="1cce9-113">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="1cce9-114">[#3536](http://nuget.codeplex.com/workitem/3536) -- IncludeReferencedProjects と共に渡すできません置換トークン。</span><span class="sxs-lookup"><span data-stu-id="1cce9-114">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
5. <span data-ttu-id="1cce9-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span><span class="sxs-lookup"><span data-stu-id="1cce9-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="1cce9-116">[#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget.push 大きなパッケージをプッシュするときは、OutOfMemoryException をスローします。</span><span class="sxs-lookup"><span data-stu-id="1cce9-116">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
6. [<span data-ttu-id="1cce9-117">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="1cce9-117">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="1cce9-118">[#3666](http://nuget.codeplex.com/workitem/3666) -プロジェクトが別の CLI と C++ プロジェクトを参照するときの修正プログラムのターゲットが正しくないパス。</span><span class="sxs-lookup"><span data-stu-id="1cce9-118">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
7. <span data-ttu-id="1cce9-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="1cce9-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="1cce9-120">[#3639](https://nuget.codeplex.com/workitem/3639) -既定では開発依存関係としてインストールするパッケージを許可します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-120">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
8. <span data-ttu-id="1cce9-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="1cce9-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="1cce9-122">[#3717](https://nuget.codeplex.com/workitem/3717) -最新のパッチ バージョンへの暗黙的なアップグレードの削除</span><span class="sxs-lookup"><span data-stu-id="1cce9-122">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
9. [<span data-ttu-id="1cce9-123">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="1cce9-123">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="1cce9-124">いくつかのバグ修正と改善 NuGet.Server、nuget.exe ミラー コマンド、およびその他のユーザー。</span><span class="sxs-lookup"><span data-stu-id="1cce9-124">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="1cce9-125">この作業は、数か月間、2.8 のマスターに統合する適切なタイミングで協力 Gregory で行われました。</span><span class="sxs-lookup"><span data-stu-id="1cce9-125">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="1cce9-126">依存関係の修正プログラムの解決</span><span class="sxs-lookup"><span data-stu-id="1cce9-126">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="1cce9-127">パッケージの依存関係を解決するときに NuGet は従来のパッケージの依存関係を満たす最下位のメジャーおよびマイナーのパッケージ バージョンを選択する戦略を実装しました。</span><span class="sxs-lookup"><span data-stu-id="1cce9-127">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="1cce9-128">メジャーおよびマイナーのバージョンとは異なり、修正プログラムのバージョン常に解決された最上位のバージョンを。</span><span class="sxs-lookup"><span data-stu-id="1cce9-128">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="1cce9-129">動作は、理由の 1 つが、依存関係を持つパッケージをインストールするための決定性の欠如が作成されます。</span><span class="sxs-lookup"><span data-stu-id="1cce9-129">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="1cce9-130">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-130">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="1cce9-131">この例では、たとえ Developer1 と Developer2 インストールPackageA@1.0.0PackageB の別のバージョンをそれぞれに終了しました。</span><span class="sxs-lookup"><span data-stu-id="1cce9-131">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="1cce9-132">NuGet 2.8 では、修正プログラムのバージョンの依存関係の解決の動作は、メジャーおよびマイナーのバージョンの動作と一致するようにこの既定の動作が変わります。</span><span class="sxs-lookup"><span data-stu-id="1cce9-132">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="1cce9-133">次に、上記の例でPackageB@1.0.0をインストールすると、インストールPackageA@1.0.0新しいパッチ バージョンに関係なく、します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-133">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="1cce9-134">-DependencyVersion スイッチ</span><span class="sxs-lookup"><span data-stu-id="1cce9-134">-DependencyVersion Switch</span></span>

<span data-ttu-id="1cce9-135">NuGet 2.8 の変更が、_既定_動作の依存関係を解決するためも追加されます。 これに DependencyVersion スイッチを使用して依存関係解決プロセスをより細かく制御パッケージ マネージャー コンソール。</span><span class="sxs-lookup"><span data-stu-id="1cce9-135">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="1cce9-136">スイッチは、最下位の可能なバージョン (既定の動作)、最高の可能なバージョンや最上位のマイナーまたは修正プログラムのバージョンに依存関係を解決できます。</span><span class="sxs-lookup"><span data-stu-id="1cce9-136">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="1cce9-137">このスイッチは、powershell コマンドでインストール パッケージにのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-137">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion スイッチ](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="1cce9-139">DependencyVersion 属性</span><span class="sxs-lookup"><span data-stu-id="1cce9-139">DependencyVersion Attribute</span></span>

<span data-ttu-id="1cce9-140">上記の詳細、NuGet が必要なアクセス許可も使用できます。 Nuget.Config ファイルに新しい属性を設定する - DependencyVersion スイッチだけでなくを定義する既定値の呼び出しでは、- DependencyVersion スイッチが指定されていない場合インストール パッケージです。</span><span class="sxs-lookup"><span data-stu-id="1cce9-140">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="1cce9-141">この値は、任意の操作のインストール パッケージを NuGet パッケージ マネージャー ダイアログでも適用されます。</span><span class="sxs-lookup"><span data-stu-id="1cce9-141">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="1cce9-142">この値を設定するには、Nuget.Config ファイルに次の属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-142">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="1cce9-143">-Whatif をプレビュー NuGet の操作</span><span class="sxs-lookup"><span data-stu-id="1cce9-143">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="1cce9-144">NuGet パッケージの一部は、厳密な依存関係のグラフを持つことができ、そのため、そのことができます、インストール中に立つ、アンインストール、または更新操作がまずどうなるかを確認します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-144">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="1cce9-145">NuGet 2.8 は、パッケージのインストール、アンインストール、パッケージ、およびコマンドの適用先となるパッケージのクロージャ全体をビジュアル化を有効にする更新プログラム パッケージのコマンドに標準の PowerShell-whatif スイッチを追加します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-145">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="1cce9-146">たとえば、実行している`install-package Microsoft.AspNet.WebApi -whatif`空の ASP.NET Web アプリケーションには、次が得られます。</span><span class="sxs-lookup"><span data-stu-id="1cce9-146">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a><span data-ttu-id="1cce9-147">パッケージのダウン グレード</span><span class="sxs-lookup"><span data-stu-id="1cce9-147">Downgrade Package</span></span>

<span data-ttu-id="1cce9-148">新しい機能を調査するために、パッケージのプレリリース版をインストールし、最後の安定したバージョンにロールバックすることは珍しくありません。</span><span class="sxs-lookup"><span data-stu-id="1cce9-148">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="1cce9-149">NuGet 2.8、前に、プレリリースのパッケージとその依存関係をアンインストールすると、以前のバージョンをインストールし、複数の手順をしました。</span><span class="sxs-lookup"><span data-stu-id="1cce9-149">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="1cce9-150">NuGet 2.8 でただし、更新プログラム パッケージはようになりました (例: パッケージの依存関係ツリー) 全体のパッケージ クロージャにロールバック以前のバージョン。</span><span class="sxs-lookup"><span data-stu-id="1cce9-150">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="1cce9-151">開発の依存関係</span><span class="sxs-lookup"><span data-stu-id="1cce9-151">Development Dependencies</span></span>

<span data-ttu-id="1cce9-152">さまざまな種類の機能は、開発プロセスを最適化するために使用されるツールを含む - NuGet パッケージとして配信できます。</span><span class="sxs-lookup"><span data-stu-id="1cce9-152">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="1cce9-153">これらのコンポーネントを新しいパッケージの開発に役立つ可能性があるときに見なされない新しいパッケージの依存関係後で発行されているとします。</span><span class="sxs-lookup"><span data-stu-id="1cce9-153">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="1cce9-154">NuGet 2.8 により、パッケージ自体を識別するために、`.nuspec`では developmentDependency としてのファイル。</span><span class="sxs-lookup"><span data-stu-id="1cce9-154">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="1cce9-155">このメタデータに追加することも、インストールされている場合、`packages.config`パッケージがインストールされたプロジェクトのファイル。</span><span class="sxs-lookup"><span data-stu-id="1cce9-155">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="1cce9-156">時を`packages.config`ファイルは後の中に、NuGet の依存関係分析`nuget.exe pack`開発の依存関係としてマークされているこれらの依存関係が除外されます。</span><span class="sxs-lookup"><span data-stu-id="1cce9-156">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="1cce9-157">さまざまなプラットフォーム向けの個々 の packages.config ファイル</span><span class="sxs-lookup"><span data-stu-id="1cce9-157">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="1cce9-158">複数のターゲット プラットフォーム用のアプリケーションを開発する場合は、別のプロジェクト ファイルのそれぞれのビルド環境を持つ一般的なは。</span><span class="sxs-lookup"><span data-stu-id="1cce9-158">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="1cce9-159">パッケージがあるさまざまなレベルのさまざまなプラットフォームのサポートのためにも別のプロジェクト ファイルで別の NuGet パッケージを使用する一般的です。</span><span class="sxs-lookup"><span data-stu-id="1cce9-159">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="1cce9-160">NuGet 2.8 別に作成してこのシナリオのサポートの強化を提供します`packages.config`さまざまなプラットフォーム固有プロジェクト ファイルのファイル。</span><span class="sxs-lookup"><span data-stu-id="1cce9-160">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![複数の package.config ファイル](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="1cce9-162">ローカル キャッシュへのフォールバック</span><span class="sxs-lookup"><span data-stu-id="1cce9-162">Fallback to Local Cache</span></span>

<span data-ttu-id="1cce9-163">NuGet パッケージの通常使用される、リモート ギャラリーからなど、 [NuGet ギャラリー](http://www.nuget.org/)ネットワーク接続を使用して、クライアントが接続されていないシナリオはよくあります。</span><span class="sxs-lookup"><span data-stu-id="1cce9-163">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="1cce9-164">ネットワーク接続を行わず、NuGet クライアントはこれらのパッケージは、ローカル NuGet キャッシュ内で、クライアント コンピューターに存在した場合でもパッケージを正常にインストールできませんでした。</span><span class="sxs-lookup"><span data-stu-id="1cce9-164">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="1cce9-165">NuGet 2.8 は、パッケージ マネージャー コンソールをキャッシュの自動フォールバックを追加します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-165">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="1cce9-166">たとえば、ときに、ネットワーク アダプターを切断して、jQuery をインストールする、コンソール次に示します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-166">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="1cce9-167">キャッシュ フォールバック機能では、特定のコマンド引数は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="1cce9-167">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="1cce9-168">さらに、フォールバックのキャッシュは、現在、パッケージ マネージャー コンソールでのみ機能 - パッケージ マネージャー ダイアログで、動作が現在機能しません。</span><span class="sxs-lookup"><span data-stu-id="1cce9-168">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="1cce9-169">WebMatrix の NuGet クライアントの更新プログラムします。</span><span class="sxs-lookup"><span data-stu-id="1cce9-169">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="1cce9-170">NuGet 2.8、と共に、WebMatrix の NuGet 拡張機能はで提供される主な機能の多くに更新もが[NuGet 2.5](../release-notes/nuget-2.5.md)します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-170">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="1cce9-171">新機能では、' Update All'、' 最小 NuGet バージョン '、およびコンテンツ ファイルの上書きの許可などがあります。</span><span class="sxs-lookup"><span data-stu-id="1cce9-171">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="1cce9-172">WebMatrix 3 で NuGet パッケージ マネージャー拡張機能の更新。</span><span class="sxs-lookup"><span data-stu-id="1cce9-172">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="1cce9-173">WebMatrix 3 を開く</span><span class="sxs-lookup"><span data-stu-id="1cce9-173">Open WebMatrix 3</span></span>
1. <span data-ttu-id="1cce9-174">リボンの拡張機能アイコンをクリックします</span><span class="sxs-lookup"><span data-stu-id="1cce9-174">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="1cce9-175">[更新] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-175">Select the Updates tab</span></span>
1. <span data-ttu-id="1cce9-176">2.5.0 を NuGet パッケージ マネージャーを更新する をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1cce9-176">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="1cce9-177">閉じて再起動 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="1cce9-177">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="1cce9-178">これは、WebMatrix 用の NuGet パッケージ マネージャー拡張機能に NuGet チームの初回リリースです。</span><span class="sxs-lookup"><span data-stu-id="1cce9-178">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="1cce9-179">コードが最近、オープン ソースの NuGet プロジェクトに Microsoft によって提供されました。</span><span class="sxs-lookup"><span data-stu-id="1cce9-179">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="1cce9-180">以前は、WebMatrix に、NuGet は統合が組み込まれているし、WebMatrix から帯域外更新できませんでした。</span><span class="sxs-lookup"><span data-stu-id="1cce9-180">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="1cce9-181">さらに、NuGet のクライアント ツールの残りの部分と共に更新する機能があるようになりました。</span><span class="sxs-lookup"><span data-stu-id="1cce9-181">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="1cce9-182">バグ修正</span><span class="sxs-lookup"><span data-stu-id="1cce9-182">Bug Fixes</span></span>

<span data-ttu-id="1cce9-183">更新プログラム パッケージのパフォーマンスの向上が行われた主要なバグ修正のいずれかのコマンドを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="1cce9-183">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="1cce9-184">NuGet のこのリリースには、これらの機能および上記のパフォーマンスの修正プログラム、に加えて、他の多くのバグ修正も含まれます。</span><span class="sxs-lookup"><span data-stu-id="1cce9-184">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="1cce9-185">リリースで対処された 181 合計問題が発生しました。</span><span class="sxs-lookup"><span data-stu-id="1cce9-185">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="1cce9-186">作業の完全な一覧の項目で修正された NuGet 2.8、くださいビュー、[このリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)します。</span><span class="sxs-lookup"><span data-stu-id="1cce9-186">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
