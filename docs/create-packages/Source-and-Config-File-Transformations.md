---
title: NuGet パッケージのソースと config ファイルの変換
description: インストール時にソース コードと構成 (XML) ファイルを変換する NuGet パッケージの機能について説明します。
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231176"
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="2e12b-103">ソース コードと構成ファイルの変換</span><span class="sxs-lookup"><span data-stu-id="2e12b-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="2e12b-104">**ソース コード変換**は、パッケージがインストールされるときに、パッケージの `content` または `contentFiles` フォルダー (`content` を使用している場合は `packages.config`、`contentFiles` を使用している場合は `PackageReference`) のファイルに一方向トークンの置き換えを適用します。この場合、トークンは、Visual Studio [プロジェクトのプロパティ](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)を参照します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-104">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="2e12b-105">これにより、プロジェクトの名前空間にファイルを挿入したり、ASP.NET プロジェクトで通常は `global.asax` に置かれるコードをカスタマイズしたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-105">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="2e12b-106">**構成ファイルの変換**を使用して、`web.config` や `app.config` などのターゲット プロジェクトに既に存在するファイルを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-106">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="2e12b-107">たとえば、場合によっては、パッケージで構成ファイルの `modules` セクションに項目を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e12b-107">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="2e12b-108">この変換は、構成ファイルに追加するセクションを記述するパッケージ内の特別なファイルを含めることで行われます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-108">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="2e12b-109">パッケージがアンインストールされるときには、同じ変更が、逆に行われ、これを双方向の変換にします。</span><span class="sxs-lookup"><span data-stu-id="2e12b-109">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="2e12b-110">変換のソース コードを指定する</span><span class="sxs-lookup"><span data-stu-id="2e12b-110">Specifying source code transformations</span></span>

1. <span data-ttu-id="2e12b-111">パッケージからプロジェクトに挿入するファイルは、パッケージ内の `content` および `contentFiles` フォルダーに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e12b-111">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="2e12b-112">たとえば、`ContosoData.cs` という名前のファイルをターゲット プロジェクトの `Models` フォルダーにインストールする場合は、パッケージの `content\Models` および `contentFiles\{lang}\{tfm}\Models` フォルダー内にファイルが置かれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e12b-112">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="2e12b-113">インストール時にトークンの置換を適用するように NuGet に指示するには、`.pp` をソース コード ファイル名に追加します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-113">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="2e12b-114">インストール後、ファイルには `.pp` 拡張子は付きません。</span><span class="sxs-lookup"><span data-stu-id="2e12b-114">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="2e12b-115">たとえば、`ContosoData.cs` で変換を行うには、パッケージ内のファイルに `ContosoData.cs.pp` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-115">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="2e12b-116">インストール後には、`ContosoData.cs` として表示されます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-116">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="2e12b-117">ソース コード ファイル内では、`$token$` 形式の大文字と小文字が区別されないトークンを使用し、NuGet でプロジェクトのプロパティと置き換える必要がある値を示します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-117">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    <span data-ttu-id="2e12b-118">インストール時に、NuGet が、ターゲット プロジェクトのルート名前空間が `$rootnamespace$` であると仮定して、`Fabrikam` を `Fabrikam` に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-118">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="2e12b-119">`$rootnamespace$` トークンは、最もよく使用されるプロジェクト プロパティです。他のすべてのトークンは、[プロジェクト プロパティ](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)に関するページに一覧表示されています。</span><span class="sxs-lookup"><span data-stu-id="2e12b-119">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="2e12b-120">当然ながら、一部のプロパティはプロジェクトの種類に固有である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2e12b-120">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="2e12b-121">構成ファイルの変換を指定する</span><span class="sxs-lookup"><span data-stu-id="2e12b-121">Specifying config file transformations</span></span>

<span data-ttu-id="2e12b-122">以降のセクションで後述するように、2 つの方法で構成ファイルの変換を実行できます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-122">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="2e12b-123">`app.config.transform` および `web.config.transform` ファイルをパッケージの `content` フォルダーに含めます。`.transform` 拡張子は、パッケージがインストールされるときに、これらのファイルが既存の構成ファイルにマージする XML を含んでいることを NuGet に指示します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-123">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="2e12b-124">パッケージがアンインストールされると、その同じ XML が削除されます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-124">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="2e12b-125">`app.config.install.xdt` および `web.config.install.xdt` ファイルをパッケージの `content` フォルダーに含めるときに、[XDT 構文](https://msdn.microsoft.com/library/dd465326.aspx)を使用して、目的の変更を記述します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-125">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="2e12b-126">このオプションを使用して、`.uninstall.xdt` ファイルも含め、プロジェクトからパッケージが削除されるときに変更を逆に実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-126">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="2e12b-127">変換は、Visual Studio でリンクとして参照されている `.config` ファイルには適用されません。</span><span class="sxs-lookup"><span data-stu-id="2e12b-127">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="2e12b-128">XDT を使用することの利点は、2 つの静的なファイルを単純にマージする代わりに、XPath が完全にサポートされる要素と属性のマッチングを使用して XML DOM の構造を操作するための構文を提供することです。</span><span class="sxs-lookup"><span data-stu-id="2e12b-128">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="2e12b-129">XDT はその後で、要素の追加、更新、削除、指定した場所での新しい要素の配置、要素の置換/削除 (子ノードを含む) を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-129">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="2e12b-130">これにより、パッケージのインストール中に実行されたすべての変換を元に戻すアンインストール変換を簡単に作成できるようになります。</span><span class="sxs-lookup"><span data-stu-id="2e12b-130">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="2e12b-131">XML 変換</span><span class="sxs-lookup"><span data-stu-id="2e12b-131">XML transforms</span></span>

