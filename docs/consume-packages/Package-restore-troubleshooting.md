---
title: Visual Studio での NuGet パッケージの復元に関するトラブルシューティング
description: Visual Studio の一般的な NuGet の復元エラーの説明とトラブルシューティングの方法です。
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860620"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="9d9cb-103">パッケージの復元エラーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="9d9cb-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="9d9cb-104">この記事では、パッケージを復元するときの一般的なエラーと、それを解決する手順に重点を置いて説明しています。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="9d9cb-105">[パッケージの復元] では、プロジェクト ファイル ( *.csproj*) のパッケージ参照か *packages.config* ファイルに一致する正しい状態になるよう、すべてのパッケージの依存関係のインストールを試みます。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="9d9cb-106">(Visual Studio では、参照は **[依存関係] \ [NuGet]** または **[参照]** ノードの下にあるソリューション エクスプローラーに表示されます。)パッケージを復元するために必要な手順に従うには、「[パッケージの復元](../consume-packages/package-restore.md#restore-packages)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="9d9cb-107">プロジェクト ファイル ( *.csproj*) のパッケージ参照、または *packages.config* ファイルが正しくない ([パッケージの復元] 後に必要な状態と一致しない) 場合は、パッケージの復元を使う代わりにパッケージをインストールまたは更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="9d9cb-108">この記事の手順で問題が解決しない場合は、シナリオをより詳しく検討できるように、[GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="9d9cb-109">このページに [このページは役に立ちましたか]</span><span class="sxs-lookup"><span data-stu-id="9d9cb-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="9d9cb-110">コントロールが表示されている場合でも使用しないでください。このコントロールでは、お客様に詳細情報を確認することができません。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="9d9cb-111">Visual Studio ユーザー向けの簡単な解決方法</span><span class="sxs-lookup"><span data-stu-id="9d9cb-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="9d9cb-112">Visual Studio を使用している場合は、まず次のようにパッケージの復元を有効にします。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="9d9cb-113">それ以外の場合は、次のセクションに進みます。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="9d9cb-114">**[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー設定]** メニュー コマンドの順に選択します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="9d9cb-115">**[パッケージの復元]** の両方のオプションをオンにします。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="9d9cb-116">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-116">Select **OK**.</span></span>
1. <span data-ttu-id="9d9cb-117">プロジェクトをもう一度ビルドします。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-117">Build your project again.</span></span>

![[ツール]/[オプション] で NuGet パッケージの復元を有効にする](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="9d9cb-119">これらの設定は `NuGet.config` ファイルで変更することもできます。[同意](#consent)に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="9d9cb-120">ご自身のプロジェクトが、MSBuild に統合されたパッケージの復元を使用する以前のプロジェクトであった場合は、パッケージの自動復元に[移行](package-restore.md#migrate-to-automatic-package-restore-visual-studio)することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="9d9cb-121">このプロジェクトは、このコンピューターにはない NuGet パッケージを参照しています</span><span class="sxs-lookup"><span data-stu-id="9d9cb-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="9d9cb-122">詳細なエラー メッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="9d9cb-123">このエラーは、ビルドしようとしているプロジェクトに、現在コンピューターまたはプロジェクトにインストールされていない NuGet パッケージへの参照が 1 つ以上含まれている場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="9d9cb-124">[PackageReference](package-references-in-project-files.md) 管理形式を使用する場合、このエラーは、[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)に関する記事で説明されているように、パッケージが "*グローバル パッケージ*" フォルダーにインストールされていないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-124">When using the [PackageReference](package-references-in-project-files.md) management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="9d9cb-125">[packages.config](../reference/packages-config.md) を使用する場合、このエラーは、パッケージがソリューション ルートにある `packages` フォルダーにインストールされていないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="9d9cb-126">このような状況は、ソース管理や別のダウンロードからプロジェクトのソース コードを取得する場合によく発生します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="9d9cb-127">パッケージは、nuget.org のようなパッケージ フィードから復元できるので、通常はソース管理やダウンロードから除外されます ([パッケージとソース管理](Packages-and-Source-Control.md)に関するページを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="9d9cb-128">パッケージを含めると、リポジトリがいっぱいになったり、.zip ファイルが不必要に大きくなったりします。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="9d9cb-129">このエラーは、プロジェクト ファイルにパッケージの場所の絶対パスが含まれているとき、そのプロジェクトを移動した場合にも発生します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="9d9cb-130">パッケージを復元するには、次のいずれかの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="9d9cb-131">プロジェクト ファイルを移動した場合、ファイルを直接編集し、パッケージ参照を更新します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="9d9cb-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([自動復元](package-restore.md#restore-packages-automatically-using-visual-studio)または[手動復元](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="9d9cb-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="9d9cb-133">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="9d9cb-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="9d9cb-134">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="9d9cb-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="9d9cb-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="9d9cb-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="9d9cb-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="9d9cb-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="9d9cb-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="9d9cb-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="9d9cb-138">復元に成功したら、"*グローバル パッケージ*" フォルダーにパッケージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="9d9cb-139">PackageReference を使用するプロジェクトの場合、復元によって `obj/project.assets.json` ファイルが再び作成されます。`packages.config` を使用するプロジェクトの場合、プロジェクトの `packages` フォルダーにパッケージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="9d9cb-140">この場合、プロジェクトを正常にビルドできるようになります。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-140">The project should now build successfully.</span></span> <span data-ttu-id="9d9cb-141">ビルドできない場合は、フォローを受けられるように [GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="9d9cb-142">資産ファイル project.assets.json が見つかりません</span><span class="sxs-lookup"><span data-stu-id="9d9cb-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="9d9cb-143">詳細なエラー メッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="9d9cb-144">PackageReference 管理形式を使用する場合、`project.assets.json` ファイルによってプロジェクトの依存関係グラフが保持されます。このグラフを使用して、必要なパッケージがすべてコンピューターにインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="9d9cb-145">このファイルはパッケージの復元を通じて動的に生成されるため、通常はソース管理に追加されません。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="9d9cb-146">その結果、自動的にパッケージを復元しない `msbuild` などのツールでプロジェクトをビルドすると、このエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="9d9cb-147">この場合、`msbuild -t:restore` の後に `msbuild` を実行するか、`dotnet build` を使用します (これでパッケージが自動的に復元されます)。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="9d9cb-148">また、[前のセクション](#missing)のいずれかの方法を使用してパッケージを復元することもできます。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="9d9cb-149">1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした</span><span class="sxs-lookup"><span data-stu-id="9d9cb-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="9d9cb-150">詳細なエラー メッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="9d9cb-151">このエラーは、NuGet の構成でパッケージの復元が無効になっていることを示します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="9d9cb-152">「[Visual Studio ユーザー向けの簡単な解決方法](#quick-solution-for-visual-studio-users)」で前述したように、Visual Studio で該当する設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="9d9cb-153">これらの設定は、該当する `nuget.config` ファイル (通常、Windows では `%AppData%\NuGet\NuGet.Config`、Mac/Linux では `~/.nuget/NuGet/NuGet.Config`) で直接編集することもできます。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="9d9cb-154">`packageRestore` の `enabled` キーと `automatic` キーが True に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="9d9cb-155">`nuget.config` の `packageRestore` 設定を直接編集する場合は、オプションのダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="9d9cb-156">その他の考えられる条件</span><span class="sxs-lookup"><span data-stu-id="9d9cb-156">Other potential conditions</span></span>

- <span data-ttu-id="9d9cb-157">ファイルが見つからないため、NuGet の復元を使用してダウンロードするというメッセージのビルド エラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="9d9cb-158">ただし、復元を実行すると、"すべてのパッケージは既にインストールされており、復元するものはありません" と表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="9d9cb-159">この場合は、`packages` フォルダー (`packages.config` の使用時) または `obj/project.assets.json` ファイル (PackageReference の使用時) を削除し、復元を実行し直してください。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="9d9cb-160">エラーが引き続き発生する場合は、コマンドラインから `nuget locals all -clear` または `dotnet locals all --clear` を使用して、「[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)」で説明されているように、"*グローバル パッケージ*" フォルダーとキャッシュ フォルダーをクリアします。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-160">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="9d9cb-161">ソース管理からプロジェクトを取得するときに、プロジェクト フォルダーが読み取り専用に設定されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="9d9cb-162">フォルダーのアクセス許可を変更し、パッケージの復元を実行し直してください。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="9d9cb-163">古いバージョンの NuGet を使用している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="9d9cb-164">最新の推奨バージョンについては、[nuget.org/downloads](https://www.nuget.org/downloads) を確認してください。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="9d9cb-165">Visual Studio 2015 の場合は、3.6.0 をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="9d9cb-166">他の問題が発生している場合、詳細を確認できるように [GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。</span><span class="sxs-lookup"><span data-stu-id="9d9cb-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
