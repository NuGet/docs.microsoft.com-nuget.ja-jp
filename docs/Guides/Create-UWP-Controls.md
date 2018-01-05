---
title: "NuGet を使って UWP をパッケージ化する方法 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: "必要なメタデータと、Visual Studio と Blend デザイナーのサポート ファイルが含まれている UWP コントロールが含まれている NuGet パッケージを作成する方法を説明します。"
keywords: "NuGet UWP コントロール、Visual Studio XAML デザイナー、Blend デザイナー、カスタム コントロール"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f51dbabd406199752e4f9d612b498f59ffb54021
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="dcd23-104">NuGet パッケージとして UWP コントロールを作成する</span><span class="sxs-lookup"><span data-stu-id="dcd23-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="dcd23-105">Visual Studio 2017 では、NuGet パッケージで配信する UWP コントロールの追加機能を活用することができます。</span><span class="sxs-lookup"><span data-stu-id="dcd23-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="dcd23-106">このガイドでは、[ExtensionSDKasNuGetPackage サンプル](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)を使用してこれらの機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="dcd23-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="pre-requisites"></a><span data-ttu-id="dcd23-107">前提条件:</span><span class="sxs-lookup"><span data-stu-id="dcd23-107">Pre-requisites:</span></span>

1.  <span data-ttu-id="dcd23-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="dcd23-108">Visual Studio 2017</span></span>
1.  <span data-ttu-id="dcd23-109">[UWP パッケージの作成](create-uwp-packages.md)方法</span><span class="sxs-lookup"><span data-stu-id="dcd23-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="dcd23-110">XAML コントロールのツールボックス/資産ウィンドウのサポートを追加する</span><span class="sxs-lookup"><span data-stu-id="dcd23-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="dcd23-111">XAML コントロールが Visual Studio の XAML デザイナーのツールボックスと Blend の [資産] ウィンドウに表示されるようにするには、パッケージ プロジェクトの `tools` フォルダーのルートに `VisualStudioToolsManifest.xml` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="dcd23-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="dcd23-112">このファイルは、ツールボックスまたは [資産] ウィンドウにコントロールを表示する必要がない場合は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="dcd23-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

<span data-ttu-id="dcd23-113">ファイルの構造は、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="dcd23-113">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="dcd23-114">ここで、</span><span class="sxs-lookup"><span data-stu-id="dcd23-114">where:</span></span>

- <span data-ttu-id="dcd23-115">*your_package_file*: `ManagedPackage.winmd` などのコントロール ファイルの名前 ("ManagedPackage" はこの例で任意の名前を使用するだけで、それ以外の意味を持ちません)。</span><span class="sxs-lookup"><span data-stu-id="dcd23-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="dcd23-116">*vs_category*: Visual Studio デザイナーのツールボックスにコントロールを表示するグループのラベル。</span><span class="sxs-lookup"><span data-stu-id="dcd23-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="dcd23-117">`VSCategory` は、コントロールをツールボックスに表示するために必要です。</span><span class="sxs-lookup"><span data-stu-id="dcd23-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="dcd23-118">*blend_category*: Blend デザイナーの [資産] ウィンドウにコントロールを表示するグループのラベル。</span><span class="sxs-lookup"><span data-stu-id="dcd23-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="dcd23-119">`BlendCategory` は、コントロールを [資産] に表示するために必要です。</span><span class="sxs-lookup"><span data-stu-id="dcd23-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="dcd23-120">*type_full_name_n*: `ManagedPackage.MyCustomControl` など、名前空間を含む、各コントロールの完全修飾名です。</span><span class="sxs-lookup"><span data-stu-id="dcd23-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="dcd23-121">マネージ コードとネイティブの両方の種類でドット形式が使用されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="dcd23-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="dcd23-122">より高度なシナリオでは、1 つのパッケージに複数のコントロール アセンブリが含まれているときに、複数の `<File>` 要素を `<FileList>` に含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="dcd23-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="dcd23-123">コントロールをカテゴリ別に整理する場合は、複数 `<ToolboxItems>` ノードを 1 つの `<File>` 内に含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="dcd23-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="dcd23-124">次の例では、`ManagedPackage.winmd` 内に実装されたコントロールが、Visual Studio と Blend で “Managed Package” という名前のグループに表示され、そのグループに “MyCustomControl” が表示されます。</span><span class="sxs-lookup"><span data-stu-id="dcd23-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="dcd23-125">これらのすべての名前は任意です。</span><span class="sxs-lookup"><span data-stu-id="dcd23-125">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio で表示されるコントロールの例](media/UWP-control-vs-toolbox.png)