<span data-ttu-id="2e12b-132">パッケージの `app.config.transform` フォルダーの `web.config.transform` と `content` は、プロジェクトの既存の `app.config` および `web.config` ファイルにマージする要素のみを含んでいます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-132">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="2e12b-133">例のように、プロジェクトが最初に `web.config` 内に次のコンテンツを含んでいると仮定します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-133">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2e12b-134">パッケージのインストール中に `MyNuModule` 要素を `modules` セクションに追加するには、次のような `web.config.transform` ファイルをパッケージの `content` フォルダー内に作成します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-134">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2e12b-135">NuGet がパッケージをインストールした後に、`web.config` は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-135">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2e12b-136">NuGet が `modules` セクションを置き換えずに、新しい要素と特性のみを追加することによって単純に新しいエントリをその中にマージしています。</span><span class="sxs-lookup"><span data-stu-id="2e12b-136">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="2e12b-137">NuGet は、どの既存の要素または属性も変更しません。</span><span class="sxs-lookup"><span data-stu-id="2e12b-137">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="2e12b-138">パッケージがアンインストールされるときに、NuGet は、`.transform` ファイルをもう一度調べ、含まれている要素を適切な `.config` ファイルから削除します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-138">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="2e12b-139">このプロセスは、パッケージのインストール後に変更する `.config` ファイルのどの行にも影響しません。</span><span class="sxs-lookup"><span data-stu-id="2e12b-139">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="2e12b-140">広範な例として、[Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) パッケージは、多くのエントリを `web.config` に追加し、それらもパッケージがアンインストールされるときに削除されます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-140">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="2e12b-141">その `web.config.transform` ファイルを調べるには、ELMAH パッケージを上記のリンクからダウンロードし、パッケージの拡張子を `.nupkg` から `.zip` に変更して、`content\web.config.transform` をその ZIP ファイル内から開きます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-141">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="2e12b-142">パッケージのインストールおよびアンインストールの影響を確認するには、新しい ASP.NET プロジェクトを Visual Studio で作成し (テンプレートは、[新しいプロジェクト] ダイアログ ボックスの **[Visual C#] > [Web]** にあります)、空の ASP.NET アプリケーションを選択します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-142">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="2e12b-143">`web.config` を開いて初期状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-143">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="2e12b-144">プロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択し、nuget.org で ELMAH を見つけて、最新バージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="2e12b-144">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="2e12b-145">`web.config` のすべての変更に注意してください。</span><span class="sxs-lookup"><span data-stu-id="2e12b-145">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="2e12b-146">次に、パッケージをアンインストールすると、`web.config` が前の状態に戻ります。</span><span class="sxs-lookup"><span data-stu-id="2e12b-146">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="2e12b-147">XDT 変換</span><span class="sxs-lookup"><span data-stu-id="2e12b-147">XDT transforms</span></span>

> [!Note]
> <span data-ttu-id="2e12b-148">[`packages.config` から `PackageReference` への移行に関するドキュメントのパッケージの互換性の問題に関するセクション](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)で説明したように、XDT 変換は、以下で説明するように、`packages.config` でのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="2e12b-148">As mentioned in the [package compatibility issues section of the docs for migrating from `packages.config` to `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformations as described below are only supported by `packages.config`.</span></span> <span data-ttu-id="2e12b-149">次のファイルをパッケージに追加すると、`PackageReference` でパッケージを使用しているコンシューマーには変換が適用されません (XDT 変換を [ で動作するようにするには、](https://github.com/NuGet/Samples/tree/master/XDTransformExample)このサンプル`PackageReference`を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="2e12b-149">If you add the below files to your package, consumers using your package with `PackageReference` will not have the transformations applied (refer to [this sample](https://github.com/NuGet/Samples/tree/master/XDTransformExample) to make XDT transforms work with`PackageReference`).</span></span>

<span data-ttu-id="2e12b-150">[XDT 構文](https://msdn.microsoft.com/library/dd465326.aspx)を使用して構成ファイルを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="2e12b-151">[ 区切り文字 (大文字と小文字は区別されません) 内にプロパティ名を含めることにより、NuGet でトークンを](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)プロジェクト プロパティ`$`に置き換えることもできます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="2e12b-152">たとえば、次の `app.config.install.xdt` ファイルは、プロジェクトの `appSettings`、`app.config`、`FullPath` 値を含む `FileName` に `ActiveConfigurationSettings` 要素を挿入します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

<span data-ttu-id="2e12b-153">別の例で、プロジェクトが最初に `web.config` 内に次のコンテンツを含んでいると仮定します。</span><span class="sxs-lookup"><span data-stu-id="2e12b-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2e12b-154">パッケージのインストール中に `MyNuModule` 要素を `modules` セクションに追加するために、パッケージの `web.config.install.xdt` は次を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="2e12b-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2e12b-155">パッケージをインストールした後、`web.config` は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2e12b-155">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2e12b-156">パッケージのアンインストール中に `MyNuModule` 要素のみを削除するには、`web.config.uninstall.xdt` ファイルは、次を含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e12b-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
