---
title: "NuGet パッケージとソース管理 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "バージョン管理システムとソース管理システム内で NuGet パッケージを処理する方法、git と TFVC でパッケージを省略する方法に関する考慮事項です。"
keywords: "NuGet のソース管理、NuGet のバージョン管理、NuGet と git、NuGet と TFS、NuGet と TFVC、パッケージの省略、ソース管理リポジトリ、バージョン管理リポジトリ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6261625d5d7eaa748f9ad15510b7b2af3c814e44
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="3d628-104">ソース管理システムで NuGet パッケージを省略する</span><span class="sxs-lookup"><span data-stu-id="3d628-104">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="3d628-105">通常、開発者はソース管理リポジトリの NuGet パッケージを省略し、代わりに[パッケージの復元](../consume-packages/package-restore.md)に依存して、ビルド前にプロジェクトの依存関係を再インストールします。</span><span class="sxs-lookup"><span data-stu-id="3d628-105">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](../consume-packages/package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="3d628-106">パッケージの復元に依存する理由には、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="3d628-106">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="3d628-107">分散型バージョン管理システム (Git など) には、リポジトリ内のすべてのファイルのすべてのバージョンの完全なコピーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3d628-107">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="3d628-108">頻繁に更新されるバイナリ ファイルは大幅に肥大化し、リポジトリを複製する時間が長くなります。</span><span class="sxs-lookup"><span data-stu-id="3d628-108">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="3d628-109">パッケージがリポジトリに含まれる場合、開発者は、プロジェクト内でハードコーディングされたパス名につながる、NuGet を使用してパッケージを参照するよりも、ディスク上のパッケージ コンテンツに直接、参照を追加する傾向にあります。</span><span class="sxs-lookup"><span data-stu-id="3d628-109">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="3d628-110">使用中のパッケージを削除しないようにする必要があるので、未使用のパッケージ フォルダーのソリューションをクリーンにするのが難しくなります。</span><span class="sxs-lookup"><span data-stu-id="3d628-110">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="3d628-111">パッケージを省略して、自分が依存するその他のユーザーからのコードとパッケージの間に所有者のクリーンな境界を維持します。</span><span class="sxs-lookup"><span data-stu-id="3d628-111">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="3d628-112">多くの NuGet パッケージは、独自のソース管理リポジトリに保持されます。</span><span class="sxs-lookup"><span data-stu-id="3d628-112">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="3d628-113">パッケージの復元は NuGet を使用した既定の動作ですが、一部の手動の動作は、以下のセクションで示すように、ソース管理からパッケージ&mdash;名前は、プロジェクトの `packages` フォルダー&mdash;を省略する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d628-113">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in the following sections.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="3d628-114">Git でパッケージを省略する</span><span class="sxs-lookup"><span data-stu-id="3d628-114">Omitting packages with Git</span></span>

<span data-ttu-id="3d628-115">ソース管理に `packages` フォルダーが含まれないようにするには、[.gitignore ファイル](https://git-scm.com/docs/gitignore)を使用します。</span><span class="sxs-lookup"><span data-stu-id="3d628-115">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to avoid including the `packages` folder in source control.</span></span> <span data-ttu-id="3d628-116">[Visual Studio プロジェクトの `.gitignore` のサンプル](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3d628-116">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="3d628-117">`.gitignore` ファイルの重要な部分は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="3d628-117">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="3d628-118">Team Foundation バージョン管理でパッケージを省略する</span><span class="sxs-lookup"><span data-stu-id="3d628-118">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="3d628-119">ソース管理にプロジェクトを追加する*前に*、可能であればこれらの手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="3d628-119">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="3d628-120">それ以外の場合は、自分のリポジトリから `packages` フォルダーを手動で削除して、続行する前にその変更をチェックインします。</span><span class="sxs-lookup"><span data-stu-id="3d628-120">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="3d628-121">選択したファイルの TFVC とのソース管理の統合を無効にするには</span><span class="sxs-lookup"><span data-stu-id="3d628-121">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="3d628-122">ソリューション フォルダー (`.sln` ファイルがある場所) で `.nuget` という名前のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="3d628-122">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="3d628-123">ヒント: Windows 上のエクスプローラーでこのフォルダーを作成するには、末尾のドットを*含む* `.nuget.` という名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="3d628-123">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="3d628-124">そのフォルダーで、`NuGet.Config` という名前のファイルを作成し、編集するために開きます。</span><span class="sxs-lookup"><span data-stu-id="3d628-124">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="3d628-125">[disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) の設定によって Visual Studio で `packages` フォルダーのすべてをスキップするように指示している場合、少なくとも次のテキストを追加します。</span><span class="sxs-lookup"><span data-stu-id="3d628-125">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="3d628-126">TFS 2010 以前を使用している場合は、自分のワークスペース マッピングで `packages` フォルダーをクロークします。</span><span class="sxs-lookup"><span data-stu-id="3d628-126">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="3d628-127">TFS 2012 以降、または Visual Studio Team Services を使用して、「[Add Files to the Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore)」 (サーバーにファイルを追加する) で説明されているように、`.tfignore` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="3d628-127">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span></span> <span data-ttu-id="3d628-128">そのファイルには、リポジトリ レベルの `\packages` フォルダーおよび他のいくつかの中間ファイルに対する変更を明示的に無視するように、以下のコンテンツを含めます。</span><span class="sxs-lookup"><span data-stu-id="3d628-128">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="3d628-129">(末尾のドットを含む `.tfignore.` という名前を使用して、エクスプローラーでファイルを作成できますが、最初に "Hide known file extensions" (既知のファイル拡張子を非表示にする) オプションを無効にする必要がある場合があります。)</span><span class="sxs-lookup"><span data-stu-id="3d628-129">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="3d628-130">`NuGet.Config` と `.tfignore` をソース管理に追加し、自分の変更をチェックインします。</span><span class="sxs-lookup"><span data-stu-id="3d628-130">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
