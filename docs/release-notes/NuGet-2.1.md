---
title: NuGet 2.1 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777028"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="9dd07-103">NuGet 2.1 リリースノート</span><span class="sxs-lookup"><span data-stu-id="9dd07-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="9dd07-104">[NuGet 2.0 リリースノート](../release-notes/nuget-2.0.md)  | [NuGet 2.2 リリースノート](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="9dd07-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="9dd07-105">NuGet 2.1 は、2012年10月4日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="9dd07-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="9dd07-106">階層 Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="9dd07-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="9dd07-107">NuGet 2.1 では、ファイルを検索するフォルダー構造を再帰的に調べ、検出され `NuGet.Config` たすべてのファイルのセットから構成を構築することで、nuget 設定をより柔軟に制御できます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="9dd07-108">例として、チームが他の内部依存関係の CI ビルドの内部パッケージリポジトリを持っている場合を考えてみます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="9dd07-109">個々のプロジェクトのフォルダー構造は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="9dd07-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="9dd07-110">また、ソリューションに対してパッケージの復元が有効になっている場合は、次のフォルダーも存在します。</span><span class="sxs-lookup"><span data-stu-id="9dd07-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="9dd07-111">チームが作業するすべてのプロジェクトでチームの内部パッケージリポジトリを使用できるようにするために、コンピューター上のすべてのプロジェクトで使用できるようにするのではなく、新しい Nuget.Config ファイルを作成し、c:\myteam フォルダーに配置することができます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="9dd07-112">プロジェクトごとにパッケージフォルダーを指定しすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9dd07-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="9dd07-113">次に示すように、c:\myteam の下にある任意のフォルダーから ' nuget.exe sources ' コマンドを実行して、ソースが追加されたことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![親 nuget 構成からのパッケージソース](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="9dd07-115">`NuGet.Config` ファイルは、次の順序で検索されます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="9dd07-116">プロジェクトフォルダーからルートへの再帰的なウォーク</span><span class="sxs-lookup"><span data-stu-id="9dd07-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="9dd07-117">Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="9dd07-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="9dd07-118">これらの構成は *逆順* で適用されます。つまり、上記の順序に基づいて、グローバル Nuget.Config が最初に適用され、その後、[ルートからプロジェクト] フォルダーから検出された Nuget.Config ファイルの後にが続き `.nuget\Nuget.Config` ます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="9dd07-119">これは、要素を使用して、 `<clear/>` 構成から一連の項目を削除する場合に特に重要です。</span><span class="sxs-lookup"><span data-stu-id="9dd07-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="9dd07-120">' パッケージ ' フォルダーの場所を指定します</span><span class="sxs-lookup"><span data-stu-id="9dd07-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="9dd07-121">以前は、NuGet は、ソリューションルートフォルダーの下にある既知の ' パッケージ ' フォルダーからソリューションのパッケージを管理していました。</span><span class="sxs-lookup"><span data-stu-id="9dd07-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="9dd07-122">NuGet パッケージがインストールされているさまざまなソリューションを持つ開発チームにとっては、ファイルシステム上のさまざまな場所に同じパッケージがインストールされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9dd07-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="9dd07-123">NuGet 2.1 では、ファイル内の要素を使用して、packages フォルダーの場所をより細かく制御 `repositoryPath` `NuGet.Config` できます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="9dd07-124">前の階層 Nuget.Config サポートの例を基にして、C:\myteam\ 下のすべてのプロジェクトで同じ packages フォルダーを共有することを想定しています。</span><span class="sxs-lookup"><span data-stu-id="9dd07-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="9dd07-125">これを実現するには、次のエントリをに追加 `c:\myteam\Nuget.Config` します。</span><span class="sxs-lookup"><span data-stu-id="9dd07-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="9dd07-126">この例では、共有 `Nuget.Config` ファイルは、深さに関係なく、C:\myteam の下に作成されるすべてのプロジェクトの [共有パッケージ] フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="9dd07-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="9dd07-127">ソリューションルートの下に既存の packages フォルダーがある場合は、NuGet によって新しい場所にパッケージが配置される前に、削除する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="9dd07-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="9dd07-128">ポータブルライブラリのサポート</span><span class="sxs-lookup"><span data-stu-id="9dd07-128">Support for Portable Libraries</span></span>

<span data-ttu-id="9dd07-129">[ポータブルライブラリ](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) は、.net 4 で初めて導入された機能です。この機能を使用すると、さまざまな Microsoft プラットフォームでの変更なしで動作するアセンブリを構築できます。これにより、the.NET Framework のバージョンから Silverlight へ、および xbox 360 を Windows Phone ことができます (現時点では、NuGet は xbox ポータブルライブラリターゲットをサポートしません)。</span><span class="sxs-lookup"><span data-stu-id="9dd07-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="9dd07-130">フレームワークのバージョンとプロファイルの [パッケージ規則](../create-packages/supporting-multiple-target-frameworks.md) を拡張することで、NuGet 2.1 では、複合フレームワークとプロファイルターゲットフォルダーを持つパッケージを作成できるようになり、ポータブルライブラリがサポートされるようになりました `lib` 。</span><span class="sxs-lookup"><span data-stu-id="9dd07-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="9dd07-131">例として、次のポータブルクラスライブラリの使用可能なターゲットプラットフォームを考えてみます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![ポータブルライブラリの作成ダイアログ](./media/releasenotes-21-plib.png)

<span data-ttu-id="9dd07-133">ライブラリをビルドしてコマンドを実行すると `nuget.exe pack MyPortableProject.csproj` 、生成された NuGet パッケージの内容を調べることによって、新しいポータブルライブラリパッケージのフォルダー構造を確認できます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![ポータブルライブラリパッケージのレイアウト](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="9dd07-135">ご覧のように、ポータブルライブラリのフォルダー名の規則は、"ポータブル-{framework 1} + {framework n}" のパターンに従います。この場合、フレームワークの識別子は既存の [フレームワーク名とバージョンの規則](../reference/target-frameworks.md)に従います。</span><span class="sxs-lookup"><span data-stu-id="9dd07-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="9dd07-136">名前とバージョンの規則の1つの例外は、Windows Phone に使用されるフレームワーク識別子にあります。</span><span class="sxs-lookup"><span data-stu-id="9dd07-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="9dd07-137">このモニカーは、フレームワーク名 ' wp ' (wp7、wp71、または wp8) を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9dd07-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="9dd07-138">たとえば、' wp7 ' を使用すると、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="9dd07-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="9dd07-139">このフォルダー構造から作成されたパッケージをインストールすると、NuGet によって、フォルダー名に指定されている複数のターゲットに対して、フレームワークとプロファイルルールが適用されるようになります。</span><span class="sxs-lookup"><span data-stu-id="9dd07-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="9dd07-140">NuGet の照合ルールの背後では、"より具体的な" ターゲットが "より具体的な" ものよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="9dd07-141">つまり、特定のプラットフォームを対象とするモニカーは、プロジェクトと互換性がある場合は常に移植可能なものよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="9dd07-142">さらに、複数のポータブルターゲットがプロジェクトと互換性がある場合、NuGet では、サポートされているプラットフォームのセットが、パッケージを参照しているプロジェクトに "最も近い" ものとして優先されます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="9dd07-143">Windows 8 および Windows Phone 8 プロジェクトを対象とする</span><span class="sxs-lookup"><span data-stu-id="9dd07-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="9dd07-144">NuGet 2.1 では、ポータブルライブラリプロジェクトを対象とするためのサポートを追加するだけでなく、Windows 8 ストアと Windows Phone 8 プロジェクトの新しいフレームワークモニカーに加えて、各プラットフォームの将来のバージョンで簡単に管理できる Windows ストアおよび Windows Phone プロジェクト用の新しい一般的なモニカーが提供されます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="9dd07-145">Windows 8 ストアアプリケーションの場合、識別子は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="9dd07-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="9dd07-146">NuGet 2.0 以前</span><span class="sxs-lookup"><span data-stu-id="9dd07-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="9dd07-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="9dd07-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="9dd07-148">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="9dd07-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="9dd07-149">Windows、Windows8、win、win8</span><span class="sxs-lookup"><span data-stu-id="9dd07-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="9dd07-150">Windows Phone プロジェクトの場合、識別子は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="9dd07-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="9dd07-151">電話 OS</span><span class="sxs-lookup"><span data-stu-id="9dd07-151">Phone OS</span></span> | <span data-ttu-id="9dd07-152">NuGet 2.0 以前</span><span class="sxs-lookup"><span data-stu-id="9dd07-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="9dd07-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="9dd07-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dd07-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="9dd07-154">Windows Phone 7</span></span> | <span data-ttu-id="9dd07-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="9dd07-155">silverlight3-wp</span></span> | <span data-ttu-id="9dd07-156">wp、wp7、Appname.windowsphone、WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="9dd07-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="9dd07-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="9dd07-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="9dd07-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="9dd07-158">silverlight4-wp71</span></span> | <span data-ttu-id="9dd07-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="9dd07-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="9dd07-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="9dd07-160">Windows Phone 8</span></span> | <span data-ttu-id="9dd07-161">(サポートされていません)</span><span class="sxs-lookup"><span data-stu-id="9dd07-161">(not supported)</span></span> | <span data-ttu-id="9dd07-162">wp8、WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="9dd07-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="9dd07-163">上記のすべての変更では、以前のフレームワーク名は引き続き NuGet 2.1 によって完全にサポートされます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="9dd07-164">今後は、新しい名前を使用する必要があります。これらの名前は、各プラットフォームの将来のバージョンでより安定しています。</span><span class="sxs-lookup"><span data-stu-id="9dd07-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="9dd07-165">ただし、2.1 より前のバージョンの NuGet では、新しい名前はサポートされ *ません* 。そのため、スイッチを作成するタイミングに応じて計画を立ててください。</span><span class="sxs-lookup"><span data-stu-id="9dd07-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="9dd07-166">パッケージマネージャーダイアログの検索機能の向上</span><span class="sxs-lookup"><span data-stu-id="9dd07-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="9dd07-167">過去数回のイテレーションでは、パッケージ検索の速度と関連性を大幅に向上させる変更が NuGet ギャラリーに導入されました。</span><span class="sxs-lookup"><span data-stu-id="9dd07-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="9dd07-168">ただし、これらの機能強化は nuget.org の Web サイトに限定されていました。</span><span class="sxs-lookup"><span data-stu-id="9dd07-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="9dd07-169">Nuget 2.1 では、[NuGet パッケージマネージャー] ダイアログボックスで検索エクスペリエンスが向上しています。</span><span class="sxs-lookup"><span data-stu-id="9dd07-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="9dd07-170">例として、Windows Azure キャッシュプレビューパッケージを検索する場合を考えてみます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="9dd07-171">このパッケージに対する適切な検索クエリは、"Azure Cache" にすることができます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="9dd07-172">以前のバージョンの [パッケージマネージャー] ダイアログでは、必要なパッケージが結果の最初のページに表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="9dd07-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="9dd07-173">ただし、NuGet 2.1 では、必要なパッケージが検索結果の先頭に表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="9dd07-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![パッケージマネージャーダイアログ検索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="9dd07-175">パッケージの更新を強制する</span><span class="sxs-lookup"><span data-stu-id="9dd07-175">Force Package Update</span></span>

<span data-ttu-id="9dd07-176">NuGet 2.1 より前では、バージョン番号が大きくない場合、NuGet はパッケージの更新をスキップします。</span><span class="sxs-lookup"><span data-stu-id="9dd07-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="9dd07-177">これにより、特に、チームが各ビルドでパッケージのバージョン番号をインクリメントしたくないビルドまたは CI シナリオの場合に、特定のシナリオに対する摩擦が発生しました。</span><span class="sxs-lookup"><span data-stu-id="9dd07-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="9dd07-178">必要な動作は、に関係なく更新を強制することでした。</span><span class="sxs-lookup"><span data-stu-id="9dd07-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="9dd07-179">NuGet 2.1 では、' 再インストール ' フラグを使用してこれに対処します。</span><span class="sxs-lookup"><span data-stu-id="9dd07-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="9dd07-180">たとえば、以前のバージョンの NuGet では、より新しいパッケージバージョンがないパッケージを更新しようとすると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="9dd07-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="9dd07-181">再インストールフラグを使用すると、新しいバージョンがあるかどうかに関係なくパッケージが更新されます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="9dd07-182">再インストールフラグが役立つもう1つのシナリオとして、フレームワークの再ターゲット設定があります。</span><span class="sxs-lookup"><span data-stu-id="9dd07-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="9dd07-183">プロジェクトのターゲットフレームワーク (たとえば、.NET 4 から .NET 4.5) を変更すると、Update-Package 再インストールによって、プロジェクトにインストールされているすべての NuGet パッケージの正しいアセンブリへの参照を更新できます。</span><span class="sxs-lookup"><span data-stu-id="9dd07-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="9dd07-184">Visual Studio 内でパッケージソースを編集する</span><span class="sxs-lookup"><span data-stu-id="9dd07-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="9dd07-185">以前のバージョンの NuGet では、Visual Studio の [オプション] ダイアログ内からパッケージソースを更新するには、パッケージソースの削除と再追加が必要でした。</span><span class="sxs-lookup"><span data-stu-id="9dd07-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="9dd07-186">NuGet 2.1 は、構成ユーザーインターフェイスの最初のクラス関数として update をサポートすることで、このワークフローを改善します。</span><span class="sxs-lookup"><span data-stu-id="9dd07-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![パッケージマネージャーの構成ダイアログ](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="9dd07-188">バグの修正</span><span class="sxs-lookup"><span data-stu-id="9dd07-188">Bug Fixes</span></span>

<span data-ttu-id="9dd07-189">NuGet 2.1 には、多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="9dd07-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="9dd07-190">NuGet 2.0 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9dd07-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
