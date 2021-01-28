---
title: NuGet パッケージの種類を設定する
description: パッケージの使用目的を示すパッケージの種類について説明します。
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774364"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="3b6a6-103">NuGet パッケージの種類を設定する</span><span class="sxs-lookup"><span data-stu-id="3b6a6-103">Set a NuGet package type</span></span>

<span data-ttu-id="3b6a6-104">NuGet 3.5+ では、パッケージに特定の *パッケージの種類* の印を付け、その用途を示すことができます。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="3b6a6-105">種類の印が付いていないパッケージ (初期のバージョンの NuGet で作成されたすべてのパッケージが相当) は種類が `Dependency` に初期設定されます。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="3b6a6-106">種類が `Dependency` のパッケージでは、ビルド時または実行時アセットがライブラリとアプリケーションに追加されます。(互換性があれば) あらゆる種類のプロジェクトにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="3b6a6-107">種類が `DotnetTool` であるパッケージは [dotnet CLI](/dotnet/articles/core/tools/index) の拡張であり、コマンド ラインから呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="3b6a6-108">このようなパッケージは .NET Core プロジェクトにのみインストールできます。復元操作には影響を与えません。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="3b6a6-109">このようなプロジェクト別の拡張機能に関する詳細は、[.NET Core 拡張性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)ドキュメントにあります。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="3b6a6-110">`Template` 型パッケージには、アプリ、サービス、ツール、クラス ライブラリなどのファイルまたはプロジェクトの作成に使用できる[カスタム テンプレート](/dotnet/core/tools/custom-templates)があります。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="3b6a6-111">カスタム タイプのパッケージでは、パッケージ ID と同じ形式ルールに準拠する任意の種類識別子が使用されます。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="3b6a6-112">ただし、`Dependency` と `DotnetTool` 以外の種類は、Visual Studio の NuGet パッケージ マネージャーには認識されません。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="3b6a6-113">パッケージの種類は `.nuspec` ファイルで設定されます。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="3b6a6-114">下位互換性を維持するには、種類 `Dependency` を明示的に設定 *しない* で、NuGet に依存するのが最適な方法です。NuGet は、種類が指定されない場合、この種類を想定します。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="3b6a6-115">`.nuspec`: `<metadata>` 要素の下の `packageTypes\packageType` ノード内のパッケージの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="3b6a6-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
