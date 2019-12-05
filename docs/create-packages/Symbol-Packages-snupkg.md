---
title: 新しいシンボル パッケージ形式 '.snupkg' を使用して NuGet シンボル パッケージを公開する方法 | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
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
ms.openlocfilehash: 8528261f90e75e2dfac8cb746b396d227c3741f4
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825186"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="dde64-104">シンボル パッケージ (.snupkg) の作成</span><span class="sxs-lookup"><span data-stu-id="dde64-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="dde64-105">シンボル パッケージを利用すると、NuGet パッケージのデバッグがしやすくなります。</span><span class="sxs-lookup"><span data-stu-id="dde64-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dde64-106">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="dde64-106">Prerequisites</span></span>

<span data-ttu-id="dde64-107">必要な [NuGet プロトコル](../api/nuget-protocols.md)を実装する、[nuget.exe v4.9.0 以上](https://www.nuget.org/downloads)または [dotnet.exe v2.2.0 以上](https://www.microsoft.com/net/download/dotnet-core/2.2)。</span><span class="sxs-lookup"><span data-stu-id="dde64-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="dde64-108">シンボル パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="dde64-108">Creating a symbol package</span></span>

<span data-ttu-id="dde64-109">dotnet.exe または MSBuild を使用する場合は、`IncludeSymbols` プロパティと `SymbolPackageFormat` プロパティを設定し、.nupkg ファイルに加えて .snupkg ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="dde64-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="dde64-110">次のプロパティを .csproj ファイルに追加するか:</span><span class="sxs-lookup"><span data-stu-id="dde64-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="dde64-111">または、コマンド ラインで次のプロパティを指定します:</span><span class="sxs-lookup"><span data-stu-id="dde64-111">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="dde64-112">or</span><span class="sxs-lookup"><span data-stu-id="dde64-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="dde64-113">NuGet.exe を使用する場合は、次のコマンドを使用すると .nupkg ファイルに加えて .snupkg ファイルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="dde64-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="dde64-114">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) プロパティには、`symbols.nupkg` (既定値) または `snupkg` の 2 つの値のいずれかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="dde64-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="dde64-115">このプロパティが指定されていない場合は、レガシ シンボル パッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="dde64-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="dde64-116">従来の形式 `.symbols.nupkg` は引き続きサポートされますが、これは互換性のみを目的としています ([レガシ シンボル パッケージ](Symbol-Packages.md)に関する記事を参照)。</span><span class="sxs-lookup"><span data-stu-id="dde64-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="dde64-117">NuGet.org のシンボル サーバーは、新しいシンボル パッケージ形式 `.snupkg` のみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="dde64-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="dde64-118">シンボル パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="dde64-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="dde64-119">便宜上、最初に NuGet で API キーを保存してください (「[パッケージを公開する](../nuget-org/publish-a-package.md)」を参照)。</span><span class="sxs-lookup"><span data-stu-id="dde64-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="dde64-120">nuget.org にプライマリ パッケージを公開した後は、次のようにしてシンボル パッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="dde64-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="dde64-121">以下のコマンドを使用して、プライマリ パッケージとシンボル パッケージの両方を同時にプッシュすることもできます。</span><span class="sxs-lookup"><span data-stu-id="dde64-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="dde64-122">.nupkg および .snupkg ファイルの両方が、現在のフォルダーに存在する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dde64-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="dde64-123">NuGet では、両方のパッケージが nuget.org に公開されます。最初に `MyPackage.nupkg` が、次に `MyPackage.snupkg` が公開されます。</span><span class="sxs-lookup"><span data-stu-id="dde64-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="dde64-124">シンボル パッケージが公開されていない場合は、NuGet.org のソースを `https://api.nuget.org/v3/index.json` として構成したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="dde64-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="dde64-125">シンボル パッケージの公開は、[NuGet V3 API](../api/overview.md#versioning) によってのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="dde64-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="dde64-126">NuGet.org のシンボル サーバー</span><span class="sxs-lookup"><span data-stu-id="dde64-126">NuGet.org symbol server</span></span>

<span data-ttu-id="dde64-127">NuGet.org は独自のシンボル サーバー リポジトリをサポートし、新しいシンボル パッケージ形式 `.snupkg` のみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="dde64-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="dde64-128">パッケージ コンシューマーは Visual Studio で自分のシンボル ソースに `https://symbols.nuget.org/download/symbols` を追加することで、nuget.org シンボル サーバーに公開されたシンボルを使用できます。それにより、Visual Studio デバッガーでパッケージ コードに入ることができます。</span><span class="sxs-lookup"><span data-stu-id="dde64-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="dde64-129">このプロセスの詳細については、「[Visual Studio デバッガーでのシンボル (.pdb) ファイルとソース ファイルの指定](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dde64-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="dde64-130">NuGet.org シンボル パッケージの制約</span><span class="sxs-lookup"><span data-stu-id="dde64-130">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="dde64-131">NuGet.org には、シンボル パッケージに対して次の制約があります。</span><span class="sxs-lookup"><span data-stu-id="dde64-131">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="dde64-132">シンボル パッケージでは、次のファイル拡張子のみが許可されます: `.pdb`、`.nuspec`、`.xml`、`.psmdcp`、`.rels`、`.p7s`</span><span class="sxs-lookup"><span data-stu-id="dde64-132">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="dde64-133">NuGet.org のシンボル サーバーでは管理対象の[ポータブル PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) のみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="dde64-133">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="dde64-134">PDB と関連付けられている .nupkg DLL は、Visual Studio バージョン 15.9 以上のコンパイラでビルドする必要があります (「[PDB 暗号化ハッシュ](https://github.com/dotnet/roslyn/issues/24429)」を参照)</span><span class="sxs-lookup"><span data-stu-id="dde64-134">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="dde64-135">これらの制約が満たされない場合、NuGet.org に発行されたシンボル パッケージは検証に失敗します。</span><span class="sxs-lookup"><span data-stu-id="dde64-135">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="dde64-136">シンボル パッケージの検証とインデックスの作成</span><span class="sxs-lookup"><span data-stu-id="dde64-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="dde64-137">[NuGet.org](https://www.nuget.org/) に発行されたシンボル パッケージは、マルウェアのスキャンなど、いくつかの検証を受けます。</span><span class="sxs-lookup"><span data-stu-id="dde64-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="dde64-138">パッケージが検証チェックに失敗した場合、そのパッケージの詳細ページにエラー メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="dde64-138">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="dde64-139">さらに、パッケージの所有者は、特定された問題の修正方法を示す電子メールを受信します。</span><span class="sxs-lookup"><span data-stu-id="dde64-139">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="dde64-140">シンボル パッケージがすべての検証に合格すると、シンボルは NuGet. org のシンボル サーバーによってインデックスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="dde64-140">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers.</span></span> <span data-ttu-id="dde64-141">インデックスが作成されると、シンボルは NuGet.org シンボル サーバーから使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="dde64-141">Once indexed, the symbol will be available for consumption from the NuGet.org symbol servers.</span></span>

<span data-ttu-id="dde64-142">パッケージの検証とインデックスの作成は、通常、15 以内で完了します。</span><span class="sxs-lookup"><span data-stu-id="dde64-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="dde64-143">パッケージ公開に予想以上の時間がかかる場合、[status.nuget.org](https://status.nuget.org/) にアクセスし、NuGet.org に中断が発生していないか確認してください。</span><span class="sxs-lookup"><span data-stu-id="dde64-143">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="dde64-144">すべてのシステムが動作しているとき、1 時間以内にパッケージが正常に公開されない場合、nuget.org にログインし、パッケージの詳細ページの [Contact Support] リンクからお問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="dde64-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="dde64-145">シンボル パッケージ構造</span><span class="sxs-lookup"><span data-stu-id="dde64-145">Symbol package structure</span></span>

<span data-ttu-id="dde64-146">.nupkg ファイルは全く変わりませんが、.snupkg ファイルには次の特性が含まれます。</span><span class="sxs-lookup"><span data-stu-id="dde64-146">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="dde64-147">.snupkg の ID とバージョンは、対応する .nupkg と同じになります。</span><span class="sxs-lookup"><span data-stu-id="dde64-147">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="dde64-148">.snupkg のファイル構造は DLL や EXE ファイルの nupkg と全く同じですが、区別されています。対応する PDB が同じフォルダ構造に含まれています。</span><span class="sxs-lookup"><span data-stu-id="dde64-148">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="dde64-149">PDB 以外の拡張子のファイルとフォルダーは snupkg から除外されたままになります。</span><span class="sxs-lookup"><span data-stu-id="dde64-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="dde64-150">.snupkg の .nuspec ファイルでは次に示すように新しい PackageType も指定されます。</span><span class="sxs-lookup"><span data-stu-id="dde64-150">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="dde64-151">指定される PackageType は 1 つだけです。</span><span class="sxs-lookup"><span data-stu-id="dde64-151">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="dde64-152">作成者が nupkg と snupkg のビルドにカスタムの nuspec を使用した場合、snupkg には 2) で説明したものと同じフォルダ階層とファイルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="dde64-152">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="dde64-153">```authors``` と ```owners``` のフィールドは snupkg の nuspec から除外されます。</span><span class="sxs-lookup"><span data-stu-id="dde64-153">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="dde64-154">```<license>``` 要素は使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="dde64-154">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="dde64-155">.snupkg には、対応する .nupkg と同じライセンスが適用されます。</span><span class="sxs-lookup"><span data-stu-id="dde64-155">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="dde64-156">関連項目</span><span class="sxs-lookup"><span data-stu-id="dde64-156">See also</span></span>

<span data-ttu-id="dde64-157">ソース リンクを使用して、.NET アセンブリのソース コードのデバッグを有効にすることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="dde64-157">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="dde64-158">詳細については、「[ソース リンクのガイダンス](/dotnet/standard/library-guidance/sourcelink)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dde64-158">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="dde64-159">シンボル パッケージの詳細については、「[NuGet パッケージのデバッグとシンボルの機能強化](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)」の設計仕様を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dde64-159">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
