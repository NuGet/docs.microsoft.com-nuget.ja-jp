---
ms.openlocfilehash: 9167b4b5943dd797c5a4cb20e53ee6832f0b3021
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623027"
---
1. <span data-ttu-id="6fb9a-101">`.nupkg` ファイルを含むフォルダーに変更します。</span><span class="sxs-lookup"><span data-stu-id="6fb9a-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="6fb9a-102">使用するパッケージ名 (一意のパッケージ ID) を指定し、キーの値を使用する API キーに置き換えて、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="6fb9a-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg --api-key qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 --source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="6fb9a-103">dotnet により、公開プロセスの結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6fb9a-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="6fb9a-104">「[dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6fb9a-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>