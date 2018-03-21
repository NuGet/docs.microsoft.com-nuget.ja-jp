---
title: "NuGet パッケージのソースと config ファイルの変換 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "インストール時にソース コードと構成 (XML) ファイルを変換する NuGet パッケージの機能について説明します。"
keywords: "NuGet パッケージのインストール、NuGet パッケージの変換、構成ファイルの変更、ソース コードの変更"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 47d02d160a7e40f323edcbd87e2c8642905b8ddf
ms.sourcegitcommit: df21fe770900644d476d51622a999597a6f20ef8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2018
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="6a6a1-104">ソース コードと構成ファイルの変換</span><span class="sxs-lookup"><span data-stu-id="6a6a1-104">Transforming source code and configuration files</span></span>

<span data-ttu-id="6a6a1-105">`packages.config` を使用するプロジェクトの場合、NuGet は、パッケージのインストール時およびアンインストール時にソースコードおよび構成ファイルに変換する機能をサポートします。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-105">For projects using `packages.config`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span> <span data-ttu-id="6a6a1-106">[PackageReference](../consume-packages/package-references-in-project-files.md) を使用してパッケージがプロジェクトにインストールされている場合、ソース コード変換のみが適用されます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-106">Only Source code transformations are applied when a package is installed in a project using [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span>

<span data-ttu-id="6a6a1-107">**ソース コード変換**は、パッケージがインストールされるときに、パッケージの `content` または `contentFiles` フォルダー (`packages.config` を使用している場合は `content`、`PackageReference` を使用している場合は `contentFiles`) のファイルに一方向トークンの置き換えを適用します。この場合、トークンは、Visual Studio [プロジェクトのプロパティ](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)を参照します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-107">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="6a6a1-108">これにより、プロジェクトの名前空間にファイルを挿入したり、ASP.NET プロジェクトで通常は `global.asax` に置かれるコードをカスタマイズしたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-108">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="6a6a1-109">**構成ファイルの変換**を使用して、`web.config` や `app.config` などのターゲット プロジェクトに既に存在するファイルを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-109">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="6a6a1-110">たとえば、場合によっては、パッケージで構成ファイルの `modules` セクションに項目を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-110">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="6a6a1-111">この変換は、構成ファイルに追加するセクションを記述するパッケージ内の特別なファイルを含めることで行われます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-111">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="6a6a1-112">パッケージがアンインストールされるときには、同じ変更が、逆に行われ、これを双方向の変換にします。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-112">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="6a6a1-113">変換のソース コードを指定する</span><span class="sxs-lookup"><span data-stu-id="6a6a1-113">Specifying source code transformations</span></span>

1. <span data-ttu-id="6a6a1-114">パッケージからプロジェクトに挿入するファイルは、パッケージ内の `content` および `contentFiles` フォルダーに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-114">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="6a6a1-115">たとえば、`ContosoData.cs` という名前のファイルをターゲット プロジェクトの `Models` フォルダーにインストールする場合は、パッケージの `content\Models` および `contentFiles\{lang}\{tfm}\Models` フォルダー内にファイルが置かれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-115">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="6a6a1-116">インストール時にトークンの置換を適用するように NuGet に指示するには、`.pp` をソース コード ファイル名に追加します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-116">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="6a6a1-117">インストール後、ファイルには `.pp` 拡張子は付きません。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-117">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="6a6a1-118">たとえば、`ContosoData.cs` で変換を行うには、パッケージ内のファイルに `ContosoData.cs.pp` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-118">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="6a6a1-119">インストール後には、`ContosoData.cs` として表示されます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-119">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="6a6a1-120">ソース コード ファイル内では、`$token$` 形式の大文字と小文字が区別されないトークンを使用し、NuGet でプロジェクトのプロパティと置き換える必要がある値を示します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-120">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="6a6a1-121">インストール時に、NuGet が、ターゲット プロジェクトのルート名前空間が `Fabrikam` であると仮定して、`$rootnamespace$` を `Fabrikam` に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-121">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="6a6a1-122">`$rootnamespace$` トークンは、最もよく使用されるプロジェクト プロパティです。他のすべてのトークンは、[プロジェクト プロパティ](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)に関するページに一覧表示されています。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-122">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="6a6a1-123">当然ながら、一部のプロパティはプロジェクトの種類に固有である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-123">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="6a6a1-124">構成ファイルの変換を指定する</span><span class="sxs-lookup"><span data-stu-id="6a6a1-124">Specifying config file transformations</span></span>

<span data-ttu-id="6a6a1-125">以降のセクションで後述するように、2 つの方法で構成ファイルの変換を実行できます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-125">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="6a6a1-126">`app.config.transform` および `web.config.transform` ファイルをパッケージの `content` フォルダーに含めます。`.transform` 拡張子は、パッケージがインストールされるときに、これらのファイルが既存の構成ファイルにマージする XML を含んでいることを NuGet に指示します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-126">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="6a6a1-127">パッケージがアンインストールされると、その同じ XML が削除されます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-127">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="6a6a1-128">`app.config.install.xdt` および `web.config.install.xdt` ファイルをパッケージの `content` フォルダーに含めるときに、[XDT 構文](https://msdn.microsoft.com/library/dd465326.aspx)を使用して、目的の変更を記述します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-128">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="6a6a1-129">このオプションを使用して、`.uninstall.xdt` ファイルも含め、プロジェクトからパッケージが削除されるときに変更を逆に実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-129">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="6a6a1-130">変換は、Visual Studio でリンクとして参照されている `.config` ファイルには適用されません。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-130">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="6a6a1-131">XDT を使用することの利点は、2 つの静的なファイルを単純にマージする代わりに、XPath が完全にサポートされる要素と属性のマッチングを使用して XML DOM の構造を操作するための構文を提供することです。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-131">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="6a6a1-132">XDT はその後で、要素の追加、更新、削除、指定した場所での新しい要素の配置、要素の置換/削除 (子ノードを含む) を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-132">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="6a6a1-133">これにより、パッケージのインストール中に実行されたすべての変換を元に戻すアンインストール変換を簡単に作成できるようになります。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-133">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="6a6a1-134">XML 変換</span><span class="sxs-lookup"><span data-stu-id="6a6a1-134">XML transforms</span></span>

<span data-ttu-id="6a6a1-135">パッケージの `content` フォルダーの `app.config.transform` と `web.config.transform` は、プロジェクトの既存の `app.config` および `web.config` ファイルにマージする要素のみを含んでいます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-135">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="6a6a1-136">例のように、プロジェクトが最初に `web.config` 内に次のコンテンツを含んでいると仮定します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-136">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6a6a1-137">パッケージのインストール中に `MyNuModule` 要素を `modules` セクションに追加するには、次のような `web.config.transform` ファイルをパッケージの `content` フォルダー内に作成します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-137">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6a6a1-138">NuGet がパッケージをインストールした後に、`web.config` は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-138">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="6a6a1-139">NuGet が `modules` セクションを置き換えずに、新しい要素と特性のみを追加することによって単純に新しいエントリをその中にマージしています。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-139">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="6a6a1-140">NuGet は、どの既存の要素または属性も変更しません。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-140">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="6a6a1-141">パッケージがアンインストールされるときに、NuGet は、`.transform` ファイルをもう一度調べ、含まれている要素を適切な `.config` ファイルから削除します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-141">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="6a6a1-142">このプロセスは、パッケージのインストール後に変更する `.config` ファイルのどの行にも影響しません。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-142">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="6a6a1-143">広範な例として、[Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) パッケージは、多くのエントリを `web.config` に追加し、それらもパッケージがアンインストールされるときに削除されます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-143">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="6a6a1-144">その `web.config.transform` ファイルを調べるには、ELMAH パッケージを上記のリンクからダウンロードし、パッケージの拡張子を `.nupkg` から `.zip` に変更して、`content\web.config.transform` をその ZIP ファイル内から開きます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-144">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="6a6a1-145">パッケージのインストールおよびアンインストールの影響を確認するには、新しい ASP.NET プロジェクトを Visual Studio で作成し (テンプレートは、[新しいプロジェクト] ダイアログ ボックスの **[Visual C#] > [Web]** にあります)、空の ASP.NET アプリケーションを選択します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-145">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="6a6a1-146">`web.config` を開いて初期状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-146">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="6a6a1-147">プロジェクトを右クリックし、**[NuGet パッケージの管理]** を選択し、nuget.org で ELMAH を見つけて、最新バージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-147">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="6a6a1-148">`web.config` のすべての変更に注意してください。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-148">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="6a6a1-149">次に、パッケージをアンインストールすると、`web.config` が前の状態に戻ります。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-149">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="6a6a1-150">XDT 変換</span><span class="sxs-lookup"><span data-stu-id="6a6a1-150">XDT transforms</span></span>

<span data-ttu-id="6a6a1-151">[XDT 構文](https://msdn.microsoft.com/library/dd465326.aspx)を使用して構成ファイルを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-151">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="6a6a1-152">`$` 区切り文字 (大文字と小文字は区別されません) 内にプロパティ名を含めることにより、NuGet でトークンを[プロジェクト プロパティ](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)に置き換えることもできます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-152">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="6a6a1-153">たとえば、次の `app.config.install.xdt` ファイルは、プロジェクトの `FullPath`、`FileName`、`ActiveConfigurationSettings` 値を含む `app.config` に `appSettings` 要素を挿入します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-153">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="6a6a1-154">別の例で、プロジェクトが最初に `web.config` 内に次のコンテンツを含んでいると仮定します。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-154">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6a6a1-155">パッケージのインストール中に `MyNuModule` 要素を `modules` セクションに追加するために、パッケージの `web.config.install.xdt` は次を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-155">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="6a6a1-156">パッケージをインストールした後、`web.config` は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-156">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="6a6a1-157">パッケージのアンインストール中に `MyNuModule` 要素のみを削除するには、`web.config.uninstall.xdt` ファイルは、次を含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="6a6a1-157">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
