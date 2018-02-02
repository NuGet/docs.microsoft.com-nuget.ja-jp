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
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>ソース管理システムで NuGet パッケージを省略する

通常、開発者はソース管理リポジトリの NuGet パッケージを省略し、代わりに[パッケージの復元](../consume-packages/package-restore.md)に依存して、ビルド前にプロジェクトの依存関係を再インストールします。

パッケージの復元に依存する理由には、次のようなものがあります。

1. 分散型バージョン管理システム (Git など) には、リポジトリ内のすべてのファイルのすべてのバージョンの完全なコピーが含まれます。 頻繁に更新されるバイナリ ファイルは大幅に肥大化し、リポジトリを複製する時間が長くなります。
1. パッケージがリポジトリに含まれる場合、開発者は、プロジェクト内でハードコーディングされたパス名につながる、NuGet を使用してパッケージを参照するよりも、ディスク上のパッケージ コンテンツに直接、参照を追加する傾向にあります。
1. 使用中のパッケージを削除しないようにする必要があるので、未使用のパッケージ フォルダーのソリューションをクリーンにするのが難しくなります。
1. パッケージを省略して、自分が依存するその他のユーザーからのコードとパッケージの間に所有者のクリーンな境界を維持します。 多くの NuGet パッケージは、独自のソース管理リポジトリに保持されます。

パッケージの復元は NuGet を使用した既定の動作ですが、一部の手動の動作は、以下のセクションで示すように、ソース管理からパッケージ&mdash;名前は、プロジェクトの `packages` フォルダー&mdash;を省略する必要があります。

## <a name="omitting-packages-with-git"></a>Git でパッケージを省略する

ソース管理に `packages` フォルダーが含まれないようにするには、[.gitignore ファイル](https://git-scm.com/docs/gitignore)を使用します。 [Visual Studio プロジェクトの `.gitignore` のサンプル](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)を参照してください。

`.gitignore` ファイルの重要な部分は次のとおりです。

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

## <a name="omitting-packages-with-team-foundation-version-control"></a>Team Foundation バージョン管理でパッケージを省略する

> [!Note]
> ソース管理にプロジェクトを追加する*前に*、可能であればこれらの手順を実行します。 それ以外の場合は、自分のリポジトリから `packages` フォルダーを手動で削除して、続行する前にその変更をチェックインします。

選択したファイルの TFVC とのソース管理の統合を無効にするには

1. ソリューション フォルダー (`.sln` ファイルがある場所) で `.nuget` という名前のフォルダーを作成します。
    - ヒント: Windows 上のエクスプローラーでこのフォルダーを作成するには、末尾のドットを*含む* `.nuget.` という名前を使用します。

1. そのフォルダーで、`NuGet.Config` という名前のファイルを作成し、編集するために開きます。

1. [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) の設定によって Visual Studio で `packages` フォルダーのすべてをスキップするように指示している場合、少なくとも次のテキストを追加します。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. TFS 2010 以前を使用している場合は、自分のワークスペース マッピングで `packages` フォルダーをクロークします。

1. TFS 2012 以降、または Visual Studio Team Services を使用して、「[Add Files to the Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore)」 (サーバーにファイルを追加する) で説明されているように、`.tfignore` ファイルを作成します。 そのファイルには、リポジトリ レベルの `\packages` フォルダーおよび他のいくつかの中間ファイルに対する変更を明示的に無視するように、以下のコンテンツを含めます。 (末尾のドットを含む `.tfignore.` という名前を使用して、エクスプローラーでファイルを作成できますが、最初に "Hide known file extensions" (既知のファイル拡張子を非表示にする) オプションを無効にする必要がある場合があります。)

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

1. `NuGet.Config` と `.tfignore` をソース管理に追加し、自分の変更をチェックインします。
