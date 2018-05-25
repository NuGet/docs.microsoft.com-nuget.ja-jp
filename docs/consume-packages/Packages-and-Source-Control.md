---
title: NuGet パッケージとソース管理
description: バージョン管理システムとソース管理システム内で NuGet パッケージを処理する方法、git と TFVC でパッケージを省略する方法に関する考慮事項です。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: bc2c6d5e9933f2f6103363a2e69fbb9b47f80ecf
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="464f9-103">ソース管理システムで NuGet パッケージを省略する</span><span class="sxs-lookup"><span data-stu-id="464f9-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="464f9-104">通常、開発者はソース管理リポジトリの NuGet パッケージを省略し、代わりに[パッケージの復元](package-restore.md)に依存して、ビルド前にプロジェクトの依存関係を再インストールします。</span><span class="sxs-lookup"><span data-stu-id="464f9-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="464f9-105">パッケージの復元に依存する理由には、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="464f9-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="464f9-106">分散型バージョン管理システム (Git など) には、リポジトリ内のすべてのファイルのすべてのバージョンの完全なコピーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="464f9-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="464f9-107">頻繁に更新されるバイナリ ファイルは大幅に肥大化し、リポジトリを複製する時間が長くなります。</span><span class="sxs-lookup"><span data-stu-id="464f9-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="464f9-108">パッケージがリポジトリに含まれる場合、開発者は、プロジェクト内でハードコーディングされたパス名につながる、NuGet を使用してパッケージを参照するよりも、ディスク上のパッケージ コンテンツに直接、参照を追加する傾向にあります。</span><span class="sxs-lookup"><span data-stu-id="464f9-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="464f9-109">使用中のパッケージを削除しないようにする必要があるので、未使用のパッケージ フォルダーのソリューションをクリーンにするのが難しくなります。</span><span class="sxs-lookup"><span data-stu-id="464f9-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="464f9-110">パッケージを省略して、自分が依存するその他のユーザーからのコードとパッケージの間に所有者のクリーンな境界を維持します。</span><span class="sxs-lookup"><span data-stu-id="464f9-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="464f9-111">多くの NuGet パッケージは、独自のソース管理リポジトリに保持されます。</span><span class="sxs-lookup"><span data-stu-id="464f9-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="464f9-112">パッケージの復元は NuGet と共に既定の動作ですが、ソース管理からパッケージ&mdash;つまり、プロジェクトの `packages` フォルダー&mdash;を省略するには、以下のセクションで示すように、一部手動の操作を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="464f9-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="464f9-113">Git でパッケージを省略する</span><span class="sxs-lookup"><span data-stu-id="464f9-113">Omitting packages with Git</span></span>

<span data-ttu-id="464f9-114">[.gitignore ファイル](https://git-scm.com/docs/gitignore)を使用して、中でも NuGet パッケージ (`.nupkg`)、`packages` フォルダー、`project.assets.json` を省略します。</span><span class="sxs-lookup"><span data-stu-id="464f9-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="464f9-115">[Visual Studio プロジェクトの `.gitignore` のサンプル](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="464f9-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="464f9-116">`.gitignore` ファイルの重要な部分は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="464f9-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="464f9-117">Team Foundation バージョン管理でパッケージを省略する</span><span class="sxs-lookup"><span data-stu-id="464f9-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="464f9-118">ソース管理にプロジェクトを追加する*前に*、可能であればこれらの手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="464f9-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="464f9-119">それ以外の場合は、自分のリポジトリから `packages` フォルダーを手動で削除して、続行する前にその変更をチェックインします。</span><span class="sxs-lookup"><span data-stu-id="464f9-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="464f9-120">選択したファイルの TFVC とのソース管理の統合を無効にするには</span><span class="sxs-lookup"><span data-stu-id="464f9-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="464f9-121">ソリューション フォルダー (`.sln` ファイルがある場所) で `.nuget` という名前のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="464f9-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="464f9-122">ヒント: Windows 上のエクスプローラーでこのフォルダーを作成するには、末尾のドットを*含む* `.nuget.` という名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="464f9-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="464f9-123">そのフォルダーで、`NuGet.Config` という名前のファイルを作成し、編集するために開きます。</span><span class="sxs-lookup"><span data-stu-id="464f9-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="464f9-124">[disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) の設定によって Visual Studio で `packages` フォルダーのすべてをスキップするように指示している場合、少なくとも次のテキストを追加します。</span><span class="sxs-lookup"><span data-stu-id="464f9-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="464f9-125">TFS 2010 以前を使用している場合は、自分のワークスペース マッピングで `packages` フォルダーをクロークします。</span><span class="sxs-lookup"><span data-stu-id="464f9-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="464f9-126">TFS 2012 以降、または Visual Studio Team Services を使用して、「[Add Files to the Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore)」 (サーバーにファイルを追加する) で説明されているように、`.tfignore` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="464f9-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span></span> <span data-ttu-id="464f9-127">そのファイルには、リポジトリ レベルの `\packages` フォルダーおよび他のいくつかの中間ファイルに対する変更を明示的に無視するように、以下のコンテンツを含めます。</span><span class="sxs-lookup"><span data-stu-id="464f9-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="464f9-128">(末尾のドットを含む `.tfignore.` という名前を使用して、エクスプローラーでファイルを作成できますが、最初に "Hide known file extensions" (既知のファイル拡張子を非表示にする) オプションを無効にする必要がある場合があります。)</span><span class="sxs-lookup"><span data-stu-id="464f9-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="464f9-129">`NuGet.Config` と `.tfignore` をソース管理に追加し、自分の変更をチェックインします。</span><span class="sxs-lookup"><span data-stu-id="464f9-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
