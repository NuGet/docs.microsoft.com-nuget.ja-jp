---
title: "ネイティブ NuGet パッケージを作成する | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 7a70d748-efe2-4f8f-a3fd-67ddb0f6214e
description: "C++ プロジェクト用にマネージ コードではなく、C++ コードを含むネイティブ NuGet パッケージを作成する方法に関する詳細です。"
keywords: "NuGet ネイティブ パッケージ、NuGet C++ パッケージ、ネイティブ コード パッケージ、C++ プロジェクトを対象とする"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fa5baaa6ecbad0f5f6dd85d657679ffbbbc8a47a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="creating-native-packages"></a><span data-ttu-id="18e88-104">ネイティブ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="18e88-104">Creating native packages</span></span>

<span data-ttu-id="18e88-105">ネイティブ パッケージには、マネージ コードの代わりに、C++ プロジェクト内で使用することを可能にするネイティブ C++ コードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="18e88-105">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="18e88-106">(「使用」セクションの「[ネイティブ C++ パッケージ](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages)」を参照してください。)</span><span class="sxs-lookup"><span data-stu-id="18e88-106">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) in the Consume section.)</span></span>

<span data-ttu-id="18e88-107">C++ プロジェクトで使用できるようにするには、パッケージが `native` フレームワークを対象にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="18e88-107">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="18e88-108">現時点では、NuGet ですべての C++ プロジェクトが同様に処理されるように、このフレームワークに関連付けられているバージョン番号はありません。</span><span class="sxs-lookup"><span data-stu-id="18e88-108">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="18e88-109">他の開発者がタグを検索して、お客様のパッケージを見つけられるように、必ず `.nuspec` の `<tags>` セクションに *native* を含めてください。</span><span class="sxs-lookup"><span data-stu-id="18e88-109">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="18e88-110">`native` を対象とするネイティブ NuGet パッケージでは、`\build`、`\content`、および `\tools` フォルダーにファイルが提供されます。`\lib` はこの場合、使用されません (NuGet では、直接 C++ プロジェクトに参照を追加することはできません)。</span><span class="sxs-lookup"><span data-stu-id="18e88-110">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="18e88-111">パッケージには、`\build` のターゲットとプロパティ ファイルも含まれる場合があります。このファイルは、NuGet によってパッケージを使用するプロジェクトに自動的にインポートされます。</span><span class="sxs-lookup"><span data-stu-id="18e88-111">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="18e88-112">これらのファイルは、`.targets` や `.props` の拡張子を含むパッケージ ID と同じ名前になります。</span><span class="sxs-lookup"><span data-stu-id="18e88-112">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="18e88-113">たとえば、[cpprestsdk](https://nuget.org/packages/cpprestsdk/) パッケージでは、`\build` フォルダーに `cpprestsdk.targets` ファイルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="18e88-113">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="18e88-114">`\build` フォルダーは、ネイティブ パッケージだけでなく、すべての NuGet パッケージに使用できます。</span><span class="sxs-lookup"><span data-stu-id="18e88-114">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="18e88-115">`\build` フォルダーでは、`\content`、`\lib`、`\tools` フォルダーと同様に、ターゲット フレームワークが尊重されます。</span><span class="sxs-lookup"><span data-stu-id="18e88-115">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="18e88-116">つまり、`\build\net40` フォルダーと `\build\net45` フォルダーを作成でき、NuGet では適切なプロパティ ファイルとターゲット ファイルがプロジェクトにインポートされるということです。</span><span class="sxs-lookup"><span data-stu-id="18e88-116">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="18e88-117">(MSBuild ターゲットをインポートするために、PowerShell スクリプトを使用する必要はありません。)</span><span class="sxs-lookup"><span data-stu-id="18e88-117">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
