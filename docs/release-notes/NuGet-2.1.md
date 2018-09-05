---
title: NuGet 2.1 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 2.1 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548598"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="7fb5c-103">NuGet 2.1 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="7fb5c-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="7fb5c-104">[NuGet 2.0 のリリース ノート](../release-notes/nuget-2.0.md) | [NuGet 2.2 リリース ノート](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="7fb5c-105">NuGet 2.1 は、2012 年 10 月 4 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="7fb5c-106">Nuget.Config の階層</span><span class="sxs-lookup"><span data-stu-id="7fb5c-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="7fb5c-107">NuGet 2.1 には探してフォルダー構造をウォークを再帰的に使用して NuGet の設定を制御するのには柔軟性が高まります`NuGet.Config`ファイルとし、見つかったすべてのファイルのセットから構成を構築します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="7fb5c-108">たとえば、チームの他の内部の依存関係の CI ビルド、パッケージの内部リポジトリがあるシナリオを検討してください。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="7fb5c-109">個々 のプロジェクトのフォルダー構造は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="7fb5c-110">さらに、ソリューションのパッケージの復元が有効な場合、次のフォルダーも存在します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="7fb5c-111">チームがいない利用できるようにすべてのプロジェクトのコンピューターの中には、すべてのプロジェクトで使用できるチームの内部のパッケージのリポジトリを確保するために新しい Nuget.Config ファイルを作成し、c:\myteam フォルダーに配置。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="7fb5c-112">方法はありませんに指定し、プロジェクトごとの [パッケージ] フォルダー。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="7fb5c-113">次に示すように c:\myteam 下にある任意のフォルダーから 'nuget.exe ソース' コマンドを実行して、ソースが追加されたことことがわかります。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![親の nuget 構成からパッケージ ソース](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="7fb5c-115">`NuGet.Config` 次の順序でのファイルが検索されます。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="7fb5c-116">ルート プロジェクト フォルダーから再帰がについて説明します</span><span class="sxs-lookup"><span data-stu-id="7fb5c-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="7fb5c-117">グローバル`Nuget.Config`(`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="7fb5c-118">この構成は、適用により、*の逆順*、上記の順序に基づくことを意味するには、全体の Nuget.Config が最初に適用される検出された Nuget.Config ファイル ルートからプロジェクト フォルダーに、後にによって`.nuget\Nuget.Config`します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="7fb5c-119">これは、使用する場合に特に重要な`<clear/>`構成から一連の項目を削除する要素。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="7fb5c-120">'パッケージ' フォルダーの場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="7fb5c-121">以前は、NuGet がソリューションのルート フォルダーの下の既知の 'パッケージ' フォルダーからソリューションのパッケージを管理します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="7fb5c-122">NuGet パッケージをインストールしているが、さまざまなソリューションが開発チームが、その結果、ファイル システム上のさまざまな場所にインストールされる同じパッケージで。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="7fb5c-123">NuGet 2.1 を使用して、[パッケージ] フォルダーの場所をより細かく制御を提供する、`repositoryPath`内の要素、`NuGet.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="7fb5c-124">Nuget.Config の階層のサポートの前の例でのビルドでは、C:\myteam\ 共有と同じパッケージ フォルダーの下のすべてのプロジェクトがあるすることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="7fb5c-125">これを実現するには、次のエントリを追加だけ`c:\myteam\Nuget.Config`です。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="7fb5c-126">この例で、共有`Nuget.Config`ファイルは、深さに関係なく C:\myteam の下に作成されるすべてのプロジェクトの共有パッケージ フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="7fb5c-127">既存のパッケージ フォルダーをソリューションのルートの下にある場合は場合、NuGet は、新しい場所にパッケージを配置前に削除する必要がありますに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="7fb5c-128">ポータブル ライブラリのサポート</span><span class="sxs-lookup"><span data-stu-id="7fb5c-128">Support for Portable Libraries</span></span>

<span data-ttu-id="7fb5c-129">[ポータブル ライブラリ](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)は Windows Phone、Xbox の偶数を Silverlight に.net Framework のバージョンからのさまざまな Microsoft プラットフォームで変更せずに作業できるアセンブリをビルドすることができます .NET 4 で初めて導入された機能です360 (ただし、現時点では、NuGet は Xbox のポータブル ライブラリのターゲットをサポートしていません)。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="7fb5c-130">拡張することによって、[パッケージ規則](../create-packages/supporting-multiple-target-frameworks.md)framework のバージョンとプロファイルは、NuGet 2.1 ようになりましたポータブル ライブラリを複合フレームワークとプロファイルのターゲットを持つパッケージの作成を有効にして`lib`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="7fb5c-131">たとえば、次のポータブル クラス ライブラリの使用可能なターゲット プラットフォームを検討してください。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![ポータブル ライブラリの作成ダイアログ](./media/releasenotes-21-plib.png)

<span data-ttu-id="7fb5c-133">ライブラリをビルドした後と、コマンド`nuget.exe pack MyPortableProject.csproj`実行は、新しいポータブル ライブラリのパッケージ フォルダーの構造を表示するには、生成された NuGet パッケージの内容が検査をします。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![ポータブル ライブラリ パッケージのレイアウト](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="7fb5c-135">ご覧のように、ポータブル ライブラリ フォルダーの名前規則のパターンに従います 'ポータブル {フレームワーク 1} + framework {n}' フレームワーク識別子が既存をに従って[フレームワークの名前とバージョンの規約](../reference/target-frameworks.md)します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="7fb5c-136">名前とバージョンの規則に 1 つの例外には、Windows Phone のために使用するフレームワークの識別子が記載されています。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="7fb5c-137">このモニカーでは、フレームワーク名 'wp' (wp7、wp71 または wp8) を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="7fb5c-138">' Silverlight-wp7' を使用してなどのエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="7fb5c-139">このフォルダー構造から作成されたパッケージをインストールするときに NuGet が、フォルダー名で指定されている複数の対象に、フレームワークやプロファイルの規則を適用できますようになりました。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="7fb5c-140">NuGet の照合ルールの背後にある、「特定性の低い」の「詳細」のターゲットが優先原則です。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="7fb5c-141">意味、特定のプラットフォームを対象とするモニカーが常に優先移植可能なはどちらもプロジェクトと互換性がある場合。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="7fb5c-142">さらに、複数の移植可能なターゲットがプロジェクトと互換性のある場合は、NuGet はサポートされているプラットフォームのセットは、パッケージを参照するプロジェクトに「最も近い」場所の 1 つを優先します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="7fb5c-143">ターゲットの Windows 8 および Windows Phone 8 プロジェクト</span><span class="sxs-lookup"><span data-stu-id="7fb5c-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="7fb5c-144">ポータブル ライブラリ プロジェクトを対象とするためのサポートを追加するだけでなく、NuGet 2.1 は Windows 8 のストアと Windows Phone 8 の両方のプロジェクトと Windows ストアとなる Windows Phone プロジェクトの新しい一般的なモニカーをいくつかの新しいフレームワークのモニカーを提供しますそれぞれのプラットフォームの将来のバージョン間での管理が容易です。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="7fb5c-145">Windows 8 ストア アプリケーションでは、識別子は次のようです。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="7fb5c-146">2.0 およびそれ以前の NuGet</span><span class="sxs-lookup"><span data-stu-id="7fb5c-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="7fb5c-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="7fb5c-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="7fb5c-148">winRT45、します。NETCore45</span><span class="sxs-lookup"><span data-stu-id="7fb5c-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="7fb5c-149">Windows、windows 8 を win、win8</span><span class="sxs-lookup"><span data-stu-id="7fb5c-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="7fb5c-150">Windows Phone プロジェクトでは、識別子は次のようです。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="7fb5c-151">Phone OS</span><span class="sxs-lookup"><span data-stu-id="7fb5c-151">Phone OS</span></span> | <span data-ttu-id="7fb5c-152">2.0 およびそれ以前の NuGet</span><span class="sxs-lookup"><span data-stu-id="7fb5c-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="7fb5c-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="7fb5c-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fb5c-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="7fb5c-154">Windows Phone 7</span></span> | <span data-ttu-id="7fb5c-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="7fb5c-155">silverlight3-wp</span></span> | <span data-ttu-id="7fb5c-156">wp、wp7、WindowsPhone、WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="7fb5c-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="7fb5c-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="7fb5c-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="7fb5c-158">silverlight4-wp71</span></span> | <span data-ttu-id="7fb5c-159">wp71、WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="7fb5c-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="7fb5c-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="7fb5c-160">Windows Phone 8</span></span> | <span data-ttu-id="7fb5c-161">(サポートされていません)</span><span class="sxs-lookup"><span data-stu-id="7fb5c-161">(not supported)</span></span> | <span data-ttu-id="7fb5c-162">wp8、WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="7fb5c-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="7fb5c-163">上記の変更は、すべての NuGet 2.1 で完全にサポートするフレームワークの古い名前が引き続き。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="7fb5c-164">今後は、新しい名前は、使用してください、それぞれのプラットフォームの将来のバージョン間でより安定したになります。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="7fb5c-165">新しい名前は*いない*する 2.1 より前のバージョンの NuGet ではサポートされて、ただし、適切に計画スイッチを作成します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="7fb5c-166">パッケージ マネージャー ダイアログ ボックスで検索機能の向上</span><span class="sxs-lookup"><span data-stu-id="7fb5c-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="7fb5c-167">過去のいくつかのイテレーションにおける速度とパッケージの検索の妥当性を大幅に向上する NuGet ギャラリーに変更が導入されました。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="7fb5c-168">ただし、これらの機能強化は、nuget.org の Web サイトに限定されていました。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="7fb5c-169">NuGet 2.1 により、検索エクスペリエンスの機能の向上が NuGet パッケージ マネージャー ダイアログを利用します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="7fb5c-170">たとえば、Windows Azure キャッシュ プレビュー パッケージを必要とすることを想像してください。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="7fb5c-171">このパッケージの適切な検索クエリには、"Azure Cache"可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="7fb5c-172">パッケージ マネージャー ダイアログの以前のバージョンで、目的のパッケージはさらには表示されない結果の最初のページ。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="7fb5c-173">ただし、NuGet の 2.1 では、目的のパッケージに表示されます、検索結果の上部にあります。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![パッケージ マネージャー ダイアログの検索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="7fb5c-175">パッケージを強制的に更新</span><span class="sxs-lookup"><span data-stu-id="7fb5c-175">Force Package Update</span></span>

<span data-ttu-id="7fb5c-176">パッケージの更新がない NuGet 2.1 では、前に NuGet をスキップは高いバージョン番号。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="7fb5c-177">これには、ビルド CI シナリオ場合や、チームがない場合にパッケージ バージョンをビルドするたびに番号をインクリメントする場合は特に – 特定のシナリオの摩擦が導入されました。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="7fb5c-178">目的の動作を強制的に更新に関係なくでした。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="7fb5c-179">NuGet 2.1 では、'再インストール' フラグを使用してこれを説明します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="7fb5c-180">たとえば、以前のバージョンの NuGet になります次最新パッケージのバージョンがないパッケージを更新しようとしています。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="7fb5c-181">かどうかに関係なく、パッケージを更新、再インストール フラグの新しいバージョンがあります。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="7fb5c-182">もう 1 つのシナリオを再インストール フラグが便利では、フレームワークの再ターゲットのです。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="7fb5c-183">(たとえば、.NET 4 から .NET 4.5)、プロジェクトのターゲット フレームワークを変更するときに更新プログラム パッケージの再インストール、プロジェクトにインストールされているすべての NuGet パッケージの適切なアセンブリへの参照を更新することができます。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="7fb5c-184">Visual Studio 内でパッケージ ソースを編集します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="7fb5c-185">NuGet の以前のバージョンでは、削除および再パッケージ ソースを追加するために必要な Visual Studio のオプション ダイアログ内からパッケージ ソースを更新しています。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="7fb5c-186">NuGet 2.1 では、構成用ユーザー インターフェイスのファースト クラスの関数として更新をサポートすることでこのワークフローが向上します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![パッケージ マネージャーの構成 ダイアログ](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="7fb5c-188">バグ修正</span><span class="sxs-lookup"><span data-stu-id="7fb5c-188">Bug Fixes</span></span>

<span data-ttu-id="7fb5c-189">NuGet 2.1 には、多くのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="7fb5c-190">作業の完全な一覧の項目で修正された NuGet 2.0 では、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)します。</span><span class="sxs-lookup"><span data-stu-id="7fb5c-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