![Blend で表示されるコントロールの例](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="dcd23-128">ツールボックス/資産ウィンドウに表示するには、すべてのコントロールを明示的に指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd23-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="dcd23-129">`Namespace.ControlName` 形式で指定したことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="dcd23-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="dcd23-130">コントロールにカスタム アイコンを追加する</span><span class="sxs-lookup"><span data-stu-id="dcd23-130">Add custom icons to your controls</span></span>

<span data-ttu-id="dcd23-131">ツールボックス/資産ウィンドウにカスタム アイコンを表示するには、プロジェクトに画像を追加するか、"Namespace.ControlName.extension" という名前の対応する `design.dll` プロジェクトに画像を追加し、ビルド アクションを "埋め込みリソース" に設定します。</span><span class="sxs-lookup"><span data-stu-id="dcd23-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="dcd23-132">利用できる形式は `.png`、`.jpg`、`.jpeg`、`.gif`、`.bmp` です。</span><span class="sxs-lookup"><span data-stu-id="dcd23-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="dcd23-133">推奨されるイメージ サイズは 64 × 64 ピクセルです。</span><span class="sxs-lookup"><span data-stu-id="dcd23-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="dcd23-134">次の例では、プロジェクトには、"ManagedPackage.MyCustomControl.png" という名前の画像ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="dcd23-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![プロジェクトでカスタム アイコンを設定する](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="dcd23-136">ネイティブ コントロールの場合は、`design.dll` プロジェクトでリソースとしてアイコンを配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd23-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="dcd23-137">特定の Windows プラットフォーム バージョンをサポートする</span><span class="sxs-lookup"><span data-stu-id="dcd23-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="dcd23-138">UWP パッケージに含まれる TargetPlatformVersion (TPV) と TargetPlatformMinVersion (TPMinV) は、アプリケーションをインストールできる OS バージョンの上限と下限の境界を定義します。</span><span class="sxs-lookup"><span data-stu-id="dcd23-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="dcd23-139">TPV ではさらに、アプリがビルドされる SDK のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="dcd23-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="dcd23-140">UWP パッケージを作成するときにこれらのプロパティを考慮してください。アプリで定義されているプラットフォームのバージョンの範囲外の API を使用すると、ビルドが失敗したり、実行時にアプリが失敗したりします。</span><span class="sxs-lookup"><span data-stu-id="dcd23-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="dcd23-141">たとえば、コントロール パッケージの TPMinV を Windows 10 Anniversary Edition (10.0、ビルド 14393) に設定し、その下限に一致する UWP プロジェクトによってのみパッケージが使用されるようにしたとします。</span><span class="sxs-lookup"><span data-stu-id="dcd23-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="dcd23-142">`project.json` ベースの UWP プロジェクトでパッケージを使用できるようにするには、次のフォルダー名を使用してコントロールをパッケージ化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd23-142">To allow your package to be consumed by `project.json` based UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0\*
\ref\uap10.0\*
```

<span data-ttu-id="dcd23-143">適切な TPMinV チェックを適用するには、[MSBuild ターゲット ファイル](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets)を作成し、ビルド フォルダーの下にパッケージ化します ("your_assembly_name" を特定のアセンブリの名前に置き換えます):</span><span class="sxs-lookup"><span data-stu-id="dcd23-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) and package it under the build folder (replacing "your_assembly_name" with the name of your specific assembly):</span></span>

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

<span data-ttu-id="dcd23-144">ターゲット ファイルがどのように表示されるかの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="dcd23-144">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="dcd23-145">デザイン時サポートの追加</span><span class="sxs-lookup"><span data-stu-id="dcd23-145">Add design-time support</span></span>

<span data-ttu-id="dcd23-146">プロパティ インスペクターのどこにコントロールのプロパティが表示されるかを構成するには、カスタム装飾などを追加し、ターゲット プラットフォームに合わせて `design.dll` ファイルを `lib\<platform>\Design` フォルダー内に配置します。</span><span class="sxs-lookup"><span data-stu-id="dcd23-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\<platform>\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="dcd23-147">また、**[[テンプレートの編集] > [コピーして編集]](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** 機能を確実に動作させるには、マージする `Generic.xaml` とリソース ディクショナリを `<AssemblyName>\Themes` フォルダーに含める必要があります </span><span class="sxs-lookup"><span data-stu-id="dcd23-147">Also, to ensure that the **[Edit Template > Edit a Copy](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<AssemblyName>\Themes` folder.</span></span> <span data-ttu-id="dcd23-148">(このファイルはコントロールの実行時の動作には影響しません)。</span><span class="sxs-lookup"><span data-stu-id="dcd23-148">(This file has no impact on the runtime behavior of a control.)</span></span>


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> <span data-ttu-id="dcd23-149">既定では、コントロールのプロパティは、プロパティ インスペクターの [その他] カテゴリの下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="dcd23-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>


## <a name="use-strings-and-resources"></a><span data-ttu-id="dcd23-150">文字列とリソースの使用</span><span class="sxs-lookup"><span data-stu-id="dcd23-150">Use strings and resources</span></span>

<span data-ttu-id="dcd23-151">文字列リソース (`.resw`) をパッケージに埋め込み、コントロールまたは使用中の UWP プロジェクトでそれを使用して、`.resw` ファイルの **[ビルド アクション]** プロパティを **PRIResource** に設定することができます。</span><span class="sxs-lookup"><span data-stu-id="dcd23-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="dcd23-152">たとえば、ExtensionSDKasNuGetPackage サンプルの [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dcd23-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="dcd23-153">画像などのパッケージの内容</span><span class="sxs-lookup"><span data-stu-id="dcd23-153">Package content such as images</span></span>

<span data-ttu-id="dcd23-154">コントロールまたは使用中の UWP プロジェクトで使用できる画像などのコンテンツをパッケージ化します。</span><span class="sxs-lookup"><span data-stu-id="dcd23-154">To package content such as images that can be used by your control or the consuming UWP project.</span></span> <span data-ttu-id="dcd23-155">次のようにこれらのファイルを `lib\uap10.0.14393.0` フォルダーに追加します ("your_assembly_name" は、特定のコントロールに一致させます)。</span><span class="sxs-lookup"><span data-stu-id="dcd23-155">add those files `lib\uap10.0.14393.0` folder as follows ("your_assembly_name" should again match your particular control):</span></span>

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

<span data-ttu-id="dcd23-156">[MSBuild ターゲット ファイル](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets)を作成して、資産が使用するプロジェクトの出力フォルダーにコピーされるようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="dcd23-156">You may also author an[MSBuild targets file](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="dcd23-157">関連項目</span><span class="sxs-lookup"><span data-stu-id="dcd23-157">See also</span></span>

- [<span data-ttu-id="dcd23-158">UWP パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="dcd23-158">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="dcd23-159">ExtensionSDKasNuGetPackage サンプル</span><span class="sxs-lookup"><span data-stu-id="dcd23-159">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
