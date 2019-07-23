---
ms.openlocfilehash: bb39e1056ea97ecf1ac70d7fd8e79e65dc04655c
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842142"
---
1. <span data-ttu-id="4879a-101">`.nupkg` ファイルを含むフォルダーに変更します。</span><span class="sxs-lookup"><span data-stu-id="4879a-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="4879a-102">使用するパッケージ名 (一意のパッケージ ID) を指定し、キーの値を使用する API キーに置き換えて、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="4879a-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="4879a-103">dotnet により、公開プロセスの結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="4879a-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="4879a-104">「[dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4879a-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>