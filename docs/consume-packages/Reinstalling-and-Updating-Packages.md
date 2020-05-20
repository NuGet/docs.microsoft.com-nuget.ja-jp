---
title: NuGet パッケージの再インストールと更新
description: パッケージをいつ更新して再インストールする必要があるのかに関する詳細と、壊れた Visual Studio のパッケージ参照について。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: 101c6d6b9d93da912f60c40b27559e80327154b8
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428427"
---
# <a name="how-to-reinstall-and-update-packages"></a><span data-ttu-id="fe9ef-103">パッケージを再インストールし更新する方法</span><span class="sxs-lookup"><span data-stu-id="fe9ef-103">How to reinstall and update packages</span></span>

<span data-ttu-id="fe9ef-104">以下の「[パッケージを再インストールするタイミング](#when-to-reinstall-a-package)」で説明しているとおり、Visual Studio のプロジェクトでは、パッケージへの参照が壊れてしまう状況が多々あります。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-104">There are a number of situations, described below under [When to Reinstall a Package](#when-to-reinstall-a-package), where references to a package might get broken within a Visual Studio project.</span></span> <span data-ttu-id="fe9ef-105">このような場合、パッケージの同じバージョンをアンインストールして再インストールすると、それらの参照は復元され動作するようになります。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-105">In these cases, uninstalling and then reinstalling the same version of the package will restore those references to working order.</span></span> <span data-ttu-id="fe9ef-106">パッケージを更新するということは、単純に更新されたバージョンをインストールすることを意味し、これによってパッケージはしばしば動作する状態に復元されます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-106">Updating a package simply means installing an updated version, which often restores a package to working order.</span></span>

<span data-ttu-id="fe9ef-107">Visual Studio のパッケージ マネージャー コンソールには、パッケージの更新と再インストールを行うための柔軟なオプションが多数用意されています。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-107">In Visual Studio, the Package Manager Console provides many flexible options for updating and reinstalling packages.</span></span>

<span data-ttu-id="fe9ef-108">パッケージの更新と再インストールは次の順序で行います。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-108">Updating and reinstalling packages is accomplished as follows:</span></span>

| <span data-ttu-id="fe9ef-109">メソッド</span><span class="sxs-lookup"><span data-stu-id="fe9ef-109">Method</span></span> | <span data-ttu-id="fe9ef-110">更新</span><span class="sxs-lookup"><span data-stu-id="fe9ef-110">Update</span></span> | <span data-ttu-id="fe9ef-111">再インストール</span><span class="sxs-lookup"><span data-stu-id="fe9ef-111">Reinstall</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fe9ef-112">パッケージ マネージャー コンソール (「[Update-Package の使用](#using-update-package)」を参照)</span><span class="sxs-lookup"><span data-stu-id="fe9ef-112">Package Manager console (described in [Using Update-Package](#using-update-package))</span></span> | <span data-ttu-id="fe9ef-113">`Update-Package` コマンド</span><span class="sxs-lookup"><span data-stu-id="fe9ef-113">`Update-Package` command</span></span> | <span data-ttu-id="fe9ef-114">`Update-Package -reinstall` コマンド</span><span class="sxs-lookup"><span data-stu-id="fe9ef-114">`Update-Package -reinstall` command</span></span> |
| <span data-ttu-id="fe9ef-115">パッケージ マネージャー UI</span><span class="sxs-lookup"><span data-stu-id="fe9ef-115">Package Manager UI</span></span> | <span data-ttu-id="fe9ef-116">**[更新]** タブで、1 つ以上のパッケージを選択し、 **[更新]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-116">On the **Updates** tab, select one or more packages and select **Update**</span></span> | <span data-ttu-id="fe9ef-117">**[インストール]** タブで、パッケージを選択し、その名前を書き留め、 **[アンインストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-117">On the **Installed** tab, select a package, record its name, then select **Uninstall**.</span></span> <span data-ttu-id="fe9ef-118">**[参照]** タブに切り替え、パッケージ名を検索して選択し、 **[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-118">Switch to the **Browse** tab, search for the package name, select it, then select **Install**).</span></span> |
| <span data-ttu-id="fe9ef-119">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="fe9ef-119">nuget.exe CLI</span></span> | <span data-ttu-id="fe9ef-120">`nuget update` コマンド</span><span class="sxs-lookup"><span data-stu-id="fe9ef-120">`nuget update` command</span></span> | <span data-ttu-id="fe9ef-121">すべてのパッケージで、パッケージ フォルダーを削除し、`nuget install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-121">For all packages, delete the package folder, then run `nuget install`.</span></span> <span data-ttu-id="fe9ef-122">1 つのパッケージで、パッケージ フォルダーを削除し、`nuget install <id>` を使用して同じものを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-122">For a single package, delete the package folder and use `nuget install <id>` to reinstall the same one.</span></span> |

> [!NOTE]
> <span data-ttu-id="fe9ef-123">dotnet CLI では、同等のプロシージャは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-123">For the dotnet CLI, the equivalent procedure is not required.</span></span> <span data-ttu-id="fe9ef-124">同様のシナリオで、[dotnet CLI を使用してパッケージを復元](package-restore.md#restore-using-the-dotnet-cli)できます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-124">In a similar scenario, you can [restore packages with the dotnet CLI](package-restore.md#restore-using-the-dotnet-cli).</span></span>

<span data-ttu-id="fe9ef-125">この記事の内容:</span><span class="sxs-lookup"><span data-stu-id="fe9ef-125">In this article:</span></span>

- [<span data-ttu-id="fe9ef-126">パッケージを再インストールするタイミング</span><span class="sxs-lookup"><span data-stu-id="fe9ef-126">When to Reinstall a Package</span></span>](#when-to-reinstall-a-package)
- [<span data-ttu-id="fe9ef-127">アップグレード バージョンを制限する</span><span class="sxs-lookup"><span data-stu-id="fe9ef-127">Constraining upgrade versions</span></span>](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a><span data-ttu-id="fe9ef-128">パッケージを再インストールするタイミング</span><span class="sxs-lookup"><span data-stu-id="fe9ef-128">When to Reinstall a Package</span></span>

1. <span data-ttu-id="fe9ef-129">**パッケージの復元後に参照が壊れた場合**: プロジェクトを開いて NuGet パッケージを復元しても、引き続き参照が壊れている場合、それらのパッケージをそれぞれ再インストールしてみてください。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-129">**Broken references after package restore**: If you've opened a project and restored NuGet packages, but still see broken references, try reinstalling each of those packages.</span></span>
1. <span data-ttu-id="fe9ef-130">**ファイルを削除したためにプロジェクトが壊れた場合**: NuGet によって、ユーザーがパッケージから追加されたアイテムを削除できなくされることはありません。したがって、パッケージからインストールされたコンテンツを不注意に簡単に変更できてしまい、プロジェクトを壊すことができます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-130">**Project is broken due to deleted files**: NuGet does not prevent you from removing items added from packages, so it's easy to inadvertently modify contents installed from a package and break your project.</span></span> <span data-ttu-id="fe9ef-131">プロジェクトを復元するには、影響を受けたパッケージを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-131">To restore the project, reinstall the affected packages.</span></span>
1. <span data-ttu-id="fe9ef-132">**パッケージの更新によりプロジェクトが壊れた場合**: パッケージを更新してプロジェクトが壊れた場合、一般的に障害は更新された可能性がある依存関係パッケージによって起こります。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-132">**Package update broke the project**: If an update to a package breaks a project, the failure is generally caused by a dependency package which may have also been updated.</span></span> <span data-ttu-id="fe9ef-133">依存関係の状態を復元するには、その特定のパッケージを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-133">To restore the state of the dependency, reinstall that specific package.</span></span>
1. <span data-ttu-id="fe9ef-134">**プロジェクトの再ターゲットまたはアップグレードの場合**: これは、プロジェクトが再ターゲットされたかアップグレードされた場合、ターゲット フレームワークの変更のためにパッケージを再インストールする必要がある場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-134">**Project retargeting or upgrade**: This can be useful when a project has been retargeted or upgraded and if the package requires reinstallation due to the change in target framework.</span></span> <span data-ttu-id="fe9ef-135">NuGet では、このような場合、プロジェクトの再ターゲット後に直ちにビルド エラーが表示されます。そしてその後のビルド警告により、パッケージを再インストールする必要がある場合があることが通知されます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-135">NuGet shows a build error in such cases immediately after project retargeting, and subsequent build warnings let you know that the package may need to be reinstalled.</span></span> <span data-ttu-id="fe9ef-136">プロジェクトをアップグレードする必要がある場合、NuGet では、プロジェクトのアップグレード ログにエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-136">For project upgrade, NuGet shows an error in the Project Upgrade Log.</span></span>
1. <span data-ttu-id="fe9ef-137">**開発時にパッケージを再インストールする場合**: パッケージ作成者は、動作をテストするために、開発しているパッケージの同じバージョンを再インストールする必要があることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-137">**Reinstalling a package during its development**: Package authors often need to reinstall the same version of package they're developing to test the behavior.</span></span> <span data-ttu-id="fe9ef-138">`Install-Package` コマンドには再インストールを強制するオプションがないので、代わりに `Update-Package -reinstall` を使用します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-138">The `Install-Package` command does not provide an option to force a reinstall, so use `Update-Package -reinstall` instead.</span></span>

## <a name="constraining-upgrade-versions"></a><span data-ttu-id="fe9ef-139">アップグレード バージョンを制限する</span><span class="sxs-lookup"><span data-stu-id="fe9ef-139">Constraining upgrade versions</span></span>

<span data-ttu-id="fe9ef-140">既定では、パッケージを再インストールまたは更新した場合、パッケージ ソースから使用可能な最新バージョンが*常に*インストールされます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-140">By default, reinstalling or updating a package *always* installs the latest version available from the package source.</span></span>

<span data-ttu-id="fe9ef-141">ただし、`packages.config` 管理形式を使用するプロジェクトでは、バージョン範囲を具体的に制限することができます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-141">In projects using the `packages.config` management format, however, you can specifically constrain the version range.</span></span> <span data-ttu-id="fe9ef-142">たとえば、恐らくはパッケージ API の大幅な変更により、アプリケーションがパッケージのバージョン 2.0 以上では機能せず、1.x のみで機能することがわかっている場合、バージョン 1.x にアップグレードすることに制限したいとします。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-142">For example, if you know that your application works only with version 1.x of a package but not 2.0 and above, perhaps due to a major change in the package API, then you'd want to constrain upgrades to 1.x versions.</span></span> <span data-ttu-id="fe9ef-143">これにより、偶発的に更新されることにより、アプリケーションが機能しなくなってしまうことを避けることができます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-143">This prevents accidental updates that would break the application.</span></span>

<span data-ttu-id="fe9ef-144">制限を設定するには、テキスト エディターで `packages.config` を開き、問題の依存関係を探し、バージョン範囲と共に `allowedVersions` 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-144">To set a constraint, open `packages.config` in a text editor, locate the dependency in question, and add the `allowedVersions` attribute with a version range.</span></span> <span data-ttu-id="fe9ef-145">たとえば、更新をバージョン 1.x に制限する場合、`allowedVersions` を `[1,2)` に設定します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-145">For example, to constrain updates to version 1.x, set `allowedVersions` to `[1,2)`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

<span data-ttu-id="fe9ef-146">いずれの場合も、「[Package versioning](../concepts/package-versioning.md#version-ranges)」(パッケージのバージョン管理) で説明されている表記を使います。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-146">In all cases, use the notation described in [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-update-package"></a><span data-ttu-id="fe9ef-147">Update-Package の使用</span><span class="sxs-lookup"><span data-stu-id="fe9ef-147">Using Update-Package</span></span>

<span data-ttu-id="fe9ef-148">以下の「[注意事項](#considerations)」を考慮しながら、Visual Studio パッケージ マネージャー コンソール (**[ツール]** > **[NuGet パッケージ マネージャー]** > **[パッケージ マネージャー コンソール]**) の [[Update-Package コマンド]](../reference/ps-reference/ps-ref-update-package.md) を使用して、すべてのパッケージを簡単に再インストールできます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-148">Being mindful of the [Considerations](#considerations) described below, you can easily reinstall any package using the [Update-Package command](../reference/ps-reference/ps-ref-update-package.md) in the Visual Studio Package Manager Console (**Tools** > **NuGet Package Manager** > **Package Manager Console**).</span></span>

```ps
Update-Package -Id <package_name> –reinstall
```

<span data-ttu-id="fe9ef-149">このコマンドの使用は、パッケージを削除し、NuGet ギャラリーで同じバージョンの同じパッケージを探すよりもはるかに簡単です。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-149">Using this command is much easier than removing a package and then trying to locate the same package in the NuGet gallery with the same version.</span></span> <span data-ttu-id="fe9ef-150">なお、`-Id` スイッチは省略可能です。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-150">Note that the `-Id` switch is optional.</span></span>

<span data-ttu-id="fe9ef-151">`-reinstall` なしの同じコマンドでは、存在する場合、パッケージがより新しいバージョンに更新されます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-151">The same command without `-reinstall` updates a package to a newer version, if applicable.</span></span> <span data-ttu-id="fe9ef-152">問題のパッケージがプロジェクトにまだインストールされていない場合、このコマンドによってエラーが表示されます。つまり、`Update-Package` でパッケージが直接インストールされません。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-152">The command gives an error if the package in question is not already installed in a project; that is, `Update-Package` does not install packages directly.</span></span>

```ps
Update-Package <package_name>
```

<span data-ttu-id="fe9ef-153">既定では、`Update-Package` はソリューション内のすべてのプロジェクトに影響します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-153">By default, `Update-Package` affects all projects in a solution.</span></span> <span data-ttu-id="fe9ef-154">特定のプロジェクトにアクションを制限するには、ソリューション エクスプローラーに表示されるプロジェクト名を使用し、`-ProjectName` スイッチを使用します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-154">To limit the action to a specific project, use the `-ProjectName` switch, using the name of the project as it appears in Solution Explorer:</span></span>

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

<span data-ttu-id="fe9ef-155">プロジェクトのすべてのパッケージを*更新*するには (または `-reinstall` を使用して再インストールするには)、特定のパッケージを指定せずに `-ProjectName` を使用します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-155">To *update* all packages in a project (or reinstall using `-reinstall`), use `-ProjectName` without specifying any particular package:</span></span>

```ps
Update-Package -ProjectName MyProject
```

<span data-ttu-id="fe9ef-156">ソリューション内のすべてのパッケージを更新するには、`Update-Package` を他の引数やスイッチなしで単体で使用します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-156">To update all packages in a solution, just use `Update-Package` by itself with no other arguments or switches.</span></span> <span data-ttu-id="fe9ef-157">すべての更新を行うには、かなり時間がかかるため、このフォームは慎重に使用してください。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-157">Use this form carefully, because it can take considerable time to perform all the updates:</span></span>

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

<span data-ttu-id="fe9ef-158">[PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)を使用してプロジェクトまたはソリューションのパッケージを更新する場合、パッケージは常に最新バージョンに更新されます (リリース前のパッケージは除きます)。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-158">Updating packages in a project or solution using [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) always updates to the latest version of the package (excluding pre-release packages).</span></span> <span data-ttu-id="fe9ef-159">プロジェクトで `packages.config` を使用している場合、必要に応じて、以下の「[アップグレード バージョンを制限する](#constraining-upgrade-versions)」で説明するとおり、更新バージョンを制限できます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-159">Projects that use `packages.config` can, if desired, limit update versions as described below in [Constraining upgrade versions](#constraining-upgrade-versions).</span></span>

<span data-ttu-id="fe9ef-160">完全なコマンドについては、「[Update-Package](../reference/ps-reference/ps-ref-update-package.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-160">For full details on the command, see the [Update-Package](../reference/ps-reference/ps-ref-update-package.md) reference.</span></span>

### <a name="considerations"></a><span data-ttu-id="fe9ef-161">注意事項</span><span class="sxs-lookup"><span data-stu-id="fe9ef-161">Considerations</span></span>

<span data-ttu-id="fe9ef-162">パッケージを再インストールする場合、以下の影響がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-162">The following may be affected when reinstalling a package:</span></span>

1. <span data-ttu-id="fe9ef-163">**プロジェクト ターゲット フレームワークの再ターゲットに従ったパッケージの再インストール**</span><span class="sxs-lookup"><span data-stu-id="fe9ef-163">**Reinstalling packages according to project target framework retargeting**</span></span>
    - <span data-ttu-id="fe9ef-164">単純なケースでは、`Update-Package –reinstall <package_name>` を使用してパッケージを再インストールするたけで機能します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-164">In a simple case, just reinstalling a package using `Update-Package –reinstall <package_name>` works.</span></span> <span data-ttu-id="fe9ef-165">古いターゲット フレームワークに対してインストールされたパッケージは、アンインストールされ、同じパッケージがそのプロジェクトの現在のターゲット フレームワークに対してインストールされます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-165">A package that is installed against an old target framework gets uninstalled and the same package gets installed against the current target framework of the project.</span></span>
    - <span data-ttu-id="fe9ef-166">パッケージで、新しいターゲット フレームワークがサポートされない場合もあります。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-166">In some cases, there may be a package that does not support the new target framework.</span></span>
        - <span data-ttu-id="fe9ef-167">パッケージがポータブル クラス ライブラリ (PCL) をサポートし、プロジェクトがパッケージがサポートしなくなったプラットフォームの組み合わせに再ターゲットされている場合、パッケージへの参照は再インストール後に失われます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-167">If a package supports portable class libraries (PCLs) and the project is retargeted to a combination of platforms no longer supported by the package, references to the package will be missing after reinstalling.</span></span>
        - <span data-ttu-id="fe9ef-168">これは直接使用しているパッケージまたは依存関係でインストールされたパッケージで生じます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-168">This can surface for packages you're using directly or for packages installed as dependencies.</span></span> <span data-ttu-id="fe9ef-169">その依存関係はサポートしない場合でも、使用しているパッケージで、新しいターゲット フレームワークを直接サポートさせることは可能です。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-169">It's possible for the package you're using directly to support the new target framework while its dependency does not.</span></span>
        - <span data-ttu-id="fe9ef-170">アプリケーションの再ターゲット後にパッケージを再インストールすることによって、ビルド エラーまたはランタイム エラーが発生する場合、ターゲット フレームワークを元に戻すか、新しいターゲット フレームワークを正しくサポートする別のパッケージを探す必要があります。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-170">If reinstalling packages after retargeting your application results in build or runtime errors, you may need to revert your target framework or search for alternative packages that properly support your new target framework.</span></span>

1. <span data-ttu-id="fe9ef-171">**プロジェクトの再ターゲットまたはアップグレード後に、packages.config に requireReinstallation 属性が追加される**</span><span class="sxs-lookup"><span data-stu-id="fe9ef-171">**requireReinstallation attribute added in packages.config after project retargeting or upgrade**</span></span>
    - <span data-ttu-id="fe9ef-172">NuGet によってプロジェクトの再ターゲットまたはアップグレードによってパッケージが影響を受けたと検出された場合、影響を受けたすべてのパッケージ参照の `packages.config` に `requireReinstallation="true"` 属性が追加されます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-172">If NuGet detects that packages were affected by retargeting or upgrading a project, it adds a `requireReinstallation="true"` attribute in  `packages.config` to all affected package references.</span></span> <span data-ttu-id="fe9ef-173">このため、Visual Studio のそれ以降の各ビルドでは、再インストールすることを忘れないように、それらのパッケージでビルド警告が発せられます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-173">Because of this, each subsequent build in Visual Studio raises build warnings for those packages so you can remember to reinstall them.</span></span>

1. <span data-ttu-id="fe9ef-174">**依存関係と共にパッケージを再インストールする**</span><span class="sxs-lookup"><span data-stu-id="fe9ef-174">**Reinstalling packages with dependencies**</span></span>
    - <span data-ttu-id="fe9ef-175">`Update-Package –reinstall` では元のパッケージの同じバージョンが再インストールされますが、依存関係は、特定のバージョン制限を指定しない限り、最新バージョンがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-175">`Update-Package –reinstall` reinstalls the same version of the original package, but installs the latest version of dependencies unless specific version constraints are provided.</span></span> <span data-ttu-id="fe9ef-176">このため、問題を修正するには必要な依存関係のみを更新します。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-176">This allows you to update only the dependencies as required to fix an issue.</span></span> <span data-ttu-id="fe9ef-177">ただし、これにより、依存関係が以前のバージョンにロールバックされる場合、依存パッケージには影響を与えずに、`Update-Package <dependency_name>` を使用して、その 1 つの依存関係のみを再インストールできます。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-177">However, if this rolls a dependency back to an earlier version, you can use `Update-Package <dependency_name>` to reinstall that one dependency without affecting the dependent package.</span></span>
    - <span data-ttu-id="fe9ef-178">`Update-Package –reinstall <packageName> -ignoreDependencies` では、元のパッケージの同じバージョンが再インストールされますが、依存関係は再インストールされません。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-178">`Update-Package –reinstall <packageName> -ignoreDependencies` reinstalls the same version of the original package but does not reinstall dependencies.</span></span> <span data-ttu-id="fe9ef-179">パッケージの依存関係を更新したことによって壊れてしまう場合、これを使用してください。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-179">Use this when updating package dependencies might result in a broken state</span></span>

1. <span data-ttu-id="fe9ef-180">**依存しているバージョンが含まれている場合にパッケージを再インストールする**</span><span class="sxs-lookup"><span data-stu-id="fe9ef-180">**Reinstalling packages when dependent versions are involved**</span></span>
    - <span data-ttu-id="fe9ef-181">上で説明したとおり、パッケージを再インストールしても、それに依存する他のインストールされているパッケージのバージョンは変わりません。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-181">As explained above, reinstalling a package does not change versions of any other installed packages that depend on it.</span></span> <span data-ttu-id="fe9ef-182">その場合、依存関係を再インストールした場合、依存パッケージが壊れてしまう場合があります。</span><span class="sxs-lookup"><span data-stu-id="fe9ef-182">It's possible, then, that reinstalling a dependency could break the dependent package.</span></span>
