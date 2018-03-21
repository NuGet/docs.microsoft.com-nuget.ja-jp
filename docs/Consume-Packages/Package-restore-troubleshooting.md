---
title: "Visual Studio での NuGet パッケージの復元に関するトラブルシューティング | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Visual Studio の一般的な NuGet の復元エラーの説明とトラブルシューティングの方法です。"
keywords: "NuGet パッケージの復元、パッケージの復元、トラブルシューティング、問題解決"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="5922e-104">パッケージの復元エラーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="5922e-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="5922e-105">この記事では、パッケージを復元するときの一般的なエラーと、それを解決する手順に重点を置いて説明しています。</span><span class="sxs-lookup"><span data-stu-id="5922e-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="5922e-106">パッケージの復元の詳細については、[パッケージの復元](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5922e-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="5922e-107">この記事の手順で問題が解決しない場合は、シナリオをより詳しく検討できるように、[GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。</span><span class="sxs-lookup"><span data-stu-id="5922e-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="5922e-108">このページに [このページは役に立ちましたか]</span><span class="sxs-lookup"><span data-stu-id="5922e-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="5922e-109">コントロールが表示されている場合でも使用しないでください。このコントロールでは、お客様に詳細情報を確認することができません。</span><span class="sxs-lookup"><span data-stu-id="5922e-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="5922e-110">Visual Studio ユーザー向けの簡単な解決方法</span><span class="sxs-lookup"><span data-stu-id="5922e-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="5922e-111">Visual Studio を使用している場合は、まず次のようにパッケージの復元を有効にします。</span><span class="sxs-lookup"><span data-stu-id="5922e-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="5922e-112">それ以外の場合は、次のセクションに進みます。</span><span class="sxs-lookup"><span data-stu-id="5922e-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="5922e-113">**[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー設定]** メニュー コマンドの順に選択します。</span><span class="sxs-lookup"><span data-stu-id="5922e-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="5922e-114">**[パッケージの復元]** の両方のオプションをオンにします。</span><span class="sxs-lookup"><span data-stu-id="5922e-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="5922e-115">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5922e-115">Select **OK**.</span></span>
1. <span data-ttu-id="5922e-116">プロジェクトをもう一度ビルドします。</span><span class="sxs-lookup"><span data-stu-id="5922e-116">Build your project again.</span></span>

![[ツール]/[オプション] で NuGet パッケージの復元を有効にする](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="5922e-118">これらの設定は `NuGet.config` ファイルで変更することもできます。[同意](#consent)に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5922e-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="5922e-119">このプロジェクトは、このコンピューターにはない NuGet パッケージを参照しています</span><span class="sxs-lookup"><span data-stu-id="5922e-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="5922e-120">詳細なエラー メッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5922e-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="5922e-121">このエラーは、1 つ以上の NuGet パッケージの参照を含むプロジェクトをビルドしようとしましたが、それらのパッケージが現在プロジェクトにキャッシュされていないことを示します</span><span class="sxs-lookup"><span data-stu-id="5922e-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently cached in the project.</span></span> <span data-ttu-id="5922e-122">(パッケージは、プロジェクトが `packages.config` を使用する場合はソリューション ルートの `packages` フォルダーにキャッシュされ、プロジェクトが PackageReference 形式を使用する場合は `obj/project.assets.json` ファイルにキャッシュされます)。</span><span class="sxs-lookup"><span data-stu-id="5922e-122">(Packages are cached in a `packages` folder at the solution root if the project uses `packages.config`, or in the `obj/project.assets.json` file if the project uses the PackageReference format.)</span></span>

<span data-ttu-id="5922e-123">このような状況は、ソース管理や別のダウンロードからプロジェクトのソース コードを取得する場合によく発生します。</span><span class="sxs-lookup"><span data-stu-id="5922e-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="5922e-124">パッケージは、nuget.org のようなパッケージ フィードから復元できるので、通常はソース管理やダウンロードから除外されます ([パッケージとソース管理](Packages-and-Source-Control.md)に関するページを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="5922e-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="5922e-125">パッケージを含めると、リポジトリがいっぱいになったり、.zip ファイルが不必要に大きくなったりします。</span><span class="sxs-lookup"><span data-stu-id="5922e-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="5922e-126">パッケージを復元するには、次のいずれかの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="5922e-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="5922e-127">Visual Studio で、**[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー設定]** メニュー コマンドを選択し、**[パッケージの復元]** の両方のオプションをオンにして、**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5922e-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="5922e-128">ソリューションをもう一度ビルドします。</span><span class="sxs-lookup"><span data-stu-id="5922e-128">Then build the solution again.</span></span>
- <span data-ttu-id="5922e-129">.NET Core プロジェクトの場合は、`dotnet restore` または `dotnet build` (自動的に復元が実行されます) を実行します。</span><span class="sxs-lookup"><span data-stu-id="5922e-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="5922e-130">コマンド ラインで `nuget restore` を実行します (ただし、`dotnet restore` を使用する `dotnet` で作成されたプロジェクトは例外です)。</span><span class="sxs-lookup"><span data-stu-id="5922e-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="5922e-131">PackageReference 形式を使用するプロジェクトのコマンド ラインで、`msbuild /t:restore` を実行します。</span><span class="sxs-lookup"><span data-stu-id="5922e-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="5922e-132">復元が成功すると、`packages` フォルダー (`packages.config` の使用時) または `obj/project.assets.json` ファイル (PackageReference の使用時) のいずれかが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5922e-132">After a successful restore, you should see either a `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference).</span></span> <span data-ttu-id="5922e-133">この場合、プロジェクトを正常にビルドできるようになります。</span><span class="sxs-lookup"><span data-stu-id="5922e-133">The project should now build successfully.</span></span> <span data-ttu-id="5922e-134">ビルドできない場合は、フォローを受けられるように [GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。</span><span class="sxs-lookup"><span data-stu-id="5922e-134">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="5922e-135">資産ファイル project.assets.json が見つかりません</span><span class="sxs-lookup"><span data-stu-id="5922e-135">Assets file project.assets.json not found</span></span>

<span data-ttu-id="5922e-136">詳細なエラー メッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5922e-136">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="5922e-137">このエラーは、[前のセクション](#missing)で説明したエラーと同じ理由で発生し、同じ救済手段を利用できます。</span><span class="sxs-lookup"><span data-stu-id="5922e-137">This error occurs for the same reasons as explained in the [previous section](#missing), and has the same remedies.</span></span> <span data-ttu-id="5922e-138">たとえば、ソース管理から取得した .NET Core プロジェクトで `msbuild` を実行しても、パッケージは自動的に復元されません。</span><span class="sxs-lookup"><span data-stu-id="5922e-138">For example, running `msbuild` on a .NET Core project that's been obtained from source control won't automatically restore packages.</span></span> <span data-ttu-id="5922e-139">この場合、`msbuild /t:restore` の後に `msbuild` を実行するか、`dotnet build` を使用します (これでパッケージが自動的に復元されます)。</span><span class="sxs-lookup"><span data-stu-id="5922e-139">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="5922e-140">1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした</span><span class="sxs-lookup"><span data-stu-id="5922e-140">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="5922e-141">詳細なエラー メッセージは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5922e-141">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="5922e-142">このエラーは、NuGet の構成でパッケージの復元が無効になっていることを示します。</span><span class="sxs-lookup"><span data-stu-id="5922e-142">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="5922e-143">「[Visual Studio ユーザー向けの簡単な解決方法](#quick-solution-for-visual-studio-users)」で前述したように、Visual Studio で該当する設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="5922e-143">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="5922e-144">これらの設定は、該当する `nuget.config` ファイル (通常、Windows では `%AppData%\NuGet\NuGet.Config`、Mac/Linux では `~/.nuget/NuGet/NuGet.Config`) で直接編集することもできます。</span><span class="sxs-lookup"><span data-stu-id="5922e-144">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="5922e-145">`packageRestore` の `enabled` キーと `automatic` キーが True に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5922e-145">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="5922e-146">`nuget.config` の `packageRestore` 設定を直接編集する場合は、オプションのダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="5922e-146">Note that if you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="5922e-147">その他の考えられる条件</span><span class="sxs-lookup"><span data-stu-id="5922e-147">Other potential conditions</span></span>

- <span data-ttu-id="5922e-148">ファイルが見つからないため、NuGet の復元を使用してダウンロードするというメッセージのビルド エラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="5922e-148">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="5922e-149">ただし、復元を実行すると、"すべてのパッケージは既にインストールされており、復元するものはありません" と表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="5922e-149">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="5922e-150">この場合は、`packages` フォルダー (`packages.config` の使用時) または `obj/project.assets.json` ファイル (PackageReference の使用時) を削除し、復元を実行し直してください。</span><span class="sxs-lookup"><span data-stu-id="5922e-150">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span>

- <span data-ttu-id="5922e-151">ソース管理からプロジェクトを取得するときに、プロジェクト フォルダーが読み取り専用に設定されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5922e-151">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="5922e-152">フォルダーのアクセス許可を変更し、パッケージの復元を実行し直してください。</span><span class="sxs-lookup"><span data-stu-id="5922e-152">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="5922e-153">古いバージョンの NuGet を使用している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5922e-153">You may be using an old version of NuGet.</span></span> <span data-ttu-id="5922e-154">最新の推奨バージョンについては、[nuget.org/downloads](https://www.nuget.org/downloads) を確認してください。</span><span class="sxs-lookup"><span data-stu-id="5922e-154">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="5922e-155">Visual Studio 2015 の場合は、3.6.0 をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5922e-155">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="5922e-156">他の問題が発生している場合、詳細を確認できるように [GitHub で問題を報告してください](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。</span><span class="sxs-lookup"><span data-stu-id="5922e-156">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>