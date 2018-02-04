---
title: "NuGet 2.8 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.8 のリリース ノートします。"
keywords: "NuGet 2.8 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 39b885adc9e23eb815f65639875c4a4c27d61a4c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="74a2a-104">NuGet 2.8 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="74a2a-104">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="74a2a-105">[NuGet 2.7.2 リリース ノート](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 リリース ノート](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="74a2a-105">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="74a2a-106">NuGet 2.8 は、2014 年 1 月 29 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="74a2a-106">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="74a2a-107">謝辞</span><span class="sxs-lookup"><span data-stu-id="74a2a-107">Acknowledgements</span></span>

1. <span data-ttu-id="74a2a-108">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span><span class="sxs-lookup"><span data-stu-id="74a2a-108">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="74a2a-109">[#3466](https://nuget.codeplex.com/workitem/3466)梱包パッケージ、依存関係パッケージの Id を検証するときにします。</span><span class="sxs-lookup"><span data-stu-id="74a2a-109">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
1. <span data-ttu-id="74a2a-110">[マルテン Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span><span class="sxs-lookup"><span data-stu-id="74a2a-110">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="74a2a-111">[#2379](https://nuget.codeplex.com/workitem/2379) -persistening 資格情報をフィードするときに、$metadata サフィックスを削除します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-111">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
1. <span data-ttu-id="74a2a-112">[Filip De の](https://www.codeplex.com/site/users/view/FilipDeVos)([@foxtricks](https://twitter.com/foxtricks))</span><span class="sxs-lookup"><span data-stu-id="74a2a-112">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="74a2a-113">[#3538](http://nuget.codeplex.com/workitem/3538) - nuget.exe update コマンド用のプロジェクト ファイルの指定をサポートします。</span><span class="sxs-lookup"><span data-stu-id="74a2a-113">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
1. [<span data-ttu-id="74a2a-114">Juan Gonzalez</span><span class="sxs-lookup"><span data-stu-id="74a2a-114">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="74a2a-115">[#3536](http://nuget.codeplex.com/workitem/3536) -- IncludeReferencedProjects と共に渡すできません置換トークンです。</span><span class="sxs-lookup"><span data-stu-id="74a2a-115">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
1. <span data-ttu-id="74a2a-116">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span><span class="sxs-lookup"><span data-stu-id="74a2a-116">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="74a2a-117">[#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget.push 大きなパッケージのプッシュ時に、OutOfMemoryException をスローします。</span><span class="sxs-lookup"><span data-stu-id="74a2a-117">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
1. [<span data-ttu-id="74a2a-118">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="74a2a-118">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="74a2a-119">[#3666](http://nuget.codeplex.com/workitem/3666) -プロジェクトが別の CLI と C++ プロジェクトを参照するときの修正プログラムの無効なターゲット パス。</span><span class="sxs-lookup"><span data-stu-id="74a2a-119">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
1. <span data-ttu-id="74a2a-120">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="74a2a-120">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="74a2a-121">[#3639](https://nuget.codeplex.com/workitem/3639) -開発の依存関係として既定でインストールするパッケージを許可します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-121">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
1. <span data-ttu-id="74a2a-122">[David ファウラー](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="74a2a-122">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="74a2a-123">[#3717](https://nuget.codeplex.com/workitem/3717) -最新のパッチ バージョンにアップグレードする暗黙の型を削除します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-123">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
1. [<span data-ttu-id="74a2a-124">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="74a2a-124">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="74a2a-125">いくつかのバグの修正と NuGet.Server、nuget.exe ミラー コマンドおよびその他の機能強化。</span><span class="sxs-lookup"><span data-stu-id="74a2a-125">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="74a2a-126">この作業は、2.8 のマスターに統合する右のタイミングで協力 Gregory を使用して数か月間、経由で行われました。</span><span class="sxs-lookup"><span data-stu-id="74a2a-126">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="74a2a-127">依存関係の解決の修正プログラム</span><span class="sxs-lookup"><span data-stu-id="74a2a-127">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="74a2a-128">パッケージの依存関係を解決するときに NuGet はパッケージへの依存関係を満たすメジャーおよびマイナーのパッケージの最も低いバージョンを選択した場合の戦略を実装してきました。</span><span class="sxs-lookup"><span data-stu-id="74a2a-128">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="74a2a-129">メジャーおよびマイナーのバージョンとは異なりただし、修正プログラムのバージョンが常に解決最高のバージョン。</span><span class="sxs-lookup"><span data-stu-id="74a2a-129">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="74a2a-130">動作が善意、依存関係を持つパッケージをインストールするための決定性の欠如が作成されます。</span><span class="sxs-lookup"><span data-stu-id="74a2a-130">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="74a2a-131">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-131">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="74a2a-132">この例では、たとえ Developer1 と Developer2 インストールPackageA@1.0.0PackageB の別のバージョンのそれぞれに終了しました。</span><span class="sxs-lookup"><span data-stu-id="74a2a-132">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="74a2a-133">NuGet 2.8 は、修正プログラムのバージョンの依存関係の解決の動作がメジャーおよびマイナー バージョンの動作と一致するように、この既定の動作を変更します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-133">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="74a2a-134">上記の例で、次に、PackageB@1.0.0インストールの結果としてインストールされるPackageA@1.0.0修正プログラムの新しいバージョンに関係なく、します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-134">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="74a2a-135">-DependencyVersion Switch</span><span class="sxs-lookup"><span data-stu-id="74a2a-135">-DependencyVersion Switch</span></span>

<span data-ttu-id="74a2a-136">NuGet 2.8 の変更が、_既定_動作の依存関係を解決するためにも追加 - DependencyVersion スイッチ経由で依存関係の解決プロセスを細かく制御パッケージ マネージャー コンソールです。</span><span class="sxs-lookup"><span data-stu-id="74a2a-136">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="74a2a-137">スイッチは、最下位の可能なバージョン (既定の動作)、最大の可能なバージョンまたは最高のマイナーまたは修正プログラムのバージョンに依存関係を解決できます。</span><span class="sxs-lookup"><span data-stu-id="74a2a-137">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="74a2a-138">このスイッチは、powershell コマンドでのインストール パッケージに対してのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-138">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion スイッチ](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="74a2a-140">DependencyVersion 属性</span><span class="sxs-lookup"><span data-stu-id="74a2a-140">DependencyVersion Attribute</span></span>

<span data-ttu-id="74a2a-141">に加えて、上述 NuGet が必要なアクセス許可も許可されている Nuget.Config ファイルの新しい属性を設定する - DependencyVersion スイッチを定義する既定値の呼び出しでは、- DependencyVersion スイッチが指定されていない場合インストール パッケージです。</span><span class="sxs-lookup"><span data-stu-id="74a2a-141">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="74a2a-142">この値が、任意の操作のインストール パッケージの NuGet Package Manager ダイアログ ボックスでも適用されます。</span><span class="sxs-lookup"><span data-stu-id="74a2a-142">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="74a2a-143">この値を設定するには、Nuget.Config ファイルに以下の属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-143">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="74a2a-144">-Whatif でプレビュー NuGet 操作</span><span class="sxs-lookup"><span data-stu-id="74a2a-144">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="74a2a-145">そのため、そのことができますのインストール中に役に立ちます、アンインストール、または更新操作が最初に何が起こるかを確認するおよび一部の NuGet パッケージの詳細な依存関係グラフがあります。</span><span class="sxs-lookup"><span data-stu-id="74a2a-145">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="74a2a-146">NuGet 2.8 は、パッケージのインストール、アンインストール パッケージおよびコマンドの適用先となるパッケージの全体のクロージャをビジュアル化を有効にする更新プログラム パッケージのコマンドを標準の PowerShell-whatif スイッチを追加します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-146">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="74a2a-147">たとえば、実行している`install-package Microsoft.AspNet.WebApi -whatif`空の ASP.NET Web アプリケーションには、次が得られます。</span><span class="sxs-lookup"><span data-stu-id="74a2a-147">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

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

## <a name="downgrade-package"></a><span data-ttu-id="74a2a-148">パッケージのダウン グレード</span><span class="sxs-lookup"><span data-stu-id="74a2a-148">Downgrade Package</span></span>

<span data-ttu-id="74a2a-149">新機能を調査するために、パッケージのプレリリース版をインストールし、最後の安定したバージョンにロールバックするには珍しいことはできません。</span><span class="sxs-lookup"><span data-stu-id="74a2a-149">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="74a2a-150">NuGet 2.8 の前に、これはプレリリースのパッケージとその依存関係をアンインストールし、以前のバージョンをインストールのプロセスを複数のステップをでした。</span><span class="sxs-lookup"><span data-stu-id="74a2a-150">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="74a2a-151">NuGet 2.8 を使用ただし、更新プログラム パッケージは今すぐパッケージ全体のクロージャ (例: パッケージの依存関係ツリー) にロールバック前のバージョン。</span><span class="sxs-lookup"><span data-stu-id="74a2a-151">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="74a2a-152">開発の依存関係</span><span class="sxs-lookup"><span data-stu-id="74a2a-152">Development Dependencies</span></span>

<span data-ttu-id="74a2a-153">さまざまな種類の機能は、NuGet パッケージの開発プロセスを最適化するために使用されるツールを含むとして配信することができます。</span><span class="sxs-lookup"><span data-stu-id="74a2a-153">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="74a2a-154">これらのコンポーネントは、新しいパッケージの開発に役立つ可能性があるときに区別しない新しいパッケージの依存関係後で発行されているとします。</span><span class="sxs-lookup"><span data-stu-id="74a2a-154">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="74a2a-155">自身を識別するパッケージの NuGet 2.8 を有効、 `.nuspec` developmentDependency としてファイル。</span><span class="sxs-lookup"><span data-stu-id="74a2a-155">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="74a2a-156">このメタデータに追加することも、インストールされている場合、`packages.config`プロジェクト、パッケージのインストール先のファイルです。</span><span class="sxs-lookup"><span data-stu-id="74a2a-156">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="74a2a-157">時を`packages.config`ファイルは後の中に、NuGet の依存関係の分析`nuget.exe pack`開発の依存関係としてマークされているこれらの依存関係が除外されます。</span><span class="sxs-lookup"><span data-stu-id="74a2a-157">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="74a2a-158">さまざまなプラットフォーム用の個別の packages.config ファイル</span><span class="sxs-lookup"><span data-stu-id="74a2a-158">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="74a2a-159">複数のターゲット プラットフォーム用のアプリケーションを開発するときは、それぞれのビルド環境のそれぞれに対して別のプロジェクト ファイルを一般的なです。</span><span class="sxs-lookup"><span data-stu-id="74a2a-159">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="74a2a-160">パッケージがさまざまなプラットフォームのサポートのさまざまなレベルにも、別のプロジェクト ファイル内の別の NuGet パッケージを使用する一般的なです。</span><span class="sxs-lookup"><span data-stu-id="74a2a-160">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="74a2a-161">NuGet 2.8 のサポートの強化このシナリオを作成することにより異なる`packages.config`さまざまなプラットフォーム固有のプロジェクト ファイルのファイルです。</span><span class="sxs-lookup"><span data-stu-id="74a2a-161">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![複数の package.config ファイル](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="74a2a-163">ローカル キャッシュにフォールバック</span><span class="sxs-lookup"><span data-stu-id="74a2a-163">Fallback to Local Cache</span></span>

<span data-ttu-id="74a2a-164">NuGet パッケージの通常使用されるリモート ギャラリーからなど、 [NuGet ギャラリー](http://www.nuget.org/)ネットワーク接続を使用するシナリオは多くのクライアントが接続されていません。</span><span class="sxs-lookup"><span data-stu-id="74a2a-164">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="74a2a-165">ネットワーク接続を行わず NuGet クライアントは、それらのパッケージは NuGet のローカル キャッシュ内のクライアント コンピューターに存在した場合でも、パッケージ - を正常にインストールできませんでした。</span><span class="sxs-lookup"><span data-stu-id="74a2a-165">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="74a2a-166">NuGet 2.8 は、キャッシュの自動フォールバックをパッケージ マネージャー コンソールに追加します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-166">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="74a2a-167">たとえば、ときに、ネットワーク アダプターを切断して、jQuery をインストールする、コンソール次に示します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-167">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="74a2a-168">キャッシュのフォールバック機能には、特定のコマンド引数は不要です。</span><span class="sxs-lookup"><span data-stu-id="74a2a-168">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="74a2a-169">さらに、フォールバック キャッシュが現在パッケージ マネージャー コンソールでのみ機能 - パッケージ マネージャー ダイアログで、動作が現在機能しません。</span><span class="sxs-lookup"><span data-stu-id="74a2a-169">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="74a2a-170">WebMatrix NuGet クライアントの更新プログラムします。</span><span class="sxs-lookup"><span data-stu-id="74a2a-170">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="74a2a-171">NuGet 2.8 と共に WebMatrix の NuGet 拡張機能も更新されたで提供される主要な機能の多くを[NuGet 2.5](../release-notes/nuget-2.5.md)です。</span><span class="sxs-lookup"><span data-stu-id="74a2a-171">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="74a2a-172">新機能では、' All Update'、' 最小 NuGet バージョン ' などのコンテンツ ファイルが上書きされることがあります。</span><span class="sxs-lookup"><span data-stu-id="74a2a-172">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="74a2a-173">WebMatrix 3 での NuGet Package Manager 拡張機能を更新します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-173">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="74a2a-174">WebMatrix 3 を開く</span><span class="sxs-lookup"><span data-stu-id="74a2a-174">Open WebMatrix 3</span></span>
1. <span data-ttu-id="74a2a-175">リボンの拡張機能のアイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="74a2a-175">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="74a2a-176">更新プログラム タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="74a2a-176">Select the Updates tab</span></span>
1. <span data-ttu-id="74a2a-177">2.5.0 に NuGet Package Manager を更新する をクリックします。</span><span class="sxs-lookup"><span data-stu-id="74a2a-177">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="74a2a-178">終了し、WebMatrix 3 の再起動</span><span class="sxs-lookup"><span data-stu-id="74a2a-178">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="74a2a-179">これは、NuGet チームの最初のリリースの NuGet Package Manager 拡張機能の WebMatrix 用です。</span><span class="sxs-lookup"><span data-stu-id="74a2a-179">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="74a2a-180">コードが最近から提供された Microsoft オープン ソース NuGet のプロジェクトにします。</span><span class="sxs-lookup"><span data-stu-id="74a2a-180">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="74a2a-181">以前は、NuGet の統合された、WebMatrix に組み込まれているし、帯域外 WebMatrix から更新できませんでした。</span><span class="sxs-lookup"><span data-stu-id="74a2a-181">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="74a2a-182">さらに、NuGet のクライアント ツールの残りの部分と共にに更新する機能があるようになりました。</span><span class="sxs-lookup"><span data-stu-id="74a2a-182">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="74a2a-183">バグ修正</span><span class="sxs-lookup"><span data-stu-id="74a2a-183">Bug Fixes</span></span>

<span data-ttu-id="74a2a-184">更新プログラム パッケージのパフォーマンスの向上が加えられた主なバグの修正のいずれかのコマンドを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="74a2a-184">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="74a2a-185">NuGet の今回のリリースには、これらの機能と、上記のパフォーマンス修正に加えて、他の多くのバグ修正も含まれます。</span><span class="sxs-lookup"><span data-stu-id="74a2a-185">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="74a2a-186">リリースで対処 181 の合計の問題が発生しました。</span><span class="sxs-lookup"><span data-stu-id="74a2a-186">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="74a2a-187">作業の完全な一覧の項目で修正 NuGet 2.8 くださいビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)です。</span><span class="sxs-lookup"><span data-stu-id="74a2a-187">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
