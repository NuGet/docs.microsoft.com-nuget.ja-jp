---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860573"
---
<span data-ttu-id="5b30a-101">[restore](../../reference/cli-reference/cli-ref-restore.md) コマンドを使用すると、*packages* フォルダーにないすべてのパッケージがダウンロードされ、インストールされます。</span><span class="sxs-lookup"><span data-stu-id="5b30a-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="5b30a-102">PackageReference に移行されたプロジェクトの場合は、代わりに [msbuild -t:restore](../package-restore.md#restore-using-msbuild) を使ってパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="5b30a-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="5b30a-103">`restore` ではパッケージがディスクに追加されるだけで、プロジェクトの依存関係は変更されません。</span><span class="sxs-lookup"><span data-stu-id="5b30a-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="5b30a-104">プロジェクトの依存関係を復元するには、`packages.config` を変更し、`restore` コマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="5b30a-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="5b30a-105">他の `nuget.exe` CLI コマンドと同様に、最初にコマンド ラインが開かれ、使用するプロジェクト ファイルが含まれているディレクトリに切り替えられます。</span><span class="sxs-lookup"><span data-stu-id="5b30a-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="5b30a-106">`restore` を使用してパッケージを復元するには:</span><span class="sxs-lookup"><span data-stu-id="5b30a-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```