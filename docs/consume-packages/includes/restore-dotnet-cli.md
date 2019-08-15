---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860600"
---
<span data-ttu-id="8517a-101">[dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用すると、プロジェクト ファイルに一覧表示されているパッケージが復元されます ([PackageReference](../../consume-packages/package-references-in-project-files.md) 参照)。</span><span class="sxs-lookup"><span data-stu-id="8517a-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="8517a-102">.NET Core 2.0 以降では、復元は、`dotnet build` と `dotnet run` で自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="8517a-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="8517a-103">NuGet 4.0 以降、`nuget restore` と同じコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="8517a-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="8517a-104">他の `dotnet` CLI コマンドと同様に、最初にコマンド ラインが開かれ、使用するプロジェクト ファイルが含まれているディレクトリに切り替えられます。</span><span class="sxs-lookup"><span data-stu-id="8517a-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="8517a-105">`dotnet restore` を使用してパッケージを復元するには:</span><span class="sxs-lookup"><span data-stu-id="8517a-105">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```