---
title: NuGet を使用して UI コントロールをパッケージ化する方法
description: UWP コントロールまたは WPF コントロールを含む NuGet パッケージを作成する方法について説明します。これには、必要なメタデータと、Visual Studio と Blend デザイナー用のサポート ファイルが含まれます。
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: dd36987e020c2daa02bb875aa9dbd69c85bba4d3
ms.sourcegitcommit: 1bd72dca2f85b4267b9924236f1d23dd7b0ed733
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951747"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="733bf-103">NuGet パッケージとして UI コントロールを作成する</span><span class="sxs-lookup"><span data-stu-id="733bf-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="733bf-104">Visual Studio 2017 では、NuGet パッケージで配信する UWP コントロールと WPF コントロール用の追加機能を活用できます。</span><span class="sxs-lookup"><span data-stu-id="733bf-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="733bf-105">このガイドでは、UWP コントロールのコンテキストから、[ExtensionSDKasNuGetPackage サンプル](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)を使用してこれらの機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="733bf-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="733bf-106">特に言及がない限り、WPF コントロールに対しても同じことが該当します。</span><span class="sxs-lookup"><span data-stu-id="733bf-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="733bf-107">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="733bf-107">Prerequisites</span></span>

1. <span data-ttu-id="733bf-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="733bf-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="733bf-109">[UWP パッケージの作成](create-uwp-packages.md)方法</span><span class="sxs-lookup"><span data-stu-id="733bf-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="733bf-110">ライブラリ レイアウトの生成</span><span class="sxs-lookup"><span data-stu-id="733bf-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="733bf-111">これは、UWP コントロールにのみ該当します。</span><span class="sxs-lookup"><span data-stu-id="733bf-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="733bf-112">`GenerateLibraryLayout` プロパティを設定すると、nuspec に個別のファイル エントリがなくても、パッケージ化の準備ができているレイアウトでプロジェクト ビルドの出力が生成されます。</span><span class="sxs-lookup"><span data-stu-id="733bf-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="733bf-113">プロジェクト プロパティから [ビルド] タブに移動し、[ライブラリ レイアウトの生成] チェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="733bf-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="733bf-114">これにより、プロジェクト ファイルが変更され、現在選択しているビルド構成とプラットフォームに対して `GenerateLibraryLayout` フラグが true に設定されます。</span><span class="sxs-lookup"><span data-stu-id="733bf-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="733bf-115">または、プロジェクト ファイルを編集して、最初の無条件プロパティ グループに `<GenerateLibraryLayout>true</GenerateLibraryLayout>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="733bf-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="733bf-116">これにより、ビルド構成とプラットフォームに関係なく、プロパティが適用されます。</span><span class="sxs-lookup"><span data-stu-id="733bf-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="733bf-117">XAML コントロールのツールボックス/資産ウィンドウのサポートを追加する</span><span class="sxs-lookup"><span data-stu-id="733bf-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="733bf-118">XAML コントロールが Visual Studio の XAML デザイナーのツールボックスと Blend の [資産] ウィンドウに表示されるようにするには、パッケージ プロジェクトの `tools` フォルダーのルートに `VisualStudioToolsManifest.xml` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="733bf-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="733bf-119">このファイルは、ツールボックスまたは [資産] ウィンドウにコントロールを表示する必要がない場合は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="733bf-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="733bf-120">ファイルの構造は、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="733bf-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="733bf-121">それぞれの文字について以下に説明します。</span><span class="sxs-lookup"><span data-stu-id="733bf-121">where:</span></span>

- <span data-ttu-id="733bf-122">*your_package_file*: `ManagedPackage.winmd` などのコントロール ファイルの名前 ("ManagedPackage" はこの例で任意の名前を使用するだけで、それ以外の意味を持ちません)。</span><span class="sxs-lookup"><span data-stu-id="733bf-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="733bf-123">*vs_category*: Visual Studio デザイナーのツールボックスにコントロールを表示するグループのラベル。</span><span class="sxs-lookup"><span data-stu-id="733bf-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="733bf-124">`VSCategory` は、コントロールをツールボックスに表示するために必要です。</span><span class="sxs-lookup"><span data-stu-id="733bf-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="733bf-125">*blend_category*: Blend デザイナーの [資産] ウィンドウにコントロールを表示するグループのラベル。</span><span class="sxs-lookup"><span data-stu-id="733bf-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="733bf-126">`BlendCategory` は、コントロールを [資産] に表示するために必要です。</span><span class="sxs-lookup"><span data-stu-id="733bf-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="733bf-127">*type_full_name_n*: `ManagedPackage.MyCustomControl` など、名前空間を含む、各コントロールの完全修飾名です。</span><span class="sxs-lookup"><span data-stu-id="733bf-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="733bf-128">マネージド コードとネイティブの両方の種類でドット形式が使用されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="733bf-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="733bf-129">より高度なシナリオでは、1 つのパッケージに複数のコントロール アセンブリが含まれているときに、複数の `<File>` 要素を `<FileList>` に含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="733bf-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="733bf-130">コントロールをカテゴリ別に整理する場合は、複数 `<ToolboxItems>` ノードを 1 つの `<File>` 内に含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="733bf-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="733bf-131">次の例では、`ManagedPackage.winmd` 内に実装されたコントロールが、Visual Studio と Blend で “Managed Package” という名前のグループに表示され、そのグループに “MyCustomControl” が表示されます。</span><span class="sxs-lookup"><span data-stu-id="733bf-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="733bf-132">これらのすべての名前は任意です。</span><span class="sxs-lookup"><span data-stu-id="733bf-132">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="733bf-135">ツールボックス/資産ウィンドウに表示するには、すべてのコントロールを明示的に指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="733bf-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="733bf-136">`Namespace.ControlName` 形式で指定したことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="733bf-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="733bf-137">コントロールにカスタム アイコンを追加する</span><span class="sxs-lookup"><span data-stu-id="733bf-137">Add custom icons to your controls</span></span>

<span data-ttu-id="733bf-138">ツールボックス/資産ウィンドウにカスタム アイコンを表示するには、プロジェクトに画像を追加するか、"Namespace.ControlName.extension" という名前の対応する `design.dll` プロジェクトに画像を追加し、ビルド アクションを "埋め込みリソース" に設定します。</span><span class="sxs-lookup"><span data-stu-id="733bf-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="733bf-139">また、関連付けられている `AssemblyInfo.cs` によって ProvideMetadata 属性 (`[assembly: ProvideMetadata(typeof(RegisterMetadata))]`) が指定されていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="733bf-139">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="733bf-140">この[サンプル](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="733bf-140">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="733bf-141">利用できる形式は `.png`、`.jpg`、`.jpeg`、`.gif`、`.bmp` です。</span><span class="sxs-lookup"><span data-stu-id="733bf-141">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="733bf-142">推奨されるイメージ サイズは 64 × 64 ピクセルです。</span><span class="sxs-lookup"><span data-stu-id="733bf-142">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="733bf-143">次の例では、プロジェクトには、"ManagedPackage.MyCustomControl.png" という名前の画像ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="733bf-143">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![プロジェクトでカスタム アイコンを設定する](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="733bf-145">ネイティブ コントロールの場合は、`design.dll` プロジェクトでリソースとしてアイコンを配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="733bf-145">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="733bf-146">特定の Windows プラットフォーム バージョンをサポートする</span><span class="sxs-lookup"><span data-stu-id="733bf-146">Support specific Windows platform versions</span></span>

<span data-ttu-id="733bf-147">UWP パッケージに含まれる TargetPlatformVersion (TPV) と TargetPlatformMinVersion (TPMinV) は、アプリケーションをインストールできる OS バージョンの上限と下限の境界を定義します。</span><span class="sxs-lookup"><span data-stu-id="733bf-147">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="733bf-148">TPV ではさらに、アプリがビルドされる SDK のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="733bf-148">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="733bf-149">UWP パッケージを作成するときにこれらのプロパティを考慮してください。アプリで定義されているプラットフォームのバージョンの範囲外の API を使用すると、ビルドが失敗したり、実行時にアプリが失敗したりします。</span><span class="sxs-lookup"><span data-stu-id="733bf-149">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="733bf-150">たとえば、コントロール パッケージの TPMinV を Windows 10 Anniversary Edition (10.0、ビルド 14393) に設定し、その下限に一致する UWP プロジェクトによってのみパッケージが使用されるようにしたとします。</span><span class="sxs-lookup"><span data-stu-id="733bf-150">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="733bf-151">UWP プロジェクトでパッケージを使用できるようにするには、次のフォルダー名を使用してコントロールをパッケージ化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="733bf-151">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="733bf-152">NuGet では、使用するプロジェクトの TPMinV が自動的にチェックされ、Windows 10 Anniversary Edition (10.0、ビルド 14393) よりも低かった場合はインストールが失敗します。</span><span class="sxs-lookup"><span data-stu-id="733bf-152">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="733bf-153">WPF の場合、たとえば、.NET Framework v4.6.1 以上をターゲットとするプロジェクトにのみ WPF コントロールのパッケージが使用されるようにするとします。</span><span class="sxs-lookup"><span data-stu-id="733bf-153">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="733bf-154">これを強制するには、次のフォルダー名を使用してコントロールをパッケージ化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="733bf-154">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="733bf-155">デザイン時サポートの追加</span><span class="sxs-lookup"><span data-stu-id="733bf-155">Add design-time support</span></span>

<span data-ttu-id="733bf-156">プロパティ インスペクターのどこにコントロールのプロパティが表示されるかを構成するには、カスタム装飾などを追加し、ターゲット プラットフォームに合わせて `design.dll` ファイルを `lib\uap10.0.14393\Design` フォルダー内に配置します。</span><span class="sxs-lookup"><span data-stu-id="733bf-156">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="733bf-157">また、**[[テンプレートの編集] > [コピーして編集]](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** 機能を確実に動作させるには、マージする `Generic.xaml` とリソース ディクショナリを `<your_assembly_name>\Themes` フォルダーに含める必要があります (ここでも実際のアセンブリ名を使用します)。</span><span class="sxs-lookup"><span data-stu-id="733bf-157">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="733bf-158">(このファイルはコントロールの実行時の動作には影響しません)。その結果、フォルダー構造は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="733bf-158">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="733bf-159">WPF の場合は、WPF コントロールのパッケージが .NET Framework v4.6.1 以上をターゲットとするプロジェクトによって使用される例で続行します。</span><span class="sxs-lookup"><span data-stu-id="733bf-159">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="733bf-160">既定では、コントロールのプロパティは、プロパティ インスペクターの [その他] カテゴリの下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="733bf-160">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="733bf-161">文字列とリソースの使用</span><span class="sxs-lookup"><span data-stu-id="733bf-161">Use strings and resources</span></span>

<span data-ttu-id="733bf-162">文字列リソース (`.resw`) をパッケージに埋め込み、コントロールまたは使用中の UWP プロジェクトでそれを使用して、`.resw` ファイルの **[ビルド アクション]** プロパティを **PRIResource** に設定することができます。</span><span class="sxs-lookup"><span data-stu-id="733bf-162">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="733bf-163">たとえば、ExtensionSDKasNuGetPackage サンプルの [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="733bf-163">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="733bf-164">これは、UWP コントロールにのみ該当します。</span><span class="sxs-lookup"><span data-stu-id="733bf-164">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="733bf-165">関連項目</span><span class="sxs-lookup"><span data-stu-id="733bf-165">See also</span></span>

- [<span data-ttu-id="733bf-166">UWP パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="733bf-166">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="733bf-167">ExtensionSDKasNuGetPackage サンプル</span><span class="sxs-lookup"><span data-stu-id="733bf-167">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
