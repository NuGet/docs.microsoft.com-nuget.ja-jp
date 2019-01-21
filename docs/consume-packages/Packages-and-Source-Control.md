---
title: NuGet パッケージとソース管理
description: バージョン管理システムとソース管理システム内で NuGet パッケージを処理する方法、git と TFVC でパッケージを省略する方法に関する考慮事項です。
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: ef4c45451cc52eb08dc627f8442c48e853d8ceaf
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324735"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>ソース管理システムで NuGet パッケージを省略する

通常、開発者はソース管理リポジトリの NuGet パッケージを省略し、代わりに[パッケージの復元](package-restore.md)に依存して、ビルド前にプロジェクトの依存関係を再インストールします。

パッケージの復元に依存する理由には、次のようなものがあります。

1. 分散型バージョン管理システム (Git など) には、リポジトリ内のすべてのファイルのすべてのバージョンの完全なコピーが含まれます。 頻繁に更新されるバイナリ ファイルは大幅に肥大化し、リポジトリを複製する時間が長くなります。
1. パッケージがリポジトリに含まれる場合、開発者は、プロジェクト内でハードコーディングされたパス名につながる、NuGet を使用してパッケージを参照するよりも、ディスク上のパッケージ コンテンツに直接、参照を追加する傾向にあります。
1. 使用中のパッケージを削除しないようにする必要があるので、未使用のパッケージ フォルダーのソリューションをクリーンにするのが難しくなります。
1. パッケージを省略して、自分が依存するその他のユーザーからのコードとパッケージの間に所有者のクリーンな境界を維持します。 多くの NuGet パッケージは、独自のソース管理リポジトリに保持されます。

パッケージの復元は NuGet と共に既定の動作ですが、ソース管理からパッケージ&mdash;つまり、プロジェクトの `packages` フォルダー&mdash;を省略するには、以下のセクションで示すように、一部手動の操作を実行する必要があります。

## <a name="omitting-packages-with-git"></a>Git でパッケージを省略する

[.gitignore ファイル](https://git-scm.com/docs/gitignore)を使用して、中でも NuGet パッケージ (`.nupkg`)、`packages` フォルダー、`project.assets.json` を省略します。 [Visual Studio プロジェクトの `.gitignore` のサンプル](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)を参照してください。

`.gitignore` ファイルの重要な部分は次のとおりです。

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

1. TFS 2012 以降、または Visual Studio Team Services を使用して、「[サーバーへのファイルの追加](/vsts/tfvc/add-files-server?view=vsts#tfignore)」で説明されているように、`.tfignore` ファイルを作成します。 そのファイルには、リポジトリ レベルの `\packages` フォルダーおよび他のいくつかの中間ファイルに対する変更を明示的に無視するように、以下のコンテンツを含めます。 (末尾のドットを含む `.tfignore.` という名前を使用して、エクスプローラーでファイルを作成できますが、最初に "Hide known file extensions" (既知のファイル拡張子を非表示にする) オプションを無効にする必要がある場合があります。)

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

1. `NuGet.Config` と `.tfignore` をソース管理に追加し、自分の変更をチェックインします。
