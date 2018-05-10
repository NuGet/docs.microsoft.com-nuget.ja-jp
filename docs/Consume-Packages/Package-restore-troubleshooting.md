---
title: Visual Studio での NuGet パッケージの復元に関するトラブルシューティング
description: Visual Studio の一般的な NuGet の復元エラーの説明とトラブルシューティングの方法です。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c552941c896d1a7136310c0a8bc6755d5974809a
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="d477e-103">パッケージの復元エラーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="d477e-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="d477e-104">この記事では、パッケージを復元するときの一般的なエラーと、それを解決する手順に重点を置いて説明しています。</span><span class="sxs-lookup"><span data-stu-id="d477e-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="d477e-105">パッケージの復元の詳細については、[パッケージの復元](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="d477e-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="d477e-106">この記事の手順で問題が解決しない場合は、シナリオをより詳しく検討できるように、[GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。</span><span class="sxs-lookup"><span data-stu-id="d477e-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="d477e-107">このページに [このページは役に立ちましたか]</span><span class="sxs-lookup"><span data-stu-id="d477e-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="d477e-108">コントロールが表示されている場合でも使用しないでください。このコントロールでは、お客様に詳細情報を確認することができません。</span><span class="sxs-lookup"><span data-stu-id="d477e-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="d477e-109">Visual Studio ユーザー向けの簡単な解決方法</span><span class="sxs-lookup"><span data-stu-id="d477e-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="d477e-110">Visual Studio を使用している場合は、まず次のようにパッケージの復元を有効にします。</span><span class="sxs-lookup"><span data-stu-id="d477e-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="d477e-111">それ以外の場合は、次のセクションに進みます。</span><span class="sxs-lookup"><span data-stu-id="d477e-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="d477e-112">**[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー設定]** メニュー コマンドの順に選択します。</span><span class="sxs-lookup"><span data-stu-id="d477e-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="d477e-113">**[パッケージの復元]** の両方のオプションをオンにします。</span><span class="sxs-lookup"><span data-stu-id="d477e-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="d477e-114">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d477e-114">Select **OK**.</span></span>
1. <span data-ttu-id="d477e-115">プロジェクトをもう一度ビルドします。</span><span class="sxs-lookup"><span data-stu-id="d477e-115">Build your project again.</span></span>

![[ツール]/[オプション] で NuGet パッケージの復元を有効にする](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="d477e-117">これらの設定は `NuGet.config` ファイルで変更することもできます。[同意](#consent)に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="d477e-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="d477e-118">このプロジェクトは、このコンピューターにはない NuGet パッケージを参照しています</span><span class="sxs-lookup"><span data-stu-id="d477e-118">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="d477e-119">詳細なエラー メッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d477e-119">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="d477e-120">このエラーは、ビルドしようとしているプロジェクトに、現在コンピューターまたはプロジェクトにインストールされていない NuGet パッケージへの参照が 1 つ以上含まれている場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="d477e-120">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="d477e-121">PackageReference 管理形式を使用する場合、このエラーは、「[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)」で説明されているように、パッケージが "*グローバル パッケージ*" フォルダーにインストールされていないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="d477e-121">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="d477e-122">`packages.config` を使用する場合、このエラーは、パッケージがソリューション ルートにある `packages` フォルダーにインストールされていないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="d477e-122">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="d477e-123">このような状況は、ソース管理や別のダウンロードからプロジェクトのソース コードを取得する場合によく発生します。</span><span class="sxs-lookup"><span data-stu-id="d477e-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="d477e-124">パッケージは、nuget.org のようなパッケージ フィードから復元できるので、通常はソース管理やダウンロードから除外されます ([パッケージとソース管理](Packages-and-Source-Control.md)に関するページを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="d477e-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="d477e-125">パッケージを含めると、リポジトリがいっぱいになったり、.zip ファイルが不必要に大きくなったりします。</span><span class="sxs-lookup"><span data-stu-id="d477e-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="d477e-126">パッケージを復元するには、次のいずれかの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="d477e-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="d477e-127">Visual Studio で、**[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー設定]** メニュー コマンドを選択し、**[パッケージの復元]** の両方のオプションをオンにして、**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d477e-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="d477e-128">ソリューションをもう一度ビルドします。</span><span class="sxs-lookup"><span data-stu-id="d477e-128">Then build the solution again.</span></span>
- <span data-ttu-id="d477e-129">.NET Core プロジェクトの場合は、`dotnet restore` または `dotnet build` (自動的に復元が実行されます) を実行します。</span><span class="sxs-lookup"><span data-stu-id="d477e-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="d477e-130">コマンド ラインで `nuget restore` を実行します (ただし、`dotnet restore` を使用する `dotnet` で作成されたプロジェクトは例外です)。</span><span class="sxs-lookup"><span data-stu-id="d477e-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="d477e-131">PackageReference 形式を使用するプロジェクトのコマンド ラインで、`msbuild /t:restore` を実行します。</span><span class="sxs-lookup"><span data-stu-id="d477e-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="d477e-132">復元に成功したら、"*グローバル パッケージ*" フォルダーにパッケージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d477e-132">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="d477e-133">PackageReference を使用するプロジェクトの場合、復元によって `obj/project.assets.json` ファイルが再び作成されます。`packages.config` を使用するプロジェクトの場合、プロジェクトの `packages` フォルダーにパッケージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d477e-133">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="d477e-134">この場合、プロジェクトを正常にビルドできるようになります。</span><span class="sxs-lookup"><span data-stu-id="d477e-134">The project should now build successfully.</span></span> <span data-ttu-id="d477e-135">ビルドできない場合は、フォローを受けられるように [GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。</span><span class="sxs-lookup"><span data-stu-id="d477e-135">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="d477e-136">資産ファイル project.assets.json が見つかりません</span><span class="sxs-lookup"><span data-stu-id="d477e-136">Assets file project.assets.json not found</span></span>

<span data-ttu-id="d477e-137">詳細なエラー メッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d477e-137">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="d477e-138">PackageReference 管理形式を使用する場合、`project.assets.json` ファイルによってプロジェクトの依存関係グラフが保持されます。このグラフを使用して、必要なパッケージがすべてコンピューターにインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d477e-138">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="d477e-139">このファイルはパッケージの復元を通じて動的に生成されるため、通常はソース管理に追加されません。</span><span class="sxs-lookup"><span data-stu-id="d477e-139">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="d477e-140">その結果、自動的にパッケージを復元しない `msbuild` などのツールでプロジェクトをビルドすると、このエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="d477e-140">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="d477e-141">この場合、`msbuild /t:restore` の後に `msbuild` を実行するか、`dotnet build` を使用します (これでパッケージが自動的に復元されます)。</span><span class="sxs-lookup"><span data-stu-id="d477e-141">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="d477e-142">また、[前のセクション](#missing)のいずれかの方法を使用してパッケージを復元することもできます。</span><span class="sxs-lookup"><span data-stu-id="d477e-142">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="d477e-143">1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした</span><span class="sxs-lookup"><span data-stu-id="d477e-143">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="d477e-144">詳細なエラー メッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d477e-144">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="d477e-145">このエラーは、NuGet の構成でパッケージの復元が無効になっていることを示します。</span><span class="sxs-lookup"><span data-stu-id="d477e-145">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="d477e-146">「[Visual Studio ユーザー向けの簡単な解決方法](#quick-solution-for-visual-studio-users)」で前述したように、Visual Studio で該当する設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="d477e-146">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="d477e-147">これらの設定は、該当する `nuget.config` ファイル (通常、Windows では `%AppData%\NuGet\NuGet.Config`、Mac/Linux では `~/.nuget/NuGet/NuGet.Config`) で直接編集することもできます。</span><span class="sxs-lookup"><span data-stu-id="d477e-147">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="d477e-148">`packageRestore` の `enabled` キーと `automatic` キーが True に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d477e-148">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="d477e-149">`nuget.config` の `packageRestore` 設定を直接編集する場合は、オプションのダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="d477e-149">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="d477e-150">その他の考えられる条件</span><span class="sxs-lookup"><span data-stu-id="d477e-150">Other potential conditions</span></span>

- <span data-ttu-id="d477e-151">ファイルが見つからないため、NuGet の復元を使用してダウンロードするというメッセージのビルド エラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="d477e-151">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="d477e-152">ただし、復元を実行すると、"すべてのパッケージは既にインストールされており、復元するものはありません" と表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="d477e-152">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="d477e-153">この場合は、`packages` フォルダー (`packages.config` の使用時) または `obj/project.assets.json` ファイル (PackageReference の使用時) を削除し、復元を実行し直してください。</span><span class="sxs-lookup"><span data-stu-id="d477e-153">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="d477e-154">エラーが引き続き発生する場合は、コマンドラインから `nuget locals all -clear` または `dotnet locals all --clear` を使用して、「[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)」で説明されているように、"*グローバル パッケージ*" フォルダーとキャッシュ フォルダーをクリアします。</span><span class="sxs-lookup"><span data-stu-id="d477e-154">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="d477e-155">ソース管理からプロジェクトを取得するときに、プロジェクト フォルダーが読み取り専用に設定されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d477e-155">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="d477e-156">フォルダーのアクセス許可を変更し、パッケージの復元を実行し直してください。</span><span class="sxs-lookup"><span data-stu-id="d477e-156">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="d477e-157">古いバージョンの NuGet を使用している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d477e-157">You may be using an old version of NuGet.</span></span> <span data-ttu-id="d477e-158">最新の推奨バージョンについては、[nuget.org/downloads](https://www.nuget.org/downloads) を確認してください。</span><span class="sxs-lookup"><span data-stu-id="d477e-158">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="d477e-159">Visual Studio 2015 の場合は、3.6.0 をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d477e-159">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="d477e-160">他の問題が発生している場合、詳細を確認できるように [GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。</span><span class="sxs-lookup"><span data-stu-id="d477e-160">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>