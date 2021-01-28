---
title: ネイティブ NuGet パッケージを作成する
description: C++ プロジェクト用にマネージド コードではなく、C++ コードを含むネイティブ NuGet パッケージを作成する方法に関する詳細です。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 2a95fca2ce5496512627e913273e5b66128e34c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774203"
---
# <a name="creating-native-packages"></a><span data-ttu-id="9130a-103">ネイティブ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="9130a-103">Creating native packages</span></span>

<span data-ttu-id="9130a-104">ネイティブ パッケージには、マネージド アセンブリではなくネイティブ バイナリが含まれているため、C++ (または同様の) プロジェクト内で使用できます。</span><span class="sxs-lookup"><span data-stu-id="9130a-104">A native package contains native binaries instead of managed assemblies, allowing it to be used within C++ (or similar) projects.</span></span> <span data-ttu-id="9130a-105">(「使用」セクションの「[ネイティブ C++ パッケージ](../consume-packages/finding-and-choosing-packages.md#native-c-packages)」を参照してください。)</span><span class="sxs-lookup"><span data-stu-id="9130a-105">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) in the Consume section.)</span></span>

<span data-ttu-id="9130a-106">C++ プロジェクトで使用できるようにするには、パッケージが `native` フレームワークを対象にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9130a-106">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="9130a-107">現時点では、NuGet ですべての C++ プロジェクトが同様に処理されるように、このフレームワークに関連付けられているバージョン番号はありません。</span><span class="sxs-lookup"><span data-stu-id="9130a-107">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="9130a-108">他の開発者がタグを検索して、お客様のパッケージを見つけられるように、必ず `.nuspec` の `<tags>` セクションに *native* を含めてください。</span><span class="sxs-lookup"><span data-stu-id="9130a-108">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="9130a-109">`native` を対象とするネイティブ NuGet パッケージでは、`\build`、`\content`、および `\tools` フォルダーにファイルが提供されます。`\lib` はこの場合、使用されません (NuGet では、直接 C++ プロジェクトに参照を追加することはできません)。</span><span class="sxs-lookup"><span data-stu-id="9130a-109">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="9130a-110">パッケージには、`\build` のターゲットとプロパティ ファイルも含まれる場合があります。このファイルは、NuGet によってパッケージを使用するプロジェクトに自動的にインポートされます。</span><span class="sxs-lookup"><span data-stu-id="9130a-110">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="9130a-111">これらのファイルは、`.targets` や `.props` の拡張子を含むパッケージ ID と同じ名前になります。</span><span class="sxs-lookup"><span data-stu-id="9130a-111">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="9130a-112">たとえば、[cpprestsdk](https://nuget.org/packages/cpprestsdk/) パッケージでは、`\build` フォルダーに `cpprestsdk.targets` ファイルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="9130a-112">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="9130a-113">`\build` フォルダーは、ネイティブ パッケージだけでなく、すべての NuGet パッケージに使用できます。</span><span class="sxs-lookup"><span data-stu-id="9130a-113">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="9130a-114">`\build` フォルダーでは、`\content`、`\lib`、`\tools` フォルダーと同様に、ターゲット フレームワークが尊重されます。</span><span class="sxs-lookup"><span data-stu-id="9130a-114">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="9130a-115">つまり、`\build\net40` フォルダーと `\build\net45` フォルダーを作成でき、NuGet では適切なプロパティ ファイルとターゲット ファイルがプロジェクトにインポートされるということです。</span><span class="sxs-lookup"><span data-stu-id="9130a-115">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="9130a-116">(MSBuild ターゲットをインポートするために、PowerShell スクリプトを使用する必要はありません。)</span><span class="sxs-lookup"><span data-stu-id="9130a-116">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
