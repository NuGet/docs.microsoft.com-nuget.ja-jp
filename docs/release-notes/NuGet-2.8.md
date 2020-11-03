---
title: NuGet 2.8 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.8 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237026"
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="7cfd7-103">NuGet 2.8 リリースノート</span><span class="sxs-lookup"><span data-stu-id="7cfd7-103">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="7cfd7-104">[NuGet 2.7.2 のリリースノート](../release-notes/nuget-2.7.2.md)  | [NuGet 2.8.1 のリリースノート](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="7cfd7-104">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="7cfd7-105">NuGet 2.8 は、2014年1月29日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-105">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="7cfd7-106">謝辞</span><span class="sxs-lookup"><span data-stu-id="7cfd7-106">Acknowledgements</span></span>

1. <span data-ttu-id="7cfd7-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ( [@leppie](https://twitter.com/leppie) )</span><span class="sxs-lookup"><span data-stu-id="7cfd7-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="7cfd7-108">[#3466](https://nuget.codeplex.com/workitem/3466) -パッケージをパックするときに、依存関係パッケージの Id を確認しています。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-108">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
2. <span data-ttu-id="7cfd7-109">[マールテン島 balliauw 氏](https://www.codeplex.com/site/users/view/maartenba) ( [@maartenballiauw](https://twitter.com/maartenballiauw) )</span><span class="sxs-lookup"><span data-stu-id="7cfd7-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="7cfd7-110">[#2379](https://nuget.codeplex.com/workitem/2379) -persistening フィードの資格情報を持っている場合に、$metadata サフィックスを削除します。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-110">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
3. <span data-ttu-id="7cfd7-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ( [@foxtricks](https://twitter.com/foxtricks) )</span><span class="sxs-lookup"><span data-stu-id="7cfd7-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="7cfd7-112">[#3538](http://nuget.codeplex.com/workitem/3538) -nuget.exe update コマンドに対してプロジェクトファイルを指定する機能をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-112">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
4. [<span data-ttu-id="7cfd7-113">フアン Gonzalez。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-113">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="7cfd7-114">[#3536](http://nuget.codeplex.com/workitem/3536) 置換トークンが-IncludeReferencedProjects で渡されません。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-114">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
5. <span data-ttu-id="7cfd7-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ( [@Sarkie_Dave](https://twitter.com/Sarkie_Dave) )</span><span class="sxs-lookup"><span data-stu-id="7cfd7-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="7cfd7-116">[#3677](http://nuget.codeplex.com/workitem/3677) -大きなパッケージをプッシュするときに OutOfMemoryException をスローします。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-116">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
6. [<span data-ttu-id="7cfd7-117">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="7cfd7-117">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="7cfd7-118">[#3666](http://nuget.codeplex.com/workitem/3666) -プロジェクトが別の CLI/c + + プロジェクトを参照している場合に、不適切なターゲットパスを修正します。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-118">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
7. <span data-ttu-id="7cfd7-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )</span><span class="sxs-lookup"><span data-stu-id="7cfd7-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="7cfd7-120">[#3639](https://nuget.codeplex.com/workitem/3639) -既定でパッケージを開発の依存関係としてインストールできるようにする</span><span class="sxs-lookup"><span data-stu-id="7cfd7-120">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
8. <span data-ttu-id="7cfd7-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )</span><span class="sxs-lookup"><span data-stu-id="7cfd7-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="7cfd7-122">[#3717](https://nuget.codeplex.com/workitem/3717) -最新の修正プログラムのバージョンへの暗黙的なアップグレードを削除する</span><span class="sxs-lookup"><span data-stu-id="7cfd7-122">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
9. [<span data-ttu-id="7cfd7-123">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="7cfd7-123">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="7cfd7-124">いくつかのバグ修正と、NuGet. Server、nuget.exe mirror コマンド、およびその他の機能強化。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-124">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="7cfd7-125">この作業は数か月にわたって行われました。 Gregory は、2.8 のマスターに統合するための適切なタイミングで動作します。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-125">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="7cfd7-126">依存関係の修正プログラムの解像度</span><span class="sxs-lookup"><span data-stu-id="7cfd7-126">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="7cfd7-127">パッケージの依存関係を解決するとき、NuGet では、パッケージの依存関係を満たす最低メジャーおよびマイナーパッケージバージョンを選択するための戦略が実装されていました。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-127">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="7cfd7-128">ただし、メジャーバージョンとマイナーバージョンとは異なり、修正プログラムのバージョンは常に最も高いバージョンに解決されていました。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-128">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="7cfd7-129">動作は攻撃者でしたが、依存関係を含むパッケージをインストールするための決定性が欠如しています。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-129">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="7cfd7-130">次の例を確認してください。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-130">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="7cfd7-131">この例では、Developer1 と Developer2 がインストールされていても PackageA@1.0.0 、それぞれ異なるバージョンの PackageB で終了しています。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-131">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="7cfd7-132">NuGet 2.8 では、修正プログラムのバージョンの依存関係の解決動作がメジャーバージョンとマイナーバージョンの動作に一致するように、この既定の動作が変更されています。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-132">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="7cfd7-133">上の例では、 PackageB@1.0.0 PackageA@1.0.0 新しい修正プログラムのバージョンに関係なく、をインストールした結果としてがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-133">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="7cfd7-134">-DependencyVersion スイッチ</span><span class="sxs-lookup"><span data-stu-id="7cfd7-134">-DependencyVersion Switch</span></span>

<span data-ttu-id="7cfd7-135">NuGet 2.8 では、依存関係を解決するための _既定_ の動作が変更されますが、パッケージマネージャーコンソールの-dependencyversion スイッチを使用して依存関係の解決プロセスをさらに細かく制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-135">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="7cfd7-136">スイッチを使用すると、依存関係を、可能な限り低いバージョン (既定の動作)、可能な限り高いバージョン、または最新のマイナーバージョンまたは修正プログラムバージョンに解決できます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-136">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="7cfd7-137">このスイッチは、powershell コマンドのインストールパッケージに対してのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-137">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion スイッチ](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="7cfd7-139">DependencyVersion 属性</span><span class="sxs-lookup"><span data-stu-id="7cfd7-139">DependencyVersion Attribute</span></span>

<span data-ttu-id="7cfd7-140">前に説明した-DependencyVersion スイッチに加えて、NuGet では、-DependencyVersion スイッチがインストールパッケージの呼び出しで指定されていない場合に、既定値を定義する Nuget.Config ファイルに新しい属性を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-140">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="7cfd7-141">この値は、すべてのインストールパッケージ操作の [NuGet パッケージマネージャー] ダイアログでも尊重されます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-141">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="7cfd7-142">この値を設定するには、次の属性を Nuget.Config ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-142">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="7cfd7-143">-Whatif を使用した NuGet 操作のプレビュー</span><span class="sxs-lookup"><span data-stu-id="7cfd7-143">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="7cfd7-144">一部の NuGet パッケージには、深い依存関係グラフを含めることができます。そのため、インストール、アンインストール、または更新の操作中に、何が発生するかを最初に確認するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-144">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="7cfd7-145">NuGet 2.8 では、コマンドが適用されるパッケージのクロージャ全体を視覚化できるように、パッケージのインストール、アンインストール、および更新パッケージの各コマンドに標準の PowerShell-whatif スイッチが追加されています。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-145">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="7cfd7-146">たとえば、空の `install-package Microsoft.AspNet.WebApi -whatif` ASP.NET Web アプリケーションでを実行すると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-146">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

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

## <a name="downgrade-package"></a><span data-ttu-id="7cfd7-147">パッケージのダウングレード</span><span class="sxs-lookup"><span data-stu-id="7cfd7-147">Downgrade Package</span></span>

<span data-ttu-id="7cfd7-148">新しい機能を調査し、最新の安定したバージョンにロールバックすることを決定するために、パッケージのプレリリース版をインストールすることは珍しくありません。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-148">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="7cfd7-149">NuGet 2.8 より前では、これはプレリリースパッケージとその依存関係をアンインストールしてから、以前のバージョンをインストールする、複数の手順から成るプロセスでした。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-149">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="7cfd7-150">ただし、NuGet 2.8 では、更新プログラムパッケージはパッケージのクロージャ全体 (パッケージの依存関係ツリーなど) を以前のバージョンにロールバックします。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-150">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="7cfd7-151">開発の依存関係</span><span class="sxs-lookup"><span data-stu-id="7cfd7-151">Development Dependencies</span></span>

<span data-ttu-id="7cfd7-152">さまざまな種類の機能を NuGet パッケージとして提供できます。これには、開発プロセスの最適化に使用するツールが含まれます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-152">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="7cfd7-153">これらのコンポーネントは、新しいパッケージの開発に役立ちますが、後で公開するときに新しいパッケージの依存関係とは見なさないでください。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-153">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="7cfd7-154">NuGet 2.8 を使用すると、パッケージは `.nuspec` developmentDependency としてファイル内で自身を識別できます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-154">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="7cfd7-155">このメタデータは、インストールされると、パッケージがインストールされ `packages.config` たプロジェクトのファイルにも追加されます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-155">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="7cfd7-156">その `packages.config` ファイルが後で NuGet の依存関係を分析したときに `nuget.exe pack` 、開発の依存関係としてマークされた依存関係は除外されます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-156">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="7cfd7-157">さまざまなプラットフォームの個々の packages.config ファイル</span><span class="sxs-lookup"><span data-stu-id="7cfd7-157">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="7cfd7-158">複数のターゲットプラットフォーム用のアプリケーションを開発する場合は、それぞれのビルド環境に対して異なるプロジェクトファイルを使用するのが一般的です。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-158">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="7cfd7-159">さまざまなプロジェクトファイルで異なる NuGet パッケージを使用することもよくあります。パッケージには、プラットフォームごとに異なるレベルのサポートが用意されているためです。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-159">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="7cfd7-160">NuGet 2.8 では、 `packages.config` プラットフォーム固有のさまざまなプロジェクトファイルごとに異なるファイルを作成することによって、このシナリオのサポートが向上しています。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-160">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![複数の package.config ファイル](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="7cfd7-162">ローカルキャッシュへのフォールバック</span><span class="sxs-lookup"><span data-stu-id="7cfd7-162">Fallback to Local Cache</span></span>

<span data-ttu-id="7cfd7-163">通常、NuGet パッケージは、ネットワーク接続を使用する [nuget ギャラリー](http://www.nuget.org/) などのリモートギャラリーから使用されますが、クライアントが接続されていないシナリオは多数あります。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-163">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="7cfd7-164">ネットワーク接続がないと、NuGet クライアントは、パッケージがローカルの NuGet キャッシュ内のクライアントコンピューターに既に存在する場合でも、パッケージを正常にインストールできませんでした。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-164">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="7cfd7-165">NuGet 2.8 では、自動キャッシュフォールバックがパッケージマネージャーコンソールに追加されます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-165">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="7cfd7-166">たとえば、ネットワークアダプターを切断して jQuery をインストールする場合、コンソールには次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-166">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="7cfd7-167">キャッシュフォールバック機能では、特定のコマンド引数は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-167">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="7cfd7-168">さらに、現在、キャッシュフォールバックはパッケージマネージャーコンソールでのみ機能します。現在、[パッケージマネージャー] ダイアログボックスで動作は機能しません。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-168">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="7cfd7-169">WebMatrix NuGet クライアントの更新プログラム</span><span class="sxs-lookup"><span data-stu-id="7cfd7-169">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="7cfd7-170">Nuget 2.8 と共に、nuget [2.5](../release-notes/nuget-2.5.md)で提供される主な機能の多くを含むように、WebMatrix 用の nuget 拡張機能も更新されました。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-170">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="7cfd7-171">新しい機能としては、' Update All '、' Minimum NuGet Version ' などがあり、コンテンツファイルの上書きが許可されています。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-171">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="7cfd7-172">WebMatrix 3 で NuGet パッケージマネージャー拡張機能を更新するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-172">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="7cfd7-173">WebMatrix 3 を開く</span><span class="sxs-lookup"><span data-stu-id="7cfd7-173">Open WebMatrix 3</span></span>
1. <span data-ttu-id="7cfd7-174">リボンの [拡張機能] アイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-174">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="7cfd7-175">[更新] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-175">Select the Updates tab</span></span>
1. <span data-ttu-id="7cfd7-176">クリックして NuGet パッケージマネージャーを2.5.0 に更新します</span><span class="sxs-lookup"><span data-stu-id="7cfd7-176">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="7cfd7-177">WebMatrix 3 を閉じて再起動する</span><span class="sxs-lookup"><span data-stu-id="7cfd7-177">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="7cfd7-178">これは、WebMatrix の nuget パッケージマネージャー拡張機能の最初のリリースです。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-178">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="7cfd7-179">このコードは、Microsoft がオープンソースの NuGet プロジェクトに最近貢献しました。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-179">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="7cfd7-180">以前は、NuGet 統合は WebMatrix に組み込まれており、WebMatrix から帯域外で更新することはできませんでした。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-180">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="7cfd7-181">NuGet のクライアントツールの残りの部分と共に、さらに更新する機能が追加されました。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-181">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="7cfd7-182">バグ修正</span><span class="sxs-lookup"><span data-stu-id="7cfd7-182">Bug Fixes</span></span>

<span data-ttu-id="7cfd7-183">バグを修正した主な問題の1つは、更新プログラムパッケージの再インストールコマンドでパフォーマンスを向上させることでした。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-183">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="7cfd7-184">これらの機能と上記のパフォーマンスの修正に加えて、この NuGet のリリースには他にも多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-184">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="7cfd7-185">リリースで解決された問題の合計は181でした。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-185">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="7cfd7-186">NuGet 2.8 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7cfd7-186">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
