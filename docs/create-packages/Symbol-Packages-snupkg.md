---
title: 新しいシンボル パッケージ形式 '.snupkg' を使用して NuGet シンボル パッケージを公開する方法 | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet シンボル パッケージ (snupkg) の作成方法。
keywords: NuGet シンボル パッケージ, NuGet パッケージ デバッグ, NuGet デバッグ対応, パッケージ シンボル, シンボル パッケージ規則
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 48ca4b62e722988b3dfe69306565d7f159805962
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453456"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="ad48a-104">シンボル パッケージ (.snupkg) の作成</span><span class="sxs-lookup"><span data-stu-id="ad48a-104">Creating symbol packages (.snupkg)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad48a-105">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="ad48a-105">Prerequisites</span></span>

<span data-ttu-id="ad48a-106">必要な [NuGet プロトコル](../api/nuget-protocols.md)を実装する、[nuget.exe v4.9.0 以上](https://www.nuget.org/downloads)または [dotnet.exe v2.2.0 以上](https://www.microsoft.com/net/download/dotnet-core/2.2)。</span><span class="sxs-lookup"><span data-stu-id="ad48a-106">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="ad48a-107">シンボル パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="ad48a-107">Creating a symbol package</span></span>

<span data-ttu-id="ad48a-108">snupkg シンボル パッケージは .nuspec ファイルまたは .csproj ファイルから作成できます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-108">A snupkg symbol package can be created from a .nuspec file or from a .csproj file.</span></span> <span data-ttu-id="ad48a-109">NuGet.exe と dotnet.exe の両方がサポートされます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-109">NuGet.exe and dotnet.exe are both supported.</span></span> <span data-ttu-id="ad48a-110">```-Symbols -SymbolPackageFormat snupkg``` のオプションが .nupkg.exe パック コマンドで使用されると、.nupkg ファイルの他に .snupkg ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-110">When the options ```-Symbols -SymbolPackageFormat snupkg``` are used on the nuget.exe pack command a .snupkg file will be created in additon to the .nupkg file.</span></span>

<span data-ttu-id="ad48a-111">.snupkg ファイルを作成するコマンドの例</span><span class="sxs-lookup"><span data-stu-id="ad48a-111">Example commands to create .snupkg files</span></span>
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

<span data-ttu-id="ad48a-112">`.snupkgs` は、既定では生成されません。</span><span class="sxs-lookup"><span data-stu-id="ad48a-112">`.snupkgs` are not produced by default.</span></span> <span data-ttu-id="ad48a-113">nuget.exe の場合は `-Symbols` と共に `SymbolPackageFormat` プロパティを、dotnet.exe の場合は `--include-symbols` を、msbuild の場合は `-p:IncludeSymbols` を渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad48a-113">You must pass the `SymbolPackageFormat` property along with `-Symbols` in case of nuget.exe, `--include-symbols` in case of dotnet.exe, or `-p:IncludeSymbols` in case of msbuild.</span></span>

<span data-ttu-id="ad48a-114">SymbolPackageFormat プロパティには、`symbols.nupkg` (既定値) または `snupkg` の 2 つの値のうちどちらかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-114">SymbolPackageFormat property can have one of the two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="ad48a-115">SymbolPackageFormat が指定されていない場合は `symbols.nupkg` が既定に設定され、レガシ シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-115">If the SymbolPackageFormat is not specified, it defaults to `symbols.nupkg` and a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="ad48a-116">従来の形式 `.symbols.nupkg` は引き続きサポートされますが、これは互換性のみを目的としています ([レガシ シンボル パッケージ](Symbol-Packages.md)に関する記事を参照)。</span><span class="sxs-lookup"><span data-stu-id="ad48a-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="ad48a-117">NuGet.org のシンボル サーバーは、新しいシンボル パッケージ形式 `.snupkg` のみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-117">NuGet.org symbols server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="ad48a-118">シンボル パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="ad48a-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="ad48a-119">便宜上、最初に NuGet で API キーを保存してください (「[パッケージを公開する](../create-packages/publish-a-package.md)」を参照)。</span><span class="sxs-lookup"><span data-stu-id="ad48a-119">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="ad48a-120">nuget.org にプライマリ パッケージを公開した後は、次のようにしてシンボル パッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="ad48a-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="ad48a-121">以下のコマンドを使用して、プライマリ パッケージとシンボル パッケージの両方を同時にプッシュすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="ad48a-122">.nupkg および .snupkg ファイルの両方が、現在のフォルダーに存在する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad48a-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="ad48a-123">NuGet では、両方のパッケージが nuget.org に公開されます。最初に `MyPackage.nupkg` が、次に `MyPackage.snupkg` が公開されます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="ad48a-124">NuGet.org のシンボル サーバー</span><span class="sxs-lookup"><span data-stu-id="ad48a-124">NuGet.org symbol server</span></span>

<span data-ttu-id="ad48a-125">NuGet.org は独自のシンボル サーバー リポジトリをサポートし、新しいシンボル パッケージ形式 `.snupkg` のみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-125">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="ad48a-126">パッケージ コンシューマーは Visual Studio で自分のシンボル ソースに `https://symbols.nuget.org/download/symbols` を追加することで、nuget.org シンボル サーバーに公開されたシンボルを使用できます。それにより、Visual Studio デバッガーでパッケージ コードに入ることができます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-126">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="ad48a-127">このプロセスの詳細については、「[Visual Studio デバッガーでのシンボル (.pdb) ファイルとソース ファイルの指定](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad48a-127">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="ad48a-128">Nuget.org シンボル パッケージの制約</span><span class="sxs-lookup"><span data-stu-id="ad48a-128">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="ad48a-129">nuget.org でサポートされているシンボル パッケージには、次の 2 つの制約があります</span><span class="sxs-lookup"><span data-stu-id="ad48a-129">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="ad48a-130">次のファイル拡張子のみをシンボル パッケージに追加できます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-130">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="ad48a-131">nuget シンボル サーバーでは管理対象の[ポータブル PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) のみが現在サポートされています。</span><span class="sxs-lookup"><span data-stu-id="ad48a-131">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="ad48a-132">PDB と関連付けられている nupkg dll は、Visual studio バージョン 15.9 以上のコンパイラでビルドする必要があります ([pdb 暗号化ハッシュ](https://github.com/dotnet/roslyn/issues/24429)に関する記事を参照)</span><span class="sxs-lookup"><span data-stu-id="ad48a-132">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="ad48a-133">それ以外のファイルの種類が .snupkg に含まれていると、nuget.org でのシンボル パッケージの公開は失敗します。</span><span class="sxs-lookup"><span data-stu-id="ad48a-133">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="ad48a-134">シンボル パッケージの検証とインデックスの作成</span><span class="sxs-lookup"><span data-stu-id="ad48a-134">Symbol package validation and indexing</span></span>

<span data-ttu-id="ad48a-135">[NuGet.org](https://www.nuget.org/) にプッシュされたパッケージは、ウイルス チェックなど、いくつかの検証を受けます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-135">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="ad48a-136">パッケージがすべての検証チェックに合格してから、シンボルのインデックスを作成し、NuGet.org シンボル サーバーで使用できるようになるまでには少し時間がかかります。</span><span class="sxs-lookup"><span data-stu-id="ad48a-136">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="ad48a-137">パッケージが検証チェックで不合格になった場合、.nupkg のパッケージの詳細ページが更新され、関連エラーが表示されます。それに関する電子メールも届きます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-137">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="ad48a-138">パッケージの検証とインデックスの作成は、通常、15 以内で完了します。</span><span class="sxs-lookup"><span data-stu-id="ad48a-138">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="ad48a-139">パッケージ公開に予想以上の時間がかかる場合、[status.nuget.org](https://status.nuget.org/) にアクセスし、nuget.org に中断が発生していないか確認してください。</span><span class="sxs-lookup"><span data-stu-id="ad48a-139">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="ad48a-140">すべてのシステムが動作しているとき、1 時間以内にパッケージが正常に公開されない場合、nuget.org にログインし、パッケージの詳細ページの [Contact Support] リンクからお問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="ad48a-140">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="ad48a-141">シンボル パッケージ構造</span><span class="sxs-lookup"><span data-stu-id="ad48a-141">Symbol package structure</span></span>

<span data-ttu-id="ad48a-142">.nupkg ファイルは全く変わりませんが、.snupkg ファイルには次の特性が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-142">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="ad48a-143">.snupkg の ID とバージョンは、対応する .nupkg と同じになります。</span><span class="sxs-lookup"><span data-stu-id="ad48a-143">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="ad48a-144">.snupkg のファイル構造は DLL や EXE ファイルの nupkg と全く同じですが、区別されています。対応する PDB が同じフォルダ構造に含まれています。</span><span class="sxs-lookup"><span data-stu-id="ad48a-144">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="ad48a-145">PDB 以外の拡張子のファイルとフォルダーは snupkg から除外されたままになります。</span><span class="sxs-lookup"><span data-stu-id="ad48a-145">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="ad48a-146">.snupkg の .nuspec ファイルでは次に示すように新しい PackageType も指定されます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-146">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="ad48a-147">指定される PackageType は 1 つだけです。</span><span class="sxs-lookup"><span data-stu-id="ad48a-147">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="ad48a-148">作成者が nupkg と snupkg のビルドにカスタムの nuspec を使用した場合、snupkg には 2) で説明したものと同じフォルダ階層とファイルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-148">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="ad48a-149">```authors``` と ```owners``` のフィールドは snupkg の nuspec から除外されます。</span><span class="sxs-lookup"><span data-stu-id="ad48a-149">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="ad48a-150">参照</span><span class="sxs-lookup"><span data-stu-id="ad48a-150">See Also</span></span>

[<span data-ttu-id="ad48a-151">NuGet パッケージのデバッグとシンボルの改善</span><span class="sxs-lookup"><span data-stu-id="ad48a-151">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
