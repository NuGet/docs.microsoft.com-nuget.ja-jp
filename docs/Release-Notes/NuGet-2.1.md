---
title: NuGet 2.1 リリース ノート |Microsoft ドキュメント
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.1 リリース ノートです。
keywords: NuGet 2.1 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 06116a86887b5561ad4e2ecad8090222d16cd333
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="33554-104">NuGet 2.1 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="33554-104">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="33554-105">[NuGet 2.0 リリース ノート](../release-notes/nuget-2.0.md) | [NuGet 2.2 リリース ノート](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="33554-105">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="33554-106">NuGet 2.1 は、2012 年 10 月 4 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="33554-106">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="33554-107">Nuget.Config の階層</span><span class="sxs-lookup"><span data-stu-id="33554-107">Hierarchical Nuget.Config</span></span>
<span data-ttu-id="33554-108">NuGet 2.1 では、再帰的に探して、フォルダー構造のウォークを使用して NuGet 設定の制御をより柔軟`NuGet.Config`ファイルとし、見つかったすべてのファイルのセットから構成をビルドします。</span><span class="sxs-lookup"><span data-stu-id="33554-108">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="33554-109">たとえば、チームが、内部のパッケージ リポジトリの他の内部の依存関係の CI ビルドを持つシナリオを考えます。</span><span class="sxs-lookup"><span data-stu-id="33554-109">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="33554-110">個々 のプロジェクトのフォルダー構造は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="33554-110">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="33554-111">さらに、パッケージの復元がソリューションの有効な場合、次のフォルダーも存在されます。</span><span class="sxs-lookup"><span data-stu-id="33554-111">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="33554-112">が使用できるようにすべてのプロジェクトのマシンで、中に、チームが機能するすべてのプロジェクトで使用できるチームの内部のパッケージ リポジトリを利用するには、新しい Nuget.Config ファイルを作成し、c:\myteam フォルダーに配置することおことができません。</span><span class="sxs-lookup"><span data-stu-id="33554-112">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="33554-113">方法がないを指定し、プロジェクトごとの [パッケージ] フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="33554-113">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="33554-114">次に示すように c:\myteam 下にある任意のフォルダーから 'nuget.exe ソース' コマンドを実行して、ソースが追加されたことことがわかります。</span><span class="sxs-lookup"><span data-stu-id="33554-114">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![親の nuget 構成からのパッケージ ソース](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="33554-116">`NuGet.Config` 次の順序でのファイルが検索されます。</span><span class="sxs-lookup"><span data-stu-id="33554-116">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="33554-117">再帰がルート プロジェクト フォルダーからウォークします。</span><span class="sxs-lookup"><span data-stu-id="33554-117">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="33554-118">グローバル`Nuget.Config`(`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="33554-118">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="33554-119">この構成は、適用により、*の逆順*、上記の順序に基づくことを意味するには、グローバル Nuget.Config はするが最初に適用、後に、検出された Nuget.Config ファイルのルートからプロジェクトのフォルダーに、その後によって`.nuget\Nuget.Config`です。</span><span class="sxs-lookup"><span data-stu-id="33554-119">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="33554-120">これは、使用する場合に特に重要な`<clear/>`構成から一連の項目を削除する要素。</span><span class="sxs-lookup"><span data-stu-id="33554-120">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="33554-121">'Packages' フォルダーの場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="33554-121">Specify ‘packages’ Folder Location</span></span>
<span data-ttu-id="33554-122">以前は、NuGet は、ソリューションのルート フォルダーの下に見つかった既知 'packages' フォルダーからソリューションのパッケージを管理するがします。</span><span class="sxs-lookup"><span data-stu-id="33554-122">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="33554-123">インストールされている NuGet パッケージである必要が多くのさまざまなソリューションを持っている開発チームの場合は、ファイル システム上のさまざまな場所にインストールされる同じパッケージになります。</span><span class="sxs-lookup"><span data-stu-id="33554-123">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="33554-124">NuGet 2.1 を使用して、[パッケージ] フォルダーの場所をより細かく制御を提供する、`repositoryPath`内の要素、`NuGet.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="33554-124">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="33554-125">Nuget.Config の階層のサポートの前の例でのビルドでは、C:\myteam\ 共有、同じパッケージ フォルダーの下のすべてのプロジェクトがあるたいことを前提としています。</span><span class="sxs-lookup"><span data-stu-id="33554-125">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="33554-126">これを行うには、単に次のエントリを追加`c:\myteam\Nuget.Config`です。</span><span class="sxs-lookup"><span data-stu-id="33554-126">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="33554-127">この例では、共有で`Nuget.Config`ファイルの深さに関係なく C:\myteam の下に作成されるすべてのプロジェクトの共有のパッケージ フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="33554-127">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="33554-128">場合は、ソリューションのルートの下の既存のパッケージ フォルダーにある場合は、NuGet は、新しい場所にパッケージを配置前に削除する必要がありますに注意してください。</span><span class="sxs-lookup"><span data-stu-id="33554-128">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="33554-129">ポータブル ライブラリのサポート</span><span class="sxs-lookup"><span data-stu-id="33554-129">Support for Portable Libraries</span></span>
<span data-ttu-id="33554-130">[ポータブル ライブラリ](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)Silverlight は、Windows Phone およびでも Xbox に.net Framework のバージョンからのさまざまな Microsoft プラットフォームでの変更なしで使用できるようにアセンブリをビルドすることができます .NET 4 で初めて導入された機能です360 (ただし、現時点では、NuGet は、Xbox ポータブル ライブラリのターゲットをサポートしていません)。</span><span class="sxs-lookup"><span data-stu-id="33554-130">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="33554-131">拡張することによって、[規則をパッケージ化](../create-packages/supporting-multiple-target-frameworks.md)framework のバージョンとプロファイルは、NuGet 2.1 では、ポータブル ライブラリを複合フレームワークとプロファイルのターゲットを持つパッケージを作成することによって`lib`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="33554-131">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="33554-132">たとえば、次のポータブル クラス ライブラリの使用可能なターゲット プラットフォームを検討してください。</span><span class="sxs-lookup"><span data-stu-id="33554-132">As an example, consider the following portable class library’s available target platforms.</span></span>

![ポータブル ライブラリの作成 ダイアログ ボックス](./media/releasenotes-21-plib.png)

<span data-ttu-id="33554-134">ライブラリをビルドした後とコマンド`nuget.exe pack MyPortableProject.csproj`実行すると、新しい、移植可能なライブラリのパッケージ フォルダーの構造を表示するには、生成された NuGet パッケージの内容が検査をします。</span><span class="sxs-lookup"><span data-stu-id="33554-134">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![ポータブル ライブラリ パッケージのレイアウト](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="33554-136">ご覧のように、ポータブル ライブラリ フォルダーの名前規則、パターンに従う 'ポータブル {フレームワーク 1} + framework {n}' フレームワーク識別子は、既存に従う、[フレームワークの名前とバージョン規則](../reference/target-frameworks.md)です。</span><span class="sxs-lookup"><span data-stu-id="33554-136">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="33554-137">Windows Phone を使用するフレームワーク識別子の名前とバージョンの規則に 1 つの例外はあります。</span><span class="sxs-lookup"><span data-stu-id="33554-137">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="33554-138">このモニカーは、フレームワーク名 'wp' (wp7、wp71 または wp8) を使用してください。</span><span class="sxs-lookup"><span data-stu-id="33554-138">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="33554-139">' Silverlight-wp7' を使用してなどのエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="33554-139">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="33554-140">このフォルダー構造から作成されたパッケージをインストールするときに NuGet がフォルダー名で指定されている複数の対象にそのフレームワークとプロファイルのルールを適用できますようになりました。</span><span class="sxs-lookup"><span data-stu-id="33554-140">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="33554-141">NuGet の照合ルールの背後にある、「特定」のターゲットが優先される「汎用性」の原則です。</span><span class="sxs-lookup"><span data-stu-id="33554-141">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="33554-142">つまり、こと、特定のプラットフォームを対象とするモニカーは常によりも優先されるポータブルのどちらもプロジェクトに互換性がある場合。</span><span class="sxs-lookup"><span data-stu-id="33554-142">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="33554-143">さらに、複数のターゲットをポータブル プロジェクトと互換性のある場合は、NuGet をここでサポートされているプラットフォームの設定は、パッケージを参照しているプロジェクトに「最も近い」のいずれかを選びます。</span><span class="sxs-lookup"><span data-stu-id="33554-143">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="33554-144">ターゲットの Windows 8 および Windows Phone 8 プロジェクト</span><span class="sxs-lookup"><span data-stu-id="33554-144">Targeting Windows 8 and Windows Phone 8 Projects</span></span>
<span data-ttu-id="33554-145">ポータブル ライブラリ プロジェクトを対象とするサポートを追加するだけでなく NuGet 2.1 では、新しいフレームワーク モニカー Windows 8 ストアおよび Windows Phone 8 の両方のプロジェクトと Windows ストアおよび Windows Phone プロジェクトとなる新しいによって一般的なモニカーそれぞれのプラットフォームの将来のバージョン間での管理が容易です。</span><span class="sxs-lookup"><span data-stu-id="33554-145">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="33554-146">Windows 8 ストア アプリケーションの場合は、識別子は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="33554-146">For Windows 8 Store applications, the identifiers look as follows:</span></span>

|<span data-ttu-id="33554-147">NuGet 2.0 およびそれ以前</span><span class="sxs-lookup"><span data-stu-id="33554-147">NuGet 2.0 and earlier</span></span>|<span data-ttu-id="33554-148">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="33554-148">NuGet 2.1</span></span>|
|----------------|-----------|
|<span data-ttu-id="33554-149">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="33554-149">winRT45, .NETCore45</span></span>|<span data-ttu-id="33554-150">Windows、windows 8、win、win8</span><span class="sxs-lookup"><span data-stu-id="33554-150">Windows, Windows8, win, win8</span></span>|

<br/>
<span data-ttu-id="33554-151">Windows Phone プロジェクトの場合は、識別子は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="33554-151">For Windows Phone projects, the identifiers look as follows:</span></span>

|<span data-ttu-id="33554-152">電話の OS</span><span class="sxs-lookup"><span data-stu-id="33554-152">Phone OS</span></span>|<span data-ttu-id="33554-153">NuGet 2.0 およびそれ以前</span><span class="sxs-lookup"><span data-stu-id="33554-153">NuGet 2.0 and earlier</span></span>|<span data-ttu-id="33554-154">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="33554-154">NuGet 2.1</span></span>
|----------------|-----------|-----------|
|<span data-ttu-id="33554-155">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="33554-155">Windows Phone 7</span></span>|<span data-ttu-id="33554-156">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="33554-156">silverlight3-wp</span></span>|<span data-ttu-id="33554-157">wp、wp7、WindowsPhone、WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="33554-157">wp, wp7, WindowsPhone, WindowsPhone7</span></span>|
|<span data-ttu-id="33554-158">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="33554-158">Windows Phone 7.5 (Mango)</span></span>|<span data-ttu-id="33554-159">silverilght4-wp71</span><span class="sxs-lookup"><span data-stu-id="33554-159">silverilght4-wp71</span></span>|<span data-ttu-id="33554-160">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="33554-160">wp71, WindowsPhone71</span></span>|
|<span data-ttu-id="33554-161">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="33554-161">Windows Phone 8</span></span>|<span data-ttu-id="33554-162">(サポートされていません)</span><span class="sxs-lookup"><span data-stu-id="33554-162">(not supported)</span></span>|<span data-ttu-id="33554-163">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="33554-163">wp8, WindowsPhone8</span></span>|
<br/>
<span data-ttu-id="33554-164">上記の変更は、すべての framework の古い名前は引き続き NuGet 2.1 によって完全にサポートします。</span><span class="sxs-lookup"><span data-stu-id="33554-164">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="33554-165">さらに、新しい名前を付けるなるのでより安定したそれぞれのプラットフォームの将来のバージョン間でします。</span><span class="sxs-lookup"><span data-stu-id="33554-165">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="33554-166">新しい名前は*いない*する NuGet の 2.1 以前のバージョンでサポートされている、ただし、適切に計画、スイッチを作成する際のです。</span><span class="sxs-lookup"><span data-stu-id="33554-166">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="33554-167">パッケージ マネージャー ダイアログ ボックスに検索機能の向上</span><span class="sxs-lookup"><span data-stu-id="33554-167">Improved Search in Package Manager Dialog</span></span>
<span data-ttu-id="33554-168">過去のいくつかのイテレーションにおける速度とパッケージの検索の妥当性が大幅に向上 NuGet ギャラリーへの変更が導入されました。</span><span class="sxs-lookup"><span data-stu-id="33554-168">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="33554-169">ただし、これらの機能強化は、nuget.org の Web サイトに限られていました。</span><span class="sxs-lookup"><span data-stu-id="33554-169">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="33554-170">NuGet 2.1 では、エクスペリエンスの強化された検索を NuGet パッケージ マネージャー ダイアログ ボックスを通じて利用できます。</span><span class="sxs-lookup"><span data-stu-id="33554-170">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="33554-171">たとえば、Windows Azure キャッシュ プレビュー パッケージを検索するようにしたい想像してください。</span><span class="sxs-lookup"><span data-stu-id="33554-171">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="33554-172">このパッケージの適切な検索クエリには、"Azure Cache"可能性があります。</span><span class="sxs-lookup"><span data-stu-id="33554-172">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="33554-173">以前のバージョンのパッケージ マネージャー ダイアログでは、目的のパッケージもリストされません結果の最初のページにします。</span><span class="sxs-lookup"><span data-stu-id="33554-173">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="33554-174">ただし、NuGet 2.1 で目的のパッケージに表示されます、検索結果の上部にあります。</span><span class="sxs-lookup"><span data-stu-id="33554-174">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![パッケージ マネージャー ダイアログの検索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="33554-176">パッケージの更新を強制します。</span><span class="sxs-lookup"><span data-stu-id="33554-176">Force Package Update</span></span>
<span data-ttu-id="33554-177">NuGet NuGet 2.1 では、前に、not があったときに、パッケージの更新をスキップは指定された高いバージョン番号。</span><span class="sxs-lookup"><span data-stu-id="33554-177">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="33554-178">これには、ここで、チームを必要としないパッケージのバージョンをビルドするたびに数値をインクリメント ビルドまたは CI シナリオの場合は特に – 特定のシナリオの摩擦が導入されました。</span><span class="sxs-lookup"><span data-stu-id="33554-178">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="33554-179">目的の動作を強制的に更新に関係なくでした。</span><span class="sxs-lookup"><span data-stu-id="33554-179">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="33554-180">NuGet 2.1 は、これを 'を再インストール' フラグに対処します。</span><span class="sxs-lookup"><span data-stu-id="33554-180">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="33554-181">たとえば、以前のバージョンの NuGet 結果は、次にパッケージのより新しいバージョンがないパッケージを更新しようとするとき。</span><span class="sxs-lookup"><span data-stu-id="33554-181">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="33554-182">かどうかに関係なく、再インストール フラグで、パッケージが更新されて新しいバージョンが存在します。</span><span class="sxs-lookup"><span data-stu-id="33554-182">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="33554-183">もう 1 つのシナリオを再インストール フラグが便利では、フレームワークが再ターゲットのされます。</span><span class="sxs-lookup"><span data-stu-id="33554-183">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="33554-184">(たとえば、.NET 4 から .NET 4.5)、プロジェクトのターゲット フレームワークを変更するときに更新プログラム パッケージの再インストールするプロジェクトにインストールされているすべての NuGet パッケージの正しいアセンブリへの参照を更新できます。</span><span class="sxs-lookup"><span data-stu-id="33554-184">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="33554-185">Visual Studio 内でのパッケージ ソースを編集します。</span><span class="sxs-lookup"><span data-stu-id="33554-185">Edit Package Sources Within Visual Studio</span></span>
<span data-ttu-id="33554-186">NuGet の以前のバージョンで削除して、パッケージ ソースを再追加するために必要な Visual Studio のオプション ダイアログ内からパッケージ ソースを更新しています。</span><span class="sxs-lookup"><span data-stu-id="33554-186">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="33554-187">NuGet 2.1 では、構成のユーザー インターフェイスのファースト クラスの関数として更新をサポートすることによりこのワークフローが向上します。</span><span class="sxs-lookup"><span data-stu-id="33554-187">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![パッケージ マネージャーの構成 ダイアログ](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="33554-189">バグ修正</span><span class="sxs-lookup"><span data-stu-id="33554-189">Bug Fixes</span></span>
<span data-ttu-id="33554-190">NuGet 2.1 には、多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="33554-190">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="33554-191">作業の完全な一覧の項目で修正 NuGet 2.0 では、くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="33554-191">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
